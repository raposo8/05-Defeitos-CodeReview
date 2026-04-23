
# 🔎 Formulário — Parte B

**Dupla:** Victor Flor 225653 e Luan Correia 228391
**Data da revisão:** 22/04/2026  

---

### Finding #1

**📍 Linha(s):** 10–13  
**🏷 Rótulo:** blocker  
**📂 Dimensão:** Segurança  
**⚠️ Severidade:** Crítica  

**🐛 Problema:**  
Construção de query SQL via concatenação de string, vulnerável a SQL Injection.

**💡 Sugestão de correção:**
```javascript
async function buscarUsuarioPorNome(nome) {
  const query = 'SELECT * FROM usuarios WHERE nome = ?';
  return db.executarQuery(query, [nome]);
}
````

**📚 Referência (opcional):** OWASP Top 10 — Injection

---

### Finding #2

**📍 Linha(s):** 28–33
**🏷 Rótulo:** blocker
**📂 Dimensão:** Erros
**⚠️ Severidade:** Alta

**🐛 Problema:**
Possível acesso a objeto `null` caso `db.buscarPorId` não encontre o usuário.

**💡 Sugestão de correção:**

```javascript
async function atualizarEmail(id, novoEmail) {
  const usuario = await db.buscarPorId('usuarios', id);

  if (!usuario) {
    throw new Error('Usuário não encontrado');
  }

  usuario.email = novoEmail;
  await db.atualizar('usuarios', id, usuario);
  return usuario;
}
```

---

### Finding #3

**📍 Linha(s):** 15–26
**🏷 Rótulo:** major
**📂 Dimensão:** Segurança
**⚠️ Severidade:** Alta

**🐛 Problema:**
Dados de entrada (`dados`) não são validados (email, tipo, senha). `TIPOS_VALIDOS` não é utilizado.

**💡 Sugestão de correção:**

```javascript
if (!TIPOS_VALIDOS.includes(dados.tipo)) {
  throw new Error('Tipo de usuário inválido');
}

if (!dados.email || !dados.email.includes('@')) {
  throw new Error('Email inválido');
}

if (!dados.senha || dados.senha.length < 6) {
  throw new Error('Senha fraca');
}
```

---

### Finding #4

**📍 Linha(s):** 35–95
**🏷 Rótulo:** major
**📂 Dimensão:** Complexidade
**⚠️ Severidade:** Alta

**🐛 Problema:**
Função `calcularLimiteEmprestimo` possui alta complexidade ciclomática e múltiplos níveis de aninhamento.

**💡 Sugestão de correção:**

```javascript
function calcularLimiteProfessor(usuario) {
  if (usuario.tempoCasaEmDias > 365) {
    if (usuario.atrasos === 0) return 20;
    if (usuario.atrasos < 3) return 15;
    return usuario.multaPendente ? 1 : 3;
  }

  if (usuario.atrasos === 0) return 10;
  if (usuario.atrasos < 3) return 7;
  return usuario.suspenso ? 0 : 2;
}
```

---

### Finding #5

**📍 Linha(s):** 35–140
**🏷 Rótulo:** major
**📂 Dimensão:** Complexidade
**⚠️ Severidade:** Média

**🐛 Problema:**
Duplicação de lógica entre `calcularLimiteEmprestimo` e `calcularLimiteComSuspensao`.

**💡 Sugestão de correção:**

```javascript
function calcularLimite(usuario, considerarSuspensao = true) {
  if (considerarSuspensao && usuario.suspenso) {
    return 0;
  }

  // reutilizar regras comuns aqui
}
```

---

### Finding #6

**📍 Linha(s):** 22
**🏷 Rótulo:** major
**📂 Dimensão:** Segurança
**⚠️ Severidade:** Média

**🐛 Problema:**
Exposição de dado sensível (email) em log.

**💡 Sugestão de correção:**

```javascript
logger.info('Usuário cadastrado com sucesso');
// ou mascarar
logger.info(`Usuario cadastrado: ${dados.email.replace(/(.{2}).+(@.+)/, '$1***$2')}`);
```

---




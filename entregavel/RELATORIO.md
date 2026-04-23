# 📦 Relatório Final

> **Atividade:** Bug Report Profissional + Code Review Guiado
> **Curso:** Qualidade de Software
> **Professor:** Prof. Claudio Nunes

---

## 👥 Identificação da dupla

| Nome completo | RA | GitHub |
|---|---|---|
| Victor Flor | 225653 | [@raposo8] |
| Luan Correia | 228391 | [@profLuanCorreia] |

**Ambiente de testes:** Edge e editor web github

---

## 📋 Sumário

- [Parte A — Bug Reports](#parte-a--bug-reports)
- [Parte B — Code Review](#parte-b--code-review)
- [Reflexão final](#-reflexão-final)
- [Declarações](#-declarações)

---

## Parte A — Bug Reports

# 🐛 Bug Reports — Parte A


**Dupla:** Victor Flor 225653 e Luan Correia 228391
**Data da exploração:** 22/04/2026
**Navegador usado:** Edge
**Sistema operacional:** Windowns 10
---

## BUG-001

**Título:** Tarefas sendo inseridas com nome em branco

**Severidade:** Baixa
**Justificativa da severidade:** O usuário não consegue identificar qual tarefa está na lista, porém, não impacta no funcionamento da aplicação

**Prioridade:** P4
**Justificativa da prioridade:** Tem impacto mínimo no funcionamento da aplicação

**Ambiente:**
- Navegador: Edge
- Sistema Operacional: Windowns 10
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Clicar no botão adicionar tarefa

**Resultado esperado:**
Validação de campo para o título da tarefa indicando erro

**Resultado obtido:**
Tarefa inserida normalmente

**Evidência:**
<img width="934" height="864" alt="image" src="https://github.com/user-attachments/assets/742b7090-7e08-4051-9ba2-1d8e4aac95c2" />

---

## BUG-002

**Título:** Não é possível filtrar as tarefas por categoria

**Severidade:** baixa
**Justificativa da severidade:** Não afeta o funcionamento principal da aplicação, pois o usuário consegue inserir as tarefas normalmente
**Prioridade:** p4
**Justificativa da prioridade:** Não afeta o funcionamento principal da aplicação

**Ambiente:**
- Navegador: Edge
- Sistema Operacional: Windowns 10
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Clicar no botão adicionar tarefa
2. Clicar na caixa filtrar

**Resultado esperado:** 
Opção para filtro de categoria disponível

**Resultado obtido:**
Apenas filtro de status atual da tarefa apresentado

**Evidência:**
<img width="956" height="973" alt="image" src="https://github.com/user-attachments/assets/42d2f995-15e8-4bd5-9f8a-0829bcacf8dc" />

---

## BUG-003

**Título:** 
Atualizar a página não persiste os dados

**Severidade:** 
Crítico
**Justificativa da severidade:**
Afeta completamente a funcionabilidade da aplicação, já que os dados não estão sendo salvos

**Prioridade:**
p1
**Justificativa da prioridade:**
Afeta completamente a funcionabilidade da aplicação.

**Ambiente:**
- Navegador: Edge
- Sistema Operacional: Windowns 10
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Clicar no botão adicionar tarefa
2. Atualizar o navegador
3.

**Resultado esperado:**
Retornar com as atividades anteriores salvas e mostrando na tela

**Resultado obtido:**
Toda a lista de tarefa estava vazia

**Evidência:**
<img width="959" height="973" alt="image" src="https://github.com/user-attachments/assets/244479e6-5e67-4639-9496-202311cda319" />

---

## ✅ Critérios de qualidade do bug report
*(Use para conferir antes de entregar)*

- [ ] Título descritivo — outra pessoa entende o problema só pelo título?
- [ ] Passos são **numerados** e **reproduzíveis** por terceiros?
- [ ] Há **pelo menos uma evidência** (screenshot, GIF ou log)?
- [ ] Severidade tem **justificativa explícita**?
- [ ] Prioridade tem **justificativa explícita**?
- [ ] Ambiente inclui **navegador + SO**?
- [ ] "Esperado vs. Obtido" deixa o gap claro?

## ✅ Checklist de qualidade dos reports

Antes de submeter, confirme em cada report:

- [ ] Título é específico e acionável (não `"Não funciona"`).
- [ ] Passos estão **numerados** e são reproduzíveis por terceiros.
- [ ] Há **pelo menos uma evidência** por report (imagem, GIF ou log).
- [ ] Severidade tem **justificativa explícita**.
- [ ] Prioridade tem **justificativa explícita**.
- [ ] Ambiente inclui **navegador + SO**.
- [ ] "Esperado × Obtido" deixa a diferença clara.
- [ ] Os 3 defeitos reportados cobrem **categorias diferentes**
      (funcional, UX, validação, persistência, etc.)

---

## Parte B — Code Review


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





## 💭 Reflexão final

> Responda em 1-2 parágrafos. Esta reflexão **é obrigatória**.

**Qual dimensão do checklist foi mais difícil aplicar? Por quê?**

Segurança. Muitos conceitos novos que eu desconhecia

**O que vocês fariam diferente se revisassem o código novamente?**

Começaria vendo secrets expostas ou sql injection

---

## 📣 Declarações


### Uso de IA como parceiro de trabalho

- [ ] Não usamos IA nesta atividade.
- [ x] Usamos IA para esclarecer conceitos teóricos.
- [ x] Usamos IA para revisar a redação dos bug reports.
- [ ] Usamos IA para discutir se um achado era ou não um defeito.
- [ ] Uso específico: [descreva]

### Declaração de autoria

Declaramos que este relatório é de autoria da dupla, que exploramos
pessoalmente a aplicação da Parte A e lemos o código da Parte B. As
findings aqui registradas representam nosso próprio julgamento
técnico.

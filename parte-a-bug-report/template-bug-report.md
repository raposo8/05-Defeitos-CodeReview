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

# **Kanban: Explicação Detalhada**

O **Kanban** é um método ágil de gestão visual de trabalho que ajuda equipes a otimizar fluxos, reduzir desperdícios e melhorar a eficiência. Surgiu na Toyota nos anos 1940 como um sistema de controle de estoque e foi adaptado para o desenvolvimento de software e outras áreas.

---

## **1. O que é Kanban?**
Kanban (看板, do japonês "cartão" ou "sinalização visual") é um **sistema puxado** (pull system) que:
- **Visualiza o trabalho** em um quadro (físico ou digital).
- **Limita o trabalho em progresso (WIP)** para evitar sobrecarga.
- **Melhora continuamente** o fluxo de trabalho com base em dados.

É usado em:
- Desenvolvimento de software
- Operações de TI
- Marketing
- Manufatura
- Qualquer processo que envolva fluxo de tarefas

---

## **2. Como Funciona o Kanban?**
O Kanban opera em **3 princípios fundamentais**:

### **📌 1. Visualização do Fluxo de Trabalho**
- O trabalho é representado em um **quadro Kanban** dividido em colunas que representam estágios do processo.
- Cada tarefa é um **cartão** (post-it ou card digital) que se move entre colunas.

**Exemplo de colunas em um Kanban simples:**
```
| A Fazer (To Do) | Em Progresso (Doing) | Feito (Done) |
```

### **📌 2. Limitação do Trabalho em Progresso (WIP)**
- Cada coluna tem um **limite máximo de tarefas** que podem estar nela ao mesmo tempo.
- Isso evita gargalos e sobrecarga da equipe.
  
**Exemplo:**
- "Em Progresso" pode ter um **WIP limitado a 3 tarefas**.
- Se já houver 3 cartões lá, a equipe **não pode puxar** mais trabalho até liberar espaço.

### **📌 3. Melhoria Contínua (Kaizen)**
- A equipe analisa métricas (como **lead time** e **throughput**) para otimizar o processo.
- Reuniões de **retrospectiva** ajudam a identificar melhorias.

---

## **3. Elementos de um Quadro Kanban**
| Componente | Descrição | Exemplo |
|------------|-----------|---------|
| **Cartões (Cards)** | Representam tarefas individuais. | "Corrigir bug no login" |
| **Colunas (Swimlanes)** | Fases do fluxo de trabalho. | "A Fazer", "Em Teste", "Concluído" |
| **Limites de WIP** | Número máximo de tarefas por coluna. | Máx. 3 em "Em Progresso" |
| **Ponto de Compromisso** | Quando uma tarefa entra no fluxo. | Reunião de planejamento |
| **Ponto de Entrega** | Quando uma tarefa é considerada pronta. | Merge no repositório |

---

## **4. Benefícios do Kanban**
✅ **Mais transparência** (todos veem o status do trabalho).  
✅ **Menos desperdício** (evita multitarefa excessiva).  
✅ **Melhor fluxo** (identifica gargalos rapidamente).  
✅ **Adaptável** (não exige mudanças bruscas no processo atual).  
✅ **Baseado em dados** (usa métricas para decisões).  

---

## **5. Kanban vs. Scrum**
| **Kanban** | **Scrum** |
|------------|----------|
| Fluxo contínuo | Trabalha em **Sprints** (ciclos fixos) |
| Sem papéis rígidos | Tem **Scrum Master** e **Product Owner** |
| Limita WIP | Planejamento baseado em **Sprint Backlog** |
| Mais flexível | Estrutura mais definida |

→ **Kanban é melhor** para times com demandas imprevisíveis.  
→ **Scrum é melhor** para projetos com entregas planejadas.

---

## **6. Ferramentas Kanban Populares**
- **Jira** (para times de desenvolvimento)
- **Trello** (simples e visual)
- **Asana** (para equipes multidisciplinares)
- **Kanbanize** (focado em métricas avançadas)

---

## **7. Como Implementar Kanban?**
1. **Mapeie seu fluxo atual** (identifique etapas).  
2. **Crie um quadro Kanban** (físico ou digital).  
3. **Defina limites de WIP** (ex.: 2 tarefas por pessoa).  
4. **Monitore métricas** (ex.: tempo médio por tarefa).  
5. **Ajuste continuamente** (remova obstáculos).  

---

### **📊 Exemplo Prático: Quadro Kanban de Desenvolvimento**
```
| A Fazer (WIP: 5) | Desenvolvimento (WIP: 3) | Testes (WIP: 2) | Pronto para Deploy |
|-------------------|--------------------------|-----------------|--------------------|
| [ ] Nova feature  | [ ] Correção de bug      | [ ] Teste A/B   | [✔] Página de login|
| [ ] Atualizar API |                          |                 |                    |
```

---

## **Conclusão**
O Kanban é **simples, mas poderoso**:
- 🎯 **Foco na visualização** do trabalho.
- 🛑 **Evita sobrecarga** com limites de WIP.
- 🔄 **Melhora continuamente** o fluxo.

É ideal para equipes que querem **mais flexibilidade** do que o Scrum oferece, mantendo a produtividade alta. 🚀

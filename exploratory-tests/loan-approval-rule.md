# Teste Exploratório — Regra de Aprovação de Empréstimo

## 1. Objetivo e Abordagem
Mapear o comportamento do motor de regras de crédito sob a perspectiva de Black-Box Testing (Caixa-Preta), devido à ausência de documentação funcional prévia para a funcionalidade de solicitação de empréstimo.

## 2. Estratégia de Engenharia Reversa
Foi aplicada a técnica de **Análise do Valor Limite (Boundary Value Testing)** combinada com **Particionamento de Equivalência (Equivalence Partitioning)** para identificar a correlação exata entre o *Valor Solicitado* e o *Valor de Entrada*.

### Matriz de Testes e Fronteiras Identificadas
* **Partição Inválida:** Entrada < 50% do valor solicitado -> Resultado: Reprovado.
* **Fronteira Inferior (Limite):** Entrada exatamente 49.92% (R$ 649,00 de R$ 1300,00) -> Resultado: Reprovado.
* **Fronteira Superior (Limite):** Entrada exatamente 50.00% (R$ 650,00 de R$ 1300,00) -> Resultado: Aprovado.
* **Partição Válida:** Entrada >= 50% do valor solicitado -> Resultado: Aprovado.

| ID | Cenário | Valor Solicitado | Valor de Entrada | Percentual | Resultado Obtido | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| T01 | Valor Irrisório | R$ 1.300,00 | R$ 10,00 | 0,76% | Reprovado (Msg Padrão) | Passou |
| T02 | Entrada Baixa | R$ 1.300,00 | R$ 100,00 | 7,69% | Reprovado (Msg Padrão) | Passou |
| T03 | Próximo ao Limite | R$ 1.300,00 | R$ 600,00 | 46,15% | Reprovado (Msg Padrão) | Passou |
| T04 | Fronteira Negativa | R$ 1.300,00 | R$ 649,00 | 49,92% | Reprovado (Msg Padrão) | Passou |
| T05 | Fronteira Positiva | R$ 1.300,00 | R$ 650,00 | 50,00% | Aprovado (Msg Padrão) | Passou |
| T06 | Valor Redondo | R$ 1.000,00 | R$ 500,00 | 50,00% | Aprovado (Msg Padrão) | Passou |

## 3. Regra de Negócio Mapeada (Grooming Asset)
> **RN01 - Percentual Mínimo de Entrada:** O sistema possui uma trava de segurança onde a operação de empréstimo só é elegível para aprovação se o valor dado como entrada for matematicamente maior ou igual a 50% do valor total solicitado pelo cliente.

## 4. Ocorrências e Débitos Técnicos
* **Comportamento do Sistema:** O motor de regras respondeu de forma consistente e estável em todas as fronteiras testadas.
* **UX/Divergência de Negócio:** Identificada ambiguidade na resposta de erro (Mensagem genérica). Foi gerada a proposta de melhoria arquitetural no report `IMP001`.

---

## Traceability Matrix

Este teste exploratório estabelece a origem da regra de negócio RN01 e sua validação prática através de execução de cenários de fronteira.

- **Requirement discovered:** RN01 (Minimum down payment rule - 50%)
- **Validated by test cases:** T01, T02, T03, T04, T05, T06
- **Linked improvement:** IMP001 (UX clarity and error message transparency) | IMP002 (Input validation and submission handling)

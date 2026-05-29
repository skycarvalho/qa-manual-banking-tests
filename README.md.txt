# QA Manual Testing — Banking System (ParaBank)

## Visão Geral

Este projeto apresenta uma análise de qualidade realizada no módulo de **solicitação de empréstimo** do sistema bancário simulado (ParaBank), com foco em validação de regras implícitas de negócio, testes exploratórios estruturados e análise de resiliência do sistema sob diferentes condições de entrada.

O objetivo principal foi identificar critérios de aprovação de empréstimo não documentados e validar a consistência do comportamento do sistema por meio de testes de fronteira e exploração guiada por hipótese.

**Sistema analisado:** https://parabank.parasoft.com/parabank/index.htm

---

## Status Atual do Ciclo de Testes

* **Status:** **BLOQUEADO (Impedimento Técnico)**
* **Motivo:** O ambiente do ParaBank apresentou instabilidade crítica no serviço de Autenticação (`Login`), retornando erro de servidor (`HTTP 500 / 504`) e impedindo o acesso ao Dashboard interno para a coleta final de evidências visuais.
* **Ação QA:** Os cenários de testes e as regras de negócio foram mapeados integralmente via *Shift-Left*. O bug de infraestrutura foi devidamente reportado na pasta `bug-reports/BUG001_login_instability.md` para atuação do time de DevOps/Desenvolvimento.

---

## Objetivos da Análise

- Identificar regras de negócio não explicitadas na documentação do sistema através de Engenharia Reversa.
- Validar comportamento e resiliência da funcionalidade de empréstimo.
- Realizar testes exploratórios estruturados com foco em mitigação de riscos.
- Aplicar análise de valores de fronteira (*Boundary Testing*) e Particionamento de Equivalência.
- Avaliar a consistência de fluxos de exceção e comportamento da interface.
- Identificar oportunidades de melhoria de UX, clareza e comunicação do sistema.

---

## Funcionalidade Executada neste Ciclo

* Solicitação de Empréstimo (Exploratory Testing & Boundary Validation)
* Análise Crítica de Autenticação (Mapeamento de Instabilidade de Ambiente)

---

## Destaques do Projeto

### Descoberta de Regra de Negócio via Teste Exploratório
Diante da ausência de documentação funcional sobre os critérios de aprovação, foi realizada uma abordagem exploratória incremental. Através de testes de valor limite, foi deduzida a **RN01**: o sistema exige matematicamente uma entrada de, no mínimo, 50% do valor solicitado para aprovar o crédito.

### Abordagem Consultiva (Visão de Produto)
Além da validação de caixa-preta, foi documentada uma proposta técnica de melhoria arquitetural e de experiência do usuário (`IMP001`), visando reduzir o abandono de funil gerado por mensagens ambíguas do sistema.

---

## Técnicas de Teste Aplicadas

* Testes Manuais Funcionais (System Testing)
* Testes Exploratórios Baseados em Hipóteses
* Análise do Valor Limite (Boundary Value Testing)
* Particionamento de Equivalência (Equivalence Partitioning)
* Testes Negativos e de Sanitização de Campos
* Análise de Erros de Integração / API (Inspeção de HTTP Status)

---

## Estrutura do Projeto

```txt
qa-manual-banking-tests/
├── bug-reports/
│   └── BUG001_login_instability.md      # Relato técnico do bloqueio crítico no Login (Erro 500)
├── evidences/                           # Capturas de tela (prints) das falhas e logs do DevTools
├── exploratory-tests/
│   └── loan-approval-rule.md            # Descoberta da RN01 via engenharia reversa e testes exploratórios
├── improvements/
│   ├── IMP001.md                        # Melhoria de UX e clareza nas mensagens de reprovação de empréstimo
│   └── IMP002.md                        # Validações preventivas de inputs e tratamento de erros de submissão
├── test-cases/
│   └── banking-functional-tests.md      # Casos de teste funcionais, negativos e de fronteira
└── README.md                            # Visão geral, rastreabilidade e matriz principal do projeto

```

## Ferramentas Utilizadas
* Testes Manuais de Caixa-Preta

* Browser DevTools (F12): Utilizado para inspeção de requisições de rede (Network tab) e triagem de erros de infraestrutura no login.

* GitHub & Markdown: Para documentação técnica e rastreabilidade.
---


## Traceability Matrix

Este projeto foi estruturado com rastreabilidade entre requisito, testes, comportamento observado e melhoria proposta.

| Requisito | Casos de Teste | Bug Relacionado | Melhoria |
|-----------|----------------|------------------|----------|
| RN01 - Entrada mínima de 50% | CT001, CT002, CT003, CT004 | BUG001 (ambiente bloqueado) | IMP001, IMP002 | 

---

## Sobre

Projeto desenvolvido por **Ana Carolina de Carvalho** com foco em testes manuais, garantia de qualidade na origem e validação de sistemas críticos de negócio.

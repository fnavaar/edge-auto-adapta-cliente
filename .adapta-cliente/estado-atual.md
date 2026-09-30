# Estado atual — EDGE AUTO (30/09/2026)

**Fase**: 1 (Módulo 1 — Extração e Conciliação) · **Execução**: 0/8 tasks · **Champion**: Bruno (CEO)

## Onde paramos

Workspace operacional entregue com SPECs e tasks prontas. **Nenhuma task executada ainda.** A primeira é "Cadastrar clientes, contratos e plantas com regras e tetos configuráveis" (prazo 05/10/2026).

## O que acontece em cada task

1. O agente lê a SPEC correspondente em `04_fase-atual/specs/`.
2. Executa em fixture sintético (nada de dado real até a política de dados).
3. Faz as perguntas de insumo da task **junto com o andamento** (lista abaixo).
4. Roda as provas (TDD) e pede **teste humano**. Só depois disso a task vira `[x]`.

## Insumos pedidos por task (respondam no próprio card)

| Task | Pergunta embutida | Pessoa |
|---|---|---|
| 1 | Aceite de que o ciclo 1 é conciliação + cobrança (recrutamento/IA fica em backlog)? | Bruno/Ricardo |
| 1 | Cláusula/planilha contratual com o teto de horas por planta | Renata |
| 1 | Qual entidade emprega e qual fatura cada contrato (EEP × EDGE) | Bruno/Financeiro |
| 1 | Champion detalhado + matriz de papéis (RACI) | Liderança |
| 3 | Resposta da API do Marque Ponto + formato de saída | Lucas/consultoria |
| 4 | Cliente piloto + planilha modelo que ele envia | Operação |
| 5 | 1–2 vídeos curtos dos processos (conciliação VW, fechamento de folha) | Meire/Renata |
| 7 | Matriz de alçadas + contatos/templates de cobrança aprovados | Meire/Renata |
| 8 | Baseline de 3 meses (tempo de conciliação; dias envio→aprovação; aprovação→pagamento) | Renata/Meire |

## Regras em vigor

- Dado real bloqueado até a política de dados (fixtures até lá).
- Fail-closed de teto e de layout de importação.
- Decisão humana em: ajuste de ponto, divergência, liberação, NFS-e, call off.
- Cobrança automática nunca dispara sem confirmação do pagamento anterior.

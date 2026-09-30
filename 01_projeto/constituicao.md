# Constituição do projeto — EDGE AUTO

Decisões acordadas que governam o projeto. Mudança aqui só por conversa explícita entre as partes.

## Ciclo 1 — o que estamos construindo

- **Núcleo do ciclo**: conciliação de ponto + cobrança (medição mensal). Recrutamento/IA, catracas/exames e DRE de contratos ficam em **backlog datado** para ciclos futuros.
- **Prioridade**: Módulo 1 (extração e conciliação) primeiro; Módulo 2 (faturamento e cobrança) em seguida.

## Métrica de sucesso

- Tempo de conciliação por colaborador/competência + dias envio→aprovação + dias aprovação→pagamento.
- Baseline coletado no início (histórico de 3 meses junto com Financeiro/RH); **meta numérica só depois de medido**.

## Regras decididas

1. Teto de horas é **configurável por cliente/projeto/planta/vigência** — nenhum valor fixo por padrão; enquanto não provado por contrato, o cálculo fica "em conferência" (fail-closed).
2. A conciliação é **parametrizável por cliente** (upload da planilha do cliente com contrato de campo a campo), com um cliente piloto definido com a operação.
3. Extração do Marque Ponto: API se confirmada; senão, importação manual com a mesma trilha — nada de prometer integração antes da prova.
4. Política de dados + matriz de alçadas + contatos/templates de cobrança aprovados **antes** de dado real e disparos.
5. Ciclo de cobrança automática **nunca** dispara novo e-mail sem confirmação do pagamento anterior.
6. Champion do projeto: **Bruno (CEO)**; RACI detalhado a confirmar com a operação (RH/Medição, Financeiro, Interface VW, liderança).

## Fora do ciclo 1

- Recrutamento com IA, catracas/exames, DRE de contratos (backlog).
- WhatsApp como canal de cobrança; emissão automática de NFS-e; decisão automática de ponto/call off.

# AP-2026-10-06-1728 — Compatibilidade entre fixtures e validadores de domínio

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: 1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5 · SPEC-1-001
- Sinal: fixtures seed e validadores server-side divergiram: nomes/flags existentes não satisfaziam o prefixo de dados sintéticos e `isSynthetic` exigidos pelo fluxo.
- Evidência: migration 0004 aplicada criou as coleções e seed inicial; primeiro QA falhou em hook, depois migration 0005 normalizou fixtures sem trocar IDs de clientes; migration 0005 aparece aplicada; QA 0.0.3 passou.
- Regra reutilizável: defina um único contrato de fixture (prefixo, flags sintéticas, campos obrigatórios e dependências) compartilhado entre seed, migration corretiva, validação server-side e formulário; valide o seed contra o mesmo validador antes de declarar task pronta. Migrações aplicadas são imutáveis; corrija por nova migration idempotente.
- Quando aplicar: ao implementar fluxos com fixtures que passarão por validação de domínio ou integração entre migrations e hooks.
- Quando não aplicar: dados produtivos após aprovação de política; não rotular registros reais como fixtures.
- Confiança: alta — a inconsistência foi observada no código, reproduziu falha de QA/integração e a correção passou pelo pipeline.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.

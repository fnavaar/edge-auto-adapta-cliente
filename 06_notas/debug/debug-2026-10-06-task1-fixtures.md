# Debug Summary — 2026-10-06 — Task 1

**Task:** 1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5 — SPEC-1-001.

- **Problema observado:** primeiro QA da versão 0.0.2 falhou em staticAnalysis e hook integration por marcador de patch residual em `pocketbase/hooks/registry_contracts_create.js`. A revisão também detectou incompatibilidade entre os nomes/flags seed da migration 0004 e os nomes/flags exigidos pelos validadores de fixture.
- **Causa raiz confirmada:** patch SEARCH/REPLACE mal aplicado deixou marcadores textuais no hook; separadamente, os fixtures seed não foram normalizados para o contrato do validador (`Fixture - `, `isSynthetic`), embora a migration 0004 já estivesse aplicada.
- **Correção:** substituição completa e limpa do hook; migration aditiva/idempotente `0005_normalize_registry_fixtures.js` renomeia fixtures, marca clientes/contratos/regras como sintéticos, preserva IDs de clientes usados por cobranças, acrescenta `fixture_normalized` ao enum de auditoria e registra before/after. A migration 0004 aplicada não foi alterada.
- **Verificação:** QA Skip v0.0.3 (`3219216`) passou setup, staticAnalysis, build, integrations e test. A migration 0005 consta como aplicada; collections e schema retornados pelo Skip confirmam campos e regras. `npm test` é placeholder e não constitui cobertura de teste. Preview exige login; não havia credencial de teste confirmada, portanto não fiz login nem criei registros por UI.
- **Publicação:** não realizada. Projeto segue `isPublished: false`.
- **Configuração pendente:** `.skip.config.json` permaneceu como a única mudança pendente relatada pelo Skip; não alterei seu conteúdo manualmente. O pipeline atual gerou versão 0.0.3 e atualizou `deployment.lastDevBuildRef` para o build atual.
- **Gate:** aguardando teste humano de Bruno no preview; a task não está concluída.

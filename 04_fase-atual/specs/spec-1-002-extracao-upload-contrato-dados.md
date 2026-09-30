# SPEC-1-002 — Extração de ponto, upload da planilha do cliente e contrato de semântica de dados

- **Fase**: F1 · **Capacidades**: C3, C4 · **Risco**: obrigatório (API externa, input externo, dado pessoal)
- **Ambiente**: Skip (GoSkip + SkipCloud) — regra geral do consultor (22/09/2026)
- **Degrau da solução**: alimenta os dois lados da comparação (ponto × planilha do cliente) com integridade; elimina a transcrição manual de espelhos PDF e previne o maior risco técnico do Módulo 1 — a quebra por semântica divergente (sem parametrização de semelhança automática).

## Contexto
- **Estado atual**: RH consulta colaborador por colaborador no Marque Ponto/MarqPonto, gera espelho PDF e transcreve em planilha; financeiro recebe reportes por e-mail; planilha do cliente chega por e-mail em formato livre.
- **Estado desejado**: entrada de ponto por API/export **se provada** (I-03), senão importação manual/lista controlada com a mesma trilha; upload da planilha do cliente validado contra **contrato de semântica de dados** por cliente (mapeamento campo a campo, fail-closed).

## Atores e permissões
- RH/Medição: executa importações/upload; não edita dado importado (só versão nova com motivo).
- Financeiro: consulta e valida.
- Somente operadores autenticados importam; toda importação registra operador.

## Dados
Fonte (API/manual/upload), arquivo (hash, data, operador), linhas importadas (colaborador, H.T., H.E.1, H.E.2, noturno, sáb/dom/fer, HT CONTRATO), campos da planilha do cliente, contrato de semântica (mapa campo→campo por cliente, formatos, unidades).

## Contrato de integração (Marque Ponto/MarqPonto)
- API/export em lote **somente após prova real** (I-03: disponibilidade + formato de saída). Nenhum endpoint, campo ou credencial é presumido.
- Sem prova: modo manual (importação de arquivo/lista controlada) com origem "manual" e mesma auditoria. A superfície nunca alega "integração ativa" sem prova.

## Regras
1. **Fail-closed de layout**: arquivo com layout/colunas divergentes do contrato é rejeitado com relatório de divergência — nada é preenchido por inferência ou semelhança.
2. **Idempotência**: reimportar o mesmo arquivo (hash idêntico) não duplica registros.
3. **Fidelidade**: valores, unidades, casas decimais e operadores são preservados como recebidos; normalização exige regra homologada no contrato.
4. Até I-07 (planilha modelo), a comparação usa fixture sintético; variante não-modelo é sinalizada, não convertida.
5. Importação proibida com dado real antes de I-06 (política) — recusa explícita.

## Fluxo e passos
1. Registrar contrato de semântica do cliente (mapa campo→campo, formatos).
2. Importar ponto (API se provada; senão manual) → validação → carga.
3. Upload da planilha do cliente → validação de layout → carga.
4. Gerar registro de origem (fonte, hash, data, operador) para cada carga.

## Exceções e rollback
- Layout divergente → rejeição + relatório; nada carrega.
- Upload repetido → idempotente, sem duplicidade.
- Carga corrompida → reversão por lote (registro inativado com motivo), nunca edição silenciosa.

## Critérios de aceite (binários)
- **CA-1-006**: entrada de ponto via API/export só ocorre com I-03 provado; caso contrário o modo manual é usado e registra origem "manual" com a mesma trilha de auditoria.
- **CA-1-007**: upload da planilha do cliente é validado contra o contrato de semântica (campo→campo); layout divergente é rejeitado com relatório de divergência e zero linhas carregadas.
- **CA-1-008**: reimportação do mesmo arquivo (hash idêntico) não gera duplicidade (teste com 2 cargas idênticas).
- **CA-1-009**: valores, unidades, casas decimais e operadores são preservados byte a byte do arquivo de origem; nenhum valor é normalizado silenciosamente.
- **CA-1-010**: planilha modelo (I-07) aceita; variante de layout não-modelo sinalizada como "fora do contrato" e não convertida; sem I-07, a validação roda em fixture sintético.
- **CA-1-011**: toda importação gera registro auditável (fonte, arquivo/hash, data, operador, total de linhas aceitas/rejeitadas).

## TDD da SPEC
- **RED**: cenário "upload de planilha com coluna extra/renomeada" → hoje o processo humano aceita e transcreve à mão (sem validação). Prova: fixture de layout divergente carregada sem recusa no fluxo atual documentado.
- **GREEN**: CA-1-006..011 em fixtures sintéticos (planilha modelo 20 linhas + variante divergente + arquivo repetido); prova: recusa com relatório (007), idempotência (008), fidelidade byte a byte (009), registro de origem (011).
- **REGRESSÃO**: cargas sucessivas de meses distintos não se misturam; rollback de lote preserva trilha; sem I-03, nenhuma superfície exibe "API ativa".

## Instruções para o Ethos
- Superfícies: tela/rota de importação de ponto; upload de planilha do cliente; editor de contrato de semântica; relatório de divergência de layout; trilha de importações.
- Fixtures sintéticos: arquivo de ponto modelo, planilha modelo do cliente, variante divergente, duplicado idêntico.
- Insumos embutidos na task: I-03 (API do Marque Ponto — Lucas Machado, "API disponível? formato de saída?"), I-07 (cliente piloto + planilha modelo — Navaar/Lucas com o cliente).
- **Ponto de parada**: se I-03 for negativa, F1 inteira opera no modo manual (previsto no escopo; fornecedor alternativo vira urgente e vai ao consultor). Se I-07 não vier, contrato de semântica fica com o fixture e a comparação real espera. Nunca presumir endpoint, campo ou formato.

## Checklist de aceite
- [ ] CA-1-006..011 provados em fixture
- [ ] Prova negativa de fail-closed registrada
- [ ] Zero "integração ativa" sem I-03
- [ ] Teste humano do RH/Medição registrado

## Tasks vinculadas
| Task (fase.md) | Critérios | Leva |
|---|---|---|
| Importar os dados de ponto com registro de origem e sem duplicidade | CA-1-006/008/009/011 | 3 |
| Receber a planilha do cliente validada pelo contrato de semântica | CA-1-007/010 | 3 |

## Emendas
(nenhuma)

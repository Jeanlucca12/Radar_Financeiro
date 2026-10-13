# Metodologia — Radar Financeiro

## 1. Objetivo

O **Radar Financeiro** é um relatório de Business Intelligence desenvolvido no Power BI para apresentar, em uma visão executiva, variações de índices de bolsas globais, moedas, Bitcoin e cotações de Bitcoin por corretora. O projeto também evidencia a qualidade dos dados utilizados.

## 2. Fonte e escopo

- **Fonte declarada:** API HG Brasil Finance, com resposta em JSON.
- **Ferramentas:** Power BI Desktop e Power Query (linguagem M).
- **Recorte:** fotografia dos dados disponibilizados pela API no momento da consulta, com variações informadas em relação à última hora útil anterior.
- **Histórico:** o projeto, na versão descrita, não armazena séries históricas.

A documentação da API, as condições de uso e eventuais limites de requisição devem ser consultados no provedor. A atualização depende da disponibilidade do serviço e de credenciais válidas, quando exigidas.

## 3. Composição da amostra

| Grupo | Quantidade de registros |
|---|---:|
| Moedas e Bitcoin | 9 |
| Índices de bolsas globais | 6 |
| Bitcoin por corretora | 4 |
| **Total** | **19** |

Os quantitativos correspondem ao retrato descrito no projeto e podem variar em novas consultas.

## 4. Fluxo de processamento

1. **Extração:** consulta à API REST da HG Brasil Finance e leitura da resposta JSON no Power Query.
2. **Estruturação:** expansão dos objetos e conversão para uma estrutura tabular com campos de identificação, grupo, valor e variação, conforme disponíveis.
3. **Padronização:** definição de tipos de dados, tratamento de valores nulos e uniformização de unidades e percentuais.
4. **Validação:** aplicação de regras de qualidade, incluindo verificação de inconsistências relacionadas a spread.
5. **Apresentação:** construção de gráficos comparativos e indicador de qualidade no Power BI.

> **Reprodutibilidade:** a lógica exata das consultas, os nomes das colunas e os critérios de spread devem ser verificados no código M efetivamente utilizado. Este documento não pressupõe fórmulas que ainda não foram fornecidas.

## 5. Regras de qualidade dos dados

O relatório classifica registros em categorias de qualidade, incluindo **OK** e **Revisar spread**. Na amostra apresentada:

| Classificação | Registros | Participação |
|---|---:|---:|
| OK | 18 | 94,74% |
| Revisar spread | 1 | 5,26% |
| **Total** | **19** | **100%** |

A identificação de um registro para revisão **não comprova erro na fonte**: indica uma condição que merece investigação antes de interpretar ou divulgar o indicador. Para auditoria completa, documentar no futuro o campo analisado, a fórmula, o limiar e o ativo/corretora sinalizado.

## 6. Indicadores e visuais

- **Bolsas globais:** variação percentual de seis índices, exibida em barras horizontais.
- **Moedas e BTC:** comparação das variações percentuais de nove registros.
- **Bitcoin por corretora:** comparação das variações de quatro corretoras.
- **Qualidade dos dados:** distribuição dos 19 registros por classificação de qualidade.

As visualizações representam **variações percentuais**, e não o valor monetário absoluto dos ativos. Os rótulos e as unidades devem ser mantidos explícitos para evitar interpretações incorretas.

## 7. Limitações e cuidados de interpretação

- Os dados são um **retrato pontual**, não uma análise histórica de tendências.
- O intervalo de comparação é o informado pela fonte: **última hora útil anterior**.
- Horários, fusos, indisponibilidades de mercado e frequências de atualização podem diferir entre ativos.
- Variações percentuais de ativos diferentes não equivalem a retornos diretamente comparáveis em todas as condições.
- Um registro sinalizado exige verificação adicional; não deve ser automaticamente excluído ou corrigido sem evidência.
- O conteúdo é informativo e educacional, **não constitui recomendação de investimento**.

## 8. Segurança e publicação

- **Não publicar** chaves de API, tokens, URLs com credenciais, arquivos `.env` ou capturas que exponham segredos.
- Verificar também as configurações e consultas dentro do arquivo `.pbix` antes de disponibilizá-lo publicamente.
- Manter no repositório apenas dados e artefatos cuja divulgação seja permitida pelos termos da fonte.
- O `.gitignore` evita novos arquivos locais indesejados, mas **não remove segredos já versionados**.

## 9. Melhorias futuras

- Registrar data/hora de coleta e fuso horário no relatório.
- Persistir snapshots para construir histórico de indicadores.
- Detalhar a regra de spread e criar uma tabela de exceções.
- Adicionar testes de qualidade e documentação do esquema retornado pela API.
- Automatizar a atualização de forma compatível com o serviço e seu plano de uso.

---

*Documento elaborado com base no resumo técnico e na captura do dashboard fornecidos para o projeto Radar Financeiro.*

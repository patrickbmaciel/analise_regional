# Tarefas do projeto

[x] identifica entrega verificada. A metodologia está em [SPEC.md](SPEC.md), os padrões em [AGENTS.md](AGENTS.md) e a execução no [README](../README.md).

## 0. Alinhamento e documentação

- [x] Consolidar a arquitetura em dois notebooks e distinguir núcleo e extensões.
- [x] Ler a proposta, os slides, os scripts das aulas e os dicionários; preservar os materiais.
- [x] Usar o Python 3.14.3 existente, sem instalar pacotes, criar ambientes ou registrar kernels.
- [x] Alinhar a simplificação: sem funções próprias, com laços simples e redução de tabelas técnicas auxiliares.

## 1. Conferência do ambiente

- [x] Verificar pacotes e APIs na versão instalada.
- [x] Executar em kernels limpos e independentes.
- [x] Eliminar exportações redundantes de ambiente/assinaturas; manter as versões informadas nos notebooks.

## 2. Auditoria dos inputs

- [x] Registrar fonte e hashes dos 21 inputs; aquisição local de data desconhecida.
- [x] Conferir 570 códigos únicos, nomes e correspondência entre formatos.
- [x] Ler o DBF em UTF-8 e verificar os atributos necessários.
- [x] Auditar valores ausentes, inválidos, escalas, denominadores e população positiva.
- [x] Reparar os sete casos autorizados somente na cópia tratada, sem mudar a Queen.
- [x] Conferir geometrias finais e equivalência métrica ao Shapefile.
- [x] Documentar conceito, temporalidade e unidade inferida da altitude.

Evidências: procedencia_inputs.csv, auditoria_dados.csv, reparos_geometrias.csv e verificações nas células do notebook 1.

## 3. Notebook 1: tratamento e exploração

- [x] Resolver a raiz e ler os inputs sem caminhos pessoais.
- [x] Construir diferenças em p.p., log da população, regimes e indicadores de amostra.
- [x] Produzir descritivas, mapas, distribuições, grafos e histogramas dos pesos.
- [x] Construir Queen e KNN-5, com IDs, diagonal, somas, ilhas, componentes e assimetria conferidos.
- [x] Calcular Moran global/local com 999 permutações e semente 42; apresentar diagramas e LISA.
- [x] Colocar cada figura em célula própria, seguida de interpretação em Markdown.
- [x] Exportar e reabrir o GeoPackage e o dicionário; preservar os inputs.

Evidências: notebook 1 executado; base/dicionário em data/processed/; oito CSVs e onze figuras de exploração.

## 4. Notebook 2: seleção e estimação

- [x] Ler a base com kernel independente e reconstruir W.
- [x] Estimar os MQO e apresentar coeficientes e diagnósticos.
- [x] Começar STGE-Pre pelo LM-WX e registrar as três trajetórias.
- [x] Estimar SDM por MQ2E White e SEM por GMM heterocedástico para comparar as duas especificações de pobreza extrema com Queen.
- [x] Verificar identificação/relevância dos instrumentos de Wy.
- [x] Registrar AK, fator comum, inadmissibilidade e limites dos diagnósticos pós-GMM.
- [x] Calcular impactos completos com IC delta e covariâncias robustas.
- [x] Interpretar H1–H3 com linguagem associativa.

Evidências: coeficientes_mqo.csv, diagnosticos_mqo.csv, trajetoria_stge.csv, coeficientes_modelos.csv, instrumentos_wy.csv, impactos_modelos.csv, diagnosticos_modelos.csv e residuos_modelos.csv.

## 5. Robustezes

- [x] Repetir seleção e estimação para extrema/KNN-5 e total/Queen.
- [x] Substituir também a condição inicial por ppov_10 no desfecho alternativo.
- [x] Conferir amostra idêntica de 570 municípios nas três análises.
- [x] Consolidar a comparação de especificações, impactos, IC e limitações.
- [x] Preservar o resultado adverso KNN: rho=1,2758, sem impactos calculáveis.

Evidência: comparacao_robustezes.csv e interpretação imediatamente após a figura comparativa.

## 6. Validação e apresentação do núcleo

- [x] Executar ambos os notebooks integralmente, na ordem, em kernels independentes.
- [x] Conferir raiz/src, alinhamento dos IDs e identidade dos impactos.
- [x] Preservar os 21 inputs e a amostra de 570 municípios.
- [x] Revisar explicações, comentários, figuras e interpretações.
- [x] Comparar resultados anteriores/novos com tolerância de 1e-9.
- [x] Atualizar README, SPEC, AGENTS e este checklist.

As verificações essenciais ficam próximas dos procedimentos. Não são criados CSVs para cada asserção, manifesto ou cenário técnico de validação.

## 7. Extensões

- [x] Preparar grupos de 348 e 222 municípios pelo corte de 50%.
- [x] Estimar regimes por interações, com W completa e parâmetro espacial comum.
- [x] Aplicar Wald/Chow conjunto e contraste específico da pobreza inicial.
- [x] Comparar desvio-padrão e IQR na mesma amostra para sigma-convergência.
- [x] Auditar os candidatos de 2000 e verificar relevância.
- [x] Concluir a avaliação de exclusão: insuficiente para justificar segunda etapa IV.
- [x] Registrar que a segunda etapa não foi executada, sem declarar estimativa IV válida.

Evidências: regimes_h4.csv, coeficientes_regimes.csv, sigma_convergencia.csv, viabilidade_instrumentos_2000.csv, relevancia_instrumentos_2000.csv e a linha de regimes em instrumentos_wy.csv.

## 8. Revisão didática solicitada

- [x] Remover as 19 funções próprias e as três expressões lambda.
- [x] Usar código sequencial e chamadas diretas das bibliotecas.
- [x] Reduzir duplicações, consolidando as exportações de 55 para 22 CSVs.
- [x] Explicar o procedimento antes de cada célula de código.
- [x] Acrescentar comentários nos blocos de código.
- [x] Manter as 17 figuras, cada qual seguida imediatamente de interpretação textual.
- [x] Preservar numericamente coeficientes, impactos/IC, diagnósticos, Moran/LISA, resíduos e extensões.

## 9. Revisão didática anterior e README de pesquisa

- [x] Reaproveitar a preparação dos mapas e retirar o laço de uma iteração na verificação de instrumentos por regimes.
- [x] Ampliar o Markdown antes das 51 células de código e depois das 17 plotagens.
- [x] Verificar comentários em gerúndio e sem ponto final e ausência de funções próprias.
- [x] Apresentar SEM e SDM lado a lado para pobreza extrema com Queen, com os limites dos respectivos diagnósticos.
- [x] Organizar o README em Introdução, Metodologia, Resultados e Considerações, com duas figuras e síntese por hipótese.
- [x] Executar os notebooks em ordem com kernels independentes do Python 3.14.3 e validar links e imagens do README.
- [x] Conferir a equivalência das 22 tabelas a tolerância de 1e-9, o GeoPackage com 570 municípios, as 17 figuras em 300 dpi e os hashes dos 21 arquivos de origem.

A validação preservou os resultados e seus limites, incluindo o AK adverso do SDM extrema/Queen, a tentativa KNN inadmissível, a avaliação descritiva após GMM e a insuficiência de exclusão instrumental.

## 10. Blocos explícitos e resultados no console

- [x] Escrever modelos, diagnósticos, desfechos, impactos e figuras em blocos explícitos.
- [x] Retirar for, if, compreensões e expressões condicionais dos blocos analíticos.
- [x] Reservar o controle de fluxo à localização da raiz e às verificações técnicas de integridade.
- [x] Apresentar modelos por print(modelo.summary) e as demais estatísticas por impressões identificadas.
- [x] Preservar os 22 CSVs e usar DataFrames no tratamento e na exportação.
- [x] Inserir interpretação após os resultados analíticos, além da leitura das 17 figuras.
- [x] Manter comentários em gerúndio e sem ponto final.
- [x] Ampliar a discussão de H1–H4, robustezes, dispersão e identificação no README, com apresentação em prosa.
- [x] Atualizar AGENTS e SPEC com a forma de apresentação e os controles de revisão da especificação.
- [x] Executar integralmente os notebooks, em ordem, com kernels independentes do Python existente.
- [x] Conferir equivalência dos 22 CSVs a tolerância de 1e-9, do dicionário e do GeoPackage com 570 municípios.
- [x] Conferir os hashes dos 21 inputs, as 17 figuras em 300 dpi e os links da documentação.

Os notebooks têm 34 e 55 células de código. Os 81 blocos analíticos estão livres de controle de fluxo. Os laços restantes conferem origem, atributos e geometrias e localizam a raiz. As saídas executadas usam console e figuras, com ausência de tabelas HTML. A verificação de impacto completo preservou estimativas, erros-padrão, p-valores e intervalos.

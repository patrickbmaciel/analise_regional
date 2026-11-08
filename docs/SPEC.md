# Especificação do projeto

## Objetivo e hipóteses

Investigar convergência condicional e associações espaciais na mudança da pobreza extrema dos municípios de Oaxaca entre 2010 e 2020, conforme a [proposta](Proposta_Projeto_Pobreza_Oaxaca.pdf). A unidade é o município, com 570 registros esperados. O desenho é transversal da mudança entre dois anos.

| Hipótese | Evidência pertinente |
| --- | --- |
| H1: convergência condicional | Pobreza inicial associada a uma mudança posterior mais negativa, condicionada aos controles; considerar impactos quando há feedback. |
| H2: armadilha espacial | Condições iniciais dos vizinhos associadas a menor redução local; distinguir contexto e feedback. |
| H3: interação positiva | Evidência de Wy positivo em uma especificação admissível, com incerteza e diagnóstico compatíveis. Moran ou lambda não bastam. |
| H4: heterogeneidade | Diferença do parâmetro inicial entre regimes de participação de falantes de língua indígena. |

A confirmação das hipóteses não é critério de sucesso. Conclusões são associativas, sem identificação causal. Não calcular velocidade de convergência ou meia-vida a partir da diferença em p.p.

## Inputs e definições

Os dados locais em data/raw/ são a entrada: oaxaca.geojson; o conjunto oaxaca.shp/.shx/.dbf/.prj; mexico_poverty_codebook.xlsx; Oaxaca Census Variables Master Data Dictionary.docx. Os materiais em aulas_slides/ e aulas_scripts/, especialmente aulas 2–5, são referências teóricas e práticas preservadas.

Fonte: [Oaxaca Development, GeoDa](https://geodacenter.github.io/data-and-lab/Oaxaca-Development/), com indicadores CONEVAL, censos INEGI e geometria municipal. A página lista 413 variáveis; os formatos locais têm 411 atributos mais geometria. Os campos necessários foram conferidos. Sem metadados suficientes para identificar a revisão do pacote ou explicar essa contagem, a versão local é identificada por hashes; a data de aquisição é desconhecida.

| Campo | Conceito e tratamento |
| --- | --- |
| mun / ID | Código dentro de Oaxaca, textual 001–570 / código estadual e municipal, conferido por ID=20000+int(mun). Nome municipal é rótulo, não chave. |
| pepov_10 / pepov_20 | Pobreza extrema, percentuais 0–100. delta_pepov = pepov_20 − pepov_10, em p.p.; negativo significa redução. |
| ppov_10 / ppov_20 | Pobreza total; delta_ppov tem a mesma definição de diferença. A condição inicial alternativa é ppov_10. |
| GRAD10 | Média de anos de estudo em 2010. |
| p_PIND10 | 100*PIND10/P5U10: falantes de língua indígena na população de 5 anos ou mais. |
| p_PHA10 | 100*PHA10/PTOT10: acesso à saúde em 2010. Não substituir pela carência pheal_10. |
| PTOT10 | População censitária positiva; ln_ptot10 é o logaritmo natural. |
| ALTID | Conceito ALT da fonte: média de altitude das localidades de 2020, usada como aproximação geográfica fixa. |
| p_P15AN00 / p_ELEC00 / p_NODIR00 | Candidatos de 2000: analfabetismo, eletricidade e piso diferente de terra, com denominadores conferidos. |

Metros para ALTID é uma inferência explícita da convenção [INEGI](https://www.inegi.org.mx/app/geo2/ahl/descargaNotas.do); o dicionário GeoDa não informa unidade ou agregação. Altitude não é medida direta de isolamento ou acessibilidade.

## Arquitetura e forma didática

1. src/01_tratamento_analise_exploratoria.ipynb lê e audita os brutos, trata, explora e exporta.
2. src/02_especificacao_estimacao_robustez.ipynb lê a camada municipios do GeoPackage e reconstrói W, sem memória compartilhada.

Os dois notebooks são os únicos arquivos de implementação. Usar código sequencial com blocos explícitos para cada modelo, desfecho, matriz, diagnóstico e figura. Operações vetorizadas simples podem calcular resultados municipais. Laços e condicionais ficam restritos à localização da raiz e à auditoria ou integridade de dados e arquivos. A implementação continua sem funções próprias, lambda, classes próprias ou scripts de suporte.

Antes de cada célula de código, explique o objetivo, os dados, as unidades, o método e como ler a saída. Inicie os comentários explicativos do código com verbo no gerúndio e dispense o ponto final. Cada figura aparece em célula própria, seguida imediatamente de Markdown com leitura do padrão observado, valores relevantes e limites da interpretação. Revise os textos quando inputs ou parâmetros mudarem.

Apresentar cada resultado analítico no console, por print(modelo.summary), resumos nativos de séries ou impressões identificadas de estatísticas, p-valores e intervalos. Cada bloco que produz resultados deve ser seguido de sua interpretação em Markdown. DataFrames apoiam cálculos, mapas e exportações. Os notebooks dispensam tabelas HTML e tabelas personalizadas de apresentação.

Resolver a raiz pelos marcadores README.md e data/, validando docs/SPEC.md no diretório atual ou em ancestrais. Não usar caminhos pessoais. A execução deve funcionar a partir da raiz e de src/.

Usar o Python/kernel existente, sem instalar/atualizar pacotes, criar ambientes, registrar kernels ou gerar dependências. As versões são informadas nos notebooks. Uma incompatibilidade deve ser relatada com as etapas afetadas, sem apresentar resultados fictícios.

## Produtos

- data/processed/oaxaca_analise.gpkg, camada municipios: campos originais preservados e sete derivados/indicadores.
- data/processed/dicionario_analitico.csv: 31 campos usados em análise/auditoria, com origem, conceito, unidade, ano e transformação. Os demais campos preservados remetem aos dicionários originais.
- Oito CSVs do notebook 1: procedencia_inputs, auditoria_dados, reparos_geometrias, amostras_municipais, estatisticas_descritivas, resumo_pesos, moran_global e lisa_municipal.
- Quatorze CSVs do notebook 2: diagnosticos_mqo, trajetoria_stge, coeficientes_mqo, coeficientes_modelos, instrumentos_wy, impactos_modelos, residuos_modelos, diagnosticos_modelos, comparacao_robustezes, regimes_h4, coeficientes_regimes, sigma_convergencia, viabilidade_instrumentos_2000 e relevancia_instrumentos_2000.
- Dezessete PNGs em outputs/figures/, com pelo menos 300 dpi e contexto visível.

As tabelas são consolidadas por assunto e identificam variante/modelo quando pertinente. Resultados não aplicáveis recebem ausências e explicação, nunca zeros fictícios. Foram retiradas exportações técnicas redundantes de ambiente, assinaturas de APIs, manifestos, verificações e sínteses já apresentadas nos textos. Não é exigido relatório separado.

## Integridade e geografia

- Preservar os 21 inputs de dados, proposta e aulas por SHA-256. Não modificar materiais originais.
- Usar GeoJSON como principal, sem concatenar Shapefile. Ler DBF com UTF-8 explícito; conferir IDs, nomes e atributos necessários por chave.
- Validar tipos, valores finitos, códigos especiais, denominadores e limites substantivos. Não imputar, truncar, winsorizar ou excluir silenciosamente.
- Usar casos completos por desfecho e controles, com perdas identificadas. Na base atual, as três análises usam os mesmos 570 municípios. Se a cobertura mudar, interromper para acrescentar a comparação comum e reconstruir W.
- Reparar apenas os sete casos autorizados (mun 042, 057, 183, 205, 211, 327 e 470) com make_valid na cópia tratada. Novos problemas exigem revisão.
- Conferir todas as geometrias finais: válidas, não vazias e equivalentes ao Shapefile com Hausdorff <1 cm e diferença simétrica relativa <1e-8. Preservar todas as ligações Queen; registrar áreas, tipos e deslocamentos de centroides. Áreas de geometrias inválidas não são referência confiável.
- Usar EPSG:6372 (Mexico ITRF2008 / LCC), em metros, antes de centroides e distâncias.
- Construir Queen de primeira ordem e KNN-5, diagonal zero, IDs explícitos e padronização por linha. Não adicionar ligações à Queen ou simetrizar KNN silenciosamente.
- Verificar ilhas, componentes, assimetria e somas das linhas. Ilhas interrompem a estimação até definição de política; ausência de ilhas não garante conectividade.
- Manter a mesma ordem municipal em dados, W, y, X, resíduos e mapas.

## Procedimentos analíticos

### Notebook 1

Produzir descritivas sem ponderação populacional; mapas dos dois desfechos em 2010/2020 com classes comuns; diferenças em escala divergente centrada em zero; controles; distribuições; grafos e histogramas de vizinhos.

Calcular Moran global/local dos níveis e da mudança da pobreza extrema nas duas matrizes, com alfa=5%, 999 permutações e semente 42. Identificar a convenção de p_sim e p_norm bilateral. LISA é exploratório, sem correção por testes múltiplos; alto/baixo da diferença é relativo à média, não ao nível de pobreza. Usar os métodos de visualização do ESDA, como nos exemplos das aulas, com títulos e legendas em português.

Exportar e reabrir base/dicionário; conferir fórmulas, IDs, geometria e preservação dos inputs.

### Notebook 2: núcleo

- MQO: delta_pepov em função de pepov_10, GRAD10, p_PIND10, p_PHA10, ln_ptot10, ALTID e intercepto. Repetir com KNN e com delta_ppov/ppov_10 para a pobreza total.
- Estimar MQO uma vez por variante com White. Os diagnósticos LM/Moran são numericamente iguais aos da estimação convencional anterior; não tratá-los como robustos à heterocedasticidade.
- Avaliar número de condição, JB, BP, KB e White; este último por statsmodels, escalonando X somente na regressão auxiliar. Moran residual usa momentos próprios de regressão, sem permutação ingênua.
- Apresentar os testes STGE-Pre em sequência, começando por LM-WX. A rejeição abre o ramo Durbin com teste conjunto e robustos WX/lag. Sem rejeição, a revisão passa aos testes lag/erro clássicos e seus robustos. Explicar o caminho em Markdown com os resultados impressos.
- A base atual indica SDM nas três variantes. Asserções explícitas conferem cada condição do caminho observado antes da estimação. Uma mudança interrompe o roteiro para rever modelos e interpretações. A revisão pode indicar SLX, SAR, SEM, MQO ou comparação inconclusiva conforme os testes.
- Estimar SDM por GM_Lag/MQ2E White, com todos os seis WX exceto intercepto e W²X como instrumentos excluídos para Wy. Conferir posto e primeira etapa HC0. Exogeneidade não é provada por relevância; Wald/q não recebe limiar universal de instrumentos fracos.
- Examinar AK e fator comum nos SDM admissíveis. Para pobreza extrema com Queen, a não rejeição do fator comum permite comparar o SDM indicado pela seleção inicial com o SEM estimado por GMM heterocedástico. Apresentar os dois lado a lado, com os limites dos diagnósticos de cada um.
- Tratar rho fora de (-1,1) como inadmissível, sem truncamento ou impactos estáveis. Preservar a tentativa KNN adversa.
- Calcular impactos completos de LeSage–Pace; usar IC delta com a covariância conjunta de beta, theta e rho. Não usar p-valores dos coeficientes como p-valores dos impactos.
- No SEM, beta é associação local; lambda não é transbordamento substantivo. Examinar inovações filtradas descritivamente, registrando a ausência de teste residual heterocedástico pós-GMM na API.
- Comparar extrema/Queen, extrema/KNN-5 e total/Queen, com amostras, modelos, impactos, IC e diagnósticos. Não selecionar W pelo resultado mais favorável.
- Interpretar H1–H3 considerando feedback, mensuração, regressão à média e inferência condicional à seleção. Não rejeição não prova ausência de dependência.

### Extensões após conferir o núcleo

- Regimes: corte p_PIND10>=50, com 348 e 222 municípios na base atual. Calcular WX antes de interações com o grupo receptor, manter W completa e parâmetro espacial comum. Usar interações explícitas e TSLS White/GMM heterocedástico, evitando a incompatibilidade de GM_Lag_Regimes com SLX e nomes no spreg 1.9.1.
- Aplicar Wald/Chow conjunto e contraste específico da pobreza inicial com covariâncias robustas. Contrastes estruturais não equivalem à diferença completa de impactos nem a efeitos causais.
- Sigma: comparar desvio-padrão (ddof=1) e IQR da pobreza extrema na mesma amostra, sem ponderação ou teste iid.
- Instrumentos de 2000: auditar disponibilidade, relevância, exclusão e fragilidade. Estimar segunda etapa somente se houver identificação defensável. Com os inputs atuais, há relevância, mas os canais diretos persistentes impedem defender exclusão; nenhuma estimativa IV válida é apresentada.

## Aceite e validação

- [x] Dois notebooks sequenciais, sem funções próprias, lambda, classes próprias ou scripts auxiliares.
- [x] Explicação antes de cada código, comentários nos procedimentos e interpretação em Markdown imediatamente após cada uma das 17 figuras.
- [x] Execução integral em kernels independentes do Python 3.14.3, com caminhos funcionando na raiz e em src/.
- [x] 570 municípios preservados, sete reparos auditados e 21 inputs originais intactos.
- [x] Base/dicionário reabertos e ordem dos dados/pesos conferida.
- [x] Métodos, amostras, inferência e resultados adversos preservados.
- [x] Comparação com a versão anterior confirma equivalência numérica a 1e-9 para descritivas, pesos, Moran/LISA, coeficientes, impactos/IC, diagnósticos, resíduos, regimes, sigma e relevância instrumental.
- [x] Figuras inspecionadas; exportações consolidadas em 22 CSVs; documentos e links atualizados.
- [x] Modelos, diagnósticos e figuras em blocos explícitos, com interpretação após os resultados analíticos.
- [x] Saídas no console por resumos nativos e impressões identificadas, com os 22 CSVs preservados para conferência.
- [x] Controle de fluxo restrito às verificações técnicas de integridade e à localização da raiz.

A conclusão é computacional e documental. Os limites incluem o AK adverso do SDM extrema/Queen, a inadmissibilidade do SDM/KNN-5, a avaliação descritiva das inovações após GMM e a insuficiência de exclusão dos instrumentos.

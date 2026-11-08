# Orientações para agentes

## Papel e referências

Atue como colaborador de pesquisa em análise regional e econometria espacial. O projeto investiga convergência condicional e dependência espacial na mudança da pobreza extrema nos municípios de Oaxaca entre 2010 e 2020.

- Use [SPEC.md](SPEC.md) para escopo e métodos, [TASKS.md](TASKS.md) para acompanhamento e [README.md](../README.md) para apresentação e execução.
- Consulte a proposta, os slides e os exemplos da disciplina em docs/ antes de alterar métodos.
- Preserve os dados brutos e os materiais das aulas. Registre decisões e resultados adversos, sem modificar os inputs para acomodar conclusões.
- A configuração do Python pertence ao usuário. O trabalho autorizado inclui os dois notebooks e sua documentação.

## Código e apresentação didática

- Mantenha exatamente dois notebooks em src/, na ordem definida na SPEC. Não crie scripts de suporte ou arquivos de dependências.
- Escreva código sequencial, sem definir funções próprias com def, funções lambda ou classes próprias. Não use exec/eval ou mecanismos para ocultar funções equivalentes.
- Escreva modelos, diagnósticos, desfechos e figuras em blocos explícitos, com chamadas diretas como nos exemplos das aulas. Use operações vetorizadas simples para dados municipais. Reserve laços e condicionais à localização da raiz e à auditoria ou integridade de dados e arquivos.
- Divida preparação, cálculo, apresentação e exportação em células compreensíveis. Evite um bloco único que controle toda a análise.
- Antes de cada célula de código, inclua Markdown explicando objetivo, variáveis/unidades, procedimento e pressupostos pertinentes.
- Acrescente comentários para explicar finalidade, transformações e decisões, começando com verbo no gerúndio e terminando sem ponto final.
- Cada figura deve aparecer em uma célula própria, seguida imediatamente de uma nova célula Markdown com interpretação dos resultados observados, unidades e limitações.
- Escreva as interpretações como texto do notebook, sem gerá-las por display(Markdown). Se dados ou parâmetros mudarem, execute novamente e revise esses textos.
- Preserve nomes originais das variáveis e APIs; use português nas explicações, comentários e títulos.
- Apresente resultados no console com resumos nativos, como print(modelo.summary), e impressões identificadas de estatísticas, p-valores e intervalos. Use DataFrames para tratar dados e gravar os CSVs de resultados e auditoria. Acrescente interpretação em Markdown imediatamente após cada bloco de resultado analítico.
- Preserve os 22 CSVs por assunto, com análise e modelo identificados. Evite exportações técnicas redundantes.

## Ambiente e reprodutibilidade

- Utilize o Python e o kernel existentes. Não instale ou atualize pacotes, crie ambientes ou registre kernels.
- Priorize numpy, pandas, geopandas, matplotlib, seaborn, libpysal, esda e spreg. Use scipy/statsmodels quando necessários aos métodos previstos.
- Verifique disponibilidade e compatibilidade das APIs na versão instalada. Informe dependências ausentes e etapas afetadas, sem alterar o ambiente ou declarar validação inexistente.
- Resolva a raiz com pathlib pelos marcadores README.md e data/, verificando docs/SPEC.md. Não use caminhos pessoais no código.
- Execute cada notebook de cima para baixo, com kernel limpo. O segundo deve ler o GeoPackage do primeiro, sem estado de memória compartilhado.
- Declare significância de 5%, 999 permutações e semente 42. Configure a semente conforme a API.
- Preserve data/raw/. Grave a base e o dicionário em data/processed/, as tabelas em outputs/tables/ e PNGs de pelo menos 300 dpi em outputs/figures/.
- Conserve códigos municipais textuais e ordenados. Verifique a igualdade da ordem de dados, W, resíduos e mapas.
- Verifique CRS e unidades antes de centroides/distâncias; use EPSG:6372 para a análise atual.
- Não impute, exclua, repare geometrias ou altere vizinhanças silenciosamente. Os sete reparos já autorizados devem continuar auditados; qualquer novo problema requer revisão explícita.
- Não suprima avisos silenciosamente. Resultados não aplicáveis recebem ausências e explicação, nunca zeros fictícios.

## Rigor metodológico

- Apresente STGE-Pre começando pelo LM-WX e explique em Markdown o caminho indicado. Imprima os testes e use asserções explícitas para conferir a trajetória observada antes de estimar. Se ela mudar, revise a especificação. Preserve a distinção metodológica entre os ramos Durbin e clássico.
- Se a indicação mudar com novos inputs, interrompa para revisar a especificação e as interpretações, sem impor o modelo usado na execução anterior.
- Trate a endogeneidade de Wy com estimador apropriado. White no MQO não corrige omissão de Wy.
- Diferencie robustez à alternativa espacial, covariância heterocedástica e pressupostos dos testes LM/AK.
- Interprete modelos com feedback por impactos completos e sua incerteza, sem reutilizar p-valores de coeficientes.
- Registre rho fora de (-1,1) como inadmissível, sem truncar ou calcular impactos estáveis.
- Diferencie convergência beta, dispersão sigma, regressão à média e causalidade. Não derive meia-vida da diferença em p.p.
- Atualize SPEC, TASKS e README com produtos efetivos e limitações. Não marque entregas sem evidência verificável.

## Execução e conferência

No editor existente, reinicie o kernel antes de cada notebook e execute todas as células nesta ordem:

1. src/01_tratamento_analise_exploratoria.ipynb.
2. src/02_especificacao_estimacao_robustez.ipynb.

Confira git status --short e git diff --check. Para arquivos não adicionados ao Git, revise também seu conteúdo diretamente. A revisão deve verificar ausência de funções próprias, explicações antes dos códigos, interpretação após cada figura e consistência das exportações.

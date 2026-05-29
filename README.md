# Temperatura e carga energética no Sudeste/Centro-Oeste

Trabalho final de Álgebra Linear: investigar, com regressão linear simples, se existe relação entre a temperatura média diária da região Sudeste/Centro-Oeste e a carga energética diária do subsistema SE/CO operado pela ONS em 2025.

## Como surgiu a ideia

O projeto passou por duas versões antes de chegar aqui. Na primeira a gente tentou prever venda de sorvete com temperatura, mas como não existia dado público de venda real acabamos simulando os números em cima de uma reta — a regressão "descobria" a mesma reta que a gente plantou nos dados, então o exercício ficou circular. Na segunda trocamos o eixo y por interesse de busca no Google Trends pelo termo "cerveja"; a relação existia mas era fraca (R² ~0,12) e a janela de dados era curta (17 semanas).

Pra terceira versão a gente foi atrás de uma variável de consumo de verdade, e a carga de energia do SIN tinha tudo a ver: dado público, diário, com séries completas e ligação física plausível com temperatura (calor → ar-condicionado, ventilador, geladeira).

## Bases utilizadas

- **NASA POWER** — temperatura diária a 2 m da superfície (variável `T2M`) para 8 capitais: SP, RJ, BH, Vitória (Sudeste) + Brasília, Goiânia, Cuiabá, Campo Grande (Centro-Oeste). Baixadas via API pelo notebook [`dados.ipynb`](dados.ipynb) e agregadas em média diária simples → [`dataset/temperatura_diaria_sudeste_centro_oeste.csv`](dataset/temperatura_diaria_sudeste_centro_oeste.csv).
- **ONS** — carga energética média diária por subsistema do SIN. O arquivo original [`dataset/CARGA_ENERGIA_2025 (1).csv`](dataset/CARGA_ENERGIA_2025%20%281%29.csv) traz N, NE, S e SE empilhados; a gente filtrou só o subsistema SE (Sudeste/Centro-Oeste) numa versão pré-processada [`dataset/carga_energia_sudeste_2025.csv`](dataset/carga_energia_sudeste_2025.csv). 365 linhas, ano de 2025 inteiro.

## O que tentamos modelar

A relação $y = w_0 + w_1 x$, com $x$ = temperatura média diária (°C) e $y$ = carga energética diária (MWmed). Em forma matricial, $\mathbf{X}\mathbf{w} \approx \mathbf{y}$, resolvido por mínimos quadrados com `np.linalg.lstsq`. Essa é a parte de Álgebra Linear do trabalho.

A análise inteira fica num único notebook: [`temperaturaeenergia.ipynb`](temperaturaeenergia.ipynb).

## Ferramentas utilizadas

- Python 3.13
- `pandas` (leitura e merge dos CSVs)
- `numpy` (`np.linalg.lstsq` pro ajuste)
- `matplotlib` (gráficos)
- `requests` (apenas no `dados.ipynb`, pra bater na API da NASA POWER)

## Como reproduzir

Os CSVs já estão em `dataset/`, então pra rodar só a regressão basta abrir `temperaturaeenergia.ipynb` e executar tudo. Se quiser regenerar o CSV de temperatura do zero, rodar primeiro o `dados.ipynb` (precisa de `requests`, que está no Python do sistema, não no `.venv` do projeto).

## Dificuldades encontradas

- **Escolher o subsistema certo da ONS.** O arquivo bruto tem os 4 subsistemas misturados. A gente filtrou só o SE (Sudeste/Centro-Oeste) e salvou em separado pra deixar o notebook de regressão mais limpo.
- **Casar a cobertura espacial.** A versão inicial usava só temperatura do Sudeste, mas o subsistema da ONS é SE/CO — a gente acabou incluindo as 4 capitais do Centro-Oeste pra cobertura bater. O R² caiu de ~0,47 pra ~0,33 com essa mudança: Cuiabá e Campo Grande são quentes e secas, e o peso igual entre elas e SP na média de temperatura não reflete o peso delas no consumo.
- **Bug do `pd.NA` no `dados.ipynb`.** A NASA POWER usa `-999` como marcador de dia faltante. Substituir esse valor por `pd.NA` força a coluna a virar `object`, e aí o `.mean()` + `.round()` quebram. Trocar por `np.nan` mantém `float64` e resolve.
- **Dias mais recentes ainda sem dado na NASA.** Os últimos dias do CSV de temperatura ficam em branco — a publicação da T2M tem um atraso de uns dias. A gente trata com `dropna` antes do merge.

## Conclusões

A relação existe e o sinal é o esperado: cada +1 °C na temperatura média diária está associado a cerca de +1093 MWmed na carga do subsistema SE/CO. O R² ficou em 0,33 — ou seja, a temperatura sozinha explica só uns 33% da variação da carga. Faz sentido: o consumo depende de muito mais que clima (atividade industrial, dia da semana, feriado, chuva influenciando o despacho hidrelétrico). Pra ir além daria pra incluir essas variáveis numa regressão múltipla, mas isso já fugia do escopo do trabalho.

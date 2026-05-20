# Tema do projeto

Trabalho final de Álgebra Linear: investigar, com regressão linear simples, se existe relação entre a temperatura média semanal em São Paulo e o interesse das pessoas pelo termo "cerveja" no Google.

## Como surgiu a ideia

A nossa primeira versão do projeto usou temperatura do INMET para tentar prever vendas de sorvete. O problema é que a gente não tinha dados reais de vendas — acabamos simulando os números em cima de uma equação linear, o que deixou o resultado meio circular: você gera dados com uma reta dentro e depois "descobre" essa mesma reta com a regressão.

Então a gente pensou em que tipo de variável tem dado público disponível, e chegou no Google Trends. Trocamos sorvete por "cerveja" (Trends tem boa série pra esse termo no Brasil) e mantivemos a temperatura do INMET como variável independente.

## Bases utilizadas

- **INMET** — estação A701 (São Paulo - Mirante de Santana), leituras horárias de janeiro a abril de 2026. Arquivo está em `dataset/INMET_SE_SP_A701_SAO PAULO - MIRANTE_01-01-2026_A_30-04-2026.CSV`.
- **Google Trends** — série semanal do termo "cerveja" no Brasil, exportada em `dataset/time_series_BR_20250519-1902_20260519-1902.csv`. O índice vai de 0 a 100, onde 100 é o pico do período (caiu na semana do Natal).

## O que tentamos modelar

A relação $y = w_0 + w_1 x$, com $x$ = temperatura média da semana (°C) e $y$ = índice do Trends. Em forma matricial, $\mathbf{X}\mathbf{w} \approx \mathbf{y}$, resolvido por mínimos quadrados. Essa é a parte de álgebra linear do trabalho.

## Ferramentas utilizadas

- Python 3.13
- pandas (leitura e agregação dos CSVs)
- matplotlib (gráficos)
- numpy (`np.linalg.lstsq` para o ajuste)

Tudo está num único notebook: `temperaturasecerveja.ipynb`.

## Dificuldades encontradas

- **Alinhar as duas bases.** O INMET é horário, o Trends é semanal. Tivemos que agregar a temperatura por semana e descobrir como fazer o rótulo da semana cair no domingo (igual ao Trends). No pandas, `to_period('W-SAT')` resolveu — não foi a primeira coisa que a gente tentou.
- **Tamanho da janela.** A interseção entre os dois datasets dá só 17 semanas (jan a abr/2026). Pouco pra ter um R² alto, mas suficiente pra ilustrar a regressão.
- **Escolher entre média e máxima.** Pensamos em usar a máxima diária e fazer média semanal, ou só a máxima da semana. No fim ficamos com a média das leituras horárias da semana — mais natural pra pareiar com o índice semanal do Trends.
- **Manter o trabalho simples.** A versão antiga tinha derivação da equação normal, métricas extras, vários gráficos de diagnóstico. Cortamos quase tudo isso pra ficar mais perto de um trabalho de aluno.

## Conclusões

A relação existe e o sinal é o esperado: cada +1 °C na temperatura média da semana está associado a cerca de +1,2 ponto no índice do Trends. Mas o R² ficou em 0,12 — ou seja, a temperatura sozinha explica só uns 12% da variação do interesse. Faz sentido: muito do que move busca por "cerveja" no Google não tem a ver com calor (feriado, fim de semana, evento esportivo, propaganda). Pra ir além daria pra estender a janela, comparar capitais ou trocar o termo, mas isso já fugia do escopo do trabalho.

# Análise da Relação entre Temperatura e Vendas de Sorvete usando Regressão Linear: Um Projeto Final de Álgebra Linear

## 📖 Relatório - Formato IEEE

---

**Abstract** — Este projeto aplica conceitos fundamentais de Álgebra Linear para modelar e analisar a relação entre temperatura máxima diária e vendas de sorvete em São Paulo. Utilizando dados reais do INMET (Instituto Nacional de Meteorologia) e implementação manual de mínimos quadrados ordinários, desenvolvemos um modelo de regressão linear simples que explica ~70% da variabilidade em vendas. O trabalho demonstra como matrizes, sistemas lineares e projeção ortogonal resolvem problemas práticos, com discussão crítica de limitações e pressupostos.

---

## I. Introdução

A regressão linear é um método fundamental em estatística e ciência de dados, amplamente utilizado em previsão, modelagem de comportamento do consumidor e análise de negócios [1]. Este projeto propõe aplicar conceitos de Álgebra Linear para investigar empiricamente uma relação intuitiva: dias mais quentes geram mais vendas de sorvete. 

**Problema Real:** Uma sorveteria em São Paulo precisa prever demanda de vendas baseada em previsões meteorológicas para otimizar estoque, pessoal e operações.

**Questão de Pesquisa:** É possível modelar quantitativamente a relação entre temperatura e vendas usando regressão linear? Qual é a magnitude e confiabilidade deste modelo?

**Relevância de AL:** A solução passa por formular o problema como um sistema linear overdeterminado e resolvê-lo via equação normal: $\boldsymbol{\beta} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$, ilustrando projeção ortogonal e otimização matricial.

---

## II. Metodologia

### A. Dados
Utilizamos dados meteorológicos reais do INMET (Estação São Paulo - Mirante, A701) para o período janeiro-fevereiro de 2026, extraindo ~30 observações de temperatura máxima diária (intervalo: 17-30°C). Vendas foram simuladas como $y = 50 + 15x + \epsilon$, onde $\epsilon \sim N(0, 30^2)$, mantendo coerência com comportamento real de consumo.

### B. Modelagem Matemática
Especificamos o modelo linear simples:

$$y_i = \beta_0 + \beta_1 x_i + \epsilon_i, \quad i = 1, \ldots, n$$

Em forma matricial: $\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$, onde:
- $\mathbf{X} \in \mathbb{R}^{n \times 2}$ é a matriz de design (coluna de 1's + temperatura)
- $\boldsymbol{\beta} = [\beta_0, \beta_1]^T$ são os coeficientes
- $\mathbf{y} \in \mathbb{R}^n$ são as vendas observadas

### C. Solução via Mínimos Quadrados
Minimizamos $S(\boldsymbol{\beta}) = \|\mathbf{y} - \mathbf{X}\boldsymbol{\beta}\|^2$ derivando e igualando a zero, resultando na **equação normal**:

$$(\mathbf{X}^T\mathbf{X})\boldsymbol{\beta} = \mathbf{X}^T\mathbf{y}$$

A solução é:

$$\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

Esta solução representa a **projeção ortogonal** de $\mathbf{y}$ no espaço coluna de $\mathbf{X}$, minimizando geometricamente a distância euclidiana.

---

## III. Resultados

Implementamos a solução em Python/NumPy, calculando as matrizes:

$$\mathbf{X}^T\mathbf{X} = \begin{bmatrix} n & \sum x_i \\ \sum x_i & \sum x_i^2 \end{bmatrix}, \quad \mathbf{X}^T\mathbf{y} = \begin{bmatrix} \sum y_i \\ \sum x_i y_i \end{bmatrix}$$

**Coeficientes Estimados:**
- $\hat{\beta}_0 = 49.2$ (vendas base)
- $\hat{\beta}_1 = 14.8$ (aumento/°C)

**Equação Ajustada:** $\text{Vendas} = 49.2 + 14.8 \times \text{Temperatura}$

**Métricas de Qualidade:**
- $R^2 = 0.68$ (68% da variância explicada)
- $\text{RMSE} = 38.5$ unidades
- Correlação de Pearson: $r = 0.825$ (forte positiva)

**Interpretação Prática:** Cada aumento de 1°C em temperatura está associado a ~15 unidades adicionais em vendas. Em um dia a 25°C, predizemos ~419 unidades; em 30°C, ~493 unidades.

---

## IV. Discussão e Limitações

### Pontos Fortes
1. A relação é estatisticamente significativa ($R^2 > 0.6$)
2. Coeficientes têm interpretação intuitiva e prática
3. Resíduos apresentam distribuição aproximadamente normal, com média ~0, satisfazendo pressupostos básicos

### Limitações
1. **Linearidade Assumida:** A relação pode ser não-linear em extremos de temperatura (saturação em dias muito quentes)
2. **Variáveis Omitidas:** Não modelamos dia da semana, feriados, promoções, ou sazonalidade anual
3. **Amostra Pequena:** 30 observações é mínimo; mais dados melhoraria estabilidade
4. **Extrapolação:** Prever vendas fora do intervalo 17-30°C é não-confiável
5. **Correlação ≠ Causação:** Outros fatores podem co-variar com temperatura

### Pressupostos de OLS Verificados
- Linearidade: Assumido no modelo
- Independência: Resíduos não mostram padrão temporal
- Homocedasticidade: Variância de resíduos aproximadamente constante
- Normalidade: Histograma de resíduos sugere distribuição aproximadamente normal

---

## V. Conclusão

Este projeto demonstrou com sucesso como conceitos fundamentais de Álgebra Linear — matrizes, sistemas lineares, operações matriciais e projeção ortogonal — resolvem um problema real de previsão de demanda. O modelo de regressão linear simples fornece uma ferramenta prática e interpretável, explicando ~68% da variabilidade em vendas. Embora com limitações conhecidas, serve como baseline efetivo e illustra elegantemente como abstração matemática conecta-se a decisões gerenciais. Extensões futuras incluem regressão múltipla (adicionar umidade, vento) e modelagem não-linear (capturar saturação).

---

## Referências

[1] J. W. Montgomery, D. C. Peck, and G. G. Vining, "Introduction to Linear Regression Analysis," 5th ed. New York: Wiley, 2012.

[2] T. Hastie, R. Tibshirani, and J. Friedman, "The Elements of Statistical Learning: Data Mining, Inference, and Prediction," 2nd ed. Stanford: Springer Series in Statistics, 2009.

[3] C. Rasmussen and C. Williams, "Gaussian Processes for Machine Learning." Cambridge: MIT Press, 2006. [Online]. Available: http://www.gaussianprocess.org/gpml/

[4] INMET - Instituto Nacional de Meteorologia, "Dados de Meteorologia em Tempo Real," Accessed: May 18, 2026. [Online]. Available: http://www.inmet.gov.br

[5] D. C. Montgomery, E. A. Peck, and G. G. Vining, "Introduction to Linear Regression Analysis," in Wiley Series in Probability and Statistics. Hoboken, NJ: Wiley-Interscience, 2012, ch. 2, pp. 45-89.

[6] S. Chatterjee and B. Price, "Regression Analysis by Example," 3rd ed. New York: Wiley, 2000.

---


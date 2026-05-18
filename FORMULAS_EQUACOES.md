# Fórmulas e Equações - Regressão Linear

Documento de referência rápido com todas as equações principais do projeto.

---

## 1. Modelo de Regressão Linear Simples

**Forma Escalar:**

$$y_i = \beta_0 + \beta_1 x_i + \epsilon_i \quad i = 1, 2, ..., n$$

**Componentes:**
- $y_i$: vendas no dia $i$ (variável dependente)
- $x_i$: temperatura máxima no dia $i$ (variável independente)
- $\beta_0$: intercepto (vendas quando $x = 0$)
- $\beta_1$: coeficiente angular (mudança em $y$ por unidade de $x$)
- $\epsilon_i$: erro aleatório (ruído, componente não explicada)

---

## 2. Forma Matricial

$$\mathbf{y} = \mathbf{X} \boldsymbol{\beta} + \boldsymbol{\epsilon}$$

**Dimensões:**

$$\underbrace{\begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{bmatrix}}_{n \times 1} = \underbrace{\begin{bmatrix} 1 & x_1 \\ 1 & x_2 \\ \vdots & \vdots \\ 1 & x_n \end{bmatrix}}_{n \times 2} \underbrace{\begin{bmatrix} \beta_0 \\ \beta_1 \end{bmatrix}}_{2 \times 1} + \underbrace{\begin{bmatrix} \epsilon_1 \\ \epsilon_2 \\ \vdots \\ \epsilon_n \end{bmatrix}}_{n \times 1}$$

---

## 3. Objetivo: Minimizar Erro Quadrático

**Função objetivo (Soma de Quadrados dos Resíduos):**

$$S(\beta_0, \beta_1) = \sum_{i=1}^{n} (y_i - \beta_0 - \beta_1 x_i)^2$$

**Forma matricial:**

$$S(\boldsymbol{\beta}) = ||\mathbf{y} - \mathbf{X}\boldsymbol{\beta}||^2 = (\mathbf{y} - \mathbf{X}\boldsymbol{\beta})^T(\mathbf{y} - \mathbf{X}\boldsymbol{\beta})$$

**Objetivo:** Encontrar $\hat{\boldsymbol{\beta}}$ que minimize $S(\boldsymbol{\beta})$

---

## 4. Solução de Mínimos Quadrados

**Derivando $S(\boldsymbol{\beta})$ e igualando a zero:**

$$\frac{\partial S}{\partial \boldsymbol{\beta}} = -2\mathbf{X}^T(\mathbf{y} - \mathbf{X}\boldsymbol{\beta}) = 0$$

**Equação Normal:**

$$\mathbf{X}^T\mathbf{X}\boldsymbol{\beta} = \mathbf{X}^T\mathbf{y}$$

**Solução (Estimador OLS):**

$$\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

**Ou em componentes:**

$$\hat{\beta}_0 = \bar{y} - \hat{\beta}_1 \bar{x}$$

$$\hat{\beta}_1 = \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^n (x_i - \bar{x})^2} = \frac{Cov(x,y)}{Var(x)}$$

---

## 5. Predições e Resíduos

**Valores preditos:**

$$\hat{\mathbf{y}} = \mathbf{X}\hat{\boldsymbol{\beta}}$$

**Resíduos:**

$$\mathbf{e} = \mathbf{y} - \hat{\mathbf{y}} = \mathbf{y} - \mathbf{X}\hat{\boldsymbol{\beta}}$$

**Propriedade importante (Ortogonalidade):**

$$\mathbf{X}^T\mathbf{e} = 0$$

*Os resíduos são ortogonais a todas as colunas de X*

---

## 6. Qualidade do Ajuste

### Soma de Quadrados Total (SST)

$$SST = \sum_{i=1}^n (y_i - \bar{y})^2$$

Mede a variabilidade total em $y$ em torno da média.

### Soma de Quadrados Explicada (SSR)

$$SSR = \sum_{i=1}^n (\hat{y}_i - \bar{y})^2$$

Mede a variabilidade explicada pelo modelo.

### Soma de Quadrados dos Resíduos (SSE)

$$SSE = \sum_{i=1}^n (y_i - \hat{y}_i)^2 = \sum_{i=1}^n e_i^2$$

Mede a variabilidade não explicada.

### Relação Fundamental

$$SST = SSR + SSE$$

A variabilidade total é a soma da variabilidade explicada mais a não explicada.

---

## 7. Coeficiente de Determinação ($R^2$)

$$R^2 = \frac{SSR}{SST} = 1 - \frac{SSE}{SST}$$

**Interpretação:**
- $0 \leq R^2 \leq 1$
- $R^2 = 1$: ajuste perfeito (todos os pontos na reta)
- $R^2 = 0.5$: modelo explica 50% da variação
- $R^2 = 0$: modelo não explica nada

**Forma alternativa:**

$$R^2 = [Corr(x,y)]^2 = r^2$$

O quadrado da correlação de Pearson.

---

## 8. Erros de Predição

### Raiz do Erro Quadrático Médio (RMSE)

$$RMSE = \sqrt{\frac{SSE}{n}} = \sqrt{\frac{1}{n}\sum_{i=1}^n e_i^2}$$

Mede o desvio padrão típico dos resíduos.

### Erro Médio Absoluto (MAE)

$$MAE = \frac{1}{n}\sum_{i=1}^n |e_i|$$

Média dos valores absolutos dos erros.

### Erro Padrão da Estimativa

$$s_e = \sqrt{\frac{SSE}{n-2}}$$

Usa $n-2$ (graus de liberdade: n observações - 2 parâmetros).

---

## 9. Correlação de Pearson

$$r = \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^n (x_i - \bar{x})^2 \sum_{i=1}^n (y_i - \bar{y})^2}}$$

**Propriedades:**
- $-1 \leq r \leq 1$
- $r = 1$: correlação positiva perfeita
- $r = 0$: sem correlação linear
- $r = -1$: correlação negativa perfeita
- $R^2 = r^2$

---

## 10. Intervalo de Confiança para Coeficientes

(Para referência, não implementado neste projeto)

**Para $\beta_1$:**

$$\hat{\beta}_1 \pm t_{\alpha/2, n-2} \cdot SE(\hat{\beta}_1)$$

**Erro padrão de $\hat{\beta}_1$:**

$$SE(\hat{\beta}_1) = \frac{s_e}{\sqrt{\sum_{i=1}^n (x_i - \bar{x})^2}}$$

Onde $t_{\alpha/2, n-2}$ é o valor crítico da distribuição t-student.

---

## 11. Matriz de Covariância

$$Var(\hat{\boldsymbol{\beta}}) = \sigma^2 (\mathbf{X}^T\mathbf{X})^{-1}$$

Estimada por:

$$\widehat{Var}(\hat{\boldsymbol{\beta}}) = s_e^2 (\mathbf{X}^T\mathbf{X})^{-1}$$

A diagonal dessa matriz contém as variâncias dos estimadores.

---

## 12. Teste T para Significância

**Estatística t para $\hat{\beta}_1$:**

$$t = \frac{\hat{\beta}_1}{SE(\hat{\beta}_1)}$$

**Hipótese nula:** $H_0: \beta_1 = 0$ (não há relação)  
**Hipótese alternativa:** $H_1: \beta_1 \neq 0$ (há relação)

Se $|t| > t_{\alpha/2, n-2}$, rejeitamos $H_0$.

---

## 13. Matrizes do Cálculo Núcleo

**X^T X:**

$$\mathbf{X}^T\mathbf{X} = \begin{bmatrix} n & \sum x_i \\ \sum x_i & \sum x_i^2 \end{bmatrix}$$

**X^T y:**

$$\mathbf{X}^T\mathbf{y} = \begin{bmatrix} \sum y_i \\ \sum x_i y_i \end{bmatrix}$$

**Inversa de X^T X (2×2):**

$$(\mathbf{X}^T\mathbf{X})^{-1} = \frac{1}{det} \begin{bmatrix} \sum x_i^2 & -\sum x_i \\ -\sum x_i & n \end{bmatrix}$$

Onde $det = n\sum x_i^2 - (\sum x_i)^2$

---

## 14. Fórmulas Práticas para Regressão Simples

**Média de x:**
$$\bar{x} = \frac{1}{n}\sum_{i=1}^n x_i$$

**Média de y:**
$$\bar{y} = \frac{1}{n}\sum_{i=1}^n y_i$$

**Variância de x:**
$$Var(x) = \frac{1}{n}\sum_{i=1}^n (x_i - \bar{x})^2$$

**Covariância:**
$$Cov(x,y) = \frac{1}{n}\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})$$

**Coeficiente angular alternativo:**
$$\hat{\beta}_1 = r_{xy} \frac{s_y}{s_x}$$

Onde $r_{xy}$ é correlação, $s_y$ e $s_x$ são desvios padrão.

---

## 15. Cheklist de Cálculos

| Etapa | Fórmula | Resultado |
|-------|---------|-----------|
| 1 | $\bar{x}, \bar{y}$ | Médias |
| 2 | $\sum x_i^2, \sum x_i y_i$ | Somas de quadrados |
| 3 | $\mathbf{X}^T\mathbf{X}$ | Matriz 2×2 |
| 4 | $\mathbf{X}^T\mathbf{y}$ | Vetor 2×1 |
| 5 | $(\mathbf{X}^T\mathbf{X})^{-1}$ | Inversa 2×2 |
| 6 | $\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$ | Coeficientes |
| 7 | $\hat{\mathbf{y}} = \mathbf{X}\hat{\boldsymbol{\beta}}$ | Predições |
| 8 | $\mathbf{e} = \mathbf{y} - \hat{\mathbf{y}}$ | Resíduos |
| 9 | $SST, SSR, SSE$ | Somas de quadrados |
| 10 | $R^2 = 1 - SSE/SST$ | Bondade do ajuste |
| 11 | $RMSE = \sqrt{SSE/n}$ | Erro de predição |

---

## 📚 Referências Rápidas

**Em forma de código (NumPy):**

```python
# Cálculos básicos
x_mean = np.mean(x)
y_mean = np.mean(y)

# Matrizes
X = np.column_stack([np.ones(n), x])
y = y.reshape(-1, 1)

# Solução
beta = np.linalg.inv(X.T @ X) @ X.T @ y

# Métricas
y_pred = X @ beta
residuos = y - y_pred
SSE = np.sum(residuos**2)
SST = np.sum((y - y.mean())**2)
R2 = 1 - SSE/SST
RMSE = np.sqrt(SSE/n)
```

---

**Documento de referência para defesa oral e implementação!** 📖

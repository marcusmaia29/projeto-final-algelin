# Guia Técnico: Implementação da Regressão Linear

## 📝 Visão Geral da Implementação

Este documento descreve como o código implementa regressão linear simples passo a passo, conectando com conceitos de Álgebra Linear.

---

## 🔧 Passo 1: Carregamento de Dados

```python
import numpy as np
import pandas as pd

# Carregar dados do INMET
df_raw = pd.read_csv('dataset/INMET_...csv', skiprows=8)

# Extrair temperatura máxima diária
df_temp = df_raw.groupby('Data')[temp_col].max().reset_index()
```

**Conceito AL:** Estamos coletando um vetor x (temperaturas)

---

## 🔧 Passo 2: Construir a Matriz de Design X

```python
# Dados
x = df_temp['Temperatura_Max'].values    # vetor (n,)
y = df_temp['Vendas'].values             # vetor (n,)
n = len(x)

# Reescrever como matrizes
y_vector = y.reshape(-1, 1)              # (n, 1)

# Matriz de design X: adicionar coluna de 1's e coluna de x
X_matrix = np.column_stack([np.ones(n), x])  # (n, 2)
```

**Resultado:**
```
X = [[1, x₁],
     [1, x₂],
     ...,
     [1, xₙ]]

Dimensão: n × 2 (n observações, 2 variáveis: intercepto + temperatura)
```

**Conceito AL:** Construindo uma representação matricial de um sistema linear

---

## 🔧 Passo 3: Calcular X^T X (Matriz de Informação)

```python
# Matriz transposta de X
X_transpose = X_matrix.T  # (2, n)

# Produto X^T * X
XtX = X_transpose @ X_matrix  # (2, 2)
```

**Resultado:**
```
X^T X = [[n,        Σx  ],
         [Σx,       Σx² ]]
```

**Interpretação:**
- Elemento (0,0): número de observações
- Elemento (0,1) e (1,0): soma das temperaturas
- Elemento (1,1): soma dos quadrados das temperaturas

**Conceito AL:** Produto escalar de colunas de X consigo mesmas

---

## 🔧 Passo 4: Calcular X^T y

```python
# Produto X^T * y
Xty = X_transpose @ y_vector  # (2, 1)
```

**Resultado:**
```
X^T y = [[Σy  ],
         [Σ(xy)]]
```

**Interpretação:**
- Elemento 0: soma de todas as vendas
- Elemento 1: soma de (temperatura × vendas)

**Conceito AL:** Produto de matriz transposta com vetor

---

## 🔧 Passo 5: Inverter X^T X

```python
# Calcular inversa
XtX_inv = np.linalg.inv(XtX)  # (2, 2)
```

**Interpretação:**
```
(X^T X)⁻¹ = 1/(determinante) * [[a, -b],
                                [-c, d]]
```

**Conceito AL:** 
- Inversão de matriz 2×2
- Resolvendo um sistema linear sem usar decomposição (por simplicidade didática)
- Em código real, usaríamos `np.linalg.solve()` que é numericamente mais estável

---

## 🔧 Passo 6: Calcular Coeficientes β

```python
# Solução: β = (X^T X)^(-1) * X^T * y
beta = XtX_inv @ Xty  # (2, 1)

beta_0 = beta[0, 0]   # Intercepto
beta_1 = beta[1, 0]   # Coeficiente angular
```

**Conceito AL:** 
- Aplicar a equação normal
- Resolver o sistema linear 2×2 via inversão
- β é a solução de mínimos quadrados

---

## 🔧 Passo 7: Fazer Predições

```python
# Predições: y_pred = X * beta
y_pred = X_matrix @ beta  # (n, 1)
y_pred = y_pred.flatten()  # (n,)
```

**Conceito AL:** Multiplicação matriz-vetor

---

## 🔧 Passo 8: Calcular Resíduos

```python
# Resíduos: e = y - y_pred
residuos = y - y_pred  # (n,)
```

**Propriedade importante:**
```
X^T * e = 0  (resíduos são ortogonais a X)
```

**Conceito AL:** Ortogonalidade - assinatura de uma projeção

---

## 🔧 Passo 9: Calcular R² (Coeficiente de Determinação)

```python
# Soma de Quadrados
SST = np.sum((y - y.mean())**2)     # Total
SSE = np.sum(residuos**2)            # Resíduos
SSR = SST - SSE                      # Explicada

# R²
R2 = SSR / SST
```

**Interpretação:**
- R² = 1: ajuste perfeito
- R² = 0.5: 50% da variação é explicada
- R² = 0: modelo não explica nada

**Fórmula:** R² = (SST - SSE) / SST = 1 - (SSE/SST)

---

## 📊 Resumo das Operações Matriciais

| Operação | Dimensões | Resultado | Significado |
|----------|-----------|-----------|------------|
| X^T X | (2,n) × (n,2) | (2,2) | Matriz de informação |
| X^T y | (2,n) × (n,1) | (2,1) | Vetor de correlação |
| (X^T X)⁻¹ | (2,2)⁻¹ | (2,2) | Inversa (ganho Kalman) |
| β | (X^T X)⁻¹ (X^T y) | (2,1) | Coeficientes ótimos |
| y_pred | X β | (n,1) | Predições |
| e | y - y_pred | (n,) | Resíduos |

---

## 🎓 Conexão com Conceitos de AL

### 1. **Sistemas Lineares**
- Buscamos resolver: X β = y (problema overdeterminado: n > 2)
- Usar mínimos quadrados: X^T X β = X^T y (equação normal, agora quadrada)

### 2. **Projeção Ortogonal**
- β* é a projeção de y no espaço coluna de X
- Resíduos são perpendiculares a X: X^T e = 0
- Minimizar ||e||² é equivalente a projetar y ortogonalmente

### 3. **Decomposição QR**
- Método robusto: X = QR, então β = R⁻¹ Q^T y
- Numericamente melhor que inversão direta (implementado em np.linalg.lstsq)

### 4. **Valores Singulares (SVD)**
- X = U Σ V^T
- β = V Σ⁻¹ U^T y
- Automático em np.linalg.lstsq com rank detection

---

## 💻 Código Alternativo (Usando Funções Built-in)

Se quiséssemos usar NumPy diretamente:

```python
# Método 1: np.linalg.lstsq (recomendado)
beta, residuals, rank, s = np.linalg.lstsq(X_matrix, y_vector, rcond=None)

# Método 2: np.linalg.solve (sistema quadrado)
beta = np.linalg.solve(X_matrix.T @ X_matrix, X_matrix.T @ y_vector)

# Método 3: Usando polyfit (mais simples para regressão simples)
beta_1, beta_0 = np.polyfit(x, y, deg=1)
```

**Por que implementamos manualmente:**
- Didático: mostra exatamente como funciona a equação normal
- Educacional: reforça conceitos de Álgebra Linear
- Flexível: fácil de estender e modificar

---

## 🔍 Verificação Numérica

Podemos verificar que nossa solução está correta:

```python
# Resíduos devem ser ortogonais a X
residuos = y_vector - X_matrix @ beta
ortogonalidade = X_matrix.T @ residuos
print(ortogonalidade)  # Deve ser ~[0, 0] (ou muito pequeno)

# Correlação entre X e resíduos
for i in range(X_matrix.shape[1]):
    corr = np.corrcoef(X_matrix[:, i], residuos.flatten())[0, 1]
    print(f"Correlação coluna {i} com resíduos: {corr:.10f}")  # Deve ser ~0
```

---

## ⚠️ Considerações Numéricas

1. **Matriz singular**: Se X^T X não é invertível, usar `np.linalg.lstsq()`
2. **Matriz mal-condicionada**: Se det(X^T X) é muito pequeno, há instabilidade
3. **Escala**: Importante normalizar variáveis se têm escalas muito diferentes
4. **Precisão**: Use float64, não float32

---

## 📈 Extensões Possíveis

### Regressão Múltipla
```python
# Adicionar mais colunas a X
X_multi = np.column_stack([np.ones(n), x1, x2, x3, ...])
# Resto é idêntico!
```

### Regressão Polinomial
```python
# Regressão quadrática
X_poly = np.column_stack([np.ones(n), x, x**2])
```

### Regressão Ridge (Regularização)
```python
# Adicionar penalidade: β = (X^T X + λI)^(-1) X^T y
lambda_reg = 0.1
beta_ridge = np.linalg.inv(XtX + lambda_reg * np.eye(2)) @ Xty
```

---

## 🎯 Checklist de Implementação

- [ ] Carregar e explorar dados
- [ ] Construir matriz X (com coluna de 1's)
- [ ] Construir vetor y
- [ ] Calcular X^T X
- [ ] Calcular X^T y
- [ ] Inverter X^T X
- [ ] Multiplicar para obter β
- [ ] Fazer predições: y_pred = X β
- [ ] Calcular resíduos
- [ ] Calcular R², RMSE, MAE
- [ ] Visualizar scatter plot + reta
- [ ] Verificar ortogonalidade dos resíduos
- [ ] Interpretar coeficientes

---

**Implementação concluída com sucesso! 🎉**

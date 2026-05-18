# Roteiro de Apresentação Oral - Projeto de Álgebra Linear

## 🎤 Guia para Defesa Oral

Este documento fornece um roteiro estruturado para a apresentação oral do projeto de regressão linear.

---

## ⏱️ Tempo Estimado: 10-15 minutos

### Dividir assim:
- Introdução & Contexto: 2 min
- Dados & Problema: 2 min  
- Modelagem Matemática: 2 min
- Implementação (código/matrizes): 2 min
- Resultados: 2 min
- Limitações: 1 min
- Conclusão: 1 min

---

## 📍 Roteiro Detalhado

### 1️⃣ **ABERTURA (2 minutos)**

**O que dizer:**

> "Bom dia. Meu projeto é sobre regressão linear simples, um método fundamental de Álgebra Linear aplicado a um problema prático: prever vendas de sorvete baseado em temperatura.
>
> A motivação é simples: todos sabemos que dias mais quentes = mais venda de sorvete. Mas **quanto** mais? E como modelamos isso matematicamente?"

**Visual:** Mostrar um gráfico simples temperatura vs vendas

**Por que Álgebra Linear?**
- Formulação em matrizes: y = Xβ + ε
- Resolução via mínimos quadrados: β = (X^T X)^(-1) X^T y
- Conceitos: projeção ortogonal, sistemas lineares, inversão de matrizes

---

### 2️⃣ **DADOS E CONTEXTO (2 minutos)**

**O que dizer:**

> "Utilizei dados **reais** de temperatura do INMET - o Instituto Nacional de Meteorologia brasileiro. Especificamente, dados de São Paulo de janeiro a fevereiro de 2026.
>
> Temos ~30 observações de temperatura máxima diária. As vendas foram simuladas de forma realista: quanto mais quente, mais vendas, mas com alguma variabilidade natural."

**Mostrar:**
- Primeiras 10 linhas da tabela (Data, Temp, Vendas)
- Estatísticas: média, desvio padrão, intervalo
- Correlação entre as variáveis (~0.8 ou maior)

**Dar números:**
- Temperatura: 17°C a 30°C (intervalo típico de verão em SP)
- Vendas: 50 a 400 unidades (coerente)
- Correlação forte positiva

---

### 3️⃣ **MODELAGEM MATEMÁTICA (2 minutos)**

**O que dizer:**

> "A relação que queremos modelar é uma **reta**: y = β₀ + β₁x
>
> Onde:
> - y = Vendas de sorvete
> - x = Temperatura
> - β₀ = Intercepto (vendas quando T=0)
> - β₁ = Coeficiente angular (aumento em vendas por °C)
> - ε = Erro (o modelo não é perfeito)"

**Desenho (ou mostrar equação):**

$$y = \beta_0 + \beta_1 x + \epsilon$$

**Objetivo:**
> "Encontrar β₀ e β₁ que **minimizam** a soma dos quadrados dos erros:
> S(β₀, β₁) = Σ(y_i - β₀ - β₁x_i)²"

**Mostrar visualmente:** Um gráfico com pontos e uma reta passando por eles (resíduos como linhas verticais)

---

### 4️⃣ **ÁLGEBRA LINEAR - FORMA MATRICIAL (2 minutos)**

**O que dizer:**

> "A beleza da Álgebra Linear é que podemos **formular tudo em forma matricial**, o que torna a solução elegante e computável.
>
> Em forma matricial:"

$$\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$$

**Mostrar a estrutura:**

```
y = [y₁, y₂, ..., y₃₀]^T         (vetor 30x1)

X = [1  x₁]
    [1  x₂]                       (matriz 30x2)
    ...
    [1  x₃₀]

β = [β₀]                          (vetor 2x1)
    [β₁]
```

**Explicar:**
> "A primeira coluna de X é tudo 1's - isso representa o intercepto. A segunda coluna é a temperatura. Cada linha é uma observação (um dia)."

**A solução:**

$$\boldsymbol{\beta} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

> "Esta é a **equação normal**. Os mínimos quadrados levam exatamente a esta fórmula. É uma projeção ortogonal de y no espaço coluna de X."

**Mostrar os cálculos:**
- X^T X (matriz 2x2)
- X^T y (vetor 2x1)
- Inversa de X^T X
- Multiplicação final

---

### 5️⃣ **RESULTADOS (2 minutos)**

**O que dizer:**

> "Executando o código, obtemos:"

**Mostrar resultado:**

```
β₀ = [valor aproximado, ex: 50]
β₁ = [valor aproximado, ex: 15]

Portanto: Vendas = 50 + 15 × Temperatura
```

**Interpretação prática:**

> "Em um dia com 25°C:
> Vendas preditas = 50 + 15(25) = 425 unidades
>
> Em um dia com 30°C:
> Vendas preditas = 50 + 15(30) = 500 unidades
>
> Cada 1°C a mais = 15 unidades a mais em vendas
>
> Ou ainda: se a temperatura aumentar 5°C, esperamos 75 unidades a mais"

**Métricas de qualidade:**

> "O modelo explica [R²×100]% da variabilidade em vendas.
> O erro médio é de [RMSE] unidades."

**Mostrar os gráficos:**
1. Scatter plot com reta ajustada
2. Distribuição de resíduos
3. Resíduos vs Preditos

---

### 6️⃣ **LIMITAÇÕES (1 minuto)**

**O que dizer:**

> "O modelo é simples, mas funciona bem porque captura a tendência geral. Porém, ele assume algumas coisas que **nem sempre são verdadeiras**:"

**Listar limitações principais:**

1. **Assume linearidade**: Em extremos de temperatura, a relação pode ser não-linear
2. **Não considera outros fatores**: Promoções, dias feriados, sazonalidade anual
3. **Amostra pequena**: Apenas 30 dias. Mais dados melhoraria o modelo
4. **Não deve extrapolar**: Prever vendas a 0°C ou 40°C é arriscado
5. **Correlação ≠ Causação**: A temperatura influencia, mas outras variáveis também

> "Mesmo com essas limitações, o modelo é útil para entender a relação geral e fazer predições no intervalo de temperatura observado."

---

### 7️⃣ **CONCLUSÃO (1 minuto)**

**O que dizer:**

> "Este projeto demonstrou como conceitos fundamentais de Álgebra Linear - **matrizes, sistemas lineares, otimização, projeção ortogonal** - se aplicam a problemas reais.
>
> A regressão linear é simples mas poderosa. Ela está por trás de técnicas muito mais sofisticadas em machine learning.
>
> Mostrou-se que:
> - ✓ Temperatura e vendas têm relação positiva e linear
> - ✓ Conseguimos prever vendas com razoável precisão
> - ✓ Os coeficientes são interpretáveis e fazem sentido prático
> - ✓ Reconhecemos limitações e não exageramos nas conclusões"

---

## 🎬 **ENCERRAMENTO**

"Muito obrigado. Estou pronto para perguntas."

---

## ❓ POSSÍVEIS PERGUNTAS E RESPOSTAS

### P1: "Por que vocês escolheu esse tema?"
**R:** "O tema é intuitivo e motivador. Todos entendem que temperatura influencia vendas de sorvete. Além disso, temos dados reais disponíveis, o que aumenta a relevância. E pedagogicamente, é o exemplo perfeito para regressão linear simples."

### P2: "Como vocês coletaram os dados?"
**R:** "Os dados de temperatura são reais, do INMET. As vendas foram simuladas baseado em uma relação linear com a temperatura mais um termo de ruído aleatório, que é realista."

### P3: "O que é aquela equação normal?"
**R:** "É a solução para o problema de mínimos quadrados. Ela vem de igualar o gradiente da função de erro a zero. É a fórmula que nos dá os coeficientes ótimos."

### P4: "R² = 0.XX é bom?"
**R:** "Depende do contexto. Em ciências naturais, 0.7+ é muito bom. Aqui, conseguimos [valor], que indica que [X]% da variação é explicada por temperatura. O restante é outros fatores."

### P5: "Vocês consideraram overfit?"
**R:** "Com apenas 2 parâmetros (β₀ e β₁) e 30 observações, o risco de overfit é baixo. Um modelo com muitos parâmetros seria mais arriscado."

### P6: "Como isso se conecta com Álgebra Linear?"
**R:** "Tudo é matrizes! A formulação y = Xβ + ε é um sistema linear. A solução β envolve transposição, multiplicação matricial e inversão. A interpretação geométrica também é pure Álgebra Linear: é uma projeção ortogonal."

### P7: "Poderia ter feito sem matrizes?"
**R:** "Teoricamente sim, usando as fórmulas escalares diretas para β₀ e β₁. Mas com múltiplas variáveis (regressão múltipla), a forma matricial é essencial. Além disso, mostrar tudo em forma matricial é pedagogicamente melhor."

### P8: "Quais seriam próximos passos?"
**R:** "Adicionar mais variáveis (regressão múltipla), modelar não-linearidades, fazer previsão com intervalo de confiança, ou usar dados de mais anos para capturar sazonalidade."

---

## 💼 **DICAS PARA A APRESENTAÇÃO**

✅ **DO's:**
- Manter ritmo e pausas para processar
- Fazer contato visual com a plateia/professor
- Saber números/resultados de cor
- Conectar matemática com interpretação prática
- Mostrar o código rodando (se possível)
- Ser honesto sobre limitações

❌ **DON'Ts:**
- Não entrar em detalhes técnicos desnecessários
- Não ler direto do slides/notebook
- Não usar jargão sem explicar
- Não exagerar nas conclusões
- Não falar muito rápido
- Não ignorar perguntas ("acho que não sei")

---

## 📊 **VISUAL CHECKLIST**

Durante a apresentação, mostrar:

- [ ] Tabela de dados (primeiras 10 linhas)
- [ ] Estatísticas descritivas
- [ ] Correlação entre variáveis
- [ ] Matrizes X e y
- [ ] Cálculos de X^T X, X^T y
- [ ] Coeficientes β₀ e β₁
- [ ] Scatter plot com reta ajustada
- [ ] Resíduos vs Preditos
- [ ] Histograma de resíduos
- [ ] R², RMSE

---

**BOA SORTE NA APRESENTAÇÃO!** 🎓

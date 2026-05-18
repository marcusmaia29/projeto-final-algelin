# Projeto Final: Álgebra Linear - Regressão Linear em Vendas de Sorvete

## 📋 Resumo do Projeto

Um projeto completo de Álgebra Linear que implementa **regressão linear simples** para analisar a relação entre temperatura máxima diária e vendas de sorvete em São Paulo, utilizando dados reais do INMET.

## 📂 Arquivos

- **regressao_linear_vendas_sorvete.ipynb** - Notebook principal (Jupyter)
- **dataset/** - Pasta contendo dados de temperatura do INMET
- **README.md** - Este arquivo

## 🎯 Objetivos

✓ Aplicar conceitos de Álgebra Linear (matrizes, sistemas lineares, projeção ortogonal)  
✓ Implementar regressão linear usando mínimos quadrados ordinários (OLS)  
✓ Interpretar coeficientes no contexto real  
✓ Avaliar a qualidade do ajuste (R², RMSE)  
✓ Discutir limitações e hipóteses do modelo  

## 📊 Estrutura do Notebook

O notebook está organizado em **9 seções principais**:

1. **Introdução** - Contextualização e objetivos
2. **Análise Exploratória** - Estatísticas descritivas dos dados
3. **Modelagem Matemática** - Formulação teórica da regressão linear
4. **Forma Matricial** - Representação em forma matricial (y = Xβ + ε)
5. **Mínimos Quadrados** - Derivação e implementação da solução ótima
6. **Visualização** - Scatter plot e reta ajustada
7. **Resultados** - Coeficientes, R², RMSE e interpretações
8. **Limitações** - Pressupostos e restrições do modelo
9. **Conclusão** - Síntese e sugestões de extensão

## 🚀 Como Executar

### Requisitos
- Python 3.8+
- Jupyter Notebook ou JupyterLab
- Bibliotecas: numpy, pandas, matplotlib

### Instalação de Dependências
```bash
pip install numpy pandas matplotlib jupyter
```

### Executar o Notebook
```bash
jupyter notebook regressao_linear_vendas_sorvete.ipynb
```

Ou use o VS Code com a extensão Jupyter e abra diretamente.

## 📈 Principais Resultados

O notebook gera:
- ✓ Estatísticas descritivas de temperatura e vendas
- ✓ Coeficientes da regressão linear (β₀, β₁)
- ✓ Gráfico de scatter plot com reta ajustada
- ✓ Métricas de qualidade: R², RMSE, MAE
- ✓ Análise de resíduos (distribuição e independência)
- ✓ Interpretação prática: impacto de cada °C em vendas

## 🔑 Conceitos de Álgebra Linear Aplicados

1. **Matrizes e Operações**
   - Construção da matriz de design X
   - Multiplicação matricial (X^T X, X^T y)
   - Inversa de matriz (X^T X)^(-1)

2. **Sistemas Lineares**
   - Equação normal: β = (X^T X)^(-1) X^T y
   - Resolução estável de sistemas quadráticos

3. **Projeção Ortogonal**
   - Interpretação geométrica: projeção de y no espaço coluna de X
   - Resíduos são ortogonais ao espaço coluna

4. **Otimização**
   - Minimização de função quadrática (soma de quadrados)
   - Cálculo via derivada (gradiente zero)

## 📝 Dados

- **Fonte**: INMET (Instituto Nacional de Meteorologia) - Brasil
- **Período**: Janeiro-Fevereiro de 2026
- **Localização**: São Paulo - Mirante
- **Variável X**: Temperatura máxima diária (°C)
- **Variável Y**: Vendas de sorvete (simuladas, ~30 observações)

## 💡 Interpretação Prática

O modelo resultante segue a forma:

**Vendas = β₀ + β₁ × Temperatura**

Onde:
- **β₀** (intercepto): Vendas base quando temperatura = 0°C
- **β₁** (slope): Aumento em vendas por cada 1°C de aumento

## ⚠️ Limitações Reconhecidas

1. Assume relação linear (pode não ser realista em extremos)
2. Não modela fatores como: promoções, dias feriados, sazonalidade
3. Amostra limitada (30 observações de um período curto)
4. Extrapolação arriscada fora do intervalo observado
5. Não há garantia de causação, apenas correlação

## 🎓 Defesa Oral - Pontos-Chave

- Problema intuitivo e motivador
- Dados reais e relevantes (INMET)
- Abordagem didática com foco em fundamentals
- Resultados claros e interpretáveis
- Reconhecimento honesto de limitações
- Conexão clara com Álgebra Linear

##  Extensões Possíveis

Com mais tempo ou dados:
- Regressão múltipla (adicionar umidade, vento, etc.)
- Regressão polinomial (capturar não-linearidades)
- Séries temporais (detectar tendências e sazonalidade)
- Análise de outliers e influência de pontos
- Bootstrap para intervalo de confiança dos coeficientes

##  Autor

Oscar Rodrigues e Marcos Maia

## 📅 Data

Mai 2026

---

**Nota**: Todos os coeficientes e métricas são calculados dinamicamente pelo notebook ao executar. Os valores variarão ligeiramente dependendo da simulação de vendas.

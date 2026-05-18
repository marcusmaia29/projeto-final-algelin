# Projeto Final: Álgebra Linear - Regressão Linear em Vendas de Sorvete

## 📋 Resumo Executivo

**Título:** Análise da Relação entre Temperatura e Vendas de Sorvete usando Regressão Linear: Um Projeto Final de Álgebra Linear

**Objetivo:** Aplicar conceitos fundamentais de Álgebra Linear para modelar e resolver um problema real de previsão de demanda, demonstrando a conexão entre abstração matemática e aplicações práticas.

**Problema Real:** Uma sorveteria em São Paulo precisa prever demanda de vendas baseada em temperatura para otimizar estoque, pessoal e operações logísticas.

**Solução:** Regressão linear simples usando mínimos quadrados ordinários (OLS), implementado manualmente via operações matriciais (equação normal: $\boldsymbol{\beta} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$).

**Principais Resultados:** 
- Correlação forte positiva (r ≈ 0.83)
- R² ≈ 0.68 (68% de variância explicada)
- Equação ajustada: **Vendas = 49.2 + 14.8 × Temperatura**
- Interpretação: cada 1°C de aumento → ~15 unidades adicionais

## 📂 Arquivos do Projeto

### Núcleo do Trabalho
- **RELATORIO_IEEE.md** ⭐ - Relatório em formato IEEE (1 página + referências)
- **regressao_linear_vendas_sorvete.ipynb** - Notebook Jupyter com implementação completa
- **README.md** - Este arquivo (guia do projeto)

### Documentação de Suporte
- **APRESENTACAO_ORAL.md** - Roteiro para defesa/arguição
- **GUIA_TECNICO.md** - Explicação técnica implementação
- **FORMULAS_EQUACOES.md** - Referência matemática completa
- **INDICE.md** - Navegação e índice
- **dataset/** - Dados de temperatura do INMET (reais)

## � Relatório Acadêmico

O projeto inclui um **relatório em formato IEEE** (RELATORIO_IEEE.md) estruturado em seções padrão:

| Seção | Conteúdo |
|-------|----------|
| **Abstract** | Síntese em ~80 palavras |
| **I. Introdução** | Contexto, problema real, questão de pesquisa |
| **II. Metodologia** | Dados (INMET), modelagem matemática, mínimos quadrados |
| **III. Resultados** | Coeficientes, R², RMSE, interpretação prática |
| **IV. Discussão** | Pontos fortes, limitações, pressupostos verificados |
| **V. Conclusão** | Síntese, impacto, extensões futuras |
| **Referências** | 6 referências acadêmicas |

**Requisitos Atendidos:**
- ✅ Formato IEEE padrão
- ✅ 1 página de conteúdo (+ referências em página 2)
- ✅ Linguagem acadêmica
- ✅ Conclusões sustentadas por fatos
- ✅ Referências críticas

---

## 🎓 Relatório Acadêmico - Estrutura IEEE

O arquivo **RELATORIO_IEEE.md** contém um relatório completo e formatado em padrão IEEE:

**Seções do Relatório:**
- **Abstract** (~80 palavras): Síntese executiva
- **I. Introdução**: Problema real, questão de pesquisa, relevância
- **II. Metodologia**: Dados (INMET), modelagem matemática, solução
- **III. Resultados**: Coeficientes, R², RMSE, interpretação prática
- **IV. Discussão**: Análise crítica, limitações, pressupostos
- **V. Conclusão**: Síntese, impacto, extensões futuras
- **Referências**: 6 referências acadêmicas selecionadas

**Características:**
- ✅ Formato padrão IEEE
- ✅ 1 página de conteúdo (referências em página 2, se necessário)
- ✅ Linguagem acadêmica e objetiva
- ✅ Conclusões sustentadas por dados
- ✅ Referências tratadas criticamente

**Para avaliação de grupo:** O professor avaliará qualidade técnica, conteúdo completo, linguagem apropriada, e tratamento crítico de referências.

---

## 🔬 Como Funciona o Projeto (Etapas)

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

## 🎤 Instruções para Arguição Individual

A arguição individual é onde **você defende suas decisões de projeto** e **interpreta os resultados**.

### O Que o Professor Avaliará

✅ **Compreensão Matemática**
- Você entende por que usar mínimos quadrados?
- Pode explicar a equação normal?
- Sabe por que X^T e = 0 (ortogonalidade)?

✅ **Implementação Técnica**
- Como as matrizes foram construídas?
- Por que inverter X^T X?
- Pode rastrear um cálculo do começo ao fim?

✅ **Interpretação de Resultados**
- O que significam β₀ = 49.2 e β₁ = 14.8?
- Como o modelo ajuda a sorveteria?
- Por que R² = 0.68 é razoável?

✅ **Discussão Crítica de Limitações**
- Quais pressupostos OLS são violados?
- O que o modelo não captura?
- Quando ele falha?

✅ **Conexão Teórico-Prática**
- Como Álgebra Linear resolve este problema?
- Qual é a interpretação geométrica?
- Como a teoria conecta com negócio?

### Documentos para Preparar a Arguição

1. **APRESENTACAO_ORAL.md** 
   - Roteiro completo de 10-15 minutos
   - 8 perguntas frequentes com respostas prontas
   - Dicas de apresentação

2. **FORMULAS_EQUACOES.md**
   - Todas as fórmulas em um só lugar
   - Checklist de cálculos
   - Referência rápida

3. **GUIA_TECNICO.md**
   - Explicação técnica passo a passo
   - Conceitos de AL demonstrados
   - Verificações numéricas

### Nota Individual

Será calculada baseada em:
- Domínio técnico do modelo matemático
- Qualidade das explicações e respostas
- Capacidade de responder perguntas de aprofundamento
- Demonstração de entendimento genuíno (não decorado)
- Honestidade ao reconhecer limitações

---

**Nota**: Todos os coeficientes e métricas são calculados dinamicamente pelo notebook ao executar. Os valores variarão ligeiramente dependendo da simulação de vendas.

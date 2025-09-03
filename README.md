# Estatísticas para Devs — Projeto

Este repositório acompanha a aula da Rocketseat "Machine Learning em Inteligência Artificial" e contém exemplos práticos em um notebook (`estatistica_devs.ipynb`) sobre medidas estatísticas básicas e visualizações com pandas/matplotlib.

## Objetivo

Reunir, explicar e exemplificar os conceitos abordados até a seção "Representação Gráfica":

- Medidas de posição
- Medidas de dispersão
- Medidas de forma
- Correlações
- Representação gráfica (histograma, barras, scatter, boxplot, linha)

## Requisitos

- Python 3.8+ (recomendado 3.11)
- pipenv (opcional, há `Pipfile` no repositório) ou um ambiente virtual de sua preferência
- Dependências principais: `pandas`, `matplotlib`

Instalação rápida (Windows - PowerShell):

```powershell
# usando pipenv (se preferir virtualenv, crie/ative o venv e use 'pip install -r requirements.txt')
pipenv install --python 3.11
pipenv install pandas matplotlib
pipenv shell
```

Ou com pip numa venv:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install pandas matplotlib
```

## Estrutura do projeto

- `estatistica_devs.ipynb` — notebook com todos os exemplos executáveis
- `Pipfile`, `Pipfile.lock` — ambiente (opcional)

## Conteúdo e exemplos práticos

A seguir há um resumo dos conceitos e os trechos de código usados no notebook. Essas células já estão no `estatistica_devs.ipynb` e podem ser executadas conforme estão.

### 1) Medidas de Posição

- Média (mean)
- Mediana (median)
- Moda (mode)

Exemplo (DataFrame `df_medidas`):

```python
# Supondo df_medidas com colunas 'idade' e 'altura'
df_medidas['idade'].mean()
df_medidas['idade'].median()
df_medidas['idade'].mode()
```

### 2) Medidas de Dispersão

- Variância (var)
- Desvio padrão (std)
- Coeficiente de variação (std/mean \* 100)

Exemplo:

```python
df_medidas.idade.var()
df_medidas.idade.std()
(df_medidas.idade.std() / df_medidas.idade.mean()) * 100
```

### 3) Medidas de Forma

- Assimetria (skew)
- Curtose (kurtosis)

Exemplo:

```python
df_medidas.idade.skew()
df_medidas.idade.kurtosis()
```

Também é útil usar `describe()` para um resumo completo:

```python
df_medidas.idade.describe()
```

### 4) Correlações

- Correlação de Pearson
- Correlação de Spearman

Exemplo:

```python
# correlação entre colunas do dataframe
df_medidas.corr(method='pearson')
# correlação entre duas séries
df_medidas.idade.corr(df_medidas.altura)
# spearman
df_medidas.corr(method='spearman')
```

### 5) Representação Gráfica (visualizações com pandas/matplotlib)

- Histograma: `Series.hist()`
- Gráfico de barras vertical: `DataFrame.plot.bar()`
- Gráfico de barras horizontal: `DataFrame.plot.barh()`
- Gráfico de dispersão: `DataFrame.plot.scatter()`
- Boxplot: `Series.plot.box()`
- Gráfico de linha (séries temporais): `DataFrame.plot.line()`

Exemplos presentes no notebook:

```python
# Histograma (idade)
df_medidas.idade.hist()

# Barras (vendas)
df_vendas.plot.bar(x='categoria', y='valor')
# Barras horizontais (quantidade)
df_vendas.plot.barh(x='categoria', y='quantidade')

# Dispersão
df_medidas.plot.scatter(x='idade', y='altura')

# Boxplot
df_medidas.idade.plot.box()

# Séries temporais (faturamento)
df_faturamento['data_ref'] = pd.to_datetime(df_faturamento['data_ref'])
df_faturamento.plot.line(x='data_ref', y='valor')
```

Observações sobre visualização:

- Para melhorar estilo e salvar figuras, use `matplotlib.pyplot` (import como `plt`) e chame `plt.show()` ou `plt.savefig('nome.png')`.
- Para notebooks, `%matplotlib inline` (ou configuração do backend) já garante a renderização embutida.

## Dados de exemplo usados no notebook

- df_medidas: dicionário com `idade` e `altura` (pequeno exemplo para cálculo de medidas)
- df_vendas: dicionário com `categoria`, `valor`, `quantidade` (gráficos de barras)
- df_faturamento: série temporal com `data_ref` e `valor` (gráfico de linhas)

## Contrato mínimo (inputs/outputs)

- Inputs: DataFrames do pandas com colunas numéricas.
- Outputs: Números (medidas estatísticas) e plots (objetos matplotlib exibidos/salvos).
- Erros comuns: colunas com tipos incorretos (ex.: datas como string — converter com `pd.to_datetime`), colunas com NaNs (usar `dropna()` ou `fillna()` antes de aplicar certas métricas).

## Casos de borda importantes

- Colunas vazias/nulas -> verificar/remover antes de calcular média/mediana
- Pequenas amostras -> medidas como curtose/assimetria podem ser instáveis
- Tipos incorretos (strings em colunas numéricas ou datas)

## Como usar este repositório

1. Abra o `estatistica_devs.ipynb` no Jupyter / VS Code
2. Instale dependências conforme seção "Requisitos"
3. Execute as células na ordem (os DataFrames de exemplo são criados nas primeiras células)

---

## Status das demandas solicitadas

- Medidas de posição: Done
- Medidas de dispersão: Done
- Medidas de forma (assimetria/curtose): Done
- Correlação (pearson/spearman): Done
- Representação gráfica até "Representação Gráfica": Done

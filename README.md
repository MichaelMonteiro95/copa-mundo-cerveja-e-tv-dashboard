# copa-mundo-cerveja-e-tv-dashboard
📊 Dashboard Power BI analisando o impacto da Copa do Mundo no consumo de cerveja e vendas de TV (2006–2024) | Kirin Holdings · Jefferies · GfK · FIFA2026 🍺⚽
# ⚽ Copa do Mundo | Impacto em consumo de Cerveja e TV — 2006 a 2024

Dashboard desenvolvido em Power BI analisando a correlação entre as edições da Copa do Mundo e o comportamento de consumo de cerveja e vendas de TV globalmente, com recortes para o Brasil e análise por campanha das seleções.

> Comecei a acompanhar a Copa do Mundo em 2006 — e desde lá os dados já estavam me dizendo algo. Esse projeto nasceu da vontade de juntar três coisas que amo: **Copa do Mundo, Dados e Cerveja** 🍺

---

## 📊 Visão geral do dashboard

| Indicador | Valor |
|---|---|
| Crescimento de cerveja em anos de Copa (mundo) | ▲ 2,3% |
| Crescimento de cerveja no país sede (sem Qatar) | ▲ 5,0% |
| Crescimento de cerveja no Brasil em anos de Copa | ▲ 5,0% |
| Crescimento de TV em anos de Copa (mundo) | ▲ 2,7% |
| Diferença cerveja Copa vs demais anos (Brasil) | 🟢 4,5 p.p |
| Diferença cerveja por campanha (≥ Quartas vs ≤ Oitavas) | 🟢 5,9 p.p |
| Diferença TV Copa vs demais anos | 🟢 3,0 p.p |

---

## 📁 Estrutura dos arquivos

```
📂 copa_dashboard/
├── 01_consumo_global_copa_vs_normal.csv
├── 02_efeito_anfitriao_cerveja.csv
├── 03_brasil_copa_vs_normal.csv
├── 04_forca_selecao_x_consumo.csv
├── 05_campeas_efeito_cerveja.csv
├── 06_vendas_tv_mundo_copa_vs_normal.csv
├── 07_dispersao_selecoes_copa2022_cerveja.csv
├── 08_carne_esportivos_copa.csv
└── README.md
```

---

## 📋 Descrição das bases

### 01 · Consumo global de cerveja — Copa vs anos normais
Série histórica de 2004 a 2024 com o consumo global de cerveja em milhões de kilolitros. Anos de Copa sinalizados para comparação direta com anos normais. Inclui marcação do período COVID-19 (2020).

- **Coluna-chave:** `tipo_ano` (Copa / Normal)
- **Métrica principal:** `consumo_global_milhoes_kl`
- **Uso no dashboard:** linha temporal principal + cálculo do multiplicador

### 02 · Efeito anfitrião — cerveja no país sede
Crescimento percentual de consumo de cerveja especificamente no país anfitrião em cada edição da Copa (2006–2022), comparado com o crescimento global do mesmo ano.

- **Coluna-chave:** `crescimento_host_pct` vs `crescimento_global_pct`
- **Atenção:** Qatar 2022 é outlier (mercado era altamente restrito antes — dado não comparável com as demais edições)

### 03 · Brasil — Copa vs anos normais
Consumo de cerveja no Brasil de 2010 a 2023, com fase atingida pela seleção brasileira em cada Copa. Permite correlacionar resultado em campo com comportamento de consumo.

- **Coluna-chave:** `brasil_anfitriao` (Sim/Não), `fase_eliminacao_br`
- **Destaque:** 2014 (anfitrião + semifinalista) = maior pico histórico

### 04 · Força da seleção anfitriã × consumo
Cruzamento entre a fase que o país anfitrião atingiu na Copa e o crescimento de consumo de cerveja naquele país. Base para o scatter plot de correlação.

- **Coluna-chave:** `fase_anfitriao`, `crescimento_cerveja_host_pct`
- **Insight:** correlação positiva — anfitriões que avançam mais geram mais consumo

### 05 · Países campeões — efeito no consumo
Crescimento de cerveja no país campeão no ano da conquista e no ano seguinte. Mostra o "efeito celebração" pós-título.

- **Destaque:** França 2018 (+2,7%) e Argentina 2022 (+3,2%) são os casos mais expressivos
- **Caso negativo:** Itália 2006 (−0,5%) — Copa foi na Alemanha, efeito limitado fora do host

### 06 · Vendas de TV — série histórica 2004–2024
Crescimento anual (YoY) de vendas de TV globalmente, com anos de Copa sinalizados. Inclui dados por mercado (global, UK online, UAE) onde disponíveis.

- **Coluna-chave:** `tipo_ano`, `copa_verao_ou_inverno`
- **Atenção:** dados globais de 2006 são estimativa. Dados de UK (IMRG) e UAE (GfK) para 2014 são verificados em fonte primária.

### 07 · Dispersão — seleções da Copa 2022 × consumo
Base principal do scatter plot. Cruza a fase atingida por cada seleção na Copa 2022 com a variação de consumo de cerveja no respectivo país (2021→2022).

- **Coluna-chave:** `codigo_fase` (1=Grupos … 7=Campeão), `variacao_pct`
- **Insight:** seleções que foram às quartas ou além cresceram em média 7,9% vs 1,4% das que saíram antes
- **Confiabilidade:** dados de EUA, Brasil, México, Alemanha, Espanha e Polônia são diretos do Kirin Holdings. Demais países são estimativas baseadas nos agregados regionais do relatório.

### 08 · Carne e material esportivo — efeito Copa
Dados de crescimento de vendas de carne (BBQ) e material esportivo (Nike, Adidas) em anos de Copa. Base complementar para análise de comportamento de consumo ampliado.

- **Destaque verificado:** Nike +13% de receita no trimestre pré-Copa 2014 · Adidas meta de €400M na Copa 2022
- **Atenção:** dados de carne são setoriais e de menor precisão — use com ressalva

---

## ⚠️ Limitações e transparência metodológica

1. **Qatar 2022 é outlier em cerveja** — crescimento de 26% não é comparável com as demais edições. O mercado era altamente restrito antes da Copa. Excluído das médias no dashboard.

2. **Dados de TV são fragmentados** — não existe série temporal global unificada e gratuita. Os dados de UK (IMRG/Capgemini) são os mais consistentes para Copa de verão.

3. **Correlação ≠ causalidade** — o crescimento de cerveja em anos de Copa reflete múltiplos fatores: recuperação econômica, sazonalidade, inflação, recuperação pós-COVID. A Copa é um driver importante, não a única variável.

4. **Estimativas sinalizadas** — colunas com `confiabilidade = "Estimativa"` são baseadas em agregados regionais do Kirin Holdings, não em dados país a país publicados diretamente.

5. **Nenhum dado veio de API** — todas as fontes são relatórios anuais públicos ou análises de bancos de investimento citadas na imprensa especializada.

---

## 🔍 Fontes

| Fonte | Uso |
|---|---|
| **Kirin Holdings** – Global Beer Consumption Report (anual, 2006–2023) | Consumo global e por país de cerveja |
| **Jefferies Research** | Crescimento de cerveja em anos de Copa no host |
| **Barclays Analysis** | Efeito Copa em cidades-sede (citado por mexicobusiness.news, jan 2026) |
| **GfK** | Mercado global de TV e dados UAE |
| **IMRG / Capgemini** – e-Retail Sales Index | Vendas online de TV no UK |
| **BBPA** – British Beer & Pub Association | Consumo de cerveja UK em 2018 |
| **William Hill News** (abr 2026) | Projeções Copa 2026 para TV |
| **Nike IR / Adidas Annual Report** | Dados de material esportivo |
| **FIFA Rankings** | Classificação das seleções |

---

## 🛠️ Como usar

1. Baixe os arquivos `.csv`
2. Importe no Power BI via **Obter Dados → Texto/CSV**
3. Relacione as tabelas pela coluna `ano` (01, 03, 06) e `edicao` (02, 04, 05)
4. Recrie ou adapte os visuais conforme sua análise

---

## 📬 Contato

Desenvolvido como projeto pessoal de análise de dados com tema Copa do Mundo 2026.  
Feedbacks, correções e contribuições são bem-vindos — abra uma issue ou entre em contato pelo LinkedIn.

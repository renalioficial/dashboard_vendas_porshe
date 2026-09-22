# 🏎️ Porsche Sales Intelligence & Data Pipeline

Um dashboard interativo e standalone para análise executiva e projeção de vendas de veículos Porsche, alimentado por um pipeline rigoroso de sanitização e padronização de dados.

![Versão](https://img.shields.io/badge/version-1.0.0-red.svg)
![Tecnologias](https://img.shields.io/badge/tech-HTML5%20%7C%20CSS3%20%7C%20JS--Vanilla%20%7C%20SVG-informational)
![Licença](https://img.shields.io/badge/license-MIT-green.svg)

---

## 📌 Visão Geral

Este projeto é uma solução completa de **Business Intelligence (BI)** composta por duas frentes principais:

1. **Pipeline de Sanitização e Qualidade de Dados (Data Cleansing):** Mapeamento e tratamento de dados brutos (datas, valores numéricos, localizações e modelos) convertendo *inputs* não estruturados ou inconsistentes para um esquema canônico limpo.
2. **Dashboard Interativo Single-File (`index.html`):** Interface dinâmica na paleta visual da marca (*O negócio em vermelho*) com filtros em tempo real, cálculo de KPIs, gráficos dinâmicos em SVG e regressão linear simples para projeção de vendas a 3 anos.

---

## 📊 Arquitetura do Dashboard

O painel é construído em arquitetura **Single Page Application (SPA)** leve, sem dependências externas (Zero frameworks/libraries JavaScript) e renderizado via SVG nativo.

### Principais Indicadores (KPIs)
* **Faturamento Total:** Soma das vendas no recorte atual em USD (`SalesPriceSanitized`).
* **Volume de Vendas:** Total de registros validados.
* **Ticket Médio:** Razão entre faturamento e volume total de vendas.
* **Projeção de 3 Anos:** Estimativa de volume acumulado para os próximos três ciclos com base na tendência linear dos dados históricos.

### Módulos e Gráficos
* **Evolução Histórica por Modelo (Linha/SVG):** Acompanha a performance de vendas ao longo dos anos de fabricação (`ModelYearSanitized`).
* **Análise de Projeção Estatística:** Gráfico de tendência linear baseada na série histórica anual.
* **Mix de Pagamento:** Distribuição percentual das formas de pagamento (`PayMethodSanitized`).
* **Receita por Região:** Volume financeiro por macrorregião derivada de `StateSanitized`.
* **Insights Executivos Automáticos:** Leitura interpretativa gerada dinamicamente conforme os filtros selecionados.

---

## 🧹 Esquema e Regras de Sanitização de Dados

O modelo de dados processa colunas brutas (*Raw Columns*) e gera colunas padronizadas (*Sanitized Columns*).

### Mapeamento de Colunas

| Coluna Origem | Coluna Sanitizada | Formato Final / Tipo | Exemplo de Regra |
|---|---|---|---|
| `sale_date` | `SaleDateSanitized` | `YYYY-MM-DD` / `INVALID` | Datas inválidas (ex: `2024-13-05`) tornam-se `INVALID`. |
| `porsche_model` | `PorscheModelSanitized` | Texto (Title Case Canônico) | Normalização de trims (`911 Turbo S`, `Macan Electric`). |
| `model_year` | `ModelYearSanitized` | `YYYY` / `INVALID` | Converte texto ("twenty twenty four") ou formatos ("20-24") em 4 dígitos. |
| `sale_price` | `SalesPriceSanitized` | Decimais em USD (`0.00`) | Remove símbolos e trata sufixos ("188k USD" -> `188000.00`). |
| `vehicle_mileage` | `VehicleMileageSanitized` | Inteiro (Milhas) | Converte KM para milhas (`1 km = 0.621371 mi`) e trata termos ("new" -> `0`). |
| `payment_method` | `PayMethodSanitized` | Categorias controladas | `Credit Card`, `Wire Transfer`, `Crypto Payment`, etc. |
| `city` | `CitySanitized` | Texto (Title Case) | Padronização de maiúsculas/minúsculas e pontuações. |
| `state` | `StateSanitized` | Código USPS (2 letras) / `INVALID` | Normaliza nomes e siglas ("California", "ca" -> `CA`). |
| `delivery_status` | `DeliveryStatusSanitized` | Categorias controladas | Trata erros ortográficos e acentuação (`Delivered`, `In Transit`, etc.). |

---

## 🚀 Como Executar o Projeto

Como o dashboard é um arquivo HTML autocontido com CSS e JavaScript integrados, nenhum servidor ou gerenciador de pacotes (como Node.js/npm) é necessário.

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/porsche-sales-intelligence.git
   ```
2. Navegue até o diretório do projeto:
   ```bash
   cd porsche-sales-intelligence
   ```
3. Abra o arquivo `index.html` em qualquer navegador moderno:
   * No Windows: dê dois cliques no arquivo `index.html`.
   * No macOS/Linux via terminal:
     ```bash
     open index.html   # macOS
     xdg-open index.html # Linux
     ```

---

## 🛠️ Tecnologias Utilizadas

* **HTML5:** Estruturação semântica.
* **CSS3:** Estilização customizada com variáveis CSS, CSS Grid, Flexbox e Tipografia Century Gothic.
* **JavaScript (ES6+):** Manipulação DOM, filtragem de arrays em tempo real, algoritmo de regressão linear (`npfit`) e geração estática/dinâmica de SVG.
* **SVG Nativo:** Gráficos de linha e projeções vetoriais sem bibliotecas externas.

---

## 📄 Licença

Este projeto está sob a licença [MIT](LICENSE). Sinta-se à vontade para usar e adaptar o código para suas próprias necessidades.
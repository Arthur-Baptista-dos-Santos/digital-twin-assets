# `Digital Twin Assets: Visualizacao Operacional e RPA`

> Digital Twin de ativos industriais com 5 paginas: navegacao hierarquica Planta-Area-Ativo, dashboard de sensores em tempo real, cadastro CRUD com exportacao, central de automacoes RPA e pipeline OCR de placas de motor. Sprint 2 do projeto Forzy, FIAP 2026.

---

## `Tecnologias`

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Streamlit](https://img.shields.io/badge/Streamlit-1.35+-ff4b4b)
![SQLite](https://img.shields.io/badge/SQLite-banco%20local-lightgrey)
![Plotly](https://img.shields.io/badge/Plotly-graficos-purple)
![Pandas](https://img.shields.io/badge/pandas-2.0+-green)
![License](https://img.shields.io/badge/license-MIT-green)

---

## `O que faz`

Representa o estado digital de ativos industriais (motores) com:

- Navegacao hierarquica: Planta > Area > Ativo com mapa visual
- Dashboard de sensores: gauges em tempo real + historico de 5 sensores (tensao, corrente, temperatura, RPM, vibracao)
- Cadastro CRUD: registro, edicao e exportacao de ativos
- Central RPA: automacao de associacao TAG/localizacao + coleta de dados
- Pipeline OCR: extrai dados de placas de motor por imagem e grava no banco

---

## `Arquitetura`

```
app.py (inicializacao + BD SQLite)
    |
    +-- pages/
    |       1_Navegacao.py      hierarquia Planta → Area → Ativo
    |       2_Dashboard.py      gauges Plotly + graficos temporais de sensores
    |       3_Cadastro.py       CRUD de ativos + exportacao CSV
    |       4_RPA.py            central de automacoes RPA com log de execucao
    |       5_Pipeline.py       OCR Placa → normalizacao → banco de dados
    |
    +-- rpa/
    |       tag_association.py      associacao automatica TAG/Localizacao
    |       record_updater.py       atualizacao em lote de registros
    |       nameplate_pipeline.py   pipeline placa do motor
    |
    +-- utils/
    |       mock_data.py            gerador de dados simulados de sensores
    |       charts.py               componentes visuais Plotly reutilizaveis
    |
    +-- database.py                 camada SQLite: plantas, areas, ativos, leituras, log_rpa
```

---

## `Banco de dados`

```sql
plantas
    id, nome, localizacao, descricao

areas
    id, planta_id, nome, codigo, tipo

ativos
    id, area_id, tag, nome, fabricante, modelo, tensao_nominal,
    corrente_nominal, potencia_kw, status, data_instalacao

leituras_sensores
    id, ativo_id, timestamp, tensao, corrente, temperatura,
    rpm, vibracao, potencia, fator_potencia

log_rpa
    id, timestamp, automacao, status, detalhes
```

---

## `Sensores monitorados`

| Sensor | Unidade | Faixa normal |
|--------|---------|-------------|
| Tensao | V | 380-440 |
| Corrente | A | depende do ativo |
| Temperatura | C | < 80 |
| Rotacao | RPM | 1750-1800 |
| Vibracao | mm/s | < 4.5 (ISO 10816 Zona A) |
| Potencia | kW | depende do ativo |
| Fator de Potencia | - | > 0.85 |

---

## `Estrutura`

```
digital-twin-assets/
├── app.py
├── database.py
├── requirements.txt
├── pages/
│   ├── 1_Navegacao.py
│   ├── 2_Dashboard.py
│   ├── 3_Cadastro.py
│   ├── 4_RPA.py
│   └── 5_Pipeline.py
├── rpa/
│   ├── tag_association.py
│   ├── record_updater.py
│   └── nameplate_pipeline.py
└── utils/
    ├── mock_data.py
    └── charts.py
```

---

## `Instalacao`

```bash
git clone https://github.com/Arthur-Baptista-dos-Santos/digital-twin-assets.git
cd digital-twin-assets

python -m venv .venv
.venv\Scripts\activate       # Windows
# source .venv/bin/activate  # Linux/Mac

pip install -r requirements.txt
streamlit run app.py
```

Acesse `http://localhost:8501`. O banco SQLite e criado automaticamente na primeira execucao.

---

## `Roadmap Forzy`

| Sprint | Foco | Repo |
|--------|------|------|
| Sprint 1 | Cadastro e visualizacao de ativos | `motor-sync` |
| Sprint 2 (este) | Digital Twin: RPA + sensores + pipeline OCR | `digital-twin-assets` |

---

## `Conceitos aplicados`

- **`Digital Twin`**: representacao digital do estado fisico de cada ativo em tempo real
- **`RPA (Robotic Process Automation)`**: automacoes que associam TAGs, atualizam registros em lote e extraem dados de placas
- **`SQLite`**: banco local com schema relacional (plantas > areas > ativos > leituras)
- **`Plotly gauges`**: visualizacao de valores de sensores em tempo real com limites configurados
- **`Pipeline OCR`**: extrai texto de imagens de placas de motor e mapeia campos para o banco

---

## `Licenca`

Distribuido sob a licenca MIT. Veja [LICENSE](LICENSE) para mais informacoes.

---

## `Autor`

**Arthur Baptista dos Santos**
RM 565346 · Inteligencia Artificial · FIAP 2025-2026

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Arthur%20Baptista-0077B5?logo=linkedin)](https://linkedin.com/in/arthur-baptista-dos-santos)
[![GitHub](https://img.shields.io/badge/GitHub-Arthur--Baptista--dos--Santos-181717?logo=github)](https://github.com/Arthur-Baptista-dos-Santos)

# Nexus MACBETH — Elicitação Qualitativa e Programação Linear

Este repositório é o módulo independente do ecossistema **NEXUS MCDM**, configurado para operar exclusivamente com o método **MACBETH**.

---

## 🎨 Identidade Visual e Branding
- **Nome Oficial:** Nexus MACBETH
- **Cores Oficiais:** Âmbar (`#F59E0B`) e Azul Escuro (`#1E3A8A`)
- **Conceito Visual:** Blocos de intervalos de atratividade qualitativa representando a escala ordinal-cardinal.
- **Copyright:** Direitos Reservados © 2026 NEXUS-MCDM. Todos os direitos reservados.

---

## 🧠 Formulação Matemática e Funcionamento

O **MACBETH (Measuring Attractiveness by a Categorical Based Evaluation Technique)** é um método qualitativo e ordinal-cardinal que gera escalas cardinais a partir de julgamentos verbais sobre a diferença de atratividade entre duas alternativas ou critérios.

### 1. Escala Semântica de Atratividade
O decisor preenche a matriz de julgamentos par a par expressando a diferença de atratividade nas seguintes categorias semânticas:
* $C_0$ ou $no$: Sem atratividade (igual)
* $C_1$ ou $very\ weak$: Atratividade muito fraca
* $C_2$ ou $weak$: Atratividade fraca
* $C_3$ ou $moderate$: Atratividade moderada
* $C_4$ ou $strong$: Atratividade forte
* $C_5$ ou $very\ strong$: Atratividade muito forte
* $C_6$ ou $extreme$: Atratividade extrema

### 2. Formulação por Programação Linear (PL)
Para extrair um vetor de pesos cardinal a partir da matriz de julgamentos ordinais qualitativos, formulamos um problema de otimização de forma a maximizar a separabilidade $\sigma$ entre os níveis de julgamentos:
$$\max \sigma$$
$$\text{sujeito a:}$$
$$v(a_i) - v(a_j) \ge 1, \quad \forall a_i \text{ mais atrativo que } a_j \quad (a_{ij} \neq no)$$
$$v(a_i) - v(a_j) - \sigma \cdot h(a_{ij}) \ge 0, \quad \forall a_i, a_j$$
$$v(a^+) = 100$$
$$v(a^-) = 0$$
Onde:
* $v(a_i)$ é a utilidade a ser gerada para cada elemento $i$.
* $a^+$ representa o critério ou alternativa de maior relevância de referência.
* $a^-$ representa a pior referência (âncoras de normalização entre 0 e 100).
* $h(a_{ij})$ é um degrau de penalização proporcional ao salto de atratividade qualitativo informado.

Caso a Programação Linear encontre uma solução viável ($\sigma > 0$), a matriz é considerada consistente e os pesos cardinais ótimos são extraídos diretamente do vetor de variáveis de decisão normalizado.

---

## 🚀 Instalação e Execução
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python app.py
```
Acesse: `http://127.0.0.1:5000`

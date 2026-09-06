# Consensus Engine & Confidence Score

## Consensus Engine

### Entrada
Análises independentes de cada agente (Grok, Manus, futuros).

Cada análise contém:
- market
- selection
- probability (0-1)
- confidence (0-100)
- reasoning
- risks

### Regras de Classificação

#### 🔥 CONSENSO FORTE
- Todos os agentes ativos concordam na **mesma seleção**
- Diferença máxima de probabilidade entre agentes ≤ 12%
- Nenhum risco crítico identificado por nenhum agente
- Score médio de confiança ≥ 70

#### 🟡 CONSENSO PARCIAL
- Agentes concordam na seleção
- Mas diferença de probabilidade > 12% **ou**
- Um dos agentes tem confiança significativamente menor

#### 🔴 DIVERGÊNCIA
- Agentes recomendam seleções diferentes
- Resultado automático: **NO BET**

---

## Confidence Score (0-100)

Composição sugerida:

| Fator                    | Peso |
|--------------------------|------|
| Consenso das IAs         | 25   |
| Estatísticas             | 20   |
| Forma recente            | 10   |
| Casa / Fora              | 10   |
| Desfalques / Escalações  | 10   |
| Motivação / Contexto     | 10   |
| Valor da odd (EV)        | 5    |
| Histórico do modelo      | 5    |
| Movimentação de odds     | 5    |
| **Total**                | 100  |

### Classificação Final

| Score   | Classificação     | Ação          |
|---------|-------------------|---------------|
| 90-100  | 🔥 ELITE          | Destacar      |
| 80-89   | 🟢 MUITO FORTE    | Recomendar    |
| 70-79   | 🟡 INTERESSANTE   | Mostrar       |
| 60-69   | ⚠️ RISCO          | Opcional      |
| < 60    | ❌ DESCARTAR      | Não mostrar   |

---

## Value Engine

```
Implied Probability = 1 / odd
EV = (estimated_prob × odd) - 1
Value = estimated_prob - implied_prob
```

Só considerar Value Bet quando:
- EV > 0
- Consensus não for divergência
- Confidence Score ≥ limite configurado

---

## No Bet Filter (obrigatório)

Descartar automaticamente se:
- Divergência entre agentes
- Dados insuficientes / qualidade baixa
- Escalações muito incertas
- Amostra estatística pequena
- Conflito forte entre estatísticas e contexto
- Odd sem valor e sem consenso forte

**Regra de ouro:** Preferir NO BET a forçar tip.

# Database Schema — Marins TIPS

## Visão Geral

PostgreSQL como banco principal.

Todas as tabelas usam `created_at` e `updated_at`.
IDs são UUID ou serial conforme o caso.

---

## Tabelas Principais

### sports
- id
- name (Football, Basketball...)
- slug

### leagues
- id
- sport_id
- name
- country
- slug
- priority (para ranking de importância)

### teams
- id
- league_id
- name
- short_name
- slug

### matches
- id
- league_id
- home_team_id
- away_team_id
- kickoff_at (timestamptz)
- status (scheduled, live, finished, postponed)
- home_score
- away_score
- round
- season
- venue

### match_statistics
- id
- match_id
- team_id
- possession
- shots
- shots_on_target
- corners
- fouls
- yellow_cards
- red_cards
- xg
- (outros campos conforme fonte)

### injuries
- id
- team_id
- player_name
- injury_type
- status (out, doubtful, suspended)
- impact (low, medium, high)
- reported_at

### news
- id
- team_id (nullable)
- match_id (nullable)
- title
- content
- sentiment (positive, neutral, negative)
- source
- published_at

### odds
- id
- match_id
- market (1x2, over_under, btts, handicap...)
- selection
- bookmaker
- odd_value
- implied_prob
- captured_at

### odds_history
- id
- odds_id
- odd_value
- captured_at

---

## Análise e Consenso

### ai_analyses
- id
- match_id
- agent (grok, manus, statistical)
- model_version
- prompt_version
- market
- selection
- probability (0-1)
- confidence (0-100)
- reasoning (text)
- risks (jsonb)
- data_timestamp (point-in-time)
- created_at

### consensus_results
- id
- match_id
- market
- selection
- consensus_type (strong, partial, divergence)
- avg_probability
- consensus_score (0-100)
- agents_agreed (jsonb)
- final_recommendation (boolean)
- created_at

### confidence_scores
- id
- match_id
- market
- selection
- total_score (0-100)
- breakdown (jsonb) — pesos de cada fator
- classification (elite, very_strong, interesting, risk, discard)
- created_at

### value_bets
- id
- match_id
- market
- selection
- estimated_prob
- implied_prob
- odd_value
- ev
- value_score
- created_at

---

## Tips e Histórico

### tips
- id
- match_id
- market
- selection
- odd_at_tip
- estimated_prob
- confidence_score
- consensus_type
- classification
- ev
- status (pending, green, red, void, cancelled)
- reasoning_summary
- risks_summary
- agents_data (jsonb)
- created_at
- settled_at

### tip_results
- id
- tip_id
- result (green, red, void)
- profit_units
- closing_odd
- clv
- settled_at

---

## Performance e Aprendizado

### agent_performance
- id
- agent
- market
- league_id (nullable)
- period_start
- period_end
- total_tips
- greens
- reds
- win_rate
- roi
- avg_clv
- avg_ev

### strategies
- id
- name
- rules (jsonb)
- min_score
- min_consensus
- min_ev
- active

### backtests
- id
- strategy_id
- period_start
- period_end
- results (jsonb)
- created_at

---

## Sistema

### users
- id
- email
- role (admin, analyst, viewer)

### audit_logs
- id
- action
- entity
- entity_id
- data (jsonb)
- created_at

---

## Observações

- Todos os dados de análise devem guardar `data_timestamp` (point-in-time).
- Nunca sobrescrever análises antigas com dados futuros.
- Odds e estatísticas são versionadas por timestamp.

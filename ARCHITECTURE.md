# Arquitetura — Marins TIPS (TIPMASTER AI)

## Visão Geral

Marins TIPS evolui para um **motor de análise esportiva multiagente** baseado em consenso entre IAs.

O sistema não existe para forçar palpites.  
Ele existe para encontrar **oportunidades de alta qualidade** ou declarar honestamente **NO BET**.

---

## Princípios Fundamentais

1. **Multiagente independente**  
   Cada IA (Grok, Manus, futuros) analisa sem ver a conclusão da outra.

2. **Consensus Engine**  
   Compara as análises e classifica o nível de acordo.

3. **Score de Confiança (0-100)**  
   Combina consenso + estatísticas + contexto + valor.

4. **Value Detection**  
   Compara probabilidade estimada vs probabilidade implícita da odd.

5. **No Bet Filter**  
   Prefere não recomendar do que recomendar com baixa confiança.

6. **Histórico verificável**  
   Toda tip é registrada com o estado do conhecimento no momento da análise (point-in-time).

---

## Fluxo Diário (Scheduler)

```
06:00  → Buscar jogos do dia (principais ligas)
06:10  → Atualizar estatísticas e forma
06:20  → Buscar notícias e desfalques
06:30  → Buscar odds
06:40  → Agente Grok analisa
06:50  → Agente Manus analisa
07:00  → Consensus Engine + Score + Value
07:05  → Ranking final + publicação
```

Durante o dia: reanálise automática em caso de mudança relevante (escalação, odd forte, notícia).

Após os jogos: registro de resultados + atualização de métricas.

---

## Componentes Principais

### 1. Data Layer
- SportsDataProvider (abstração)
- OddsProvider
- NewsProvider
- Injury & Lineup Analyzer

### 2. AI Agents
- Grok Agent
- Manus Agent
- (Futuro) Statistical Model Agent

Cada agente recebe os mesmos dados e produz análise independente.

### 3. Consensus Engine
Compara:
- Mercado escolhido
- Direção do palpite
- Probabilidade estimada
- Confiança
- Riscos identificados

Classifica:
- 🔥 Consenso Forte
- 🟡 Consenso Parcial
- 🔴 Divergência → NO BET

### 4. Scoring System
Confidence Score (0-100) baseado em:
- Consenso das IAs
- Estatísticas
- Forma recente
- Casa/Fora
- Desfalques
- Motivação/contexto
- Valor da odd
- Histórico do modelo no mercado

### 5. Value Engine
- Probabilidade implícita da odd
- EV (Expected Value)
- Value Score

### 6. Filters
- No Bet Filter (dados insuficientes, divergência, etc.)
- Score mínimo configurável
- EV mínimo

### 7. History & Learning
- Registro completo de cada tip
- Track Record (ROI, Win Rate, CLV, etc.)
- Agent Performance Score
- Backtesting Lab

---

## Stack Tecnológica (Planejada)

**Frontend**  
- Next.js (App Router)  
- Tailwind CSS  
- Dark mode profissional

**Backend**  
- Node.js + TypeScript  
- API routes ou serviço separado

**Banco**  
- PostgreSQL

**Cache / Filas**  
- Redis + BullMQ (jobs)

**Infra**  
- Docker  
- Vercel (frontend) + Railway/Render (backend) ou full Docker

**IA Layer**  
- Abstração AIProvider (permite trocar Grok / Manus / outros)

---

## Estrutura de Pastas (alvo)

```
marins-tips/
├── apps/
│   └── web/                 # Next.js frontend
├── packages/
│   ├── core/                # Lógica de negócio (consensus, score, value)
│   ├── agents/              # Grok, Manus, Statistical
│   ├── data/                # Providers de dados
│   └── db/                  # Schema e queries
├── docs/
│   ├── ARCHITECTURE.md
│   ├── API.md
│   └── DATABASE.md
├── docker-compose.yml
└── README.md
```

---

## Fases de Implementação

### Fase 1 — Fundação (atual)
- [x] Nome mantido: Marins TIPS
- [x] Página diária com dual analysis (Grok x Manus)
- [ ] Documentação de arquitetura
- [ ] Estrutura de pastas e monorepo básico
- [ ] Schema inicial do banco

### Fase 2 — Core Logic
- Consensus Engine
- Confidence Score
- Value Engine
- No Bet Filter

### Fase 3 — Dados
- Integração com fontes de jogos e estatísticas
- Desfalques e notícias
- Odds tracker

### Fase 4 — Histórico e Métricas
- Registro de tips
- Track Record
- CLV e EV

### Fase 5 — Dashboard e Automação
- Daily Tips ranking
- Scheduler
- Alertas

---

## Regra de Ouro

> O sistema deve procurar razões para **não apostar**.  
> A melhor decisão possível em muitos dias é: **NO BET**.

---

Atualizado em: 05/09/2026

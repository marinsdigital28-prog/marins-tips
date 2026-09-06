# Marins TIPS

**Sistema de análise esportiva multiagente com consenso entre IAs**

Nome mantido. Ideia do TIPMASTER AI implementada de forma incremental sob a marca Marins TIPS.

---

## O que é

Marins TIPS não é apenas um gerador de palpites.

É um **comitê virtual de analistas** que:

- Analisa jogos de forma independente (Grok + Manus)
- Compara as conclusões
- Calcula consenso e confiança
- Detecta valor (Value Bet)
- Filtra oportunidades ruins
- Tem coragem de dizer **NO BET**

---

## Status Atual

### Fase 1 — Fundação (em andamento)

- [x] Nome: Marins TIPS
- [x] Página diária com análise dual (Grok x Manus)
- [x] Cobertura das principais ligas (não só Brasileirão)
- [x] Arquitetura documentada (`ARCHITECTURE.md`)
- [ ] Estrutura de pastas e monorepo
- [ ] Schema do banco de dados
- [ ] Consensus Engine
- [ ] Confidence Score
- [ ] Value Engine

---

## Como usar hoje

1. Eu atualizo os jogos principais do dia
2. Preencho a coluna **Grok**
3. Você pede para o Manus analisar (ou cola a análise dele)
4. Eu cruzo e gero a **Entrada Final** com classificação de consenso

Comandos:
- `Atualiza o Marins TIPS`
- `Atualiza os jogos`
- `Cruzar com Manus` (quando você colar a análise)

---

## Princípio Central

> O sistema procura razões para **não apostar**.  
> A melhor decisão em muitos dias é: **NO BET**.

---

## Roadmap

Veja o arquivo completo em [`ARCHITECTURE.md`](./ARCHITECTURE.md)

---

## Aviso

Este sistema fornece análises estatísticas e probabilísticas.  
Resultados esportivos são incertos. Não existe garantia de lucro.  
Apostas envolvem risco de perda financeira.

---

**Repositório:** https://github.com/marinsdigital28-prog/marins-tips

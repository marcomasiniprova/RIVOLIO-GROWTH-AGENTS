# Branch dedicato alla sessione builder (Valerio + Claude)

Questo branch `claude/MAIN-AI-AGENT` (ex `claude/svuotare-repository-k0k9w7`, rinominato da Valerio il 06/09)
e' la **casa della sessione builder interattiva** (quella dove Valerio e' presente e scrive, con i 4 popup a ogni prompt).

## MAPPA DEI BRANCH (pulita il 06/09 da Valerio) — NON confondersi mai piu'
Il repo `RIVOLIO-GROWTH-AGENTS` ha SOLO 3 branch, ognuno con un ruolo preciso:
- **`main`** = il TEAM: le skill degli agenti (`.claude/skills`), i docs, CLAUDE.md, motore-contenuti. Gli agenti fanno `git pull origin main` e leggono da qui. NON contiene la dashboard.
- **`claude/rivo-growth-team`** = il CODICE DELLA DASHBOARD (`mission-control/`, Next.js su Railway). Da non toccare senza motivo.
- **`claude/MAIN-AI-AGENT`** = QUESTO branch, dove vivo io (la sessione builder). Config personale + skill solo mie (es. copertura-prompt).

## Cosa cambia rispetto a `main`

- **Niente cap `autoCompactWindow: 200000`.** Quel tetto e' la config degli **agenti** (routine cron),
  non della sessione builder. Qui e' rimosso: la sessione builder scala alla context window con cui
  viene lanciata (fino a 1M token con Opus 4.8), senza compattazioni premature ne' taglio netto anticipato.
- Restano intatte: la deny-list dei segreti (`.env`, chiavi, credenziali) e l'allow di `Bash(curl:*)`.
- Gli hook `SessionStart` e `Stop` restano per compatibilita' ma sono inerti per la builder
  (SessionStart fa pull solo se sei su `main`; Stop e' un guardrail dei ruoli che chiamano run_start).

## Regola

**NON fare merge di questo branch su `main`.** La config di `main` deve restare quella degli agenti
(cap 200k). Questa e' solo per la sessione builder.

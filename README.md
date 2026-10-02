# Agent Trainer

Il compagno di adoption che segue ogni utente HubSpot, uno a uno, durante e dopo la formazione. Costruito su Polyant da Exelab.

![Schema del flusso](docs/funzionale/schema-flusso.svg)

Repo di progettazione e contesto. L'agente vive su Polyant; qui stanno i documenti che lo descrivono e le call da cui nascono le decisioni.

## Contenuto

- [docs/STATO.md](docs/STATO.md): stato del lavoro, decisioni, correzioni da fare.
- [docs/funzionale/documento-funzionale.md](docs/funzionale/documento-funzionale.md): documento funzionale.
- [docs/funzionale/pno-use-case-e-setup.md](docs/funzionale/pno-use-case-e-setup.md): use case in scope per l'MVP (PoC PNO).
- [docs/funzionale/schema-flusso.svg](docs/funzionale/schema-flusso.svg): schema del flusso.
- [.eve/sources/transcripts/](.eve/sources/transcripts/): call Fireflies.
- [docs/decisions/](docs/decisions/): ADR.

## Come si lavora

Le modifiche passano da branch (`feat/...`, `fix/...`) e pull request su `main`. Vedi [CLAUDE.md](CLAUDE.md) per le regole e l'ordine di lettura per riprendere in una nuova sessione.

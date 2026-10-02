# ADR-001: osservatore e valutatore sono due servizi distinti

Data: 03/10/2026. Deciso da Diego, sulla base della call del 02/10 ([trascrizione](../../.eve/sources/transcripts/2026-10-02-agent-trainer-presentazione-finale.md)). Stato: approvato; osservatore implementato su Polyant, valutatore da costruire.

## Decisione
I controlli dell'agente sui dati HubSpot si dividono in due servizi.

- **Osservatore.** Controlla che i record siano in ordine (contatto senza azienda, deal senza amount o close date, deal fermo, deal in Prepare Offer senza fee, Closed Lost incompleto). Non guarda l'obiettivo dell'utente. Si attiva quando l'utente ha completato gli esercizi di onboarding. Gennaro lo chiama "poliziotto".
- **Valutatore.** Confronta l'utente con i **suoi obiettivi** (settimanali, trimestrali) e produce riconoscimento, avanzamento e task per rientrare. Copre UC12 (contratto firmato e avanzamento sul trimestre) e UC14 (sotto target il giovedì). Ha bisogno di un'informazione in più: gli obiettivi di team e persona.

Regole dell'osservatore:
- **Aggregato, non puntuale.** Un solo task per controllo, con il conteggio dei record da sistemare e il link a una vista HubSpot che li elenca. Una vista per ogni controllo, filtrata sull'owner. Il testo del task si imposta da Polyant.
- Se il task viene chiuso senza aver sistemato i record, si riapre.

Gli obiettivi si danno a Polyant da un documento o una tabella. I goal e il forecast di HubSpot restano un'evoluzione possibile, ma di norma li crea il manager per ogni venditore, quindi sono scomodi da popolare.

## Perimetro
Osservatore, valutatore, obiettivi individuali e gamification di base (livelli, badge, serie) sono in MVP. Classifiche, benchmark anonimo e regole di igiene dei task (tetto di messaggi e task aperti) sono personalizzazione a pagamento.

## Conseguenze
- `docs/funzionale/documento-funzionale.md`: capitoli 7.2 e 9 aggiornati (osservatore, valutatore, obiettivi e gamification di base in MVP).
- `docs/funzionale/pno-use-case-e-setup.md`: UC05-UC10 e UC13 diventano task aggregati con link a una vista; UC12 e UC14 passano nella sezione "Valutazione".
- Per ogni controllo dell'osservatore va creata una vista HubSpot.
- Il valutatore dipende dalla disponibilità degli obiettivi per utente: è l'input da chiedere al cliente.

## Da verificare
Il confine non è netto. In call Diego nota che UC12 "controlla anche" (vede il contratto firmato) e poi confronta con il target. Se i due servizi condividano i dati letti, o lo facciano due letture separate, non è stato discusso.

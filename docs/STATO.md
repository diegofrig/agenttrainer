# Stato di Agent Trainer

Aggiornato al 3 ottobre 2026, dopo la call "presentazione finale" del 2 ottobre ([trascrizione](../.eve/sources/transcripts/2026-10-02-agent-trainer-presentazione-finale.md)).

Persone: Diego Frigerio (progettazione, committente), Gennaro Paglia (configurazione su Polyant), Fabrizio Regini.

## Dove siamo

Dato dalla call del 2/10:

- **Onboarding (percorso iniziale): testato e funziona.** Entrando nel team "venditori" l'utente riceve i task di onboarding. Chiusi i primi due ne arrivano altri due, poi altri cinque. A completamento degli ultimi cinque si attiva l'osservatore. Dopo la chiusura di un task ci vuole un paio di minuti prima del successivo.
- **Esercizi e testi si modificano da Polyant**, senza sviluppo: testo, regola, esercizi, anche divisi per team. Si inserisce il team, non le singole persone.
- **Osservatore (controlli sui dati): costruito, visto in funzione solo in parte.** Gennaro dice che le logiche degli UC sono "tutte uguali" e che mancano solo UC12 e UC14. Diego ha visto aprirsi e riaprirsi il task del contatto senza azienda e quello dei deal senza amount o close date; il resto non l'ha testato.
- **Non fatto:** UC12, UC14 (reportistica), report e riepiloghi di andamento, "verifica finale" (parole di Gennaro).

## Decisioni della call

| Cosa | Decisione | Fonte |
|---|---|---|
| Osservatore | Controllo **aggregato**, non puntuale: un solo task per più record ("hai 10 contatti senza azienda"), non uno per record. Con import di 10 contatti Gennaro ne aveva ottenuti dieci. | 21:03 |
| Osservatore | Il task contiene il **link a una vista HubSpot** dei record da sistemare, una vista per ogni controllo, dinamica per owner. Il testo del task si imposta da Polyant. | 21:47 a 25:30 |
| Osservatore | Se il task viene chiuso senza aver sistemato i record, **si riapre**. | 20:39, 30:27 |
| UC11 | **Tolto.** Né Diego né Gennaro capiscono cosa dovesse controllare. | 30:48 a 31:20 |
| UC12, UC14 | **Fuori dall'osservatore**, vanno nella parte di valutazione e reportistica. Gennaro li fa dopo, insieme ai report. | 15:52 a 18:50, 34:10 |
| Valutatore | Nuova figura accanto all'osservatore: confronta l'utente con i **suoi obiettivi**. Gli obiettivi si danno a Polyant da un documento o tabella; i goal/forecast di HubSpot restano un'evoluzione possibile. | 16:45 a 19:48 |
| Badge First signature | La firma del primo contratto genera un task di riconoscimento. Classifiche e dashboard: dopo l'MVP. | 31:49 a 33:32 |
| Lingua | Default inglese. Possibile miglioramento: lingua dell'utente da HubSpot. Gennaro deve verificare se il dato è recuperabile. | 36:54 a 37:39 |
| UC17 | Task al Team Leader quando un utente passa a rischio, scelto come caso per testare il Team Leader. Gennaro: l'informazione c'è, dal criterio del permission set. | 46:32 a 47:08 |
| UC19 | Quadro per Exelab: si parte dalla soluzione più semplice (mail o Slack). | 35:05 a 35:36 |
| Task di training | Devono contenere anche il link alla documentazione HubSpot. | 02:28 a 02:48 |

## Prossimi passi dichiarati

- **Gennaro:** finire la reportistica (UC12, UC14, UC15-UC19), sistemare UC06, mettere i link alle viste nei task, verificare la lingua utente.
- **Diego:** studiare come mettere una knowledge base dentro HubSpot per supportare l'utente mentre lavora (Breeze o alternative, costi). Poi un momento con Gennaro per capire se serve sviluppo.
- **Diego:** stimare i costi di WhatsApp, Slack e Teams come canali, e capire come usare la memoria per utente, che oggi nei task non produce nulla di utile.
- **Budget:** serve capire quanto lavoro resta oltre la prossima settimana, per poter pianificare a gennaio. Stima non ancora fatta.

## Decisioni di Diego del 3 ottobre

Prese sui punti emersi dal confronto tra i due documenti e la call. Applicate a `docs/funzionale/` nella PR "Allineamento documenti".

| Punto | Decisione | Dove applicata |
|---|---|---|
| Verifica degli esercizi | Nell'MVP l'esercizio è fatto quando l'utente spunta il task. La verifica sui dati è upsell, anche nella PoC PNO. | PNO sezione 5 |
| Controlli dell'osservatore | Task aggregato con link a una vista HubSpot (vedi ADR-001). | PNO sezione 4 |
| Badge, livelli, serie | In MVP. Classifiche e benchmark anonimo restano add-on. | Funzionale 9.1 e 9.2, PNO sezione 6 |
| Obiettivi individuali | In MVP. | Funzionale 7.2, 9.1, 9.2; schema |
| Stati di adoption | Cinque: non iniziato, in corso, onboarding completato, adottato, a rischio. | Funzionale capitolo 4; schema |
| Tetto di task e messaggi | Upsell. Nell'MVP non c'è un limite. | Funzionale 9.2, PNO sezione 4 |
| Training transcript | Fonte potenziale nello schema. | Schema |
| Osservatore e valutatore | Due servizi distinti. | [ADR-001](decisions/ADR-001-osservatore-e-valutatore.md) |

UC11 resta fuori e non viene annotato nel PNO: il salto di numerazione è chiaro.

UC06: il controllo vale per le Organization con country Netherlands **e** owner del team Netherlands (confermato da Diego il 3/10).

## Ancora da sciogliere

1. **UC17, task al Team Leader.** Scritto nel PNO, ma in call "la roba del team leader forse non l'ho messa". Stato di implementazione da chiedere a Gennaro.
2. **UC19, canale.** Il PNO ora dice "Slack o Email, si parte dalla soluzione più semplice da implementare". La scelta non è fatta.
3. **Esempi dei task (PNO, sezione 4).** Sono scritti al singolare. Con i task aggregati vanno riscritti con il conteggio dei record. Non l'ho fatto: sono testi che Gennaro tiene su Polyant.
4. **UC09.** La regola "se PNO ha già un task su quel deal non ne apre un secondo" è stata riformulata come "deal esclusi dalla vista". È una traduzione mia della regola nel modello aggregato.
5. **Verifica sui dati.** La colonna "Verifica" del PNO è ora "Verifica sui dati (upsell)". Per D5, D6 e P16 il valore è "Spunta", che nell'ottica della nuova regola è la sola verifica prevista. Da pulire.

## Da verificare (non è chiaro dalla call)

- Notifiche: la campanella degli account risulta vuota nonostante i task creati. Diego ipotizza che manchi la notifica via email. Non verificato.
- Il riconoscimento a fine onboarding (UC16): Diego dice di non averlo visto funzionare.
- Dove si costruisce la chat con knowledge base (dentro HubSpot, Breeze, altro): aperto, studio di Diego.
- Remax è citato da Gennaro come precedente per la knowledge base. Non c'è altro in questo repo su Remax.

## Fireflies da aggiungere

Diego ha call della settimana (fino al 3/10) in cui si è parlato di Agent Trainer, non ancora importate. Non urgente.

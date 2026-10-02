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

## Da modificare nei documenti

Incoerenze tra i documenti e la call. **I file in `docs/funzionale/` non sono stati toccati**, a parte il link all'immagine nella prima riga del documento funzionale (prima puntava a un artifact su claude.ai, ora al file del repo). Da decidere cosa correggere e dove.

### Tra i due documenti

1. **Verifica degli esercizi.** Il documento funzionale dice che nell'MVP la verifica è sulla spunta del task, e la verifica sui dati reali è upsell (7.1, 8, 9.1, 9.2). Il documento PNO dice che nella PoC la verifica è sui dati, e la tabella degli esercizi indica quasi sempre un dato come verifica (prima email tracciata, primo deal, ecc.). Sono due promesse diverse. Va deciso quale vale per l'MVP, e se la PoC PNO è un'eccezione dichiarata.
2. **Stati di adoption.** Il documento funzionale ne ha quattro (non iniziato, in corso, adottato, a rischio), e lo schema SVG ne mostra tre più "a rischio". Il PNO ne ha cinque, con "Onboarding Completato". In call Diego ha proposto lo stato in più. Va aggiunto al documento funzionale e allo schema, oppure il PNO resta un caso a parte.
3. **Gamification, benchmark e serie.** Nel documento funzionale sono add-on a pagamento (9.2). Il PNO li include in MVP (sezione 6: livelli, badge, serie). In call Diego propone di fare subito il task di riconoscimento per "First signature", lasciando classifiche e dashboard a dopo. Va deciso se il perimetro MVP include i badge.
4. **Obiettivi individuali.** Il documento funzionale li colloca in upsell. Il PNO ha target settimanali e trimestrali già dentro la logica degli stati (target settimanali) e dei riepiloghi. Contraddizione sul perimetro.
5. **Frequenza e task generati.** Il documento funzionale chiede un tetto di messaggi e task aperti (13). Il PNO prevede task su ogni trigger, tre reminder per task e riepilogo ogni lunedì. Nessun tetto indicato.

### Nel documento PNO, rispetto alla call

6. **UC11** non compare nell'elenco (la numerazione salta da UC10 a UC12): coerente con la decisione di toglierlo, ma va scritto che è tolto.
7. **UC12 e UC14** sono nella tabella "Lavoro quotidiano" come use case dell'osservatore. In call sono stati spostati nella valutazione e reportistica.
8. **UC06** non è chiaro a Gennaro (termini NL/BE, KvK, Vestigingsnummer, campi AFAS). Il testo del task va chiarito, e va precisato cosa si intende per "Organization NL" (country dell'organization, owner del team Netherlands, o entrambi: Diego dice "anche owner del team Netherlands").
9. **UC17 / team leader.** Scritto nel documento come task al Team Leader. In call: "la roba del team leader forse non l'ho messa"; Gennaro lo lega alla reportistica. Stato di implementazione non chiaro.
10. **UC19.** Il testo contiene "vedi soluzione più sempolice": nota di lavoro lasciata nel documento, da trasformare in decisione (mail o Slack).

### Nel documento funzionale

11. **Training Transcript** compare nelle fonti (sezione 5A) ma non nello schema SVG. In call Diego dice "qua aggiungerei il training transcript". Da allineare lo schema.
12. **Osservatore e valutatore** sono due concetti emersi in call e assenti da entrambi i documenti. Potrebbe valere un'ADR in `docs/decisions/`.
13. **Check aggregato con link alla vista.** Vale per tutti i controlli dell'osservatore ma non è scritto nel PNO, che parla di "task sull'Organization / sul contact / sul deal", cioè un task per record. Contraddice la decisione "osservatore aggregato" della tabella sopra.

## Da verificare (non è chiaro dalla call)

- Notifiche: la campanella degli account risulta vuota nonostante i task creati. Diego ipotizza che manchi la notifica via email. Non verificato.
- Il riconoscimento a fine onboarding (UC16): Diego dice di non averlo visto funzionare.
- Dove si costruisce la chat con knowledge base (dentro HubSpot, Breeze, altro): aperto, studio di Diego.
- Remax è citato da Gennaro come precedente per la knowledge base. Non c'è altro in questo repo su Remax.

## Fireflies da aggiungere

Diego ha call della settimana (fino al 3/10) in cui si è parlato di Agent Trainer, non ancora importate. Non urgente.

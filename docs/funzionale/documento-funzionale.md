# Agent Trainer: Documento Funzionale

[**Vedi immagine**](schema-flusso.svg) (schema del flusso, in questo repo; il link originale era un artifact su claude.ai)

---

## 1\. Introduzione e contesto

Le aziende che Exelab affianca sono sempre più grandi e portano su HubSpot un numero di utenti in costante crescita. Più si allarga questo bacino, più diventa difficile formare tutti e seguire l'adoption persona per persona con il modello classico, fatto di sessioni 1-to-1 e affiancamento manuale. Il tempo dei formatori non cresce alla stessa velocità del numero di utenti da seguire.

Agent Trainer nasce per rispondere a questo problema. È un agente costruito su Polyant che affianca ogni utente del cliente durante e dopo la formazione, con l'obiettivo di portarlo a usare HubSpot in autonomia nel lavoro quotidiano. L'esperienza punta a restare il più vicino possibile a un percorso 1-to-1 a prescindere dal numero di persone coinvolte: ogni utente viene seguito nelle sue attività, sollecitato al momento giusto e accompagnato nella pratica.

L'agente si collega all'HubSpot del cliente, da cui legge come ciascuno sta usando la piattaforma, e vive di default dentro HubSpot stesso. Parte da una configurazione standard, pronta da collegare, e nei casi in cui il cliente lo richiede può essere personalizzato sul proprio processo con pochi input aggiuntivi, come elemento di upsell.

Agent Trainer ha due interlocutori:

- l'utente finale del cliente, che riceve formazione, esercizi e supporto continuo nel suo lavoro su HubSpot;  
- Exelab, che configura e gestisce l'agente, sceglie chi seguire e monitora l'andamento dell'adoption, condividendone i risultati con il cliente.

Nell'MVP il setup e la gestione dell'agente sono in capo a Exelab. Non è previsto un amministratore lato cliente che configura l'agente.

---

## 2\. Obiettivo

Massimizzare l'**adoption** di HubSpot: portare ogni utente del cliente a usare davvero il CRM nei processi che abbiamo implementato, nel minor tempo possibile e in autonomia.

Tutto il resto discende da qui. Quando le persone usano la piattaforma, generano dati reali che possiamo misurare, percepiscono il valore dello strumento e del nostro lavoro, e restano clienti soddisfatti. Da questo terreno nascono in modo naturale nuove occasioni di collaborazione. Queste occasioni non sono un compito dell'agente: emergono come conseguenza dell'adoption che l'agente costruisce.

L'agente è quindi tarato su un solo risultato: ridurre il tempo che separa la consegna del progetto dal momento in cui l'utente lavora su HubSpot senza più bisogno di assistenza.

---

## 3\. Descrizione di massima

Agent Trainer è un compagno di adoption asincrono. Segue ogni utente, uno per uno, durante e dopo la formazione, per portarlo a usare HubSpot nel lavoro quotidiano. Vive di default dentro HubSpot e lavora secondo un ciclo continuo:

- **Osserva.** Legge come ciascun utente sta usando HubSpot: cosa crea, quali attività logga, dove si è bloccato e quali parti del processo implementato non ha ancora iniziato a usare.  
- **Ingaggia.** Interviene al momento giusto con un messaggio breve e mirato, sia programmato a cadenza bassa, sia innescato da ciò che l'utente fa o non fa.  
- **Fa praticare.** Assegna esercizi concreti da svolgere in piattaforma, perché la pratica ripetuta è ciò che fa attecchire l'uso dello strumento.  
- **Verifica.** Controlla che gli esercizi siano stati svolti.  
- **Rinforza.** Riconosce i progressi, ricorda cosa manca e tiene memoria di dove ciascuno fatica, così ogni interazione resta personale.

Questo ciclo non si esaurisce in un singolo momento. La ricerca sull'apprendimento è netta su un punto: gran parte di ciò che si impara in una sessione di formazione si dimentica nei giorni successivi se non viene messo in pratica. Per questo Agent Trainer lavora distribuito nel tempo, con sollecitazioni e pratica ripetuta, invece di concentrare tutto in una formazione unica.

Nella forma **MVP** l'agente è proattivo: osserva, assegna esercizi, sollecita, riepiloga e comunica all'utente come sta andando e cosa gli resta. In questa fase la comunicazione è a senso unico (il dettaglio è al capitolo 7.5). La chat con cui l'utente interroga l'agente e i canali oltre HubSpot sono parte della personalizzazione a pagamento. Più il cliente personalizza l'agente, più questo smette di parlare di HubSpot in generale e inizia a parlare del processo specifico di quel cliente, avvicinandosi al training 1-to-1 ma scalato su tutti gli utenti insieme.

---

## 4\. Stato di adoption per utente

Per intervenire in modo sensato, l'agente ha bisogno di sapere a che punto è ogni persona. Per questo tiene, per ciascun utente, uno stato di adoption. È la base oggettiva con cui decide quando intervenire e su cosa, ed è anche ciò che permette di dimostrare il valore al cliente con numeri, non con impressioni.

Lo stato si costruisce così:

- **Baseline all'attivazione.** Al momento in cui l'agente prende in carico un utente, fotografa il punto di partenza: cosa già usa e cosa no. Senza un punto di partenza non si distingue il progresso dal rumore.  
- **Poche dimensioni misurabili.** Lo stato poggia su pochi segnali chiari, ad esempio: attivazione di base (email e calendario collegati, primo uso del workspace), creazione di record e attività, avanzamento sugli esercizi, uso dei processi chiave del progetto.  
- **Stati semplici.** Ogni utente si trova in uno stato leggibile a colpo d'occhio: non iniziato, in corso, onboarding completato, adottato, a rischio (chi aveva cominciato e ha rallentato).  
- **Target di arrivo.** Si definisce cosa significa "adottato" per quel ruolo e quel progetto, così l'obiettivo è chiaro e misurabile.

L'agente aggiorna lo stato nel tempo a partire dai dati di HubSpot e lo usa per modulare nudge, esercizi e riepiloghi.

Le dimensioni esatte e le soglie dipendono dai dati disponibili (capitolo 8\) e, quando si vuole confrontare l'utente con obiettivi individuali, dalla personalizzazione (capitolo 9).

---

## 5\. Mappa delle componenti

**A. Fonti di conoscenza** (cosa l'agente sa)

- HubSpot, dati live: utilizzo della piattaforma, record e attività creati per utente, dati sui deal, creazione di asset come workflow ed email, dati di login (i login sono disponibili solo con HubSpot Enterprise).  
- Progettazione funzionale della soluzione: descrive cosa l'utente deve saper fare nel processo specifico del cliente.  
- FAQ di progetto: le risposte già raccolte e validate con il cliente durante la delivery.  
- Knowledge base HubSpot: la documentazione di prodotto di HubSpot, cioè come si fanno le cose nella piattaforma. È riusabile su tutti i clienti.  
- Training Transcript: transcript delle call di formazione con il cliente

**B. Configurazione e contenuti** (come l'agente è tarato per cliente e utente)

- Comportamento dell'agente: persona, tono, regole d'ingaggio, cadenza, consapevolezza del ruolo.  
- Obiettivi individuali: ad esempio quanti deal creare o chiudere.  
- Esercizi: il set di default più gli esercizi custom.

**C. L'agente Polyant** (il motore)

- Motore di coaching: ragiona, decide quando e come intervenire, e tiene aggiornato lo stato di adoption per utente.  
- Memoria per utente: ricorda obiettivi, progressi, storia e dove la persona ha faticato. È la componente che fa percepire l'esperienza come un 1-to-1.

**D. Azioni** (cosa fa)

- Monitora l'uso su HubSpot, assegna esercizi e li fa praticare, verifica il completamento, manda nudge proattivi, produce riepiloghi di avanzamento, comunica all'utente come sta andando e cosa resta.

**E. Canali** (dove parla)

- HubSpot di default. Slack, Teams e WhatsApp come upsell.

**F. Anello di ritorno**

- Reporting di adoption verso Exelab, che lo condivide con il cliente.

---

## 6\. Utenti e ruoli

**Utente finale del cliente.** È la persona che usa HubSpot e che l'agente segue. Nell'MVP partiamo dal team sales, perché è il caso d'uso più diretto e ad alto impatto. L'agente ha una consapevolezza di base del ruolo, sufficiente a orientare il tipo di esercizi e di sollecitazioni. La personalizzazione profonda per ruolo, con percorsi e contenuti distinti, e l'estensione ad altri team (ad esempio marketing e service) sono parte dell'upsell e delle evoluzioni.

**Exelab.** Configura e gestisce l'agente da Polyant, prepara il set di esercizi e la base di conoscenza, attiva eventuali personalizzazioni, regola comportamento e cadenza, seleziona chi seguire e monitora i risultati. Nell'MVP è l'unico soggetto che mette mano alla configurazione.

---

## 7\. Funzionalità

### 7.1 Esercizi: assegnazione, pratica e verifica

**Cosa fa.** Trasforma la formazione in pratica concreta: assegna a ogni utente compiti operativi da svolgere dentro HubSpot, li segue e verifica che vengano completati. È il cuore del principio per cui oltre metà del tempo di formazione è attività svolta dall'utente.

**Come si comporta (MVP).**

- Parte da un set di esercizi di default, valido per quasi tutti gli utenti e indipendente dal progetto: collega l'email, collega il calendario, logga la prima attività, crea il primo deal, costruisci la tua dashboard personale.  
- Ogni esercizio viene recapitato come task di HubSpot assegnato all'utente.  
- Il task contiene una micro-guida autosufficiente (due o tre passi) e il link all'articolo giusto della knowledge base HubSpot.  
- La verifica avviene sulla spunta del task: quando l'utente lo segna come completato, l'esercizio risulta fatto.

**Come si comporta (Upsell).**

- Esercizi custom legati al processo specifico del cliente, ricavati dalla progettazione funzionale. Le pillole formative e le checklist diventano task dedicati.  
- Verifica basata sui dati reali oltre alla spunta. Il dettaglio di cosa si riesce a verificare dai dati è al capitolo 8\.

**Cosa serve perché funzioni.** La lista degli esercizi di default con il relativo task e la micro-guida, preparata una volta e riusata su tutti i clienti. Per gli esercizi custom serve la progettazione funzionale del progetto.

### 7.2 Monitoraggio dell'uso di HubSpot

**Come si comporta.**

- Rileva i record e le attività create da ciascun utente (contatti, deal, note, chiamate, meeting, task) e i dati sui deal in pipeline.  
- Rileva la creazione di asset come workflow ed email, segnale utile soprattutto per i team marketing (rilevante quando l'agente verrà esteso oltre i sales).  
- Riconosce i segnali di inattività o di processo non ancora avviato (ad esempio un utente che non logga attività da diversi giorni, o che non ha mai creato un deal pur dovendolo fare).

**Cosa serve perché funzioni.** Il collegamento all'HubSpot del cliente.

Monitoraggio dell'uso e confronto con gli obiettivi individuali in MVP. I controlli sui dati (l'osservatore) segnalano con un solo task per controllo, con il link a una vista HubSpot dei record da sistemare.

### 7.3 Nudge e ingaggio proattivo

**Come si comporta.**

- Due tipi di sollecitazione: programmata (a cadenza bassa) e innescata da eventi (ad esempio un esercizio scaduto, un deal fermo da troppo tempo, un traguardo raggiunto).  
- Dentro HubSpot le sollecitazioni prendono la forma di task assegnati all'utente o di note che taggano la persona, così arrivano nell'ambiente in cui già lavora. Nell'MVP possono partire da workflow di HubSpot.  
- Messaggi brevi, con un solo passo da fare e un tono che incoraggia.

**Cosa serve perché funzioni.** Le regole di ingaggio e la cadenza, impostate in modo standard e regolabili da Exelab via Polyant. Nell'MVP non c'è gestione della frequenza lato utente: è una configurazione standard che colleghiamo all'HubSpot del cliente e che funziona da subito. Al massimo si seleziona chi riceve la formazione dall'agente.

Nudge dentro HubSpot in MVP. I messaggi proattivi innescati su canali esterni (WhatsApp, Slack) sono upsell.

### 7.4 Riepiloghi di avanzamento

**Come si comporta.**

- All'utente: cosa ha completato, cosa gli resta, come sta andando rispetto al periodo precedente. Formato breve e leggibile, recapitato dentro HubSpot.  
- A Exelab: il quadro di adoption del team, utile a capire chi procede bene e chi va supportato. Exelab lo condivide con il cliente.

**Cosa serve perché funzioni.** I dati di monitoraggio (7.2) e lo stato degli esercizi (7.1).

Riepiloghi standard in MVP. Reportistica e KPI custom in upsell (capitolo 12).

### 7.5 Interazione dell'utente e risposte

**Come si comporta (MVP).**

- La comunicazione è a senso unico, dall'agente all'utente. L'agente comunica andamento, esercizi e cosa resta tramite task, note e riepiloghi proattivi.  
- Dentro HubSpot non esiste in modo nativo una superficie di chat su cui l'utente possa scrivere all'agente. Per questo nell'MVP l'utente non pone domande: riceve. La micro-guida dentro i task (7.1) serve proprio a dare aiuto utile anche senza una chat.

**Come abilitare le domande dell'utente.**

- Strade possibili: collegarsi a Breeze oppure costruire un chatbot dedicato in HubSpot o usare canali come Slack, Whatsapp o Teams.

**Cosa può rispondere una volta abilitata l'interazione.**

- Risposte sul proprio andamento e sui propri esercizi ("come sto andando rispetto a settimana scorsa?", "cosa mi resta da fare?"), basate sui dati che l'agente già monitora.  
- Chat how-to ancorata al processo specifico del cliente ("come si fa X"), che attinge alla documentazione di prodotto HubSpot, alla progettazione funzionale e alle FAQ di progetto.

**Cosa serve perché funzioni.** Una superficie di interazione (Breeze, chatbot HubSpot, o un canale esterno). Per la chat how-to serve inoltre la base di conoscenza: documentazione di prodotto HubSpot, progettazione funzionale, FAQ di progetto.

### 7.6 Memoria per utente

**Come si comporta.**

- Ricorda lo stato di avanzamento, evita di ripetere cose già fatte, riprende da dove si era rimasti. Senza memoria l'agente ripartirebbe da zero a ogni interazione; con la memoria dà continuità al percorso.

---

## 8\. Cosa l'agente legge da HubSpot

La capacità dell'agente di osservare e verificare dipende da cosa HubSpot rende disponibile in automatico. La cosa importante è sapere cosa leggiamo.

**Cosa leggiamo in automatico, per utente.**

- Record creati: contatti, deal e altri oggetti creati dalla persona.  
- Attività loggate: note, chiamate, meeting, email registrate, task.  
- Dati sui deal: stage, data dell'ultima attività, numero di attività collegate.  
- Asset creati: workflow ed email creati dalla persona, segnale utile soprattutto per i team marketing.

**Cosa non leggiamo in automatico.**

- Lo stato di collegamento di email e calendario. Non è leggibile in automatico: si deduce da un segnale indiretto (ad esempio la comparsa della prima email tracciata o del primo meeting sincronizzato) oppure si chiede all'utente di confermarlo.  
- I dati di login (chi è entrato e quando). Sono disponibili solo con HubSpot Enterprise. Gli esercizi e i controlli basati sui login richiedono quindi questo piano.  
- L'uso di funzioni specifiche (ad esempio le sequenze) e l'ultimo accesso come dato strutturato. Vivono solo dentro l'interfaccia di HubSpot e non sono esposti in automatico.

**Conseguenza sulla verifica degli esercizi.**

- Nell'MVP la verifica è sulla spunta del task di HubSpot e non dipende da questi vincoli: funziona sempre.  
- Nell'upsell, verifichiamo sui dati reali

---

## 9\. MVP e Personalizzazione

Per semplicità il documento usa due secchi: cosa è incluso nell'MVP standard, e cosa è personalizzazione a pagamento (che raccoglie sia le estensioni su misura per il cliente sia gli add-on opzionali).

### 9.1 Cosa contiene l'MVP

L'MVP è l'agente standard, pronto da collegare all'HubSpot del cliente, proattivo e operante dentro HubSpot. Parte dal team sales.

- Stato di adoption per utente, costruito sui dati standard.  
- Monitoraggio dell'uso di HubSpot per utente (record, attività, dati sui deal; rilevazione di workflow ed email creati).  
- Set di esercizi di default, recapitati come task di HubSpot con micro-guida, con verifica sulla spunta del task.  
- Nudge proattivi dentro HubSpot, sotto forma di task o note che taggano la persona, programmati a cadenza bassa e innescati da eventi.  
- Riepiloghi di avanzamento all'utente e versione aggregata a Exelab.  
- Comunicazione proattiva di andamento e cosa resta (a senso unico, senza domande dell'utente).  
- Memoria per utente.  
- Consapevolezza di base del ruolo e contesto di progetto leggero.  
- Selezione di chi riceve la formazione dall'agente.
- Obiettivi individuali per utente (ad esempio target di deal creati o chiusi, target di attività), usati per lo stato di adoption, i riepiloghi e la valutazione.
- Osservatore: controlli sui dati, con un solo task per controllo e il link a una vista HubSpot dei record da sistemare.
- Valutatore: confronto dell'utente con i suoi obiettivi (ad esempio un contratto firmato rispetto al target del trimestre).
- Gamification di base: livelli, badge e serie, con il riconoscimento sotto forma di task.

### 9.2 Cosa è Personalizzazione a pagamento

Tutto ciò che porta l'agente oltre lo standard, sia adattarlo al processo del cliente, sia abilitare funzioni opzionali.

Personalizzazione sul processo del cliente:

- Interazione bidirezionale con l'utente e chat how-to ancorata al processo specifico, alimentata dalla progettazione funzionale e dalle FAQ di progetto. Richiede una superficie di interazione (Breeze, chatbot in HubSpot, o un canale esterno).  
- Esercizi custom oltre i default, derivati dalla progettazione funzionale. Disegnati per non premiare l'attività-vetrina: i segnali di qualità (completezza dei dati, igiene della pipeline) fanno da contrappeso al solo volume, così "crea 5 deal" non si soddisfa con 5 deal vuoti.  
- Personalizzazione profonda per ruolo ed estensione ad altri team (marketing, service).  
- Verifica degli esercizi basata sui dati reali invece che sulla sola spunta.  
- KPI e metriche di reporting custom.

Misura dell'efficacia dell'agente e miglioramento nel tempo:

- Metriche sull'agente stesso: tasso di apertura e di azione sui nudge, completamento degli esercizi, opt-out, numero di utenti spostati di stato di adoption (ad esempio da "non iniziato" ad "adottato"). Servono a tarare l'agente e a dimostrarne il valore.  
- Ciclo FAQ: le domande a cui l'agente non sa rispondere vengono raccolte e segnalate a Exelab, che le trasforma in nuove voci di knowledge base. L'agente migliora nel tempo quasi a costo zero.

Add-on opzionali:

- Canali aggiuntivi: WhatsApp, Slack, Teams (capitolo 11).  
- Messaggi proattivi innescati su canali esterni.  
- Gamification avanzata (classifiche), benchmark anonimo verso pari ruolo, vista manager conversazionale (il responsabile chiede dell'andamento del team), messaggi audio, risposte rapide a pulsanti.  
- Esercizi e controlli basati sui login (richiedono HubSpot Enterprise).
- Regole di igiene dei task: tetto di messaggi e di task aperti per utente, silenzio quando l'utente è già attivo (capitolo 13).

### 9.3 Come si configura la personalizzazione su Polyant

La personalizzazione punta a richiedere pochi input e poco tempo. Si appoggia all'interfaccia no-code di Polyant, con cui Exelab regola l'agente senza intervento tecnico. I livelli di input sono tre:

- **Progettazione funzionale della soluzione.** Si carica come base di conoscenza dell'agente. Da qui l'agente ricava cosa l'utente deve saper fare e su cosa concentrare esercizi e risposte.  
- **Obiettivi individuali.** Si impostano i target per utente, contro cui l'agente misura l'andamento.  
- **Esercizi assegnati.** Si parte dal set di default e si aggiungono gli esercizi custom, con il relativo criterio di verifica.  
- **FAQ di progetto.** Raccolte durante la delivery, che diventano materiale di risposta.

Dall'interfaccia Polyant, Exelab regola inoltre comportamento, tono, regole d'ingaggio e cadenza, e seleziona i destinatari della formazione.

### 9.4 Modello di erogazione

Una opzione commerciale da valutare: l'agente viene fornito incluso per una finestra di training definita (ad esempio il periodo di formazione e adoption iniziale legato alla delivery), e la sua continuazione oltre quella finestra diventa un canone mensile.

Oltre a generare ricavo ricorrente, questo modello ha un effetto utile sull'adoption: una finestra inclusa a tempo spinge il cliente a far onboardare le proprie risorse in fretta, invece di rimandare. L'agente accompagna il go-live come parte del progetto, e resta attivo nel tempo solo per i clienti che scelgono di mantenerlo.

---

## 10\. Esperienza e tono

La formazione di Exelab deve essere una bella storia da raccontare: simpatica, così che le persone arrivino volentieri all'interazione, e utile, così che ogni volta si portino a casa qualcosa. Agent Trainer eredita questo principio nel modo in cui parla.

- **Pratica più che spiegazione.** Oltre metà dell'esperienza è l'utente che fa, in linea con il principio di formazione hands-on di Exelab e con l'evidenza che si impara molto di più facendo che ascoltando.  
- **Distribuito nel tempo.** Sollecitazioni e pratica ripetuta lungo le settimane, per contrastare il naturale oblio di ciò che si è appreso in aula.  
- **Messaggi brevi, un passo alla volta.** Ogni intervento ha uno scopo chiaro e una sola azione richiesta.  
- **Tono che incoraggia.** Si valorizza il progresso e si celebrano i traguardi. Le sollecitazioni hanno un tono di accompagnamento.  
- **Cadenza misurata.** La frequenza è bassa per non diventare fastidiosa. È gestita da Exelab via Polyant, non dall'utente; nell'MVP è uno standard che funziona così com'è.

---

## 11\. Canali

**HubSpot (MVP, di default).** L'agente vive dentro HubSpot. Gli esercizi arrivano come task con micro-guida, le sollecitazioni come task o note che taggano la persona, i riepiloghi nello stesso ambiente in cui l'utente già lavora. La comunicazione in MVP è a senso unico: l'utente riceve, non scrive all'agente (vedi 7.5). Nessun canale aggiuntivo da configurare.

**Canali esterni (upsell).** Su richiesta del cliente l'agente può parlare su altri canali, con una differenza importante da tenere presente:

- **WhatsApp.** I messaggi proattivi richiedono template pre-approvati da Meta e partono tipicamente da workflow di HubSpot. È il modello già adottato su MaxCoach. Questo dà controllo ma vincola i messaggi proattivi ai template approvati.  
- **Slack e canali nativi Polyant.** Non richiedono l'approvazione di template come Meta, quindi l'agente è più libero di decidere cosa scrivere nel momento.

I canali esterni abilitano anche l'interazione bidirezionale, cioè la possibilità per l'utente di scrivere all'agente. Ogni canale aggiuntivo oltre HubSpot è a pagamento.

---

## 12\. Come misuriamo il successo

- **Attività.** Le persone usano la piattaforma? Frequenza di accesso (dove disponibile), record creati per utente, attività loggate, asset creati (workflow, email), esercizi completati.  
- **Qualità.** La usano bene? Completezza dei dati, igiene della pipeline (deal fermi), rispetto delle regole di processo. I segnali di qualità fanno anche da contrappeso al solo volume, per non premiare l'attività di facciata.  
- **Outcome.** Stanno arrivando i risultati? Deal in pipeline, avanzamento verso gli obiettivi individuali (dove impostati).

---

## 13\. Punti da approfondire

- **Logica di intervento e igiene dei task.** Elenco dei trigger, tetto di messaggi per settimana, regola di silenzio quando l'utente è già attivo, comportamento quando un nudge viene ignorato più volte, numero massimo di task aperti generati dall'agente, attenzione a non sporcare i KPI di task del cliente con i task dell'agente. È l'area che decide se l'agente viene percepito come utile o come fastidioso.  
- **Guardrail dell'agente.** Cosa l'agente non deve fare: inventare risposte (deve ancorarsi a knowledge base e FAQ e, se non sa, rimandare al referente Exelab), mostrare a un utente i dati di un altro (la separazione per ruolo va resa regola esplicita e verificata), gestione dei dati HubSpot mancanti o ambigui, momenti in cui passare la palla a un umano.  
- **Intake della personalizzazione.** Il set minimo di input richiesti al cliente e la mappatura da progettazione funzionale a esercizi, così la promessa "pochi input" regge anche in delivery.  
- **Punti minori.** Chi invia i messaggi proattivi nell'MVP (workflow di HubSpot o eventi gestiti dall'agente), comportamento multilingua, fase pilota con un gruppo di champion prima del rollout esteso, modalità mantenimento per chi è già autonomo (si lega bene al canone mensile).

---

## 14\. Appendice: mappatura funzioni e mattoni di Polyant

Mappatura leggera, a uso di chi costruirà l'agente. Resta fuori dal corpo funzionale.

- **Comportamento dell'agente** (persona, tono, regole, ruolo): impostazioni di prompt dell'istanza.  
- **Esercizi**: gestiti come skill o contenuti configurabili, recapitati come task di HubSpot.  
- **Base di conoscenza** (documentazione di prodotto HubSpot, progettazione funzionale, FAQ): knowledge base dell'istanza.  
- **Memoria per utente e stato di adoption**: memoria persistente per utente, nativa.  
- **Reazione agli eventi HubSpot** (esercizio scaduto, deal fermo, traguardo): motore di eventi proattivo (Room), alimentato dagli eventi di HubSpot.  
- **Nudge programmati e riepiloghi periodici**: scheduler dei task pianificati.  
- **Lettura dei dati HubSpot**: connettore HubSpot.  
- **Canali** (HubSpot, WhatsApp, Slack, Teams): canali dell'istanza.  
- **Superficie di interazione per le domande dell'utente in HubSpot**: collegamento a Breeze o chatbot dedicato (da valutare, fuori MVP se complesso).  
- **Configurazione no-code lato Exelab**: pannello di amministrazione di Polyant.

# Agent Trainer per PNO: use case e setup

Cosa configurare in Agent Trainer per seguire i sales di PNO nella PoC. I testi dell'agente sono in inglese.

## 1\. Persona

L'agente è per il sales PNO un manager che conosce il suo lavoro e lo specialista HubSpot che lo ha formato.

- **Da manager:** conosce il mestiere (prima intervista per capire il fit, offerta con fee fisse, orarie e success fee, consorzi, contratti quadro, cicli lunghi dei grant europei). Guarda i numeri della settimana, indica il deal su cui agire, riconosce i risultati.  
- **Da specialista HubSpot:** conosce il setup PNO (pipeline, campi obbligatori per stage, naming dei deal, visibilità per country, connettori verso Matchpoint e AFAS, arricchimento KvK). Quando chiede un dato spiega a cosa serve.

Regole: un solo passo per task; tono che incoraggia; niente risposte inventate, se non sa rimanda al referente Exelab.

## 2\. Chi segue

- Tutti gli utenti dei team sales di tutte le country PNO. Ruoli: sales rep, BD, consultant, country manager. Una country è un team di HubSpot.  
- Ogni giorno l'agente controlla i team: chi entra inizia il percorso, chi viene disattivato esce. Una nuova country non richiede setup, salvo gli esercizi specifici (NL, BE, NO).  
- All'ingresso l'agente registra la baseline: Organization, contact, deal e attività delle 4 settimane precedenti, deal aperti con stage e ultima attività. Chi è appena stato onboardato di solito non ha ancora record: formazione e import dei dati storici avvengono a cavallo. Il percorso parte comunque, con esercizi che non richiedono record esistenti.  
- Il percorso ha una fine: dopo un periodo dall'ingresso (da configurare, per esempio uno o due mesi) l'agente smette di seguire l'utente.

## 3\. Target e stati

Target settimanali per i trigger, obiettivi trimestrali per la motivazione. "Deal gestito" è un deal aperto dell'utente con almeno un'attività o un cambio di stage nella settimana. "Chiuso" è Contract Signed.

|  | Sales rep e BD | Consultant |
| :---- | :---- | :---- |
| Settimana: Organization nuove | 1 | \- |
| Settimana: deal gestiti | 5 (o tutti, se ne ha meno) | 5 (o tutti) |
| Settimana: attività loggate | 5 | 5 |
| Trimestre: Organization nuove | 12 | \- |
| Trimestre: deal creati | 6 | 3 |
| Trimestre: Contract Signed | 2 (3 per NL e local grant IT) | 1 |

Se sales e consultant sono la stessa persona valgono i target del sales rep. Il target sui deal gestiti si applica solo a chi ha almeno un deal aperto.

| Stato | Regola |
| :---- | :---- |
| Non iniziato | Nessun record o attività dall'ingresso |
| In corso | Attività presenti, target settimanali non ancora raggiunti con continuità |
| Onboarding Completato | Terminati esercizi di Onboarding (terminati UC in Percorso Iniziale) |
| Adottato | Esercizi di default completati e target settimanali raggiunti 3 settimane su 4 |
| A rischio | Era in corso o adottato e manca un target settimanale 2 settimane di fila |

Gli obiettivi trimestrali non entrano nello stato.

## 4\. Use case

Tutti lavorano sul canale HubSpot: ogni comunicazione dell'agente è un task assegnato all'utente. L'agente legge i dati ogni mattina e interviene solo quando scatta un trigger.

Tutti i task hanno la scadenza al giorno successivo (configurabile) e due reminder: uno all'assegnazione, uno il giorno prima della scadenza.

**Controlli aggregati.** I controlli sui dati (UC05-UC10, UC13) aprono un solo task per controllo, non uno per record: il task dice quanti record sono da sistemare e contiene il link a una vista HubSpot che li elenca (una vista per controllo, filtrata sull'owner). Se il task viene chiuso senza aver sistemato i record, si riapre. Gli esempi in tabella sono scritti al singolare: nel task reale compare il conteggio ("you have 2 deals without amount or close date").

**Nessun tetto nell'MVP.** Non c'è un limite ai task generati per utente: le regole di igiene dei task (tetto di messaggi e di task aperti) sono personalizzazione a pagamento.

### Percorso iniziale

| \# | Trigger | Cosa fa l'agente | Esempio |
| :---- | :---- | :---- | :---- |
| UC01 | Utente entra nel percorso | Assegna D1 e D2 | "Let's connect your Outlook calendar today: client meetings will land in HubSpot on their own." |
| UC02 | D1 e D2 completati | Assegna D3 e D4; a completamento lo stato passa a "in corso". Se l'utente non ha ancora record, D3 e D4 partono da un'Organization che crea lui | "Log your last call with a client: two lines are enough." |
| UC03 | Prima settimana | Assegna D5, D6, D7, D8 e P1 | "Save a view with your open deals by stage: it's your starting point every morning." |
| UC04 | Livello completato | Sblocca il livello successivo (sezione 6\) e assegna i nuovi esercizi | "Set-up done. Next: your prospecting routine." |

### Lavoro quotidiano

| \# | Trigger | Cosa fa l'agente | Esempio |
| :---- | :---- | :---- | :---- |
| UC05 | Organization creata senza dominio | Task aggregato con link alla vista delle Organization senza dominio | "Add the domain: it's what stops a colleague from creating the same company again." |
| UC06 | Organization NL (country Netherlands e owner del team Netherlands) senza KvK e Vestigingsnummer, o Organization BE senza campi AFAS | Task aggregato con link alla vista delle Organization incomplete | "Add the KvK or Vestigingsnummer now: without it this Organization will not reach AFAS." |
| UC07 | Contact creato senza Organization | Task aggregato con link alla vista dei contact senza Organization | "Link this contact to its Organization, otherwise it won't sync to Matchpoint." |
| UC08 | Deal nuovo senza amount o close date, o con nome fuori formato | Task aggregato con link alla vista dei deal incompleti | "No close date yet. Put your best estimate: it goes straight into your country's forecast." |
| UC09 | Deal aperto senza attività né cambio di stage da 3 giorni | Task aggregato con link alla vista dei deal fermi, esclusi quelli su cui PNO ha già un task | "Nothing has moved here for 3 days. If you spoke to the client, log it; if not, a short call usually gets it going." |
| UC10 | Deal in Prepare Offer senza fee | Task aggregato con link alla vista dei deal senza fee | "Fill in the fees: the amount is calculated from them and stays at zero until you do." |
| UC13 | Deal in Closed Lost senza motivo, o "Timing not right" senza data di follow-up | Task aggregato con link alla vista dei deal da completare | "Add the follow-up date: HubSpot will remind you when it's time to call back." |

### Valutazione

UC12 e UC14 non controllano un dato: confrontano l'utente con i suoi obiettivi. Sono del valutatore, non dell'osservatore, e si costruiscono insieme ai riepiloghi (vedi `docs/decisions/ADR-001-osservatore-e-valutatore.md`). Gli obiettivi si danno a Polyant da un documento o una tabella.

| \# | Trigger | Cosa fa l'agente | Esempio |
| :---- | :---- | :---- | :---- |
| UC12 | Deal in Contract Signed | Riconoscimento, avanzamento sul trimestre, controllo dei dati di progetto | "Contract signed, well done: 2 of 3 this quarter. Project data is complete, so the handover can start." |
| UC14 | Giovedì, utente sotto un target settimanale | Task con un passo per rientrare entro venerdì | "You're at 3 of 5 deals worked this week. Two of yours have been quiet since Monday: one update each and you're there." |

### Andamento

| \# | Trigger | Cosa fa l'agente |
| :---- | :---- | :---- |
| UC15 | Lunedì | Riepilogo settimanale all'utente, come task con un testo breve (sezione 7\) |
| UC16 | Passaggio ad "adottato" | Riconoscimento |
| UC17 | Passaggio ad "a rischio" | Task a Team Leader per avvisarlo del fatto che \[user\] è in difficoltà |
| UC18 | Badge o serie raggiunti | Riconoscimento (sezione 6\) |
| UC19 | Lunedì | Quadro per Exelab: utenti per stato e per country, utenti a rischio con l'ultimo segnale, target e obiettivi raggiunti, esercizi completati. Recapitato agli utenti Exelab nel portale del cliente, come Slack o Email: si parte dalla soluzione più semplice da implementare |

In memoria per ogni utente: country, team, ruolo, baseline, stato nel tempo, esercizi fatti e scaduti, dove fatica, ultimi task e se hanno prodotto un'azione. L'agente non ripete esercizi già completati.

## 5\. Esercizi

Ogni esercizio è un task con micro-guida di due o tre passi e link all'articolo della knowledge base HubSpot. Nell'MVP l'esercizio risulta fatto quando l'utente spunta il task. La colonna a destra indica il dato su cui si potrà verificare il completamento: la verifica sui dati è personalizzazione a pagamento.

| \# | Esercizio | Micro-guida (task, in inglese) | Verifica sui dati (upsell) |
| :---- | :---- | :---- | :---- |
| D1 | Collega l'email | Install the HubSpot add-in from the Outlook store (not from HubSpot) and keep logging on for client emails | Prima email tracciata |
| D2 | Collega il calendario | Connect your Outlook calendar in HubSpot settings | Primo meeting sincronizzato |
| D3 | Logga la prima attività | Open an Organization you work on (create it if it's not there yet), log your last call or meeting with a short note | Prima attività |
| D4 | Crea il primo deal | From that Organization, create a deal named Topic \- Country \- Client Name | Primo deal |
| D5 | Personalizza la scheda | Customize the right sidebar and the sections of a record so the fields you use most are on top | Spunta |
| D6 | Usa le viste preparate | Open the views prepared for your team and check they show the records you expect | Spunta |
| D7 | Email da template | Send an email from a record using one of the templates | Email loggata |
| D8 | App mobile | Install the HubSpot mobile app, find a contact and log a note from your phone | Attività loggata da mobile |
| P1 | Notifiche e vista personale | Set the notifications you really need, then save a view of your open deals | Vista salvata |
| P2 | Organization senza duplicati | Search the domain first; create the Organization only if it doesn't exist, with the domain filled in | Organization con dominio, nessun duplicato |
| P3 | Contact associato | Create the contact from its Organization, or link it right after | Contact associato |
| P4 | Slot per la prima intervista | In the email, use Insert proposal times and offer two or three slots | Email loggata o meeting creato |
| P5 | Deal completo | Name: Topic \- Country \- Client Name (Role, C or P in consortia). Add estimated amount and close date | Nome, amount e close date |
| P6 | Playbook in prima intervista | Open the deal, launch "PNO \- First Interview qualification", fill it during the call | Playbook compilato |
| P7 | Prepare Offer | Move the deal to Prepare Offer and fill in the required fields and the fees | Stage e campi compilati |
| P8 | Invio offerta | Send the offer, move the deal to Negotiation, set the offer sent date | Stage e data |
| P9 | Collega di un'altra country | Add your colleague in Other PNO Contacts and tag them in a note | Campo e nota con menzione |
| P10 | Follow-up | Create a follow-up task; close it when the client replies (it doesn't close on its own) | Task completato |
| P11 | Chiusura | Contract Signed: type of remuneration, project name, project ID, type of service, start and end date, notes, fees. Closed Lost: reason, and follow-up date if "Timing not right" | Stage e campi compilati |
| P12 | Parent e child | Link a subsidiary to its parent Organization | Associazione |
| P13 | NL | Create a Dutch Organization with KvK or Vestigingsnummer, working language and Tax ID | Campi compilati |
| P14 | BE | Create a Belgian Organization with the AFAS required fields | Campi compilati |
| P15 | NO | Log all this week's sales activities in HubSpot; after signing, the project moves to SuperOffice | Attività loggate |
| P16 | Country manager | Open the Team activity timeline report and check your team's week | Spunta |

Il country manager fa D1-D8 e P16. Gli esercizi specifici di country si attivano solo per quella country.

## 6\. Gamification

Gli esercizi seguono il processo di vendita in quattro livelli. Il livello successivo si sblocca quando il precedente è completato.

| Livello | Esercizi | Badge |
| :---- | :---- | :---- |
| 1\. Set-up | D1, D2, D3, D5, D6, D7, D8, P1 | Ready to sell |
| 2\. Prospecting | P2, P3, P4 (+ P13 o P14) | First contact pro |
| 3\. Pipeline | D4, P5, P6, P7, P8, P10 | Pipeline builder |
| 4\. Closing | P9, P11 (+ P15) | Deal closer |

Badge di risultato:

| Badge | Quando |
| :---- | :---- |
| First signature | Primo Contract Signed |
| Clean pipeline | Una settimana senza deal fermi da più di 3 giorni |
| On a roll | 4 settimane di fila con tutti i target settimanali |
| Quarter done | Obiettivi del trimestre raggiunti |

**Serie:** settimane consecutive con tutti i target settimanali raggiunti. **Benchmark anonimo** (fuori MVP, add-on): posizione rispetto ai pari ruolo della propria country, senza nomi.

## 7\. Riepiloghi

**All'utente, ogni lunedì, come task:**

> **Your HubSpot week, 5-9 October** This week: 1 new Organization, 6 deals worked, 7 activities logged. All weekly targets hit. This quarter: 4 of 12 Organizations, 1 of 2 contracts signed. Level 3, Pipeline builder. Streak: 3 weeks. Next step: move your offer for Acme to Negotiation once it's sent.

**A Exelab, ogni lunedì, come task nel portale del cliente:** per country e team, utenti per stato e variazione sulla settimana, utenti a rischio con l'ultimo segnale, target settimanali e obiettivi trimestrali raggiunti, livelli ed esercizi completati.

## 8\. FAQ per l'agente

Risposte da usare nelle micro-guide e, quando ci sarà la chat, nelle risposte.

| Domanda | Risposta |
| :---- | :---- |
| Lead, contact o deal? | PNO non usa l'oggetto Lead. Si lavora con contact e Organization; creare il deal equivale a qualificare l'opportunità |
| Come evito un'azienda doppia? | Cerca per dominio prima di creare (il dominio è la parte dell'email dopo la @). HubSpot avvisa solo se dominio o email sono compilati |
| Posso unire due duplicati? | Sì, se sono della tua country. Tra country diverse serve un admin |
| Chi vede note e task? | Tutto il team della tua country |
| Come lavoro con un collega di un'altra country? | Aggiungilo in Other PNO Contacts e taggalo in una nota |
| Posso non registrare un'email? | Sì, disattiva il logging nell'add-in prima di inviare. Le email interne PNO non si registrano |
| Non trovo l'add-in di Outlook | Si installa dallo store di Outlook, non da HubSpot |
| Come nomino un deal? | Topic \- Country \- Client Name (Role), con C coordinator o P partner nei consorzi. Contratti quadro: FC \- Client Name, un deal per ogni progetto annuale |
| Fee fisse e success fee: due deal? | No, un deal. Compila le singole fee: l'amount si calcola da lì |
| Cosa compilo a Contract Signed? | Type of remuneration, project name, project ID, type of service, date di inizio e fine, note, fee |
| Deal perso, ma il cliente può tornare | Closed Lost con "Timing not right" e data di follow-up: HubSpot crea il task di ricontatto |
| Ho spostato un deal per errore | View all properties, cronologia della property Deal stage |
| Il reminder sull'offerta si chiude da solo? | No, va chiuso a mano |
| Un contatto su più Organization? | Sì, si può associare a tutte |
| Manca un valore nella lista Program | Lo aggiunge solo un admin |
| Posso modificare il playbook? | No, solo un admin |
| Country manager: attività del team? | Report Team activity timeline, filtrato sul tuo team |
| NL: creo l'organizzazione in AFAS? | No, in HubSpot con KvK o Vestigingsnummer, lingua di lavoro e Tax ID; il connettore la porta in AFAS |
| NO: dove registro le attività? | La vendita in HubSpot; dopo la firma, progetto e comunicazioni in SuperOffice |

## 9\. Da aggiungere in seguito

Non fanno parte della PoC.

- **Country manager con target di team.** Il country manager ha come target la somma dei target delle persone del suo team, per settimana e per trimestre; nei suoi riepiloghi vede il totale del team rispetto alla somma; il suo stato si calcola sui target del team. Il lunedì riceve un task quando un membro del team non ha raggiunto il target settimanale.

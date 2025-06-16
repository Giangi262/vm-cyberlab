# vm-cyberlab-info

Disclaimer Etico e Legale
Questo laboratorio è stato creato esclusivamente a scopo educativo e didattico.
Tutti gli attacchi simulati vengono eseguiti su macchine virtuali controllate e configurate appositamente per essere vulnerabili.
Mi dissocio completamente da qualsiasi uso illecito, dannoso o non autorizzato delle tecniche mostrate.
L’obiettivo è capire come funzionano gli attacchi per poterli riconoscere, prevenirli e difendere i sistemi reali.

Laboratorio di sicurezza informatica con macchine virtuali Kali Linux e Metasploitable 2, Pfsense e Windows Xp/10. Installazione

Virtualizzazione
Nel mondo della cybersecurity e dell’ethical hacking, uno dei concetti che sentirai nominare spesso è la virtualizzazione.
Ma che cos’è, in parole semplici?
La virtualizzazione è una tecnologia che ci permette di prendere un computer fisico — come un server o anche il nostro portatile — e "dividerlo" in più computer virtuali, che funzionano ognuno come se fossero veri e separati.
È un po’ come se un unico computer fosse in grado di ospitare altri computer al suo interno, ognuno con il proprio sistema operativo e le proprie applicazioni, ma senza bisogno di hardware aggiuntivo. Questi “mini-computer” si chiamano macchine virtuali, o VM.
Perché si fa tutto questo?
Beh, ci sono tanti motivi, ma i principali sono:
si risparmia: invece di comprare cinque PC, posso usarne uno solo ben potente,
si ottimizzano le risorse: non lascio inutilizzata metà della RAM o della CPU del mio computer,
e si guadagna in flessibilità: posso creare una macchina virtuale, provarci cose (anche sbagliate), e poi cancellarla senza fare danni.
Un esempio pratico?
Immagina di avere un server fisico con 32 GB di RAM e 8 CPU. Con la virtualizzazione, puoi decidere di creare 4 macchine virtuali. A ciascuna assegni 8 GB di RAM e 2 CPU. Così, all’interno di un solo computer, ne hai creati quattro virtuali.
Questa divisione permette a più sistemi operativi di funzionare contemporaneamente sullo stesso hardware fisico. È molto usata nei laboratori di cybersecurity, perché ti permette di simulare attacchi e difese senza toccare il sistema reale o mettere in pericolo la rete vera.
In breve, la virtualizzazione è la base per creare ambienti di test, studiare attacchi, difese e imparare senza rischiare. È come avere un campo di addestramento tutto tuo, direttamente nel tuo computer.

Quando parliamo di virtualizzazione, uno degli strumenti più importanti è l’hypervisor.
Ma cos’è, esattamente?
L’hypervisor è un programma speciale che ha il compito di creare, gestire e far funzionare le macchine virtuali (VM).
Senza di lui, la virtualizzazione non esisterebbe: è lui che divide le risorse fisiche (come CPU, RAM e disco) tra le varie VM.

Hypervisor di Tipo 1 (Bare-Metal)
Gli hypervisor di tipo 1, chiamati anche bare-metal, sono quelli che vengono installati direttamente sull’hardware fisico, come se fossero loro stessi il sistema operativo del computer.
In pratica, non serve Windows, Linux o qualsiasi altro sistema operativo prima: appena accendi il computer, parte subito l’hypervisor.
Questo tipo di hypervisor è molto usato nei datacenter, nei server aziendali, e in contesti dove servono prestazioni elevate e massima stabilità.
I suoi vantaggi principali:
Ha accesso diretto all’hardware, quindi funziona in modo più veloce e più efficiente
Ha meno ritardi (latenze) tra le richieste delle VM e il processore
È più stabile e sicuro, perché non dipende da un sistema operativo che potrebbe andare in crash

Hypervisor di Tipo 2 (Hosted) 
Gli hypervisor di tipo 2, detti anche hosted, sono quelli che non si installano direttamente sull’hardware del computer, ma funzionano dentro un sistema operativo già esistente, come Windows, macOS o Linux.
Immagina il tuo PC personale: hai Windows installato, apri VirtualBox, e da lì crei e gestisci le macchine virtuali.
Ecco, VirtualBox è un hypervisor di Tipo 2.
Come funziona?
Il sistema operativo host (es. Windows) gestisce le risorse hardware del computer: RAM, CPU, disco…
L’hypervisor (es. VirtualBox) si appoggia su questo sistema operativo e ti permette di creare, avviare e controllare le macchine virtuali
Quindi, tutto passa prima attraverso il sistema operativo, poi arriva alle VM.
Esempi comuni di hypervisor di tipo 2:
VirtualBox (gratuito, molto usato nei corsi e laboratori)
Vantaggi:
Facile da installare e usare
Perfetto per chi studia o fa test in locale
Non serve cambiare sistema operativo o configurazioni complesse
Svantaggi:
È meno veloce rispetto al tipo 1, perché ogni azione deve passare anche dal sistema operativo host
Meno stabile in ambienti critici (es. server aziendali)
In poche parole:
Se stai imparando la cybersecurity o vuoi fare test sul tuo computer, l’hypervisor di tipo 2 è quello perfetto per te. È semplice, gratuito e ti permette di fare tutto quello che ti serve in un ambiente virtuale sicuro.

Container e Docker – Virtualizzazione di livello 3 
Negli ultimi anni, accanto alla virtualizzazione classica con le macchine virtuali (VM), è nata una tecnologia più leggera, più veloce e più portatile: si chiama containerizzazione.
Una delle piattaforme più famose per usare i container è Docker.
Come funziona?
Con Docker e i container, non crei copie intere del computer (come con le macchine virtuali),
ma usi il tuo sistema operativo, dividendolo in tanti ambienti isolati, ognuno dedicato a un'app diversa.
Ogni container ha:
la sua app
le sue librerie
le sue impostazioni
Ma tutti usano lo stesso sistema operativo principale, cioè il tuo.
Esempio concreto:
Immagina il tuo computer come una pizza intera 🍕:
Con le macchine virtuali, prepari una pizza intera per ogni persona (cioè per ogni app), ognuna col suo impasto (sistema operativo) → pesante e lento
Con i container, tagli la stessa pizza in fette, ognuna con gusti diversi (cioè le app) → veloce e leggero
Poi quando parliamo di librerie nei container (come Docker), ci riferiamo a librerie di programmazione o di sistema.
Le librerie sono pezzi di codice già pronti che aiutano i programmi a funzionare, e sì, sono pensate per la programmazione.
Quindi, in breve:
I container non contengono un sistema operativo intero,
ma solo l'app + librerie necessarie, e usano il sistema operativo del computer dove girano.

Creazione di un Laboratorio Virtuale per il Pentesting – spiegato semplice
Se vogliamo imparare davvero come ragionano gli hacker, come attaccano un sistema e quali strumenti usano, non basta la teoria.
Dobbiamo mettere le mani in pasta. Serve un ambiente dove possiamo provare tutto in sicurezza, senza rischiare danni veri.

Per questo motivo, (e anche per esercitarci da soli), costruiremo un vero e proprio laboratorio virtuale.
A cosa serve questo laboratorio?
L'obiettivo è simulare attacchi informatici reali, come fanno i criminali, per:
capire dove e come un sistema può essere vulnerabile,
testare strumenti di attacco e tecniche difensive,
imparare a pensare come un hacker, per diventare più bravi a difendere.
E soprattutto, farlo in un ambiente controllato, sicuro e legale, usando la virtualizzazione.
Cosa useremo per costruirlo?
Per creare questo laboratorio, ci affideremo a VirtualBox, un software gratuito che ci permette di creare più “computer virtuali” dentro al nostro PC.
Le 3 macchine virtuali che useremo inizialmente
1. Kali Linux – la macchina attaccante
È una distribuzione Linux pensata per il penetration testing.
Ha già installati strumenti come:
Nmap (scansione),
Metasploit (exploit),
Burp Suite (analisi web),
e molti altri.
È la macchina dell'hacker etico, da cui lanceremo gli attacchi.
2. Metasploitable 2 – la prima macchina bersaglio
È una macchina deliberatamente vulnerabile, pensata proprio per essere attaccata.
Serve per fare pratica con exploit reali, testare Metasploit e simulare intrusioni in modo realistico.
3. Windows 10/Xp – un secondo bersaglio
Serve per simulare un computer “vero” di un utente, come quelli che troviamo in azienda.
Qui possiamo testare:
attacchi tramite phishing,
exploit di servizi Windows,
movimenti laterali in rete.
In sintesi
Stiamo creando un mini mondo virtuale, con attaccanti e vittime, per simulare attacchi veri in un ambiente sicuro.
È il miglior modo per imparare davvero la cybersecurity: provare sul campo.

Un po’ di terminologia utile:
Termine	                          Significato
Hardware	                        Le parti fisiche del tuo PC (RAM, CPU, disco, ecc.)
Sistema operativo (host)	        Il sistema operativo del tuo computer (es. Windows 10)
Software di virtualizzazione	    Il programma che gestisce le macchine virtuali (es. VirtualBox)
Sistema operativo (guest)	        Il sistema operativo che installi dentro la macchina virtuale (es. Kali Linux)
App (nelle VM)	                  I programmi che girano dentro la macchina virtuale (es. Metasploit)

Cosa possiamo fare con le schede di rete virtuali?
Con queste schede possiamo:
far parlare tra loro solo le VM, lasciandole isolate dal resto del mondo;
permettere la comunicazione tra la VM e il PC reale;
dare accesso a Internet alla macchina virtuale.
Le modalità principali (che vedrai in VirtualBox):
Modalità	                             Cosa fa	Quando si usa
NAT	                                   La VM può accedere a Internet, ma non può essere raggiunta da fuori	Per aggiornare tool in Kali o scaricare file
Bridged Adapter	                       La VM è sulla stessa rete del tuo PC, come se fosse un altro dispositivo	Per fare attacchi su rete reale (es. contro un altro PC fisico)
Internal Network	                     Le VM comunicano solo tra loro, niente Internet, niente host	Per simulare attacchi tra due VM isolate
Host-Only Adapter	                     Le VM parlano con il tuo PC (host) ma non vanno su Internet	Per analizzare traffico, fare scanning dal tuo PC
Esempio pratico:
Se vuoi che Kali attacchi Metasploitable ma nessuna delle due abbia accesso a Internet → usi Internal Network
Se vuoi aggiornare Kali da Internet → usi NAT
Se vuoi che Kali possa "vedere" anche il tuo PC reale → usi Host-Only
In sintesi
Le schede di rete virtuali ti permettono di controllare completamente le connessioni nel tuo laboratorio.
Puoi decidere chi parla con chi, se le macchine sono isolate o se accedono a Internet, a seconda di quello che vuoi testare.





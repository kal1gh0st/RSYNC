# RSYNC
![immagine](https://user-images.githubusercontent.com/56889513/117019303-94e60680-acf5-11eb-8d0d-e9a56f063ce6.png)

Il nome rsync indica un protocollo di rete per la sincronizzazione dei file che risale al 1996 ed è stato sviluppato, tra gli altri, da Andrew Tridgell, principale responsabile del progetto SAMBA. Oltre al protocollo, esiste uno strumento con lo stesso nome che consente la comunicazione. L'applicazione con licenza GPL può essere utilizzata gratuitamente e trasferisce i dati da una directory di origine alla directory di destinazione desiderata, in locale o su una rete pubblica. Rsync confronta la dimensione dei file e il tempo di creazione di tutti i file nelle cartelle di origine e di destinazione in modo che solo i file modificati debbano essere copiati a ogni sincronizzazione. Per questo, l'operazione di backup di rsync è indicata come un backup incrementale, che ha il vantaggio di poter essere eseguita rapidamente e occupa poco spazio.

 N.B.
rsync è disponibile per tutti i comuni sistemi operativi UNIX come OS/2, Linux o macOS. Grazie al wrapper API Cygwin è utilizzabile anche su Microsoft Windows.

Oltre al backup dei dati e alla generazione dei cosiddetti server mirror (immagini complete del server), gli scenari di utilizzo tipici di rsync includono la sincronizzazione dei dati in aziende con posizioni diverse e una connessione dati debole. In particolare, quest'ultima funzione oggi è quasi esclusivamente adottata dalle moderne tecnologie cloud, anche perché una connessione dati debole è sempre meno comune.

Riepilogo delle principali opzioni di rsync
I backup di rsync si caratterizzano per l'elevata efficienza. L'approccio incrementale garantisce un utilizzo minimo della rete, il che è particolarmente utile per file di grandi dimensioni, indipendentemente dal fatto che le modifiche a questi file siano molte o minime. Come strumento a riga di comando, rsync funziona per impostazione predefinita tramite il terminale o tramite il prompt dei comandi se si utilizza rsync su un dispositivo Windows. Le immissioni hanno sempre la seguente sintassi:

rsync -(-)Opzioni Percorso di origine Percorso di destinazione
I percorsi di origine e destinazione devono indicare la rispettiva directory di origine e la directory in cui rsync deve archiviare la copia di backup. Le opzioni, che possono essere abbreviate con lettere o scritte per intero, definiscono le singole impostazioni dei backup di rsync. I parametri più importanti, che possono essere combinati liberamente, sono riassunti nella seguente tabella:

Opzione

Funzione

-r, --recursive

Il backup di rsync considera tutte le sottodirectory contenute

-u, --update

Istruzione per saltare i file più recenti nella directory di destinazione rispetto alla directory di partenza

-c, --checksum

Differenziazione dei file di origine e di destinazione in base ai checksum

-l, --links

I collegamenti simbolici vengono copiati come tali (e non come file)

-p, --perms

Le autorizzazioni sui file vengono mantenute

-g, --group

Le autorizzazioni di gruppo sui file vengono mantenute

-t, --times

Le marche temporali dei file (ultima modifica) vengono mantenute

-o, --owner

Il proprietario del file viene mantenuto (solo se amministratore)

-D, --devices

I dati del dispositivo vengono mantenuti

-z, --compress

Compressione automatica dei file trasmessi

--compress-level=NUM

Determinazione del grado di compressione; è possibile un valore (“NUM”) compreso tra 0 (nessuna compressione) e 9 (compressione massima)

-v, --verbose

Maggiori dettagli durante il processo di backup

-q, --quiet

Nasconde tutti i dettagli sul processo di backup (tranne i messaggi di errore)

-a, --archive

Modalità di archiviazione, che è la modalità predefinita ed è identica alla combinazione di opzioni -rlptgoD

-n, --dry-run

Esecuzione del test: non vengono apportate modifiche effettive

-h, --help

Menu di aiuto (può essere utilizzato solo senza specificare directory di origine e destinazione o altri argomenti)

--bwlimit=KBPS

Limitazione della larghezza di banda (kilobyte al secondo); ad esempio  --bwlimit=30 (limite di 30 kbit/s)

                --exclude=MODELLO

Esclusione di un modello dalla sincronizzazione; ad esempio --exclude cartella di esempio (la cartella di esempio non verrà sincronizzata.)

--delete

Eliminazione di tutti i file che si trovano nella directory di destinazione ma non nella directory di origine

--progress

Visualizzazione della durata del backup di rsync e della velocità di trasmissione

--list-only

Elenco dei file anziché di un backup

--stats

Rapporto dettagliato sui dati trasferiti (numero, dimensioni)

--max-size=SIZE

Definizione di una dimensione massima del file; ad esempio --max-size=10MB (verranno trasferiti solo file di dimensioni fino a 10 MB.)

--ignore-errors

Sospende l'interruzione del processo di backup in caso di errore

Configurare i backup di rsync su server Linux
Per utilizzare rsync su sistemi operativi Linux, installate il protocollo nell'omonimo pacchetto e create i backup utilizzando i comandi del terminale. In alternativa, è possibile utilizzare applicazioni come Back In Time, rsnapshot (per backup automatici regolari) o Unison, che consentono il controllo del processo di backup tramite un'interfaccia grafica. Di seguito vi illustriamo i passaggi chiave per impostare i processi di backup con rsync, usando ad esempio Ubuntu.

Per impostazione predefinita, rsync è già installato su Ubuntu. In caso contrario, recuperate l'installazione utilizzando il comando seguente:

sudo apt-get install rsync
Se rsync è installato, utilizzate i comandi del terminale desiderati per specificare la directory di origine e di destinazione, nonché le opzioni di backup. Ad esempio, è possibile eseguire la modalità predefinita (“Archivio”) come segue:

rsync -a Directory di origine Directory di destinazione

| Risorsa | Limite predefinito |
| --- | --- |
| Numero di account di archiviazione per sottoscrizione |200<sup>1</sup> |
| Capacità massima dell'account di archiviazione |500 TB<sup>2</sup> |
| Numero massimo di contenitori BLOB, BLOB, condivisioni file, tabelle, code, entità o messaggi per account di archiviazione |Nessun limite |
| Dimensione massima di un singolo contenitore BLOB o di una singola tabella o coda |Uguale alla capacità massima dell'account di archiviazione |
| Numero massimo di blocchi in un BLOB in blocchi o in un BLOB in coda |50.000 |
| Dimensione massima di un blocco di un BLOB in blocchi |100 MB |
| Dimensione massima di un BLOB in blocchi |50.000 x 100 MB (circa 4,75 TB) |
| Dimensione massima di un blocco in un BLOB di aggiunta |4 MB |
| Dimensione massima di un BLOB di aggiunta |50.000 x 4 MB (circa 195 GB) |
| Dimensione massima di un BLOB di pagine |8 TB |
| Dimensione massima di un'entità di tabella |1 MB |
| Numero massimo di proprietà di un'entità di tabella |252 |
| Dimensione massima di un messaggio in una coda |64 KB |
| Dimensione massima di una condivisione file |5 TB |
| Dimensione massima di un file in una condivisione file |1 TB |
| Numero massimo di file in una condivisione file |Solo il limite è hello 5 TB totali di capacità della condivisione file hello |
| Numero massimo di operazioni di I/O al secondo per condivisione |1000 |
| Numero massimo di file in una condivisione file |Solo il limite è hello 5 TB totali di capacità della condivisione file hello |
| Numero massimo di criteri di accesso archiviati per ogni contenitore, condivisione di file, tabella o coda |5 |
| Frequenza massima di richieste per account di archiviazione |BLOB: 20.000 richieste al secondo<sup>2</sup> per i BLOB di qualsiasi dimensione valido (limitate solo dai limiti di ingresso/uscita dell'account hello) <br />File: 1000 operazioni di I/O al secondo (con dimensione di 8 KB) per condivisione file <br />Code: 20.000 messaggi al secondo (supponendo una dimensione dei messaggi di 1 KB)<br />Tabelle: 20.000 transazioni al secondo (supponendo una dimensione delle entità di 1 KB) |
| Velocità effettiva da raggiungere per BLOB singolo |Backup too60 MB al secondo o backup too500 richieste al secondo |
| Velocità effettiva da raggiungere per coda singola (messaggi di 1 KB) |Too2000 messaggi al secondo |
| Velocità effettiva da raggiungere per partizione di tabella singola (entità di 1 KB) |Le entità too2000 al secondo |
| Velocità effettiva da raggiungere per singola condivisione di file |Backup too60 MB al secondo |
| Traffico in ingresso massimo<sup>3</sup> per account di archiviazione (aree degli Stati Uniti) |10 Gbps con archiviazione GRS/ZRS<sup>4</sup> abilitata, 20 Gbps per LRS<sup>2</sup> |
| Traffico in uscita massimo<sup>3</sup> per account di archiviazione (aree degli Stati Uniti) |20 Gbps con archiviazione RA-GRS/GRS/ZRS<sup>4</sup> abilitata, 30 Gbps per LRS<sup>2</sup> |
| Traffico in ingresso massimo<sup>3</sup> per account di archiviazione (aree non degli Stati Uniti) |5 Gbps con archiviazione GRS/ZRS<sup>4</sup> abilitata, 10 Gbps per LRS<sup>2</sup> |
| Traffico in uscita massimo<sup>3</sup> per account di archiviazione (aree non degli Stati Uniti) |10 Gbps con archiviazione RA-GRS/GRS/ZRS<sup>4</sup> abilitata, 15 Gbps per LRS<sup>2</sup> |

<sup>1</sup>Sono inclusi gli account di archiviazione Standard e Premium. Se sono necessari più di 200 account di archiviazione, inviare una richiesta tramite il [supporto tecnico di Azure](https://azure.microsoft.com/support/faq/). il team di archiviazione di Azure Hello esamina il caso aziendale e può approvare too250 gli account di archiviazione. 

<sup>2</sup> tooget toogrow precedenti di account di archiviazione standard hello annunciato i limiti di capacità, in ingresso e uscita e richiesta di velocità, verificare una richiesta tramite [supporto Azure](https://azure.microsoft.com/support/faq/). il team di archiviazione di Azure Hello esamina richiesta hello e può approvare limiti più elevati in caso per caso.

<sup>3</sup>*in ingresso* fa riferimento a dati tooall (richieste) inviati tooa account di archiviazione. *In uscita* fa riferimento tooall dati (risposte) ricevuti da un account di archiviazione.  

<sup>4</sup>Le opzioni di replica di Archiviazione di Azure includono:
* **RA-GRS**: Archiviazione con ridondanza geografica e accesso in lettura. Se RA-GRS è abilitata, le destinazioni in uscita per la posizione secondaria hello sono toothose identici per la posizione primaria hello.
* **GRS**: archiviazione con ridondanza geografica. 
* **ZRS**: archiviazione con ridondanza della zona. Disponibile solo per i BLOB in blocchi. 
* **LRS**: archiviazione con ridondanza locale. 



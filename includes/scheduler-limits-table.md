Hello nella tabella seguente vengono descritti i limiti, le quote principali hello, impostazioni predefinite e le limitazioni nell'utilità di pianificazione di Azure.

| Risorsa | Descrizione del limite |
| --- | --- |
| **Dimensioni del processo** |La dimensione massima del processo è di 16 K. Se un'operazione PUT o PATCH determina un processo di dimensioni maggiori rispetto a questi limiti, viene restituito un codice di stato 400 di richiesta non valida. |
| **Dimensioni dell’URL della richiesta** |Dimensione massima dell'URL di richiesta hello è 2.048 caratteri. |
| **Dimensioni aggregate dell'intestazione** |Le dimensioni aggregate massime dell'intestazione sono di 4.096 caratteri. |
| **Numero di intestazioni** |Il numero massimo di intestazioni è di 50 intestazioni. |
| **Dimensioni del corpo** |La dimensione massima del corpo è di 8.192 caratteri. |
| **Intervallo di ricorrenza** |L’intervallo massimo delle ricorrenze è di 18 mesi. |
| **Ora toostart ora** |"Ora toostart ora" massimo è 18 mesi. |
| **Cronologia processi** |Le dimensioni massime dei corpi delle risposte archiviati nella cronologia processi è di 2.048 byte. |
| **Frequenza** |quota di frequenza massima predefinita di Hello è 1 ora in una raccolta di processi gratuita e 1 minuto in una raccolta di processi standard. frequenza max Hello è configurabile in un toobe raccolta processo inferiore hello massimo. Tutti i processi nella raccolta di processi hello sono valore hello limitato impostato per la raccolta di processi hello. Se si tenta di un processo con una frequenza maggiore rispetto a frequenza massima di hello nella raccolta di processi hello toocreate richiesta avrà esito negativo con un codice di stato di conflitto 409. |
| **Processi** |quota massima processi di Hello predefinita è 5 processi in una raccolta di processi gratuita e 50 in una raccolta di processi standard. numero massimo di Hello di processi è configurabile in una raccolta di processi. Tutti i processi nella raccolta di processi hello sono valore hello limitato impostato per la raccolta di processi hello. Se si tenta di toocreate più processi rispetto alla quota massima processi hello quindi richiesta hello ha esito negativo con un codice di stato di conflitto 409. |
| **Raccolte processi** |Il numero massimo di raccolte processi per ogni sottoscrizione è 200.000. |
| **Periodo di memorizzazione della cronologia dei processi** |Cronologia processo viene mantenuta per i mesi too2 o backup toohello ultimo esecuzioni di 1000. |
| **Memorizzazione di processi completati e con errori** |I processi completati e con errori vengono conservati per 60 giorni. |
| **Timeout** |Esiste un timeout delle richieste statico (non configurabile) di 60 secondi per le azioni HTTP. Per le operazioni in esecuzione più lungo, seguire i protocolli HTTP asincroni; ad esempio, restituire immediatamente un codice 202, ma continuare a lavorare in background hello. |


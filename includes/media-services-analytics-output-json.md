processo Hello produce un file di output JSON che contiene i metadati relativi a facce rilevati e registrati. metadati Hello includono le coordinate che indica il percorso di hello di facce, nonché un viso ID numerico che indica hello di rilevamento della persona. Numeri di ID tipo di carattere sono tooreset soggetta a circostanze quando frontale hello viene smarrito o sovrapposta nel frame hello, risultante in alcune persone più ID di assegnazione.

Hello output che JSON include hello gli attributi seguenti:

| Elemento | Descrizione |
| --- | --- |
| version |Si riferisce toohello versione di hello API Video. |
| index | (Si applica solo tooAzure Media Redactor) definisce l'indice di frame hello dell'evento corrente hello. |
| timescale |"Tick" al secondo del video hello. |
| offset |Si tratta di differenza di orario hello dei timestamp. Nella versione 1.0 delle API Video, questo valore è sempre 0. Negli scenari futuri supportati questo valore potrebbe cambiare. |
| framerate |Fotogrammi al secondo di hello video. |
| fragments |metadati Hello sono suddivise denominate frammenti di segmenti diversi. Ogni frammento contiene un inizio, una durata, un numero di intervallo e uno o più eventi. |
| start |Hello ora di inizio del primo evento di hello in 'tick'. |
| duration |lunghezza di Hello del frammento di hello, in "tick". |
| interval |intervallo di Hello di ogni voce di evento all'interno di frammento hello, in "tick". |
| eventi |Ogni evento contiene i caratteri tipografici hello rilevare e analizzare le entro tale periodo di tempo. È una matrice di eventi. matrice esterno Hello rappresenta un intervallo di tempo. matrice interna Hello è costituita da 0 o più eventi che si sono verificati a questo punto nel tempo. Le parentesi quadre vuote [] indicano che non sono stati rilevati volti. |
| id |Hello l'ID del tipo di carattere hello viene tenuta traccia. Questo numero potrebbe cambiare inavvertitamente se un volto non viene rilevato. Un utente specificato deve avere hello ID in tutto hello video generale, ma questo non può essere garantito scadenza toolimitations nell'algoritmo di rilevamento hello (occlusione e così via) |
| x, y |Hello in alto a sinistra X e y pari hello affrontano rettangolo in una scala normalizzata di too1.0 0,0. <br/>-X e Y coordinate sono toolandscape relativo sempre, pertanto se si dispone di un ritratto video (o rivolta verso il basso, nel caso di hello di iOS), sarà necessario conseguenza tootranspose hello coordinate. |
| width, height |Hello larghezza e altezza del carattere tipografico hello rettangolo in una scala normalizzata di too1.0 0,0. |
| facesDetected |Ciò viene trovato alla fine hello risultati JSON hello e riepiloga il numero di hello di facce algoritmo hello rilevato durante hello video. Poiché può essere reimpostato inavvertitamente hello ID se viene rilevato un tipo di carattere (ad esempio carattere viene disattivato schermata, è assente), questo numero non può sempre uguale hello true svariate facce video hello. |


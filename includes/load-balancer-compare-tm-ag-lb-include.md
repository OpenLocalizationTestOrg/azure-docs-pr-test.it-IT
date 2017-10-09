## <a name="load-balancer-differences"></a>Differenze del servizio di bilanciamento del carico

Sono disponibili il traffico di rete toodistribute diverse opzioni utilizzando Microsoft Azure. Queste opzioni funzionano in modo diverso, vantano un set di funzionalità differenti e supportano diversi scenari. Possono essere utilizzate singolarmente o in combinazione.

* **Il bilanciamento del carico Azure** funziona a livello di trasporto hello (livello 4 nello stack di riferimento di hello OSI rete). Consente la distribuzione a livello di rete del traffico tra le istanze di un'applicazione in esecuzione in hello stesso data center di Azure.
* **Gateway applicazione** funziona al livello di applicazione hello (livello 7 nello stack di riferimento di hello OSI rete). Opera come un servizio proxy inverso, chiusura connessione client hello e inoltro richiede gli endpoint tooback-end.
* **Gestione traffico** opera a livello DNS hello.  Usa gli endpoint di tooglobally distribuita traffico degli utenti finali toodirect le risposte DNS. I client quindi connettersi direttamente toothose endpoint.

Hello nella tabella seguente vengono riepilogate le funzionalità di hello offerte da ogni servizio:

| Service | Azure Load Balancer | gateway applicazione | servizio Gestione traffico |
| --- | --- | --- | --- |
| Tecnologia |Livello trasporto (livello 4) |Livello applicazione (livello 7) |Livello DNS |
| Protocolli di applicazioni supportati |Qualsiasi |HTTP, HTTPS e WebSocket |Qualsiasi (è richiesto un endpoint HTTP per il monitoraggio degli endpoint) |
| Endpoint |Istanze del ruolo VM e Servizi cloud di Azure |Un indirizzo IP interno di Azure, un indirizzo IP Internet pubblico, una VM di Azure o un servizio cloud di Azure |VM di Azure, Servizi Cloud, App Web di Azure ed endpoint esterni |
| Supporto della rete virtuale |Può essere utilizzato sia per applicazioni con connessione Internet sia per applicazioni interne (rete virtuale) |Può essere utilizzato sia per applicazioni con connessione Internet sia per applicazioni interne (rete virtuale) |Supporta solo applicazioni con connessione Internet |
| Monitoraggio degli endpoint |supportato tramite probe |supportato tramite probe |supportato tramite HTTP/HTTPS GET |

Azure bilanciamento del carico e Gateway applicazione route rete traffico tooendpoints ma dispongono di utilizzo diversi scenari toowhich traffico toohandle. Hello nella tabella seguente aiuta a differenza di hello informazioni sui servizi di bilanciamento del carico due hello:

| Tipo | Azure Load Balancer | gateway applicazione |
| --- | --- | --- |
| Protocolli |UDP/TCP |HTTP, HTTPS e WebSocket |
| Prenotazione IP |Supportato |Non supportate |
| Modalità di bilanciamento del carico |5 tuple (IP di origine, porta di origine, IP di destinazione, porta di destinazione, tipo di protocollo) |Round robin<br>Routing basato su URL |
| Modalità di bilanciamento del carico (IP di origine / sessioni permanenti) |2 tuple (IP di origine e IP di destinazione), 3 tuple (IP di origine, IP di destinazione e porta). Può aumentare o diminuire in base al numero di hello delle macchine virtuali |Affinità basata sui cookie<br>Routing basato su URL |
| Probe di integrità |Predefinito: intervallo di probe - 15 secondi. Esclusione dalla rotazione: 2 errori ripetuti. Supporta le probe definite dall'utente |Inattivo: intervallo di probe - 30 secondi. Esclusione dopo 5 errori consecutivi di traffico live o un errore di probe singolo in modalità di inattività. Supporta le probe definite dall'utente |
| Offload SSL |Non supportate |Supportato |
| Routing basato su URL | Non supportate | Supportato|
| Criteri SSL | Non supportate | Supportato|

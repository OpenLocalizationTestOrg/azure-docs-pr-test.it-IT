In questo passaggio si test listener del gruppo di disponibilità hello tramite un'applicazione client in esecuzione su hello stessa rete.

Connettività client presenta hello seguenti requisiti:

* Listener di toohello le connessioni client devono provenire da macchine che si trovano in un servizio cloud diverso da hello uno che gli host hello le repliche di disponibilità Always On.
* Se hello AlwaysOn repliche si trovano in subnet diverse, i client devono specificare *MultisubnetFailover = True* nella stringa di connessione hello. I risultati condizione connessione parallela tenta tooreplicas in hello subnet diverse. Questo scenario include la distribuzione di un gruppo di disponibilità AlwaysOn tra più aree.

Un esempio è tooconnect toohello listener da una delle macchine virtuali Ciao hello stessa rete virtuale di Azure (ma non quello che ospita una replica). Un modo semplice di toocomplete questo test è tootry tooconnect SQL Server Management Studio toohello gruppo di disponibilità. Un altro metodo semplice è toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), come segue:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Se il valore EndpointPort hello *1433*, non si toospecify richiesto nella chiamata di hello. Hello chiamata precedente presuppone anche quel computer client hello è unita in join toohello nello stesso dominio e il chiamante hello disponga delle autorizzazioni sul database hello utilizzando l'autenticazione di Windows.
> 
> 

Quando si testa il listener hello, essere toofail che su hello toomake gruppo di disponibilità assicurarsi che i client possono connettersi toohello listener attraverso i failover.


---
title: aaaConnect computer tooOMS utilizzando hello OMS Gateway | Documenti Microsoft
description: Collegare i dispositivi gestiti da OMS e i computer monitorati da Operations Manager con il servizio OMS toohello hello OMS Gateway toosend dati quando non hanno accesso a Internet.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Connettere i computer senza tooOMS accesso Internet usando hello OMS Gateway

Questo documento descrive come il OMS gestiti e i computer monitorati System Center Operations Manager possono inviare servizio OMS toohello di dati quando non hanno accesso a Internet. Hello Gateway OMS, che è un proxy di inoltro HTTP che supporta HTTP tunneling comando hello connessione HTTP, può raccogliere i dati e inviarla servizio OMS toohello per loro conto.  

Hello OMS Gateway supporta:

* Funzionalità Hybrid Runbook Workers di Automazione di Azure  
* I computer Windows con Microsoft Monitoring Agent hello connesso direttamente tooan area di lavoro OMS
* I computer Linux con hello agente OMS per Linux connesso direttamente tooan area di lavoro OMS  
* System Center Operations Manager 2012 SP1 con UR7, Operations Manager 2012 R2 con UR3 o il gruppo di gestione di Operations Manager 2016 integrato con OMS.  

Se i criteri di sicurezza IT non consentono i computer su toohello di tooconnect la rete Internet, ad esempio punto di vendita (POS) dispositivi o i server che supportano servizi IT, ma è necessario tooconnect tooOMS loro toomanage e monitorarli, che possono essere configurati toocommunicate direttamente con hello OMS Gateway tooreceive configuration e l'inoltro dei dati per loro conto.  Se questi computer sono configurati con hello OMS agent toodirectly connettersi tooan area di lavoro OMS, tutti i computer verranno invece comunicare con OMS Gateway hello.  gateway Hello trasferisce i dati da hello agenti tooOMS direttamente, non l'analisi dei dati di hello in transito.

Quando un gruppo di gestione di Operations Manager è integrato con OMS, il server di gestione di hello può essere configurato tooconnect toohello le informazioni di configurazione di Gateway di OMS tooreceive e inviare i dati raccolti a seconda della soluzione hello che è stata abilitata.  Agenti di Operations Manager inviano alcuni dati, ad esempio gli avvisi di Operations Manager, valutazione della configurazione, spazio dell'istanza e server di gestione capacità data toohello. Altri volumi elevati di dati, ad esempio i log di IIS, prestazioni e gli eventi di protezione vengono inviati direttamente toohello OMS Gateway.  Se si dispone di uno o più server Gateway di Operations Manager distribuiti in una rete Perimetrale o altri toomonitor rete isolata sistemi non attendibili, Impossibile comunicare con un Gateway di OMS.  I server Gateway di gestione di operazioni è possibile solo server di gestione tooa report.  Quando un gruppo di gestione di Operations Manager è configurato toocommunicate con hello Gateway OMS, le informazioni di configurazione proxy hello vanno distribuito automaticamente tooevery computer gestito tramite agente che dati toocollect configurato per Log Analitica, anche se impostazione di Hello è vuota.    

tooprovide la disponibilità elevata per direttamente connessi o gruppi di gestione di operazioni che comunicano con OMS tramite il gateway di hello, è possibile utilizzare tooredirect di bilanciamento del carico di rete e distribuire il traffico hello tra più server gateway.  Se si arresta un server gateway, il traffico di hello è reindirizzato tooanother nodo disponibile.  

Si consiglia di installare l'agente OMS hello in computer hello hello toomonitor di software OMS Gateway hello Gateway OMS e analizzare i dati sulle prestazioni o l'evento. Inoltre, hello agente consente di hello OMS Gateway identificare hello endpoint di servizio che deve toocommunicate con.

Ogni agente deve disporre gateway tooits connettività di rete in modo che gli agenti possono trasferire automaticamente tooand dati dal gateway hello. L'installazione del gateway hello in un controller di dominio non è consigliata.

Hello seguente diagramma mostra il flusso di dati da tooOMS diretta degli agenti utilizzano server gateway hello.  Agenti devono essere loro corrispondenza configurazione proxy hello stesso hello porta OMS Gateway è configurato toocommunicate con tooOMS.  

![Diagramma della comunicazione degli agenti diretti con OMS](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Hello diagramma seguente illustra il flusso di dati da un tooOMS gruppo di gestione Operations Manager.   

![Diagramma della comunicazione di Operations Manager con OMS](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Prerequisiti

Durante la definizione di un hello toorun computer Gateway OMS, questo deve essere installato seguente hello:

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008
* .NET Framework 4.5
* Almeno un processore a 4 core e 8 GB di memoria

### <a name="language-availability"></a>Lingue disponibili

Hello OMS Gateway è disponibile nelle seguenti lingue hello:

- Cinese (semplificato)
- Cinese (tradizionale)
- Ceco
- Olandese
- Inglese
- Francese
- Tedesco
- Ungherese
- Italiano
- Giapponese
- Coreano
- Polacco
- Portoghese (Brasile)
- Portoghese (Portogallo)
- Russo
- Spagnolo (internazionale)

## <a name="download-hello-oms-gateway"></a>Scaricare hello OMS Gateway

Esistono tre modi tooget hello versione più recente del file di installazione del Gateway OMS hello.

1. Scaricare da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443).

2. Scaricare dal portale OMS hello.  Dopo l'accesso tooyour area di lavoro OMS, passare troppo**impostazioni** > **Connected Sources** > **server Windows** e fare clic su **Scaricare OMS Gateway**.

3. Scaricare da hello [portale di Azure](https://portal.azure.com).  Dopo avere effettuato l'accesso:  

   1. Sfoglia elenco hello dei servizi e quindi selezionare **Analitica Log**.  
   2. Selezionare un'area di lavoro.
   3. Nel pannello dell'area di lavoro, in **General** fare clic su **Avvio rapido**.
   4. In **scegliere un'area di lavoro toohello di tooconnect origine di dati**, fare clic su **computer**.
   5. In hello **agente diretto** pannello, fare clic su **scaricare Gateway OMS**.<br><br> ![Scaricare il gateway OMS](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Installare hello OMS Gateway

tooinstall un gateway, eseguire hello alla procedura seguente.  Se è installata una versione precedente, in precedenza denominato *server d'inoltro Analitica Log*, sarà aggiornato toothis versione.  

1. Dalla cartella di destinazione hello, fare doppio clic su **Gateway.msi OMS**.
2. In hello **iniziale** pagina, fare clic su **Avanti**.<br><br> ![Configurazione guidata gateway](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. In hello **contratto di licenza** selezionare **accetto i termini hello nel contratto di licenza hello** tooagree toohello contratto di licenza e quindi fare clic su **successivo**.
4. In hello **indirizzo e una porta proxy** pagina:
   1. Toobe numero di porta di tipo hello TCP usata per il gateway di hello. Viene configurata una regola in ingresso con questo numero di porta in Windows Firewall.  valore predefinito di Hello è 8080.
      intervallo valido di Hello del numero di porta hello è 1-65535. Se l'input hello non è compreso in questo intervallo, viene visualizzato un messaggio di errore.
   2. Facoltativamente, se hello server in cui il gateway hello installata toocommunicate esigenze tramite un proxy, digitare l'indirizzo del proxy hello in cui è necessario tooconnect hello gateway. ad esempio `http://myorgname.corp.contoso.com:80`.  Se vuoto, gateway hello tenterà tooconnect toohello Internet direttamente.  Se il server proxy richiede l'autenticazione, immettere un nome utente e una password.<br><br> ![Configurazione guidata del proxy del gateway](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. Fare clic su **Avanti**.
5. Se non si dispone di Microsoft Update è attivato, hello Microsoft Update verrà visualizzata la pagina in cui è possibile scegliere tooenable è. Effettuare una selezione e quindi fare clic su **Avanti**. In caso contrario, continuare toohello successivo.
6. In hello **cartella di destinazione** pagina lasciare hello predefinito c:\Programmi\Microsoft Files\OMS Gateway o un tipo hello percorso della cartella in cui si desidera tooinstall gateway e quindi fare clic su **Avanti**.
7. In hello **tooinstall pronto** pagina, fare clic su **installare**. Controllo dell'Account utente potrebbero essere visualizzati tooinstall dell'autorizzazione richiesta. In questo caso fare clic su **Sì**.
8. Al termine dell'installazione fare clic su **Fine**. È possibile verificare che il servizio hello in esecuzione, aprire lo snap-in Services. msc hello e verificare che **OMS Gateway** viene visualizzato nell'elenco di hello del servizi e lo stato è **esecuzione**.<br><br> ![Servizi – Gateway OMS](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Configurare il bilanciamento del carico di rete
È possibile configurare il gateway hello per la disponibilità elevata mediante Bilanciamento carico di rete (NLB) utilizzando Microsoft bilanciamento del carico (NLB, Network Load) o servizi di bilanciamento del carico basato su hardware.  Hello bilanciamento del carico gestisce il traffico reindirizzando hello richieste connessioni da hello gli agenti OMS o il server di gestione di Operations Manager tramite i relativi nodi. Se si arresta un server Gateway, il traffico hello Ottiene nodi tooother reindirizzato.

toolearn come toodesign e distribuire un cluster di bilanciamento carico di rete Windows Server 2016, vedere [bilanciamento carico di rete](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Hello passaggi seguenti descrivono le modalità di caricamento di cluster di bilanciamento del carico tooconfigure una rete di Microsoft.  

1.  Eseguire l'accesso a server di Windows hello che è un membro del cluster di bilanciamento carico di rete hello con un account amministrativo.  
2.  Aprire Gestione bilanciamento carico di rete in Server Manager, fare clic su **Strumenti** e quindi su **Gestione bilanciamento carico di rete**.
3. Fare doppio clic su indirizzo IP del cluster hello tooconnect un server Gateway di OMS con Microsoft Monitoring Agent installato, hello e quindi fare clic su **tooCluster Aggiungi Host**.<br><br> ![Gestione bilanciamento carico di rete: aggiunta di Host tooCluster](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Immettere l'indirizzo IP di hello del server gateway hello che si desidera tooconnect.<br><br> ![Gestione bilanciamento carico di rete: aggiunta di Host tooCluster: Connect](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>Configurare l'agente OMS e il gruppo di gestione di Operations Manager
Hello nella sezione seguente include i passaggi per la modalità tooconfigure connessi direttamente gli agenti OMS, un gruppo di gestione di Operations Manager o i Runbook worker ibridi di automazione di Azure con hello OMS Gateway toocommunicate con OMS.  

toounderstand requisiti e i passaggi per la modalità tooinstall hello agente OMS nei computer Windows direttamente connessione tooOMS, vedere [tooOMS computer Windows di connettersi](log-analytics-windows-agents.md) o per vedere i computer Linux [connettere i computer Linux tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>Configurazione dell'agente OMS hello e Operations Manager toouse hello Gateway OMS come un server proxy

### <a name="configure-standalone-oms-agent"></a>Configurare un agente OMS autonomo
Vedere [configurare le impostazioni proxy e firewall con Microsoft Monitoring Agent hello](log-analytics-proxy-firewall.md) per informazioni sulla configurazione di un toouse agente un server proxy, che in questo caso è hello gateway.  Se sono stati distribuiti più server gateway dietro un bilanciamento del carico di rete, configurazione del proxy dell'agente OMS hello è l'indirizzo IP virtuale hello di hello bilanciamento carico di rete:<br><br> ![Proprietà di Microsoft Monitoring Agent –Impostazioni proxy](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Configurare Operations Manager - tutti gli agenti utilizzano hello nello stesso server proxy
Configurare i server gateway di Operations Manager tooadd hello.  Hello Operations Manager, configurazione del proxy viene automaticamente applicato agenti tooall reporting tooOperations Manager, anche se l'impostazione di hello è vuota.

toouse hello Gateway toosupport Operations Manager, è necessario quanto segue:

* Microsoft Monitoring Agent (versione dell'agente: **8.0.10900.0** e versioni successive) installato nel server Gateway hello e configurato per aree di lavoro OMS hello con cui si desidera toocommunicate.
* gateway di Hello deve disporre della connettività Internet o da server proxy tooa connesso che esegue.

> [!NOTE]
> Se non si specifica un valore per il gateway hello, valori vuoti vengono inseriti gli agenti tooall.


1. Console di Operations Manager aprire hello e in **Operations Management Suite**, fare clic su **connessione** e quindi fare clic su **Configure Proxy Server**.<br><br> ![Operations Manager – Configurare il server proxy](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Selezionare **utilizzare hello di tooaccess un server proxy Operations Management Suite** e quindi digitare indirizzo hello del server Gateway OMS hello o un indirizzo IP virtuale di hello bilanciamento carico di rete. Assicurarsi di avviare con hello `http://` prefisso.<br><br> ![Operations Manager – Indirizzo del server proxy](./media/log-analytics-oms-gateway/scom02.png)<br>
3. Fare clic su **Finish**. Il server di Operations Manager è l'area di lavoro OMS tooyour connesso.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Configurare Operations Manager: agenti specifici usano il server proxy
Per gli ambienti di grandi dimensioni o complessi, è consigliabile solo specifici server (o gruppi) toouse hello server Gateway di OMS.  Per questi server, è possibile aggiornare hello agente direttamente come questo valore viene sovrascritto dal valore globale di hello hello gruppo di gestione di Operations Manager.  È invece necessario toooverride hello regola utilizzata toopush questi valori.

> [!NOTE]
> Questa stessa tecnica di configurazione può essere utilizzato tooallow hello di più server Gateway OMS nell'ambiente in uso.  Ad esempio, si debba specifico toobe di server Gateway OMS specificata in base a ogni area.

1. Console di Operations Manager aprire hello e seleziona hello **Authoring** dell'area di lavoro.  
2. Nell'area di lavoro creazione e modifica hello selezionare **regole** e fare clic su hello **ambito** sulla barra degli strumenti di Operations Manager hello. Se questo pulsante non è disponibile, verificare di avere selezionato un oggetto, non una cartella nel riquadro monitoraggio hello toomake. Hello **ambito oggetti Management Pack** la finestra di dialogo Visualizza un elenco di oggetti, gruppi o le classi di destinazione comuni.
3. Tipo **servizio integrità** in hello **cercare** campo, selezionarlo dall'elenco di hello.  Fare clic su **OK**.  
4. Cercare la regola hello **regola impostazione Proxy di Advisor** hello Operations console dalla barra degli strumenti fare clic su **esegue l'override** e quindi troppo**Override hello Rule\For un oggetto specifico della classe: integrità Servizio** e selezionare un oggetto specifico dall'elenco di hello.  Facoltativamente, è possibile creare un gruppo personalizzato contenente l'oggetto servizio di integrità hello del server hello desidera tooapply tooand questo override quindi applicare hello override toothat gruppo.
5. In hello **proprietà di sostituzione** finestra di dialogo fare clic su un segno di spunta in hello tooplace **Override** colonna successiva toohello **WebProxyAddress** parametro.  In hello **valore di sostituzione** immettere l'URL di hello hello OMS Gateway server garantire che si avvia con hello `http://` prefisso.
   >[!NOTE]
   > Regola di hello tooenable non è necessario perché è già gestito automaticamente con un override contenuto in hello Microsoft System Center Advisor Secure Reference Override management pack per Microsoft System Center Advisor Monitoring Server Group hello.
   >
6. Selezionare un management pack hello **selezionare management pack di destinazione** elenco o creare un nuovo management pack non bloccato facendo **New**.
7. Dopo avere completato le modifiche, fare clic su **OK**.

### <a name="configure-for-automation-hybrid-workers"></a>Configurare per i ruoli di lavoro ibridi di automazione
Se si dispone di Runbook worker ibridi automazione nell'ambiente in uso, hello alla procedura seguente fornisce soluzioni alternative manuale, temporaneo tooconfigure hello Gateway toosupport li.

In hello alla procedura seguente, è necessario tooknow hello area in cui si trova hello account di automazione di Azure. percorso di hello toolocate:

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare il servizio di automazione di Azure hello.
3. Selezionare l'account di automazione di Azure appropriato hello.
4. Visualizzarne l'area in **Località**.<br><br> ![Portale di Azure – Località dell'account di Automazione](./media/log-analytics-oms-gateway/location.png)  

Utilizzare hello tabelle tooidentify hello URL per ogni percorso seguente:

**URL del servizio dati del processo di runtime**

| **Località** | **URL** |
| --- | --- |
| Stati Uniti centro-settentrionali |ncus-jobruntimedata-prod-su1.azure-automation.net |
| Europa occidentale |we-jobruntimedata-prod-su1.azure-automation.net |
| Stati Uniti centro-meridionali |scus-jobruntimedata-prod-su1.azure-automation.net |
| Stati Uniti orientali 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Canada centrale |cc-jobruntimedata-prod-su1.azure-automation.net |
| Europa settentrionale |ne-jobruntimedata-prod-su1.azure-automation.net |
| Asia sudorientale |sea-jobruntimedata-prod-su1.azure-automation.net |
| India centrale |cid-jobruntimedata-prod-su1.azure-automation.net |
| Giappone |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australia |ase-jobruntimedata-prod-su1.azure-automation.net |

**URL del servizio agente**

| **Località** | **URL** |
| --- | --- |
| Stati Uniti centro-settentrionali |ncus-agentservice-prod-1.azure-automation.net |
| Europa occidentale |we-agentservice-prod-1.azure-automation.net |
| Stati Uniti centro-meridionali |scus-agentservice-prod-1.azure-automation.net |
| Stati Uniti orientali 2 |eus2-agentservice-prod-1.azure-automation.net |
| Canada centrale |cc-agentservice-prod-1.azure-automation.net |
| Europa settentrionale |ne-agentservice-prod-1.azure-automation.net |
| Asia sudorientale |sea-agentservice-prod-1.azure-automation.net |
| India centrale |cid-agentservice-prod-1.azure-automation.net |
| Giappone |jpe-agentservice-prod-1.azure-automation.net |
| Australia |ase-agentservice-prod-1.azure-automation.net |

Se il computer è registrato come un Runbook Worker ibrido automaticamente per l'applicazione di patch utilizzando una soluzione di gestione degli aggiornamenti di hello, seguire questi passaggi:

1. Aggiungere elenco di dati di Runtime del processo servizio URL toohello Host consentito hello hello OMS Gateway. Ad esempio: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Riavviare il servizio di OMS Gateway hello utilizzando hello cmdlet di PowerShell seguente:`Restart-Service OMSGatewayService`

Se il computer in boarded tooAzure automazione mediante i cmdlet di registrazione di Runbook Worker ibrido hello, seguire questi passaggi:

1. Aggiungere hello OMS Gateway hello agente del servizio registrazione URL toohello consentito elenco Host. Ad esempio: `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Aggiungere elenco di dati di Runtime del processo servizio URL toohello Host consentito hello hello OMS Gateway. Ad esempio: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Riavviare il servizio di OMS Gateway hello.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Cmdlet PowerShell utili
I cmdlet consentono di completare le attività che sono le impostazioni di configurazione del Gateway di tooupdate necessari hello OMS. Prima di usarli, assicurarsi di:

1. Installare hello OMS Gateway (con estensione MSI).
2. Aprire una finestra della console di PowerShell.
3. modulo hello tooimport, digitare il comando seguente:`Import-Module OMSGateway`
4. Se si è verificato alcun errore nel passaggio precedente hello, è stato importato il modulo hello e hello cmdlet possono essere utilizzati. Digitare `Get-Module OMSGateway`.
5. Dopo aver apportato le modifiche utilizzando i cmdlet di hello, assicurarsi che si riavvia il servizio Gateway hello.

Se si verifica un errore nel passaggio 3, non è stato importato il modulo di hello. Errore Hello potrebbe verificarsi quando PowerShell è il modulo di hello toofind non è possibile. È possibile trovarlo nel percorso di installazione del Gateway hello: *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Cmdlet** | **Parametri** | **Descrizione** | **Esempio** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Chiave |Ottiene la configurazione di hello del servizio hello |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Chiave (obbligatorio) <br> Valore |Configurazione del servizio hello di hello modifiche |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Ottiene l'indirizzo di hello del proxy di inoltro (padre) |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Indirizzo<br> Nome utente<br> Password |Imposta hello indirizzo (e credenziali) del proxy di inoltro (padre) |1. Impostare un proxy di inoltro e le credenziali:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Impostare un proxy di inoltro che non richiede autenticazione: `Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. L'impostazione proxy di inoltro crittografato hello:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |Ottiene hello è attualmente consentito host (solo hello host consentiti configurati localmente, non include host consentiti scaricato automaticamente) |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Host (obbligatorio) |Aggiunge hello host toohello elenco consentito |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Host (obbligatorio) |Rimuove host hello hello elenco consentito |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Oggetto (obbligatorio) |Aggiunge l'oggetto certificato di hello client toohello elenco consentito |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Oggetto (obbligatorio) |Rimuove soggetto del certificato client hello hello elenco consentito |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Ottiene hello è attualmente consentito il client soggetti certificato (solo localmente hello configurata consentiti argomenti, non includere automaticamente scaricati consentiti argomenti) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Risoluzione dei problemi
toocollect gli eventi registrati dal gateway hello, è necessario tooalso è installato l'agente OMS hello.<br><br> ![Visualizzatore eventi – Log del gateway OMS](./media/log-analytics-oms-gateway/event-viewer.png)

**ID e descrizioni dell'evento del gateway OMS**

Hello nella tabella seguente hello ID evento e le descrizioni per gli eventi di Log di OMS Gateway.

| **ID** | **Descrizione** |
| --- | --- |
| 400 |Qualsiasi errore dell'applicazione che non dispone di un ID specifico |
| 401 |Configurazione errata. Ad esempio: listenPort = "text" anziché un intero |
| 402 |Eccezione durante l'analisi dei messaggi di handshake TLS |
| 403 |Errore di rete. Ad esempio: Impossibile connettersi a server tootarget |
| 100 |Informazioni generali |
| 101 |Servizio avviato |
| 102 |Servizio arrestato |
| 103 |Ricevuto un comando HTTP CONNECT dal client |
| 104 |Non è stato ricevuto un comando HTTP CONNECT |
| 105 |Server di destinazione non è presente nell'elenco consentito o porta di destinazione hello non è una porta sicura (443) <br> <br> Verificare che l'agente di MMA hello sul server Gateway e agenti di hello comunicando hello Gateway sono connesso toohello stessa area di lavoro Log Analitica. |
| 105 |ERRORE TcpConnection – Certificato client non valido: CN=Gateway <br><br> Assicurarsi che: <br>    <br> &#149; Si usi un gateway con il numero di versione 1.0.395.0 o successiva. <br> &#149; Hello MMA agente nel server Gateway e agenti hello comunicando hello Gateway siano connesso toohello stessa area di lavoro Log Analitica. |
| 106 |Un motivo qualsiasi sessione TLS hello è sospetto e rifiutati |
| 107 |sessione TLS Hello è stata verificata. |

**Toocollect i contatori delle prestazioni**

Hello nella tabella seguente mostra hello contatori delle prestazioni disponibili per hello OMS Gateway. È possibile aggiungere contatori di hello utilizzando Performance Monitor.

| **Nome** | **Descrizione** |
| --- | --- |
| Gateway OMS/Connessione client attiva |Numero di connessioni di rete client attive (TCP) |
| Gateway OMS/Numero di errori |Numero di errori |
| Gateway OMS/Client connesso |Numero di client connessi |
| Gateway OMS/Numero di rifiuti |Numero di rifiuti a causa di errore di convalida tooany TLS |

![Contatori delle prestazioni del gateway OMS](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>Ottenere supporto
Quando si è connesso toohello portale di Azure, è possibile creare una richiesta di assistenza con hello Gateway OMS o qualsiasi altro servizio di Azure o funzionalità di un servizio.
toorequest assistenza, fare clic sul simbolo di punto interrogativo hello in hello alto a destra del portale hello e quindi fare clic su **nuova richiesta di assistenza**. Completare quindi il nuovo modulo di richiesta il supporto di hello.

![Nuova richiesta di supporto](./media/log-analytics-oms-gateway/support.png)

È anche possibile lasciare commenti e suggerimenti su OMS o Log Analitica in hello [forum sul feedback su Microsoft Azure](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere le origini dati](log-analytics-data-sources.md) dati toocollect hello Connected Sources nell'area di lavoro OMS e archiviarlo nel repository OMS hello.

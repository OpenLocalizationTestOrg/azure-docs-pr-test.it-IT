---
title: gateway di dati locale aaaInstall - App Azure per la logica | Documenti Microsoft
description: Prima di accedere a origini dati in locale, installare il gateway di dati hello locale per il trasferimento dei dati rapido e la crittografia tra origini dati in locale e la logica App
keywords: accesso ai dati, locale, trasferimento dei dati, crittografia, origini dei dati
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Installare il gateway dati locale di hello per le app di logica di Azure

Prima di App per la logica può accedere a origini dati in locale, è necessario installare e configurare gateway dati locale di hello. gateway Hello funge da ponte che fornisce il trasferimento dei dati rapido e la crittografia tra i sistemi locali e le app di logica. gateway Hello inoltra i dati da origini locali sui canali crittografati tramite hello Azure Service Bus. Tutto il traffico viene generato come proteggere il traffico in uscita dall'agente gateway hello. Altre informazioni, vedere [funzionamento gateway dati hello](#gateway-cloud-service).

gateway Hello supporta le connessioni delle origini dati toothese in locale:

*   BizTalk Server 2016
*   DB2  
*   File system
*   Informix
*   MQ
*   MySQL
*   Oracle Database
*   PostgreSQL
*   Server applicazioni SAP 
*   Server messaggi SAP
*   SharePoint
*   SQL Server
*   Teradata

Questi passaggi mostrano come toofirst installazione hello sul gateway dati locale prima di [impostare una connessione tra gateway hello e App per la logica](./logic-apps-gateway-connection.md). Per altre informazioni sui connettori supportati, vedere [Connettori per le app per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list). 

Per informazioni su come toouse hello gateway con altri servizi, vedere i seguenti articoli:

*   [Gateway dati locale di Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Gateway dati locale di Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Gateway dati locale di Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Gateway dati locale di Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>Requisiti

**Minimo**:

* .NET Framework 4.5
* Windows 7 versione a 64 bit o Windows Server 2008 R2 (o versione successiva)

**Consigliato**:

* 8 CPU core
* 8 GB di memoria
* Windows 2012 R2 versione a 64 bit (o versione successiva)

**Considerazioni importanti**:

* Installare il gateway di dati locale hello solo in un computer locale.
È possibile installare il gateway hello in un controller di dominio.

   > [!TIP]
   > Non si dispone di gateway hello tooinstall sul hello nello stesso computer dell'origine dati. latenza toominimize, è possibile installare gateway hello più vicino come origine di dati possibili tooyour, o su hello stesso computer, presupponendo che si disponga di autorizzazioni.

* Non installare il gateway hello in un computer che consente di disattivare, passa alla toosleep o non connettersi toohello Internet perché non è possibile eseguire il gateway hello in tali circostanze. Le prestazioni del gateway possono anche diminuire su una rete wireless.

* Durante l'installazione, è necessario accedere con un [account aziendale o dell'istituto di istruzione](https://docs.microsoft.com/azure/active-directory/sign-up-organization) gestito da Azure Active Directory (Azure AD), non con un account Microsoft. 

  Si dispone di toouse hello stesso lavoro o scuola account in un secondo momento in hello Azure portal quando si crea e associa una risorsa di gateway con l'installazione di gateway. È quindi possibile selezionare la risorsa del gateway quando si crea la connessione hello tra la logica app e hello in origine dati locale. [Perché è necessario usare un account di Azure AD aziendale o dell'istituto di istruzione?](#why-azure-work-school-account)

  > [!TIP]
  > Se si è effettuata l'iscrizione a un'offerta di Office 365 senza fornire l'indirizzo di posta elettronica aziendale effettivo, l'indirizzo di accesso sarà simile a jeff@contoso.onmicrosoft.com. 

* Se si dispone di un gateway esistente impostato con un programma di installazione è precedente alla versione 14.16.6317.4, è possibile modificare la posizione del gateway dal programma di installazione più recente hello in esecuzione. Tuttavia, è possibile utilizzare hello tooset di programma di installazione più recente di un nuovo gateway con percorso hello che si desidera invece.
  
  Se si dispone di un programma di installazione di gateway è precedente alla versione 14.16.6317.4, ma non è stato installato il gateway, è possibile scaricare e usare hello programma di installazione più recente.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Installare il gateway dati hello

1.  [Scaricare ed eseguire il programma di installazione di hello gateway in un computer locale](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).

2. Leggere e accettare i termini di hello di utilizzo e informativa sulla privacy.

3. Specificare il percorso di hello sul computer locale in cui si desidera gateway hello tooinstall.

4. Quando richiesto, accedere con il proprio account aziendale o dell'istituzione di istruzione di Azure, non con un account Microsoft.

   ![Accedere con l'account aziendale o dell'istituto di istruzione di Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. Registrare il gateway installato presso hello [servizio cloud gateway](#gateway-cloud-service). Scegliere l'opzione che **consente di registrare un nuovo gateway in questo computer**.

   il servizio cloud gateway Hello crittografa e archivia le credenziali dell'origine dati e i dettagli del gateway. 
   servizio Hello indirizza anche le query e i relativi risultati tra le app per la logica, gateway dati locale di hello e l'origine dati in locale.

6. Specificare un nome per l'installazione del gateway. Creare una chiave di ripristino, quindi confermarla. 

   > [!IMPORTANT] 
   > La chiave di ripristino deve contenere almeno otto caratteri. Assicurarsi di salvare e conservare la chiave di hello in un luogo sicuro. Questa chiave è necessaria inoltre quando si desidera toomigrate, ripristinare o acquisire la proprietà di un gateway esistente.

   1. area di toochange hello predefinita per il servizio cloud gateway hello e Bus di servizio di Azure utilizzati dall'installazione del gateway, scegliere **area Modifica**.

      ![Cambiare area](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      area predefinita Hello è area hello associata al tenant di Azure AD.

   2. Nel riquadro successivo di hello, aprire hello **selezionare area** troppo scegliere un'area diversa.

      ![Selezionare un'altra area](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      Ad esempio, si potrebbe selezionare hello app logica stessa area o hello selezionare area più vicina tooyour locale dati di origine in modo da ridurre la latenza. Le risorse gateway e l'app per la logica possono avere posizioni diverse.

      > [!IMPORTANT]
      > Dopo l'installazione non è possibile modificare questa area. Determina inoltre quest'area e limita percorso hello in cui è possibile creare hello risorse di Azure per il gateway. Pertanto, quando si crea la risorsa del gateway in Azure, verificare che percorso della risorsa hello corrisponda area hello selezionata durante l'installazione del gateway.
      > 
      > Se si desidera toouse un'area diversa per il gateway in un secondo momento, è necessario impostare di un nuovo gateway.

   3. Al termine, scegliere **Fine**.

7. Ora in cui è possibile, seguire la procedura hello Azure portal [creare una risorsa di Azure per il gateway](../logic-apps/logic-apps-gateway-connection.md). 

Altre informazioni, vedere [funzionamento gateway dati hello](#gateway-cloud-service).

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>Eseguire la migrazione, ripristinare o sostituire un gateway esistente

tooperform queste attività, è necessario disporre di chiave di ripristino hello che è stato specificato durante l'installazione di gateway hello.

1. Dal menu di avvio del computer, scegliere **Gateway dati locale**.

2. Dopo hello apre programma di installazione, eseguire l'accesso con hello stesso Azure di lavoro o scuola account precedentemente utilizzato gateway hello tooinstall.

3. Scegliere **Eseguire la migrazione, ripristinare o acquisire la proprietà di un gateway esistente**.

4. Specificare la chiave di ripristino e nome hello per gateway hello che si desidera eseguire, il ripristino o toomigrate sulla.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Riavviare il gateway hello

gateway di Hello viene eseguito come servizio Windows. Come qualsiasi altro servizio di Windows, è possibile avviare e arrestare il servizio di hello in diversi modi. Ad esempio, puoi aprire un prompt dei comandi con autorizzazioni elevate in hello computer in cui è in esecuzione gateway hello ed eseguire entrambi questi comandi:

* servizio hello toostop, eseguire questo comando:
  
    `net stop PBIEgwService`

* servizio hello toostart, eseguire questo comando:
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Account del servizio Windows

gateway dati locale di Hello impostato toouse `NT SERVICE\PBIEgwService` per Windows hello le credenziali di accesso del servizio. Per impostazione predefinita, il gateway hello ha diritto "Accesso come servizio" hello per macchina hello in cui si installa il gateway hello.

> [!NOTE]
> Hello account del servizio Windows diverso dall'account hello utilizzato per la connessione a origini dati locali tooon e dal hello Azure lavoro o l'account dell'istituto di istruzione usato toosign in toocloud servizi.

## <a name="configure-a-firewall-or-proxy"></a>Configurare un firewall o proxy

gateway Hello crea una connessione in uscita troppo [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). informazioni sul proxy tooprovide per il gateway, vedere [configurare le impostazioni proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).

toocheck se il firewall o proxy, potrebbe bloccare le connessioni, verificare se il computer può connettersi effettivamente toohello internet e hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). Da un prompt di PowerShell eseguire questo comando:

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> Questo comando verifica solo la connettività di rete e connettività toohello Azure Service Bus. Pertanto il comando hello non vengono eseguite toodo con gateway hello o un servizio cloud gateway di hello che crittografa e archivia le credenziali e i dettagli del gateway. 
>
> Questo comando è disponibile solo in Windows Server 2012 R2 o in una versione successiva e in Windows 8.1 o in una versione successiva. Nelle versioni precedenti del sistema operativo, è possibile utilizzare Telnet troppo testare la connettività. Altre informazioni su [bus di servizio di Azure e soluzioni ibride](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

I risultati dovrebbero essere simili toothis esempio:

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

Se **TcpTestSucceeded** non è stato impostato troppo**True**, potrebbe essere bloccato da un firewall. Se si desidera toobe completa, sostituire hello **ComputerName** e **porta** sotto i valori con valori di hello [configurare porte](#configure-ports) in questo argomento.

firewall Hello anche potrebbe bloccare le connessioni che hello che Azure Service Bus rende toohello Data Center di Azure. Se si verifica questo scenario, approvare (sbloccare) tutti gli indirizzi IP per i Data Center nell'area di hello. Per tali indirizzi IP, [get hello Azure elenco di indirizzi IP qui](https://www.microsoft.com/download/details.aspx?id=41653).

## <a name="configure-ports"></a>Configurare le porte

gateway Hello crea una connessione in uscita troppo[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) e comunica su porte in uscita: TCP 443 (predefinita), 5671, 5672, 9350 a 9354. gateway Hello non richiede porte in ingresso. Altre informazioni su [bus di servizio di Azure e soluzioni ibride](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

| NOMI DI DOMINIO | PORTE IN USCITA | Descrizione |
| --- | --- | --- |
| *. analysis.windows.net | 443 | HTTPS | 
| *.login.windows.net | 443 | HTTPS | 
| *.servicebus.windows.net | 5671-5672 | Advanced Message Queuing Protocol (AMQP) | 
| *.servicebus.windows.net | 443, 9350-9354 | Listener in Inoltro del Bus di servizio su TCP (richiede 443 per l'acquisizione del token di Controllo di accesso) | 
| *.frontend.clouddatahub.net | 443 | HTTPS | 
| *.core.windows.net | 443 | HTTPS | 
| login.microsoftonline.com | 443 | HTTPS | 
| *.msftncsi.com | 443 | Connettività internet tootest utilizzato hello gateway non è raggiungibile dal servizio Power BI hello. | 

Se si dispone di indirizzi IP tooapprove anziché domini hello, è possibile scaricare e utilizzare hello [elenco di intervalli IP dei data center Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). In alcuni casi, hello Azure Service Bus delle connessioni con indirizzo IP anziché nomi di dominio completo.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Come funziona il gateway dati hello?

gateway dati Hello facilita la comunicazione rapida e sicura tra l'app per la logica, il servizio cloud gateway hello e l'origine dati locale. 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

Pertanto, quando utente hello nel cloud hello interagisce con un elemento che è connesso tooyour locale origine dati:

1. servizio cloud gateway di Hello crea una query, insieme alle credenziali crittografato hello per l'origine di dati, hello e invia hello query toohello coda tooprocess gateway hello.

2. il servizio cloud gateway Hello analizza query hello e inserisce toohello richiesta hello Azure Service Bus.

3. gateway dati locale di Hello esegue il polling hello Azure Service Bus per le richieste in sospeso.

4. gateway Hello Ottiene hello query, decrittografa le credenziali di hello e collega l'origine dati toohello con tali credenziali.

5. gateway Hello invia hello query toohello origine per l'esecuzione.

6. risultati di Hello vengono inviati dall'origine dati hello, toohello indietro gateway e il servizio cloud gateway toohello. Hello servizio cloud gateway Usa quindi i risultati di hello.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="general"></a>Generale

**Domande e**: è necessario un gateway per le origini dati nel cloud hello, ad esempio SQL Azure? <br/>
**R**: No. Un gateway si connette a origini dati locali tooon solo.

**Domande e**: gateway hello dispone toobe installato hello stesso computer come origine dati hello? <br/>
**R**: No. gateway Hello stabilisce la connessione origine dati toohello utilizzando le informazioni di connessione hello fornito. Prendere in considerazione gateway hello come un'applicazione client in questo senso. gateway Hello sufficiente hello funzionalità tooconnect toohello nome del server che è stato specificato.

<a name="why-azure-work-school-account"></a>

**Domande e**: perché devo non è un lavoro di Azure o dell'istituto di istruzione toosign account in? <br/>
**Oggetto**: È possibile utilizzare un lavoro di Azure o scuola account quando si installa gateway dati locale di hello. L'account di accesso viene archiviato in un tenant gestito da Azure Active Directory (Azure AD). Nome dell'entità utente dell'account di Azure AD (UPN) corrisponde in genere, indirizzo di posta elettronica hello.

**D**: Dove sono archiviate le credenziali? <br/>
**Oggetto**: credenziali hello immesse per un'origine dati vengono crittografate e archiviate nel servizio cloud gateway di hello. le credenziali di Hello vengono decrittografate nel gateway dati locale di hello.

**D**: Sono previsti requisiti per la larghezza di banda della rete? <br/>
**R**: È consigliabile che la connessione di rete abbia una buona velocità effettiva. Ogni ambiente è diverso e quantità hello di invio di dati influisce sui risultati di hello. Uso di ExpressRoute può contribuire a tooguarantee un livello di velocità effettiva tra sedi locali e hello Data Center di Azure.
È possibile utilizzare hello dello strumento di terze parti Azure Speed Test app toohelp misuratore la velocità effettiva.

**Domande e**: che cos'è la latenza di hello per le query tooa dati di origine in esecuzione dal gateway hello? Che cos'è l'architettura migliore hello? <br/>
**Oggetto**: tooreduce latenza di rete, installare hello gateway come origine dati toohello Chiudi possibili. Se è possibile installare il gateway di hello sull'origine dati effettivi hello, la prossimità riduce la latenza di hello introdotta. Prendere in considerazione i Data Center hello troppo. Ad esempio, se il servizio utilizza hello Data Center di Stati Uniti occidentali e SQL Server è ospitato in una macchina virtuale di Azure, la macchina virtuale di Azure deve essere in Stati Uniti occidentali hello troppo. Questo prossimità riduce la latenza ed evitare addebiti in uscita sulla macchina virtuale di Azure hello.

**Domande e**: come vengono inviati risultati toohello indietro cloud? <br/>
**Oggetto**: risultati vengono inviati tramite hello Azure Service Bus.

**Domande e**: sono presenti eventuali gateway toohello le connessioni in ingresso dal cloud hello? <br/>
**R**: No. gateway di Hello Usa le connessioni in uscita tooAzure Bus di servizio.

**D**: Cosa accade se si bloccano le connessioni in uscita? Cosa devo tooopen? <br/>
**Oggetto**: Vedere porte hello e gli host che hello Usa gateway.

**Domande e**: ciò che viene chiamato il servizio Windows effettivo di hello?<br/>
**Oggetto**: In servizi, il gateway di hello è chiamato servizio Power BI Enterprise Gateway.

**Domande e**: possibile hello servizio gateway di Windows eseguito con un account Azure Active Directory? <br/>
**R**: No. servizio Windows Hello deve avere un account Windows valido. Per impostazione predefinita, il servizio di hello viene eseguito con hello SID del servizio, NT SERVICE\PBIEgwService.

### <a name="high-availability-and-disaster-recovery"></a>Disponibilità elevata e ripristino di emergenza

**D**: Quali opzioni sono disponibili per il ripristino di emergenza? <br/>
**Oggetto**: È possibile utilizzare toorestore chiave di ripristino hello o spostare un gateway. Quando si installa il gateway di hello, specificare la chiave di ripristino hello.

**Domande e**: che cos'è il vantaggio di hello della chiave di ripristino hello? <br/>
**Oggetto**: chiave di ripristino hello fornisce un modo toomigrate o ripristinare le impostazioni del gateway dopo un'emergenza.

**Domande e**: sono disponibili piani per l'abilitazione di scenari a disponibilità elevata con gateway hello? <br/>
**Oggetto**: questi scenari sono roadmap hello, ma è ancora non dispone di una sequenza temporale.

## <a name="troubleshooting"></a>Risoluzione dei problemi

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**Domande e**: come è possibile vedere quali sono le query vengono inviate toohello origine di dati locale? <br/>
**Oggetto**: È possibile abilitare la traccia di query, che include le query hello che vengono inviate. Tenere presente che query toochange risalendo toohello valore originale al termine della risoluzione dei problemi. Se il tracciamento delle query non viene disabilitato, si creeranno dei log più grandi.

È anche possibile usare gli strumenti per il tracciamento delle query di cui è dotata l'origine dati. Ad esempio, è possibile usare Eventi estesi o SQL Profiler per SQL Server e Analysis Services.

**Domande e**: dove sono i registri di gateway hello? <br/>
**R**: Vedere la sezione Strumenti più avanti in questo argomento.

### <a name="update-toohello-latest-version"></a>Aggiornare la versione più recente di toohello

Molti problemi possono verificarsi quando la versione di gateway hello diventa obsoleta. Come buona pratica, assicurarsi di utilizzare la versione più recente di hello. Se è stato aggiornato gateway hello per un mese o più, si potrebbe si consiglia di installare una versione più recente di hello del gateway hello e verificare se è possibile riprodurre il problema di hello.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Errore: Impossibile tooadd utente toogroup. (Utenti log delle prestazioni -2147463168 PBIEgwService)

È possibile che venga visualizzato questo errore se si tenta di gateway di hello tooinstall in un controller di dominio che non è supportato. Assicurarsi di distribuire gateway hello in un computer che non è un controller di dominio.

## <a name="tools"></a>Strumenti

### <a name="collect-logs-from-hello-gateway-configurer"></a>Raccogliere registri da configurer gateway hello

È possibile raccogliere i log per il gateway hello. Iniziare sempre con i registri di hello!

#### <a name="installer-logs"></a>Log dei programmi di installazione

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>Log di configurazione

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>Log del servizio gateway Enterprise

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>Log eventi

È possibile trovare il Gateway di gestione di dati e PowerBIGateway registri in hello **registri applicazioni e servizi**.

### <a name="fiddler-trace"></a>Fiddler Trace

[Fiddler](http://www.telerik.com/fiddler) è uno strumento gratuito di Telerik che consente di monitorare il traffico HTTP. È possibile visualizzare il traffico con il servizio Power BI da computer client hello hello. Questo servizio consente di visualizzare errori e altre informazioni correlate.

## <a name="next-steps"></a>Passaggi successivi
    
* [Connessione dati tooon locale da App per la logica](../logic-apps/logic-apps-gateway-connection.md)
* [Funzionalità di Enterprise Integration](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Connettori per App per la logica di Azure](../connectors/apis-list.md)

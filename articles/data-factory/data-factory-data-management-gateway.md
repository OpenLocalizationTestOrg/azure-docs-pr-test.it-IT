---
title: Gateway di gestione per Data Factory aaaData | Documenti Microsoft
description: Impostare un data gateway toomove di dati tra sedi locali e hello cloud. Usare Gateway di gestione dati in Azure Data Factory toomove i dati.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Gateway di gestione dati
gateway di gestione dati Hello è un agente client che è necessario installare nei dati on-premise ambiente toocopy tra archivi dati locali e cloud. Hello dati locali supportati da Data Factory di archivi sono disponibili in hello [origini dati supportate](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sezione.

In questo articolo si integra con questa procedura dettagliata hello in hello [spostare i dati tra sedi locali e cloud archivi dati](data-factory-move-data-between-onprem-and-cloud.md) articolo. In questa procedura dettagliata hello, creare una pipeline che utilizza hello gateway toomove dati da un tooan di database di SQL Server on-premise blob di Azure. Questo articolo fornisce informazioni dettagliate sul gateway di gestione dati hello. 

È possibile scalare orizzontalmente un gateway di gestione di dati mediante l'associazione di più computer locali con gateway hello. È possibile aumentare le prestazioni aumentando il numero di processi di spostamento di dati eseguibili contemporaneamente in un nodo. Questa funzionalità è disponibile anche per un gateway logico con un singolo nodo. Per informazioni dettagliate, vedere l'articolo [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) (Gateway di gestione dati - Disponibilità elevata e scalabilità (anteprima).

> [!NOTE]
> Gateway supporta attualmente solo attività di copia hello e attività di stored procedure in Data Factory. Non è il gateway hello toouse possibili origini dati locali di tooaccess un'attività personalizzata.      

## <a name="overview"></a>Panoramica
### <a name="capabilities-of-data-management-gateway"></a>Funzionalità del gateway di gestione dati
Gateway di gestione dati fornisce hello seguenti funzionalità:

* Modello le origini dati e origini dati cloud interno hello stessa data factory e spostano i dati.
* Disporre di un unico riquadro per il monitoraggio e gestione con visibilità lo stato del gateway dalla pagina di hello Data Factory.
* Gestire origini dati di accesso tooon locali in modo sicuro.
  * Firewall toocorporate è necessaria alcuna modifica. Gateway consente solo le connessioni basate su HTTP in uscita tooopen internet.
  * È possibile crittografare le informazioni sulle credenziali per gli archivi dati locali usando il proprio certificato.
* Spostare i dati in modo efficiente, i dati vengono trasferiti in parallelo, resilienti toointermittent problemi di rete con la logica di ripetizione automatica.

### <a name="command-flow-and-data-flow"></a>Flusso dei comandi e flusso di dati
Quando si usa un copia attività toocopy di dati tra sedi locali e cloud, attività hello Usa un gateway tootransfer di dati da toocloud di origine dati locale e viceversa.

Ecco il flusso di dati di alto livello hello per e un riepilogo dei passaggi per la copia con gateway dati: ![flusso di dati utilizzando gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Sviluppatori di dati crea un gateway per una Data Factory di Azure utilizzando entrambi hello [portale di Azure](https://portal.azure.com) o [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).
2. Sviluppatori di dati consente di creare un servizio collegato per un archivio dati locale specificando gateway hello. Come servizio collegato da parte dell'impostazione hello, sviluppatori di dati utilizzano le credenziali e i tipi di autenticazione toospecify applicazione hello impostazione delle credenziali.  finestra di dialogo applicazione comunica con i dati di hello Hello impostare credenziali archiviate tootest credenziali toosave gateway hello e di connessione.
3. Gateway crittografa le credenziali di hello con hello certificato associata gateway hello (fornito dallo sviluppatore di dati), prima di salvare le credenziali di hello in cloud hello.
4. Servizio Data Factory comunica con il gateway hello per la pianificazione e gestione dei processi tramite un canale di controllo che utilizza una coda del bus di servizio condiviso di Azure. Quando un processo di attività di copia deve toobe avviata, in Data Factory coda richiesta hello insieme a informazioni sulle credenziali. Gateway verrà avviato il processo di hello dopo il polling della coda di hello.
5. gateway Hello decrittografa le credenziali di hello con hello stesso certificato e quindi si connette toohello archivio di dati locale con le credenziali e il tipo di autenticazione appropriato.
6. gateway Hello copia dati da un archivio di cloud tooa archivio locale o, viceversa, a seconda della configurazione in pipeline di dati hello hello attività di copia. Per questo passaggio, gateway hello comunica direttamente con i servizi di archiviazione basata su cloud, ad esempio l'archiviazione Blob di Azure tramite un canale di sicuro (HTTPS).

### <a name="considerations-for-using-gateway"></a>Considerazioni sull'uso del gateway
* Una singola istanza del gateway di gestione dati può essere usata per più origini dati locali. Tuttavia, **una singola istanza del gateway è abbinato tooonly una data factory di Azure** e non può essere condivisa con data factory di un altro.
* In un computer può essere installata **una sola istanza del gateway di gestione dati**. Si supponga che si dispone di due data factory necessarie tooaccess origini di dati locali, è necessario gateway tooinstall sul computer due locale. In altre parole, un gateway è abbinato tooa data factory specificata
* Hello **gateway non è necessario toobe su hello stesso computer come origine dati hello**. Tuttavia, con l'origine dati toohello più vicino di gateway riduce il tempo di hello per origine dati di hello gateway tooconnect toohello. Si consiglia di installare gateway hello in un computer diverso da hello uno quell'origine dati host locale. Quando hello gateway e l'origine dati si trovano in computer diversi, gateway hello non si contendono le risorse con l'origine dati.
* È possibile avere **più gateway in computer diversi, la connessione toohello stessa origine dati locale**. Ad esempio, si dispone di due gateway gestisce due data factory ma hello stessa origine dati locale è registrato con entrambe le data factory hello.
* Se un gateway è già installato nel computer per uno scenario **Power BI**, installare un **gateway separato per Azure Data Factory** in un altro computer.
* È necessario usare il gateway anche quando si usa **ExpressRoute**.
* Considerare l'origine dati come origine dati locale, ovvero protetta da firewall, anche quando si usa **ExpressRoute**. Usare la connettività di tooestablish hello gateway tra il servizio di hello e origine dati hello.
* È necessario **usare gateway hello** anche se l'archivio dati hello è nel cloud hello in un **VM IaaS di Azure**.

## <a name="installation"></a>Installazione
### <a name="prerequisites"></a>Prerequisiti
* Hello supportato **del sistema operativo** versioni sono Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Installazione di gateway di gestione dati hello in un controller di dominio non è attualmente supportata.
* È necessario .NET Framework 4.5.1 o versioni successive. Se si installa il gateway in un computer Windows 7, installare .NET Framework 4.5 o versioni successive. Per informazioni dettagliate, vedere [Requisiti di sistema di .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) .
* Hello consigliato **configurazione** per il computer gateway hello è di almeno 2 GHz, 4 core, 8 GB di RAM e disco 80 GB.
* Se il computer host hello entra in sospensione, gateway hello non risponde toodata richieste. Pertanto, configurare un'apposita **risparmio di energia** computer hello prima di installare gateway hello. Se configurato toohibernate macchina hello, installazione del gateway hello richiede un messaggio.
* È necessario essere un amministratore tooinstall macchina hello e configurare il gateway di gestione dati hello correttamente. È possibile aggiungere altri utenti toohello **gateway di gestione dati utenti** gruppo locale di Windows. i membri di Hello di questo gruppo sono in grado di toouse hello **Gestione configurazione di Gateway di gestione di dati** gateway hello tooconfigure di strumento.

Come copiare verificarsi esecuzioni di attività in una frequenza specifica, hello utilizzo delle risorse (CPU, memoria) nel computer di hello anche segue hello stesso modello con ore di punta e periodi di inattività. Utilizzo delle risorse anche dipende molto quantità hello di spostamento dei dati. Quando sono in corso più processi di copia, l'utilizzo delle risorse aumenta durante i periodi di picco.

### <a name="installation-options"></a>Opzioni di installazione
È possibile installare il gateway di gestione di dati in hello seguenti modi:

* Mediante il download di un pacchetto di installazione MSI dal hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Hello MSI può anche essere utilizzati tooupgrade esistente dati Gestione gateway toohello versione più recente, con tutte le impostazioni mantenute.
* Facendo clic sul collegamento **Scaricare e installare il gateway dati** in INSTALLAZIONE MANUALE o **Installa direttamente in questo computer** in INSTALLAZIONE RAPIDA. Vedere l'articolo [Spostare dati tra origini locali e il cloud mediante il Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per le istruzioni dettagliate sull'installazione rapida. passaggio manuale Hello consente toohello download center.  istruzioni di Hello per scaricare e installare il gateway hello dall'area download sono riportate nella sezione successiva hello.

### <a name="installation-best-practices"></a>Procedure consigliate per l'installazione:
1. Configurare risparmio di energia sul computer host hello per gateway hello in modo che hello macchina non lo stato di ibernazione. Se il computer host hello entra in sospensione, gateway hello non risponde toodata richieste.
2. Eseguire il backup hello certificato associata hello gateway.

### <a name="install-hello-gateway-from-download-center"></a>Installare il gateway hello dall'area download
1. Passare troppo[pagina di download di Gateway di gestione dati Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).
2. Fare clic su **scaricare**, selezionare la versione appropriata di hello (**32-bit** Visual Studio. **a 64 bit**) e fare clic su **Avanti**.
3. Eseguire hello **MSI** direttamente o salvarlo tooyour disco ed eseguire.
4. In hello **iniziale** pagina, selezionare un **language** fare clic su **Avanti**.
5. **Accettare** hello contratto di licenza e fare clic su **Avanti**.
6. Selezionare **cartella** tooinstall hello gateway e fare clic su **Avanti**.
7. In hello **tooinstall pronto** pagina, fare clic su **installare**.
8. Fare clic su **fine** toocomplete installazione.
9. Ottenere la chiave di hello dal portale di Azure hello. Sezione successiva di hello per le istruzioni dettagliate, vedere.
10. In hello **registro gateway** pagina di **Gestione configurazione di Gateway di gestione di dati** in esecuzione nel computer, hello i passaggi seguenti:
    1. Incollare la chiave hello testo hello.
    2. Facoltativamente, fare clic su **chiave del gateway Mostra** toosee testo del tasto hello.
    3. Fare clic su **Register**.

### <a name="register-gateway-using-key"></a>Registrare il gateway con la chiave
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Se è ancora stato creato un gateway logico nel portale di hello
un gateway nella chiave di hello hello portal e ottenere da hello toocreate **configura** pagina, eseguire i passaggi della procedura dettagliata in hello [spostare i dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Se il gateway logico hello è già stato creato nel portale di hello
1. Nel portale di Azure passare toohello **Data Factory** pagina e fare clic su **servizi collegati** riquadro.

    ![Pagina Data factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. In hello **servizi collegati** pagina, seleziona hello logico **gateway** creato nel portale di hello.

    ![gateway logico](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. In hello **Gateway dati** pagina, fare clic su **scaricare e installare il gateway dati**.

    ![Collegamento nel portale di hello per il download](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. In hello **configura** pagina, fare clic su **chiave ricreare**. Fare clic su Sì nella finestra di messaggio hello dopo la lettura con attenzione.

    ![Ricrea chiave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Fare clic sulla chiave di toohello copia pulsante Avanti. chiave di Hello è Appunti toohello copiato.

    ![Copiare la chiave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Notifiche/icone nell'area di notifica
Hello immagine seguente vengono illustrate alcune hello cassetto icone presenti.

![icone dell'area di notifica](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Se il cursore si sposta sul messaggio di icona/notifica hello sistema barra delle applicazioni, vedrai i dettagli sullo stato di hello dell'operazione di aggiornamento del gateway/hello in una finestra popup.

### <a name="ports-and-firewall"></a>Porte e firewall
Sono disponibili due firewall, è necessario tooconsider: **firewall aziendale** in esecuzione sul router centrale di hello dell'organizzazione di hello, e **Windows firewall** configurato come un daemon sul computer locale hello dove hello gateway è installato.  

![firewall](./media/data-factory-data-management-gateway/firewalls2.png)

A livello di firewall aziendale, è necessario configurare seguente hello domini e le porte in uscita:

| Nomi di dominio | Porte | Descrizione |
| --- | --- | --- |
| *.servicebus.windows.net |443, 80 |Utilizzato per la comunicazione con il backend Data Movement Service |
| *.core.windows.net |443 |Utilizzato per la copia di staging mediante il BLOB di Azure (se configurata)|
| *.frontend.clouddatahub.net |443 |Utilizzato per la comunicazione con il backend Data Movement Service |


A livello di Windows Firewall queste porte in uscita sono generalmente abilitate. Se non è possibile configurare le porte e domini hello conseguenza nel computer gateway.

> [!NOTE]
> 1. In base all'origine / sink, è possibile toowhitelist altri domini e le porte in uscita in aziendali/Windows firewall.
> 2. Per alcuni database Cloud (ad esempio: [Database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access)e così via), potrebbe essere necessario toowhitelist di indirizzo IP del Gateway per la configurazione di firewall.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Copiare i dati da un archivio dati di origine dati archivio tooa sink
Verificare che le regole del firewall hello sono attivate correttamente sul firewall aziendale hello, Windows firewall nel computer gateway hello, e dati hello archiviano stesso. L'abilitazione di queste regole consente hello origine tooboth tooconnect di gateway e sink correttamente. Abilitare le regole per ogni archivio dati coinvolto nell'operazione di copia hello.

Ad esempio, toocopy da **un sink di Database SQL di Azure locale dati archivio tooan o un sink di Azure SQL Data Warehouse**, hello i passaggi seguenti:

* Consentire comunicazioni **TCP** in uscita sulla porta **1433** per Windows Firewall e il firewall aziendale.
* Configurare le impostazioni di firewall hello di SQL Azure tooadd hello indirizzo IP del server dell'elenco di hello gateway macchina toohello di indirizzi IP consentiti.

> [!NOTE]
> Se il firewall non consente la porta in uscita 1433, il gateway non riesce ad accedere direttamente ad Azure SQL. In questo caso, è possibile utilizzare [staging copia](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Database Azure / Azure SQL DW. In questo scenario, richiederebbe solo HTTPS (porta 443) per lo spostamento dei dati di hello.
>
>


### <a name="proxy-server-considerations"></a>Considerazioni sui server proxy
Se nell'ambiente di rete aziendale utilizza un proxy server tooaccess hello internet, configurare le impostazioni proxy appropriati toouse di dati Gestione gateway. È possibile impostare il proxy di hello durante la fase di registrazione iniziale hello.

![Impostare il proxy durante la registrazione](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

Gateway utilizza il servizio cloud toohello tooconnect di hello proxy server. Fare clic sul collegamento **Modifica** durante la configurazione iniziale. Vedrai hello **impostazione proxy** finestra di dialogo.

![Impostare il proxy tramite Gestione configurazione](media/data-factory-data-management-gateway/SetProxySettings.png)

Sono disponibili tre opzioni di configurazione:

* **Non usare il proxy**: Gateway non utilizza i servizi di toocloud tooconnect proxy in modo esplicito.
* **Utilizzare il proxy di sistema**: il Gateway utilizza proxy hello impostazione configurata in diahost.exe.config e diawp.exe.config.  Se è configurato alcun proxy diahost.exe.config e diawp.exe.config, gateway si connette toocloud servizio direttamente senza dover passare attraverso proxy.
* **Utilizzare il proxy personalizzato**: configurare hello HTTP proxy impostazione toouse per il gateway, invece di usare le configurazioni in diahost.exe.config e diawp.exe.config.  L'indirizzo e la porta sono valori obbligatori.  Nome utente e password sono facoltativi a seconda dell'impostazione di autenticazione del proxy.  Tutte le impostazioni vengono crittografate con il certificato delle credenziali hello del gateway hello e archiviate in locale nel computer host di gateway hello.

Servizio Host di gateway di gestione dati Hello viene riavviata automaticamente dopo aver salvato le impostazioni del proxy hello aggiornato.

Dopo che gateway è stato registrato correttamente, se si desidera tooview o aggiornare le impostazioni proxy, utilizzare Gestione configurazione di Gateway di gestione di dati.

1. Avviare **Gestione configurazione di Gateway di gestione dati**.
2. Passare toohello **impostazioni** scheda.
3. Fare clic su **modifica** collegamento **HTTP Proxy** hello toolaunch sezione **Set Proxy HTTP** finestra di dialogo.  
4. Dopo aver fatto clic hello **Avanti** pulsante, viene visualizzato un messaggio di avviso che chiede di per l'impostazione proxy di autorizzazione toosave hello e riavviare il servizio Host di Gateway di hello.

È possibile visualizzare e aggiornare il proxy HTTP tramite lo strumento Gestione configurazione.

![Impostare il proxy tramite Gestione configurazione](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Se si configura un server proxy con l'autenticazione NTLM, account di dominio hello viene eseguito il servizio Host di Gateway. Se si modifica la password di hello per l'account di dominio hello in un secondo momento, ricordare tooupdate le impostazioni di configurazione per il servizio hello e riavviarlo di conseguenza. A causa di toothis requisito, si consiglia di che utilizzare un dominio dedicato account tooaccess hello server proxy che non richiede la password di hello tooupdate frequentemente.
>
>

### <a name="configure-proxy-server-settings"></a>Configurare le impostazioni del server proxy
Se si seleziona **Usa il proxy di sistema** impostazione per il proxy HTTP di hello, gateway Usa impostazione diahost.exe.config e diawp.exe.config proxy hello.  Se viene specificato alcun proxy in diahost.exe.config e diawp.exe.config, gateway si connette toocloud servizio direttamente senza dover passare attraverso proxy. Hello procedura riportata di seguito vengono fornite istruzioni per l'aggiornamento dei file diahost.exe.config hello.  

1. In Esplora File, file originale hello costituiscono una copia di C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback-safe.
2. Avviare Notepad.exe come amministratore e aprire il file di testo "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config". Trovare un tag predefinito hello per system.net come illustrato nel seguente codice hello:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   È quindi possibile aggiungere i dettagli del server proxy come illustrato nell'esempio seguente hello:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Proprietà aggiuntive sono consentite all'interno di hello proxy tag toospecify hello necessarie impostazioni come scriptLocation. Fare riferimento troppo[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) sulla sintassi.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Salvare il file di configurazione di hello nel percorso originale di hello, quindi riavviare il servizio Host di Gateway di gestione dati, che preleva modifiche hello hello. servizio hello toorestart: utilizzare l'applet Servizi dal Pannello di controllo hello o da hello **Gestione configurazione di Gateway di gestione di dati** > fare clic su hello **Arresta servizio** , quindi fare clic su hello **Avviare servizio**. Se non viene avviato il servizio di hello, è probabile che sia stato aggiunto una sintassi non corretta di tag XML nel file di configurazione dell'applicazione hello che è stato modificato.

> [!IMPORTANT]
> Non dimenticare tooupdate **entrambi** diahost.exe.config e diawp.exe.config.  


Inoltre punti toothese, è inoltre necessario che Microsoft Azure sia nell'elenco elementi consentiti dell'azienda toomake. elenco di Hello di indirizzi IP di Microsoft Azure può essere scaricato da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Possibili sintomi di problemi correlati al firewall e al server proxy
Se si verifica errori toohello simile dopo quelli, è probabile causa configurazione tooimproper di hello server proxy o firewall, che blocca i gateway di connessione tooauthenticate di Factory tooData stesso. Fare riferimento tooprevious sezione tooensure il server proxy e firewall siano configurate correttamente.

1. Quando si tenta di gateway hello tooregister, viene visualizzato il seguente errore hello: "chiave del gateway hello tooregister non riuscito. Prima di tentare nuovamente la chiave del gateway hello tooregister, verificare che sia stato avviato hello gateway di gestione dati è in uno stato di connessione e hello servizio Host di Gateway di gestione di dati."
2. Quando si apre Gestione configurazione, lo stato del gateway visualizzato può essere "Disconnesso" o "Connessione". Quando si visualizzano i registri eventi di Windows, in "Visualizzatore eventi" > "Registri applicazioni e servizi" > "Gateway di gestione dati" vedere i messaggi di errore, ad esempio hello errore seguente:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Aprire la porta 8050 per la crittografia delle credenziali
Hello **impostazione delle credenziali** utilizzi dell'applicazione hello porta in ingresso **8050** toorelay gateway toohello di credenziali quando si configura una locale il servizio nel portale di Azure hello collegato. Durante l'installazione di gateway, per impostazione predefinita, installazione del gateway hello verrà aperto nel computer gateway hello.

Se si utilizza un firewall di terze parti, è possibile aprire manualmente la porta hello 8050. In caso di problema di firewall durante l'installazione di gateway, è possibile provare a usare hello seguenti gateway hello tooinstall di comando senza configurare il firewall hello.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Se si sceglie di non tooopen porta hello 8050 nel computer gateway hello, utilizzare meccanismi diversi dalla hello **impostazione delle credenziali** dati dell'applicazione tooconfigure archiviano le credenziali. È ad esempio possibile usare il cmdlet di PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) . Per informazioni su come impostare le credenziali dell'archivio dati, vedere la sezione [Impostare le credenziali e la sicurezza](#set-credentials-and-securityy) .

## <a name="update"></a>Aggiornare
Per impostazione predefinita, il gateway di gestione di dati viene automaticamente aggiornato quando è disponibile una versione più recente del gateway hello. gateway Hello non viene aggiornata fino a quando non vengono eseguite tutte le attività pianificata hello. Nessuna ulteriore attività viene elaborata dal gateway hello fino a quando non viene completata l'operazione di aggiornamento hello. Se hello aggiornamento non riesce, gateway viene eseguito il rollback toohello vecchia versione.

Viene visualizzato l'ora dell'aggiornamento pianificato hello in hello seguenti posizioni:

* pagina delle proprietà di gateway Hello in hello portale di Azure.
* Home page di hello Gestione configurazione di Gateway di gestione dati
* Messaggi di notifica dell'aria di notifica

scheda Home di Hello di hello Gestione configurazione di Gateway di gestione di dati consente di visualizzare la pianificazione di aggiornamento hello e hello ultimo tempo hello gateway non ha installato o aggiornato.

![Pianificare gli aggiornamenti](media/data-factory-data-management-gateway/UpdateSection.png)

È possibile installare update hello immediatamente o attendere hello gateway toobe aggiornati automaticamente in fase di hello pianificata. Ad esempio, hello seguente immagine Mostra hello messaggio di notifica nell'hello Gateway Configuration Manager con il pulsante di aggiornamento hello che è possibile fare clic su tooinstall viene immediatamente.

![Aggiorna in Gestione configurazione di Gateway di gestione dati](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

messaggio di notifica Hello nella barra delle applicazioni hello sarebbe come illustrato nella seguente immagine hello:

![Messaggio nell'area di notifica](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Viene visualizzato lo stato di hello dell'operazione di aggiornamento (manuale o automatica) nella barra delle applicazioni hello. Quando si avvia Gestione configurazione di Gateway successivo, viene visualizzato un messaggio per la notifica di hello barra gateway hello è stato aggiornato insieme a un collegamento troppo[novità nuovo argomento](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>funzionalità di aggiornamento automatico toodisable/attiva
È possibile Abilita/disabilita la funzionalità di aggiornamento automatico hello effettuando hello alla procedura seguente:

[Per gateway a nodo singolo]
1. Avviare Windows PowerShell nel computer gateway hello.
2. Passa a cartella C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript toohello.
3. Esecuzione hello successivo comando tooturn hello l'aggiornamento automatico delle funzionalità di disattivare.   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tooturn nuovamente in:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Per gateway a più nodi a disponibilità e scalabilità elevate (anteprima)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Avviare Windows PowerShell nel computer gateway hello.
2. Passa a cartella C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript toohello.
3. Esecuzione hello successivo comando tooturn hello l'aggiornamento automatico delle funzionalità di disattivare.   

    Per il gateway con funzionalità di disponibilità elevata (anteprima), è necessario un parametro di AuthKey aggiuntivo.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tooturn nuovamente in:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Se si accede portale hello da un computer diverso dal computer del gateway hello, è necessario assicurarsi che un'applicazione hello Gestione credenziali può connettersi toohello computer del gateway. Se un'applicazione hello non può raggiungere i computer del gateway hello, quindi non consente tooset le credenziali per l'origine dati hello e tootest connessione toohello dati.  

Quando si utilizza hello **impostazione delle credenziali** applicazione portale hello consente di crittografare credenziali hello con certificato hello specificato in hello **certificato** scheda di hello **Gateway Configuration Manager** nel computer gateway hello.

Se si sta cercando un approccio basato su API per la crittografia delle credenziali hello, è possibile utilizzare hello [New AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) credenziali tooencrypt cmdlet di PowerShell. cmdlet di Hello Usa certificato hello che tale gateway è configurato toouse tooencrypt hello credenziali. Aggiungere le credenziali crittografate toohello **EncryptedCredential** elemento di hello **connectionString** in hello JSON. Per utilizzare JSON hello hello [New AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet o nell'Editor delle Data Factory hello.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Esiste un altro approccio per impostare le credenziali usando l'editor delle data factory. Se si crea un SQL Server collegato usando hello editor e immettere le credenziali in testo normale, le credenziali di hello vengono crittografate utilizzando un certificato a cui appartiene il servizio di Data Factory hello. Non utilizza il certificato di hello che tale gateway è configurato toouse. Anche se questo approccio può apparire leggermente più veloce, in alcuni casi risulta meno sicuro. È pertanto consigliabile seguire questo approccio solo per scopi di sviluppo o di test.

## <a name="powershell-cmdlets"></a>Cmdlet PowerShell
Questa sezione viene descritto come toocreate e registrare un gateway con i cmdlet PowerShell di Azure.

1. Avviare **Azure PowerShell** in modalità di amministrazione.
2. Accedi tooyour account Azure eseguendo hello comando seguente e immettere le credenziali di Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Hello utilizzare **New AzureRmDataFactoryGateway** toocreate cmdlet un gateway logico come indicato di seguito:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Comando di esempio e output**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. In Azure PowerShell, passare cartella toohello: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**. Eseguire **RegisterGateway.ps1** associata alla variabile locale hello **$Key** come illustrato nel comando seguente hello. Questo script registra l'agente client hello installato nel computer con gateway di hello logico creato in precedenza.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    È possibile registrare il gateway hello in un computer remoto utilizzando il parametro IsRegisterOnRemoteMachine hello. Esempio:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. È possibile utilizzare hello **Get AzureRmDataFactoryGateway** elenco hello tooget di cmdlet di gateway nella data factory. Quando hello **stato** Mostra **online**, significa che il gateway è toouse pronto.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
È possibile rimuovere un gateway tramite hello **Remove AzureRmDataFactoryGateway** descrizione cmdlet e aggiornamento per un gateway tramite hello **Set AzureRmDataFactoryGateway** cmdlet. Per la sintassi e altri dettagli relativi a questi cmdlet, vedere Riferimento ai cmdlet di Data Factory.  

### <a name="list-gateways-using-powershell"></a>Elencare i gateway usando PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Rimuovere il gateway usando PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Passaggi successivi
* Vedere l'articolo [Spostare dati tra archivi dati locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) . In questa procedura dettagliata hello, creare una pipeline che utilizza hello gateway toomove dati da un tooan di database di SQL Server on-premise blob di Azure.  

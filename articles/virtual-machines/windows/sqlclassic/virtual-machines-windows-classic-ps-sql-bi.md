---
title: aaaSQL Server Business Intelligence | Documenti Microsoft
description: "In questo argomento utilizza le risorse create con il modello di distribuzione classica hello e descrive le funzionalità di Business Intelligence (BI) hello disponibili per SQL Server in esecuzione su macchine virtuali di Azure (VM)."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>SQL Server Business Intelligence in Macchine virtuali di Azure
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

nella raccolta di macchine virtuali di Microsoft Azure Hello sono incluse immagini contenenti installazioni di SQL Server. Hello SQL Server sono supportate nelle immagini della raccolta hello edizioni hello stessi file di installazione, è possibile installare computer tooon locali e macchine virtuali. Questo argomento vengono riepilogati hello SQL Server Business Intelligence (BI) installate nelle immagini hello le funzionalità e i passaggi di configurazione necessari dopo il provisioning di una macchina virtuale. Questo argomento descrive inoltre le topologie di distribuzione supportate per le funzionalità di Business Intelligence e le procedure consigliate.

## <a name="license-considerations"></a>Considerazioni sulle licenze
Esistono due modi toolicense SQL Server in macchine virtuali di Microsoft Azure:

1. Vantaggi di mobilità delle licenze che fanno parte del contratto Software Assurance. Per altre informazioni, vedere [Mobilità delle licenze tramite Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. Pagare la tariffa oraria di macchine virtuali di Azure con SQL Server installato. Vedere la sezione "SQL Server" in hello [macchine virtuali: prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Per altre informazioni sulla gestione delle licenze e le tariffe attuali, vedere l'articolo relativo alle [domande frequenti sulle licenze di macchine virtuali](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>Immagini SQL Server disponibili nella raccolta macchine virtuali di Azure
nella raccolta di macchine virtuali di Microsoft Azure Hello sono incluse diverse immagini contenenti Microsoft SQL Server. installato sulle immagini di macchina virtuale hello software Hello varia in base hello versione del sistema operativo hello hello del e SQL Server. elenco di Hello delle immagini disponibili nella raccolta di macchine virtuali di Azure hello cambia di frequente.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Immagine SQL nella raccolta di macchine virtuali di Azure](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hello seguente script di PowerShell restituisce hello elenco di immagini di Azure che contengono "SQL Server" in ImageName hello:

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Per ulteriori informazioni sulle edizioni e le funzionalità supportate da SQL Server, vedere l'esempio hello:

* [Edizioni di SQL Server](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Funzioni supportate dalle edizioni di SQL Server 2016 hello](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>Le funzionalità di Business Intelligence installate su hello immagini della Galleria macchina virtuale di SQL Server
Hello nella tabella seguente vengono riepilogate le funzionalità di Business Intelligence hello installate hello comune Microsoft Azure raccolta immagini di macchina virtuale per SQL Server:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| Funzionalità SQL Server BI | Installato nell'immagine della raccolta hello | Note |
| --- | --- | --- |
| **Modalità nativa di Reporting Services** |Sì |Installata ma richiede la configurazione, inclusi l'URL di gestione report hello. Vedere la sezione hello [configurare Reporting Services](#configure-reporting-services). |
| **Modalità SharePoint di Reporting Services** |No |Hello immagine della raccolta di macchine virtuali di Microsoft Azure non include SharePoint o SharePoint i file di installazione. <sup>1</sup> |
| **Modalità multidimensionale e di Data mining di Analysis Services (OLAP)** |Sì |Istanza di Analysis Services installato e configurato come hello predefinita |
| **Modalità tabulare di Analysis Services** |No |Supportata nelle immagini di SQL Server 2012, 2014 e 2016 ma non è installata per impostazione predefinita. Installare un'altra istanza di Analysis Services. Vedere la sezione hello installare altri servizi di SQL Server e funzionalità in questo argomento. |
| **Analysis Services Power Pivot per SharePoint** |No |Hello immagine della raccolta di macchine virtuali di Microsoft Azure non include SharePoint o SharePoint i file di installazione. <sup>1</sup> |

<sup>1</sup> Per altre informazioni su SharePoint e le macchine virtuali di Azure, vedere gli articoli [Microsoft Azure Architectures for SharePoint 2013](https://technet.microsoft.com/library/dn635309.aspx) (Architetture di Microsoft Azure per SharePoint 2013) e [SharePoint Deployment on Microsoft Azure Virtual Machines](https://www.microsoft.com/download/details.aspx?id=34598)(Distribuzione di SharePoint in macchine virtuali di Microsoft Azure).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Eseguire hello tooget comando PowerShell seguente di un elenco dei servizi installati che contengono "SQL" nel nome del servizio hello.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Indicazioni generali e procedure consigliate
* dimensioni consigliata per una macchina virtuale è minimo Hello **A3** quando si utilizza SQL Server Enterprise Edition. Hello **A4** dimensioni della macchina virtuale sono consigliata per distribuzioni di SQL Server Business Intelligence di Analysis Services e Reporting Services.
  
    Per informazioni sulle dimensioni di macchina virtuale corrente hello, vedere [dimensioni delle macchine virtuali per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Una procedura consigliata per la gestione disco è diverso da toostore file di dati, log e backup su unità **C**: e **D**:. Ad esempio, è possibile creare i dischi dati **E**: e **F**:.
  
  * unità di Hello la memorizzazione nella cache dei criteri per l'unità predefinita hello **C**: non è ottimale per l'utilizzo di dati.
  * Hello **D**: unità è un'unità temporanea che viene utilizzata principalmente per il file di paging hello. Hello **D**: non è persistente e non viene salvata nell'archiviazione blob. Gestione attività, ad esempio una dimensione di macchina virtuale modifica toohello Reimposta hello **D**: unità. È consigliabile troppo**non** utilizzare hello **D**: unità per i file di database, incluso tempdb.
    
    Per ulteriori informazioni sulla creazione e collegamento di dischi, vedere [come tooAttach tooa un disco dati macchina virtuale](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Arrestare o disinstallare i servizi non si prevede toouse. Per esempio, se macchina virtuale hello viene usato solo per Reporting Services, arrestare o disinstallare Analysis Services e SQL Server Integration Services. Hello immagine seguente è riportato un esempio di servizi di hello che vengono avviati per impostazione predefinita.
  
    ![Servizi di SQL Server](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > motore di database di SQL Server Hello è necessario negli scenari di BI hello è supportato. In una topologia di macchina virtuale del singolo server, è necessario il motore di database hello toobe in esecuzione su hello stessa macchina virtuale.
  
    Per ulteriori informazioni, vedere l'esempio hello: [disinstallare Reporting Services](https://msdn.microsoft.com/library/hh479745.aspx) e [disinstallare un'istanza di Analysis Services](https://msdn.microsoft.com/library/ms143687.aspx).
* Controllare se in **Windows Update** sono disponibili nuovi "aggiornamenti importanti". le immagini di macchina virtuale di Microsoft Azure Hello vengono aggiornate di frequente; Tuttavia gli aggiornamenti importanti potrebbe diventare disponibili da **Windows Update** dopo l'ultimo aggiornamento dell'immagine di macchina virtuale hello.

## <a name="example-deployment-topologies"></a>Topologie di distribuzione di esempio
di seguito Hello sono esempi di distribuzione che utilizzano macchine virtuali di Microsoft Azure. topologie di Hello in questi diagrammi sono solo alcune delle possibili topologie hello che è possibile utilizzare con funzionalità di Business Intelligence di SQL Server e macchine virtuali di Microsoft Azure.

### <a name="single-virtual-machine"></a>Singola macchina virtuale
Analysis Services, Reporting Services e il motore di Database SQL Server e origini dati in una singola macchina virtuale.

![scenario BI iaaS con 1 macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>Due macchine virtuali
* Analysis Services, Reporting Services e hello il motore di Database di SQL Server in una singola macchina virtuale. Questa distribuzione include i database del server di report hello.
* Origini dati in una seconda macchina virtuale. Hello seconda macchina virtuale include il motore di Database di SQL Server come origine dati.

![Scenario BI IaaS con 2 macchine virtuali](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Dati misti di Azure nel database SQL di Azure
* Analysis Services, Reporting Services e hello il motore di Database di SQL Server in una singola macchina virtuale. Questa distribuzione include i database del server di report hello.
* Origine dati è il database di SQL Azure.

![macchina virtuale scenari BI iaas e AzureSQL come origine dati](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Dati ibridi locali
* In questo esempio di distribuzione hello il motore di Database di SQL Server Analysis Services e Reporting Services eseguito in una singola macchina virtuale. host macchina virtuale Hello hello database del server di report. macchina virtuale Hello è tooan aggiunti a un dominio locale tramite la rete virtuale di Azure o alcuni altri soluzione di tunneling VPN.
* L'origine dati è locale.

![macchina virtuale scenari BI iaas e origini dati locali](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Configurazione di Reporting Services in modalità nativa
immagine della raccolta Hello macchina virtuale per SQL Server include la modalità nativa di Reporting Services installata, ma non è configurato il server di report di hello. passaggi di Hello in questa sezione Configura server di report di Reporting Services di hello. Per informazioni più dettagliate sulla configurazione della modalità nativa di Reporting Services, vedere [Installare il server di report in modalità nativa di Reporting Services](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Per contenuto simile che utilizza i server di report hello tooconfigure script Windows PowerShell, vedere [utilizzare PowerShell tooCreate un Azure VM con un Server in modalità nativa Report](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Connettersi toohello macchina virtuale e avviare Gestione configurazione Reporting Services hello
Sono disponibili due flussi di lavoro comuni per la connessione tooan macchina virtuale di Azure:

* tooconnect in hello, fare clic sul nome della macchina virtuale hello hello e quindi fare clic su **Connetti**. Verrà aperta una connessione desktop remota e il nome di computer hello viene popolato automaticamente.
  
    ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Connessione macchina virtuale toohello con connessione Desktop remoto di Windows. Nell'interfaccia utente di hello di desktop remoto hello:
  
  1. Hello tipo **nome del servizio cloud** come nome del computer hello.
  2. Digitare due punti (:) e il numero di porta pubblica configurato per l'endpoint di desktop remoto di hello TCP hello.
     
      Myservice.cloudapp.net:63133
     
      Per altre informazioni, vedere l'articolo relativo alla [definizione di servizio cloud](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Avviare Gestione configurazione di Reporting Services**

In **Windows Server 2012/2016**:

1. Da hello **avviare** digitare **Reporting Services** toosee un elenco di App.
2. Fare clic con il pulsante destro del mouse su **Gestione configurazione Reporting Services** e scegliere **Esegui come amministratore**.

In **Windows Server 2008 R2**:

1. Fare clic su **Start** e quindi su **Tutti i programmi**.
2. Fare clic su **Microsoft SQL Server 2016**.
3. Fare clic su **Strumenti di configurazione**.
4. Fare clic con il pulsante destro del mouse su **Gestione configurazione Reporting Services** e scegliere **Esegui come amministratore**.

In alternativa:

1. Fare clic su **Avvia**.
2. In hello **Cerca programmi e file** tipo finestra di dialogo **reporting services**. Se hello macchina virtuale è in esecuzione Windows Server 2012, digitare **reporting services** nella schermata Start di Windows Server 2012 hello.
3. Fare clic con il pulsante destro del mouse su **Gestione configurazione Reporting Services** e scegliere **Esegui come amministratore**.
   
    ![ricerca di Gestione configurazione ssrs](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Configurare Reporting Services
**Account del servizio e URL del servizio web:**

1. Verificare hello **nome Server** è nome del server locale hello e fare clic su **Connetti**.
2. Hello nota vuoto **Nome Database del Server di Report**. Hello database viene creato al termine della configurazione di hello.
3. Verificare hello **stato Server di Report** è **Started**. Se si desidera che il servizio di hello tooverify in Server Manager di Windows, servizio hello è hello **SQL Server Reporting Services** servizio Windows.
4. Fare clic su **Account del servizio** e modificare account hello in base alle esigenze. Se macchina virtuale hello viene usato in un ambiente unita in join non di dominio, hello incorporato **ReportServer** è sufficiente un account. Per ulteriori informazioni sull'account del servizio hello, vedere [Account del servizio](https://msdn.microsoft.com/library/ms189964.aspx).
5. Fare clic su **URL servizio Web** nel riquadro di sinistra hello.
6. Fare clic su **applica** tooconfigure i valori predefiniti di hello.
7. Hello nota **URL servizio Web ReportServer**. Si noti che la porta TCP predefinita hello è 80 e fa parte dell'URL hello. In un passaggio successivo è creare un Endpoint della macchina virtuale Microsoft Azure per la porta hello.
8. In hello **risultati** riquadro verifica azioni di hello completate.

**Database:**

1. Fare clic su **Database** nel riquadro di sinistra hello.
2. Fare clic su **Modifica database**.
3. Accertarsi che l'opzione **Crea un nuovo database del server di report** sia selezionata e quindi fare clic su Avanti.
4. Verificare il **Nome server** e fare clic su **Test connessione**.
5. Se il risultato di hello **Test della connessione riuscito**, fare clic su **OK** e quindi fare clic su **Avanti**.
6. Nome del database hello nota **ReportServer** hello e **modalità Server di Report** è **nativo** quindi fare clic su **Avanti**.
7. Fare clic su **Avanti** su hello **credenziali** pagina.
8. Fare clic su **Avanti** su hello **riepilogo** pagina.
9. Fare clic su **Avanti** su hello **sullo stato di avanzamento e di fine** pagina.

**URL Portale Web o URL Gestione report per le versioni 2012 e 2014:**

1. Fare clic su **URL del portale Web**, o **URL gestione Report** per 2014 e 2012, nel riquadro di sinistra hello.
2. Fare clic su **Apply**.
3. In hello **risultati** riquadro verifica azioni di hello completate.
4. Fare clic su **Esci**.

Per informazioni sulle autorizzazioni del server di report, vedere [Concessione di autorizzazioni in un server di report in modalità nativa](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Sfoglia toohello gestione Report locale
configurazione di hello tooverify, manager tooreport Sfoglia in hello macchina virtuale.

1. In hello macchina virtuale, avviare Internet Explorer con privilegi di amministratore.
2. Sfoglia toohttp://localhost/reports su hello macchina virtuale.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>portale web di tooConnect tooRemote o gestione Report per 2014 e 2012
Se si desidera, portale web di tooconnect toohello o gestione Report per 2014 e 2012, nella macchina virtuale hello da un computer remoto, creare una nuova macchina virtuale Endpoint TCP. Per impostazione predefinita, il server di report hello è in ascolto delle richieste HTTP sulla **la porta 80**. Se si configura server di report hello, toouse URL di una porta diversa, è necessario specificare il numero della porta in hello attenendosi alle istruzioni.

1. Creare un Endpoint per hello macchina virtuale sulla porta TCP 80. Per ulteriori informazioni, vedere hello [endpoint della macchina virtuale e porte del Firewall](#virtual-machine-endpoints-and-firewall-ports) sezione in questo documento.
2. Aprire la porta 80 nel firewall della macchina virtuale hello.
3. Passare al portale web toohello o Gestione report, utilizzando una macchina virtuale di Azure **nome DNS** come nome del server nell'URL hello hello. ad esempio:
   
    **Server di report**: http://uebi.cloudapp.net/reportserver **Portale Web**: http://uebi.cloudapp.net/reports
   
    [Configurare un firewall per l'accesso al server di report](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate e pubblicare report toohello macchina virtuale di Azure
Hello nella tabella seguente vengono riepilogati alcuni dei report esistenti hello opzioni toopublish disponibile da un server di report locale computer toohello ospitato in hello macchina virtuale di Microsoft Azure:

* **Generatore report**: macchina virtuale di hello inclusa hello-versione ClickOnce di Generatore Report di Microsoft SQL Server per SQL 2014 e 2012. hello Generatore Report di toostart prima volta sulla macchina virtuale hello con SQL 2016:
  
  1. Avviare il browser con privilegi amministrativi.
  2. Toohello web del portale di hello macchina virtuale, di individuare e selezionare hello **scaricare** sull'icona nell'angolo superiore destro di hello.
  3. Selezionare **Generatore report**.
     
     Per altre informazioni, vedere [Start Report Builder](https://msdn.microsoft.com/library/ms159221.aspx)(Avviare il Generatore report).
* **SQL Server Data Tools**: VM: SQL Server Data Tools sia installato nella macchina virtuale hello e può essere utilizzato toocreate **progetti Server di Report** e report sulla macchina virtuale hello. SQL Server Data Tools è possibile pubblicare server di report di toohello hello report sulla macchina virtuale hello.
* **SQL Server Data Tools - Remoto**: nel computer locale creare un progetto di Reporting Services in SQL Server Data Tools contenente i report di Reporting Services. Configurare l'URL del servizio web tooconnect toohello hello progetto.
  
    ![proprietà del progetto ssdt per un progetto SSRS](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Creare una. Disco rigido disco rigido virtuale che contiene i report e quindi carica e collega unità hello.
  
  1. Creare un disco rigido VHD nel computer locale che contenga i report.
  2. Creare e installare un certificato di gestione.
  3. Caricare hello tooAzure di file di disco rigido virtuale utilizzando il cmdlet Add-AzureVHD hello [creazione e caricamento di un disco rigido virtuale di Windows Server di tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Collegare una macchina virtuale di hello disco toohello.

## <a name="install-other-sql-server-services-and-features"></a>Installare altri servizi e funzionalità di SQL Server
tooinstall ulteriori servizi di SQL Server, ad esempio Analysis Services in modalità tabulare, eseguire l'installazione guidata di hello SQL server. file di installazione Hello sono sul disco locale della macchina virtuale hello.

1. Fare clic su **Start** e quindi su **Tutti i programmi**.
2. Fare clic su **Microsoft SQL Server 2016**, **Microsoft SQL Server 2014** o **Microsoft SQL Server 2012** e quindi su **Strumenti di configurazione**.
3. Fare clic su **Centro installazione SQL Server**.

O eseguire C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe o C:\SQLServer_11.0_full\setup.exe

> [!NOTE]
> Hello prima volta che si esegue l'installazione di SQL Server, l'installazione di più file possono essere scaricati e richiedono il riavvio della macchina virtuale hello e il riavvio del programma di installazione di SQL Server.
> 
> Se è necessario toorepeatedly personalizzare l'immagine di hello selezionata dalla hello macchina virtuale di Microsoft Azure, è consigliabile creare la propria immagine di SQL Server. È stata abilitata la funzionalità di Analysis Services SysPrep con SQL Server 2012 SP1 CU2. Per altre informazioni, vedere [Considerazioni sull'installazione di SQL Server tramite SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) e [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Supporto SysPrep per ruoli server).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall modalità tabulare di Analysis Services
i passaggi in questa sezione Hello **riepilogare** hello installazione della modalità tabulare di Analysis Services. Per ulteriori informazioni, vedere l'esempio hello:

* [Installare Analysis Services in modalità tabulare](https://msdn.microsoft.com/library/hh231722.aspx)
* [Modellazione tabulare (esercitazione AdventureWorks)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall modalità tabulare di Analysis Services:**

1. Nell'installazione guidata di hello SQL Server, fare clic su **installazione** in hello riquadro sinistro e quindi fare clic su **installazione autonoma di nuovo SQL server oppure aggiungere l'installazione esistente di funzionalità tooan**.
   
   * Se viene visualizzato hello **Sfoglia per cartelle**, tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full o c:\SQLServer_11.0_full e quindi fare clic su **Ok**.
2. Fare clic su **Avanti** nella pagina aggiornamenti del prodotto hello.
3. In hello **tipo di installazione** selezionare **eseguire una nuova installazione di SQL Server** e fare clic su **Avanti**.
4. In hello **impostazione ruolo** pagina, fare clic su **installazione funzionalità SQL Server**.
5. In hello **Selezione funzionalità** pagina, fare clic su **Analysis Services**.
6. In hello **configurazione istanza** , digitare un nome descrittivo, ad esempio **tabulare** in **istanza denominata** e **Id istanza** testo finestre.
7. In hello **configurazione di Analysis Services** selezionare **modalità tabulare**. Aggiungere l'elenco hello corrente utente toohello autorizzazioni amministrative.
8. Completare e chiudere l'installazione guidata di SQL Server hello.

## <a name="analysis-services-configuration"></a>Configurazione di Analysis Services
### <a name="remote-access-tooanalysis-services-server"></a>TooAnalysis di accesso remoto i Server di servizi
Il server Analysis Services supporta solo l'autenticazione di windows. tooaccess Analysis Services in modalità remota da applicazioni client, ad esempio SQL Server Management Studio o SQL Server Data Tools, macchina virtuale hello deve toobe tooyour aggiunti a un dominio locale, utilizzando le funzionalità di rete virtuale di Azure. Per altre informazioni, vedere [Rete virtuale di Azure](../../../virtual-network/virtual-networks-overview.md).

Un'**istanza predefinita** di Analysis Services è in ascolto sulla porta TCP **2383**. Aprire hello porta nel firewall delle macchine virtuali hello. Anche un'istanza denominata di Analysis Services in cluster è in ascolto sulla porta **2383**.

Per un **istanza denominata** di Analysis Services, è necessario il servizio SQL Server Browser hello toomanage accesso alla porta. configurazione predefinita di SQL Server Browser Hello è porta **2382**.

Aprire la porta nel firewall delle macchine virtuali hello, **2382** e creare una porta dell'istanza denominata di Analysis Services statico.

1. tooverify porte già in utilizzare hello macchina virtuale e il processo che utilizza porte hello, eseguire hello comando con privilegi amministrativi seguente:
   
        netstat /ao
2. Utilizzare SQL Server Management Studio toocreate un statico di Analysis Services denominata porta dell'istanza mediante l'aggiornamento 'Porta' valore tabulare AS proprietà generali dell'istanza. Per ulteriori informazioni, vedere hello "Utilizzare una porta fissa per impostazione predefinita o istanza denominata" in [configurare Windows Firewall di hello tooAllow accesso ad Analysis Services](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Riavviare l'istanza tabulare hello hello servizio Analysis Services.

Per ulteriori informazioni, vedere hello **endpoint della macchina virtuale e porte del Firewall** sezione in questo documento.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Endpoint della macchina virtuale e porte del Firewall
Questa sezione vengono riepilogati gli endpoint di macchina virtuale di Microsoft Azure tooopen toocreate e porte nei firewall macchina virtuale hello. Hello nella tabella seguente sono riepilogati hello **TCP** hello tooopen di porte nel firewall delle macchine virtuali hello e di endpoint toocreate per le porte.

* Se si utilizza una singola macchina virtuale e hello due elementi seguenti sono vere, non è necessario toocreate endpoint di macchina virtuale e porte hello tooopen in firewall hello hello VM non è necessaria.
  
  * Funzionalità di SQL Server toohello sulla hello VM non è connettersi in remoto. La definizione di una macchina virtuale di toohello connessione desktop remoto e accedere alle funzionalità di SQL Server hello in locale hello VM non è considerata una funzionalità di SQL Server toohello di connessione remota.
  * Non è parte dominio di hello VM tooan locale tramite la rete virtuale di Azure o un'altra soluzione di tunneling VPN.
* Se la macchina virtuale hello non è unita in join tooa dominio ma si desidera tooremotely connettersi toohello funzionalità di SQL Server nella macchina virtuale:
  
  * Aprire le porte hello in firewall hello hello macchina virtuale.
  * Creare l'endpoint della macchina virtuale per hello indicato porte (*).
* Caso di macchina virtuale hello tooa aggiunti a un dominio tramite un tunnel VPN, ad esempio le funzionalità di rete virtuale di Azure, gli endpoint di hello non sono necessari. Tuttavia è possibile aprire porte hello in firewall hello hello macchina virtuale.
  
  | Porta | Tipo | Descrizione |
  | --- | --- | --- |
  | **80** |TCP |Accesso remoto al server di report (*). |
  | **1433** |TCP |SQL Server Management Studio (*). |
  | **1434** |UDP |Browser SQL Server. È necessario quando hello VM tooa aggiunti a un dominio. |
  | **2382** |TCP |Browser SQL Server. |
  | **2383** |TCP |Istanza predefinita di SQL Server Analysis Services e cluster delle istanze denominate. |
  | **Definito dall'utente** |TCP |Creare un statico Analysis Services denominata porta dell'istanza per un numero di porta desiderato e quindi sbloccare il numero di porta hello firewall hello. |

Per ulteriori informazioni sulla creazione di endpoint, vedere l'esempio hello:

* Creare endpoint:[come configurare gli endpoint di tooSet tooa macchina virtuale](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* SQL Server: Vedere sezione "Completare la configurazione passaggi tooconnect toohello macchina virtuale mediante SQL Server Management Studio" hello [Provisioning di una macchina virtuale di SQL Server in Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Hello diagramma seguente illustra tooopen porte hello in hello toofeatures di accesso remoto tooallow firewall VM e ai componenti a hello macchina virtuale.

![tooopen porte per le applicazioni di Business Intelligence in macchine virtuali di Azure](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Risorse
* Esaminare i criteri di supporto hello per software server Microsoft usato nell'ambiente di macchina virtuale di Azure hello. Hello argomento viene riepilogato il supporto per funzionalità quali BitLocker, Clustering di Failover e bilanciamento carico di rete. [Supporto di software server Microsoft per le macchine virtuali Microsoft Azure](http://support.microsoft.com/kb/2721672).
* [Panoramica di SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Macchine virtuali](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Provisioning di una macchina virtuale di SQL Server in Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [Come tooAttach tooa un disco dati macchina virtuale](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [La migrazione di un tooSQL Database Server in una macchina virtuale di Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Determinare hello modalità Server di un'istanza di Analysis Services](https://msdn.microsoft.com/library/gg471594.aspx)
* [Modellazione multidimensionale (esercitazione AdventureWorks)](https://technet.microsoft.com/library/ms170208.aspx)
* [Centro di documentazione di Azure](https://azure.microsoft.com/documentation/)
* [Utilizzo di Power BI in un ambiente ibrido](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [È possibile inviare commenti e suggerimenti e informazioni di contatto tramite Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Contenuti della community
* [Gestione del database SQL di Azure con PowerShell](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)


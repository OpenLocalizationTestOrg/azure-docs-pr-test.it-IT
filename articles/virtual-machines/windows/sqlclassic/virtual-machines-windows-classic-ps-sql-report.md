---
title: "aaaUse PowerShell tooCreate una macchina virtuale con una modalità Server di Report nativa | Documenti Microsoft"
description: "In questo argomento vengono descritte e illustrate distribuzione hello e la configurazione di un server di report di SQL Server Reporting Services in modalità nativa in una macchina virtuale di Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Utilizzare PowerShell tooCreate un Azure VM con un Server in modalità nativa Report
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

In questo argomento vengono descritte e illustrate distribuzione hello e la configurazione di un server di report di SQL Server Reporting Services in modalità nativa in una macchina virtuale di Azure. Hello passaggi di questo utilizzo di documento, una combinazione di macchina virtuale di hello toocreate passaggi manuali e script di Windows PowerShell tooconfigure Reporting Services su hello macchina virtuale. script di configurazione Hello include l'apertura di una porta del firewall per HTTP o HTTPs.

> [!NOTE]
> Se non è necessario **HTTPS** nel server di report, hello **saltare il passaggio 2**.
> 
> Dopo aver creato hello VM nel passaggio 1, passare toohello sezione utilizza script tooconfigure hello server di rapporti e HTTP. Dopo l'esecuzione di script hello, il server di report di hello è toouse pronto.

## <a name="prerequisites-and-assumptions"></a>Prerequisiti e presupposti
* **Sottoscrizione di Azure**: verificare il numero di core disponibili nella sottoscrizione di Azure hello. Se si crea una dimensione della macchina virtuale consigliata hello **A3**, è necessario **4** core disponibili. Se si usa la dimensione di macchina virtuale **A2**, sono necessari **2** core disponibili.
  
  * limite di core hello tooverify della sottoscrizione, in hello portale di Azure classico, fare clic su impostazioni nel riquadro sinistro di hello e quindi fare clic su utilizzo nel menu superiore hello.
  * tooincrease hello quota core, contatta [supporto Azure](https://azure.microsoft.com/support/options/). Per informazioni sulle dimensioni delle macchine virtuali, vedere [Dimensioni delle macchine virtuali per Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Scripting di Windows PowerShell**: argomento hello si presuppone una conoscenza di base di Windows PowerShell. Per ulteriori informazioni sull'utilizzo di Windows PowerShell, vedere l'esempio hello:
  
  * [Avvio di Windows PowerShell in Windows Server](https://technet.microsoft.com/library/hh847814.aspx)
  * [Introduzione a Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>Passaggio 1: Eseguire il provisioning di una macchina virtuale di Azure
1. Sfoglia toohello portale di Azure classico.
2. Fare clic su **macchine virtuali** nel riquadro di sinistra hello.
   
    ![macchine virtuali di microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. Fare clic su **Nuovo**.
   
    ![pulsante nuovo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Fare clic su **Da raccolta**.
   
    ![nuova macchina virtuale dalla raccolta](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Fare clic su **SQL Server 2014 RTM Standard – Windows Server 2012 R2** e quindi fare clic su toocontinue freccia hello.
   
    ![Avanti](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Se è necessario funzionalità sottoscrizioni guidate dai dati di Reporting Services hello, scegliere **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**. Per ulteriori informazioni sulle edizioni di SQL Server e il supporto di funzionalità, vedere [funzionalità supportate dalle edizioni di SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. In hello **configurazione della macchina virtuale** pagina, modificare hello seguenti campi:
   
   * Se è presente più di **data di rilascio versione**, selezionare hello versione più recente.
   * **Nome della macchina virtuale**: nome del computer hello viene anche utilizzato nella pagina Configurazione successiva hello come hello predefinito nome DNS servizio Cloud. nome DNS Hello deve essere univoco tra hello servizio di Azure. Provare a configurare hello macchina virtuale con un nome di computer che descrive quale hello macchina virtuale viene utilizzata per. Ad esempio, ssrsnativecloud.
   * **Piano**: Standard.
   * **Dimensioni: A3** hello consiglia di dimensioni delle macchine Virtuali per carichi di lavoro di SQL Server. Se una macchina virtuale viene utilizzata solo come server di report, è sufficiente una dimensione A2, a meno che il server di report hello di cui si verifichi un elevato carico di lavoro. Per informazioni sui prezzi delle macchine virtuali, vedere [Macchine virtuali - Prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Nuovo nome utente**: nome hello specificato viene creato come amministratore in hello macchina virtuale.
   * **Nuova password** e **Conferma**. Questa password viene utilizzata per il nuovo account di amministratore hello e, è consigliabile che utilizzare una password complessa.
   * Fare clic su **Avanti**. ![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. Nella pagina successiva di hello, modificare hello seguenti campi:
   
   * **Servizio cloud**: selezionare **Crea un nuovo servizio cloud**.
   * **Nome DNS del servizio cloud**: si tratta di nome DNS pubblico hello di hello servizio Cloud associato hello macchina virtuale. nome predefinito Hello è hello digitato nel nome della macchina virtuale hello. Se nei passaggi successivi di argomento hello, si crea un certificato SSL attendibile e il nome DNS hello è utilizzato per il valore di hello di hello "**rilasciato a**" del certificato hello.
   * **Affinità di area/gruppo/rete virtuale**: scegliere gli utenti finali hello area più vicini tooyour.
   * **Account di archiviazione**: usare un account di archiviazione generato automaticamente.
   * **Set di disponibilità**: nessuno.
   * **Gli endpoint** Keep hello **Desktop remoto** e **PowerShell** endpoint e quindi aggiungere l'endpoint HTTP o HTTPS, a seconda dell'ambiente.
     
     * **HTTP**: hello predefinito porte pubbliche e private sono **80**. Si noti che se si utilizza una porta privata diversa dalla 80, modificare **$HTTPport = 80** nello script http hello.
     * **HTTPS**: hello predefinito porte pubbliche e private sono **443**. Una procedura consigliata è toochange porta privata di hello e configurare il firewall e hello report server toouse hello porta privata. Per ulteriori informazioni sugli endpoint, vedere [come configurare la comunicazione con una macchina virtuale tooSet](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Si noti che se si usa una porta diversa dalla 443, modificare il parametro hello **$HTTPsport = 443** in hello script HTTPS.
   * Fare clic su Avanti. ![Avanti](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. Hello ultima pagina della procedura guidata hello, mantenere l'impostazione predefinita di hello **installazione agente della macchina virtuale hello** selezionato. Hello passaggi in questo argomento non usano agente VM hello ma se si prevede di tookeep questa macchina virtuale, estensioni e agente VM hello consentirà tooenhance he CM.  Per ulteriori informazioni sull'agente VM hello, vedere [agente VM ed estensioni-parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). Uno dei hello estensioni predefinite installate e in esecuzione è l'estensione "BGINFO" hello che visualizza sul desktop VM hello, informazioni di sistema, ad esempio l'indirizzo IP interno e libera spazio su disco.
9. Fare clic su Completa. ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Hello **stato** di macchina virtuale viene visualizzato come hello **avvio in corso (Provisioning)** durante il processo di provisioning hello e viene visualizzato come **esecuzione** quando hello macchina virtuale è disponibile e pronta toouse.

## <a name="step-2-create-a-server-certificate"></a>Passaggio 2: Creare un certificato del server
> [!NOTE]
> Se non si usa HTTPS nel server di report hello, è possibile **saltare il passaggio 2** e passare la sezione toohello **usare HTTP e server di report di script tooconfigure hello**. Utilizzare hello HTTP script tooquickly configurare il server di report hello e report hello server sarà toouse pronto.

In ordine toouse HTTPS su hello VM, è necessario un certificato SSL attendibile. A seconda dello scenario, è possibile utilizzare uno dei seguenti due metodi hello:

* Un certificato SSL valido emesso da un'autorità di certificazione (CA) e ritenuto attendibile da Microsoft. i certificati radice della CA Hello sono necessari toobe distribuiti tramite hello programma Microsoft Root Certificate. Per ulteriori informazioni su questo programma, vedere [Windows e Windows Phone 8 SSL programma Root Certificate (autorità di certificazione membro)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) e [toohello introduzione programma Microsoft Root Certificate](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Un certificato autofirmato. I certificati autofirmati non sono consigliati per gli ambienti di produzione.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse un certificato creato da un'autorità di certificati attendibili (CA)
1. **Richiedere un certificato server per il sito Web di hello da un'autorità di certificazione**. 
   
    È possibile utilizzare Gestione guidata certificati Server Web hello entrambi toogenerate un file di richiesta di certificato (Certreq.txt) inviare tooa autorità di certificazione o toogenerate una richiesta per un'autorità di certificazione online. Ad esempio, Servizi certificati Microsoft in Windows Server 2012. A seconda di livello hello garanzia di identificazione offerto dal certificato del server, è alcuni mesi tooseveral giorni tooapprove autorità di certificazione hello la richiesta e inviare un file di certificato. 
   
    Per ulteriori informazioni sulla richiesta di un server di certificati, vedere l'esempio hello: 
   
   * Usare [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).
   * Sicurezza strumenti tooAdminister Windows Server 2012.
     
     [Strumenti di sicurezza tooAdminister Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Hello **rilasciato a** campo di hello attendibile il certificato SSL deve essere hello stesso come hello **nome DNS del servizio Cloud** usati per hello nuova macchina virtuale.

2. **Installare il certificato di server hello nel server Web hello**. in questo caso, server Web Hello è hello macchina virtuale che ospita il server di report di hello e sito Web di hello viene creato nei passaggi successivi quando si configura Reporting Services. Per ulteriori informazioni sull'installazione certificato server hello sul server Web hello utilizzando lo snap-in MMC certificato hello, vedere [installare un certificato Server](https://technet.microsoft.com/library/cc740068).
   
    Se si desidera toouse hello script incluso in questo argomento, il server di report tooconfigure hello, hello valore certificati hello **identificazione personale** è richiesto come parametro dello script hello. Nella sezione hello Avanti per informazioni dettagliate su come tooobtain hello identificazione personale del certificato hello.
3. Assegnare server di report toohello certificato server hello. assegnazione di Hello è completata nella sezione successiva di hello quando si configura il server di report hello.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>hello toouse certificato autofirmato macchine virtuali
Un certificato autofirmato è stato creato su hello VM quando è stato eseguito il provisioning hello macchina virtuale. certificato Hello è hello stesso nome come nome DNS VM hello. Errori di certificato tooavoid ordine, è necessario che il certificato hello è considerato attendibile in hello macchina virtuale stessa e anche da tutti gli utenti del sito hello.

1. CA radice hello tootrust del certificato hello in hello macchina virtuale locale, aggiungere hello certificato toohello **autorità di certificazione radice attendibili**. di seguito Hello è un riepilogo dei passaggi di hello necessari. Per informazioni dettagliate su come tootrust hello autorità di certificazione, vedere [installare un certificato Server](https://technet.microsoft.com/library/cc740068).
   
   1. Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti. A seconda della configurazione del browser, potrebbe essere richiesta toosave un file RDP per la connessione toohello macchina virtuale.
      
       ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Nome della macchina virtuale utilizza hello utente, nome utente e password configurati durante la creazione di hello macchina virtuale. 
      
       In hello seguente immagine, ad esempio, nome della macchina virtuale hello è **ssrsnativecloud** e nome utente hello è **testuser**.
      
       ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Eseguire mmc.exe. Per ulteriori informazioni, vedere [procedura: visualizzare certificati con hello Snap-in MMC](https://msdn.microsoft.com/library/ms788967.aspx).
   3. In un'applicazione console hello **File** menu, aggiungere hello **certificati** snap-in, selezionare **Account Computer** quando richiesto e quindi fare clic su **Avanti**.
   4. Selezionare **Computer locale** toomanage e quindi fare clic su **fine**.
   5. Fare clic su **Ok** e quindi espandere hello **certificati - personale** nodi e quindi fare clic su **certificati**. Hello certificato è citato dopo il nome DNS hello di hello VM e termina con **cloudapp.net**. Nome del certificato hello destro e fare clic su **copia**.
   6. Espandere hello **autorità di certificazione radice attendibili** nodo e quindi rapida **certificati** e quindi fare clic su **Incolla**.
   7. toovalidate, doppio clic sul nome certificato hello in **autorità di certificazione radice attendibili** e verificare che non siano presenti errori e viene visualizzato il certificato. Se si desidera toouse hello HTTPS script incluso in questo argomento, il server di report tooconfigure hello, hello valore certificati hello **identificazione personale** è richiesto come parametro dello script hello. **valore di identificazione personale hello tooget**, completare la procedura seguente hello. È inoltre disponibile un'identificazione digitale di PowerShell esempio tooretrieve hello nella sezione [utilizzano server di report di script tooconfigure hello e HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Fare doppio clic sul nome di hello del certificato di hello, ad esempio ssrsnativecloud.cloudapp.net.
      2. Fare clic su hello **dettagli** scheda.
      3. Fare clic su **Identificazione personale**. il valore di Hello dell'identificazione digitale hello viene visualizzato nel campo dei dettagli hello, ad esempio a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9C 2C fb 2f.
      4. Copiare l'identificazione personale hello e salvare il valore di hello per un momento successivo o modificare script hello adesso.
      5. (*) Prima di eseguire script hello, rimuovere hello gli spazi tra coppie di hello di valori. Ad esempio identificazione personale hello annotata in precedenza sarebbe a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.
      6. Assegnare server di report toohello certificato server hello. assegnazione di Hello è completata nella sezione successiva di hello quando si configura il server di report hello.

Se si utilizza un certificato SSL autofirmato, nome hello hello certificato corrisponde già a hostname hello di hello macchina virtuale. Pertanto, hello DNS della macchina hello è già registrato globalmente e sono accessibili da qualsiasi client.

## <a name="step-3-configure-hello-report-server"></a>Passaggio 3: Configurare hello Server di Report
In questa sezione illustra la configurazione hello VM come un server di report in modalità nativa di Reporting Services. È possibile utilizzare uno dei seguenti server di report di metodi tooconfigure hello hello:

* Utilizzare server di report di hello script tooconfigure hello
* Utilizzare Gestione configurazione tooConfigure hello Server di Report.

Per istruzioni più dettagliate, vedere la sezione hello [toohello connessione macchina virtuale e avviare Gestione configurazione Reporting Services di hello](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Nota sull'autenticazione:** l'autenticazione di Windows hello metodo di autenticazione consigliato ed è l'autenticazione di Reporting Services predefinito hello. Solo gli utenti che sono configurati su hello VM possono accedere a Reporting Services e assegnato tooReporting ruoli di servizi.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Utilizzare server di report di script tooconfigure hello e HTTP
toouse hello Windows PowerShell script tooconfigure hello server di report, hello completo alla procedura seguente. configurazione di Hello include HTTP, HTTPS non:

1. Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti. A seconda della configurazione del browser, potrebbe essere richiesta toosave un file RDP per la connessione toohello macchina virtuale.
   
    ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Nome della macchina virtuale utilizza hello utente, nome utente e password configurati durante la creazione di hello macchina virtuale. 
   
    In hello seguente immagine, ad esempio, nome della macchina virtuale hello è **ssrsnativecloud** e nome utente hello è **testuser**.
   
    ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. In hello macchina virtuale, aprire **Windows PowerShell ISE** con privilegi amministrativi. Hello PowerShell ISE è installato per impostazione predefinita in Windows server 2012. È consigliabile che usare hello ISE anziché una finestra standard di Windows PowerShell, che può incollare script hello in hello ISE, modificare script hello e quindi eseguire script hello.
3. In Windows PowerShell ISE, fare clic su hello **vista** menu e quindi fare clic su **Mostra riquadro di Script**.
4. Copiare lo script seguente hello e incollare hello script nel riquadro di script di Windows PowerShell ISE hello.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Se hello VM è stato creato con una porta HTTP diversa dalla 80, modificare il parametro hello $HTTPport = 80.
6. script Hello è attualmente configurato per Reporting Services. Se si desidera script hello toorun per Reporting Services, modificare lo spazio dei nomi di hello percorso toohello parte versione hello troppo "v11" nell'istruzione hello Get-WmiObject.
7. Eseguire script hello.

**Convalida**: tooverify che funzionalità di server di report di base hello sia operativa, vedere hello [configurazione hello verificare](#verify-the-configuration) sezione più avanti in questo argomento.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Utilizzare server di report di script tooconfigure hello e HTTPS
toouse Windows PowerShell tooconfigure hello server di report, hello completo alla procedura seguente. configurazione di Hello include HTTPS, ma non HTTP.

1. Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti. A seconda della configurazione del browser, potrebbe essere richiesta toosave un file RDP per la connessione toohello macchina virtuale.
   
    ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Nome della macchina virtuale utilizza hello utente, nome utente e password configurati durante la creazione di hello macchina virtuale. 
   
    In hello seguente immagine, ad esempio, nome della macchina virtuale hello è **ssrsnativecloud** e nome utente hello è **testuser**.
   
    ![account di accesso con il nome della macchina virtuale](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. In hello macchina virtuale, aprire **Windows PowerShell ISE** con privilegi amministrativi. Hello PowerShell ISE è installato per impostazione predefinita in Windows server 2012. È consigliabile che usare hello ISE anziché una finestra standard di Windows PowerShell, che può incollare script hello in hello ISE, modificare script hello e quindi eseguire script hello.
3. tooenable l'esecuzione di script, eseguire il comando di Windows PowerShell seguente hello:
   
        Set-ExecutionPolicy RemoteSigned
   
    È quindi possibile eseguire i seguenti criteri hello tooverify hello:
   
        Get-ExecutionPolicy
4. In **Windows PowerShell ISE**, fare clic su hello **vista** menu e quindi fare clic su **Mostra riquadro di Script**.
5. Copiare hello seguente script e incollarlo nel riquadro di script di Windows PowerShell ISE hello.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Modificare hello **$certificatehash** parametro nello script hello:
   
   * Si tratta di un parametro **obbligatorio** . Se non è stato salvato il valore di certificato hello nei passaggi precedenti hello, utilizzare uno dei seguenti valore hash del certificato hello toocopy metodi di identificazione personale certificati hello hello.:
     
       Nella macchina virtuale hello, aprire Windows PowerShell ISE ed eseguire hello comando seguente:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       output di Hello avrà un aspetto simile toohello seguente. Se lo script di hello restituisce una riga vuota, hello macchina virtuale non dispone di un certificato configurato, ad esempio, vedere la sezione hello [toouse hello certificato autofirmato macchine virtuali](#to-use-the-virtual-machines-self-signed-certificate).
     
     OPPURE
   * Hello macchina virtuale eseguire mmc.exe e quindi aggiungere hello **certificati** snap-in.
   * In hello **autorità di certificazione radice attendibili** nodo fare doppio clic sul nome del certificato. Se si utilizza hello autofirmato di hello macchina virtuale, il certificato di hello denominato in base al nome DNS hello di hello macchina virtuale e termina con **cloudapp.net**.
   * Fare clic su hello **dettagli** scheda.
   * Fare clic su **Identificazione personale**. il valore di Hello dell'identificazione digitale hello viene visualizzato nel campo dei dettagli hello, ad esempio af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48
   * **Prima di eseguire script hello**, rimuovere gli spazi tra coppie di hello di valori hello. Ad esempio, af1160b64b288d890a8212ff6ba9c3664f319048
7. Modificare hello **$httpsport** parametro: 
   
   * Se si utilizza la porta 443 per endpoint HTTPS hello, quindi non è necessario tooupdate questo parametro nello script hello. In caso contrario, utilizzare il valore di porta hello selezionato durante la configurazione di endpoint privato HTTPS hello in hello macchina virtuale.
8. Modificare hello **$DNSName** parametro: 
   
   * script Hello è configurato per un certificato con caratteri jolly $DNSName = "+". Se si esegue l'operazione non tooconfigure desiderata per un binding al certificato con caratteri jolly, commento $DNSName = "+"e abilitare la seguente riga hello completo $DNSNAme il riferimento, # # $DNSName="$server.cloudapp.net hello".
     
       Modificare il valore di hello $DNSName se non si desidera il nome DNS della macchina virtuale hello di toouse per Reporting Services. Se si usa il parametro hello, certificato hello è necessario utilizzare anche il nome e si registra il nome di hello a livello globale in un server DNS.
9. script Hello è attualmente configurato per Reporting Services. Se si desidera script hello toorun per Reporting Services, modificare lo spazio dei nomi di hello percorso toohello parte versione hello troppo "v11" nell'istruzione hello Get-WmiObject.
10. Eseguire script hello.

**Convalida**: tooverify che funzionalità di server di report di base hello sia operativa, vedere hello [configurazione hello verificare](#verify-the-connection) sezione più avanti in questo argomento. binding al certificato hello tooverify aprire un prompt dei comandi con privilegi amministrativi e quindi eseguire hello comando seguente:

    netsh http show sslcert

il risultato di Hello includerà seguente hello:

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Utilizzare Gestione configurazione tooConfigure hello Server di Report
Se non si desidera toorun script di PowerShell di hello tooconfigure server di report di hello, seguire i passaggi di hello in questa sezione toouse hello Reporting Services in modalità nativa tooconfigure hello report server di configuration manager.

1. Dal portale di Azure classico hello, selezionare hello macchina virtuale e fare clic su Connetti. Usa il nome utente hello e la password configurati durante la creazione di hello macchina virtuale.
   
    ![connettere la macchina virtuale di tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Eseguire Windows update e installare gli aggiornamenti toohello macchina virtuale. Se è necessario un riavvio della macchina virtuale hello, riavviare hello macchina virtuale e riconnettersi toohello macchina virtuale dal portale di Azure classico hello.
3. Dal menu di avvio hello in hello macchina virtuale, digitare **Reporting Services** e aprire **Gestione configurazione Reporting Services**.
4. Lasciare i valori predefiniti di hello per **nome Server** e **istanza Server di Report**. Fare clic su **Connetti**.
5. Nel riquadro di sinistra hello, fare clic su **URL servizio Web**.
6. Per impostazione predefinita, Reporting Services è configurato per la porta HTTP 80 con IP "Tutti assegnati". tooadd HTTPS:
   
   1. In **certificato SSL**: hello selezionare certificato toouse, ad esempio [nome macchina virtuale]. cloudapp.net. Se non sono elencati certificati, vedere la sezione hello **passaggio 2: creare un certificato Server** per informazioni su come tooinstall e attendibilità hello certificato su hello macchina virtuale.
   2. In **Porta SSL**scegliere 443. Se è configurato l'endpoint privato HTTPS hello in hello macchina virtuale con una porta privata diversa, utilizzare quel valore.
   3. Fare clic su **applica** e attendere toocomplete operazione hello.
7. Nel riquadro di sinistra hello, fare clic su **Database**.
   
   1. Fare clic su **Modifica database**.
   2. Fare clic su **Crea un nuovo database del server di report** e quindi su **Avanti**.
   3. Lasciare l'impostazione predefinita hello **nome Server**: hello VM assegnare il nome e valore predefinito di hello **tipo di autenticazione** come **utente corrente** – **lasicurezzaintegrata**. Fare clic su **Avanti**.
   4. Lasciare l'impostazione predefinita hello **nome del Database** come **ReportServer** e fare clic su **Avanti**.
   5. Lasciare l'impostazione predefinita hello **tipo di autenticazione** come **credenziali del servizio** e fare clic su **Avanti**.
   6. Fare clic su **Avanti** su hello **riepilogo** pagina.
   7. Una volta completata la configurazione hello, fare clic su **fine**.
8. Nel riquadro di sinistra hello, fare clic su **URL gestione Report**. Lasciare l'impostazione predefinita hello **Directory virtuale** come **report** e fare clic su **applica**.
9. Fare clic su **uscita** tooclose hello Gestione configurazione Reporting Services.

## <a name="step-4-open-windows-firewall-port"></a>Passaggio 4: Aprire la porta di Windows Firewall
> [!NOTE]
> Se si usa uno hello script tooconfigure hello server di report, è possibile ignorare questa sezione. una porta del firewall hello tooopen passaggio è incluso uno script di Hello. valore predefinito di Hello è la porta 80 per HTTP e la porta 443 per HTTPS.
> 
> 

tooconnect in modalità remota tooReport Manager o hello Report Server nella macchina virtuale hello, un Endpoint TCP è obbligatorio in hello macchina virtuale. È necessario tooopen hello stessa porta nel firewall della macchina virtuale di hello. Hello endpoint è stato creato quando è stato eseguito il provisioning hello macchina virtuale.

In questa sezione fornisce informazioni di base in modo tooopen hello porta del firewall. Per altre informazioni, vedere [Configurare un firewall per l'accesso al server di report](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Se si utilizza server di report hello tooconfigure hello script, è possibile ignorare questa sezione. una porta del firewall hello tooopen passaggio è incluso uno script di Hello.
> 
> 

Se è configurata una porta privata per HTTPS diversa dalla 443, modificare hello lo script seguente in modo appropriato. porta tooopen **443** su hello Windows Firewall, completare i seguenti hello:

1. Aprire una finestra di Windows PowerShell con privilegi amministrativi.
2. Se si utilizza una porta diversa dalla 443 durante la configurazione di endpoint HTTPS hello in hello macchina virtuale, aggiornare la porta di hello in hello comando seguente e quindi eseguire il comando di hello:
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Al termine del comando di hello, **Ok** viene visualizzato nel prompt dei comandi di hello.

tooverify che porta hello è aperto, aprire una finestra di Windows PowerShell e hello esecuzione comando seguente:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Verificare la configurazione di hello
tooverify che la funzionalità server di report di base hello ora sia in esecuzione, aprire il browser con privilegi amministrativi e quindi Sfoglia toohello seguenti report di gestione report server URL:

* In hello VM, visitare toohello URL server di report:
  
        http://localhost/reportserver
* In hello VM, visitare toohello URL di gestione report:
  
        http://localhost/Reports
* Dal computer locale, passare toohello **remoto** Gestione report in VM hello. Aggiornare il nome DNS hello in hello seguente esempio come appropriato. Quando viene richiesto di immettere una password, utilizzare le credenziali di amministratore hello creato quando è stato eseguito il provisioning hello VM. nome utente di Hello è hello [dominio]\[nome utente] formato, dove dominio hello è hello VM nome, ad esempio ssrsnativecloud\testuser. Se non si utilizza HTTP**S**, rimuovere hello **s** nell'URL hello. Nella sezione hello Avanti per informazioni sulla creazione di altri utenti nella macchina virtuale.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* Dal computer locale, passare toohello URL del server di report remoto. Aggiornare il nome DNS hello in hello seguente esempio come appropriato. Se non si utilizza HTTPS, è possibile rimuovere hello s hello URL.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Creare utenti e assegnare ruoli
Dopo la configurazione e la verifica hello server di report, un'attività amministrativa comune è toocreate uno o più utenti e assegnare i ruoli di servizi tooReporting di utenti. Per ulteriori informazioni, vedere l'esempio hello:

* [Creare un account utente locale](https://technet.microsoft.com/library/cc770642.aspx)
* [Concedere l'accesso utente tooa il Server di Report (gestione Report)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Creare e gestire le assegnazioni di ruoli](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate e pubblicare report toohello macchina virtuale di Azure
Hello nella tabella seguente vengono riepilogati alcuni dei report esistenti hello opzioni toopublish disponibile da un server di report locale computer toohello ospitato in hello macchina virtuale di Microsoft Azure:

* **Lo script RS.exe**: utilizzare RS.exe script toocopy gli elementi del report da e tooyour server di report esistente macchina virtuale di Microsoft Azure. Per ulteriori informazioni, vedere la sezione hello "modalità nativa tooNative modalità-macchina virtuale di Microsoft Azure" in [Sample Reporting Services rs.exe Script tooMigrate contenuto tra server di Report](https://msdn.microsoft.com/library/dn531017.aspx).
* **Generatore report**: macchina virtuale di hello inclusa hello-versione ClickOnce di Generatore Report di Microsoft SQL Server. hello Generatore Report di toostart prima volta sulla macchina virtuale hello:
  
  1. Avviare il browser con privilegi amministrativi.
  2. Gestione tooreport sulla macchina virtuale hello e fare clic su **Generatore Report** nella barra multifunzione hello.
     
     Per altre informazioni, vedere [Installazione, disinstallazione e supporto di Generatore report](https://technet.microsoft.com/library/dd207038.aspx).
* **SQL Server Data Tools: Macchina virtuale**: se hello VM è stato creato con SQL Server 2012 e SQL Server Data Tools sia installato nella macchina virtuale hello e può essere utilizzato toocreate **progetti Server di Report** e report sulla hello virtuale macchina. SQL Server Data Tools è possibile pubblicare server di report di toohello hello report sulla macchina virtuale hello.
  
    Se è stato creato con SQL server 2014 hello VM, è possibile installare SQL Server Data Tools - BI per visual Studio. Per ulteriori informazioni, vedere l'esempio hello:
  
  * [Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools e SQL Server Business Intelligence (SSDT-BI)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools - Remoto**: nel computer locale creare un progetto di Reporting Services in SQL Server Data Tools contenente i report di Reporting Services. Configurare l'URL del servizio web tooconnect toohello hello progetto.
  
    ![proprietà del progetto ssdt per un progetto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Utilizzare script**: utilizzare contenuto del server di report toocopy di script. Per ulteriori informazioni, vedere [Sample Reporting Services rs.exe Script tooMigrate contenuto tra server di Report](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Ridurre i costi se non si utilizza hello VM
> [!NOTE]
> toominimize addebiti per le macchine virtuali di Azure quando non è in uso, è stato chiuso hello macchina virtuale dal portale di Azure classico hello. Se si utilizzano opzioni di risparmio energia di Windows hello all'interno di un tooshut VM verso il basso hello VM, viene comunque addebitato hello stesso importo per hello macchina virtuale. gli addebiti tooreduce, è necessario tooshut hello VM nel portale di Azure classico hello verso il basso. Se non è più necessario hello VM, ricordare di hello toodelete VM e hello spese di archiviazione tooavoid file VHD associato. Per ulteriori informazioni, vedere la sezione di hello domande frequenti al [dettagli prezzi-macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Altre informazioni
### <a name="resources"></a>Risorse
* Per contenuti analoghi relativi tooa distribuzione a server singolo di SQL Server Business Intelligence e SharePoint 2013, vedere [tooCreate utilizzare Windows PowerShell una macchina virtuale Azure con SQL Server BI e SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* Per simile tooa correlati contenuto distribuzione multiserver di SQL Server Business Intelligence e SharePoint 2013, vedere [distribuire SQL Server Business Intelligence in macchine virtuali di Azure](https://msdn.microsoft.com/library/dn321998.aspx).
* Per informazioni generali toodeployments correlati di SQL Server Business Intelligence in macchine virtuali di Azure, vedere [SQL Server Business Intelligence in macchine virtuali di Azure](virtual-machines-windows-classic-ps-sql-bi.md).
* Per ulteriori informazioni sul costo hello addebiti di calcolo di Azure, vedere scheda macchine virtuali hello del [calcolatore dei costi Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Contenuti della community
* Per istruzioni dettagliate su come toocreate una modalità nativa di Reporting Services server di report senza usare lo script, vedere [di Hosting SQL Reporting Services nella macchina virtuale Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Risorse tooother collegamenti per SQL Server in macchine virtuali di Azure
[Panoramica di SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)


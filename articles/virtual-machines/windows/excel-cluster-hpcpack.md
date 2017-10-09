---
title: aaaHPC Pack del cluster per Excel e SOA | Documenti Microsoft
description: Introduzione all'esecuzione di carichi di lavoro Excel e SOA su larga scala in un cluster HPC Pack in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Introduzione all'esecuzione di carichi di lavoro Excel e SOA in un cluster HPC Pack in Azure
Questo articolo illustra come cluster toodeploy Microsoft HPC Pack 2012 R2 in macchine virtuali di Azure utilizzando un modello di avvio rapido di Azure o, facoltativamente, uno script di distribuzione di Azure PowerShell. cluster Hello utilizza toorun progettate immagini di macchina virtuale di Azure Marketplace Microsoft Excel o i carichi di lavoro di architettura orientata ai servizi (SOA) con HPC Pack. È possibile utilizzare hello toorun di cluster HPC di Excel e di servizi SOA da un computer client locale. servizi di HPC Excel Hello includono offload cartella di lavoro di Excel e funzioni definite dall'utente di Excel o funzioni definite dall'utente.

> [!IMPORTANT] 
> Questo articolo si basa su funzionalità, modelli e script per HPC Pack 2012 R2. Questo scenario non è attualmente supportato in HPC Pack 2016.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

In generale, hello diagramma seguente mostra cluster HPC Pack hello create.

![Cluster HPC con nodi che eseguono carichi di lavoro di Excel][scenario]

## <a name="prerequisites"></a>Prerequisiti
* **Computer client** -è necessario un cluster di toohello processi basati su Windows client computer toosubmit esempio SOA ed Excel. È necessario anche un hello toorun computer di Windows Azure PowerShell script di distribuzione di cluster (se si sceglie il metodo di distribuzione).
* **Sottoscrizione di Azure** : se non è disponibile una sottoscrizione di Azure, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi minuti.
* **Quota di core** -potrebbe essere necessario quota hello tooincrease di core, soprattutto se si distribuiscono più nodi del cluster con dimensioni delle macchine Virtuali multicore. Se si utilizza un modello di avvio rapido di Azure, la quota di core hello in Gestione risorse è per ogni area di Azure. In tal caso, si potrebbe essere necessario quota hello tooincrease in un'area specifica. Vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../../azure-subscription-service-limits.md). una quota, tooincrease [aprire una richiesta di supporto clienti online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) senza alcun costo.
* **Licenza di Microsoft Office** : se si distribuiscono nodi di calcolo usando un'immagine di VM di HPC Pack 2012 R2 di Marketplace con Microsoft Excel, viene installata una versione di valutazione di Microsoft Excel Professional Plus 2013 di 30 giorni. Dopo il periodo di valutazione di hello, è necessario tooprovide uno valido Microsoft Office licenza tooactivate Excel toocontinue toorun carichi di lavoro. Vedere [Attivazione di Excel](#excel-activation) più avanti in questo articolo. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Passaggio 1. Configurazione di un cluster HPC Pack in Azure
Vengono illustrati due opzioni tooset di cluster HPC Pack 2012 R2 hello: prima, utilizzando un modello di avvio rapido di Azure e hello portale di Azure quindi, usando uno script di distribuzione di Azure PowerShell.

### <a name="option-1-use-a-quickstart-template"></a>Opzione 1. Uso di un modello di Guida introduttiva
Utilizzare un tooquickly modello di avvio rapido di Azure di distribuire un cluster HPC Pack nel portale di Azure hello. Quando si apre il modello di hello nel portale di hello, si ottiene un'interfaccia utente semplice in cui è immettere impostazioni hello per il cluster. Ecco i passaggi di hello. 

> [!TIP]
> È possibile usare un [modello di Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) che crea un cluster simile, specifico per i carichi di lavoro di Excel. Hello procedura leggermente diversa dal successivo hello.
> 
> 

1. Visitare hello [pagina modello di creazione del Cluster HPC in GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Se si desidera, è possibile esaminare informazioni sul modello hello e il codice sorgente hello.
2. Fare clic su **distribuire tooAzure** toostart una distribuzione con il modello di hello in hello portale di Azure.
   
   ![Distribuire tooAzure modello][github]
3. Nel portale di hello, seguire questi parametri di hello tooenter passaggi per il modello di cluster HPC hello.
   
   a. In hello **parametri** pagina, immettere o modificare i valori per parametri modello hello. (Fare clic su hello icona Avanti tooeach impostazione per le informazioni della Guida). Nella seguente schermata hello vengono visualizzati i valori di esempio. Questo esempio viene creato un cluster denominato *hpc01* in hello *hpc.local* dominio costituito da un nodo head e 2 nodi di calcolo. nodi di calcolo Hello vengono creati da un'immagine di macchina virtuale di HPC Pack che include Microsoft Excel.
   
   ![Immettere i parametri][parameters-new-portal]
   
   > [!NOTE]
   > nodo head di Hello macchina virtuale viene creato automaticamente da hello [più recente immagine del Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) di HPC Pack 2012 R2 in Windows Server 2012 R2. Attualmente l'immagine di hello è basato su HPC Pack 2012 R2 Update 3.
   > 
   > Macchine virtuali del nodo calcolo vengono create dall'immagine più recente di hello della famiglia di nodo di calcolo hello selezionato. Seleziona hello **ComputeNodeWithExcel** opzione hello più recente HPC Pack calcolo nodo immagine che include una versione di valutazione di Microsoft Excel Professional Plus 2013. toodeploy un cluster per le sessioni SOA generale o per l'offload di UDF di Excel, scegliere hello **ComputeNode** opzione (senza Excel installato).
   > 
   > 
   
   b. Scegliere la sottoscrizione hello.
   
   c. Creare un gruppo di risorse cluster hello, ad esempio *hpc01RG*.
   
   d. Scegliere un percorso per il gruppo di risorse hello, ad esempio Stati Uniti centrali.
   
   e. In hello **legali** pagina, esaminare le condizioni di hello. Se si accettano le condizioni, fare clic su **Acquista**. Quindi, dopo aver impostato i valori hello per modello di hello, fare clic su **crea**.
4. Quando viene completata la distribuzione di hello (in genere richiede circa 30 minuti), esportare file del certificato hello cluster dal nodo head del cluster hello. Successivamente, importare il certificato pubblico hello client tooprovide hello sul lato server dell'autenticazione del computer per l'associazione HTTP protetta.
   
   a. Nel portale di Azure hello, andare toohello dashboard nodo head hello selezionare e fare clic su **Connetti** nella parte superiore di hello di hello pagina tooconnect tramite Desktop remoto.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Usare le procedure standard in Gestione certificati tooexport hello nodo head certificato (che si trova in Cert: \LocalMachine\My) senza chiave privata hello. In questo esempio esportare *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Esportare il certificato di hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Opzione 2. Utilizzare script di distribuzione IaaS di HPC Pack hello
script di distribuzione IaaS di HPC Pack Hello fornisce un altro modo versatile toodeploy un cluster HPC Pack. Viene creato un cluster nel modello di distribuzione classica hello, mentre il modello di hello modello di distribuzione Azure Resource Manager hello. Inoltre, script hello è compatibile con una sottoscrizione in hello Azure globale o il servizio Cina di Azure.

**Ulteriori prerequisiti**

* **Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.
* **Script di distribuzione IaaS di HPC Pack** : scaricare e decomprimere hello versione dello script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Controllare la versione di hello dello script di hello eseguendo `New-HPCIaaSCluster.ps1 –Version`. In questo articolo si basa sulla versione 4.5.0 o successiva di script hello.

**Creare il file di configurazione di hello**

 script di distribuzione IaaS di HPC Pack Hello viene utilizzato un file di configurazione XML come input che descrive l'infrastruttura di hello del cluster HPC hello. toodeploy creati dall'immagine di nodo di calcolo hello che include Microsoft Excel, i nodi di calcolo di un cluster costituito da un nodo head e 18 sostituire i valori per l'ambiente in hello seguenti il file di configurazione di esempio. Per ulteriori informazioni sul file di configurazione di hello, vedere il file Manual.rtf hello nella cartella script hello e [creare un cluster HPC con lo script di distribuzione IaaS di HPC Pack hello](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Note sul file di configurazione hello**

* Hello **VMName** del nodo head hello **deve** essere hello stesso come hello **ServiceName**, o i processi SOA di esito negativo toorun.
* Assicurarsi di specificare **EnableWebPortal** in modo che hello certificato del nodo head viene generato ed esportato.
* file Hello specifica uno script di PowerShell di post-configurazione PostConfig.ps1 in esecuzione sul nodo head hello. Hello lo script di esempio seguente configura stringa di connessione di archiviazione di Azure hello, ruolo del nodo calcolo hello viene rimosso dal nodo head di hello e visualizza tutti i nodi in linea quando vengono distribuiti. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Eseguire script hello**

1. Aprire la console di PowerShell hello in computer client hello come amministratore.
2. Modifica directory toohello cartella di script (E:\IaaSClusterScript in questo esempio).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. toodeploy hello HPC Pack cluster esegue hello comando seguente. Si presuppone che si trova il file di configurazione hello in E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

script di distribuzione di HPC Pack Hello viene eseguito per un certo tempo. Uno script di hello cosa esegue è tooexport e scaricare il certificato di cluster hello e salvarla nella cartella documenti dell'utente corrente hello hello client computer. script di Hello genera di seguito toohello simile messaggio. In un passaggio seguente, importare certificato hello nell'archivio certificati appropriato hello.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Passaggio 2. Offload di cartelle di lavoro di Excel ed esecuzione di funzioni definite dall'utente da un client locale
### <a name="excel-activation"></a>Attivazione di Excel
Quando si usa l'immagine VM ComputeNodeWithExcel hello per carichi di lavoro di produzione, è necessario un valido Microsoft Office licenza chiave tooactivate Excel sui nodi di calcolo hello tooprovide. In caso contrario, la versione di valutazione hello di Excel scade dopo 30 giorni e in esecuzione le cartelle di lavoro di Excel avrà esito negativo con hello COMException (0x800AC472). 

È possibile rearm Excel per altri 30 giorni del periodo di valutazione: accedere al nodo head toohello e clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` su Excel tutti i nodi di calcolo di tramite HPC Cluster Manager. La riattivazione del periodo di prova può avvenire al massimo due volte. Successivamente occorre fornire un codice di licenza di Office valido.

Hello Office Professional Plus 2013 installato nell'immagine di macchina virtuale hello è un'edizione con contratti multilicenza con una chiave (Multilicenza generico). Per attivarla, è possibile usare il Servizio di gestione delle chiavi, l'attivazione basata su Active Directory o il codice ad attivazione multipla. 

    * toouse AD/KMS-BA, utilizzare un server di gestione delle CHIAVI esistente o configurarne uno nuovo con hello pacchetto licenze Volume di Microsoft Office 2013. (Se si desidera, è possibile configurare il server di hello nel nodo head di hello.) Quindi, attivare hello codice Product key host tramite hello Internet o telefono. Quindi clusrun `ospp.vbs` tooset hello porta e il server di gestione delle CHIAVI e attivare di Office su tutti i nodi di calcolo Excel hello. 

    * toouse MAK, clusrun prima `ospp.vbs` tooinput hello chiave e quindi attivare tutti i nodi di calcolo Excel hello tramite hello Internet o telefono. 

> [!NOTE]
> Con questa immagine di VM non è possibile usare codici Product Key di Office Professional Plus 2013. Se si dispone di codici e supporti di installazione validi per edizioni di Office o Excel diverse dall'edizione multilicenza di Office Professional Plus 2013, è possibile usarli in alternativa. Prima disinstallare questa edizione di volume e installare l'edizione hello in uso. Hello reinstallato Excel del nodo di calcolo può essere acquisito in un toouse immagine di macchina virtuale personalizzata in una distribuzione su larga scala.
> 
> 

### <a name="offload-excel-workbooks"></a>Offload di cartelle di lavoro di Excel
Seguire questi toooffload passaggi una cartella di lavoro di Excel in modo che venga eseguito nel cluster HPC Pack hello in Azure. toodo, è necessario disporre di Excel 2010 o 2013 già installato nel computer client hello.

1. Utilizzare una delle opzioni di hello nel passaggio 1 toodeploy un cluster HPC Pack con Excel hello immagine del nodo di calcolo. Ottenere hello cluster certificato (. cer) e nome utente del cluster e la password.
2. Computer client hello importare certificati cluster hello in Cert: \CurrentUser\Root.
3. Verificare che Excel sia installato. Creare un file Excel.exe. config con hello seguente contenuto hello stessa cartella Excel.exe nel computer client hello. Questo passaggio garantisce che hello del componente aggiuntivo di HPC Pack 2012 R2 Excel COM viene caricato correttamente.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Configurare il cluster di HPC Pack toohello hello client toosubmit processi. Un'opzione è hello toodownload completo [HPC Pack 2012 R2 Update 3 installazione](http://www.microsoft.com/download/details.aspx?id=49922) e installare il client di HPC Pack hello. In alternativa, scaricare e installare hello [utilità client di HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) e hello appropriato Visual C++ 2010 redistributable per il computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. In questo esempio viene usata una cartella di lavoro di Excel di esempio denominata ConvertiblePricing_Complete.xlsb. È possibile scaricarlo [qui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Copiare hello Excel cartella di lavoro tooa cartella di lavoro, ad esempio D:\Excel\Run.
7. Aprire una cartella di lavoro di Excel hello. In hello **sviluppare** della barra multifunzione, fare clic su **componenti aggiuntivi COM** e verificare che hello HPC Pack Excel componente aggiuntivo viene caricato correttamente.
   
   ![Componente aggiuntivo Excel per HPC Pack][addin]
8. Le righe di commento macro VBA modifica hello HPCControlMacros in Excel modificando hello come illustrato nell'hello lo script seguente. Sostituire con i valori appropriati per il proprio ambiente.
   
   ![Macro Excel per HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Copiare directory upload tooan hello Excel cartella di lavoro, ad esempio D:\Excel\Upload. La directory specificata nella costante HPC_DependsFiles hello nella macro VBA hello.
10. cartella di lavoro hello toorun in cluster hello in Azure, fare clic su hello **Cluster** pulsante foglio di lavoro hello.

### <a name="run-excel-udfs"></a>Esecuzione delle funzioni definite dall'utente di Excel
toorun Excel funzioni definite dall'utente, seguire passaggi precedenti, hello tooset 1-3 backup computer client hello. Per funzioni definite dall'utente di Excel, non è necessaria un'applicazione Excel toohave hello installata sui nodi di calcolo. Pertanto, quando si crea il cluster di nodi di calcolo, è possibile scegliere un'immagine del nodo di calcolo normale anziché hello calcolo immagine del nodo con Excel.

> [!NOTE]
> È presente un limite di 34 caratteri in hello Excel 2010 e 2013 cluster connettore finestra di dialogo. Utilizzare questa finestra di dialogo casella toospecify hello cluster che esegue hello funzioni definite dall'utente. Se il nome completo del cluster hello è più lungo (ad esempio, hpcexcelhn01.southeastasia.cloudapp.azure.com), non è possibile inserirlo nella finestra di dialogo hello. Hello soluzione alternativa è tooset una variabile a livello di computer, ad esempio *CCP_IAASHN* con valore hello hello lungo nome di cluster. Quindi, immettere *CCP_IAASHN %* nella finestra di dialogo hello come nome del nodo head del cluster hello. 
> 
> 

Dopo la distribuzione di cluster hello è completata, continuare con hello seguendo i passaggi toorun incorporato esempio UDF di Excel. Per UDF di Excel personalizzati, vedere questi [risorse](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL e distribuirli nei cluster IaaS hello.

1. Aprire una nuova cartella di lavoro di Excel. In hello **sviluppare** della barra multifunzione, fare clic su **Add-Ins**. Quindi, nella finestra di dialogo hello, fare clic su **Sfoglia**, passare toohello %CCP_HOME%Bin\XLL32 cartella e selezionare l'esempio hello ClusterUDF32.xll. Se hello ClusterUDF32 non esiste nel computer client hello, copiarlo nella cartella %CCP_HOME%Bin\XLL32 hello nel nodo head hello.
   
   ![Selezionare hello funzione definita dall'utente][udf]
2. Fare clic su **File** > **Opzioni** > **Avanzate**. In **formule**, controllare **consentono di un cluster di calcolo definito dall'utente XLL funzioni toorun**. Quindi fare clic su **opzioni** e immettere il nome completo del cluster hello in **nome nodo head del Cluster**. (Come indicato in precedenza questa casella di input è limitato too34 caratteri, in modo da un nome lungo cluster potrebbe non essere adatto. Per i nomi di cluster lunghi, è possibile usare una variabile a livello di computer).
   
   ![Configurare hello funzione definita dall'utente][options]
3. hello toorun calcolo funzione definita dall'utente nel cluster hello, fare clic su una cella con il valore =XllGetComputerNameC() hello e premere INVIO. funzione Hello recupera semplicemente il nome di hello del nodo di calcolo hello in cui hello funzione definita dall'utente in esecuzione. Per eseguire prima di hello, una finestra di dialogo credenziali richiede hello nome utente e password tooconnect toohello cluster IaaS.
   
   ![Eseguire una UDF][run]
   
   Quando sono presenti molti toocalculate celle, premere Maiusc-Alt-Ctrl + calcolo di hello toorun F9 su tutte le celle.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Passaggio 3. Esecuzione di un carico di lavoro SOA da un client locale
applicazioni SOA generali toorun cluster IaaS di HPC Pack hello innanzitutto utilizzare uno dei metodi di hello in cluster di hello toodeploy passaggio 1. Specificare un'immagine di un nodo di calcolo generico in questo caso, poiché non è necessario Excel sui nodi di calcolo hello. Attenersi quindi alla procedura seguente:

1. Dopo aver recuperato il certificato di cluster hello, importarlo nel computer client hello in Cert: \CurrentUser\Root.
2. Installare hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) e [utilità client di HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923). Questi strumenti consentono di toodevelop ed eseguono applicazioni SOA.
3. Scaricare hello HelloWorldR2 [codice di esempio](https://www.microsoft.com/download/details.aspx?id=41633). Aprire hello HelloWorldR2.sln in Visual Studio 2010 o 2012. Questo esempio non è attualmente compatibile con le versioni più recenti di Visual Studio.
4. Prima di compilazione progetto EchoService hello. Quindi, distribuire cluster IaaS di hello servizio toohello in hello stesso modo in cui si distribuiscono tooan locale del cluster. Per informazioni dettagliate, vedere hello Readme in HelloWordR2. Modificare e compilare hello HellWorldR2 e da altri progetti, come descritto nella seguente sezione toogenerate hello SOA applicazioni client eseguite in un cluster IaaS di Azure hello.

### <a name="use-http-binding-with-azure-storage-queue"></a>Uso dell'associazione Http con coda di archiviazione di Azure
associazione Http toouse con una coda di archiviazione di Azure, apportare alcune modifiche toohello codice di esempio.

* Aggiornare il nome del cluster hello.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* Facoltativamente, utilizzare predefinito hello TransportScheme SessionStartInfo o impostare in modo esplicito tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Utilizzare l'associazione predefinita per hello BrokerClient.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    O impostare in modo esplicito utilizzando basicHttpBinding hello.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* Facoltativamente, impostare hello UseAzureQueue flag tootrue in SessionStartInfo. Se non impostato, verrà impostato tootrue per impostazione predefinita quando il nome del cluster hello suffissi di dominio di Azure e hello TransportScheme è Http.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Uso dell'associazione Http senza coda di archiviazione di Azure
associazione Http toouse senza una coda di archiviazione di Azure, in modo esplicito set hello UseAzureQueue flag toofalse in hello SessionStartInfo.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Uso dell'associazione NetTcp
toouse NetTcp associazione configurazione hello è cluster locale di simili tooconnecting tooan. È necessario tooopen alcuni endpoint nella macchina virtuale del nodo head hello. Se si utilizza del cluster di hello toocreate hello IaaS di HPC Pack distribuzione script, ad esempio, set di endpoint hello in hello portale di Azure come indicato di seguito.

1. Arrestare VM hello.
2. Aggiungere le porte TCP hello 9090, 9087, 9091, 9094 per sessione, hello Broker, rispettivamente di Service Broker worker e servizi di dati,
   
    ![Configurare gli endpoint][endpoint-new-portal]
3. Avviare hello macchina virtuale.

applicazione client SOA Hello è necessario apportare alcuna modifica, ad eccezione di modifica hello head toohello IaaS completa nome cluster.

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sull'esecuzione di carichi di lavoro di Excel con HPC Pack, vedere [queste risorse](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) .
* Vedere l'articolo relativo alla [gestione dei servizi SOA in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) per altre informazioni sulla distribuzione e sulla gestione dei servizi SOA con HPC Pack.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png

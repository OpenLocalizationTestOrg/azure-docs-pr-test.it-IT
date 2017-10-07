---
title: aaaSet di un cluster di Azure Service Fabric | Documenti Microsoft
description: Guida introduttiva. Creare un cluster Windows o Linux di Service Fabric in Azure.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Creare il primo cluster di Service Fabric di Azure
Un [cluster di Service Fabric](service-fabric-deploy-anywhere.md) è un set di computer fisici o macchine virtuali connesse tramite rete in cui vengono distribuiti e gestiti i microservizi. Questa Guida rapida consente di un cluster di cinque nodi, in esecuzione su Windows o Linux, tramite hello toocreate [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) o [portale di Azure](http://portal.azure.com) in pochi minuti.  

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.


## <a name="use-hello-azure-portal"></a>Utilizzare hello portale di Azure

Accedere al portale di Azure toohello [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Creare il cluster hello

1. Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.
2. Selezionare **calcolo** da hello **New** blade e quindi selezionare **Cluster di Service Fabric** da hello **calcolo** blade.
3. Compilare hello Service Fabric **nozioni di base** form. Per **del sistema operativo**, selezionare la versione hello di Windows o Linux desiderato hello toorun i nodi del cluster. nome utente Hello e la password immessa in questo caso è toolog utilizzati nella macchina virtuale toohello. Per **Gruppo di risorse** creare un nuovo gruppo. Un gruppo di risorse è un contenitore logico in cui vengono create e gestite collettivamente le risorse di Azure. Al termine fare clic su **OK**.

    ![Output installazione del cluster][cluster-setup-basics]

4. Compilare hello **configurazione Cluster** form.  Per **Numero di tipi di nodo** immettere "1".

5. Selezionare **il tipo di nodo 1 (principale)** e compilare hello **configurazione del tipo di nodo** form.  Immettere un nome di tipo di nodo e impostare hello [il livello di durabilità](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) troppo "Bronze".  Selezionare una dimensione di VM.

    Dimensioni VM hello, il numero di macchine virtuali, gli endpoint personalizzati, di definire tipi di nodo e altre impostazioni per le macchine virtuali di quel tipo di hello. Ogni tipo di nodo definito è configurato come un set di scalabilità della macchina virtuale separata, ovvero toodeploy usato e le macchine virtuali gestite come un set. Ogni tipo di nodo può essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse.  Hello prima o primario, tipo di nodo è in servizi di sistema di Service Fabric sono ospitati e devono avere cinque o più macchine virtuali.

    La [pianificazione della capacità](service-fabric-cluster-capacity.md) è un passaggio importante per qualsiasi distribuzione di produzione.  Per questa Guida introduttiva, tuttavia, non vengono eseguite applicazioni, quindi selezionare una VM con dimensioni *DS1_v2 Standard*.  Selezionare "Argento" per hello [livello di affidabilità](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) e una scala di macchina virtuale iniziale imposta la capacità di 5.  

    Endpoint personalizzati aprono le porte nel servizio di bilanciamento carico di Azure hello in modo che sia possibile connettersi ad applicazioni in esecuzione nel cluster hello.  Immettere "80, 8172" tooopen le porte 80 e 8172.

    Non archiviare hello **configurare le impostazioni avanzate** nella quale viene utilizzata per la personalizzazione di endpoint di gestione di TCP o HTTP, gli intervalli di porte di applicazione, [vincoli di posizionamento](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), e [capacità proprietà](service-fabric-cluster-resource-manager-metrics.md).    

    Selezionare **OK**.

6. In hello **configurazione Cluster** modulo, impostare **diagnostica** troppo**su**.  Per questa Guida rapida, non è necessario tooenter qualsiasi [infrastruttura impostazione](service-fabric-cluster-fabric-settings.md) proprietà.  In **versione di Fabric**selezionare **automatica** modalità di aggiornamento in modo che Microsoft aggiorna automaticamente la versione hello hello dell'infrastruttura di esecuzione del codice cluster hello.  Impostare la modalità di hello troppo**manuale** se si desidera troppo[scegliere una versione supportata](service-fabric-cluster-upgrade.md) tooupgrade per. 

    ![Configurazione del tipo di nodo][node-type-config]

    Selezionare **OK**.

7. Compilare hello **sicurezza** form.  Per questa Guida introduttiva selezionare **Senza protezione**.  È altamente consigliabile toocreate un cluster protetto per i carichi di lavoro, tuttavia, poiché chiunque in modo anonimo può connettersi cluster non sicuri tooan ed eseguire operazioni di gestione.  

    I certificati vengono usati in Service Fabric tooprovide autenticazione e crittografia toosecure vari aspetti di un cluster e le relative applicazioni. Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md).  mediante Azure Active Directory o tooset i certificati per la protezione delle applicazioni, l'autenticazione utente tooenable [creare un cluster da un modello di gestione risorse](service-fabric-cluster-creation-via-arm.md).

    Selezionare **OK**.

8. Riepilogo hello di revisione.  Se si desidera toodownload un modello di gestione delle risorse compilato in base alle impostazioni di hello immesso, selezionare **Scarica modello e i parametri**.  Selezionare **crea** cluster hello toocreate.

    È possibile visualizzare lo stato di avanzamento di hello creazione nelle notifiche hello. (Fare clic sull'icona di campanello"hello" nella barra di stato hello in alto hello destra dello schermo). Se fa clic su **Pin tooStartboard** durante la creazione di cluster hello, vedrai **la distribuzione di Cluster di Service Fabric** bloccato toohello **avviare** Lavagna.

### <a name="view-cluster-status"></a>Visualizzare lo stato del cluster
Una volta creato il cluster, è possibile controllare il cluster in hello **Panoramica** pannello nel portale di hello. È ora possibile visualizzare i dettagli di hello del cluster nel dashboard di hello, tra cui endpoint pubblico del cluster hello e tooService un collegamento Fabric Explorer.

![Stato del cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualizzare i cluster hello tramite Service Fabric explorer
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) rappresenta un ottimo strumento per la visualizzazione del cluster e la gestione delle applicazioni.  Service Fabric Explorer è un servizio in esecuzione nel cluster hello.  Diritti di accesso usando un browser web, fare clic su hello **Service Fabric Explorer** collegamento del cluster hello **Panoramica** hello portale.  È inoltre possibile immettere l'indirizzo hello direttamente nel browser hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

dashboard del cluster Hello viene fornita una panoramica del cluster, incluso un riepilogo dell'applicazione e l'integrità del nodo. visualizzazione del nodo Hello Mostra struttura fisica di hello del cluster di hello. Per un determinato nodo, è possibile esaminare le applicazioni con il codice distribuito in quel nodo.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Connettere il cluster toohello tramite PowerShell
Verificare che tale cluster hello è in esecuzione tramite la connessione tramite PowerShell.  Hello modulo ServiceFabric di PowerShell viene installato con hello [Service Fabric SDK](service-fabric-get-started.md).  Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet stabilisce un cluster di toohello di connessione.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md) per altri esempi di connessione tooa cluster. Dopo la connessione toohello cluster, utilizzare hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet un elenco di nodi nelle informazioni del cluster e lo stato di hello per ogni nodo. **HealthState** deve essere *OK* per ogni nodo.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Rimuovere il cluster hello
Un cluster di Service Fabric è costituito da altre risorse di Azure inoltre toohello risorsa del cluster stesso. In modo toocompletely eliminare un cluster di Service Fabric è inoltre necessario toodelete che tutti hello è composto di risorse. cluster di Hello più semplice modo toodelete hello e tutte le risorse di hello che consuma è gruppo di risorse toodelete hello. Per altri modi toodelete un cluster o toodelete alcune risorse, ma non tutte, hello in un gruppo di risorse, vedere [eliminare un cluster](service-fabric-cluster-delete.md)

Eliminare un gruppo di risorse nel portale di Azure hello:
1. Passare il cluster di Service Fabric toohello da toodelete.
2. Fare clic su hello **gruppo di risorse** nome nella pagina di essentials hello del cluster.
3. In hello **risorse gruppo Essentials** pagina, fare clic su **Elimina gruppo di risorse** e seguire le istruzioni di hello l'eliminazione di hello toocomplete pagina hello del gruppo di risorse.
    ![Eliminare il gruppo di risorse hello][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Usare Azure Powershell toodeploy un cluster protetto
1. Scaricare hello [Azure Powershell versione 4.0 o versione successiva del modulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) nel computer.

2. Aprire una finestra di Windows PowerShell, hello esecuzione comando seguente. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Viene visualizzata un output simile toohello.

    ![Elenco PS][ps-list]

3. Account di accesso tooAzure e toowhich sottoscrizione selezionare hello si desidera toocreate hello cluster

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Esecuzione hello successivo comando toonow creare un cluster protetto. Non dimenticare parametri hello toocustomize. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    comando Hello può richiedere da toocomplete minuti too30 di 10 minuti, alla fine di hello di esso, è necessario ottenere una simile toohello seguenti di output. output di Hello dispone di informazioni sul certificato hello, KeyVault in cui sono stati caricati, hello e hello cartella locale in cui copiare il certificato di hello. 

    ![Output PS][ps-out]

5. Copia output intero hello e salvare il file di testo tooa dobbiamo toorefer tooit. Prendere nota di hello dall'output di hello le seguenti informazioni. 

    - **CertificateSavedLocalPath**: c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint**: C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint**: https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort**: 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Installare il certificato di hello sul computer locale
  
tooconnect toohello cluster, è necessario il certificato di hello tooinstall nell'archivio personale (My) hello dell'utente corrente hello. 

Eseguire hello seguente PowerShell

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Si è ora pronto tooconnect tooyour sicura cluster.

### <a name="connect-tooa-secure-cluster"></a>Connettere il cluster protetto di tooa 

Eseguire hello cluster sicuro tooa tooconnect comando PowerShell seguente. dettagli del certificato Hello devono corrispondere a un certificato che è stato utilizzato tooset di cluster hello. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Hello seguente esempio mostra hello parametri completed: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Eseguire hello seguente toocheck comando che si è connessi e hello cluster è integro.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Pubblicare il cluster tooyour app da Visual Studio

Ora che configuri un cluster di Azure, è possibile pubblicare il tooit di applicazioni da Visual Studio dal seguente hello [pubblica tooan cluster](service-fabric-publish-app-remote-cluster.md) documento. 

### <a name="remove-hello-cluster"></a>Rimuovere il cluster hello
Un cluster è costituito da altre risorse di Azure inoltre toohello risorsa del cluster stesso. cluster di Hello più semplice modo toodelete hello e tutte le risorse di hello che consuma è gruppo di risorse toodelete hello. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Passaggi successivi
Una volta impostati un cluster di sviluppo, provare seguente hello:
* [Creare un cluster sicuro nel portale di hello](service-fabric-cluster-creation-via-portal.md)
* [Creare un cluster da un modello](service-fabric-cluster-creation-via-arm.md) 
* [Distribuire le app tramite PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG

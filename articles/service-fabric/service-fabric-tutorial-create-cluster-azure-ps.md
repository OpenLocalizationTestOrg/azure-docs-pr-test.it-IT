---
title: aaaCreate un'infrastruttura del servizio cluster in Azure | Documenti Microsoft
description: Informazioni su come toocreate Windows o Linux Service Fabric cluster in Azure utilizzando PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Creare un cluster sicuro in Azure con PowerShell
Questa esercitazione viene illustrato come toocreate un'infrastruttura del servizio cluster (Windows o Linux) in esecuzione in Azure. Al termine, si dispone di un cluster in esecuzione nel cloud hello che è possibile distribuire applicazioni.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un cluster sicuro di Service Fabric in Azure tramite PowerShell
> * Cluster hello protetta con un certificato x. 509
> * Connettere il cluster toohello tramite PowerShell
> * Rimuovere un cluster

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione:
- Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- Installare hello [modulo di Service Fabric SDK e PowerShell](service-fabric-get-started.md)
- Installare hello [Azure Powershell versione del modulo 4.1 o versione successiva](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Hello procedura crea una cluster di Service Fabric di anteprima (singola macchina virtuale) a nodo singolo. cluster Hello è protetto da un certificato autofirmato creato insieme a cluster hello viene quindi inserito in un insieme di credenziali chiave. Cluster a nodo singolo non può essere scalato oltre una macchina virtuale e i cluster di anteprima non possono essere aggiornato toonewer versioni.

costi toocalculate mediante l'esecuzione di un cluster di Service Fabric in Azure usare hello [calcolatore dei costi Azure](https://azure.microsoft.com/pricing/calculator/).
Per altre informazioni sulla creazione di cluster di Service Fabric, vedere [Creare un cluster di Service Fabric usando Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Creare cluster hello tramite Azure PowerShell
1. Scaricare una copia locale del file di parametro hello e al modello di Azure Resource Manager hello da hello [il modello di gestione risorse di Azure per Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repository GitHub.  *azuredeploy.JSON* hello Azure Resource Manager modello che definisce un cluster di Service Fabric. *azuredeploy.Parameters.JSON* è un file di parametri per la distribuzione di cluster toocustomize hello.

2. Personalizzare i seguenti parametri in hello hello *azuredeploy.parameters.json* file dei parametri:

   | .       | Descrizione | Valore consigliato |
   | --------------- | ----------- | --------------- |
   | clusterLocation | cluster di hello toodeploy toowhich area Azure Hello. | *ad esempio westeurope, eastasia, eastus* |
   | clusterName     | Nome del cluster hello desiderato toocreate. | *ad esempio bobs-sfpreviewcluster* |
   | adminUserName   | account di amministratore locale Hello in macchine virtuali del cluster hello. | *Qualsiasi nome utente di Windows Server valido* |
   | adminPassword   | Password dell'account di amministratore locale hello in macchine virtuali del cluster hello. | *Qualsiasi password di Windows Server valido* |
   | clusterCodeVersion | toorun versione di Service Fabric Hello. 255.255.X.255 sono versioni di anteprima. | **255.255.5718.255** |
   | vmInstanceCount | numero di Hello di macchine virtuali del cluster (può essere 1 o 3-99). | **1** | *Per un cluster di anteprima, specificare solo una macchina virtuale* |

3. Aprire una console di PowerShell, account di accesso tooAzure e selezionare una sottoscrizione hello da cluster hello toodeploy in:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Creare e crittografare una password per hello certificato toobe utilizzata dall'infrastruttura del servizio.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Creare il cluster hello e il certificato eseguendo hello comando seguente:

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >Hello `-CertificateSubjectName` parametro devono essere allineate con il parametro di clusterName hello specificata nel file dei parametri di hello, nonché come hello dominio associato toohello area di Azure si è scelto, ad esempio: `clustername.eastus.cloudapp.azure.com`.

Al termine della configurazione di hello, che genera informazioni sui cluster hello creato in Azure. Copia anche hello cluster certificato toohello - CertificateOutputFolder directory nel percorso di hello che per questo parametro è specificato. È necessario questo tooaccess certificato Service Fabric Explorer e visualizzare l'integrità hello del cluster.

Prendere nota dell'URL di hello per il cluster, che potrebbe essere simile toohello seguente URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>Modificare il certificato di hello & accedere Service Fabric Explorer ##

1. Fare doppio clic su hello tooopen tramite certificato hello importazione guidata certificati.

2. Utilizzare le impostazioni predefinite, ma assicurarsi che toocheck hello **contrassegna questa chiave come esportabile.** casella di controllo, in hello **protezione della chiave privata** passaggio. Visual Studio deve certificato hello tooexport quando si configura l'autenticazione di Azure del Registro di sistema contenitore tooService dell'infrastruttura Cluster più avanti in questa esercitazione.

3. È ora possibile aprire Service Fabric Explorer in un browser. toodo in tal caso, passare toohello **ManagementEndpoint** URL per il cluster usando un web browser e certificato selezionare hello che è stato salvato nel computer.

>[!NOTE]
>Quando si apre Service Fabric Explorer, viene visualizzato un errore di certificato, poiché si usa un certificato autofirmato. In Edge, è necessario tooclick *dettagli* e quindi hello *andare nella pagina Web toohello* collegamento. In Chrome, è necessario tooclick *avanzate* e quindi hello *procedere* collegamento.

>[!NOTE]
>Se la creazione del cluster di hello non riesce, è sempre possibile rieseguire comando hello, che aggiorna le risorse di hello già distribuite. Se un certificato è stato creato come parte della distribuzione di hello non è riuscita, viene generato uno nuovo. creazione del cluster tootroubleshoot, vedere [creare un cluster di Service Fabric usando Gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Connettere il cluster protetto di toohello
Connettere il cluster toohello utilizzando il modulo di PowerShell di Service Fabric hello installato con hello Service Fabric SDK.  In primo luogo, è possibile installare il certificato di hello nell'archivio personale (My) hello dell'utente corrente di hello nel computer in uso.  Eseguire il comando PowerShell seguente hello:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Si è ora pronto tooconnect tooyour sicura cluster.

Hello **Service Fabric** modulo PowerShell fornisce molti cmdlet per la gestione di cluster, applicazioni e servizi di Service Fabric.  Hello utilizzare [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello sicura cluster. Hello identificazione personale del certificato e i dettagli di endpoint di connessione vengono trovati nell'output di hello da un passaggio precedente.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Verificare che si è connessi e hello cluster è integro utilizzando hello [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Pulire le risorse

Un cluster è costituito da altre risorse di Azure inoltre toohello risorsa del cluster stesso. cluster di Hello più semplice modo toodelete hello e tutte le risorse di hello che consuma è gruppo di risorse toodelete hello.

Accedi tooAzure e selezionare l'ID sottoscrizione hello con cui si desidera che il cluster di hello tooremove.  È possibile trovare l'ID sottoscrizione effettuando l'accesso toohello [portale di Azure](http://portal.azure.com). Eliminare il gruppo di risorse hello e tutte le risorse cluster hello utilizzando hello [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un cluster di Service Fabric in Azure
> * Cluster hello protetta con un certificato x. 509
> * Connettere il cluster toohello tramite PowerShell
> * Rimuovere un cluster

Successivamente, spostare toohello successivo dell'esercitazione toolearn come toodeploy un'applicazione esistente.
> [!div class="nextstepaction"]
> [Distribuire un'app .NET tramite Docker Compose](service-fabric-host-app-in-a-container.md)

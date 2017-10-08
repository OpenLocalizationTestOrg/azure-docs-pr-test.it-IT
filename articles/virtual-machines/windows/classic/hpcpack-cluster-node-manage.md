---
title: nodi di calcolo cluster HPC Pack aaaManage | Documenti Microsoft
description: Informazioni su tooadd strumenti di script PowerShell, rimuovere, avviare e arrestare i nodi di calcolo cluster HPC Pack 2012 R2 in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Gestire il numero di hello e la disponibilità dei nodi di calcolo in un cluster HPC Pack in Azure
Se si crea un cluster HPC Pack 2012 R2 in macchine virtuali di Azure, è possibile modi tooeasily aggiungere, rimuovere, avviare (provisioning) o arrestare (effettuarne il deprovisioning) alcune macchine virtuali del nodo del cluster di calcolo. toodo queste attività, eseguire gli script di PowerShell di Azure che vengono installati nella macchina virtuale del nodo head hello. Questi script consente di controllare il numero di hello e disponibilità delle risorse di cluster HPC Pack in modo che è possibile controllare i costi.

> [!IMPORTANT] 
> In questo articolo si applica solo a tooHPC Pack 2012 R2 cluster in Azure creato utilizzando il modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.
> Inoltre, gli script di PowerShell hello descritti in questo articolo non sono disponibili in HPC Pack 2016.

## <a name="prerequisites"></a>Prerequisiti
* **Cluster HPC Pack 2012 R2 in macchine virtuali di Azure**: creare un cluster HPC Pack 2012 R2 nel modello di distribuzione classica hello. Ad esempio, è possibile automatizzare distribuzione hello utilizzando l'immagine di macchina virtuale di HPC Pack 2012 R2 hello in hello Azure Marketplace e uno script di PowerShell di Azure. Per informazioni e i prerequisiti, vedere [creare un Cluster HPC con lo script di distribuzione IaaS di HPC Pack hello](hpcpack-cluster-powershell-script.md).
  
    Dopo la distribuzione, trovare hello script di gestione di nodo % hello CCP\_nella cartella bin % HOME nel nodo head hello. Eseguire ogni script hello come amministratore.
* **Certificato di gestione o di file di impostazioni di pubblicazione Azure**: È necessario uno dei seguenti hello toodo nel nodo head hello:
  
  * **File di impostazioni di pubblicazione hello importazione Azure**. toodo, hello esecuzione seguendo i cmdlet PowerShell di Azure nel nodo head hello:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Configurare il certificato di gestione di Azure hello nel nodo head hello**. Se si dispone di file con estensione cer hello, importarlo nell'archivio certificati CurrentUser\My di hello e quindi eseguire hello seguente cmdlet di Azure PowerShell per l'ambiente di Azure (cloud o AzureChinaCloud):
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>Aggiungere le macchine virtuali dei nodi di calcolo
Aggiungere nodi di calcolo con hello **Add-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintassi
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>parameters
* **ServiceName**: nome del servizio cloud hello nuove macchine virtuali del nodo di calcolo vengono aggiunti.
* **ImageName**: nome dell'immagine di macchina virtuale di Azure, che può essere ottenuto tramite hello portale di Azure classico o i cmdlet di Azure PowerShell **Get-AzureVMImage**. immagine di Hello deve soddisfare hello seguenti requisiti:
  
  1. Deve essere installato un sistema operativo Windows.
  2. HPC Pack deve essere installato nel ruolo del nodo calcolo hello.
  3. immagine di Hello deve essere un'immagine privata della categoria di utente hello, non un'immagine di macchina virtuale di Azure pubblica.
* **Quantità**: numero di calcolo nodo macchine virtuali toobe aggiunto.
* **InstanceSize**: dimensione di hello macchine virtuali del nodo di calcolo.
* **DomainUserName**: il nome utente di dominio, ovvero toojoin utilizzati hello nuove macchine virtuali toohello dominio.
* **DomainUserPassword**: la Password dell'utente di dominio hello.
* **NodeNameSeries** (facoltativo): modello di denominazione per hello nodi di calcolo. deve essere formato Hello &lt; *radice\_nome*&gt;&lt;*avviare\_numero*&gt;%. Ad esempio, MyCN % 10% significa una serie di hello consente di calcolare i nomi dei nodi a partire da MyCN11. Se non specificato, hello script utilizza hello configurato serie di denominazione di nodo nel cluster HPC hello.

### <a name="example"></a>Esempio
Hello esempio seguente viene aggiunta nodo di calcolo grandi dimensioni 20 macchine virtuali nel servizio cloud hello *hpcservice1*, in base all'immagine di macchina virtuale hello *hpccnimage1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>Rimuovere le macchine virtuali dei nodi di calcolo
Rimuovere i nodi di calcolo con hello **Remove-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintassi
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>parameters
* **Nome**: rimuovere i nomi di toobe i nodi del cluster. Sono supportati caratteri jolly. nome del set di parametri Hello è nome. Non è possibile specificare entrambi hello **nome** e **nodo** parametri.
* **Nodo**: oggetto HpcNode hello per hello nodi toobe rimossa, che può essere ottenuto tramite i cmdlet di HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nome del set di parametri Hello è nodo. Non è possibile specificare entrambi hello **nome** e **nodo** parametri.
* **DeleteVHD** (facoltativo): l'impostazione toodelete dischi hello associata per hello macchine virtuali che sono state rimosse.
* **Force** (facoltativo): l'impostazione tooforce offline i nodi HPC prima di rimuoverli.
* **Conferma** (facoltativo): Richiedi conferma prima di eseguire il comando hello.
* **WhatIf**: impostazione toodescribe cosa accadrebbe se venisse eseguito il comando di hello senza eseguire effettivamente il comando hello.

### <a name="example"></a>Esempio
Hello esempio seguente viene forzato nodi offline hello cui nomi iniziano con *HPCNode-CN,* e li rimuove i nodi di hello e i dischi associati.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>Avviare le macchine virtuali dei nodi di calcolo
Inizio nodi con hello **Start-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintassi
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>parameters
* **Nome**: i nomi di hello cluster nodi toobe avviato. Sono supportati caratteri jolly. nome del set di parametri Hello è nome. Non è possibile specificare entrambi hello **nome** e **nodo** parametri.
* **Nodo**-oggetto HpcNode hello per hello nodi toobe avviato, che può essere ottenuto tramite i cmdlet di HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nome del set di parametri Hello è nodo. Non è possibile specificare entrambi hello **nome** e **nodo** parametri.

### <a name="example"></a>Esempio
Hello esempio seguente viene avviato nodi cui nomi iniziano con *HPCNode-CN,*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>Arrestare le macchine virtuali dei nodi di calcolo
Arresta nodi di calcolo con hello **Stop-hpciaasnode.ps1** script.

### <a name="syntax"></a>Sintassi
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>parameters
* **Nome**-i nomi di toobe di nodi cluster hello arrestato. Sono supportati caratteri jolly. nome del set di parametri Hello è nome. Non è possibile specificare entrambi hello **nome** e **nodo** parametri.
* **Nodo**: oggetto HpcNode hello per hello nodi toobe arrestato, che può essere ottenuto tramite i cmdlet di HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nome del set di parametri Hello è nodo. Non è possibile specificare entrambi hello **nome** e **nodo** parametri.
* **Force** (facoltativo): l'impostazione tooforce offline i nodi HPC prima di arrestarli.

### <a name="example"></a>Esempio
Hello esempio seguente viene forzato nodi non in linea con i nomi che iniziano *HPCNode-CN,* e quindi si arresta hello nodi.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Passaggi successivi
* tooautomatically aumentare o ridurre i nodi del cluster in base al carico di lavoro corrente hello dei processi e attività in cluster hello hello, vedere [automaticamente aumentare e ridurre le risorse di cluster HPC Pack hello Azure secondo toohello cluster del carico di lavoro](hpcpack-cluster-node-autogrowshrink.md).


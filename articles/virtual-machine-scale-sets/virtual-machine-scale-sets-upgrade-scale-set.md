---
title: imposta una scala di macchina virtuale di Azure aaaUpgrade | Documenti Microsoft
description: "Aggiornare un set di scalabilità di macchine virtuali di Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Aggiornare un set di scalabilità di macchine virtuali
Questo articolo descrive come è possibile distribuire un sistema operativo aggiornamento tooan macchina virtuale di Azure set di scalabilità senza tempo di inattività. In questo contesto, un aggiornamento del sistema operativo comporta la modifica di versione di hello o SKU di hello del sistema operativo o hello URI di un'immagine personalizzata. L'aggiornamento senza tempi di inattività implica l'aggiornamento di una macchina virtuale alla volta o in gruppi, ad esempio un dominio di errore alla volta, anziché contemporaneamente. In questo modo, è possibile mantenere in esecuzione tutte le macchine virtuali non in fase di aggiornamento.

tooavoid ambiguità, si distingue quattro tipi di aggiornamento del sistema operativo potrebbe essere necessario tooperform:

* Modifica di versione di hello o SKU di un'immagine della piattaforma. Ad esempio la modifica Ubuntu versione 14.04.2-LTS da 14.04.201506100 too14.04.201507060 o la modifica hello Ubuntu più recente 15.10 SKU too16.04.0-LTS/latest. Questo scenario è illustrato in questo articolo.
* Modifica hello URI che punta tooa nuova versione di un'immagine personalizzata è stata compilata (**proprietà** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **immagine** > **uri**). Questo scenario è illustrato in questo articolo.
* Modifica hello immagine riferimento di un set di scalabilità che è stato creato utilizzando i dischi gestiti di Azure.
* L'applicazione di patch hello del sistema operativo da una macchina virtuale (esempi di questo tipo includono l'installazione di una patch di sicurezza e l'esecuzione di Windows Update). Questo scenario è supportato ma non è trattato in questo articolo.

I set di scalabilità delle macchine virtuali che vengono distribuiti come parte di un cluster di [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) non sono trattati qui. Per altre informazioni sulle patch di Service Fabric vedere [Applicare patch al sistema operativo Windows nel cluster di Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application).

Hello base hello di sequenza per la modifica del sistema operativo, versione/SKU di un'immagine della piattaforma o URI di un'immagine personalizzata hello è simile al seguente:

1. Ottenere modello scala hello macchina virtuale.
2. Versione di hello modifica SKU, riferimento a un'immagine o valore URI nel modello di hello.
3. Aggiornare il modello di hello.
4. Eseguire un *manualUpgrade* chiamare su macchine virtuali hello in set di scalabilità hello. Questo passaggio è rilevante solo se *upgradePolicy* è troppo**manuale** nel set della scalabilità. Se è impostato troppo**automatico**, tutte le macchine virtuali hello vengono aggiornate contemporaneamente, con conseguente rallentamento dei tempi di inattività.

Con queste informazioni in considerazione, vediamo come è possibile aggiornare la versione hello di un set in PowerShell e tramite l'API REST hello di scalabilità. Questi esempi riguardano caso hello di un'immagine della piattaforma, ma in questo articolo fornisce informazioni sufficienti affinché si tooadapt immagine personalizzata di tooa questo processo.

## <a name="powershell"></a>PowerShell
Questo esempio viene aggiornato un set di scalabilità di macchine virtuali di Windows (creazione toohello nuova versione 4.0.20160229. Dopo aver aggiornato il modello di hello, esegue un'istanza di macchina virtuale un aggiornamento alla volta.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Se si sta aggiornando hello URI per un'immagine personalizzata anziché la modifica di una versione dell'immagine della piattaforma, sostituire "set hello nuova versione" hello riga con un comando che verrà aggiornata hello URI dell'immagine di origine. Ad esempio, se il set di scalabilità di hello è stato creato senza l'utilizzo di dischi gestiti di Azure, aggiornamento hello avrà un aspetto simile al seguente:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Se un'immagine personalizzata in base a set di scalabilità è stata creata utilizzando i dischi gestiti di Azure, quindi riferimento all'immagine di hello verranno aggiornato. ad esempio:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Hello API REST
Di seguito sono riportati alcuni esempi di Python che utilizzano hello tooroll di API REST di Azure di un aggiornamento di versione del sistema operativo. Entrambi utilizzano lightweight hello [azurerm](https://pypi.python.org/pypi/azurerm) libreria di API REST di Azure wrapper funzioni toodo un'operazione GET su scala hello Imposta modello, seguito da un'operazione PUT con un modello aggiornato. Sono anche esaminare le visualizzazioni di istanze di macchina virtuale macchine virtuali di hello tooidentify dal dominio di aggiornamento.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) script Python usato tooroll out un tooa di aggiornamento del sistema operativo in esecuzione sulla scalabilità della macchina virtuale è impostato un dominio di aggiornamento alla volta.

![Script Vmssupgrade per la scelta delle macchine virtuali o di un dominio di aggiornamento](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Questo script consente di scegliere tooupdate specifiche macchine virtuali o specificare un dominio di aggiornamento. Supporta la modifica di una versione dell'immagine della piattaforma o hello URI di un'immagine personalizzata.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) è un editor generico per i set di scalabilità di macchine virtuali che mostra lo stato della macchina virtuale come heatmap in cui una riga rappresenta un dominio di aggiornamento. Tra le altre cose, è possibile aggiornare il modello di hello per un set di scalabilità con una nuova versione, SKU o URI dell'immagine personalizzata e quindi selezionare tooupgrade di domini di errore. Quando si esegue questa operazione, tutte le macchine virtuali hello in tale dominio di aggiornamento vengono aggiornati toohello nuovo modello. In alternativa, è possibile eseguire un aggiornamento in sequenza in base alle dimensioni di batch hello di propria scelta.  

Hello schermata riportata di seguito viene illustrato un modello di un set per Ubuntu 14.04-2LTS versione 14.04.201507060 di scalabilità. Strumento toothis sono state aggiunte molte altre opzioni dopo questa schermata.

![Modello Vmsseditor di un set di scalabilità per Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Dopo aver fatto clic **aggiornamento** e quindi **Ottieni dettagli**, tooupdate l'avvio delle macchine virtuali in UD 0.

![Vmsseditor che illustra un aggiornamento in corso](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)


---
title: Dischi di macchina virtuale scala set collegati dati aaaAzure | Documenti Microsoft
description: "Informazioni su come toouse collegati dischi di dati con il set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Set di scalabilità di macchine virtuali di Azure e dischi di dati collegati
I [set di scalabilità di macchine virtuali](/azure/virtual-machine-scale-sets/) di Azure supportano ora macchine virtuali con dischi di dati collegati. I dischi dati possono essere definiti nel profilo di archiviazione hello per set di scalabilità che sono stati creati con dischi gestiti di Azure. In precedenza hello solo le opzioni di archiviazione collegata direttamente disponibili con le macchine virtuali nel set di scalabilità sono state unità hello del sistema operativo e unità temporanea.

> [!NOTE]
>  Quando si crea un set di scalabilità con i dischi dati collegati definiti, è comunque necessario toomount e hello formato dischi all'interno di una macchina virtuale toouse li (proprio come per le macchine virtuali di Azure autonoma). Un modo pratico di toodo equivale toouse un'estensione di uno script personalizzato che chiama un toopartition script standard e formattazione tutti i dischi dati hello in una macchina virtuale.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Creare un set di scalabilità con dischi di dati collegati
Toocreate un modo semplice una scala impostata con i dischi collegati è hello toouse [CLI di Azure](https://github.com/Azure/azure-cli) _vmss creare_ comando. Hello di esempio seguente crea un gruppo di risorse di Azure e un set di scalabilità della macchina virtuale delle macchine virtuali Ubuntu 10, ognuno con dischi dati collegati 2, 50 GB e 100 GB.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Si noti che hello _vmss creare_ comando per impostazione predefinita di determinati valori di configurazione, se non si specifica. toosee hello opzioni disponibili che è possibile eseguire l'override di provare a:
```bash
az vmss create --help
```
Un altro modo toocreate, un set di scalabilità con dischi dati collegati è toodefine imposta una scala in un modello di gestione risorse di Azure, includere un _dataDisks_ sezione hello _storageProfile_e distribuire hello modello. Hello 50 e 100 GB disco esempio sopra riportato sarebbe definire simile al seguente nel modello hello:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
È possibile visualizzare un esempio completo e pronto toodeploy di un modello di set di scalabilità con un disco collegato, definito qui: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Aggiunta di una scala dei dati su disco tooan esistente set
> [!NOTE]
>  È possibile collegare solo set di scalabilità con i tooa dischi dati che è stata creata con [dischi gestiti di Azure](./virtual-machine-scale-sets-managed-disks.md).

È possibile aggiungere un data disco tooa VM set di scalabilità mediante Azure CLI _collega disco vmss az_ comando. Specificare un lun che non sia già in uso. Hello CLI esempio seguente aggiunge un toolun di unità di 50 GB 3:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

esempio di PowerShell seguente Hello aggiunge un toolun di unità di 50 GB 3:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Dimensioni delle macchine Virtuali diverse hanno limiti diversi in numeri hello di supportano le unità collegate. Controllare hello [le caratteristiche di dimensioni di macchina virtuale](../virtual-machines/windows/sizes.md) prima di aggiungere un nuovo disco.

È inoltre possibile aggiungere un disco mediante l'aggiunta di un nuovo toohello voce _dataDisks_ proprietà hello _storageProfile_ di una scala impostare definizione e l'applicazione hello modifica. tootest, trovare una definizione di set di scalabilità esistente nel hello [Esplora inventario risorse di Azure](https://resources.azure.com/). Selezionare _modifica_ e aggiungere un nuovo elenco toohello disco dei dischi dati. Ad esempio, utilizzando l'esempio hello precedente:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Selezionare quindi _inserire_ tooapply hello cambia tooyour set di scalabilità. Questo esempio funziona se si usano macchine virtuali con dimensioni che supportano più di due dischi di dati collegati.

> [!NOTE]
> Quando si effettua una scala tooa Modifica definizione, ad esempio aggiunta o rimozione di un disco dati del set, si applica a macchine virtuali tooall appena creato, ma si applica solo le macchine virtuali tooexisting se hello _upgradePolicy_ proprietà è impostata troppo "automatico". Se è impostato troppo "manuale", è necessario toomanually applicare hello nuovo modello tooexisting macchine virtuali. È possibile farlo nel portale di hello utilizzando hello _aggiornamento AzureRmVmssInstance_ PowerShell comando o tramite hello _az vmss update-istanze_ comando CLI.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Aggiunta di dati pre-popolato dischi tooan esistente scala set 
> Quando si aggiungono dischi tooan esistente set di scalabilità di modello, in base alla progettazione, hello verrà creato un disco sempre vuoto. Questo scenario include anche nuove istanze create dal set di scalabilità hello. Questo comportamento è perché definizione scaleset hello è un disco dati vuoto. Nelle unità di dati pre-popolato toocreate ordine per un modello di set di scalabilità esistente, è possibile scegliere una delle due opzioni:

* Copiare dati dai dischi di dati di hello istanza 0 VM toohello hello altre macchine virtuali eseguendo uno script personalizzato.
* Creare un'immagine gestita con disco hello del sistema operativo più dischi di dati (con dati hello richiesto) e creare un nuovo scaleset con immagine di hello. In questo modo ogni nuova macchina virtuale creata disporrà di un tipo di dati su disco che viene fornito nella definizione di hello di hello scaleset. Poiché questa definizione farà riferimento tooan immagine con un disco dati che contiene dati personalizzati, ogni macchina virtuale in hello scaleset automaticamente verrà visualizzata con queste modifiche.

> Hello toocreate modo un'immagine personalizzata è disponibili qui: [creare un'immagine gestita di una macchina virtuale generalizzata in Azure](/azure/virtual-machines/windows/capture-image-resource/) 

> utente Hello deve hello toocapture istanza 0 macchina virtuale che dispone di hello dati necessari e quindi utilizzare tale disco rigido virtuale per la definizione dell'immagine hello.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Rimuovere un disco dati da un set di scalabilità
È possibile rimuovere un disco dati da un set di scalabilità di macchine virtuali usando il comando _az vmss disk detach_ dell'interfaccia della riga di comando di Azure. Ad esempio hello comando che segue rimuove il disco di hello definito a lun 2:
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
Analogamente è possibile rimuovere un disco da un set tramite la rimozione di una voce da hello di scalabilità _dataDisks_ proprietà hello _storageProfile_ e applicazione hello modifica. 

## <a name="additional-notes"></a>Note aggiuntive
Il supporto per dischi dati collegati del set di dischi gestiti di Azure e la scala è disponibile nella versione dell'API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) di hello API Microsoft. COMPUTE o versione successiva.

Nell'implementazione iniziale di hello del supporto di dischi collegati per set di scalabilità, è possibile collegare o scollegare i dischi dati di singole macchine virtuali in un set di scalabilità.

Il supporto del portale di Azure per i dischi di dati collegati nei set di scalabilità è inizialmente limitato. A seconda dei requisiti che è possibile utilizzare modelli di Azure, i dischi collegati da toomanage CLI, PowerShell, gli SDK e API REST.



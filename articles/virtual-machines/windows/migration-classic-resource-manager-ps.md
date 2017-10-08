---
title: aaaMigrate tooResource gestione con PowerShell | Documenti Microsoft
description: Questo articolo descrive la migrazione hello supportata dalla piattaforma IaaS risorse quali macchine virtuali (VM), le reti virtuali (reti virtuali) e gli account di archiviazione da tooAzure classico Resource Manager (ARM) utilizzando i comandi di PowerShell di Azure
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Eseguire la migrazione di risorse IaaS da tooAzure classico Gestione risorse tramite Azure PowerShell
Queste procedure illustrano di funzionamento dei comandi toomigrate infrastruttura come un servizio (IaaS) alle risorse dal modello di distribuzione Azure Resource Manager hello distribuzione classica modello toohello toouse Azure PowerShell.

Se si desidera, è anche possibile eseguire la migrazione alle risorse utilizzando hello [Azure interfaccia della riga di comando (CLI di Azure)](../linux/migration-classic-resource-manager-cli.md).

* Per informazioni generali sugli scenari di migrazione supportati, vedere [migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di](migration-classic-resource-manager-overview.md).
* Per istruzioni dettagliate e informazioni dettagliate sulla migrazione, vedere [tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](migration-classic-resource-manager-deep-dive.md).
* [Rivedere gli errori di migrazione più comuni](migration-classic-resource-manager-errors.md)

<br>
Ecco un ordine di hello tooidentify diagramma di flusso in cui è necessario passaggi toobe eseguite durante un processo di migrazione

![Schermata che illustra i passaggi della migrazione hello](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>Passaggio 1: Pianificare la migrazione
Ecco alcune procedure consigliate che è consigliabile quando si valutano la migrazione di risorse IaaS da tooResource classico Manager:

* Leggere hello [supportate e non supportate funzionalità e configurazioni](migration-classic-resource-manager-overview.md). Se si dispone di macchine virtuali che utilizzano le configurazioni non supportate o funzionalità, è consigliabile attendere hello e configurazione delle funzionalità supporto toobe annunciato. In alternativa, se adatto alle proprie esigenze, rimuovere tale funzionalità o esce da tale migrazione tooenable della configurazione.
* Se si sono state automatizzate script da distribuire l'infrastruttura e le applicazioni oggi, provare a toocreate una configurazione di test simile utilizzando gli script per la migrazione. In alternativa, è possibile impostare gli ambienti di esempio di tramite hello portale di Azure.

> [!IMPORTANT]
> Gateway applicazione non sono attualmente supportati per la migrazione da tooResource classico Manager. toomigrate una rete virtuale classica con un gateway di applicazione, rimuovere gateway hello prima dell'esecuzione di una rete di hello toomove operazione Prepare. Dopo aver completato la migrazione di hello, riconnettersi gateway hello in Gestione risorse di Azure.
>
>Gateway ExpressRoute connessione tooExpressRoute circuiti in un'altra sottoscrizione non è possibile eseguire la migrazione automaticamente. In questi casi, è possibile rimuovere gateway ExpressRoute hello, la migrazione della rete virtuale hello e ricreare il gateway di hello. Vedere [ExpressRoute di eseguire la migrazione di circuiti e associate reti virtuali dal modello di distribuzione di gestione risorse toohello classico hello](../../expressroute/expressroute-migration-classic-resource-manager.md) per ulteriori informazioni.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>Passaggio 2: Installare una versione più recente di hello di Azure PowerShell
Esistono due opzioni principali tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) o [installazione guidata piattaforma Web (WebPI)](http://aka.ms/webpi-azps). WebPI riceve aggiornamenti mensili. PowerShell Gallery riceve aggiornamenti su base continua. Questo articolo si basa su Azure PowerShell versione 2.1.0.

Per istruzioni sull'installazione, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>Passaggio 3: Assicurarsi che sia un amministratore per la sottoscrizione di hello nel portale di Azure
tooperform questa migrazione, è necessario essere aggiunto come coamministratore della sottoscrizione hello in hello [portale di Azure](https://portal.azure.com).

1. Sign in hello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, selezionare **sottoscrizione**. Se questa voce non viene visualizzata, selezionare **Altri servizi**.
3. Trovare la voce di hello sottoscrizione appropriata, quindi esaminare hello **ruolo MY** campo. Per un coamministratore, deve essere il valore di hello _amministratore dell'Account_.

Se non si è in grado di tooadd un coamministratore, quindi contattare un amministratore del servizio o coamministratore per tooget sottoscrizione hello aggiunti manualmente.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>Passaggio 4: impostare la sottoscrizione e iscriversi per la migrazione
Avviare prima un prompt di PowerShell. Per la migrazione, è necessario tooset dell'ambiente per entrambi classico e Gestione risorse.

Eseguire l'accesso tooyour account per il modello di gestione risorse hello.

```powershell
    Login-AzureRmAccount
```

Ottenere le sottoscrizioni disponibili hello utilizzando hello comando seguente:

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Impostare la sottoscrizione di Azure per hello sessione corrente. In questo esempio imposta hello nome predefinito della sottoscrizione troppo**iscrizione Azure**. Sostituire nome sottoscrizione di esempio hello con valori personalizzati.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> La registrazione è un passaggio da eseguire una sola volta, ma è necessario provvedervi prima di tentare la migrazione. Senza registrazione, vedrai hello seguente messaggio di errore:
>
> *BadRequest: Subscription is not registered for migration* (Richiesta non valida: la sottoscrizione non è registrata per la migrazione)
>
>

Registrare con provider di risorse di migrazione hello utilizzando hello comando seguente:

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Attendere cinque minuti per hello toofinish di registrazione. È possibile controllare lo stato di hello dell'approvazione hello utilizzando hello comando seguente:

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Assicurarsi che RegistrationState sia `Registered` prima di procedere.

Accedi a questo punto tooyour account per il modello classico hello.

```powershell
    Add-AzureAccount
```

Ottenere le sottoscrizioni disponibili hello utilizzando hello comando seguente:

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Impostare la sottoscrizione di Azure per hello sessione corrente. In questo esempio imposta sottoscrizione predefinita hello troppo**iscrizione Azure**. Sostituire nome sottoscrizione di esempio hello con valori personalizzati.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Passaggio 5: Assicurarsi di disporre di core a sufficienza macchina virtuale di gestione risorse di Azure in hello area della distribuzione corrente o rete virtuale di Azure
È possibile utilizzare hello seguente PowerShell comando toocheck hello numero corrente di core che nel gestore di risorse di Azure. toolearn più sulle quote di core, vedere [limiti e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

Questo esempio viene verificata la disponibilità di hello in hello **Stati Uniti occidentali** area. Sostituire nome dell'area esempio hello con valori personalizzati.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>Passaggio 6: Eseguire i comandi toomigrate le risorse IaaS
> [!NOTE]
> Tutte le operazioni descritte di seguito hello sono idempotenti. Se si dispone di un problema diverso da una funzionalità non supportata o un errore di configurazione, è consigliabile che si riprova hello preparare, interrompere o l'operazione di commit. piattaforma Hello tenta quindi di nuovo l'azione hello.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>Passaggio 6.1: Opzione 1 - Eseguire la migrazione delle macchine virtuali in un servizio cloud (non in una rete virtuale)
Ottenere un elenco di servizi cloud tramite hello comando seguente, quindi selezione hello cloud servizio che si desidera toomigrate hello. Se è hello macchine virtuali nel servizio cloud hello in una rete virtuale o se hanno ruoli web o di lavoro, il comando di hello restituisce un messaggio di errore.

```powershell
    Get-AzureService | ft Servicename
```

Ottenere il nome distribuzione hello per il servizio cloud hello. In questo esempio, è il nome di servizio hello **servizio**. Sostituire nome del servizio di esempio hello con il proprio nome di servizio.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Preparare le macchine virtuali hello nel servizio cloud hello per la migrazione. Si dispone di due opzioni toochoose da.

* **Opzione 1. Eseguire la migrazione di hello macchine virtuali tooa piattaforma rete virtuale creata**

    In primo luogo, verificare se è possibile eseguire la migrazione del servizio cloud hello utilizzando hello seguenti comandi:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Hello comando precedente consente di visualizzare eventuali avvisi ed errori che blocca la migrazione. Se la convalida ha esito positivo, è possibile spostare toohello **Prepare** passaggio:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Opzione 2. Eseguire la migrazione tooan rete virtuale esistente nel modello di distribuzione di gestione risorse di hello**

    In questo esempio imposta hello Nome gruppo di risorse troppo**myResourceGroup**, hello nome di rete virtuale troppo**myVirtualNetwork** e hello nome di subnet troppo**mySubNet**. Sostituire i nomi di hello nell'esempio hello con nomi hello delle proprie risorse.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    In primo luogo, verificare se è possibile eseguire la migrazione di rete virtuale di hello utilizzando hello comando seguente:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Hello comando precedente consente di visualizzare eventuali avvisi ed errori che blocca la migrazione. Se la convalida ha esito positivo, è possibile procedere con hello riportata dopo il passaggio di preparazione:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Dopo l'operazione di preparazione hello ha esito positivo con uno dei precedenti opzioni hello, eseguire una query dello stato di migrazione hello di hello macchine virtuali. Verificare che siano in hello `Prepared` stato.

In questo esempio imposta hello nome della macchina virtuale troppo**myVM**. Sostituire il nome di esempio hello con il proprio nome di macchina virtuale.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

Controllare la configurazione di hello hello preparata risorse con PowerShell o hello portale di Azure. Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente:

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>Passaggio 6.1: Opzione 2 - Eseguire la migrazione delle macchine virtuali in un una rete virtuale

macchine virtuali toomigrate in una rete virtuale, la migrazione della rete virtuale hello. macchine virtuali Hello eseguire automaticamente la migrazione con la rete virtuale hello. Selezione hello rete virtuale che si desidera toomigrate.
> [!NOTE]
> [Eseguire la migrazione di una macchina virtuale classica](migrate-single-classic-to-resource-manager.md) creando una nuova macchina virtuale di gestione delle risorse con i dischi gestiti utilizzando hello (sistema operativo e dati) i file VHD della macchina virtuale hello.
<br>

> [!NOTE]
> nome della rete virtuale Hello potrebbe essere diverso rispetto a quanto mostrato in hello nuovo portale. nuovo portale di Azure Hello Visualizza nome hello come `[vnet-name]` ma il nome di rete virtuale effettivo hello è di tipo `Group [resource-group-name] [vnet-name]`. Prima della migrazione, nome di rete virtuale effettivo hello di ricerca usando il comando di hello `Get-AzureVnetSite | Select -Property Name` oppure visualizzarlo in hello vecchio portale di Azure. 

In questo esempio imposta hello nome di rete virtuale troppo**myVnet**. Sostituire nome di rete virtuale di esempio hello con valori personalizzati.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Se la rete virtuale hello contiene web o ruoli di lavoro o macchine virtuali con configurazioni non supportate, viene visualizzato un messaggio di errore di convalida.
>
>

In primo luogo, verificare se è possibile eseguire la migrazione di rete virtuale hello utilizzando hello comando seguente:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Hello comando precedente consente di visualizzare eventuali avvisi ed errori che blocca la migrazione. Se la convalida ha esito positivo, è possibile procedere con hello riportata dopo il passaggio di preparazione:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Controllare la configurazione di hello hello preparata macchine virtuali con Azure PowerShell o hello portale di Azure. Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente:

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Passaggio 6.2: Eseguire la migrazione di un account di archiviazione
Dopo avere utilizzato la migrazione di macchine virtuali hello, si consiglia di che migrare gli account di archiviazione hello.

Prima di eseguire la migrazione di account di archiviazione hello, eseguire prima i controlli dei prerequisiti:

* **Eseguire la migrazione di macchine virtuali classiche cui dischi vengono archiviati nell'account di archiviazione hello**

    Comando precedente restituisce RoleName e DiskName proprietà di tutti i dischi di macchina virtuale classici hello nell'account di archiviazione hello. RoleName è il nome di hello di hello toowhich di macchina virtuale che è collegato un disco. Se il comando precedente restituisce dischi Assicurarsi quindi che toowhich di macchine virtuali sono collegati i dischi vengono migrati prima della migrazione hello account di archiviazione.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Eliminare classico scollegati dischi di macchina virtuale archiviati nell'account di archiviazione hello**

    Trovare i dischi di macchina virtuale classici nell'archiviazione hello account tramiti il seguente comando:

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Se il comando sopra restituisce uno o più dischi, eliminare tali dischi tramite il seguente comando:

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Immagini di macchina virtuale di eliminazione archiviate nell'account di archiviazione hello**

    Comando precedente restituisce tutte le immagini di macchina virtuale hello con disco del sistema operativo archiviato nell'account di archiviazione hello.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Comando precedente restituisce tutte le immagini di macchina virtuale hello con dischi di dati archiviati nell'account di archiviazione hello.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Eliminare tutte le immagini VM hello restituite da sopra i comandi usando il comando precedente:
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Convalidare ogni account di archiviazione per la migrazione utilizzando hello comando seguente. In questo esempio, nome account di archiviazione hello è **myStorageAccount**. Sostituire il nome di esempio hello con nome hello dell'account di archiviazione.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Passaggio successivo è l'account di archiviazione hello tooPrepare per la migrazione

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Controllare la configurazione di hello hello preparata con Azure PowerShell o hello Azure portale account di archiviazione. Se non si è pronti per la migrazione e si desidera lo stato precedente di toogo toohello indietro, utilizzare hello comando seguente:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Se si verificano problemi configurazione preparata hello, è possibile spostarsi in avanti e commit risorse hello utilizzando hello comando seguente:

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica della migrazione supportata dalla piattaforma IaaS risorse tooAzure classico Gestione risorse di](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Pianificazione della migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utilizzare le risorse IaaS toomigrate CLI da Gestione risorse di tooAzure classico](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Strumenti della community per facilitare la migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Rivedere gli errori di migrazione più comuni](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hello revisione più domande frequenti su IaaS la migrazione di risorse da Gestione risorse di tooAzure classico](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

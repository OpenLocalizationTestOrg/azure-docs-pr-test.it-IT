---
title: "una macchina virtuale (versione classica) con più schede di rete - Azure PowerShell aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una macchina virtuale (versione classica) con più schede di rete con PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>Creare una macchina virtuale (classica) con più schede di interfaccia di rete usando PowerShell

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

È possibile creare macchine virtuali (VM) in Azure e collegare più tooeach (NIC) di interfacce di rete delle macchine virtuali. Più schede di interfaccia rete consentono la separazione dei tipi di traffico tra schede di interfaccia di rete. Ad esempio, una che scheda di rete può comunicare con hello Internet, mentre l'altra comunica solo con le risorse interne non connessi toohello Internet. Hello possibilità tooseparate il traffico di rete tra più schede di rete è necessario per molti dispositivi virtuali di rete, ad esempio distribuzione delle applicazioni e soluzioni per l'ottimizzazione WAN.

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come tooperform questi passaggi tramite hello [il modello di distribuzione di gestione risorse](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.

## <a name="prerequisites"></a>Prerequisiti

Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario. toocreate queste risorse, completate hello passaggi che seguono. Creare una rete virtuale seguendo i passaggi hello hello [creare una rete virtuale](virtual-networks-create-vnet-classic-netcfg-ps.md) articolo.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Creare macchine virtuali di back-end di hello
Hello che macchine virtuali di back-end dipendono dalla creazione di hello di hello seguenti risorse:

* **Subnet Back-end**. server di database Hello faranno parte di una subnet distinta, toosegregate traffico. script Hello riportato di seguito prevede tooexist questa subnet in una rete virtuale denominata *WTestVnet*.
* **Account di archiviazione per dischi dati**. Per ottenere prestazioni migliori, dischi dati hello nei server di database hello utilizzerà la tecnologia di unità SSD allo stato solido, che richiede un account di archiviazione premium. Verificare che hello distribuire archiviazione premium toosupport località di Azure.
* **Set di disponibilità**. Tutti i server di database verranno aggiunti tooa unico set di disponibilità, tooensure almeno una delle macchine virtuali hello sia in esecuzione durante la manutenzione.

### <a name="step-1---start-your-script"></a>Passaggio 1 - avviare lo script
È possibile scaricare hello completo script di PowerShell utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Eseguire operazioni di hello seguenti toochange hello script toowork nell'ambiente in uso.

1. Modificare i valori hello di variabili di hello riportate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [prerequisiti](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Modificare i valori hello di variabili di hello riportate di seguito in base ai valori hello desiderato toouse per la distribuzione di back-end.

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Passaggio 2 - creare le risorse necessarie per le macchine virtuali
È necessario toocreate un nuovo servizio cloud e uno spazio di archiviazione di account per i dischi dati hello per tutte le macchine virtuali. È inoltre necessario toospecify un'immagine e un account amministratore locale per hello macchine virtuali. completare queste risorse, toocreate hello i passaggi seguenti:

1. Creare un nuovo servizio cloud

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Creare un account di archiviazione premium

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Set di account di archiviazione hello creato in precedenza come account di archiviazione per la sottoscrizione corrente hello.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Selezionare un'immagine per hello macchina virtuale.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Impostare le credenziali dell'account amministratore locale hello.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>Passaggio 3 - creare delle macchine virtuali
È necessario un ciclo di toocreate toouse come più macchine virtuali che desidera e creare hello necessarie schede di rete e le macchine virtuali all'interno di ciclo hello. hello toocreate schede di rete e le macchine virtuali, eseguire hello alla procedura seguente.

1. Avviare un `for` hello toorepeat ciclo comandi toocreate una macchina virtuale e due schede di rete come numero di volte in base alle esigenze, in base al valore di hello di hello `$numberOfVMs` variabile.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Creare un `VMConfig` oggetto specificando hello immagine, dimensioni e set di disponibilità per hello macchina virtuale.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Eseguire il provisioning di hello macchina virtuale come macchina virtuale Windows.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Impostare il valore predefinito di hello NIC e assegnare un indirizzo IP statico.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Aggiungere una seconda scheda di rete per ogni macchina virtuale.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Creare dischi toodata per ogni macchina virtuale.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. Creare ogni macchina virtuale e il ciclo di hello finale.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Passaggio 4: hello Esegui script
Ora che è stato scaricato e modificare script hello in base alle proprie esigenze, Run ha script di database di back-end hello toocreate le macchine virtuali con più schede di rete.

1. Salvare lo script ed eseguirlo da hello **PowerShell** prompt dei comandi o **PowerShell ISE**. Verrà visualizzato un output iniziale hello, come illustrato di seguito.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Immettere le informazioni di hello necessari nella richiesta di credenziali hello e fare clic su **OK**. viene restituito l'output di Hello seguente.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded

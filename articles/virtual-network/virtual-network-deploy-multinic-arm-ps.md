---
title: "una macchina virtuale con più schede di rete - Azure PowerShell aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una macchina virtuale con più schede di rete con PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a>Creare una macchina virtuale con più schede di interfaccia di rete usando PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-deploy-multinic-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-deploy-multinic-arm-cli.md)
> * [Modello](virtual-network-deploy-multinic-arm-template.md)
> * [PowerShell (Classic)](virtual-network-deploy-multinic-classic-ps.md) (PowerShell (classico))
> * [Interfaccia della riga di comando di Azure (versione classica)](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.

## <a name="prerequisites"></a>Prerequisiti
Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario. completare queste risorse, toocreate hello i passaggi seguenti:

1. Passare troppo[pagina modello hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Nella pagina toohello destra del modello di hello **gruppo di risorse padre**, fare clic su **distribuire tooAzure**.
3. Se necessario, modificare i valori di parametro hello, quindi seguire i passaggi hello nel gruppo di risorse hello toodeploy portale hello anteprima di Azure.

> [!IMPORTANT]
> Assicurarsi che i nomi degli account di archiviazione siano univoci. In Azure non sono infatti ammessi nomi di account di archiviazione duplicati.
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Creare macchine virtuali di back-end di hello
Hello che macchine virtuali di back-end dipendono dalla creazione di hello di hello seguenti risorse:

* **Account di archiviazione per dischi dati**. Per ottenere prestazioni migliori, dischi dati hello nei server di database hello utilizzerà la tecnologia di unità SSD allo stato solido, che richiede un account di archiviazione premium. Verificare che hello distribuire archiviazione premium toosupport località di Azure.
* **Schede di rete**. Ogni macchina virtuale ha due schede di rete, una per l'accesso al database e una per la gestione.
* **Set di disponibilità**. Tutti i server di database verranno aggiunti tooa unico set di disponibilità, tooensure almeno una delle macchine virtuali hello sia in esecuzione durante la manutenzione.  

### <a name="step-1---start-your-script"></a>Passaggio 1 - avviare lo script
È possibile scaricare hello completo script di PowerShell utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1). Eseguire operazioni di hello seguenti toochange hello script toowork nell'ambiente in uso.

1. Modificare i valori hello di variabili di hello riportate di seguito in base al gruppo di risorse esistente distribuito in precedenza in [prerequisiti](#Prerequisites).

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. Modificare i valori hello di variabili di hello riportate di seguito in base ai valori hello desiderato toouse per la distribuzione di back-end.

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. Recuperare le risorse esistenti di hello necessari per la distribuzione.

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Passaggio 2 - creare le risorse necessarie per le macchine virtuali
È necessario un nuovo gruppo di risorse, un account di archiviazione per i dischi dati hello, toocreate e un gruppo di disponibilità per tutte le macchine virtuali. Le credenziali dell'account amministratore locale hello è alos necessario per ogni macchina virtuale. esecuzione di queste risorse, toocreate hello i passaggi seguenti.

1. Creare un nuovo gruppo di risorse.

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. Creare un nuovo account di archiviazione premium, nel gruppo di risorse hello creato in precedenza.

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. Creare un nuovo set di disponibilità.

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. Ottenere l'amministratore locale hello toobe le credenziali di account utilizzato per ogni macchina virtuale.

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a>Passaggio 3: creare le schede NIC hello e macchine virtuali di back-end
È necessario un ciclo di toocreate toouse come più macchine virtuali che desidera e creare hello necessarie schede di rete e le macchine virtuali all'interno di ciclo hello. hello toocreate schede di rete e le macchine virtuali, eseguire hello alla procedura seguente.

1. Avviare un `for` hello toorepeat ciclo comandi toocreate una macchina virtuale e due schede di rete come numero di volte in base alle esigenze, in base al valore di hello di hello `$numberOfVMs` variabile.
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Creare hello che NIC utilizzato per l'accesso al database.

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. Creare hello che NIC utilizzato per l'accesso remoto. Si noti come questa scheda di rete ha un tooit di gruppo associata.

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. Creare l'oggetto `vmConfig` .

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. Creare due dischi dati per ciascuna macchina virtuale. Notare che i dischi dati hello in account di archiviazione premium hello creato in precedenza.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. Configurare hello del sistema operativo e immagine toobe utilizzato per hello macchina virtuale.

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. Aggiungere hello due schede di rete creati in precedenza toohello `vmConfig` oggetto.

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. Creare disco del sistema operativo hello e hello macchina virtuale. Hello preavviso `}` finale hello `for` ciclo.

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a>Passaggio 4: hello Esegui script
Ora che è stato scaricato e modificare script hello in base alle proprie esigenze, Run ha script di database di back-end hello toocreate le macchine virtuali con più schede di rete.

1. Salvare lo script ed eseguirlo da hello **PowerShell** prompt dei comandi o **PowerShell ISE**. Verrà visualizzato l'output di hello iniziale, come indicato di seguito:

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. Dopo alcuni minuti, compilare la richiesta di credenziali hello e fare clic su **OK**. output di Hello seguente rappresenta una singola macchina virtuale. Si noti hello intero processo ha impiegato toocomplete 8 minuti.

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK

---
title: "aaaCreate e gestire macchine virtuali di Windows Azure che utilizzano più schede di rete | Documenti Microsoft"
description: "Informazioni su come toocreate e gestire macchine Virtuali di Windows che dispone di più tooit collegato a schede di rete tramite modelli di Azure PowerShell o Gestione risorse."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Creare e gestire una macchina virtuale Windows che ha più schede di interfaccia di rete
Macchine virtuali (VM) in Azure può avere più toothem schede (NIC) collegato interfaccia di rete virtuale. Uno scenario comune è toohave subnet diverse per la connettività front-end e back-end, o una rete dedicata tooa monitoraggio o una soluzione di backup. In questo articolo illustra in dettaglio come toocreate una macchina virtuale che dispone di più schede di rete associata tooit. Verrà inoltre descritto come le schede NIC tooadd o rimuovere da una macchina virtuale esistente. Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.

Per informazioni dettagliate, tra cui toocreate vedere più schede di rete all'interno di script PowerShell [distribuzione di macchine virtuali di più schede di rete](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Prerequisiti
Assicurarsi di avere hello [versione più recente di Azure PowerShell installato e configurato](/powershell/azure/overview).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Creare una macchina virtuale con più NIC
Creare prima un gruppo di risorse. esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *EastUs* percorso:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Creare la rete virtuale e le subnet
Uno scenario comune è per una rete virtuale di toohave due o più subnet. Una subnet sia per il traffico front-end, hello altri per il traffico di back-end. tooconnect tooboth subnet, quindi utilizzare più schede di rete nella macchina virtuale.

1. Definire due subnet della rete virtuale con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). esempio Hello definisce subnet hello per *mySubnetFrontEnd* e *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Creare la rete virtuale e le subnet con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). esempio Hello crea una rete virtuale denominata *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Creare più schede di rete
Creare due schede di interfaccia di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Collegare una scheda di rete toohello front-end subnet e una scheda di rete toohello back-end. esempio Hello crea NIC denominata *myNic1* e *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

In genere si crea anche un [il gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) o [bilanciamento del carico](../../load-balancer/load-balancer-overview.md) toohelp gestire e distribuire il traffico tra le macchine virtuali. Hello [dettagliate più schede di rete VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) articolo illustra la creazione di un gruppo di sicurezza di rete e l'assegnazione delle schede di rete.

### <a name="create-hello-virtual-machine"></a>Creare una macchina virtuale hello
Ora avviare toobuild configurazione della macchina virtuale. Ogni dimensione della macchina virtuale ha un limite per il numero totale di schede di rete che è possibile aggiungere VM tooa hello. Per altre informazioni, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md).

1. Impostare il toohello credenziali VM `$cred` variabile come indicato di seguito:

    ```powershell
    $cred = Get-Credential
    ```

2. Definire la VM con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). esempio Hello definisce una macchina virtuale denominata *myVM* e si utilizza una dimensione di macchina virtuale che supporta più di due schede di rete (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Creare il resto di hello della configurazione della macchina virtuale con [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Hello di esempio seguente crea una macchina virtuale di Windows Server 2016:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Collegare hello due schede di rete creato in precedenza con [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Creare infine la VM con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Aggiungere un tooan NIC VM esistente
aggiungere un tooan NIC virtuale macchina virtuale esistente, si dealloca hello VM, tooadd hello NIC virtuale, quindi avviare hello macchina virtuale.

1. Deallocare hello macchina virtuale con [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). esempio Hello dealloca hello macchina virtuale denominata *myVM* in *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Ottenere la configurazione esistente di hello di hello VM con [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello *myVM* in *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. esempio Hello crea una scheda di rete virtuale con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) denominato *myNic3* collegato troppo*mySubnetBackEnd*. Hello NIC virtuale viene quindi collegato toohello macchina virtuale denominata *myVM* in *myResourceGroup* con [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>Schede di interfaccia di rete virtuale primarie
    Una delle schede di rete in una macchina virtuale multi-NIC hello deve toobe primario. Se una delle schede di rete virtuale esistente di hello in hello VM è già impostato come primario, è possibile ignorare questo passaggio. Hello seguente si presuppone che due schede di rete virtuale sono ora presenti in una macchina virtuale e si desidera tooadd hello prima NIC (`[0]`) come hello primario:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Avvia macchina virtuale con hello [inizio AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Rimuovere una scheda di interfaccia di rete da una VM esistente
tooremove una scheda di rete virtuale da una macchina virtuale esistente, deallocare hello macchina virtuale, rimuovere hello NIC virtuale, quindi avviare hello macchina virtuale.

1. Deallocare hello macchina virtuale con [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). esempio Hello dealloca hello macchina virtuale denominata *myVM* in *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Ottenere la configurazione esistente di hello di hello VM con [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello *myVM* in *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Ottenere informazioni su hello NIC rimuovere con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Hello seguente esempio ottiene informazioni sul *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Rimuovere hello NIC con [Remove AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) , quindi aggiornare hello macchina virtuale con [aggiornamento AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm). Hello esempio seguente viene rimosso *myNic3* ottenuta da `$nicId` nel precedente passaggio hello:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Avvia macchina virtuale con hello [inizio AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Creare più schede di interfaccia di rete con i modelli
Modelli di gestione risorse di Azure forniscono un modo toocreate più istanze di una risorsa durante la distribuzione, ad esempio la creazione di più schede di rete. Modelli di gestione risorse utilizzano dichiarativa JSON file toodefine l'ambiente. Per altre informazioni, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). È possibile utilizzare *copia* numero hello toospecify di toocreate istanze:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Per altre informazioni, vedere [Creazione di più istanze con *copy*](../../resource-group-create-multiple.md). 

È inoltre possibile utilizzare `copyIndex()` tooappend un nome di risorsa tooa numero. È quindi possibile creare *myNic1*, *MyNic2* e così via. Hello codice riportato di seguito viene illustrato un esempio di aggiunta di valore di indice hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

È possibile consultare un esempio completo di [creazione di più schede di interfaccia di rete tramite i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Passaggi successivi
Revisione [dimensioni delle macchine Virtuali di Windows](sizes.md) quando si cerca toocreate una macchina virtuale che dispone di più schede di rete. Prestare attenzione toohello massimo schede di rete che supporta ogni dimensione della macchina virtuale. 



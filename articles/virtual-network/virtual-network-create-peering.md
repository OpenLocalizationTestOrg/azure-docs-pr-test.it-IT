---
title: aaaCreate un peering di rete virtuale di Azure - Gestione risorse - stessa sottoscrizione | Documenti Microsoft
description: Informazioni su come toocreate un peering di rete virtuale tra reti virtuali create tramite Gestione risorse presenti in hello stessa sottoscrizione di Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Creare un peering di rete virtuale - Resource Manager, stessa sottoscrizione

In questa esercitazione viene illustrato toocreate peering tra reti virtuali create tramite Gestione risorse di rete virtuale. Entrambe le reti virtuali presenti in hello stessa sottoscrizione. Peering due risorse di consente di reti virtuali in reti virtuali diverse toocommunicate reciprocamente con hello stessa larghezza di banda e latenza, come se fosse di risorse hello in hello stessa rete virtuale. Altre informazioni sul [Peering di rete virtuale](virtual-network-peering-overview.md). 

Hello passaggi toocreate un peering di reti virtuali sono diversi, a seconda che le reti virtuali hello siano hello uguale o diverso, sottoscrizioni e che [modello di distribuzione Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) vengono create le reti virtuali hello tramite. Informazioni su come toocreate un virtuale rete peering in altri scenari, fare clic su uno scenario di hello di hello nella tabella seguente:

|Modello di distribuzione di Azure  | Sottoscrizione di Azure  |
|--------- |---------|
|[Entrambi con Resource Manager](create-peering-different-subscriptions.md) |Diversa|
|[Uno con Resource Manager, uno con una distribuzione classica](create-peering-different-deployment-models.md) |Uguale|
|[Uno con Resource Manager, uno con una distribuzione classica](create-peering-different-deployment-models-subscriptions.md) |Diversa|

Impossibile creare una rete virtuale peering tra due reti virtuali distribuite tramite il modello di distribuzione classica hello. Un peering di reti virtuali può essere creato solo tra due reti virtuali presenti in hello stessa regione di Azure. Se è necessario tooconnect reti virtuali che sono stati creati tramite il modello di distribuzione classica hello o che esistono in diverse aree di Azure, è possibile utilizzare un Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello reti virtuali. 

È possibile utilizzare hello [portale di Azure](#portal), hello Azure [interfaccia della riga di comando](#cli) (CLI), Azure [PowerShell](#powershell), o un [modellodigestionerisorsediAzure](#template) toocreate un peering di rete virtuale. Fare clic su uno qualsiasi dei hello precedente dello strumento collegamenti toogo direttamente toohello i passaggi per la creazione di una rete virtuale peering utilizzando lo strumento di scelta.

## <a name="portal"></a>Creare un peering - Portale di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com). account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
2. Fare clic su **+ Nuovo**, **Rete** e quindi **Rete virtuale**.
3. In hello **crea rete virtuale** pannello, immettere o selezionare i valori per hello seguenti impostazioni, quindi fare clic su **crea**:
    - **Nome**: *myVnet1*
    - **Spazio indirizzi**: *10.0.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.0.0.0/24*
    - **Sottoscrizione**: selezionare la propria sottoscrizione
    - **Gruppo di risorse**: selezionare **Crea nuovo** e immettere *myResourceGroup*
    - **Località**: *Stati Uniti orientali*
4. Completare i passaggi da 2-3 nuovamente specificando hello seguenti valori nel passaggio 3:
    - **Nome**: *myVnet2*
    - **Spazio indirizzi**: *10.1.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.1.0.0/24*
    - **Sottoscrizione**: selezionare la propria sottoscrizione
    - **Gruppo di risorse**: selezionare **Usa esistente** e quindi *myResourceGroup*
    - **Località**: *Stati Uniti orientali*
5. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myResourceGroup*. Fare clic su **myResourceGroup** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myresourcegroup** gruppo di risorse. gruppo di risorse Hello contiene hello due reti virtuali create nei passaggi precedenti.
6. Fare clic su **myVNet1**.
7. In hello **myVnet1** pannello visualizzato, fare clic su **peering** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello.
8. In hello **myVnet1 - peering** blade che venivano visualizzate, fare clic su **+ Aggiungi**
9. In hello **Aggiungi peering** blade che viene visualizzata, immettere o selezionare hello le opzioni seguenti, quindi fare clic su **OK**:
     - **Nome**: *myVnet1ToMyVnet2*
     - **Modello di distribuzione della rete virtuale**: selezionare **Resource Manager**. 
     - **Sottoscrizione**: selezionare la propria sottoscrizione
     - **Rete virtuale**: fare clic su **Scegliere una rete virtuale** e quindi scegliere **myVnet2**.
     - **Consenti accesso alla rete virtuale:** assicurarsi che sia selezionato **Abilitato**.
    Questa esercitazione non prevede l'uso di altre impostazioni. lettura toolearn su tutte le impostazioni peer, [gestire peering di reti virtuali](virtual-network-manage-peering.md#create-a-peering).
10. Dopo aver fatto clic **OK** nel passaggio precedente hello, hello **Aggiungi peering** pannello chiude e viene visualizzato hello **myVnet1 - peering** pannello nuovamente. Dopo alcuni secondi, hello peering creato viene visualizzato nel pannello hello. **Avviato** è elencato nella hello **stato PEERING** colonna per hello **myVnet1ToMyVnet2** peering è creato. Si è stato effettuato il peering tooVnet2 Vnet1, ma ora è necessario connettersi myVnet2 toomyVnet1. peering Hello è necessario creare in entrambe le direzioni risorse tooenable hello toocommunicate di reti virtuali tra loro.
11. Completare di nuovo i passaggi da 5 a 10 per myVnet2.  Nome hello peering *myVnet2ToMyVnet1*.
12. Pochi secondi dopo aver fatto clic **OK** toocreate hello peering per MyVnet2, hello **myVnet2ToMyVnet1** peering appena creato viene elencato con **connesso** in hello  **Lo stato di PEERING** colonna.
13. Completare di nuovo i passaggi da 5 a 7 per MyVnet1. Hello **stato PEERING** per hello **myVnet1ToVNet2** peering fa ora parte anche **connesso**. peering Hello è stata stabilita correttamente dopo aver visualizzato **connesso** in hello **stato PEERING** colonna per entrambe le reti virtuali nel peering hello.
14. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
15. **Facoltativo**: le risorse di hello toodelete creati in questa esercitazione, hello completo di passaggi di hello [eliminare risorse](#delete-portal) sezione di questo articolo.

Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Creare un peering - Interfaccia della riga di comando di Azure

Hello lo script seguente:

- Richiede hello Azure CLI versione 2.0.4 o versioni successive. versione di hello toofind, eseguire hello `az --version` comando. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Funziona in una shell Bash. Per opzioni all'esecuzione di script CLI di Azure su client Windows, vedere [in esecuzione hello CLI di Azure in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Anziché installare hello CLI e le relative dipendenze, è possibile utilizzare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. Fare clic su hello **provarla** pulsante nello script hello tooyour accedere indicato di seguito, che richiama una Shell di Cloud che consente l'accesso con account di Azure. tooexecute hello script, fare clic su hello **copia** pulsante e incollare il contenuto di hello nella Shell Cloud.

1. Creare un gruppo di risorse e due reti virtuali.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Creare una rete virtuale peering tra due reti virtuali hello.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Dopo l'esecuzione di script hello esaminare hello peering per ogni rete virtuale. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Rieseguire hello precedente comando, sostituendo *myVnet1* con *myVnet2*. Mostra i comandi di output di Hello di entrambi **connesso** in hello **PeeringState** colonna.

     Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
5. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-cli) in questo articolo.


## <a name="powershell"></a>Creare un peering - PowerShell

1. Installare hello l'ultima versione di hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. toostart una sessione di PowerShell, andare troppo**avviare**, immettere **powershell**, quindi fare clic su **PowerShell**.
3. In PowerShell, accedere tooAzure immettendo hello `login-azurermaccount` comando. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
4. Creare un gruppo di risorse e due reti virtuali. script hello tooexecute seguente hello copia dello script, incollarlo in PowerShell e quindi premere `Enter` dopo l'ultima riga hello viene visualizzata nella schermata di hello:

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Creare una rete virtuale peering tra due reti virtuali hello. Esempio hello copia dello script, incollare in tooPowerShell e quindi premere `Enter` dopo l'ultima riga hello viene visualizzata nella schermata di hello:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview hello subnet per la rete virtuale hello, seguente hello copia comando, incollare in tooPowerShell e quindi premere `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Rieseguire hello precedente comando, sostituendo *myVnet1* con *myVnet2*. Mostra i comandi di output di Hello di entrambi **connesso** in hello **PeeringState** colonna.
7. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
8. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-powershell) in questo articolo.

Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Creare un peering - Modello di Resource Manager

1. Fare riferimento al modello di Resource Manager per [creare un peering di rete virtuale](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering). Le istruzioni vengono forniti con il modello di hello per la distribuzione modello hello utilizzando hello hello Azure CLI, PowerShell o il portale di Azure. Log nello strumento toowhichever scelto toodeploy hello modello con un account che dispone hello toocreate delle autorizzazioni necessarie a una rete virtuale peering. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
2. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
3. **Facoltativo**: le risorse di hello toodelete creati in questa esercitazione, hello completo di passaggi di hello [eliminare risorse](#delete) sezione di questo articolo, utilizzando hello hello Azure CLI, PowerShell o il portale di Azure.

## <a name="permissions"></a>Autorizzazioni

Hello che è utilizzare una rete virtuale peering toocreate devono disporre hello necessarie ruolo o autorizzazioni. Ad esempio, se si sono stati peering due reti virtuali denominate VNet1 e VNet2, all'account deve essere assegnato hello seguente ruolo minimo o autorizzazioni per ogni rete virtuale:
    
|Rete virtuale|Ruolo|Autorizzazioni|
|---|---|---|
|VNet1|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Altre informazioni, vedere [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e l'assegnazione di autorizzazioni specifiche troppo[ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Gestione risorse (solo).

## <a name="delete"></a>Eliminare risorse
Al termine di questa esercitazione, è possibile risorse hello toodelete creato nell'esercitazione di hello, in modo non si incorrere in costi di utilizzo. Un gruppo di risorse anche se si elimina tutte le risorse che si trovano nel gruppo di risorse hello.

### <a name="delete-portal"></a>Portale di Azure

1. Nella casella di ricerca portale hello, immettere **myResourceGroup**. Nei risultati della ricerca hello, fare clic su **myResourceGroup**.
2. In hello **myResourceGroup** pannello, fare clic su hello **eliminare** icona.
3. l'eliminazione di hello tooconfirm, in hello **hello di tipo nome gruppo di risorse** immettere **myResourceGroup**, quindi fare clic su **eliminare**.

### <a name="delete-cli"></a>

Immettere hello comando seguente:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Immettere hello comando seguente:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Passaggi successivi

- Acquisire familiarità con importanti [vincoli e comportamenti del peering di rete virtuale](virtual-network-manage-peering.md#requirements-and-constraints) prima di creare un peering di rete virtuale per l'uso in produzione.
- Acquisire informazioni più dettagliate su tutte le [impostazioni per il peering di rete virtuale](virtual-network-manage-peering.md#create-a-peering).
- Informazioni su come troppo[creare un hub e spoke topologia di rete](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con peering di rete virtuale.

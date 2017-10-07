---
title: aaaCreate virtuale di Azure di rete peer - diversi modelli di distribuzione - stessa sottoscrizione | Documenti Microsoft
description: Informazioni su come toocreate un peering di rete virtuale tra reti virtuali creati tramite i modelli di distribuzione di Azure diversi esistono in hello stessa sottoscrizione di Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Creare un peering di rete virtuale: diversi modelli di distribuzione, stessa sottoscrizione 

In questa esercitazione viene illustrato toocreate una rete virtuale peering tra reti virtuali create tramite diversi modelli di distribuzione. Entrambe le reti virtuali presenti in hello stessa sottoscrizione. Peering due risorse di consente di reti virtuali in reti virtuali diverse toocommunicate reciprocamente con hello stessa larghezza di banda e latenza, come se fosse di risorse hello in hello stessa rete virtuale. Altre informazioni sul [Peering di rete virtuale](virtual-network-peering-overview.md). 

Hello passaggi toocreate un peering di reti virtuali sono diversi, a seconda che le reti virtuali hello siano hello uguale o diverso, sottoscrizioni e che [modello di distribuzione Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) vengono create le reti virtuali hello tramite. Informazioni su come toocreate un virtuale rete peering in altri scenari, fare clic su uno scenario di hello di hello nella tabella seguente:

|Modello di distribuzione di Azure  | Sottoscrizione di Azure  |
|--------- |---------|
|[Entrambi con Resource Manager](virtual-network-create-peering.md) |Uguale|
|[Entrambi con Resource Manager](create-peering-different-subscriptions.md) |Diversa|
|[Uno con Resource Manager, uno con la distribuzione classica](create-peering-different-deployment-models-subscriptions.md) |Diversa|

Impossibile creare una rete virtuale peering tra due reti virtuali distribuite tramite il modello di distribuzione classica hello. Un peering di reti virtuali può essere creato solo tra due reti virtuali presenti in hello stessa regione di Azure. Se è necessario tooconnect reti virtuali che sono stati creati tramite il modello di distribuzione classica hello o che esistono in diverse aree di Azure, è possibile utilizzare un Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello reti virtuali. 

È possibile utilizzare hello [portale di Azure](#portal), hello Azure [interfaccia della riga di comando](#cli) (CLI), o Azure [PowerShell](#powershell) toocreate un peering di rete virtuale. Fare clic su uno qualsiasi dei hello precedente dello strumento collegamenti toogo direttamente toohello i passaggi per la creazione di una rete virtuale peering utilizzando lo strumento di scelta.

## <a name="cli"></a>Creare un peering - Portale

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
4. Fare clic su **+ Nuovo**. In hello **hello ricerca Marketplace** digitare *rete virtuale*. Fare clic su **rete virtuale** quando viene visualizzato nei risultati della ricerca hello. 
5. In hello **rete virtuale** pannello seleziona **classico** in hello **selezionare un modello di distribuzione** casella e quindi fare clic su **crea**.
6. In hello **crea rete virtuale** pannello, immettere o selezionare i valori per hello seguenti impostazioni, quindi fare clic su **crea**:
    - **Nome**: *myVnet2*
    - **Spazio indirizzi**: *10.1.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.1.0.0/24*
    - **Sottoscrizione**: selezionare la propria sottoscrizione
    - **Gruppo di risorse**: selezionare **Usa esistente** e quindi *myResourceGroup*
    - **Località**: *Stati Uniti orientali*
7. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myResourceGroup*. Fare clic su **myResourceGroup** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myresourcegroup** gruppo di risorse. gruppo di risorse Hello contiene hello due reti virtuali create nei passaggi precedenti.
8. Fare clic su **myVNet1**.
9. In hello **myVnet1** pannello visualizzato, fare clic su **peering** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello.
10. In hello **myVnet1 - peering** blade che venivano visualizzate, fare clic su **+ Aggiungi**
11. In hello **Aggiungi peering** blade che viene visualizzata, immettere o selezionare hello le opzioni seguenti, quindi fare clic su **OK**:
     - **Nome**: *myVnet1ToMyVnet2*
     - **Modello di distribuzione della rete virtuale**: selezionare **Classica**. 
     - **Sottoscrizione**: selezionare la propria sottoscrizione
     - **Rete virtuale**: fare clic su **Scegliere una rete virtuale** e quindi scegliere **myVnet2**.
     - **Consenti accesso alla rete virtuale:** assicurarsi che sia selezionato **Abilitato**.
    Questa esercitazione non prevede l'uso di altre impostazioni. lettura toolearn su tutte le impostazioni peer, [gestire peering di reti virtuali](virtual-network-manage-peering.md#create-a-peering).
12. Dopo aver fatto clic **OK** nel passaggio precedente hello, hello **Aggiungi peering** pannello chiude e viene visualizzato hello **myVnet1 - peering** pannello nuovamente. Dopo alcuni secondi, hello peering creato viene visualizzato nel pannello hello. **Connesso** è elencato nella hello **stato PEERING** colonna per hello **myVnet1ToMyVnet2** peering è creato.

    Hello peering viene stabilito ora. Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
14. **Facoltativo**: le risorse di hello toodelete creati in questa esercitazione, hello completo di passaggi di hello [eliminare risorse](#delete-portal) sezione di questo articolo.

## <a name="cli"></a>Creare un peering - Interfaccia della riga di comando di Azure

1. [Installare](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) rete virtuale di hello toocreate hello Azure CLI 1.0 (classico).
2. Aprire una sessione di comando e accedere utilizzando hello tooAzure `azure login` comando.
3. Eseguire hello CLI in modalità di gestione del servizio immettendo hello `azure config mode asm` comando.
4. Immettere hello comando toocreate hello rete virtuale (classico) seguente:
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Creare un gruppo di risorse e una rete virtuale con Resource Manager. È possibile utilizzare hello CLI 1.0 o 2.0 ([installare](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). In questa esercitazione, hello 2.0 CLI è usato toocreate hello rete virtuale (Resource Manager), poiché 2.0 deve essere utilizzato toocreate hello peering. Eseguire hello seguente bash script CLI dal computer locale con hello CLI 2.0.4 installato o versione successiva. Per le opzioni di esecuzione bash script CLI su client Windows, vedere [in esecuzione hello CLI di Azure in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). È anche possibile eseguire script di hello utilizzando hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. Fare clic su hello **provarla** pulsante nello script hello tooyour accedere indicato di seguito, che richiama una Shell di Cloud che consente l'accesso con account di Azure. tooexecute hello script, fare clic su hello **copia** pulsante e Incolla, il contenuto di hello nella Shell Cloud, quindi premere `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Creare una rete virtuale peering tra hello due reti virtuali create tramite hello diversi modelli di distribuzione. Lo script seguente hello copia viene tooa editor di testo sul PC. Sostituire `<subscription id>` con l'ID della sottoscrizione. Se non si conosce l'Id sottoscrizione, immettere hello `az account show` comando. valore per Hello **id** in hello l'output è l'ID sottoscrizione. Incollare hello modificato script nella sessione CLI tooyour e quindi premere `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Dopo l'esecuzione di script hello esaminare hello peering per la rete virtuale hello Gestione risorse (). Comando seguente hello copia, incollarlo nella sessione CLI e quindi premere `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    output di Hello Visualizza **connesso** in hello **PeeringState** colonna. 

    Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
9. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-cli) in questo articolo.

## <a name="powershell"></a>Creare un peering - PowerShell

1. Installare hello l'ultima versione di hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) e [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) moduli. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Avviare una sessione di PowerShell.
3. In PowerShell, accedere tooAzure immettendo hello `Add-AzureAccount` comando.
4. toocreate una rete virtuale (classica) con PowerShell, è necessario creare una nuova o modificarne un esistente, il file di configurazione di rete. Informazioni su come troppo[esportare, aggiornare e importare il file di configurazione di rete](virtual-networks-using-network-configuration-file.md). Hello file deve includere il seguente hello **VirtualNetworkSite** elemento per la rete virtuale di hello utilizzati in questa esercitazione:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > L'importazione di un file di configurazione di rete modificato può causare modifiche tooexisting reti virtuali (classiche) nella sottoscrizione. Assicurarsi di aggiungere solo reti virtuali precedente hello e di non modificare o rimuovere qualsiasi rete virtuale esistente dalla sottoscrizione. 
5. Accedere in rete virtuale di hello toocreate tooAzure (gestione delle risorse) immettendo hello `login-azurermaccount` comando. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
6. Creare un gruppo di risorse e una rete virtuale con Resource Manager. Copiare script hello, incollarlo in PowerShell e quindi premere `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Creare una rete virtuale peering tra hello due reti virtuali create tramite hello diversi modelli di distribuzione. Lo script seguente hello copia viene tooa editor di testo sul PC. Sostituire `<subscription id>` con l'ID della sottoscrizione. Se non si conosce l'Id sottoscrizione, immettere hello `Get-AzureRmSubscription` tooview comando è. valore per Hello **Id** in hello restituito l'output è l'ID sottoscrizione. script hello tooexecute, lo script dall'editor di testo modificato di hello copia, quindi fare doppio clic nella sessione di PowerShell e quindi premere `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Dopo l'esecuzione di script hello esaminare hello peering per la rete virtuale hello Gestione risorse (). Comando seguente hello copia, incollarlo nella sessione di PowerShell e quindi premere `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    output di Hello Visualizza **connesso** in hello **PeeringState** colonna.

    Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
10. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-powershell) in questo articolo.
 
## <a name="permissions"></a>Autorizzazioni

Hello che è utilizzare una rete virtuale peering toocreate devono disporre hello necessarie ruolo o autorizzazioni. Ad esempio, se si sono stati peering due reti virtuali denominate myVnet1 e myVnet2, all'account deve essere assegnato hello seguente ruolo minimo o autorizzazioni per ogni rete virtuale:
    
|Rete virtuale|Modello di distribuzione|Ruolo|Autorizzazioni|
|---|---|---|---|
|myVnet1|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnet2|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Altre informazioni, vedere [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e l'assegnazione di autorizzazioni specifiche troppo[ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Gestione risorse (solo).

## <a name="delete"></a>Eliminare risorse
Al termine di questa esercitazione, è possibile risorse hello toodelete creato nell'esercitazione di hello, in modo non si incorrere in costi di utilizzo. Un gruppo di risorse anche se si elimina tutte le risorse che si trovano nel gruppo di risorse hello.

### <a name="delete-portal"></a>Portale di Azure

1. Nella casella di ricerca portale hello, immettere **myResourceGroup**. Nei risultati della ricerca hello, fare clic su **myResourceGroup**.
2. In hello **myResourceGroup** pannello, fare clic su hello **eliminare** icona.
3. l'eliminazione di hello tooconfirm, in hello **hello di tipo nome gruppo di risorse** immettere **myResourceGroup**, quindi fare clic su **eliminare**.

### <a name="delete-cli"></a>

1. Usare la rete virtuale di hello toodelete hello Azure CLI 2.0 Gestione risorse () con hello comando seguente:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Usare la rete virtuale di hello toodelete hello Azure CLI 1.0 (versione classica) con hello seguenti comandi:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Immettere hello comando toodelete hello (Resource Manager) di rete virtuale seguente:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete hello rete virtuale (classico) con PowerShell, è necessario modificare un file di configurazione di rete esistente. Informazioni su come troppo[esportare, aggiornare e importare il file di configurazione di rete](virtual-networks-using-network-configuration-file.md). Rimuovere hello elemento VirtualNetworkSite per la rete virtuale di hello utilizzati in questa esercitazione seguente:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > L'importazione di un file di configurazione di rete modificato può causare modifiche tooexisting reti virtuali (classiche) nella sottoscrizione. Assicurarsi di rimuovere solo la rete virtuale precedente di hello e di non modificare o rimuovere qualsiasi altra rete virtuale esistente dalla sottoscrizione. 

## <a name="next-steps"></a>Passaggi successivi

- Acquisire familiarità con importanti [vincoli e comportamenti del peering di rete virtuale](virtual-network-manage-peering.md#requirements-and-constraints) prima di creare un peering di rete virtuale per l'uso in produzione.
- Acquisire informazioni più dettagliate su tutte le [impostazioni per il peering di rete virtuale](virtual-network-manage-peering.md#create-a-peering).
- Informazioni su come troppo[creare un hub e spoke topologia di rete](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con peering di rete virtuale.

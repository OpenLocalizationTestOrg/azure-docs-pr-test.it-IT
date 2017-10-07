---
title: "una rete virtuale di Azure (classica) con più subnet aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una rete virtuale (classica) con più subnet in Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Creare una rete virtuale (classica) con più subnet

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Microsoft consiglia di creare la maggior parte delle nuove reti virtuali tramite hello [Gestione risorse](virtual-networks-create-vnet-arm-pportal.md) modello di distribuzione.

In questa esercitazione, informazioni su come toocreate una base rete virtuale di Azure (versione classica) con separati subnet pubblica e privata. È possibile creare risorse di Azure, ad esempio macchine virtuali e servizi cloud in una subnet. Le risorse create in reti virtuali (classico) possono comunicare tra loro e con le risorse di rete virtuale di tooa connesso altre reti.

Altre informazioni su tutte le impostazioni relative alla [rete virtuale](virtual-network-manage-network.md) e alla [subnet](virtual-network-manage-subnet.md).

> [!WARNING]
> Le reti virtuali (classica) vengono eliminate immediatamente da Azure quando una [sottoscrizione viene disabilitata](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Reti virtuali (classiche) vengono eliminate indipendentemente dall'esistono di risorse nella rete virtuale hello. Se si abilita di nuovo sottoscrizione hello in un secondo momento, è necessario ricreare le risorse presenti nella rete virtuale hello.

È possibile creare una rete virtuale (versione classica) con hello [portale di Azure](#portal), hello [Azure interfaccia della riga di comando (CLI) 1.0](#azure-cli), o [PowerShell](#powershell).

## <a name="portal"></a>di Microsoft Azure

1. In un browser Internet, visitare toohello [portale di Azure](https://portal.azure.com). Accedere usando l'[account Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Fare clic su **+ nuovo** nel portale di hello.
3. Immettere *rete virtuale* in hello **hello ricerca Marketplace** casella nella parte superiore di hello di hello **New** pannello visualizzato.  Fare clic su **rete virtuale** quando viene visualizzato nei risultati della ricerca hello.
4. Selezionare **classico** in hello **selezionare un modello di distribuzione** casella hello **rete virtuale** pannello visualizzato, quindi fare clic su **crea**. 
5. Immettere hello seguendo i valori hello **crea rete virtuale (classico)** blade e quindi fare clic su **crea**:

    |Impostazione|Valore|
    |---|---|
    |Nome|myVnet|
    |Spazio degli indirizzi|10.0.0.0/16|
    |Nome della subnet|Pubblico|
    |Intervallo di indirizzi subnet|10.0.0.0/24|
    |Gruppo di risorse|Lasciare selezionata l'opzione **Crea nuovo** e quindi immettere **myResourceGroup**.|
    |Sottoscrizione e località|Selezionare la sottoscrizione e la posizione.

    Se si tooAzure nuovo, altre informazioni, vedere [gruppi di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [percorsi](https://azure.microsoft.com/regions) (definita anche tooas *aree*).
4. Nel portale di hello, è possibile creare una sola subnet quando si crea una rete virtuale. In questa esercitazione, creare una subnet secondo dopo aver creato la rete virtuale hello. In un secondo momento, è possibile creare le risorse accessibili da Internet in hello **pubblica** subnet. È anche possibile creare le risorse che non sono accessibili da Internet Ciao hello **privata** subnet. toocreate hello secondo subnet, immettere **myVnet** in hello **individuare risorse** casella nella parte superiore di hello della pagina hello. Fare clic su **myVnet** quando viene visualizzato nei risultati della ricerca hello.
5. Fare clic su **subnet** (in hello **impostazioni** sezione) su hello **crea rete virtuale (classico)** pannello visualizzato.
6. Fare clic su **+ Aggiungi** su hello **myVnet - subnet** pannello visualizzato.
7. Immettere **privata** per **nome** su hello **aggiungere subnet** blade. Immettere **10.0.1.0/24** per **Intervallo indirizzi**.  Fare clic su **OK**.
8. In hello **myVnet - subnet** pannello, è possibile visualizzare hello **pubblica** e **privata** subnet a cui è stato creato.
9. **Parametro facoltativo**: al termine di questa esercitazione, è possibile risorse hello toodelete creato, in modo che non si incorrere in costi di utilizzo:
    - Fare clic su **Panoramica** su hello **myVnet** blade.
    - Fare clic su hello **eliminare** icona su hello **myVnet** blade.
    - l'eliminazione di hello tooconfirm, fare clic su **Sì** in hello **rete virtuale Delete** casella.

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

1. È possibile [installare e configurare hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), oppure utilizzare hello CLI all'interno di hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. Guida di tooget per i comandi CLI, digitare `azure <command> --help`. 
2. In una sessione CLI, accedi tooAzure con il comando che segue hello. Se si fa clic **provarla** nella casella hello sottostante, consente di aprire una Shell di Cloud. Tooyour sottoscrizione di Azure, è possibile accedere senza dover immettere hello comando seguente:

    ```azurecli-interactive
    azure login
    ```

3. hello tooensure CLI è in modalità di gestione dei servizi, immettere hello comando seguente:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Creare una rete virtuale con una subnet privata:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Creare una subnet pubblica all'interno di rete virtuale hello:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Esaminare la rete virtuale hello e subnet:

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Parametro facoltativo**: È possibile che le risorse di hello toodelete creato al termine di questa esercitazione, in modo che non si incorrere in costi di utilizzo:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Se non è possibile specificare un toocreate gruppo di risorse una rete virtuale (classica) utilizzando hello CLI, Azure crea rete virtuale hello in un gruppo di risorse denominato *predefinito rete*.

## <a name="powershell"></a>PowerShell

1. Installare hello l'ultima versione di hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) modulo. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Avviare una sessione di PowerShell.
3. In PowerShell, accedere tooAzure immettendo hello `Add-AzureAccount` comando.
4. Modificare l'esempio hello percorso e nome file, come appropriato, quindi esportare il file di configurazione di rete esistente:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate una rete virtuale con subnet pubbliche e private, utilizzare qualsiasi hello tooadd editor di testo **VirtualNetworkSite** elemento che segue toohello file di configurazione di rete.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Hello revisione completa [schema di file di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Importare i file di configurazione di rete hello:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > L'importazione di un file di configurazione di rete modificato può causare modifiche tooexisting reti virtuali (classiche) nella sottoscrizione. Assicurarsi di aggiungere solo reti virtuali precedente hello e di non modificare o rimuovere qualsiasi rete virtuale esistente dalla sottoscrizione. 

7. Esaminare la rete virtuale hello e subnet:

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Parametro facoltativo**: È possibile che le risorse di hello toodelete creato al termine di questa esercitazione, in modo che non si incorrere in costi di utilizzo. toodelete hello rete virtuale completezza i passaggi da 4 a 6 nuovamente questo hello rimozione ora **VirtualNetworkSite** elemento aggiunto nel passaggio 5.
 
> [!NOTE]
> Se non è possibile specificare un toocreate gruppo di risorse una rete virtuale (classica) nell'utilizzo di PowerShell, Azure crea rete virtuale hello in un gruppo di risorse denominato *predefinito rete*.

---

## <a name="next-steps"></a>Passaggi successivi

- toolearn su tutte le reti virtuali e le impostazioni di subnet, vedere [gestire reti virtuali](virtual-network-manage-network.md) e [gestire subnet della rete virtuale](virtual-network-manage-subnet.md). Si sono disponibili varie opzioni per l'utilizzo di reti virtuali e le subnet in una diversi requisiti toomeet ambiente produzione.
- toofilter in ingresso e in uscita traffico della subnet, creare e applicare [gruppi di sicurezza di rete](virtual-networks-nsg.md) toosubnets.
- Creare un [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) macchina virtuale, quindi connetterla tooan una rete virtuale esistente.
- reti virtuali tooconnect due in hello nello stesso percorso di Azure, creare un [peering reti virtuali](create-peering-different-deployment-models.md) tra reti virtuali hello. È possibile connettersi a una rete virtuale (classico) tooa di rete virtuale, Gestione risorse (), ma non è possibile creare un peering tra due reti virtuali (classico).
- Connessione rete locale tooan di rete virtuale hello utilizzando un [Gateway VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.

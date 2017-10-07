---
title: "una rete virtuale di Azure con più subnet aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una rete virtuale con più subnet in Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Creare una rete virtuale con più subnet

In questa esercitazione, informazioni su come toocreate una rete virtuale Azure di base con separati subnet pubblica e privata. All'interno di una subnet è possibile creare risorse di Azure come macchine virtuali, ambienti del servizio app, set di scalabilità di macchine virtuali, Azure HDInsight e altri servizi cloud. Risorse nelle reti virtuali possono comunicare tra loro e con le risorse di rete virtuale di tooa connesso altre reti.

Nelle sezioni seguenti Hello includono passaggi che è possibile richiedere toocreate una rete virtuale tramite hello [portale di Azure](#portal), hello Azure interfaccia della riga di comando ([CLI di Azure](#azure-cli)), [Azure PowerShell ](#powershell)e un [modello di Azure Resource Manager](#resource-manager-template). il risultato di Hello è hello stesso, indipendentemente dal fatto che di quale strumento usare rete virtuale di toocreate hello. Fare clic su una sezione di toothat toogo collegamento strumento di esercitazione hello. Altre informazioni su tutte le impostazioni relative alla [rete virtuale](virtual-network-manage-network.md) e alla [subnet](virtual-network-manage-subnet.md).

Questo articolo fornisce passaggi toocreate una rete virtuale e modello di distribuzione di gestione delle risorse hello, hello modello di distribuzione è che consigliabile utilizzare durante la creazione di nuove reti virtuali. Se è necessario toocreate una rete virtuale (classico), vedere [creare una rete virtuale (classico)](create-virtual-network-classic.md). Se non si ha familiarità con i modelli di distribuzione di Azure, vedere l'articolo [Informazioni sui modelli di distribuzione di Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Portale di Azure

1. In un browser Internet, visitare toohello [portale di Azure](https://portal.azure.com). Accedere usando l'[account Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Nel portale di hello, fare clic su **+ nuovo** > **rete** > **rete virtuale**.
3. In hello **crea rete virtuale** pannello, immettere i seguenti valori hello e quindi fare clic su **crea**:

    |Impostazione|Valore|
    |---|---|
    |Nome|myVnet|
    |Spazio degli indirizzi|10.0.0.0/16|
    |Nome della subnet|Pubblico|
    |Intervallo di indirizzi subnet|10.0.0.0/24|
    |Gruppo di risorse|Lasciare selezionata l'opzione **Crea nuovo** e quindi immettere **myResourceGroup**.|
    |Sottoscrizione e località|Selezionare la sottoscrizione e la posizione.

    Se si tooAzure nuovo, altre informazioni, vedere [gruppi di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [percorsi](https://azure.microsoft.com/regions) (definita anche tooas *aree*).
4. Nel portale di hello, è possibile creare una sola subnet quando si crea una rete virtuale. In questa esercitazione, creare una subnet secondo dopo aver creato la rete virtuale hello. In un secondo momento, è possibile creare le risorse accessibili da Internet in hello **pubblica** subnet. È anche possibile creare le risorse che non sono accessibili da Internet Ciao hello **privata** subnet. toocreate hello secondo subnet, hello **individuare risorse** nella parte superiore di hello della pagina hello, immettere **myVnet**. Nei risultati della ricerca hello, fare clic su **myVnet**. Se si dispone di più reti virtuali con hello stesso nome nella sottoscrizione, controllare i gruppi di risorse hello elencati in ogni rete virtuale. Assicurarsi di fare clic su hello **myVnet** risultati con il gruppo di risorse hello ricerca **myResourceGroup**.
5. In hello **myVnet** pannello, in **impostazioni**, fare clic su **subnet**.
6. In hello **myVnet - subnet** pannello, fare clic su **+ Subnet**.
7. In hello **aggiungere subnet** pannello per **nome**, immettere **privata**. Come **Intervallo indirizzi** immettere **10.0.1.0/24**.  Fare clic su **OK**.
8. In hello **myVnet - subnet** blade, revisione hello subnet. È possibile visualizzare hello **pubblica** e **privata** subnet a cui è stato creato.
9. **Facoltativo:** risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-portal) in questo articolo.

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

I comandi CLI di Azure sono hello stesso, se si esegue comandi hello da Windows, Linux o Mac OS. Esistono tuttavia differenze di scripting tra le shell dei sistemi operativi. script di Hello in hello alla procedura seguente viene eseguito in una shell Bash. 

1. [Installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di hello Azure CLI installato. Guida di tooget per i comandi CLI, digitare `az <command> --help`. Anziché installare hello CLI e relativi prerequisiti, è possibile usare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Hello Shell Cloud ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell (**> _**) pulsante nella parte superiore di hello di hello [portale](https://portal.azure.com) oppure fare semplicemente clic hello *provarla* pulsante nei passaggi hello che seguono. 
2. Se in esecuzione in locale hello CLI, accedi tooAzure con hello `az login` comando. Se si utilizza hello Shell Cloud, si è già connessi.
3. Hello revisione seguente script e i relativi commenti. Nel browser, copiare hello script e incollarlo nella sessione CLI:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Al termine dello script hello in esecuzione, esaminare le subnet hello per la rete virtuale hello. Copiare hello comando seguente e quindi incollarlo nella sessione CLI:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-cli) in questo articolo.

## <a name="powershell"></a>PowerShell

1. Installare hello l'ultima versione di hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. In una sessione di PowerShell, accedi tooAzure con il [account Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) utilizzando hello `login-azurermaccount` comando.

3. Hello revisione seguente script e i relativi commenti. Nel browser, copiare hello script e incollarlo nella sessione di PowerShell:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. tooreview hello subnet per la rete virtuale hello, copiare hello comando seguente e quindi incollarlo nella sessione di PowerShell:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-powershell) in questo articolo.

## <a name="resource-manager-template"></a>Modello di Resource Manager

È possibile distribuire una rete virtuale usando un modello di Azure Resource Manager. toolearn più informazioni sui modelli, vedere [che cos'è Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). modello di hello tooaccess e toolearn sui relativi parametri, vedere hello [creare una rete virtuale con due subnet](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) modello. È possibile distribuire il modello di hello utilizzando hello [portale](#template-portal), [CLI di Azure](#template-cli), o [PowerShell](#template-powershell).

**Facoltativo:** risorse hello toodelete create in questa esercitazione, hello completato i passaggi in tutte le sezioni di [eliminare risorse](#delete) in questo articolo.

### <a name="template-portal"></a>Portale di Azure

1. Nel browser aprire hello [pagina modello](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Fare clic su hello **distribuire tooAzure** pulsante. Se si è connessi non è già tooAzure, accedere schermata di accesso al portale Azure hello che viene visualizzata.
3. Accedi a portale toohello utilizzando il [account Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se non si ha un account Azure, è possibile iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Immettere i seguenti valori per parametri hello hello:

    |.|Valore|
    |---|---|
    |Sottoscrizione|Selezionare la propria sottoscrizione|
    |Gruppo di risorse|myResourceGroup|
    |Percorso|Selezionare una località|
    |Nome della rete virtuale|myVnet|
    |Prefisso di indirizzo della rete virtuale|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Pubblico|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Privato|

5. Accettare le condizioni toohello e quindi fare clic su **acquisto** toodeploy rete virtuale di hello.

### <a name="template-cli"></a>

1. [Installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di hello Azure CLI installato. Guida di tooget per i comandi CLI, digitare `az <command> --help`. Anziché installare hello CLI e relativi prerequisiti, è possibile usare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Hello Shell Cloud ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell **> _** pulsante nella parte superiore di hello di hello [portale](https://portal.azure.com), oppure fare semplicemente clic hello **provarla** pulsante nei passaggi hello che seguono. 
2. Se in esecuzione in locale hello CLI, accedi tooAzure con hello `az login` comando. Se si utilizza hello Shell Cloud, si è già connessi.
3. un gruppo di risorse per la rete virtuale hello toocreate, comando copia hello seguente, incollarlo nella sessione CLI:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. È possibile distribuire il modello di hello utilizzando uno dei seguenti parametri opzioni hello:
    - **Valori predefiniti**. Immettere hello comando seguente:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Valori personalizzati**. Scaricare e modificare il modello di hello prima di distribuire il modello di hello. È anche possibile distribuire il modello di hello utilizzando i parametri dalla riga di comando hello o distribuire il modello di hello con un file di parametri separati. file di modello e i parametri di hello toodownload, fare clic su hello **Sfoglia su GitHub** pulsante hello [creare una rete virtuale con due subnet](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) page del modello. In GitHub, fare clic su hello **azuredeploy.parameters.json** o **azuredeploy.json** file. Quindi, fare clic su hello **Raw** file hello toodisplay di pulsante. Nel browser, copiare il contenuto di hello del file hello. Salvare hello contenuto tooa file nel computer in uso. È possibile modificare i valori dei parametri nel modello hello hello o distribuire il modello di hello con un file di parametri separati.  

    altre informazioni sulle toolearn come modelli toodeploy usando questi metodi, digitare `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Installare hello l'ultima versione di hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. In una sessione di PowerShell, toosign con il [account Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), immettere `login-azurermaccount`.
3. un gruppo di risorse per la rete virtuale hello, toocreate immettere hello comando seguente:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. È possibile distribuire il modello di hello utilizzando uno dei seguenti parametri opzioni hello:
    - **Valori predefiniti**. Immettere hello comando seguente:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Valori personalizzati**. Scaricare e modificare il modello di hello prima di distribuirlo. È anche possibile distribuire il modello di hello utilizzando i parametri dalla riga di comando hello o distribuire il modello di hello con un file di parametri separati. file di modello e i parametri di hello toodownload, fare clic su hello **Sfoglia su GitHub** pulsante hello [creare una rete virtuale con due subnet](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) page del modello. In GitHub, fare clic su hello **azuredeploy.parameters.json** o **azuredeploy.json** file. Quindi, fare clic su hello **Raw** file hello toodisplay di pulsante. Nel browser, copiare il contenuto di hello del file hello. Salvare hello contenuto tooa file nel computer in uso. È possibile modificare i valori dei parametri nel modello hello hello o distribuire il modello di hello con un file di parametri separati.  

    altre informazioni sulle toolearn come modelli toodeploy usando questi metodi, digitare `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Eliminare risorse

Al termine di questa esercitazione, è possibile risorse hello toodelete creato, in modo che non si incorrere in costi di utilizzo. Un gruppo di risorse anche se si elimina tutte le risorse che si trovano nel gruppo di risorse hello.

### <a name="delete-portal"></a>Portale di Azure

1. Nella casella di ricerca portale hello, immettere **myResourceGroup**. Nei risultati della ricerca hello, fare clic su **myResourceGroup**.
2. In hello **myResourceGroup** pannello, fare clic su hello **eliminare** icona.
3. l'eliminazione di hello tooconfirm, in hello **hello di tipo nome gruppo di risorse** immettere **myResourceGroup**, quindi fare clic su **eliminare**.

### <a name="delete-cli"></a>

In una sessione CLI, immettere hello comando seguente:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

In una sessione di PowerShell, immettere il comando seguente hello:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Passaggi successivi

- toolearn su tutte le reti virtuali e le impostazioni di subnet, vedere [gestire reti virtuali](virtual-network-manage-network.md#view-vnet) e [gestire subnet della rete virtuale](virtual-network-manage-subnet.md#create-subnet). Si sono disponibili varie opzioni per l'utilizzo di reti virtuali e le subnet in una diversi requisiti toomeet ambiente produzione.
- toofilter in ingresso e in uscita traffico della subnet, creare e applicare [gruppi di sicurezza di rete](virtual-networks-nsg.md) toosubnets.
- Creare un [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) macchina virtuale, quindi connetterla tooan una rete virtuale esistente.
- reti virtuali tooconnect due in hello nello stesso percorso di Azure, creare un [peering reti virtuali](virtual-network-peering-overview.md) tra reti virtuali hello.
- Connessione rete locale tooan di rete virtuale hello utilizzando un [Gateway VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.

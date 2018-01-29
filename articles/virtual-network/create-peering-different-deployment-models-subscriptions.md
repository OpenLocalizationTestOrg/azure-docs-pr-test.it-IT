---
title: Creare un peering di rete virtuale di Azure - Modelli di distribuzione diversa - Sottoscrizioni diverse | Microsoft Docs
description: Informazioni su come creare un peering di rete virtuale tra reti virtuali distribuite tramite modelli di distribuzione di Azure diversi e incluse in sottoscrizioni di Azure diverse.
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
ms.date: 09/15/2017
ms.author: jdial;anavin
ms.openlocfilehash: 441bb0a269de400c82abc083118f5e0642523640
ms.sourcegitcommit: c25cf136aab5f082caaf93d598df78dc23e327b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Creare un peering di rete virtuale: diversi modelli di distribuzione e sottoscrizioni

In questa esercitazione si apprenderà a creare un peering di rete virtuale tra reti virtuali create con modelli di distribuzione diversi. Le reti virtuali sono incluse in sottoscrizioni diverse. Il peering di due reti virtuali consente alle risorse che si trovano in reti virtuali diverse di comunicare tra loro con la stessa larghezza di banda e la stessa latenza come se fossero nella stessa rete virtuale. Altre informazioni sul [Peering di rete virtuale](virtual-network-peering-overview.md).

I passaggi per creare un peering di rete virtuale sono diversi a seconda che le reti virtuali siano incluse nella stessa sottoscrizione o in sottoscrizioni diverse e in base al [modello di distribuzione di Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) con il quale sono state create le reti virtuali. Per informazioni su come creare un peering di rete virtuale in altri scenari, fare clic sullo scenario nella tabella seguente:

|Modello di distribuzione di Azure  | Sottoscrizione di Azure  |
|--------- |---------|
|[Entrambi con Resource Manager](virtual-network-create-peering.md) |Uguale|
|[Entrambi con Resource Manager](create-peering-different-subscriptions.md) |Diversa|
|[Uno con Resource Manager, uno con una distribuzione classica](create-peering-different-deployment-models.md) |Uguale|

Non è possibile creare un peering di rete virtuale tra due reti virtuali distribuite tramite il modello di distribuzione classica. La possibilità di eseguire il peering di reti virtuali create tramite modelli di distribuzione diversi che esistono in sottoscrizioni diverse attualmente è in anteprima. Per completare questa esercitazione, è innanzitutto necessario [registrarsi](#register) per usare la funzionalità. Questa esercitazione usa le reti virtuali che esistono nella stessa area. Anche la possibilità di eseguire il peering di reti virtuali in aree diverse è in anteprima. Anche per usare tale funzionalità, è necessario [registrarsi](#register). Le due funzionalità sono indipendenti. Per completare questa esercitazione, è necessario registrarsi solo per la funzionalità di peering delle reti virtuali create tramite modelli di distribuzione diversi che esistono in sottoscrizioni diverse. 

Quando si crea un peering di rete virtuale tra reti virtuali incluse in sottoscrizioni diverse, entrambe le sottoscrizioni devono essere associate allo stesso tenant di Azure Active Directory. Se non si ha già un tenant di Azure Active Directory, è possibile [crearne uno](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rapidamente. 

La possibilità di connettere reti virtuali create tramite un modello di distribuzione, diversi modelli di distribuzione, aree diverse o sottoscrizioni associate agli stessi tenant o a tenant diversi di Azure Active Directory tramite un [Gateway VPN](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) di Azure è in versione di anteprima e non richiede la registrazione.

Per creare un peering di rete virtuale, è possibile usare il [portale di Azure](#portal), l'[interfaccia della riga di comando](#cli) di Azure o [Azure PowerShell](#powershell). Facendo clic sui collegamenti degli strumenti precedenti, si passa direttamente alle procedure per la creazione di un peering di rete virtuale con il determinato strumento.

## <a name="portal"></a>Creare un peering - Portale di Azure

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si usa un account dotato di autorizzazioni per entrambe le sottoscrizioni, è possibile usare lo stesso account per tutti i passaggi, ignorando i passaggi per la disconnessione dal portale e quelli per l'assegnazione a un altro utente delle autorizzazioni per le reti virtuali. Prima di completare i passaggi seguenti, è necessario eseguire la registrazione per l'anteprima. Per eseguire la registrazione per l'anteprima, completare i passaggi nella sezione [Eseguire la registrazione per l'anteprima](#register) di questo articolo. I passaggi rimanenti non riescono se non si registrano entrambe le sottoscrizioni per l'anteprima.
 
1. Accedere al [portale di Azure](https://portal.azure.com) come UserA. L'account con cui si esegue l'accesso deve avere le autorizzazioni necessarie per la creazione di un peering di rete virtuale. Vedere la sezione [Autorizzazioni](#permissions) di questo articolo per informazioni dettagliate.
2. Fare clic su **+ Nuovo**, **Rete** e quindi **Rete virtuale**.
3. Nel pannello **Crea rete virtuale** immettere o selezionare i valori necessari per le impostazioni seguenti e quindi fare clic su **Crea**:
    - **Nome**: *myVnetA*
    - **Spazio indirizzi**: *10.0.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.0.0.0/24*
    - **Sottoscrizione**: selezionare la sottoscrizione A.
    - **Gruppo di risorse**: selezionare **Crea nuovo** e immettere *myResourceGroupA*
    - **Località**: *Stati Uniti orientali*
4. Nella casella **Cerca risorse** nella parte superiore del portale digitare *myVnetA*. Fare clic su **myVnetA** quando viene visualizzato nei risultati della ricerca. Viene visualizzato un pannello per la rete virtuale **myVnetA**.
5. Nel pannello **myVnetA** visualizzato fare clic su **Controllo di accesso (IAM)** nell'elenco verticale di opzioni sul lato sinistro del pannello.
6. Nel pannello **myVnetA - Controllo di accesso (IAM)** visualizzato fare clic su **+ Aggiungi**.
7. Nel pannello **Aggiungi autorizzazioni** visualizzato selezionare **Collaboratore rete** nella casella **Ruolo**.
8. Nella casella **Seleziona** selezionare UserB o digitare l'indirizzo di posta elettronica di UserB per cercarlo. L'elenco di utenti mostrato è tratto dallo stesso tenant di Azure Active Directory della rete virtuale per la quale si sta configurando il peering. Quando viene visualizzato nell'elenco, fare clic su UserB.
9. Fare clic su **Salva**.
10. Disconnettersi dal portale come UserA e quindi accedere come UserB.
11. Fare clic su **+ Nuovo**, digitare *Rete virtuale* nella casella **Cerca nel Marketplace**, quindi fare clic su **Rete virtuale** nei risultati della ricerca.
12. Nel pannello **Rete virtuale** che viene visualizzato selezionare **Classico** nella casella **Selezionare un modello di distribuzione** e fare clic su **Crea**.
13.   Nella casella Crea rete virtuale (classico) visualizzata immettere i valori seguenti:

    - **Nome**: *myVnetB*
    - **Spazio indirizzi**: *10.1.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.1.0.0/24*
    - **Sottoscrizione**: selezionare la sottoscrizione B.
    - **Gruppo di risorse**: selezionare **Crea nuovo** e immettere *myResourceGroupB*
    - **Località**: *Stati Uniti orientali*

14. Nella casella **Cerca risorse** nella parte superiore del portale digitare *myVnetB*. Fare clic su **myVnetB** quando viene visualizzato nei risultati della ricerca. Viene visualizzato un pannello per la rete virtuale **myVnetB**.
15. Nel pannello **myVnetB** visualizzato fare clic su **Proprietà** nell'elenco verticale di opzioni sul lato sinistro del pannello. Copiare il valore di **ID RISORSA**, che verrà usato in un passaggio successivo. L'ID risorsa è simile all'esempio seguente: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Completare i passaggi da 5 a 9 per myVnetB immettendo **UserA** nel passaggio 8.
17. Disconnettersi dal portale come UserB e accedere come UserA.
18. Nella casella **Cerca risorse** nella parte superiore del portale digitare *myVnetA*. Fare clic su **myVnetA** quando viene visualizzato nei risultati della ricerca. Viene visualizzato un pannello per la rete virtuale **myVnet**.
19. Fare clic su **myVnetA**.
20. Nel pannello **myVnetA** visualizzato fare clic su **Peer** nell'elenco di opzioni verticale sul lato sinistro del pannello.
21. Nel pannello **myVnetA - Peer** visualizzato fare clic su **+ Aggiungi**
22. Nel pannello **Aggiungi peering** visualizzato immettere o selezionare le opzioni seguenti e quindi fare clic su **OK**:
     - **Nome**: *myVnetAToMyVnetB*
     - **Modello di distribuzione della rete virtuale**: selezionare **Classica**.
     - **Conosco l'ID della risorsa**: selezionare questa casella di controllo.
     - **ID risorsa**: immettere l'ID risorsa indicato nel passaggio 15.
     - **Consenti accesso alla rete virtuale:** assicurarsi che sia selezionato **Abilitato**.
    Questa esercitazione non prevede l'uso di altre impostazioni. Per informazioni su tutte le impostazioni per il peering, vedere [Gestire i peering di rete virtuale](virtual-network-manage-peering.md#create-a-peering).
23. Dopo aver fatto clic su **OK** nel passaggio precedente, il pannello **Aggiungi peering** si chiude e viene visualizzato di nuovo il pannello **myVnetA - Peer**. Dopo alcuni secondi, il peering creato viene visualizzato nel pannello. Nella colonna **STATO PEERING** relativa al peering **myVnetAToMyVnetB** creato è specificato lo stato **Connesso**. Il peering viene quindi stabilito. Non è necessario eseguire il peering tra la rete virtuale creata con modello di distribuzione classica e la rete virtuale creata con Resource Manager.

    Tutte le risorse di Azure create in una delle reti virtuali possono ora comunicare tra loro tramite i relativi indirizzi IP. Se si usa la risoluzione dei nomi di Azure predefinita per le reti virtuali, le risorse contenute nelle reti virtuali non sono in grado di risolvere i nomi tra le reti virtuali. Se si intende risolvere i nomi tra le reti virtuali in peering, è necessario creare un proprio server DNS. Per informazioni sulla configurazione, vedere [Risoluzione dei nomi usando il server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Facoltativo**: anche se la creazione delle macchine virtuali non è illustrata in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale ed eseguire la connessione da una macchina virtuale all'altra per convalidare la connettività.
25. **Facoltativo**: per eliminare le risorse create in questa esercitazione, completare i passaggi della sezione [Eliminare risorse](#delete-portal) di questo articolo.

## <a name="cli"></a>Creare un peering - Interfaccia della riga di comando di Azure

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si usa un account dotato di autorizzazioni per entrambe le sottoscrizioni, è possibile usare lo stesso account per tutti i passaggi, ignorando i passaggi per la disconnessione da Azure e rimuovendo le righe dello script per la creazione delle assegnazioni dei ruoli utente. Sostituire UserA@azure.com e UserB@azure.com in tutti gli script seguenti con i nomi utente usati per UserA e UserB. 

Prima di completare i passaggi seguenti, è necessario eseguire la registrazione per l'anteprima. Per eseguire la registrazione per l'anteprima, completare i passaggi nella sezione [Eseguire la registrazione per l'anteprima](#register) di questo articolo. I passaggi rimanenti non riescono se non si registrano entrambe le sottoscrizioni per l'anteprima.

1. [Installare](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l'interfaccia della riga di comando di Azure 1.0 per creare la rete virtuale con modello di distribuzione classico.
2. Aprire una sessione dell'interfaccia della riga di comando e accedere ad Azure come UserB usando il comando `azure login`.
3. Eseguire l'interfaccia della riga di comando in modalità di gestione del servizio immettendo il comando `azure config mode asm`.
4. Per creare una rete virtuale con modello di distribuzione classico, immettere il comando seguente:
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. I passaggi rimanenti devono essere completati con un bash shell con l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive [installato](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json) o mediante Azure Cloud Shell. Azure Cloud Shell è una shell Bash gratuita che può essere eseguita direttamente nel portale di Azure. Include l'interfaccia della riga di comando di Azure preinstallata e configurata per l'uso con l'account. Fare clic sul pulsante **Prova** nello script seguente per aprire una Cloud Shell tramite cui è possibile accedere all'account di Azure personale. Per le opzioni sull'esecuzione di script dell'interfaccia della riga di comando bash nel client Windows, vedere [Esecuzione dell'interfaccia della riga di comando di Azure in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Copiare lo script seguente in un editor di testo nel PC. Sostituire `<SubscriptionB-Id>` con l'ID della sottoscrizione. Se l'ID della sottoscrizione non è noto, immettere il comando `az account show`. Il valore per **id** nell'output è l'ID della sottoscrizione. Copiare lo script modificato, incollarlo nella sessione dell'interfaccia della riga di comando 2.0 e quindi premere `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Durante la creazione della rete virtuale con distribuzione classica nel passaggio 4, Azure crea la rete virtuale nel gruppo di risorse *Default-Networking*.
7. Disconnettere UserB da Azure e accedere come a UserA nell'interfaccia della riga di comando 2.0.
8. Creare un gruppo di risorse e una rete virtuale con Resource Manager. Copiare lo script seguente, incollarlo nella sessione dell'interfaccia della riga di comando e quindi premere `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get the id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions to myVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Creare un peering di rete virtuale tra due reti virtuali create con modelli di distribuzione diversi. Copiare lo script seguente in un editor di testo nel PC. Sostituire `<SubscriptionB-id>` con l'ID della sottoscrizione. Se l'ID della sottoscrizione non è noto, immettere il comando `az account show`. Il valore per **id** nell'output è l'ID della sottoscrizione. Azure ha creato la rete virtuale con distribuzione classica creata nel passaggio 4 in un gruppo di risorse denominato *Default-Networking*. Incollare lo script modificato nella sessione dell'interfaccia della riga di comando e quindi premere `Enter`.

    ```azurecli-interactive
    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Dopo aver eseguito lo script, rivedere i peering di ciascuna rete virtuale creata con Resource Manager. Copiare lo script seguente e incollarlo nella sessione dell'interfaccia della riga di comando:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    L'output mostra **Connesso** nella colonna **PeeringState**.

    Tutte le risorse di Azure create in una delle reti virtuali possono ora comunicare tra loro tramite i relativi indirizzi IP. Se si usa la risoluzione dei nomi di Azure predefinita per le reti virtuali, le risorse contenute nelle reti virtuali non sono in grado di risolvere i nomi tra le reti virtuali. Se si intende risolvere i nomi tra le reti virtuali in peering, è necessario creare un proprio server DNS. Per informazioni sulla configurazione, vedere [Risoluzione dei nomi usando il server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Facoltativo**: anche se la creazione delle macchine virtuali non è illustrata in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale ed eseguire la connessione da una macchina virtuale all'altra per convalidare la connettività.
12. **Facoltativo:** per eliminare le risorse create in questa esercitazione, completare la procedura descritta in [Eliminare risorse](#delete-cli) in questo articolo.

## <a name="powershell"></a>Creare un peering - PowerShell

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si usa un account dotato di autorizzazioni per entrambe le sottoscrizioni, è possibile usare lo stesso account per tutti i passaggi, ignorando i passaggi per la disconnessione da Azure e rimuovendo le righe dello script per la creazione delle assegnazioni dei ruoli utente. Sostituire UserA@azure.com e UserB@azure.com in tutti gli script seguenti con i nomi utente usati per UserA e UserB. 

Prima di completare i passaggi seguenti, è necessario eseguire la registrazione per l'anteprima. Per eseguire la registrazione per l'anteprima, completare i passaggi nella sezione [Eseguire la registrazione per l'anteprima](#register) di questo articolo. I passaggi rimanenti non riescono se non si registrano entrambe le sottoscrizioni per l'anteprima.

1. Installare la versione più recente di [Azure](https://www.powershellgallery.com/packages/Azure) PowerShell e i moduli [AzureRm](https://www.powershellgallery.com/packages/AzureRM/). Se non si ha familiarità con Azure PowerShell, vedere [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) (Panoramica di Azure PowerShell).
2. Avviare una sessione di PowerShell.
3. In PowerShell accedere alla sottoscrizione di UserB come UserB immettendo il comando `Add-AzureAccount`.
4. Per creare una rete virtuale con distribuzione classica con PowerShell, è necessario creare un nuovo file di configurazione di rete o modificarne uno esistente. Informazioni su come [esportare, aggiornare e importare il file di configurazione di rete](virtual-networks-using-network-configuration-file.md). Il file deve includere l'elemento **VirtualNetworkSite** seguente per la rete virtuale usata in questa esercitazione:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
    > L'importazione di un file di configurazione di rete modificato può modificare le reti virtuali esistenti create con distribuzione classica nella sottoscrizione. Assicurarsi di aggiungere solo la rete virtuale precedente e di non modificare o rimuovere le reti virtuali esistenti dalla sottoscrizione. 

5. Accedere alla sottoscrizione di UserB come UserB per usare i comandi di Resource Manager immettendo il comando `login-azurermaccount`.
6. Assegnare le autorizzazioni utente di UserA alla rete virtuale B. Copiare lo script seguente in un editor di testo nel PC e sostituire `<SubscriptionB-id>` con l'ID della sottoscrizione B. Se non si conosce l'ID della sottoscrizione, immettere il comando `Get-AzureRmSubscription` per visualizzarlo. Il valore di **Id** nell'output restituito è l'ID della sottoscrizione. Azure ha creato la rete virtuale con distribuzione classica creata nel passaggio 4 in un gruppo di risorse denominato *Default-Networking*. Per eseguire lo script, copiare lo script modificato, incollarlo in PowerShell e quindi premere `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Disconnettersi da Azure come UserB e accedere alla sottoscrizione di UserA come UserA immettendo il comando `login-azurermaccount`. L'account con cui si esegue l'accesso deve avere le autorizzazioni necessarie per la creazione di un peering di rete virtuale. Vedere la sezione [Autorizzazioni](#permissions) di questo articolo per informazioni dettagliate.
8. Per creare la rete virtuale con Resource Manager copiare lo script seguente, incollarlo in PowerShell e premere `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Assegnare le autorizzazioni di UserB a myVnetA. Copiare lo script seguente in un editor di testo nel PC e sostituire `<SubscriptionA-Id>` con l'ID della sottoscrizione A. Se non si conosce l'ID della sottoscrizione, immettere il comando `Get-AzureRmSubscription` per visualizzarlo. Il valore di **Id** nell'output restituito è l'ID della sottoscrizione. Incollare la versione modificata dello script in PowerShell e quindi premere `Enter` per eseguirla.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Copiare lo script seguente in un editor di testo nel PC, sostituire `<SubscriptionB-id>` con l'ID della sottoscrizione B. Per eseguire il peering di myVnetA a myVnetB copiare lo script modificato, incollarlo in PowerShell e premere `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Per visualizzare lo stato del peering di myVnetA copiare lo script seguente, incollarlo in PowerShell e premere `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Lo stato è **Connesso**. Viene modificato in **Connesso** dopo la configurazione del peering a myVnetA da myVnetB.

    Tutte le risorse di Azure create in una delle reti virtuali possono ora comunicare tra loro tramite i relativi indirizzi IP. Se si usa la risoluzione dei nomi di Azure predefinita per le reti virtuali, le risorse contenute nelle reti virtuali non sono in grado di risolvere i nomi tra le reti virtuali. Se si intende risolvere i nomi tra le reti virtuali in peering, è necessario creare un proprio server DNS. Per informazioni sulla configurazione, vedere [Risoluzione dei nomi usando il server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Facoltativo**: anche se la creazione delle macchine virtuali non è illustrata in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale ed eseguire la connessione da una macchina virtuale all'altra per convalidare la connettività.
13. **Facoltativo:** per eliminare le risorse create in questa esercitazione, completare la procedura descritta in [Eliminare risorse](#delete-powershell) in questo articolo.

## <a name="permissions"></a>Autorizzazioni

Gli account usati per creare un peering di rete virtuale devono disporre del ruolo o delle autorizzazioni necessarie. Ad esempio, per eseguire il peering di due reti virtuali denominate myVNetA e myVNetB, è necessario assegnare all'account il ruolo minimo o le autorizzazioni minime seguenti per ogni rete virtuale:
    
|Rete virtuale|Modello di distribuzione|Ruolo|Autorizzazioni|
|---|---|---|---|
|myVnetA|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnetB|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Altre informazioni sui [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e sull'assegnazione di autorizzazioni specifiche ai [ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo Resource Manager).

## <a name="delete"></a>Eliminare risorse
Al termine di questa esercitazione, è necessario eliminare le risorse create, per non incorrere in costi di utilizzo. Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse all'interno di esso.

### <a name="delete-portal"></a>Portale di Azure

1. Nella casella di ricerca del portale immettere **myResourceGroupA**. Nei risultati della ricerca fare clic su **myResourceGroupA**.
2. Nel pannello **myResourceGroupA** fare clic sull'icona **Elimina**.
3. Per confermare l'eliminazione, nella casella **DIGITARE IL NOME DEL GRUPPO DI RISORSE** immettere **myResourceGroupA** e quindi fare clic su **Elimina**.
4. Nella casella **Cerca risorse** nella parte superiore del portale digitare *myVnetB*. Fare clic su **myVnetB** quando viene visualizzato nei risultati della ricerca. Viene visualizzato un pannello per la rete virtuale **myVnetB**.
5. Nel pannello **myVnetB** fare clic su **Elimina**.
6. Per confermare l'eliminazione, nella casella **Elimina rete virtuale** fare clic su **Sì**.

### <a name="delete-cli"></a>

1. Accedere ad Azure tramite l'interfaccia della riga di comando di Azure 2.0 per eliminare la rete virtuale creata con Resource Manager con il comando seguente:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Accedere ad Azure tramite l'interfaccia della riga di comando di Azure 1.0 per eliminare la rete virtuale creata con distribuzione classica con il comando seguente:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Al prompt dei comandi di PowerShell immettere il comando seguente per eliminare la rete virtuale creata con Resource Manager:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. Per eliminare una rete virtuale creata con distribuzione classica con PowerShell, è necessario modificare un file di configurazione di rete esistente. Informazioni su come [esportare, aggiornare e importare il file di configurazione di rete](virtual-networks-using-network-configuration-file.md). Rimuovere l'elemento VirtualNetworkSite seguente dalla rete virtuale usata in questa esercitazione:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
    > L'importazione di un file di configurazione di rete modificato può modificare le reti virtuali esistenti create con distribuzione classica nella sottoscrizione. Assicurarsi di rimuovere solo la rete virtuale precedente e di non modificare o rimuovere altre reti virtuali esistenti dalla sottoscrizione. 

## <a name="register"></a>Eseguire la registrazione per l'anteprima

La possibilità di eseguire il peering di reti virtuali create tramite modelli di distribuzione di Azure diversi che esistono in sottoscrizioni diverse attualmente è in anteprima. Le funzionalità in anteprima non offrono lo stesso livello di disponibilità e affidabilità delle funzionalità in versione di disponibilità generale. Per ricevere le notifiche più aggiornate su disponibilità e stato della funzionalità in anteprima, vedere la pagina [Aggiornamenti della rete virtuale di Azure](https://azure.microsoft.com/updates/?product=virtual-network). 

Innanzitutto, è necessario registrarsi per la funzionalità tra sottoscrizioni, tra la modelli di distribuzione prima che sia possibile usarla. Completare i passaggi seguenti all'interno della sottoscrizione in cui si trovano le reti virtuali per cui si desidera eseguire il peering, tramite Azure PowerShell o l'interfaccia della riga di comando di Azure:

### <a name="powershell"></a>PowerShell

1. Installare la versione più recente del modulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) di PowerShell. Se non si ha familiarità con Azure PowerShell, vedere [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) (Panoramica di Azure PowerShell).
2. Avviare una sessione di PowerShell e accedere ad Azure usando il comando `Login-AzureRmAccount`.
3. Registrare per l'anteprima la sottoscrizione in cui si trova ognuna delle reti virtuali di cui si vuole eseguire il peering immettendo i comandi seguenti:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
4. Verificare di essere registrati per l'anteprima immettendo il comando seguente:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

    Non completare i passaggi descritti nelle sezioni relative al portale, all'interfaccia della riga di comando di Azure, a PowerShell o al modello di Gestione risorse di questo articolo finché l'output di **RegistrationState** che si riceve dopo aver immesso il comando precedente non corrisponde a **Registrato** per entrambe le sottoscrizioni.

> [!NOTE]
> Questa esercitazione usa le reti virtuali che esistono nella stessa area. Anche la possibilità di eseguire il peering di reti virtuali in aree diverse è in anteprima. Per registrarsi al peering tra aree o globale, completare di nuovo i passaggi 1-4, usando `-FeatureName AllowGlobalVnetPeering` anziché `-FeatureName AllowClassicCrossSubscriptionPeering`. Le due funzionalità sono indipendenti l'una dall'altra. Non è necessario registrarsi per entrambe, a meno che non si desideri usarle entrambe. La funzionalità è disponibile in un set limitato di aree (inizialmente, Stati Uniti centro-occidentali, Canada centrale e Stati Uniti occidentali 2).

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

1. [Installare e configurare l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli?toc=%2Fazure%2Fvirtual-network%2Ftoc.json).
2. Assicurarsi di usare la versione 2.0.18 o successiva dell'interfaccia della riga di comando di Azure immettendo il comando `az --version`. Se non si usa questa versione, installare la versione più recente.
3. Accedere ad Azure con il comando `az login`.
4. Registrare all'anteprima immettendo i comandi seguenti:

   ```azurecli-interactive
   az feature register --name AllowGlobalVnetPeering --namespace Microsoft.Network
   az provider register --name Microsoft.Network
   ```

5. Verificare di essere registrati per l'anteprima immettendo il comando seguente:

    ```azurecli-interactive
    az feature show --name AllowGlobalVnetPeering --namespace Microsoft.Network
    ```

    Non completare i passaggi descritti nelle sezioni relative al portale, all'interfaccia della riga di comando di Azure, a PowerShell o al modello di Resource Manager di questo articolo finché l'output di **RegistrationState** che si riceve dopo aver immesso il comando precedente non corrisponde a **Registered** (Registrato) per entrambe le sottoscrizioni.

> [!NOTE]
> Questa esercitazione usa le reti virtuali che esistono nella stessa area. Anche la possibilità di eseguire il peering di reti virtuali in aree diverse è in anteprima. Per registrarsi al peering tra aree o globale, completare di nuovo i passaggi 1-5, usando `--name AllowGlobalVnetPeering` anziché `--name AllowClassicCrossSubscriptionPeering`. Le due funzionalità sono indipendenti l'una dall'altra. Non è necessario registrarsi per entrambe, a meno che non si desideri usarle entrambe. La funzionalità è disponibile in un set limitato di aree (inizialmente, Stati Uniti centro-occidentali, Canada centrale e Stati Uniti occidentali 2).

## <a name="next-steps"></a>Passaggi successivi

- Acquisire familiarità con importanti [vincoli e comportamenti del peering di rete virtuale](virtual-network-manage-peering.md#requirements-and-constraints) prima di creare un peering di rete virtuale per l'uso in produzione.
- Acquisire informazioni più dettagliate su tutte le [impostazioni per il peering di rete virtuale](virtual-network-manage-peering.md#create-a-peering).
- Acquisire informazioni su come [Creare una topologia di rete hub-spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con il peering di rete virtuale.

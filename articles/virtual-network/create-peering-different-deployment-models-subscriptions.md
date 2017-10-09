---
title: un peering di rete virtuale di Azure - aaaCreate distribuzione diversi modelli - diverse sottoscrizioni | Documenti Microsoft
description: Informazioni su come toocreate creata una rete virtuale peering tra reti virtuali tramite i modelli di distribuzione di Azure diversi presenti in diverse sottoscrizioni di Azure.
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Creare un peering di rete virtuale: diversi modelli di distribuzione e sottoscrizioni

In questa esercitazione viene illustrato toocreate una rete virtuale peering tra reti virtuali create tramite diversi modelli di distribuzione. reti virtuali Hello si trovano in diverse sottoscrizioni. Peering due risorse di consente di reti virtuali in reti virtuali diverse toocommunicate reciprocamente con hello stessa larghezza di banda e latenza, come se fosse di risorse hello in hello stessa rete virtuale. Altre informazioni sul [Peering di rete virtuale](virtual-network-peering-overview.md). 

Hello passaggi toocreate un peering di reti virtuali sono diversi, a seconda che le reti virtuali hello siano hello uguale o diverso, sottoscrizioni e che [modello di distribuzione Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) vengono create le reti virtuali hello tramite. Informazioni su come toocreate un virtuale rete peering in altri scenari, fare clic su uno scenario di hello di hello nella tabella seguente:

|Modello di distribuzione di Azure  | Sottoscrizione di Azure  |
|--------- |---------|
|[Entrambi con Resource Manager](virtual-network-create-peering.md) |Uguale|
|[Entrambi con Resource Manager](create-peering-different-subscriptions.md) |Diversa|
|[Uno con Resource Manager, uno con una distribuzione classica](create-peering-different-deployment-models.md) |Uguale|

Impossibile creare una rete virtuale peering tra due reti virtuali distribuite tramite il modello di distribuzione classica hello. Un peering di reti virtuali può essere creato solo tra due reti virtuali presenti in hello stessa regione di Azure. Quando la creazione di una rete virtuale peering tra reti virtuali presenti in diverse sottoscrizioni, le sottoscrizioni devono essere entrambi hello associata toohello stesso tenant Azure Active Directory. Se non si ha già un tenant di Azure Active Directory, è possibile [crearne uno](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rapidamente. Se è necessario tooconnect virtuale reti che sono stati creati tramite il modello di distribuzione classica hello, che esistono in diverse aree di Azure o che esistono nelle sottoscrizioni associate toodifferent tenant di Azure Active Directory, è possibile usare un Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello reti virtuali. 

> [!WARNING]
> La creazione di un peering di rete virtuale tra reti virtuali create con modelli di distribuzione di Azure diversi e incluse in sottoscrizioni di Azure diverse è attualmente in anteprima. Peering di reti virtuali create in questo scenario potrebbe non essere hello dello stesso livello di disponibilità e affidabilità come la creazione di una rete virtuale peering in genere negli scenari di rilascio di disponibilità. I peering di rete virtuale creati in questo scenario non sono supportati, possono presentare funzionalità limitate e potrebbero non essere disponibili in tutte le aree di Azure. Per hello più notifiche su disponibilità e lo stato di questa funzionalità, vedere hello [Aggiorna rete virtuale di Azure](https://azure.microsoft.com/updates/?product=virtual-network) pagina.

È possibile utilizzare hello [portale di Azure](#portal), hello Azure [interfaccia della riga di comando](#cli) (CLI), o Azure [PowerShell](#powershell) toocreate un peering di rete virtuale. Fare clic su uno qualsiasi dei hello precedente dello strumento collegamenti toogo direttamente toohello i passaggi per la creazione di una rete virtuale peering utilizzando lo strumento di scelta.

## <a name="register"></a>Registro per l'anteprima di hello

tooregister per l'anteprima di hello, hello completo passaggi successivi per entrambe le sottoscrizioni che contengono le reti virtuali hello si desidera toopeer. Hello solo lo strumento è possibile utilizzare tooregister per l'anteprima di hello è PowerShell.

1. Installare hello l'ultima versione di hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Avviare una sessione di PowerShell e accedere utilizzando hello tooAzure `login-azurermaccount` comando.
3. Registrare la sottoscrizione per l'anteprima di hello immettendo hello seguenti comandi:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    Non attenersi hello hello portale, CLI di Azure o PowerShell sezioni di questo articolo finché hello **RegistrationState** output viene visualizzato dopo l'immissione di comando seguente hello è **registrati** per entrambe le sottoscrizioni:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Creare un peering - Portale di Azure

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si utilizza un account che dispone di autorizzazioni tooboth sottoscrizioni, è possibile utilizzare hello stesso account per tutti i passaggi, ignorare i passaggi di hello per la registrazione dal portale hello e ignorare i passaggi di hello per l'assegnazione di reti virtuali toohello di autorizzazioni di un altro utente. Prima di completare i passaggi hello, è necessario registrare per l'anteprima di hello. tooregister, hello completato i passaggi in hello [registrazione per l'anteprima di hello](#register) sezione di questo articolo. Non proseguire con hello rimanenti passaggi fino a quando non sono registrate entrambe le sottoscrizioni per l'anteprima di hello.
 
1. Accedi toohello [portale di Azure](https://portal.azure.com) come utente. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
2. Fare clic su **+ Nuovo**, **Rete** e quindi **Rete virtuale**.
3. In hello **crea rete virtuale** pannello, immettere o selezionare i valori per hello seguenti impostazioni, quindi fare clic su **crea**:
    - **Nome**: *myVnetA*
    - **Spazio indirizzi**: *10.0.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.0.0.0/24*
    - **Sottoscrizione**: selezionare la sottoscrizione A.
    - **Gruppo di risorse**: selezionare **Crea nuovo** e immettere *myResourceGroupA*
    - **Località**: *Stati Uniti orientali*
4. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myVnetA*. Fare clic su **myVnetA** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myVnetA** rete virtuale.
5. In hello **myVnetA** pannello visualizzato, fare clic su **Access control (IAM)** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello.
6. In hello **myVnetA - controllo di accesso (IAM)** pannello visualizzato, fare clic su **+ Aggiungi**.
7. In hello **aggiungere autorizzazioni** pannello viene visualizzato, selezionare **collaboratore rete** in hello **ruolo** casella.
8. In hello **selezionare** selezionare UserB o digitare toosearch indirizzo di posta elettronica dell'utente b. Hello elenco di utenti illustrato proviene da hello stesso tenant di Azure Active Directory come la rete virtuale hello si sta configurando hello peering per. Fare clic su UserB quando viene visualizzato nell'elenco di hello.
9. Fare clic su **Salva**.
10. Disconnettersi da portale hello come UtenteA, quindi accedere come utente b.
11. Fare clic su **+ nuovo**, tipo *rete virtuale* in hello **hello ricerca Marketplace** casella, quindi fare clic su **rete virtuale** nei risultati della ricerca hello .
12. In hello **rete virtuale** pannello viene visualizzato, selezionare **classico** in hello **selezionare un modello di distribuzione** casella, quindi fare clic su **crea**.
13.   Nella finestra hello crea rete virtuale (classico) che viene visualizzata, immettere hello seguenti valori:

    - **Nome**: *myVnetB*
    - **Spazio indirizzi**: *10.1.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.1.0.0/24*
    - **Sottoscrizione**: selezionare la sottoscrizione B.
    - **Gruppo di risorse**: selezionare **Crea nuovo** e immettere *myResourceGroupB*
    - **Località**: *Stati Uniti orientali*

14. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myVnetB*. Fare clic su **myVnetB** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myVnetB** rete virtuale.
15. In hello **myVnetB** pannello visualizzato, fare clic su **proprietà** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello. Hello copia **ID risorsa**, che viene utilizzato in un passaggio successivo. ID della risorsa Hello è simile toohello seguente esempio: /Subscriptions/<ID<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Completare i passaggi da 5 a 9 per myVnetB immettendo **UserA** nel passaggio 8.
17. Disconnettersi da portale hello come utente b e accedere come utente.
18. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myVnetA*. Fare clic su **myVnetA** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myVnet** rete virtuale.
19. Fare clic su **myVnetA**.
20. In hello **myVnetA** pannello visualizzato, fare clic su **peering** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello.
21. In hello **myVnetA - peering** blade che venivano visualizzate, fare clic su **+ Aggiungi**
22. In hello **Aggiungi peering** blade che viene visualizzata, immettere o selezionare hello le opzioni seguenti, quindi fare clic su **OK**:
     - **Nome**: *myVnetAToMyVnetB*
     - **Modello di distribuzione della rete virtuale**: selezionare **Classica**.
     - **Conosco l'ID della risorsa**: selezionare questa casella di controllo.
     - **ID di risorsa**: immettere l'ID risorsa hello myVnetB dal passaggio 15.
     - **Consenti accesso alla rete virtuale:** assicurarsi che sia selezionato **Abilitato**.
    Questa esercitazione non prevede l'uso di altre impostazioni. lettura toolearn su tutte le impostazioni peer, [gestire peering di reti virtuali](virtual-network-manage-peering.md#create-a-peering).
23. Dopo aver fatto clic **OK** nel passaggio precedente hello, hello **Aggiungi peering** pannello chiude e viene visualizzato hello **myVnetA - peering** pannello nuovamente. Dopo alcuni secondi, hello peering creato viene visualizzato nel pannello hello. **Connesso** è elencato nella hello **stato PEERING** colonna per hello **myVnetAToMyVnetB** peering è creato. Hello peering viene stabilito ora. È presente alcuna necessità toopeer hello rete virtuale (classico) toohello virtuale rete Gestione risorse ().

    Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
25. **Facoltativo**: le risorse di hello toodelete creati in questa esercitazione, hello completo di passaggi di hello [eliminare risorse](#delete-portal) sezione di questo articolo.

## <a name="cli"></a>Creare un peering - Interfaccia della riga di comando di Azure

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si utilizza un account che dispone di autorizzazioni tooboth sottoscrizioni, è possibile utilizzare hello stesso account per tutti i passaggi, ignorare i passaggi di hello per la registrazione all'esterno di Azure e rimuovere righe hello di script che creano le assegnazioni di ruolo di utente. Sostituire UserA@azure.com e UserB@azure.com in tutti i seguenti script con i nomi utente hello in uso per UserA e UserB hello. 

Prima di completare i passaggi hello, è necessario registrare per l'anteprima di hello. tooregister, hello completato i passaggi in hello [registrazione per l'anteprima di hello](#register) sezione di questo articolo. Non proseguire con hello rimanenti passaggi fino a quando non sono registrate entrambe le sottoscrizioni per l'anteprima di hello.

1. [Installare](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) rete virtuale di hello toocreate hello Azure CLI 1.0 (classico).
2. Aprire una sessione CLI e accedere come utente b utilizzando hello tooAzure `azure login` comando.
3. Eseguire hello CLI in modalità di gestione del servizio immettendo hello `azure config mode asm` comando.
4. Immettere hello comando toocreate hello rete virtuale (classico) seguente:
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Hello rimanenti passaggi deve essere completata con una shell bash hello Azure CLI 2.0.4 o versioni successive [installato](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), oppure utilizzando hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. Fare clic su hello **provarla** pulsante hello gli script seguenti, che consente di aprire una Shell di Cloud che consente l'accesso tooyour account Azure. Per le opzioni di esecuzione bash gli script CLI in un client Windows, vedere [in esecuzione hello CLI di Azure in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Lo script seguente hello copia viene tooa editor di testo sul PC. Sostituire `<SubscriptionB-Id>` con l'ID della sottoscrizione. Se non si conosce l'Id sottoscrizione, immettere hello `az account show` comando. valore per Hello **id** in hello l'output è l'ID sottoscrizione. Copiare script hello modificato, incollarlo nella sessione tooyour CLI 2.0 e quindi premere `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Al momento della creazione rete virtuale hello (classico) nel passaggio 4, Azure creato rete virtuale hello in hello *predefinito rete* gruppo di risorse.
7. Accedi hello CLI 2.0 UserB da Azure e accedere come utente.
8. Creare un gruppo di risorse e una rete virtuale con Resource Manager. Esempio hello copia script, incollarlo in una sessione CLI tooyour e quindi premere `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
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

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Creare una rete virtuale peering tra hello due reti virtuali create tramite hello diversi modelli di distribuzione. Lo script seguente hello copia viene tooa editor di testo sul PC. Sostituire `<SubscriptionB-id>` con l'ID della sottoscrizione. Se non si conosce l'Id sottoscrizione, immettere hello `az account show` comando. valore per Hello **id** in hello l'output è l'ID sottoscrizione. Azure creato rete virtuale a hello (classico) creato nel passaggio 4 in un gruppo di risorse denominato *predefinito rete*. Incollare hello modificato script nella sessione CLI e quindi premere `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Dopo l'esecuzione di script hello esaminare hello peering per la rete virtuale hello Gestione risorse (). Copiare lo script seguente hello e quindi incollarlo nella sessione CLI:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    output di Hello Visualizza **connesso** in hello **PeeringState** colonna.

    Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
12. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-cli) in questo articolo.

## <a name="powershell"></a>Creare un peering - PowerShell

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si utilizza un account che dispone di autorizzazioni tooboth sottoscrizioni, è possibile utilizzare hello stesso account per tutti i passaggi, ignorare i passaggi di hello per la registrazione all'esterno di Azure e rimuovere righe hello di script che creano le assegnazioni di ruolo di utente. Sostituire UserA@azure.com e UserB@azure.com in tutti i seguenti script con i nomi utente hello in uso per UserA e UserB hello. 

Prima di completare i passaggi hello, è necessario registrare per l'anteprima di hello. tooregister, hello completato i passaggi in hello [registrazione per l'anteprima di hello](#register) sezione di questo articolo. Non proseguire con hello rimanenti passaggi fino a quando non sono registrate entrambe le sottoscrizioni per l'anteprima di hello.

1. Installare hello l'ultima versione di hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) e [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) moduli. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Avviare una sessione di PowerShell.
3. In PowerShell, accedere nella sottoscrizione di tooUserB UserB immettendo hello `Add-AzureAccount` comando.
4. toocreate una rete virtuale (classica) con PowerShell, è necessario creare una nuova o modificarne un esistente, il file di configurazione di rete. Informazioni su come troppo[esportare, aggiornare e importare il file di configurazione di rete](virtual-networks-using-network-configuration-file.md). Hello file deve includere il seguente hello **VirtualNetworkSite** elemento per la rete virtuale di hello utilizzati in questa esercitazione:

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
    > L'importazione di un file di configurazione di rete modificato può causare modifiche tooexisting reti virtuali (classiche) nella sottoscrizione. Assicurarsi di aggiungere solo reti virtuali precedente hello e di non modificare o rimuovere qualsiasi rete virtuale esistente dalla sottoscrizione. 

5. Accedere nella sottoscrizione di tooUserB i comandi di gestione risorse di UserB toouse immettendo hello `login-azurermaccount` comando.
6. Assegnare a UserA autorizzazioni toovirtual rete seguente hello B. copia dello script di editor di testo tooa nel PC e sostituire `<SubscriptionB-id>` con ID hello sottoscrizione B. Se non si conosce l'Id sottoscrizione hello, immettere hello `Get-AzureRmSubscription` tooview comando è. valore per Hello **Id** in hello restituito l'output è l'ID sottoscrizione. Azure creato rete virtuale a hello (classico) creato nel passaggio 4 in un gruppo di risorse denominato *predefinito rete*. script di hello tooexecute, lo script modificato hello copia, incollarlo in tooPowerShell e quindi premere `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Disconnettersi da Azure come utente b e riconnettersi nella sottoscrizione di tooUserA UserA immettendo hello `login-azurermaccount` comando. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
8. Creare una rete virtuale hello (gestione delle risorse) copiando lo script, incollarlo in tooPowerShell e premendo quindi seguente hello `Enter`:

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

9. Assegnare UserB toomyVnetA di autorizzazioni. Esempio hello copia script editor di testo tooa nel PC e sostituire `<SubscriptionA-Id>` con hello ID della sottoscrizione A. Se non si conosce l'Id sottoscrizione hello, immettere hello `Get-AzureRmSubscription` tooview comando è. valore per Hello **Id** in hello restituito l'output è l'ID sottoscrizione. Incollare hello versione modificata dello script hello in PowerShell e quindi premere `Enter` tooexecute è.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Copia hello seguente script di editor di testo tooa nel PC e sostituire `<SubscriptionB-id>` con hello l'ID di sottoscrizione B. toopeer myVnetA toomyVNetB, copiare script hello modificato, incollarlo in tooPowerShell e quindi premere `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Visualizzare lo stato di peering hello di myVnetA copiando lo script, incollarlo in PowerShell e quindi premendo seguente hello `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    è stato Hello **connesso**. Diventa troppo**connesso** quando si configura hello toomyVnetA peering da myVnetB.

    Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
13. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-powershell) in questo articolo.

## <a name="permissions"></a>Autorizzazioni

Hello che è utilizzare una rete virtuale peering toocreate devono disporre hello necessarie ruolo o autorizzazioni. Ad esempio, se si sono stati peering due reti virtuali denominate myVnetA e myVnetB, all'account deve essere assegnato hello seguente ruolo minimo o autorizzazioni per ogni rete virtuale:
    
|Rete virtuale|Modello di distribuzione|Ruolo|Autorizzazioni|
|---|---|---|---|
|myVnetA|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnetB|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Altre informazioni, vedere [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e l'assegnazione di autorizzazioni specifiche troppo[ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Gestione risorse (solo).

## <a name="delete"></a>Eliminare risorse
Al termine di questa esercitazione, è possibile risorse hello toodelete creato nell'esercitazione di hello, in modo non si incorrere in costi di utilizzo. Un gruppo di risorse anche se si elimina tutte le risorse che si trovano nel gruppo di risorse hello.

### <a name="delete-portal"></a>Portale di Azure

1. Nella casella di ricerca portale hello, immettere **myResourceGroupA**. Nei risultati della ricerca hello, fare clic su **myResourceGroupA**.
2. In hello **myResourceGroupA** pannello, fare clic su hello **eliminare** icona.
3. l'eliminazione di hello tooconfirm, in hello **hello di tipo nome gruppo di risorse** immettere **myResourceGroupA**, quindi fare clic su **eliminare**.
4. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myVnetB*. Fare clic su **myVnetB** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myVnetB** rete virtuale.
5. In hello **myVnetB** pannello, fare clic su **eliminare**.
6. l'eliminazione di hello tooconfirm, fare clic su **Sì** in hello **rete virtuale Delete** casella.

### <a name="delete-cli"></a>

1. Accedere utilizzando hello tooAzure rete virtuale di hello toodelete 2.0 CLI Gestione risorse () con hello comando seguente:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Accedere utilizzando hello tooAzure rete virtuale di hello toodelete 1.0 CLI di Azure (versione classica) con hello seguenti comandi:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Al prompt dei comandi di PowerShell hello, immettere hello comando toodelete hello (Resource Manager) di rete virtuale seguente:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello rete virtuale (classico) con PowerShell, è necessario modificare un file di configurazione di rete esistente. Informazioni su come troppo[esportare, aggiornare e importare il file di configurazione di rete](virtual-networks-using-network-configuration-file.md). Rimuovere hello elemento VirtualNetworkSite per la rete virtuale di hello utilizzati in questa esercitazione seguente:

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
    > L'importazione di un file di configurazione di rete modificato può causare modifiche tooexisting reti virtuali (classiche) nella sottoscrizione. Assicurarsi di rimuovere solo la rete virtuale precedente di hello e di non modificare o rimuovere qualsiasi altra rete virtuale esistente dalla sottoscrizione. 

## <a name="next-steps"></a>Passaggi successivi

- Acquisire familiarità con importanti [vincoli e comportamenti del peering di rete virtuale](virtual-network-manage-peering.md#requirements-and-constraints) prima di creare un peering di rete virtuale per l'uso in produzione.
- Acquisire informazioni più dettagliate su tutte le [impostazioni per il peering di rete virtuale](virtual-network-manage-peering.md#create-a-peering).
- Informazioni su come troppo[creare un hub e spoke topologia di rete](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con peering di rete virtuale.

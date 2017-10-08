---
title: peering - Resource Manager - diverse sottoscrizioni di rete virtuale di Azure aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate una rete virtuale peering tra reti virtuali create tramite Gestione risorse presenti in diverse sottoscrizioni di Azure.
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Creare un peering di rete virtuale - Resource Manager, sottoscrizioni diverse 

In questa esercitazione viene illustrato toocreate peering tra reti virtuali create tramite Gestione risorse di rete virtuale. reti virtuali Hello si trovano in diverse sottoscrizioni. Peering due risorse di consente di reti virtuali in reti virtuali diverse toocommunicate reciprocamente con hello stessa larghezza di banda e latenza, come se fosse di risorse hello in hello stessa rete virtuale. Altre informazioni sul [Peering di rete virtuale](virtual-network-peering-overview.md). 

Hello passaggi toocreate un peering di reti virtuali sono diversi, a seconda che le reti virtuali hello siano hello uguale o diverso, sottoscrizioni e che [modello di distribuzione Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) vengono create le reti virtuali hello tramite. Informazioni su come toocreate un virtuale rete peering in altri scenari, fare clic su uno scenario di hello di hello nella tabella seguente:

|Modello di distribuzione di Azure  | Sottoscrizione di Azure  |
|--------- |---------|
|[Entrambi con Resource Manager](virtual-network-create-peering.md) |Uguale|
|[Uno con Resource Manager, uno con una distribuzione classica](create-peering-different-deployment-models.md) |Uguale|
|[Uno con Resource Manager, uno con una distribuzione classica](create-peering-different-deployment-models-subscriptions.md) |Diversa|

Impossibile creare una rete virtuale peering tra due reti virtuali distribuite tramite il modello di distribuzione classica hello. Un peering di reti virtuali può essere creato solo tra due reti virtuali presenti in hello stessa regione di Azure. Quando la creazione di una rete virtuale peering tra reti virtuali presenti in diverse sottoscrizioni, le sottoscrizioni devono essere entrambi hello associata toohello stesso tenant Azure Active Directory. Se non si ha già un tenant di Azure Active Directory, è possibile [crearne uno](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rapidamente. Se è necessario tooconnect virtuale reti che sono stati creati tramite il modello di distribuzione classica hello, che esistono in diverse aree di Azure o che esistono nelle sottoscrizioni associate toodifferent tenant di Azure Active Directory, è possibile usare un Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello reti virtuali. 

È possibile utilizzare hello [portale di Azure](#portal), hello Azure [interfaccia della riga di comando](#cli) (CLI), o Azure [PowerShell](#powershell) toocreate un peering di rete virtuale. Fare clic su uno qualsiasi dei hello precedente dello strumento collegamenti toogo direttamente toohello i passaggi per la creazione di una rete virtuale peering utilizzando lo strumento di scelta.

## <a name="portal"></a>Creare un peering - Portale di Azure

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si utilizza un account che dispone di autorizzazioni tooboth sottoscrizioni, è possibile utilizzare hello stesso account per tutti i passaggi, ignorare i passaggi di hello per la registrazione dal portale hello e ignorare i passaggi di hello per l'assegnazione di reti virtuali toohello di autorizzazioni di un altro utente.

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
8. In hello **selezionare** casella, selezionare un utente b o digitare toosearch indirizzo di posta elettronica dell'utente b. Hello elenco di utenti illustrato proviene da hello stesso tenant di Azure Active Directory come la rete virtuale hello si sta configurando hello peering per.
9. Fare clic su **Salva**.
10. In hello **myVnetA - controllo di accesso (IAM)** pannello, fare clic su **proprietà** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello. Hello copia **ID risorsa**, che viene utilizzato in un passaggio successivo. ID della risorsa Hello è simile toohello seguente esempio: /Subscriptions/<ID<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. Disconnettersi da portale hello come UtenteA, quindi accedere come utente b.
12. Completare i passaggi 2 e 3, immettere o selezionare hello seguenti valori nel passaggio 3:

    - **Nome**: *myVnetB*
    - **Spazio indirizzi**: *10.1.0.0/16*
    - **Nome subnet**: *predefinito*
    - **Intervallo di indirizzi subnet**: *10.1.0.0/24*
    - **Sottoscrizione**: selezionare la sottoscrizione B.
    - **Gruppo di risorse**: selezionare **Crea nuovo** e immettere *myResourceGroupB*
    - **Località**: *Stati Uniti orientali*

13. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myVnetB*. Fare clic su **myVnetB** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myVnetB** rete virtuale.
14. In hello **myVnetB** pannello visualizzato, fare clic su **proprietà** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello. Hello copia **ID risorsa**, che viene utilizzato in un passaggio successivo. ID della risorsa Hello è simile toohello seguente esempio: /Subscriptions/<ID<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Fare clic su **Access control (IAM)** in hello **myVnetB** blade e quindi i passaggi da 5 a 10 per completare myVnetB, immettendo **UserA** nel passaggio 8.
16. Disconnettersi da portale hello come utente b e accedere come utente.
17. In hello **individuare risorse** casella nella parte superiore di hello del portale di hello, tipo *myVnetA*. Fare clic su **myVnetA** quando viene visualizzato nei risultati della ricerca hello. Viene visualizzato un pannello per hello **myVnet** rete virtuale.
18. Fare clic su **myVnetA**.
19. In hello **myVnetA** pannello visualizzato, fare clic su **peering** elenco verticale di hello di opzioni sul lato sinistro di blade hello hello.
20. In hello **myVnetA - peering** blade che venivano visualizzate, fare clic su **+ Aggiungi**
21. In hello **Aggiungi peering** blade che viene visualizzata, immettere o selezionare hello le opzioni seguenti, quindi fare clic su **OK**:
     - **Nome**: *myVnetAToMyVnetB*
     - **Modello di distribuzione della rete virtuale**: selezionare **Resource Manager**.
     - **Conosco l'ID della risorsa**: selezionare questa casella di controllo.
     - **ID di risorsa**: immettere l'ID di risorsa hello dal passaggio 14.
     - **Consenti accesso alla rete virtuale:** assicurarsi che sia selezionato **Abilitato**.
    Questa esercitazione non prevede l'uso di altre impostazioni. lettura toolearn su tutte le impostazioni peer, [gestire peering di reti virtuali](virtual-network-manage-peering.md#create-a-peering).
22. Dopo aver fatto clic **OK** nel passaggio precedente hello, hello **Aggiungi peering** pannello chiude e viene visualizzato hello **myVnetA - peering** pannello nuovamente. Dopo alcuni secondi, hello peering creato viene visualizzato nel pannello hello. **Avviato** è elencato nella hello **stato PEERING** colonna per hello **myVnetAToMyVnetB** peering è creato. Si è stato effettuato il peering myVnetA toomyVnetB, ma ora è necessario connettersi myVnetB toomyVnetA. peering Hello è necessario creare in entrambe le direzioni risorse tooenable hello toocommunicate di reti virtuali tra loro.
23. Disconnettersi da portale hello come UserA e accedere come utente b.
24. Completare di nuovo i passaggi da 17 a 21 per myVnetB. Nel passaggio 21, nome hello peering *myVnetBToMyVnetA*selezionare *myVnetA* per **rete virtuale**e immettere l'ID di hello al passaggio 10 in hello **IDdirisorsa** casella.
25. Pochi secondi dopo aver fatto clic **OK** toocreate hello peering per myVnetB, hello **myVnetBToMyVnetA** peering appena creato viene elencato con **connesso** in hello  **Lo stato di PEERING** colonna.
26. Disconnettersi da portale hello come utente b e accedere come utente.
27. Completare di nuovo i passaggi da 17 a 19. Hello **stato PEERING** per hello **myVnetAToVNetB** peering fa ora parte anche **connesso**. peering Hello è stata stabilita correttamente dopo aver visualizzato **connesso** in hello **stato PEERING** colonna per entrambe le reti virtuali nel peering hello. Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
29. **Facoltativo**: le risorse di hello toodelete creati in questa esercitazione, hello completo di passaggi di hello [eliminare risorse](#delete-portal) sezione di questo articolo.

## <a name="cli"></a>Creare un peering - Interfaccia della riga di comando di Azure

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si utilizza un account che dispone di autorizzazioni tooboth sottoscrizioni, è possibile utilizzare hello stesso account per tutti i passaggi, ignorare i passaggi di hello per la registrazione all'esterno di Azure e rimuovere righe hello di script che creano le assegnazioni di ruolo di utente. Sostituire UserA@azure.com e UserB@azure.com in tutti i seguenti script con i nomi utente hello in uso per UserA e UserB hello.

Hello lo script seguente:

- Richiede hello Azure CLI versione 2.0.4 o versioni successive. versione di hello toofind, eseguire `az --version`. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Funziona in una shell Bash. Per opzioni all'esecuzione di script CLI di Azure su client Windows, vedere [in esecuzione hello CLI di Azure in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Anziché installare hello CLI e le relative dipendenze, è possibile utilizzare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. Fare clic su hello **provarla** pulsante nello script hello che segue, che richiama una Shell di Cloud che è possibile accedere tooyour account Azure con. 

1. Aprire una sessione CLI e accedere come UserA utilizzando hello tooAzure `azure login` comando. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
2. Copiare hello seguendo l'editor di testo script tooa nel PC, sostituire `<SubscriptionA-Id>` con ID di SubscriptionA hello, quindi hello copia lo script modificato, incollarlo nella sessione CLI, premere `Enter`. Se non si conosce l'Id sottoscrizione, immettere il comando di 'Mostra account az' hello. valore per Hello **id** in hello l'output è l'ID sottoscrizione.

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     assegnazione di Hello dell'autorizzazione per l'utente b non è un requisito. Peering può essere stabilito anche se gli utenti singolarmente generano richieste di peering per le loro rispettive reti virtuali, purché hello richiede corrispondenza. Aggiunta di un utente con privilegi di myVNetB come un collaboratore alla rete nella rete virtuale locale hello rende più semplice programma di installazione toodo hello.
3. Disconnettersi da Azure come UserA utilizzando hello `az logout` comando, quindi accedi tooAzure come utente b. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
4. Creare myVnetB. Copiare il contenuto di script hello nell'editor di testo passaggio 2 tooa sul PC. Sostituire `<SubscriptionA-Id>` con ID di SubscriptionB hello. Modificare 10.0.0.0/16 too10.1.0.0/16 e modifica tutti come tooB tooA Bs tutti. Copiare hello modificare script e incollarla nella sessione CLI tooyour e premere `Enter`. 
5. Disconnettersi da Azure come utente b e accedere tooAzure come utente.
6. Creare una rete virtuale peering da myVnetA toomyVnetB. Copiare hello seguendo l'editor di testo tooa script contenuto nel PC. Sostituire `<SubscriptionB-Id>` con ID di SubscriptionB hello. script di hello tooexecute, lo script modificato hello copia, incollarlo nella sessione CLI e premere INVIO.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. Consente di visualizzare lo stato di peering hello di myVnetA.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    è stato Hello **avviato**. Diventa troppo**connesso** dopo aver creato hello peering toomyVnetA da myVnetB.

8. Disconnettersi UserA da Azure e accedere in tooAzure come utente b.
9. Creare hello peering da myVnetB toomyVnetA. Copiare il contenuto di script hello nell'editor di testo passaggio 6 tooa nel PC. Sostituire `<SubscriptionB-Id>` con hello ID SubscriptionA e modificare tutti come tooB e tooA Bs tutti. Dopo aver apportato le modifiche di hello, hello copia lo script modificato, incollarlo nella sessione CLI e premere `Enter`.
10. Consente di visualizzare lo stato di peering hello di myVnetB. Copiare il contenuto di script hello nell'editor di testo passaggio 7 tooa sul PC. Modificare un tooB per gruppo di risorse hello e nomi di rete virtuale, copiare script hello, incollare hello modificato script nella sessione CLI tooyour e quindi premere `Enter`. Hello peering lo stato è **connesso**. Hello troppo peering lo stato delle modifiche myVnetA**connesso** dopo aver creato hello peering da myVnetB toomyVnetA. È possibile riconnettersi a UserA tooAzure e passaggio Completamento 7 tooverify hello peering stato myVnetA. 

    > [!NOTE]
    > Hello peering non viene stabilita fino a quando non è stato peering hello **connesso** per entrambe le reti virtuali.

11. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
12. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-cli) in questo articolo.

Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Creare un peering - PowerShell

Questa esercitazione usa account diversi per ogni sottoscrizione. Se si utilizza un account che dispone di autorizzazioni tooboth sottoscrizioni, è possibile utilizzare hello stesso account per tutti i passaggi, ignorare i passaggi di hello per la registrazione all'esterno di Azure e rimuovere righe hello di script che creano le assegnazioni di ruolo di utente. Sostituire UserA@azure.com e UserB@azure.com in tutti i seguenti script con i nomi utente hello in uso per UserA e UserB hello.

1. Installare hello l'ultima versione di hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modulo. Se si tooAzure nuovo PowerShell, vedere [Panoramica di Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Avviare una sessione di PowerShell.
3. In PowerShell, accedere tooAzure come UserA immettendo hello `login-azurermaccount` comando. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
4. Creare un gruppo di risorse e la rete virtuale r. copia hello segue testo tooa script editor nel PC. Sostituire `<SubscriptionA-Id>` con ID di SubscriptionA hello. Se non si conosce l'Id sottoscrizione, immettere hello `Get-AzureRmSubscription` tooview comando è. valore per Hello **Id** in hello restituito l'output è l'ID sottoscrizione. script di hello tooexecute, lo script modificato hello copia, incollarlo in tooPowerShell e quindi premere `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    assegnazione di Hello dell'autorizzazione per l'utente b non è un requisito. Peering può essere stabilito anche se gli utenti singolarmente generano richieste di peering per le loro rispettive reti virtuali, purché hello richiede corrispondenza. Aggiunta di un utente con privilegi di hello altra rete virtuale come un utente nella rete virtuale locale hello rende più semplice programma di installazione toodo hello.
5. Disconnettere UserA da Azure e accedere come UserB. account Hello che si accede è necessario hello delle autorizzazioni necessarie toocreate un peering di rete virtuale. Vedere hello [autorizzazioni](#permissions) sezione di questo articolo per informazioni dettagliate.
6. Copiare il contenuto di script hello nell'editor di testo passaggio 4 tooa sul PC. Sostituire `<SubscriptionA-Id>` con ID hello too10.1.0.0/16 10.0.0.0/16 B. modifica di sottoscrizione. Modificare tutti come tooB e tooA Bs tutti. script di hello tooexecute, lo script modificato hello copia, Incolla in PowerShell e quindi premere `Enter`.
7. Disconnettere UserB da Azure e accedere come UserA.
8. Creare hello peering da myVnetA toomyVnetB. Lo script seguente hello copia viene tooa editor di testo sul PC. Sostituire `<SubscriptionB-Id>` con hello l'ID di sottoscrizione script hello tooexecute b., copiare script hello modificato, incollare in tooPowerShell e quindi premere `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. Consente di visualizzare lo stato di peering hello di myVnetA.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    è stato Hello **avviato**. Diventa troppo**connesso** quando si configura hello toomyVnetA peering da myVnetB.

10. Disconnettere UserA da Azure e accedere come UserB.
11. Creare hello peering da myVnetB toomyVnetA. Copiare il contenuto di script hello nell'editor di testo passaggio 8 tooa sul PC. Sostituire `<SubscriptionB-Id>` con hello ID di sottoscrizione A e modifica tooB dell'e tooA tutti B. script di hello tooexecute, lo script modificato hello copia, incollarlo in tooPowerShell e quindi premere `Enter`.
12. Consente di visualizzare lo stato di peering hello di myVnetB. Copiare il contenuto di script hello nell'editor di testo passaggio 9 tooa sul PC. Modificare un tooB per gruppo di risorse hello e nomi di rete virtuale. script di hello tooexecute, incollare hello Modifica script di PowerShell e quindi premere `Enter`. è stato Hello **connesso**. stato peering di Hello **myVnetA** modificato anche**connesso** dopo aver creato hello peering da **myVnetB** troppo**myVnetA**. È possibile riconnettersi a UserA tooAzure e passaggio Completamento 9 tooverify hello peering stato myVnetA. 

    > [!NOTE]
    > Hello peering non viene stabilita fino a quando non è stato peering hello **connesso** per entrambe le reti virtuali.

    Tutte le risorse di Azure che crei in entrambe le reti virtuali sono ora in grado di toocommunicate tra loro tramite i relativi indirizzi IP. Se si utilizza la risoluzione dei nomi di Azure predefinito per le reti virtuali hello, hello risorse nelle reti virtuali hello non sono in grado di tooresolve nomi tra reti virtuali hello. Se si desidera tooresolve nomi tra reti virtuali in un peering, è necessario creare il proprio server DNS. Informazioni su come tooset backup [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **Parametro facoltativo**: anche se la creazione di macchine virtuali non viene descritta in questa esercitazione, è possibile creare una macchina virtuale in ogni rete virtuale e connettersi da una macchina virtuale toohello altre toovalidate connettività.
14. **Parametro facoltativo**: risorse hello toodelete create in questa esercitazione, hello completato i passaggi [eliminare risorse](#delete-powershell) in questo articolo.

## <a name="permissions"></a>Autorizzazioni

Hello che è utilizzare una rete virtuale peering toocreate devono disporre hello necessarie ruolo o autorizzazioni. Ad esempio, se si sono stati peering due reti virtuali denominate **myVnetA** e **myVnetB**, l'account deve essere assegnato hello seguente ruolo minimo o autorizzazioni per ogni rete virtuale:
    
|Rete virtuale|Ruolo|Autorizzazioni|
|---|---|---|
|myVnetA|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Altre informazioni, vedere [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e l'assegnazione di autorizzazioni specifiche troppo[ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Gestione risorse (solo).

## <a name="delete"></a>Eliminare risorse
Al termine di questa esercitazione, è possibile risorse hello toodelete creato nell'esercitazione di hello, in modo non si incorrere in costi di utilizzo. Un gruppo di risorse anche se si elimina tutte le risorse che si trovano nel gruppo di risorse hello.

### <a name="delete-portal"></a>Portale di Azure

1. Accedere toohello portale di Azure come utente.
2. Nella casella di ricerca portale hello, immettere **myResourceGroupA**. Nei risultati della ricerca hello, fare clic su **myResourceGroupA**.
3. In hello **myResourceGroupA** pannello, fare clic su hello **eliminare** icona.
4. l'eliminazione di hello tooconfirm, in hello **hello di tipo nome gruppo di risorse** immettere **myResourceGroupA**, quindi fare clic su **eliminare**.
5. Disconnettersi da portale hello come UserA e accedere come utente b.
6. Completare i passaggi da 2 a 4 per myResourceGroupB.

### <a name="delete-cli"></a>

1. Accedi tooAzure come UserA ed eseguire hello comando seguente:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. Disconnettersi da Azure come UserA e accedere come UserB.
3. Eseguire hello comando seguente:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. Accedi tooAzure come UserA ed eseguire hello comando seguente:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. Disconnettersi da Azure come UserA e accedere come UserB.
3. Eseguire hello comando seguente:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Passaggi successivi

- Acquisire familiarità con importanti [vincoli e comportamenti del peering di rete virtuale](virtual-network-manage-peering.md#requirements-and-constraints) prima di creare un peering di rete virtuale per l'uso in produzione.
- Acquisire informazioni più dettagliate su tutte le [impostazioni per il peering di rete virtuale](virtual-network-manage-peering.md#create-a-peering).
- Informazioni su come troppo[creare un hub e spoke topologia di rete](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con peering di rete virtuale.

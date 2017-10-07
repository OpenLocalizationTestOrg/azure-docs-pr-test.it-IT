---
title: aaaCreate, modificare o eliminare una rete virtuale di Azure | Documenti Microsoft
description: Informazioni su come toocreate, modificare o eliminare una rete virtuale in Azure.
services: virtual-network
documentationcenter: na
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
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Creare, modificare o eliminare una rete virtuale

Informazioni su come toocreate ed eliminare un virtuale rete e modificare le impostazioni, come i server DNS e indirizzo IP spazi, per una rete virtuale esistente.

Una rete virtuale è una rappresentazione della rete nel cloud hello. Una rete virtuale è un isolamento logico di hello Azure cloud dedicato tooyour sottoscrizione di Azure. Per ogni rete virtuale creata, è possibile:
- Scegliere un tooassign di spazio di indirizzo. Uno spazio indirizzi è costituito da uno o più intervalli di indirizzi, definiti tramite la notazione CIDR (Classless Inter-Domain Routing), ad esempio 10.0.0.0/16.
- Scegliere il server DNS fornito da Azure di hello toouse oppure utilizzare il proprio server DNS. Tutte le risorse di rete virtuale connessa toohello vengono assegnate i nomi tooresolve questo server DNS nella rete virtuale hello.
- Segmento hello rete virtuale nella subnet, ognuno con il proprio intervallo di indirizzi, nello spazio di indirizzi hello della rete virtuale hello. toolearn toocreate, modifica e subnet di eliminazione, vedere [Aggiungi, modifica o Elimina subnet](virtual-network-manage-subnet.md).

Questo articolo spiega come toocreate, modificare ed eliminare le reti virtuali con modello di distribuzione Azure Resource Manager hello.

## <a name="before"></a>Prima di iniziare

Prima di iniziare l'attività hello descritte in questo articolo, completare hello seguenti prerequisiti:

- Se si tooworking nuovo con le reti virtuali, che è consigliabile consultare esercizio hello in [creare la prima rete virtuale Azure](virtual-network-get-started-vnet-subnet.md). Questa esercitazione consente di acquisire maggiore familiarità con le reti virtuali.
- toolearn sui limiti per le reti virtuali, revisione [i limiti di Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Accedi al portale di Azure toohello, hello Azure strumento da riga di comando (CLI di Azure) o Azure PowerShell utilizzando l'account di Azure. Se non si ha un account di Azure, registrarsi per ottenere un [account per la versione di valutazione gratuita](https://azure.microsoft.com/free).
- Se si prevede di toouse attività hello toocomplete descritta in questo articolo i comandi di PowerShell, è necessario innanzitutto [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Assicurarsi di aver hello la versione più recente di hello cmdlet di Azure PowerShell installati. Guida di tooget per i comandi di PowerShell negli esempi di hello, immettere `get-help <command> -full`.
- Se si prevede di toouse attività hello toocomplete descritta in questo articolo i comandi CLI di Azure, è necessario innanzitutto [installare e configurare Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Assicurarsi di aver hello la versione più recente di Azure CLI installato. Guida di tooget con i comandi CLI di Azure, immettere `az <command> --help`.


## <a name="create-vnet"></a>Creare una rete virtuale

toocreate una rete virtuale:

1. Accedi toohello [portale](https://portal.azure.com) con un account che è assegnato autorizzazioni per il ruolo di collaboratore rete hello (almeno) per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Fare clic su **Nuovo** > **Rete** > **Rete virtuale**.
3. In hello **rete virtuale** pannello in hello **selezionare un modello di distribuzione** , lasciare **Gestione risorse** selezionata e quindi fare clic su **crea**.
4. In hello **crea rete virtuale** pannello, immettere o selezionare i valori per hello seguenti impostazioni, quindi fare clic su **crea**:
    - **Nome**: hello nome deve essere univoco in hello [gruppo di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) selezionare toocreate hello di rete virtuale in. È possibile modificare il nome di hello dopo aver creata la rete virtuale hello. È possibile creare più reti virtuali in momenti diversi. Per alcuni suggerimenti sull'assegnazione del nome, vedere [Naming conventions](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) (Convenzioni di denominazione). Una convenzione di denominazione seguente consente di rendere più semplice toomanage più reti virtuali.
    - **Lo spazio degli indirizzi**: specificare lo spazio degli indirizzi hello in notazione CIDR. è possibile definire spazio degli indirizzi di Hello pubbliche o private (RFC 1918). Se si definisce lo spazio degli indirizzi hello come pubblico o privato, lo spazio degli indirizzi hello è raggiungibile solo dalla rete virtuale hello, da reti virtuali interconnesse e da qualsiasi rete locale che si è connessi toohello di rete virtuale. Non è possibile aggiungere hello spazi di indirizzi seguenti:
        - 224.0.0.0/4 (multicast)
        - 255.255.255.255/32 (broadcast)
        - 127.0.0.0/8 (loopback)
        - 169.254.0.0/16 (locale rispetto al collegamento)
        - 168.63.129.16/32 (DNS interno)

      Sebbene sia possibile definire un solo spazio degli indirizzi quando si crea la rete virtuale hello, è possibile aggiungere più spazi di indirizzi dopo avere creata la rete virtuale hello. toolearn come un indirizzo tooadd spazio tooan rete virtuale esistente, vedere [aggiungere o rimuovere uno spazio degli indirizzi](#add-address-spaces) in questo articolo.

      >[!WARNING]
      >Se una rete virtuale dispone di spazi di indirizzi che si sovrappongono a un'altra rete virtuale di rete o locale, non è possibile connettere reti hello due. Prima di definire uno spazio degli indirizzi, considerare la possibilità di potrebbe tooconnect hello rete virtuale tooother le reti virtuali o reti locali in hello future.
      >
      >

    - **Nome della subnet**: nome della subnet hello deve essere univoco nella rete virtuale hello. È possibile modificare il nome di subnet hello dopo la creazione di subnet hello. portale Hello richiede la definizione di una subnet quando si crea una rete virtuale, anche se una rete virtuale non è necessario toohave qualsiasi subnet. Nel portale di hello, è possibile definire una sola subnet quando si crea una rete virtuale. È possibile aggiungere la rete virtuale altre subnet toohello in un secondo momento, dopo aver creata la rete virtuale hello. tooadd una rete virtuale tooa subnet, vedere [creare una subnet](virtual-network-manage-subnet.md#create-subnet) in [crea, modifica o Elimina subnet](virtual-network-manage-subnet.md). Per creare una rete virtuale con più subnet, è possibile usare l'interfaccia della riga di comando di Azure o PowerShell.

      >[!TIP]
      >In alcuni casi, il traffico di controllo o toofilter routing tra subnet hello admins creare subnet diverse. Prima di definire le subnet, provare a come si toofilter e instradare il traffico tra le subnet. toolearn ulteriori informazioni sui filtri di traffico tra subnet, vedere [gruppi di sicurezza di rete](virtual-networks-nsg.md). Azure effettua il routing automatico del traffico tra le subnet. È tuttavia possibile eseguire l'override delle route predefinite di Azure. toolearn come toooverride Azure predefinito subnet il routing del traffico, vedere [le route definite dall'utente](virtual-networks-udr-overview.md).
      >

    - **Intervallo di indirizzi di subnet**: hello intervallo deve essere all'interno dello spazio di indirizzo hello immesso per la rete virtuale hello. è possibile specificare intervallo più piccolo di Hello è/29, di cui fornisce otto gli indirizzi IP per subnet hello. Azure riserve hello prima e ultima indirizzi in ogni subnet per conformità al protocollo. Altri tre indirizzi sono riservati per l'uso da parte del servizio di Azure. Di conseguenza, una rete virtuale con un intervallo di indirizzi di subnet /29 ha solo tre indirizzi IP utilizzabili. Se si prevede un gateway VPN di rete virtuale tooa tooconnect, è necessario creare una subnet del gateway. Altre informazioni su [considerazioni specifiche sugli intervalli di indirizzi per le subnet di gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). È possibile modificare l'intervallo di indirizzi hello dopo la creazione di subnet hello in condizioni specifiche. toolearn toochange un intervallo di indirizzi di subnet, vedere [modificare le impostazioni di subnet](#change-subnet) in [Aggiungi, modifica o Elimina subnet](virtual-network-manage-subnet.md).
    - **Sottoscrizione**: selezionare una [sottoscrizione](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Non è possibile utilizzare hello stessa rete virtuale in più di una sottoscrizione di Azure. Tuttavia, è possibile connettere una rete virtuale in uno reti di toovirtual di sottoscrizione in altre sottoscrizioni. tooconnect reti virtuali in diverse sottoscrizioni, usare Gateway VPN di Azure o peering di rete virtuale. Deve essere di qualsiasi risorsa di Azure che si connette la rete virtuale toohello in hello stessa sottoscrizione di rete virtuale hello.
    - **Gruppo di risorse**: selezionare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) esistente o crearne uno nuovo. Può essere una risorsa di Azure che si connette la rete virtuale toohello in hello stesso gruppo di risorse di rete virtuale hello o in un gruppo di risorse diverso.
    - **Località**: selezionare una [località](https://azure.microsoft.com/regions/) di Azure. Le località sono dette anche aree. Una rete virtuale può trovarsi in una sola località di Azure. Tuttavia, è possibile connettersi una rete virtuale in una rete virtuale in tooa percorso in un'altra posizione tramite un gateway VPN. Deve essere di qualsiasi risorsa di Azure che si connette la rete virtuale toohello in hello stesso percorso di rete virtuale hello.

**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|[az network vnet create](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Visualizzare le reti virtuali e le impostazioni

reti virtuali tooview e impostazioni:

1. Accedi toohello [portale](https://portal.azure.com) con un account che è assegnato autorizzazioni per il ruolo di collaboratore rete hello (almeno) per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella di ricerca portale hello, immettere **reti virtuali**. Nei risultati della ricerca hello, fare clic su **le reti virtuali**.
3. In hello **le reti virtuali** pannello, fare clic su rete virtuale hello che si desidera utilizzare impostazioni tooview per.
4. Hello impostazioni riportate di seguito sono elencate nel Pannello di hello per la rete virtuale di hello selezionato:
    - **Panoramica**: fornisce informazioni sulla rete virtuale hello, incluso lo spazio di indirizzi e i server DNS. Hello cattura di schermata seguente vengono mostrate hello Panoramica impostazioni per una rete virtuale denominata **MyVNet**:

        ![Panoramica dell'interfaccia di rete](./media/virtual-network-manage-network/vnet-overview.png)

      In hello **Panoramica** pannello, è possibile spostare una rete virtuale tooa sottoscrizione o la risorsa gruppo diverso. toolearn toomove una rete virtuale, vedere [spostare sottoscrizione o il gruppo di risorse diverso tooa risorse](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). articolo di Hello vengono elencati i prerequisiti e come risorse toomove utilizzando hello portale di Azure, PowerShell e CLI di Azure. Tutte le risorse di rete virtuale connessa toohello devono essere spostati con la rete virtuale hello.
    - **Lo spazio degli indirizzi**: sono elencati gli spazi di indirizzi hello assegnati toohello di rete virtuale. hello di toolearn come tooadd e rimuovere uno spazio degli indirizzi, completare i passaggi in [aggiungere o rimuovere uno spazio degli indirizzi](#address-spaces) in questo articolo.
    - **I dispositivi connessi**: vengono elencate tutte le risorse di rete virtuale connessa toohello. Hello schermata precedente, tre interfacce di rete e un bilanciamento del carico di rete virtuale connessa toohello. Sono elencate le nuove risorse di creare e connettere la rete virtuale toohello. Se si elimina una risorsa di rete virtuale connessa toohello, non è più visualizzato nell'elenco di hello.
    - **Subnet**: viene visualizzato un elenco di subnet che esiste all'interno di rete virtuale hello. toolearn tooadd e rimuovere una subnet, vedere [creare una subnet](virtual-network-manage-subnet.md#create-subnet) e [eliminare una subnet](virtual-network-manage-subnet.md#delete-subnet) in [Aggiungi, modifica o Elimina subnet](virtual-network-manage-subnet.md).
    - **I server DNS**: È possibile specificare se hello Azure interno del server DNS o un server DNS personalizzato fornisce la risoluzione dei nomi per i dispositivi di rete virtuale connessa toohello. Quando si crea una rete virtuale tramite il portale di Azure hello, server DNS di Azure vengono utilizzati per la risoluzione dei nomi all'interno di una rete virtuale, per impostazione predefinita. i server DNS di hello toomodify, hello completo di passaggi [aggiungere, modificare o rimuovere un server DNS](#dns-servers) in questo articolo.
    - **Peering**: se sono presenti peering esistente nella sottoscrizione hello, essi sono elencati di seguito. È possibile visualizzare le impostazioni per i peering esistenti o creare, modificare ed eliminare peering. toolearn ulteriori informazioni su peering, vedere [peering di rete virtuale](virtual-network-peering-overview.md).
    - **Proprietà**: Visualizza le impostazioni sulle hello rete virtuale, inclusi ID risorsa della rete virtuale hello e hello è nella sottoscrizione di Azure.
    - **Diagramma**: diagramma hello fornisce una rappresentazione visiva di tutti i dispositivi di rete virtuale connessa toohello. diagramma di Hello ha alcune informazioni chiave sui dispositivi hello. toomanage un dispositivo in questa vista, nel diagramma hello, fare clic su dispositivo hello.
    - **Impostazioni comuni di Azure**: toolearn informazioni sulle impostazioni comuni di Azure, vedere hello le seguenti informazioni:
        *   [Log attività](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Controllo di accesso (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Tag](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Blocchi](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Script di automazione](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|[az network vnet show](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Aggiungere o rimuovere uno spazio indirizzi

È possibile aggiungere e rimuovere spazi indirizzi per una rete virtuale. Uno spazio degli indirizzi deve essere specificato nella notazione CIDR e non possono sovrapporsi con altri spazi degli indirizzi all'interno di hello stessa rete virtuale. è possibile definire spazi degli indirizzi di Hello pubbliche o private (RFC 1918). Se si definisce lo spazio degli indirizzi hello come pubblico o privato, lo spazio degli indirizzi hello è raggiungibile solo dalla rete virtuale hello, da reti virtuali interconnesse e da qualsiasi rete locale che si è connessi toohello di rete virtuale. Non è possibile aggiungere hello spazi di indirizzi seguenti:

- 224.0.0.0/4 (multicast)
- 255.255.255.255/32 (broadcast)
- 127.0.0.0/8 (loopback)
- 169.254.0.0/16 (locale rispetto al collegamento)
- 168.63.129.16/32 (DNS interno)

tooadd o rimuovere uno spazio degli indirizzi:

1. Accedi toohello [portale](https://portal.azure.com) con un account che è assegnato autorizzazioni per il ruolo di collaboratore rete hello (almeno) per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella di ricerca portale hello, immettere **reti virtuali**. Nei risultati della ricerca hello, selezionare **le reti virtuali**.
3. In hello **le reti virtuali** pannello, fare clic su hello rete virtuale per cui si desidera tooadd o rimuova uno spazio degli indirizzi.
4. In hello virtuale in rete pannello **impostazioni**, fare clic su **lo spazio degli indirizzi**.
5. Nel Pannello di hello hello dello spazio degli indirizzi, completare una delle seguenti opzioni hello:
    - **Aggiungere uno spazio degli indirizzi**: immettere il nuovo spazio di indirizzi hello. lo spazio degli indirizzi di Hello non può coincidere con uno spazio di indirizzi esistente definito per la rete virtuale hello.
    - **Rimuovere uno spazio indirizzi**: fare clic con il pulsante destro del mouse su uno spazio indirizzi e quindi fare clic su **Rimuovi**. Se esiste una subnet nello spazio degli indirizzi di hello, è possibile rimuovere lo spazio degli indirizzi di hello. tooremove uno spazio degli indirizzi, è necessario innanzitutto eliminare qualsiasi subnet (e le risorse che sono connessi toohello subnet) che esiste nello spazio degli indirizzi hello.
6. Fare clic su **Salva**.

**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|Solo Resource Manager|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Aggiungere, modificare o rimuovere un server DNS

Tutte le macchine virtuali che sono la rete virtuale connessa toohello registrare con il server DNS hello specificati per la rete virtuale hello. Utilizzano inoltre hello specificato server DNS per la risoluzione dei nomi. Ogni scheda di interfaccia di rete di una VM può avere le proprie impostazioni per i server DNS. Se una scheda di rete ha le proprie impostazioni di server DNS, sostituiscono le impostazioni del server per la rete virtuale hello hello DNS. toolearn informazioni sulle impostazioni DNS NIC, vedere [interfaccia attività e le impostazioni di rete](virtual-network-network-interface.md#change-dns-servers). toolearn ulteriori informazioni su risoluzione dei nomi per le macchine virtuali e istanze del ruolo in servizi Cloud di Azure, vedere [risoluzione dei nomi per le macchine virtuali e istanze del ruolo](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, modificare o rimuovere un server DNS:

1. Accedi toohello [portale](https://portal.azure.com) con un account che è assegnato autorizzazioni per il ruolo di collaboratore rete hello (almeno) per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella di ricerca del portale hello, digitare **reti virtuali**. Nei risultati della ricerca hello, selezionare **le reti virtuali**.
3. In hello **le reti virtuali** pannello, fare clic su impostazioni DNS toochange per la rete virtuale hello.
4. In hello virtuale in rete pannello **impostazioni**, fare clic su **server DNS**.
5. Selezionare una delle seguenti opzioni nel pannello hello che elenca i server DNS hello:
    - **Predefinito (fornito da Azure)**: tutti i nomi delle risorse e gli indirizzi IP privati sono toohello registrati automaticamente i server DNS di Azure. È possibile risolvere i nomi tra le risorse che sono connesso toohello stessa rete virtuale. Non è possibile utilizzare questa opzione tooresolve nomi tra reti virtuali. i nomi tooresolve più reti virtuali, è necessario utilizzare un server DNS personalizzato.
    - **Custom**: È possibile aggiungere uno o più server, backup toohello Azure limitare per una rete virtuale. toolearn ulteriori informazioni sui limiti del server DNS, vedere [i limiti di Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). È necessario hello le opzioni seguenti:
        - **Aggiungere un indirizzo**: aggiunge l'elenco di server DNS hello server tooyour rete virtuale. Questa opzione Registra anche i server DNS hello in Azure. Se è già stato registrato un server DNS in Azure, è possibile selezionare il server DNS nell'elenco di hello.
        - **Rimuovere un indirizzo**: fare clic su Avanti toohello server in cui si desidera tooremove, **X**. Eliminazione del server di hello rimuove server hello solo da questo elenco di rete virtuale. server DNS Hello rimane registrato in Azure per le altre toouse di reti virtuali.
        - **Indirizzi server DNS riordina**: è importante che questi siano elencati i server DNS in hello tooverify correggere ordine per l'ambiente. Gli elenchi dei server DNS vengono utilizzati in ordine di hello che sono state specificate. e non rappresentano una configurazione di tipo round robin. Se è possibile raggiungere i server DNS prima di hello nell'elenco di hello, hello utilizzerà tale server DNS, indipendentemente dal fatto che server DNS hello funzioni correttamente. Rimuovere tutti i server DNS hello elencati e quindi aggiungerli nuovamente nell'ordine hello desiderato.
        - **Modificare un indirizzo**: evidenziare hello server DNS nell'elenco di hello e quindi immettere hello nuovo nome.
6. Fare clic su **Salva**.
7. Riavviare le macchine virtuali hello che sono connessi toohello rete virtuale, quindi vengono assegnate nuove impostazioni del server DNS hello. Macchine virtuali continuano toouse le impostazioni DNS correnti finché non vengono riavviate.

**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Eliminare una rete virtuale

È possibile eliminare una rete virtuale solo se non esistono alcun tooit connesso alle risorse. Se sono presenti risorse tooany connesso subnet all'interno di rete virtuale hello, è necessario eliminare prima le risorse hello subnet tooall connesso in rete virtuale hello. Hello i passaggi toodelete una risorsa variano a seconda delle risorse di hello. documentazione di hello toolearn modalità di lettura le risorse toodelete toosubnets connesso, per ogni tipo di risorsa desiderato toodelete. toodelete una rete virtuale:

1. Accedi toohello [portale](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella di ricerca portale hello, immettere **reti virtuali**. Nei risultati della ricerca hello, fare clic su **le reti virtuali**.
3. In hello **le reti virtuali** blade, hello selezionare rete virtuale toodelete.
4. Nel Pannello di rete virtuale hello, tooconfirm che non sono presenti dispositivi connessi in rete virtuale toohello, **impostazioni**, fare clic su **i dispositivi connessi**. Se sono presenti dispositivi connessi, è necessario eliminarli prima di poter eliminare la rete virtuale hello. Se non sono presenti dispositivi connessi, fare clic su **Panoramica**.
5. Nella parte superiore di hello del Pannello di hello, fare clic su hello **eliminare** icona.
6. l'eliminazione di hello tooconfirm della rete virtuale hello, fare clic su **Sì**.


**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|[azure network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Passaggi successivi

- toocreate una macchina virtuale e quindi connetterla tooa di rete virtuale, vedere [creare una rete virtuale e connettere le macchine virtuali](virtual-network-get-started-vnet-subnet.md#create-vms).
- toofilter il traffico di rete tra subnet all'interno di una rete virtuale, vedere [creare gruppi di sicurezza di rete](virtual-networks-create-nsg-arm-pportal.md).
- toopeer una rete virtuale tooanother di rete virtuale, vedere [creare una rete virtuale peering](virtual-network-create-peering.md#portal).
- toolearn sulle opzioni per la connessione a una rete locale tooan di rete virtuale, vedere [sul Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).

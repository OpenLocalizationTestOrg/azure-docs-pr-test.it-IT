---
title: aaaAdd, modificare o eliminare una subnet di rete virtuale di Azure | Documenti Microsoft
description: Informazioni su come tooadd, modificare o eliminare una subnet della rete virtuale in Azure.
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
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Aggiungere, modificare o eliminare le subnet di rete virtuale

Informazioni su come tooadd, modificare o eliminare una subnet della rete virtuale. 

Se non si ha familiarità con le reti virtuali, prima di aggiungere, modificare o eliminare una subnet, è consigliabile leggere [Panoramica della rete virtuale di Azure](virtual-networks-overview.md) e [Creare, modificare o eliminare le reti virtuali](virtual-network-manage-network.md). Tutte le risorse di Azure distribuite in una rete virtuale vengono distribuite in una subnet entro una rete virtuale. In genere, vengono create più subnet all'interno di una rete virtuale per:
- **Filtrare il traffico tra subnet**. È possibile applicare rete sicurezza gruppi toosubnets toofilter in ingresso e in uscita per tutte le risorse (ad esempio macchine virtuali) che si trovano nella rete virtuale hello il traffico di rete. altre informazioni sulle toolearn toocreate un gruppo di sicurezza di rete, vedere [creare gruppi di sicurezza di rete](virtual-networks-create-nsg-arm-pportal.md).
- **Controllare il routing tra subnet**. Azure crea route predefinite in modo che il traffico venga indirizzato automaticamente tra le subnet. È possibile sostituire le route predefinite di Azure creando route definite dall'utente. toolearn più sulle route definite dall'utente, vedere [creare route definite dall'utente](virtual-network-create-udr-arm-ps.md). 

Questo articolo spiega come tooadd, modificare ed eliminare una subnet per le reti virtuali che sono state create tramite il modello di distribuzione del hello Azure Resource Manager.
 
## <a name="before"></a>Prima di iniziare

Prima di iniziare l'attività hello descritte in questo articolo, completare hello seguenti prerequisiti:

- Se si tooworking nuovo con le reti virtuali, che è consigliabile consultare esercizio hello in [creare la prima rete virtuale Azure](virtual-network-get-started-vnet-subnet.md). Questa esercitazione consente di acquisire maggiore familiarità con le reti virtuali.
- toolearn sui limiti per le reti virtuali, revisione [i limiti di Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Accedi al portale di Azure toohello, hello Azure strumento da riga di comando (CLI di Azure) o Azure PowerShell utilizzando l'account di Azure. Se non si ha un account di Azure, registrarsi per ottenere un [account per la versione di valutazione gratuita](https://azure.microsoft.com/free).
- Se si prevede di toouse attività hello toocomplete descritta in questo articolo i comandi di PowerShell, è necessario innanzitutto [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Assicurarsi di aver hello la versione più recente di hello cmdlet di Azure PowerShell installati. Guida di tooget per i comandi di PowerShell negli esempi di hello, immettere `get-help <command> -full`.
- Se si prevede di toouse che attività hello toocomplete descritta in questo articolo i comandi CLI di Azure, è necessario:
    - [Installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Assicurarsi di aver hello la versione più recente di Azure CLI installato.
    - Utilizzare hello Shell di Cloud di Azure. Anziché installare hello CLI e le relative dipendenze, è possibile utilizzare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell (**> _**) icona nella parte superiore di hello di hello portale di Azure. 

  Guida di tooget con i comandi CLI di Azure, immettere `az <command> --help`.

## <a name="create-subnet"></a>Aggiungere una subnet

tooadd una subnet:

1. Accedi toohello [portale](https://portal.azure.com) con un account che è assegnato autorizzazioni per il ruolo di collaboratore rete hello (almeno) per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella di ricerca portale hello, immettere **reti virtuali**. Nei risultati della ricerca hello, fare clic su **le reti virtuali**.
3. In hello **le reti virtuali** pannello, fare clic su tooadd si desidera una subnet per la rete virtuale hello.
4. Nel Pannello di rete virtuale hello, fare clic su **subnet**.
5. Fare clic su **+Subnet**.
6. In hello **aggiungere subnet** pannello, immettere i valori per hello seguenti parametri:
    - **Nome**: hello nome deve essere univoco all'interno di rete virtuale hello.
    - **Intervallo di indirizzi**: hello intervallo deve essere univoco all'interno dello spazio di indirizzo hello per la rete virtuale hello. intervallo di Hello non può sovrapporsi ad altri intervalli di indirizzi subnet all'interno di rete virtuale hello. specificare lo spazio degli indirizzi Hello utilizzando la notazione Classless Inter-Domain Routing (CIDR). Ad esempio, in una rete virtuale con lo spazio di indirizzi 10.0.0.0/16 è possibile definire lo spazio di indirizzi di subnet 10.0.0.0/24. è possibile specificare intervallo più piccolo di Hello è/29, di cui fornisce otto gli indirizzi IP per subnet hello. Azure riserve hello prima e ultima indirizzi in ogni subnet per conformità al protocollo. Altri tre indirizzi sono riservati per l'uso da parte del servizio di Azure. Di conseguenza, la definizione di una subnet/29 comporta tre indirizzi IP utilizzabili nella subnet hello intervallo di indirizzi. Se si prevede un gateway VPN di rete virtuale tooa tooconnect, è necessario creare una subnet del gateway. Altre informazioni su [considerazioni specifiche sugli intervalli di indirizzi per le subnet di gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). È possibile modificare l'intervallo di indirizzi hello dopo l'aggiunta di subnet hello, in condizioni specifiche. toolearn toochange un intervallo di indirizzi di subnet, vedere [modificare le impostazioni di subnet](#change-subnet) in questo articolo.
    - **Il gruppo di sicurezza di rete**: facoltativamente, è possibile associare un gruppo di sicurezza di rete esistente hello subnet toocontrol traffico di rete in ingresso e in uscita filtro per la subnet hello. Hello il gruppo di sicurezza di rete deve esistere in hello stessa sottoscrizione e il percorso di rete virtuale hello. Deve essere creato anche con modello di distribuzione di gestione risorse di hello. altre informazioni sulle toolearn toocreate un gruppo di sicurezza di rete, vedere [gruppi di sicurezza di rete](virtual-networks-create-nsg-arm-pportal.md).
    - **Tabella di route**: facoltativamente, è possibile associare una tabella di route esistente hello subnet toocontrol il traffico di rete routing tooother reti. Hello route tabella deve esistere nel hello stessa sottoscrizione e il percorso di rete virtuale hello. Deve essere creato anche con modello di distribuzione di gestione risorse di hello. toolearn altre informazioni sulle tabelle di routing toocreate, vedere [le route definite dall'utente](virtual-network-create-udr-arm-ps.md).
    - **Gli utenti**: È possibile controllare l'accesso toohello subnet utilizzando ruoli predefiniti o i ruoli personalizzati. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e utenti tooaccess hello subnet [utilizzare ruolo assegnazione toomanage accesso tooyour Azure risorse](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. tooadd hello subnet toohello rete virtuale selezionato, fare clic su **OK**.

**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>Cambiare le impostazioni della subnet

È possibile modificare i gruppi di sicurezza di rete, le tabelle di route e subnet tooa di accesso utente per la gestione delle risorse in una subnet. toolearn su queste impostazioni, in [aggiungere una subnet](#create-subnet), vedere il passaggio 6. Se si desidera spazio degli indirizzi di hello toochange di una subnet, è innanzitutto necessario eliminare tutte le risorse che si trovano nella subnet hello. Hello i passaggi toodelete una risorsa variano a seconda delle risorse di hello. toolearn come toodelete risorse presenti nella subnet, documentazione hello lettura per ogni risorsa di tipo, che si desidera toodelete. intervallo di indirizzi hello toochange per una subnet:

1. Accedi toohello [portale](https://portal.azure.com) con un account che è assegnato autorizzazioni per il ruolo di collaboratore rete hello (almeno) per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella di ricerca portale hello, immettere **reti virtuali**. Nei risultati della ricerca hello, fare clic su **le reti virtuali**.
3. In hello **le reti virtuali** pannello, fare clic su hello di rete virtuale per cui si desidera toochange un intervallo di indirizzi della subnet.
4. Fare clic su subnet hello per cui si desidera l'intervallo di indirizzi toochange hello.
5. Nel pannello subnet hello in hello **intervallo di indirizzi** , immettere il nuovo intervallo di indirizzi hello. intervallo di Hello deve essere univoco all'interno dello spazio di indirizzo hello per la rete virtuale hello. intervallo di Hello non può sovrapporsi ad altri intervalli di indirizzi subnet all'interno di rete virtuale hello. specificare lo spazio degli indirizzi Hello utilizzando la notazione CIDR. Ad esempio, in una rete virtuale con lo spazio di indirizzi 10.0.0.0/16 è possibile definire lo spazio di indirizzi di subnet 10.0.0.0/24. è possibile specificare intervallo più piccolo di Hello è/29, di cui fornisce otto gli indirizzi IP per subnet hello. Azure riserve hello prima e ultima indirizzi in ogni subnet per conformità al protocollo. Altri tre indirizzi sono riservati per l'uso da parte del servizio di Azure. Di conseguenza una subnet con l'intervallo di indirizzi /29 ha tre indirizzi IP utilizzabili. Se si prevede un gateway VPN di rete virtuale tooa tooconnect, è necessario creare una subnet del gateway. Altre informazioni su [considerazioni specifiche sugli intervalli di indirizzi per le subnet di gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). È possibile modificare l'intervallo di indirizzi hello dopo la creazione di subnet hello in condizioni specifiche. toolearn toochange un intervallo di indirizzi di subnet, vedere [modificare le impostazioni di subnet](#change-subnet) in questo articolo.
6. Fare clic su **Salva**.

**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Eliminare una subnet

È possibile eliminare una subnet solo se non sono presenti risorse nella subnet hello. Se nella subnet hello sono disponibili risorse, è necessario eliminare le risorse di hello che si trovano nella subnet hello prima di poter eliminare la subnet hello. Hello i passaggi toodelete una risorsa variano a seconda delle risorse di hello. toolearn come toodelete risorse presenti nella subnet, documentazione hello lettura per ogni risorsa di tipo, che si desidera toodelete. toodelete una subnet:

1. Accedi toohello [portale](https://portal.azure.com) con un account che è assegnato autorizzazioni per il ruolo di collaboratore rete hello (almeno) per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella di ricerca portale hello, immettere **reti virtuali**. Nei risultati della ricerca hello, fare clic su **le reti virtuali**.
3. In hello **le reti virtuali** pannello, fare clic su rete virtuale di hello da toodelete una subnet da.
4. In hello virtuale in rete pannello **impostazioni**, fare clic su **subnet**.
5. Nell'elenco di hello di subnet che viene visualizzato nel Pannello di subnet hello, subnet hello rapida toodelete, scegliere **eliminare**, quindi fare clic su **Sì** subnet hello toodelete.

**Comandi**

|Strumento|Comando|
|---|---|
|Interfaccia della riga di comando di Azure|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Passaggi successivi

toocreate una macchina virtuale in una subnet, vedere [creare una rete virtuale e distribuire macchine virtuali nella subnet hello](virtual-network-get-started-vnet-subnet.md#create-vms).

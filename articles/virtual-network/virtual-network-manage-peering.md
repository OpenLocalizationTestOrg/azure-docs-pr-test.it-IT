---
title: aaaCreate, modificare o eliminare una rete virtuale di Azure peering | Documenti Microsoft
description: Informazioni su come toocreate, modificare o eliminare un peering di rete virtuale.
services: virtual-network
documentationcenter: na
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
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Creare, modificare o eliminare un peering reti virtuali

Informazioni su come toocreate, modificare o eliminare un peering di rete virtuale. Consente di peering di rete virtuale è tooconnect due reti virtuali in hello stesso percorso di Azure tramite hello rete backbone di Azure. Una volta il peering, due reti virtuali hello vengono ancora gestite come risorse diverse. Le risorse in una rete virtuale di comunicano con hello stessa larghezza di banda e latenza come se fosse risorse hello in hello stessa rete virtuale. Se non si ha familiarità con la rete virtuale peering, si consiglia di leggere hello [Panoramica peer della rete virtuale](virtual-network-peering-overview.md) e completamento hello [creare un'esercitazione di peering reti virtuali](virtual-network-create-peering.md), prima del completamento attività Hello in questo articolo.

## <a name="before-you-begin"></a>Prima di iniziare

Completare hello seguenti attività prima di completare i passaggi descritti in qualsiasi sezione di questo articolo:

- Hello revisione [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn articolo sui limiti per il peering.
- Accedi toohello portale di Azure, Azure interfaccia della riga di comando (CLI) o Azure PowerShell con un account di Azure. Se non si ha un account Azure, registrarsi per ottenere un [account per la versione di prova gratuita](https://azure.microsoft.com/free).
- Se l'utilizzo di PowerShell comandi toocomplete attività in questo articolo, [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di hello più recente dei cmdlet di Azure PowerShell hello installato. Guida di tooget per i comandi di PowerShell, con esempi, digitare `get-help <command> -full`.
- Se tramite l'interfaccia della riga di comando (CLI) Azure comandi toocomplete attività in questo articolo, [installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di hello Azure CLI installato. Guida di tooget per i comandi CLI, digitare `az <command> --help`. Anziché installare hello CLI e relativi prerequisiti, è possibile usare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Hello Shell Cloud ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell **> _** pulsante nella parte superiore di hello di hello [portale](https://portal.azure.com). 

## <a name="create-a-peering"></a>Creare un peering

>[!NOTE]
>Esistono diversi requisiti, vincoli, e considerazioni toosuccessfully creare una rete virtuale peering. Prima di creare un peering, assicurarsi di avere familiarizzato con hello [requisiti e vincoli](#requirements-and-constraints) e [delle autorizzazioni necessarie](#permissions).
>

1. Accedi toohello [portale](https://portal.azure.com) con un account assegnato hello necessario [ruolo o autorizzazioni](#permissions).
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *reti virtuali*. Quando **le reti virtuali** viene visualizzato nei risultati della ricerca hello, selezionarlo. Non selezionare **le reti virtuali (classico)** se esso viene visualizzato nell'elenco di hello, non è possibile creare un peering da una rete virtuale venga distribuita tramite il modello di distribuzione classica hello.
3. In hello **le reti virtuali** pannello visualizzato, fare clic su desiderato toocreate un peer per la rete virtuale hello.
4. Nel riquadro di hello che viene visualizzato per la rete virtuale di hello è selezionata, fare clic su **peering** in hello **impostazioni** sezione.
5. Fare clic su **+ Aggiungi**. 
6. <a name="add-peering"></a>In hello **aggiungere peering** pannello, immettere o selezionare i valori per hello seguenti impostazioni:
    - **Nome:** hello nome per il peering hello deve essere univoco all'interno di rete virtuale hello.
    - **Il modello di distribuzione di rete virtuale:** selezionare quali hello di modello di distribuzione virtuale di rete da toopeer con è stata distribuita tramite.
    - **Conosce l'ID di risorsa:** se si dispone di accesso in lettura toohello rete virtuale da toopeer con, lasciare deselezionata questa casella di controllo. Se non si dispone di rete virtuale di accesso in lettura toohello o si desidera toopeer con sottoscrizione, questa casella di controllo. Immettere l'ID di risorsa completa hello della rete virtuale di hello da toopeer con in hello **ID risorsa** casella che si verificava quando è stata selezionata la casella hello. Immettere l'ID deve essere per una rete virtuale presente in risorse di Hello hello Azure stesso [percorso](https://azure.microsoft.com/regions) come questa rete virtuale. ID di risorsa completo Hello appare similetroppo/sottoscrizioni/<Id>/providers/Microsoft.Network/virtualNetworks//ResourceGroups / < resource-group-name > < virtual-network-name >. È possibile ottenere l'ID di risorsa hello per una rete virtuale visualizzando le proprietà di hello per una rete virtuale. proprietà hello tooview per una rete virtuale, vedere toolearn [gestire reti virtuali](virtual-network-manage-network.md#view-vnet).
    - **Sottoscrizione:** hello seleziona [sottoscrizione](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) della rete virtuale hello desiderato toopeer con. Il numero di sottoscrizioni che vengono elencate dipende dal numero di sottoscrizioni a cui l'account ha accesso in lettura. Se è stata selezionata hello **ID risorsa** casella di controllo, questa impostazione non è disponibile. È possibile eseguire il peering di reti virtuali in sottoscrizioni diverse purché entrambe le reti virtuali siano state create tramite Resource Manager. toopeer possibilità Hello per le sottoscrizioni create tramite diversi modelli di distribuzione è in versione di anteprima. Registrazione per l'anteprima di hello prima di creare un peering tra reti virtuali distribuite attraverso diversi modelli di distribuzione esistenti in diverse sottoscrizioni. Per ulteriori informazioni su tooregister per l'anteprima di hello e [peer reti virtuali create mediante modelli di distribuzione diversi in diverse sottoscrizioni](create-peering-different-deployment-models-subscriptions.md).
    - **Rete virtuale:** selezionare hello rete virtuale da toopeer con. È possibile selezionare una rete virtuale creata tramite un modello di distribuzione di Azure, ma la rete virtuale hello deve essere nella stessa posizione di rete virtuale di hello sta avvio hello peering da hello. È necessario disporre lettura rete virtuale toohello di accesso per tale toobe visibile nell'elenco di hello. Se è presente una rete virtuale, ma grigio, è possibile che lo spazio di indirizzo hello per la rete virtuale hello si sovrappone con spazio di indirizzi hello per questa rete virtuale. Se gli spazi indirizzi delle reti virtuali si sovrappongono, non è possibile eseguire il peering. Se è stata selezionata hello **ID risorsa** casella di controllo, questa impostazione non è disponibile.
    - **Consentire l'accesso di rete virtuale:** selezionare **abilitato** (impostazione predefinita), se si desidera che la comunicazione tra reti virtuali hello due tooenable. Consente la comunicazione tra reti virtuali, risorse connesse tooeither toocommunicate di rete virtuale con l'altro con hello stessa larghezza di banda e latenza, come se fossero connesso toohello stessa rete virtuale. Tutte le comunicazioni tra le risorse in due reti virtuali hello sono su hello Azure rete privata. Hello **VirtualNetwork** tag predefinito per i gruppi di sicurezza di rete comprende la rete virtuale hello e peering reti virtuali. altre informazioni sulle toolearn rete tag predefiniti gruppo di sicurezza, leggere hello [Panoramica di gruppi di sicurezza di rete](virtual-networks-nsg.md#default-tags) articolo.  Selezionare **disabilitato** se non si desidera toohello tooflow traffico peering reti virtuali. È possibile selezionare **disabilitato** se si è stato effettuato il peering una rete virtuale con un'altra rete virtuale, ma in alcuni casi si toodisable il flusso del traffico tra reti virtuali hello due. L'abilitazione/disabilitazione può risultare più pratica che eliminare e ricreare i peering. Quando questa impostazione è disabilitata, non il flusso del traffico tra hello peering reti virtuali.
    - **Consentire il traffico inoltrato:** controllare questo toohello di traffico inoltrato tooallow casella peering reti virtuali (il traffico non è stato originato nella rete virtuale di peering hello) rete virtuale di tooflow toothis. Inoltro del traffico è comune per la distribuzione di un dispositivo di rete virtuale nella rete virtuale di hello si sta peering con e create route definite dall'utente tooforward traffico tramite appliance di hello rete virtuale. Se si lascia questa casella non è selezionata (impostazione predefinita), il traffico inoltrato dalla rete virtuale di peering hello non può passare toothis di rete virtuale. Durante l'abilitazione di questa funzionalità consente il traffico di hello inoltrato tramite il peering hello, non creare le route definite dall'utente o dispositivi di rete virtuale. Le route definite dall'utente e le appliance virtuali di rete vengono create separatamente. Informazioni sulle [route definite dall'utente](virtual-networks-udr-overview.md).
    - **Consenti transito gateway:** questa casella di controllo se si dispone di una rete virtuale di rete virtuale gateway toothis collegato e si desidera tooallow traffico da hello peering tooflow di rete virtuale tramite il gateway hello. Ad esempio, la rete virtuale sia collegato tooan rete locale tramite un gateway di rete virtuale. Controllo di che questa casella consente il traffico dal hello peering tooflow di rete virtuale tramite rete virtuale di hello gateway toothis associata. Se si seleziona questa casella, rete virtuale di peering hello non può avere un gateway configurato. rete virtuale di peering Hello deve avere hello **Usa gateway remoto** casella di controllo selezionata quando l'impostazione hello peering da hello altra rete virtuale toothis di rete virtuale. Se si lascia questa casella non è selezionata (impostazione predefinita), il traffico di rete virtuale di peering hello ancora flussi di rete virtuale toothis, ma non può passare da una rete virtuale di rete virtuale gateway toothis associata. Altre informazioni sui [gateway di rete virtuale](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). 
    
    Non è possibile abilitare questa opzione se si esegue il peering di una rete virtuale (Resource Manager) con una rete virtuale (versione classica). Se il traffico hello passa tra due reti virtuali hello, hello (classico) traffico di rete virtuale non può passare da una rete di virtuale di rete gateway toohello collegato (gestione delle risorse).
    - **Usare i gateway remoti:** controllare il traffico tooallow casella da tooflow questa rete virtuale tramite una rete virtuale gateway toohello collegato rete virtuale con cui sta peering. Ad esempio, sta peering con la rete virtuale hello ha un gateway VPN associato che consente la comunicazione tooan della rete locale.  Selezionando questa casella consente il traffico dal tooflow rete virtuale tramite hello VPN gateway toohello collegato il peering reti virtuali. Se si seleziona questa casella, rete virtuale di peering hello deve disporre di un tooit collegato gateway di rete virtuale e hello **consentire transito gateway** casella di controllo selezionata. Se si lascia questa casella non è selezionata (impostazione predefinita), dalla rete virtuale di peering hello ancora traffico toothis virtuale di rete, ma non può passare da una rete virtuale di rete virtuale gateway toothis associata. 
    
    Non è possibile abilitare questa opzione se si esegue il peering di una rete virtuale (Resource Manager) con una rete virtuale (versione classica). Anche se il traffico hello passa tra due reti virtuali hello, traffico di rete virtuale (gestione delle risorse) hello non può passare da una rete gateway toohello collegato rete virtuale (classica).
7. Fare clic su hello **OK** pulsante tooadd hello subnet toohello rete virtuale selezionata.

### <a name="commands"></a>Comandi:

|Strumento|Comando|
|---|---|
|CLI|[az network vnet peering create](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>Scenari

Un peering di rete virtuale verrà creato tra reti virtuali create tramite hello stesso o diversi modelli di distribuzione esistenti in hello sottoscrizioni uguale o diverse. Completare un'esercitazione dettagliata per uno dei seguenti scenari hello:
 
|Modello di distribuzione di Azure  | Subscription  |
|---------|---------|
|Entrambi Resource Manager |[Uguale](virtual-network-create-peering.md)|
| |[Diversa](create-peering-different-subscriptions.md)|
|Uno di Resource Manager, uno della versione classica     |[Uguale](create-peering-different-deployment-models.md)|
| |[Diversa](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Visualizzare o modificare le impostazioni dei peering

1. Accedi toohello [portale](https://portal.azure.com) con un account assegnato hello necessario [ruolo o autorizzazioni](#permissions).
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *reti virtuali*. Quando **le reti virtuali** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **le reti virtuali** pannello visualizzato, fare clic su desiderato toocreate un peer per la rete virtuale hello.
4. Nel riquadro di hello che viene visualizzato per la rete virtuale di hello è selezionata, fare clic su **peering** in hello **impostazioni** sezione.
5. Fare clic su hello peering tooview desiderato oppure modificare le impostazioni per.
6. Modificare l'impostazione appropriata hello. Informazioni sulle opzioni di hello per ogni impostazione [passaggio 6](#add-peering) di hello creare una sezione di peering di questo articolo. 

    >[!NOTE]
    >Esistono diversi requisiti, vincoli, e considerazioni toosuccessfully creare una rete virtuale peering. Prima di creare un peering, assicurarsi di avere familiarizzato con hello [requisiti e vincoli](#requirements-and-constraints) e [delle autorizzazioni necessarie](#permissions).
    >

7. Fare clic su **Salva**.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[elenco di peering reti virtuali rete AZ](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist peering per una rete virtuale, [az Mostra peering reti virtuali di rete](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow impostazioni per il peering specifico, e [az aggiornamento peering reti virtuali di rete](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) impostazioni peer toochange.|
|PowerShell|[Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve consente di visualizzare le impostazioni peer e [Set AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange impostazioni.|

## <a name="delete-a-peering"></a>Eliminare un peering
Quando viene eliminato un peering, toohello peering rete virtuale non è più flussi di traffico da una rete virtuale. Quando sono peering reti virtuali distribuite tramite Gestione risorse, ogni rete virtuale ha un peer toohello altra rete virtuale. Se l'eliminazione di hello peering da una rete virtuale disabilita la comunicazione tra reti virtuali hello hello, non eliminare hello peering da hello altra rete virtuale. Hello stato peering per hello peering che esiste in hello altra rete virtuale è **Disconnected**. Non è possibile ricreare hello peering fino a quando non si ricreare hello peering nella rete virtuale prima di hello e lo stato di peering hello virtuale sia per le reti modifiche troppo*connesso*. 

Se si desidera toocommunicate reti virtuali, a volte, ma non sempre, anziché l'eliminazione di un peering, è possibile impostare hello **consentire l'accesso di rete virtuale** impostazione troppo**disabilitato** invece. toolearn, vedere passaggio 6 di hello [creare un peering](#create-peering) sezione di questo articolo. Disabilitare e abilitare l'accesso alla rete può risultare più facile che eliminare e ricreare i peering.

1. Accedi toohello [portale](https://portal.azure.com) con un account assegnato hello necessario [ruolo o autorizzazioni](#permissions).
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *reti virtuali*. Quando **le reti virtuali** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **le reti virtuali** pannello visualizzato, fare clic su rete virtuale di hello da toodelete un peering da.
4. Nel pannello hello che viene visualizzato per la rete virtuale di hello è selezionata, fare clic su **peering** in **impostazioni**.
5. Selezionare nell'elenco hello di peering che viene visualizzato nel Pannello di peering hello, hello rapida peering si desidera toodelete **eliminare**, quindi **Sì** hello toodelete peering dalla prima rete virtuale hello.
6. Hello completo precedenti passaggi toodelete hello peering da hello altra rete virtuale nel peering hello.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network vnet peering delete](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>Requisiti e vincoli 

- le reti virtuali Hello che peer è necessario disporre di spazi di indirizzi IP non sovrapposte.
- Non è possibile aggiungere o eliminare spazi di indirizzi in una rete virtuale dopo che ne è stato eseguito il peering con un'altra rete virtuale. tooadd o rimuovere spazi degli indirizzi, hello di eliminazione peering, aggiungere o rimuovere gli spazi degli indirizzi di hello, quindi ricreare il peering hello. spazi di indirizzi tooadd o rimuovere gli spazi degli indirizzi da reti virtuali, leggere hello [crea, modifica o Elimina le reti virtuali](virtual-network-manage-network.md#add-address-spaces) articolo. 
- È possibile notare due reti virtuali distribuite tramite Gestione risorse o una rete virtuale distribuito tramite Gestione risorse con una rete virtuale venga distribuita tramite il modello di distribuzione classica hello. Non è possibile esaminare due reti virtuali create tramite il modello di distribuzione classica hello. Se non si ha familiarità con i modelli di distribuzione di Azure, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo. È possibile utilizzare un [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect due reti virtuali create tramite il modello di distribuzione classica hello.
- Quando si peering due reti virtuali create a Resource Manager, un peering deve essere configurato per ogni rete virtuale nel peering hello. Quando si crea hello peering toohello seconda rete virtuale dalla rete virtuale prima di hello, lo stato di peering hello è *avviato*.  Quando si crea hello peering da hello rete virtuale secondo toohello prima rete virtuale, lo stato di peering è *connesso*. Se si visualizza lo stato di peering hello per la rete virtuale prima di hello, viene visualizzato lo stato modificato da *avviato* troppo*connesso*. peering Hello non è stata stabilita correttamente fino a quando lo stato di peering hello per entrambi peering di reti virtuali è *connesso*. 
- Quando peering una rete virtuale creata tramite Gestione risorse con una rete virtuale creata tramite il modello di distribuzione classica hello, configurare solo un peering per la rete virtuale di hello distribuita tramite Gestione risorse. È possibile configurare peering per una rete virtuale (classica) o tra due reti virtuali distribuite tramite il modello di distribuzione classica hello. Quando si crea hello peering dalla rete virtuale di toohello (Resource Manager) di rete virtuale hello (classico), lo stato di peering hello è *aggiornamento*, quindi subito modifiche troppo*connesso*.   
- Un peering viene stabilito tra due reti virtuali. I peering non sono transitivi. Se si creano peering tra:
    - VirtualNetwork1 e VirtualNetwork2
    - VirtualNetwork2 e VirtualNetwork3

  Non vengono stabiliti peering tra la VirtualNetwork1 e la VirtualNetwork3 tramite la VirtualNetwork2. Se si desidera che una rete virtuale peering tra VirtualNetwork1 e VirtualNetwork3 toocreate, è necessario toocreate un peering tra VirtualNetwork1 e VirtualNetwork3.
- Non è possibile risolvere i nomi nelle reti virtuali con peering usando la risoluzione dei nomi di Azure predefinita. i nomi tooresolve in altre reti virtuali, è necessario utilizzare un server DNS personalizzato. modalità di lettura tooset configurare il proprio server DNS, toolearn hello [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) articolo.
- Le risorse in entrambe le reti virtuali nel peering hello possono comunicare tra loro hello stessa larghezza di banda e latenza come se fossero hello stessa rete virtuale. Ogni dimensione di macchina virtuale presenta tuttavia una specifica larghezza di banda di rete massima. ulteriori informazioni sulla larghezza di banda di rete massima per le dimensioni di macchina virtuale diversa, leggere hello toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale.
- È possibile connettersi a reti virtuali, distribuite tramite Gestione risorse che sono in hello stesso, o diverse sottoscrizioni.
- È possibile connettersi a reti virtuali distribuite attraverso diversi modelli di distribuzione che sono in hello stesso, o diverse sottoscrizioni (anteprima). 
- Hello sottoscrizioni che sono entrambe le reti virtuali devono essere associato toohello stesso tenant di Azure Active Directory. Se non si ha già un tenant di AD, è possibile [crearne uno](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rapidamente. È possibile utilizzare un [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect due reti virtuali presenti in diverse sottoscrizioni associate toodifferent tenant di Active Directory.
- Una rete virtuale può essere il peering tooanother rete virtuale e il traffico di rete virtuale tooanother connessi con un gateway di rete virtuale di Azure. Quando le reti virtuali sono connessi tramite il peering e un gateway, il traffico tra reti virtuali hello convogliato tramite configurazione peering hello, anziché gateway hello.
- È previsto un importo minimo per il traffico in ingresso e in uscita che usa un peering di rete virtuale. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/virtual-network).


## <a name="permissions"></a>Autorizzazioni

Hello che è utilizzare una rete virtuale peering toocreate devono disporre hello necessarie ruolo o autorizzazioni. Ad esempio, se si sono stati peering due reti virtuali denominate myVnetA e myVnetB, all'account deve essere assegnato hello seguente ruolo minimo o autorizzazioni per ogni rete virtuale:
    
|Rete virtuale|Modello di distribuzione|Ruolo|Autorizzazioni|
|---|---|---|---|
|myVnetA|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnetB|Gestione risorse|[Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Classico|[Collaboratore reti virtuali classiche](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Altre informazioni, vedere [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e l'assegnazione di autorizzazioni specifiche troppo[ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Gestione risorse (solo).

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toocreate un [topologia di rete hub e spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 

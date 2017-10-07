---
title: aaaCreate, modificare o eliminare un indirizzo IP pubblico Azure | Documenti Microsoft
description: Informazioni su come toocreate, modificare o eliminare un indirizzo IP pubblico.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Creare, modificare o eliminare un indirizzo IP pubblico

Informazioni su un indirizzo IP pubblico di indirizzi e come toocreate, modificare ed eliminare uno. Un indirizzo IP pubblico è una risorsa con impostazioni proprie configurabili. Consente l'assegnazione di risorse di Azure un tooother di indirizzo IP pubblico:
- Tooresources connettività Internet in ingresso, ad esempio macchine virtuali (VM) di Azure, set di scalabilità di macchine virtuali di Azure, Gateway VPN di Azure, i gateway applicazione e bilanciamento del carico di Azure con connessione Internet. Risorse di Azure è possono ricevere comunicazioni in ingresso da hello Internet senza un indirizzo IP pubblico assegnato. Anche se alcune risorse di Azure sono intrinsecamente accessibile attraverso gli indirizzi IP pubblici, le altre risorse devono disporre di indirizzi IP pubblici assegnati toobe toothem accessibile da Internet hello.
- Connettività in uscita toohello Internet utilizzando un indirizzo IP prevedibile. Ad esempio, una macchina virtuale possono comunicare in uscita toohello Internet senza un tooit di indirizzo IP pubblico, ma il relativo indirizzo è l'indirizzo di rete convertita da indirizzo pubblico di Azure tooan imprevedibile. Assegnazione di una risorsa tooa di indirizzo IP pubblica consente tooknow quale indirizzo IP viene utilizzato per la connessione in uscita hello. Anche se è prevedibile, indirizzo hello può cambiare, a seconda della scelta metodo di assegnazione di hello. Per altre informazioni, vedere [Creare un indirizzo IP pubblico](#create-a-public-ip-address). altre informazioni sulle connessioni in uscita da risorse di Azure, leggere hello toolearn [comprendere le connessioni in uscita](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.

## <a name="before-you-begin"></a>Prima di iniziare

Completare hello seguenti attività prima di completare i passaggi in alcuna sezione di questo articolo:

- Hello revisione [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn articolo sui limiti per gli indirizzi IP pubblici.
- Accedi toohello Azure [portal](https://portal.azure.com), Azure interfaccia della riga di comando (CLI) o Azure PowerShell con un account di Azure. Se non si ha un account Azure, registrarsi per ottenere un [account per la versione di prova gratuita](https://azure.microsoft.com/free).
- Se l'utilizzo di PowerShell comandi toocomplete attività in questo articolo, [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di cmdlet di Azure PowerShell hello installato. Guida di tooget per i comandi di PowerShell, con esempi, digitare `get-help <command> -full`.
- Se tramite l'interfaccia della riga di comando (CLI) Azure comandi toocomplete attività in questo articolo, [installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di hello Azure CLI installato. Guida di tooget per i comandi CLI, digitare `az <command> --help`. Anziché installare hello CLI e relativi prerequisiti, è possibile usare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell **> _** pulsante nella parte superiore di hello di hello [portale](https://portal.azure.com).

Per gli indirizzi IP pubblici è previsto un addebito nominale. tooview hello sui prezzi, leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. 

## <a name="create-a-public-ip-address"></a>Creare un indirizzo IP pubblico

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *indirizzo ip pubblico*. Quando **gli indirizzi IP pubblici** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. Fare clic su **+ Aggiungi** in hello **indirizzo IP pubblico** pannello visualizzato.
4. Immettere o selezionare i valori delle seguenti impostazioni in hello hello **creare l'indirizzo IP pubblico** pannello visualizzato, quindi fare clic su **crea**:

    |Impostazione|Obbligatorio?|Dettagli|
    |---|---|---|
    |Nome|Sì|nome Hello deve essere univoco nel gruppo di risorse hello selezionate.|
    |Versione indirizzo IP|Sì| Selezionare IPv4 o IPv6. Mentre IPv4 pubblico, gli indirizzi possono essere assegnate tooseveral risorse di Azure, un indirizzo IP pubblico IPv6 può essere solo servizio di bilanciamento del carico tooan con connessione Internet. servizio di bilanciamento del carico Hello è possibile caricare bilanciamento IPv6 traffico tooAzure delle macchine virtuali. Altre informazioni, vedere [il bilanciamento del carico delle macchine di toovirtual traffico IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |Assegnazione indirizzi IP|Sì|**Dinamica:** gli indirizzi dinamici vengono assegnati solo dopo che è associato l'indirizzo IP pubblico hello tooa NIC associata tooa VM e hello macchina virtuale viene avviata per hello prima volta. Gli indirizzi dinamici è possono modificare se hello VM hello NIC associata toois arrestato (deallocato). Hello indirizzo rimane hello stesso se hello VM viene riavviato o arrestato (ma non deallocati). **Statico:** gli indirizzi statici vengono assegnati quando viene creato l'indirizzo IP pubblico hello. Gli indirizzi statici non non lo stato di modifica anche se hello VM viene inserito nella hello arrestato (deallocato). indirizzo Hello viene rilasciata solo quando viene eliminato hello NIC. È possibile modificare il metodo di assegnazione di hello dopo la creazione di hello NIC. Se si seleziona IPv6 per hello **versione IP**, metodo di assegnazione è disponibile solo hello è **dinamica**.|
    |Timeout di inattività (minuti)|No|Quanti minuti tookeep aprire una connessione TCP o HTTP senza basarsi su client toosend messaggi keep-alive. Se si seleziona IPv6 in **Versione indirizzo IP**, questo valore non può essere modificato. |
    |Etichetta del nome DNS|No|Deve essere univoco all'interno di hello località di Azure crei nome hello in (in tutte le sottoscrizioni e tutti i clienti). servizio DNS di Azure pubblico Hello registra automaticamente hello nome e indirizzo IP per la connessione con nome hello tooa risorse. Azure aggiunge *location.cloudapp.azure.com* (dove la posizione è posizione hello selezionata) nome toohello forniti hello toocreate completamente nome DNS completo. Se si sceglie toocreate entrambe le versioni di indirizzo, hello stesso nome DNS viene assegnato tooboth hello IPv4 e gli indirizzi IPv6. Hello servizio DNS di Azure contiene i record di nome sia IPv4 e IPv6 AAAA e risponde con entrambi i record quando il nome DNS hello viene cercato. client Hello sceglie quale toocommunicate indirizzo (IPv4 o IPv6) con.|
    |Crea un indirizzo IPv6 (o IPv4)|No| A seconda del valore selezionato in **Versione indirizzo IP**, viene visualizzato l'indirizzo IPv6 o IPv4. Se ad esempio si seleziona **IPv4** per **Versione indirizzo IP**, qui viene visualizzato **IPv6**.
    |Nome (visibile solo se è stata selezionata hello **creare un indirizzo IPv6 (o IPv4)** casella di controllo)|Sì, se si seleziona hello **creare IPv6** (o IPv4) la casella di controllo.|Hello nome deve essere diverso dal nome hello immettere per hello prima **nome** in questo elenco. Se si sceglie toocreate IPv4 sia un indirizzo IPv6, il portale di hello crea due separato pubbliche risorse indirizzo IP, una con ogni versione di indirizzo IP assegnato tooit.|
    |Assegnazione di indirizzi IP (visibile solo se è stata selezionata hello **creare un indirizzo IPv6 (o IPv4)** casella di controllo)|Sì, se si seleziona hello **creare IPv6** (o IPv4) la casella di controllo.|Se la casella di controllo di hello **creare un indirizzo IPv4**, è possibile selezionare un metodo di assegnazione. Se la casella di controllo di hello **creare un indirizzo IPv6**, non è possibile selezionare un metodo di assegnazione, come deve essere **dinamica**.|
    |Sottoscrizione|Sì|Deve essere presente in hello stesso [sottoscrizione](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) come risorsa hello desiderato tooassociate hello indirizzo IP pubblico da.|
    |Gruppo di risorse|Sì|Può esistere in hello uguale o diverso, [gruppo di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) come risorsa hello desiderato tooassociate hello indirizzo IP pubblico da.|
    |Percorso|Sì|Deve essere presente in hello stesso [percorso](https://azure.microsoft.com/regions), definita anche tooas area, come risorsa hello da tooassociate hello indirizzo IP pubblico da.|

**Comandi**

Se il portale di hello fornisce hello opzione toocreate due pubbliche risorse indirizzo IP (uno IPv4 e uno IPv6), hello seguenti comandi di PowerShell e CLI crea una risorsa con un indirizzo per una versione IP o hello altri. Se si desidera che i due pubbliche risorse indirizzo IP, una per ogni versione IP, è necessario eseguire il comando hello due volte, specificando nomi diversi e versioni per le risorse indirizzo IP pubbliche hello. 

|Strumento|Comando|
|---|---|
|CLI|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Visualizzare un indirizzo IP pubblico, modificarne le impostazioni o eliminarlo

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *indirizzo ip pubblico*. Quando **gli indirizzi IP pubblici** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **gli indirizzi IP pubblici** pannello visualizzato, fare clic sul nome hello di hello indirizzo IP pubblico desidera tooview, le impostazioni per modificare o eliminare.
4. Nel pannello hello che viene visualizzato per l'indirizzo IP pubblico hello, completare una delle seguenti opzioni a seconda che si voglia tooview, hello eliminare o modificare l'indirizzo IP pubblico hello.
    - **Visualizzazione**: hello **Panoramica** sezione del pannello hello Mostra impostazioni per l'indirizzo IP pubblico hello della chiave, ad esempio l'interfaccia di rete hello è associata troppo (se indirizzo hello è l'interfaccia di rete associato tooa). portale Hello non viene visualizzata la versione hello dell'indirizzo hello (IPv4 o IPv6). tooview hello informazioni sulla versione, hello utilizzare PowerShell o CLI comando tooview hello indirizzo IP pubblico. Se la versione dell'indirizzo IP hello è IPv6, hello assegnato indirizzo non viene visualizzata per portale hello, PowerShell o hello CLI. 
    - **Eliminare**: toodelete hello indirizzo IP pubblico, fare clic su **eliminare** in hello **Panoramica** sezione del pannello hello. Se l'indirizzo hello è attualmente associato tooan la configurazione IP, non può essere eliminata. Se l'indirizzo di hello è attualmente associato a una configurazione, fare clic su **annullare l'associazione** indirizzo hello toodissociate dalla configurazione IP hello.
    - **Modifica**: fare clic su **Configurazione**. Modificare le impostazioni utilizzando le informazioni di hello nel passaggio 4 di hello [creare un indirizzo IP pubblico](#create-a-public-ip-address) sezione di questo articolo. assegnazione di hello toochange per un indirizzo IPv4 statico toodynamic, è innanzitutto necessario dissociare indirizzo IPv4 pubblico hello dalla configurazione IP hello che è associata. È quindi possibile modificare hello assegnazione metodo toodynamic e fare clic su **associare** tooassociate hello IP indirizzo toohello stesso IP configurazione, una configurazione diversa o è possibile lasciare l'associazione è annullata. un indirizzo IP pubblico, in hello toodissociate **Panoramica** fare clic su **annullare l'associazione**.

>[!WARNING]
>Quando si modifica il metodo di assegnazione di hello da toodynamic statico, si perdono hello IP che è stato assegnato l'indirizzo IP pubblico toohello. Mentre hello Azure server DNS pubblici mantenere un mapping tra gli indirizzi statici o dinamici e qualsiasi etichetta del nome DNS (se è definito uno), è possibile modificare un indirizzo IP dinamico quando hello macchina virtuale viene avviato dopo in hello arrestato (deallocato). indirizzo hello tooprevent da modificare, assegnare un indirizzo IP statico.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[elenco di ip pubblico di rete AZ](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist gli indirizzi IP pubblici, [az rete public-ip-Mostra](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) impostazioni tooshow; [aggiornamento public-ip di rete az](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [az rete public-ip eliminare](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve un indirizzo IP pubblico fa riferimento a oggetto e visualizzare le relative impostazioni, [Set AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate impostazioni. [Remove AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Passaggi successivi
Assegnare indirizzi IP pubblici durante la creazione di hello seguendo le risorse di Azure:

- Macchine virtuali [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Servizio di bilanciamento del carico con connessione Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Gateway applicazione Azure](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Connessione da sito a sito con gateway VPN di Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)

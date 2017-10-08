---
title: gli indirizzi IP aaaConfigure per un'interfaccia di rete di Azure | Documenti Microsoft
description: Informazioni su come tooadd, modificare e rimuovere gli indirizzi IP privati e pubblici per un'interfaccia di rete.
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
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Aggiungere, modificare o rimuovere indirizzi IP per un'interfaccia di rete di Azure

Informazioni su come tooadd, modificare e rimuovere indirizzi IP pubblici e privati per un'interfaccia di rete. Gli indirizzi IP privati assegnati l'interfaccia di rete tooa abilitare toocommunicate una macchina virtuale con altre risorse in una rete virtuale di Azure e delle reti connesse. Un indirizzo IP privato consente inoltre le comunicazioni in uscita toohello Internet utilizzando un indirizzo IP prevedibile. Oggetto [indirizzo IP pubblico](virtual-network-public-ip-address.md) assegnato tooa interfaccia di rete consente le comunicazioni in ingresso tooa macchina virtuale hello Internet. indirizzo Hello consente inoltre le comunicazioni in uscita dalla macchina virtuale di hello toohello Internet utilizzando un indirizzo IP prevedibile. Per maggiori informazioni, vedere [Informazioni sulle connessioni in uscita in Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Se è necessario toocreate, modificare o eliminare un'interfaccia di rete, leggere hello [gestire un'interfaccia di rete](virtual-network-network-interface.md) articolo. Se è necessario interfacce di rete tooadd tooor remove di interfacce di rete da una macchina virtuale, leggere hello [aggiungere o rimuovere le interfacce di rete](virtual-network-network-interface-vm.md) articolo. 


## <a name="before-you-begin"></a>Prima di iniziare

Completare hello seguenti attività prima di completare i passaggi in alcuna sezione di questo articolo:

- Hello revisione [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn articolo sui limiti per gli indirizzi IP pubblici e privati.
- Accedi toohello Azure [portal](https://portal.azure.com), Azure interfaccia della riga di comando (CLI) o Azure PowerShell con un account di Azure. Se non si ha un account Azure, registrarsi per ottenere un [account per la versione di prova gratuita](https://azure.microsoft.com/free).
- Se l'utilizzo di PowerShell comandi toocomplete attività in questo articolo, [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di cmdlet di Azure PowerShell hello installato. Guida di tooget per i comandi di PowerShell, con esempi, digitare `get-help <command> -full`.
- Se tramite l'interfaccia della riga di comando (CLI) Azure comandi toocomplete attività in questo articolo, [installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di hello Azure CLI installato. Guida di tooget per i comandi CLI, digitare `az <command> --help`. Anziché installare hello CLI e relativi prerequisiti, è possibile usare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell **> _** pulsante nella parte superiore di hello di hello [portale](https://portal.azure.com).

## <a name="add-ip-addresses"></a>Aggiungere indirizzi IP

È possibile aggiungere il numero [privata](#private) e [pubblica](#public) [IPv4](#ipv4) indirizzi come interfaccia di rete necessarie tooa, entro i limiti di hello elencati nella hello [i limiti di Azure ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) articolo. Non è possibile utilizzare hello portale tooadd un'interfaccia di rete esistente IPv6 indirizzo tooan (sebbene sia possibile utilizzare hello portale tooadd un'interfaccia di rete tooa di indirizzo IPv6 privata quando si crea l'interfaccia di rete hello). È possibile utilizzare PowerShell o hello CLI tooadd un IPv6 privata indirizzo tooone [configurazione IP secondaria](#secondary) (fino a quando non sono presenti configurazioni di IP secondarie esistente) per una rete esistente che non è collegata interfaccia tooa virtuale macchina. Non è possibile utilizzare qualsiasi tooadd strumento un'interfaccia di rete tooa di indirizzo IPv6 pubblica. Vedere [IPv6](#ipv6) per informazioni dettagliate sull'uso di indirizzi IPv6. 

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su desiderato tooadd IPv4 indirizzo per l'interfaccia di rete hello.
4. Fare clic su **le configurazioni IP** in hello **impostazioni** sezione del pannello hello per interfaccia di rete hello selezionato.
5. Fare clic su **+ Aggiungi** nel pannello hello che viene aperta per le configurazioni IP.
6. Specificare hello segue, quindi fare clic su **OK** tooclose hello **configurazione IP aggiungere** pannello:

    |Impostazione|Obbligatorio?|Dettagli|
    |---|---|---|
    |Nome|Sì|Deve essere univoco per l'interfaccia di rete hello|
    |Tipo|Sì|Poiché si sta aggiungendo un'interfaccia di rete esistente IP configurazione tooan e ogni interfaccia di rete deve essere un [primario](#primary) è l'unica opzione di configurazione IP, **secondario**.|
    |Metodo di assegnazione di indirizzi IP privati|Sì|[**Dinamica** ](#dynamic) gli indirizzi possono cambiare macchina virtuale hello viene riavviato dopo già hello arrestato (deallocato). Azure assegna un indirizzo disponibile dallo spazio di indirizzi hello hello subnet hello dell'interfaccia di rete è connesso a. [**Statico** ](#static) indirizzi non vengono rilasciati fino a quando non viene eliminato l'interfaccia di rete hello. Specificare un indirizzo IP da hello subnet spazio intervallo di indirizzi non è attualmente in uso da un'altra configurazione IP.|
    |Indirizzo IP pubblico|No|**Disabilitata:** alcuna risorsa di indirizzo IP pubblica non è la configurazione IP toohello attualmente associato. **Abilitato:** selezionare un indirizzo IPv4 pubblico esistente o crearne uno nuovo. modalità di lettura di un indirizzo IP pubblico, toocreate toolearn hello [gli indirizzi IP pubblici](virtual-network-public-ip-address.md#create-a-public-ip-address) articolo.|
7. Aggiungere manualmente secondario private IP indirizzi toohello macchina virtuale sistema operativo completando istruzioni hello hello [assegnare più indirizzi IP di sistemi operativi di computer toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config) articolo. Vedere [privata](#private) gli indirizzi IP per le considerazioni speciali prima aggiunta manuale di sistema operativo della macchina virtuale tooa gli indirizzi IP. Non aggiungere qualsiasi pubblica IP indirizzi toohello virtuale sistema operativo della macchina.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic ip-config create](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>Modificare le impostazioni degli indirizzi IP

Metodo di assegnazione hello toochange di un indirizzo IPv4, modifica hello indirizzo IPv4 statico, potrebbe essere necessario o indirizzo IP pubblico di modifica hello assegnato tooa interfaccia di rete. Se si desidera modificare l'indirizzo IPv4 privato hello di una configurazione IP secondaria associata a un'interfaccia di rete secondaria in una macchina virtuale (altre informazioni, vedere [interfacce di rete primarie e secondarie](virtual-network-network-interface-vm.md#about)), sul posto hello virtuale macchina in hello arrestato (deallocato) prima del completamento hello alla procedura seguente: 

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su interfaccia di rete hello tooview desiderato oppure modificare le impostazioni dell'indirizzo IP per.
4. Fare clic su **le configurazioni IP** in hello **impostazioni** sezione del pannello hello per interfaccia di rete hello selezionato.
5. Fare clic su configurazione IP hello desiderato toomodify dall'elenco di hello nel pannello hello che viene aperta per le configurazioni IP.
6. Modificare le impostazioni hello, in base alle esigenze, utilizzando le informazioni di hello sulle impostazioni di hello nel passaggio 6 di hello [aggiungere una configurazione IP](#create-ip-config) sezione di questo articolo. Fare clic su **salvare** pannello hello tooclose per la configurazione IP hello è stato modificato.

>[!NOTE]
>Se l'interfaccia di rete primaria hello dispone di più configurazioni IP e si modifica l'indirizzo IP privato hello della configurazione IP primaria hello, è necessario riassegnarlo manualmente hello primario e secondario IP indirizzi toohello interfaccia di rete all'interno di Windows (non obbligatorio per Linux). interfaccia di rete tooa gli indirizzi IP all'interno di un sistema operativo, di assegnare toomanually leggere hello [assegnare più indirizzi IP macchine toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config) articolo. Vedere [privata](#private) gli indirizzi IP per le considerazioni speciali prima aggiunta manuale di sistema operativo della macchina virtuale tooa gli indirizzi IP. Non aggiungere qualsiasi pubblica IP indirizzi toohello virtuale sistema operativo della macchina.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>Rimuovere indirizzi IP

È possibile rimuovere [privata](#private) e [pubblica](#public) indirizzi IP di un'interfaccia di rete, ma un'interfaccia di rete deve sempre avere almeno un tooit di indirizzo IPv4 privato.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su interfaccia di rete hello desiderato tooremove gli indirizzi IP.
4. Fare clic su **le configurazioni IP** in hello **impostazioni** sezione del pannello hello per interfaccia di rete hello selezionato.
5. Fare doppio clic su un [secondario](#secondary) configurazione IP (non è possibile eliminare hello [primario](#primary) configurazione) toodelete desiderati, fare clic su **eliminare**, quindi fare clic su **Sì**  eliminazione hello tooconfirm. Se la configurazione di hello contiene una risorsa di indirizzo IP pubblica associato tooit, risorse hello sono dissociata dalla configurazione IP hello, ma hello risorsa non viene eliminata.
6. Chiude hello **le configurazioni IP** blade.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic ip-config delete](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>Configurazioni IP

[Privato](#private) e (facoltativamente) [pubblica](#public) gli indirizzi IP vengono assegnati tooone o più configurazioni IP assegnato tooa interfaccia di rete. Esistono due tipi di configurazioni IP:

### <a name="primary"></a>Primario

Ogni interfaccia di rete viene assegnata a una configurazione IP primaria. Una configurazione IP primaria:

- È un [privata](#private) [IPv4](#ipv4) tooit indirizzo assegnato. Non è possibile assegnare una privata [IPv6](#ipv6) configurazione IP primaria di indirizzo tooa.
- Può inoltre essere un [pubblica](#public) tooit indirizzo IPv4. È possibile assegnare a una pubblico tooa primaria o secondaria IP configurazione di indirizzi IPv6. È tuttavia possibile assegnare a un pubblico IPv6 indirizzo tooan del bilanciamento del carico di Azure, che consente di caricare bilanciare l'indirizzo IPv6 privato traffico tooa virtuale della macchina. Per altre informazioni, vedere [Dettagli e le limitazioni per IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>Secondario

Configurazione IP primaria tooa, un'interfaccia di rete può inoltre disporre di zero o più configurazioni IP secondarie tooit assegnate. Una configurazione IP secondaria:

- Deve avere una privata tooit di indirizzo IPv4 o IPv6. Se hello indirizzo IPv6, l'interfaccia di rete hello può avere solo una configurazione IP secondaria. Se hello indirizzo IPv4, l'interfaccia di rete hello potrebbe essere più configurazioni IP secondarie tooit assegnate. toolearn ulteriori informazioni su quanti gli indirizzi IPv4 pubblici e privati possono essere assegnati tooa l'interfaccia di rete, vedere hello [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) articolo.  
- Potrebbe anche essere un tooit di indirizzo IPv4 pubblico, se l'indirizzo IP privato hello è IPv4. Se l'indirizzo IP privato hello IPv6, è possibile assegnare a un pubblico IPv4 o IPv6 toohello IP configurazione degli indirizzi. L'assegnazione di più interfaccia di rete tooa di indirizzi IP è, ad esempio utile in scenari:
    - Ospitare più siti Web o servizi con indirizzi IP e certificati SSL diversi in un singolo server.
    - Una macchina virtuale che funge da appliance virtuale di rete, ad esempio un firewall o un servizio di bilanciamento del carico.
    - Hello uno qualsiasi di indirizzi IPv4 privati per uno dei pool di back-end di bilanciamento del carico di Azure tooan interfacce di rete hello hello tooadd possibilità. In hello precedente, solo hello IPv4 indirizzo primario per l'interfaccia di rete primaria hello è possibile aggiungere pool back-end tooa. toolearn ulteriori informazioni su come tooload bilanciare più configurazioni di IPv4, vedere hello [il bilanciamento del carico di più configurazioni IP](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo. 
    - tooload possibilità Hello bilanciare un'interfaccia di rete assegnate tooa di indirizzo IPv6. toolearn ulteriori informazioni su come tooload bilanciare tooa indirizzo privato di IPv6, vedere hello [indirizzi IPv6 di bilanciare il carico](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.


## <a name="address-types"></a>Tipi di indirizzi

È possibile assegnare i seguenti tipi di tooan gli indirizzi IP hello [configurazione IP](#ip-configurations):

### <a name="private"></a>Privato

Privato [IPv4](#ipv4) indirizzi abilitare toocommunicate una macchina virtuale con le altre risorse in una rete virtuale o altre reti connesse. Una macchina virtuale non può essere comunicata in ingresso, né grado di comunicare in uscita con una privata macchina virtuale hello [IPv6](#ipv6) indirizzo, con un'eccezione. Una macchina virtuale possono comunicare con bilanciamento del carico di Azure hello utilizzando un indirizzo IPv6. Per altre informazioni, vedere [Dettagli e le limitazioni per IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

Per impostazione predefinita, i server DHCP di Azure hello assegnano l'indirizzo IPv4 privato hello per hello [configurazione IP primaria](#primary) di hello rete interfaccia toohello interfaccia di rete all'interno del sistema operativo di hello macchina virtuale. A meno che non necessario, si debba mai manualmente impostare hello indirizzo IP di un'interfaccia di rete all'interno del sistema operativo della macchina virtuale hello. 

> [!WARNING]
> Se l'indirizzo IPv4 hello impostato come indirizzo IP primario hello un'interfaccia di rete all'interno del sistema operativo della macchina virtuale è sempre diverso indirizzo IPv4 privato hello assegnato configurazione IP primaria toohello hello principale dell'interfaccia di rete associata tooa macchina virtuale in Azure, si perde la connettività toohello virtual machine.

Esistono scenari in cui è necessario toomanually impostare l'indirizzo IP hello un'interfaccia di rete all'interno del sistema operativo della macchina virtuale hello. Ad esempio, è necessario impostare manualmente hello primari e secondari indirizzi di un sistema operativo Windows, quando si aggiungono più tooan di indirizzi IP macchina virtuale di Azure. Per una macchina virtuale Linux, potrebbe essere toomanually set hello secondario gli indirizzi IP. Vedere [aggiungere indirizzi del sistema operativo VM tooa](virtual-network-multiple-ip-addresses-portal.md#os-config) per informazioni dettagliate. Quando si imposta manualmente l'indirizzo IP hello all'interno del sistema operativo hello, è consigliabile assegnare sempre hello indirizzi toohello la configurazione IP per un'interfaccia di rete utilizzando il metodo di assegnazione statica (anziché dinamico) hello. Assegnazione indirizzo hello tramite il metodo statico hello assicura che l'indirizzo hello non cambia in Azure. Se avrai bisogno di indirizzo hello toochange assegnato tooan la configurazione IP, è consigliabile è:

1. macchina virtuale di hello tooensure riceve un indirizzo dal server DHCP di Azure hello, modificare l'assegnazione di hello tooDHCP back-indirizzo IP all'interno del sistema operativo hello e la macchina virtuale di riavvio hello hello.
2. Arresta (dealloca) macchina virtuale hello.
3. Modificare l'indirizzo IP hello per la configurazione IP hello in Azure.
4. Avviare la macchina virtuale hello.
5. [Configurare manualmente](virtual-network-multiple-ip-addresses-portal.md#os-config) hello secondario IP indirizzi all'interno del sistema operativo hello (nonché l'indirizzo IP primario hello all'interno di Windows) toomatch è impostato in Azure.
 
Seguendo i passaggi precedenti hello, hello private IP indirizzo assegnato toohello interfaccia di rete all'interno di Azure e all'interno del sistema operativo della macchina virtuale, rimangono hello stesso. traccia tookeep dei quali macchine virtuali all'interno di sottoscrizione che viene impostato manualmente gli indirizzi IP all'interno di un sistema operativo, considerare l'aggiunta di Azure [tag](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello le macchine virtuali. È possibile usare ad esempio "Assegnazione indirizzi IP: statica". In questo modo, è possibile trovare facilmente le macchine virtuali hello nella sottoscrizione che impostare hello indirizzo IP all'interno del sistema operativo hello manualmente.

Tooenabling toocommunicate una macchina virtuale con altre risorse all'interno di hello stesso o connesse reti virtuali, un indirizzo IP privato indirizzo anche consente inoltre di una macchina virtuale toocommunicate in uscita toohello Internet. Le connessioni in uscita vengono convertita dall'indirizzo IP pubblico imprevisto di Azure tooan indirizzo di rete di origine. informazioni su Azure connettività Internet in uscita, leggere hello toolearn [Azure connettività Internet in uscita](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo. Indirizzo IP privato della macchina virtuale in ingresso tooa da hello Internet non è possibile comunicare.

### <a name="public"></a>Pubblico

Gli indirizzi IP pubblici abilitare la connettività in ingresso tooa macchina virtuale hello Internet. Le connessioni in uscita toohello Internet di utilizzare un indirizzo IP prevedibile. Per maggiori informazioni, vedere [Informazioni sulle connessioni in uscita in Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). È possibile assegnare una configurazione IP tooan degli indirizzi IP pubblica, ma non è necessario. Se non si assegna una macchina virtuale tooa di indirizzo IP pubblica, può comunque comunicare in uscita toohello Internet tramite il relativo indirizzo IP privato. informazioni su indirizzi IP pubblici, leggere hello toolearn [indirizzo IP pubblico](virtual-network-public-ip-address.md) articolo.

Esistono limiti toohello privato e gli indirizzi IP pubblici che è possibile assegnare tooa interfaccia di rete. Per informazioni dettagliate, leggere hello [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) articolo.

> [!NOTE]
> Azure converte privata tooa pubblica indirizzo IP una macchina virtuale. Di conseguenza, non è a conoscenza di eventuali indirizzi IP pubblici assegnati tooit hello del sistema operativo, pertanto non c'è alcuna necessità tooever manualmente, assegnare un indirizzo IP pubblico nel sistema operativo hello.

## <a name="assignment-methods"></a>Metodi di assegnazione

Vengono assegnati indirizzi IP pubblici e privati con hello dei seguenti metodi di assegnazione:

### <a name="dynamic"></a>Dinamico

Gli indirizzi IPv4 e (facoltativamente) IPv6 privati dinamici vengono assegnati per impostazione predefinita. Gli indirizzi dinamici è possono modificare se macchina virtuale hello viene inserito hello arrestato (deallocato), quindi avviato. Se non si desidera toochange indirizzi IPv4 per la durata hello della macchina virtuale hello, assegnare gli indirizzi di hello tramite hello di metodo statico. È possibile assegnare solo un indirizzo IPv6 privato utilizzando il metodo di assegnazione dinamica hello. È possibile assegnare a una pubblico tooan IP configurazione di indirizzi IPv6 usando dei metodi.

### <a name="static"></a>statico

Non modificano gli indirizzi assegnati tramite il metodo statico di hello fino a quando non viene eliminata una macchina virtuale. Assegnare manualmente una privato configurazione indirizzo IPv4 statico tooan IP dallo spazio di indirizzi hello per interfaccia di rete hello hello subnet è in. (Facoltativamente), è possibile assegnare una pubblica o privata configurazione indirizzo IPv4 statico tooan IP. È possibile assegnare a una pubblica o privata IPv6 indirizzo tooan configurazione con IP statico. toolearn ulteriori informazioni su come Azure assegna indirizzi IPv4 pubblici statici, vedere hello [indirizzo IP pubblico](virtual-network-public-ip-address.md) articolo.

## <a name="ip-address-versions"></a>Versioni di indirizzi IP

È possibile specificare hello l'assegnazione di indirizzi seguenti versioni:

### <a name="ipv4"></a>IPv4

Ogni interfaccia di rete deve avere una configurazione IP [primaria](#primary) a cui è assegnato un indirizzo [IPv4](#ipv4) [privato](#private). È possibile aggiungere una o più configurazioni IP [secondarie](#secondary) che dispongono di un indirizzo IPv4 privato e (facoltativamente) un indirizzo IPv4 [pubblico](#public).

### <a name="ipv6"></a>IPv6

È possibile assegnare zero o uno privato [IPv6](#ipv6) indirizzo tooone configurazione IP secondaria di un'interfaccia di rete. interfaccia di rete di Hello non può avere qualsiasi configurazione IP secondarie esistente. È possibile aggiungere una configurazione IP con un indirizzo IPv6 tramite il portale di hello. Usare PowerShell o hello CLI tooadd una configurazione IP con una IPv6 indirizzo tooan esistente rete interfaccia privata. interfaccia di rete Hello non può essere collegato tooan macchina virtuale esistente.

> [!NOTE]
> Se è possibile creare un'interfaccia di rete con un indirizzo IPv6 tramite il portale di hello, è possibile aggiungere una rete interfaccia tooa nuovo o esistente macchina virtuale esistente, tramite il portale di hello. Utilizzare PowerShell o hello Azure CLI 2.0 toocreate un'interfaccia di rete con un indirizzo IPv6 privato, quindi collegare l'interfaccia di rete hello durante la creazione di una macchina virtuale. È possibile collegare un'interfaccia di rete con un indirizzo IPv6 privato assegnato macchina virtuale esistente di tooit tooan. È possibile aggiungere una privata configurazione IP tooan di indirizzo IPv6 per qualsiasi macchina virtuale di rete dell'interfaccia associata tooa utilizzano strumenti (portale, CLI o PowerShell).

È possibile assegnare a una pubblico tooa primaria o secondaria IP configurazione di indirizzi IPv6.

## <a name="next-steps"></a>Passaggi successivi
toocreate una macchina virtuale con diverse configurazioni IP, leggere hello seguenti articoli:

|Attività|Strumento|
|---|---|
|Creare una macchina virtuale con più NIC|[Interfaccia della riga di comando](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Creare una macchina virtuale con una singola scheda di interfaccia di rete e più indirizzi IPv4|[Interfaccia della riga di comando](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Creare una macchina virtuale con una singola scheda di interfaccia di rete con un indirizzo IPv6 privato (dietro un Azure Load Balancer)|[Interfaccia della riga di comando](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Modello di Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|

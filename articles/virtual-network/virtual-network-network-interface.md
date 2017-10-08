---
title: aaaCreate, modificare o eliminare un'interfaccia di rete di Azure | Documenti Microsoft
description: "Informazioni su cosa è un'interfaccia di rete e come modificare le impostazioni per toocreate ed eliminare uno."
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
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Creare, modificare o eliminare un'interfaccia di rete

Informazioni su come modificare le impostazioni per toocreate ed eliminare un'interfaccia di rete. Un'interfaccia di rete consente toocommunicate una macchina virtuale di Azure con Internet, Azure e alle risorse locali. Quando si crea una macchina virtuale tramite il portale di Azure hello, portale hello crea un'interfaccia di rete con le impostazioni predefinite per l'utente. È possibile invece scegliere toocreate interfacce di rete con impostazioni personalizzate e aggiungere uno o più rete interfacce tooa macchina virtuale durante la creazione. È inoltre possibile impostazioni interfaccia di rete toochange predefinite per un'interfaccia di rete esistente. Questo articolo spiega come toocreate un'interfaccia di rete con impostazioni personalizzate, modificare le impostazioni esistenti, ad esempio l'assegnazione di rete filtro (gruppo di sicurezza di rete), assegnazione subnet, le impostazioni del server DNS e l'inoltro IP e l'eliminazione di un'interfaccia di rete.

Se è necessario tooadd, modificare o rimuovere gli indirizzi IP per un'interfaccia di rete, leggere hello [gli indirizzi IP gestire](virtual-network-network-interface-addresses.md) articolo. Se è necessario interfacce di rete tooadd o rimuovere le interfacce di rete da macchine virtuali, leggere hello [aggiungere o rimuovere le interfacce di rete](virtual-network-network-interface-vm.md) articolo.


## <a name="before-you-begin"></a>Prima di iniziare

Completare hello seguenti attività prima di completare i passaggi in alcuna sezione di questo articolo:

- Hello revisione [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn articolo sui limiti per le interfacce di rete.
- Accedi toohello Azure [portal](https://portal.azure.com), Azure interfaccia della riga di comando (CLI) o Azure PowerShell con un account di Azure. Se non si ha un account Azure, registrarsi per ottenere un [account per la versione di prova gratuita](https://azure.microsoft.com/free).
- Se l'utilizzo di PowerShell comandi toocomplete attività in questo articolo, [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di cmdlet di Azure PowerShell hello installato. Guida di tooget per i comandi di PowerShell, con esempi, digitare `get-help <command> -full`.
- Se tramite l'interfaccia della riga di comando (CLI) Azure comandi toocomplete attività in questo articolo, [installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di hello Azure CLI installato. Guida di tooget per i comandi CLI, digitare `az <command> --help`. Anziché installare hello CLI e relativi prerequisiti, è possibile usare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell **> _** pulsante nella parte superiore di hello di hello [portale](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Creare un'interfaccia di rete

Quando si crea una macchina virtuale tramite il portale di Azure hello, portale hello crea un'interfaccia di rete con le impostazioni predefinite per l'utente. Se si preferisce specificare tutte le impostazioni di interfaccia di rete, è possibile creare un'interfaccia di rete con impostazioni personalizzate e collegare la macchina virtuale hello rete interfaccia tooa quando si crea una macchina virtuale hello (tramite PowerShell o hello CLI di Azure). È anche possibile creare un'interfaccia di rete e aggiungerlo come macchina virtuale esistente tooan (tramite PowerShell o hello CLI di Azure). toolearn come interfaccia di rete tooadd per toocreate una macchina virtuale con un oggetto esistente o rimuovere le interfacce di rete da macchine virtuali esistenti, leggere hello [aggiungere o rimuovere le interfacce di rete](virtual-network-network-interface-vm.md) articolo. Prima di creare un'interfaccia di rete, è necessario disporre di un oggetto esistente [rete virtuale](virtual-networks-create-vnet-arm-pportal.md) in hello stessa posizione e sottoscrizione si crea un'interfaccia di rete in.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su **+ Aggiungi**.
4. In hello **interfaccia di rete crea** blade che verrà visualizzata, immettere o selezionare i valori per hello seguenti impostazioni, quindi fare clic su **crea**:

    |Impostazione|Obbligatorio?|Dettagli|
    |---|---|---|
    |Nome|Sì|nome Hello deve essere univoco nel gruppo di risorse hello selezionate. Nel corso del tempo, probabilmente si accumuleranno più interfacce di rete nella sottoscrizione di Azure. Hello lettura [convenzioni di denominazione](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) articolo per più semplice di interfacce di rete di suggerimenti durante la creazione di un toomake convenzione di denominazione gestione diversi. Hello nome non può essere modificato dopo la creazione di interfaccia di rete hello.|
    |Rete virtuale|Sì|Selezionare hello rete virtuale per l'interfaccia di rete hello. È possibile assegnare solo una rete interfaccia tooa rete virtuale presente in hello stessa sottoscrizione e il percorso come interfaccia di rete hello. Dopo la creazione di un'interfaccia di rete, non è possibile modificare una rete virtuale di hello a che viene assegnato. Hello macchine virtuali aggiunte toomust di interfaccia di rete hello inoltre esistere hello stesso percorso e sottoscrizione come interfaccia di rete hello.|
    |Subnet|Sì|Selezionare una subnet all'interno di rete virtuale di hello selezionato. È possibile modificare la subnet hello interfaccia di rete hello viene assegnato tooafter viene creato.|
    |Assegnazione di indirizzi IP privati|Sì| In questa impostazione, si è scelto il metodo di assegnazione hello per hello indirizzo IPv4. Scegliere tra hello dei seguenti metodi di assegnazione: **dinamica:** quando si seleziona questa opzione, Azure assegna automaticamente un indirizzo disponibile dallo spazio di indirizzi hello della subnet hello selezionato. Azure può assegnare un'interfaccia di rete tooa indirizzo diverso quando macchina virtuale hello in viene avviato dopo già hello arrestato (deallocato). Hello indirizzo rimane hello uguali se il riavvio della macchina virtuale hello senza già hello arrestato (deallocato). **Statico:** quando si seleziona questa opzione, è necessario assegnare manualmente un indirizzo IP disponibile nello spazio di indirizzi hello della subnet hello è stata selezionata. Gli indirizzi statici non vengono modificano fino a quando non vengono modificati o l'interfaccia di rete hello viene eliminato. È possibile modificare il metodo di assegnazione di hello dopo la creazione di interfaccia di rete hello. server DHCP di Azure Hello assegna questa interfaccia di rete toohello indirizzo all'interno del sistema operativo hello della macchina virtuale hello.|
    |Gruppo di sicurezza di rete|No| Lasciare impostato troppo**Nessuno**, selezionare un oggetto esistente [il gruppo di sicurezza di rete](virtual-networks-nsg.md), o [creare un gruppo di sicurezza di rete](virtual-networks-create-nsg-arm-pportal.md). Gruppi di sicurezza di rete consentono il traffico di rete toofilter da e verso un'interfaccia di rete. È possibile applicare zero o una rete sicurezza gruppo tooa interfaccia di rete. Zero o un gruppo di sicurezza di rete può essere applicata anche l'interfaccia di rete hello toohello subnet viene assegnato a. Quando un gruppo di sicurezza di rete è tooa applicata l'interfaccia di rete e l'interfaccia di rete hello subnet hello è assegnato, che si verifichino risultati imprevisti a volte. i gruppi di sicurezza di rete tootroubleshoot toonetwork applicato interfacce e le subnet, leggere hello [risolvere i problemi relativi a gruppi di sicurezza di rete](virtual-network-nsg-troubleshoot-portal.md#nsg) articolo.|
    |Sottoscrizione|Sì|Selezionare una delle [sottoscrizioni](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) di Azure. macchina virtuale Hello si collega una rete interfaccia tooand hello rete virtuale connetterlo toomust esiste in hello stessa sottoscrizione.|
    |Indirizzo IP privato (IPv6)|No| Se si seleziona questa casella di controllo, un indirizzo IPv6 è l'interfaccia di rete toohello assegnato, inoltre toohello indirizzo IPv4 assegnato toohello interfaccia di rete. Vedere hello [IPv6](#IPv6) sezione di questo articolo per informazioni importanti sull'utilizzo di IPv6 con interfacce di rete. È possibile selezionare un metodo di assegnazione per hello indirizzo IPv6. Se si sceglie tooassign un indirizzo IPv6, viene assegnato con metodo dinamico hello.
    |Nome IPv6 (viene visualizzato solo quando hello **indirizzo IP privato (IPv6)** casella di controllo è selezionata) |Sì, se hello **indirizzo IP privato (IPv6)** casella di controllo è selezionata.| Configurazione IP secondaria tooa per interfaccia di rete hello viene assegnato questo nome. Ulteriori informazioni sulle configurazioni IP in hello [consente di visualizzare le impostazioni dell'interfaccia di rete](#view-network-interface-settings) sezione di questo articolo.|
    |Gruppo di risorse|Sì|Selezionare un [gruppo di risorse](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) esistente o crearne uno. Un'interfaccia di rete possono essere presenti in hello stesso o una rete virtuale hello o gruppo di risorse diverso rispetto a macchina virtuale hello viene collegato, la connessione.|
    |Percorso|Sì|macchina virtuale Hello si collega una rete interfaccia tooand hello rete virtuale connetterlo toomust esiste in hello stesso [percorso](https://azure.microsoft.com/regions), definita anche tooas un'area.|

portale Hello hello opzione tooassign non fornisce un'interfaccia di rete toohello di indirizzo IP pubblica quando si crea, anche se il portale di hello creare un indirizzo IP pubblico e assegnarvi tooa interfaccia di rete quando si crea una macchina virtuale utilizzando portale hello. toolearn come tooadd una rete pubblica toohello dell'indirizzo IP dell'interfaccia dopo la creazione, lettura hello [gli indirizzi IP gestire](virtual-network-network-interface-addresses.md) articolo. Se si desidera toocreate un'interfaccia di rete con un indirizzo IP pubblico, è necessario utilizzare hello CLI o PowerShell toocreate hello interfaccia di rete.

>[!Note]
> Azure assegna un'interfaccia di rete di MAC indirizzo toohello solo dopo che l'interfaccia di rete hello è macchina virtuale tooa collegato e macchina virtuale hello è stato avviato hello prima volta. È possibile specificare l'indirizzo MAC hello che Azure assegna toohello interfaccia di rete. Hello interfaccia di rete toohello MAC indirizzo rimane assegnati finché non viene eliminato l'interfaccia di rete hello o indirizzo IP privato hello assegnato toohello configurazione IP primaria dell'interfaccia di rete primaria hello viene modificato. informazioni su indirizzi IP e le configurazioni IP, leggere hello toolearn [gli indirizzi IP gestire](virtual-network-network-interface-addresses.md) articolo.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Visualizzare le impostazioni dell'interfaccia di rete

È possibile visualizzare e modificare la maggior parte delle impostazioni di un'interfaccia di rete dopo la sua creazione.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su interfaccia di rete hello tooview desiderato oppure modificare le impostazioni per.
4. Hello impostazioni riportate di seguito sono elencate nel pannello hello che viene visualizzato per l'interfaccia di rete hello selezionato:
    - **Panoramica:** fornisce informazioni sull'interfaccia di rete hello, ad esempio gli indirizzi IP di hello assegnati tooit, l'interfaccia di rete hello hello subnet rete virtuale viene assegnato a, e l'interfaccia di rete hello hello macchina virtuale è collegata troppo (se è collegato tooone). Hello seguente immagine vengono mostrate hello Panoramica impostazioni per un'interfaccia di rete denominata **mywebserver256**: ![Cenni preliminari sull'interfaccia di rete](./media/virtual-network-network-interface/nic-overview.png) è possibile spostare un gruppo di risorse diverso tooa interfaccia di rete o sottoscrizione, fare clic su (**modificare**) toohello Avanti **gruppo di risorse** o **nome sottoscrizione**. Se si sposta l'interfaccia di rete hello, è necessario spostare tutti l'interfaccia di rete correlati toohello risorse con esso. Se l'interfaccia di rete hello è macchina virtuale tooa collegato, ad esempio, è necessario spostare anche macchina virtuale hello e altre risorse correlate alla macchina virtuale. toomove un'interfaccia di rete, leggere hello [spostare risorse tooa nuovo gruppo di risorse o sottoscrizione](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) articolo. articolo di Hello vengono elencati i prerequisiti e come risorse toomove utilizzando portale di Azure PowerShell, hello e hello CLI di Azure.
    - **Le configurazioni IP:** indirizzi pubblici e privati IPv4 e IPv6 tooIP configurazioni assegnati sono elencati di seguito. Se la configurazione IP tooan viene assegnato da un indirizzo IPv6, indirizzi di hello non viene visualizzato. Altre informazioni sulle configurazioni IP come indirizzi IP tooadd e rimuovere hello [indirizzi IP di configurazione per un'interfaccia di rete di Azure](virtual-network-network-interface-addresses.md) articolo. In questa sezione vengono configurati anche l'inoltro IP e l'assegnazione di subnet. ulteriori informazioni su queste impostazioni, leggere hello toolearn [abilitare o disabilitare l'inoltro IP](#enable-or-disable-ip-forwarding) e [modificare assegnazione subnet](#change-subnet-assignment) sezioni di questo articolo.
    - **I server DNS:** è possibile specificare quale server DNS un'interfaccia di rete viene assegnata da hello server DHCP di Azure. Hello interfaccia di rete può ereditare impostazione hello da hello interfaccia di rete hello di rete virtuale viene assegnato a, o un'impostazione personalizzata che sostituisce l'impostazione di hello per cui è assegnata la rete virtuale hello. toomodify ciò che viene visualizzato, hello completo di passaggi di hello [server DNS modifica](#change-dns-servers) sezione di questo articolo.
    - **Rete gruppo di sicurezza ():** Visualizza quale gruppo è associata l'interfaccia di rete toohello (se presente). Contiene un traffico di rete toofilter regole in entrata e in uscita per l'interfaccia di rete hello. Se un gruppo è l'interfaccia di rete associato toohello, nome hello di hello che viene visualizzato il gruppo associato. toomodify ciò che viene visualizzato, hello completo di passaggi di hello [gestire le associazioni gruppo di sicurezza di rete](virtual-network-manage-nsg-arm-portal.md#manage-associations) articolo.
    - **Proprietà:** consente di visualizzare le impostazioni di interfaccia di rete hello, incluso il relativo indirizzo MAC (vuoto se non è l'interfaccia di rete hello macchina virtuale associata tooa) della chiave e hello esiste nella sottoscrizione.
    - **Le regole di sicurezza efficace:** sono elencate le regole di sicurezza, se l'interfaccia di rete hello tooa collegato in esecuzione sulla macchina virtuale e un gruppo è l'interfaccia di rete associato toohello, subnet hello viene assegnato a, oppure entrambi. toolearn ulteriori informazioni su ciò che viene visualizzato, leggere hello [risolvere i problemi relativi a gruppi di sicurezza di rete](virtual-network-nsg-troubleshoot-portal.md#nsg) articolo. ulteriori informazioni sulla NSGs, leggere hello toolearn [gruppi di sicurezza di rete](virtual-networks-nsg.md) articolo.
    - **Route valide:** sono elencate le route, se l'interfaccia di rete hello è collegato tooa in esecuzione sulla macchina virtuale. le route di Hello sono una combinazione di cicli di hello predefinito di Azure, le route definite dall'utente (UDR) e le route BGP eventualmente presenti per l'interfaccia di rete hello hello subnet viene assegnato a. toolearn ulteriori informazioni su ciò che viene visualizzato, leggere hello [risolvere route](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) articolo. altre informazioni sulle predefinito di Azure e UDRs, leggere hello toolearn [le route definite dall'utente](virtual-networks-udr-overview.md) articolo.
    - **Impostazioni comuni di gestione risorse di Azure:** toolearn ulteriori informazioni sulle impostazioni comuni di gestione risorse di Azure, leggere hello [log attività](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [Access control (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [tag ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Blocca](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), e [script di automazione](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) articoli.

**Comandi**

Se l'interfaccia di rete tooa viene assegnato da un indirizzo IPv6, hello output PowerShell restituisce fatti hello che viene assegnato l'indirizzo di hello, ma non restituisce indirizzo hello assegnato. Analogamente, hello CLI restituisce fatto hello che hello indirizzo assegnato, ma restituisce *null* nel relativo output per l'indirizzo di hello.

|Strumento|Comando|
|---|---|
|CLI|[elenco di AZ rete nic](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview interfacce di rete nella sottoscrizione hello; [Mostra scheda di rete az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooview impostazioni per un'interfaccia di rete|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview interfacce di rete nelle impostazioni di sottoscrizione o la vista hello per un'interfaccia di rete|

## <a name="change-dns-servers"></a>Modificare i server DNS

server DNS Hello viene assegnato da hello Azure DHCP server toohello interfaccia di rete all'interno del sistema operativo di hello macchina virtuale. server DNS Hello assegnato è qualsiasi impostazione del server DNS hello è per un'interfaccia di rete. toolearn informazioni sulle impostazioni di risoluzione nome per un'interfaccia di rete, vedere [la risoluzione dei nomi per le macchine virtuali](virtual-networks-name-resolution-for-vms-and-role-instances.md). interfaccia di rete Hello può ereditare le impostazioni di hello dalla rete virtuale hello o utilizzare le proprie impostazioni univoche che sostituiscono l'impostazione di hello per la rete virtuale hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su interfaccia di rete hello tooview desiderato oppure modificare le impostazioni per.
4. Nel Pannello di hello per interfaccia di rete hello è selezionata, fare clic su **server DNS** in **impostazioni**.
5. Selezionare una delle opzioni seguenti:
    - **Ereditare da una rete virtuale (impostazione predefinita)**: scegliere questa opzione tooinherit hello impostazioni del server DNS definito per l'interfaccia di rete hello hello rete virtuale viene assegnato a. A livello di rete virtuale hello, un server DNS personalizzato o un server DNS fornito da Azure hello è definito. Hello server DNS fornito da Azure può risolvere i nomi host per le risorse assegnate toohello stessa rete virtuale. FQDN deve essere tooresolve utilizzato per le risorse assegnate toodifferent le reti virtuali.
    - **Custom**: È possibile configurare i propri nomi tooresolve di server DNS su più reti virtuali. Immettere l'indirizzo IP hello del server hello desiderato toouse come server DNS. indirizzo server DNS di Hello specificato viene assegnato solo l'interfaccia di rete toothis ed esegue l'override a che le impostazioni DNS per interfaccia di rete hello hello rete virtuale viene assegnato.
6. Fare clic su **Salva**.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>Abilitare o disabilitare l'inoltro IP

L'inoltro IP consente macchina virtuale hello che è collegata un'interfaccia di rete:
- Ricevere il traffico di rete non destinato a uno degli indirizzi IP hello assegnati tooany delle configurazioni IP hello assegnato toohello interfaccia di rete.
- Inviare il traffico di rete con un indirizzo IP di origine diversa rispetto a hello tooone assegnato una delle configurazioni IP dell'interfaccia di rete.

Hello deve essere attivata per ogni interfaccia di rete di macchina virtuale toohello collegati che riceve il traffico che hello tooforward esigenze di macchina virtuale. Una macchina virtuale può inoltrare il traffico che abbia più interfacce di rete o tooit di interfaccia associata una singola rete. Durante l'inoltro dell'indirizzo IP è un'impostazione di Azure, macchina virtuale hello necessario eseguire anche un traffico di hello tooforward in grado di applicazione, ad esempio firewall, ottimizzazione WAN e il bilanciamento del carico delle applicazioni. Quando una macchina virtuale è in esecuzione applicazioni di rete, macchina virtuale hello è spesso tooas cui un dispositivo di rete virtuale. È possibile visualizzare un elenco toodeploy pronto accessori di rete virtuale in hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). L'inoltro IP viene in genere usato con le route definite dall'utente. altre informazioni sulle route definite dall'utente, leggere hello toolearn [le route definite dall'utente](virtual-networks-udr-overview.md) articolo.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su interfaccia di rete hello desiderati tooenable o disabilitare l'inoltro per IP.
4. Nel Pannello di hello per interfaccia di rete hello è selezionata, fare clic su **le configurazioni IP** in hello **impostazioni** sezione.
5. Fare clic su **abilitato** o **disabilitato** impostazione di hello toochange (impostazione predefinita).
6. Fare clic su **Salva**.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Cambiare l'assegnazione delle subnet

È possibile modificare la subnet hello, ma non hello rete virtuale, assegnato a un'interfaccia di rete.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **interfacce di rete** pannello visualizzato, fare clic su interfaccia di rete hello tooview desiderato oppure modificare le impostazioni per.
4. Fare clic su **le configurazioni IP** in **impostazioni** nel Pannello di hello per interfaccia di rete hello selezionato. Se gli indirizzi IP privati per tutte le configurazioni IP elencati **(statico)** toothem successivo, è necessario modificare hello IP indirizzo assegnazione metodo toodynamic completando i passaggi di hello che seguono. Tutti gli indirizzi IP privati devono essere assegnati con hello assegnazione dinamica toochange hello subnet assegnazione del metodo per l'interfaccia di rete hello. Se gli indirizzi di hello vengono assegnati con metodo dinamico hello, continuare toostep cinque. Se tutti gli indirizzi IPv4 vengono assegnati con il metodo di assegnazione statica di hello, completare hello seguendo i passaggi toochange hello assegnazione metodo toodynamic:
    - Fare clic su configurazione IP hello desiderato hello toochange metodo di assegnazione indirizzo IPv4 per elenco hello delle configurazioni IP.
    - Nel pannello hello che viene visualizzato per la configurazione IP hello, fare clic su **dinamica** per hello **assegnazione** metodo. È possibile assegnare un indirizzo IPv6 con il metodo di assegnazione statica di hello.
    - Fare clic su **Salva**.
5. Selezionare subnet hello desiderato hello di toofrom interfaccia di rete di tooconnect hello **Subnet** elenco a discesa.
6. Fare clic su **Salva**. Nuovi indirizzi dinamici vengono assegnati dall'intervallo di indirizzi hello subnet per subnet nuova hello. Dopo l'assegnazione hello rete interfaccia tooa nuova subnet, è possibile assegnare un indirizzo IPv4 statico dall'intervallo di indirizzi subnet nuova hello se si sceglie. altre informazioni sull'aggiunta, modifica e rimozione di indirizzi IP per un'interfaccia di rete, leggere hello toolearn [gli indirizzi IP gestire](virtual-network-network-interface-addresses.md) articolo.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Eliminare un'interfaccia di rete

È possibile eliminare un'interfaccia di rete fino a quando non è una macchina virtuale tooa associata. In caso di macchina virtuale tooa collegato, è necessario prima lo stato di macchina virtuale hello arrestato (deallocato) hello sul posto, quindi scollegare l'interfaccia di rete di hello dalla macchina virtuale hello, prima di poter eliminare l'interfaccia di rete hello. toodetach un'interfaccia di rete da una macchina virtuale, hello completato i passaggi in hello [scollegare un'interfaccia di rete da una macchina virtuale](virtual-network-network-interface-vm.md#vm-remove-nic) sezione di hello [aggiungere o rimuovere le interfacce di rete](virtual-network-network-interface-vm.md) articolo. Eliminazione di una macchina virtuale si disconnette tutti tooit di allegato di interfacce di rete, ma non elimina le interfacce di rete hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che rappresenta le autorizzazioni assegnate (almeno) per il ruolo di collaboratore rete hello per la sottoscrizione. Hello lettura [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ulteriori informazioni sull'assegnazione di ruoli e autorizzazioni tooaccounts toolearn di articolo.
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *interfacce di rete*. Quando **interfacce di rete** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. Interfaccia di rete hello rapida toodelete desiderato e fare clic su **eliminare**.
4. Fare clic su **Sì** tooconfirm eliminazione hello dell'interfaccia di rete.

Quando si elimina un'interfaccia di rete, qualsiasi MAC o gli indirizzi IP assegnati tooit vengono rilasciati.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Passaggi successivi
gli indirizzi di una macchina virtuale con più interfacce di rete o indirizzo IP, toocreate leggere hello seguenti articoli:

**Comandi**

|Attività|Strumento|
|---|---|
|Creare una macchina virtuale con più NIC|[Interfaccia della riga di comando](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Creare una macchina virtuale con una singola scheda di interfaccia di rete e più indirizzi IPv4|[Interfaccia della riga di comando](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Creare una macchina virtuale con una singola scheda di interfaccia di rete con un indirizzo IPv6 privato (dietro un Azure Load Balancer)|[Interfaccia della riga di comando](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Modello di Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|

---
title: tooor interfacce di rete aaaAdd rimuovere macchine virtuali di Azure | Documenti Microsoft
description: Informazioni su come tooor interfacce di rete tooadd rimuove le interfacce di rete da macchine virtuali.
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
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>Aggiungere le interfacce di rete tooor rimuovere dalle macchine virtuali

Informazioni su come tooadd una rete esistente interfaccia durante la creazione di una macchina virtuale oppure aggiungere o rimuovere le interfacce di rete da una macchina virtuale esistente in hello arrestato (deallocato). Un'interfaccia di rete consente toocommunicate una macchina virtuale (VM) di Azure con Internet, Azure e alle risorse locali. Una macchina virtuale può avere una o più interfacce di rete. 

Se è necessario tooadd, modificare o rimuovere gli indirizzi IP per un'interfaccia di rete, leggere hello [gestire gli indirizzi IP dell'interfaccia di rete](virtual-network-network-interface-addresses.md) articolo. Se è necessario toocreate, modificare o eliminare le interfacce di rete, leggere hello [gestire interfacce di rete](virtual-network-network-interface.md) articolo.

## <a name="before"></a>Prima di iniziare

Completare hello seguenti attività prima di completare i passaggi in alcuna sezione di questo articolo:

- Informazioni sulle interfacce di rete quanti ogni dimensione di Linux e macchina virtuale di Windows supporta esaminando hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale.
- Accedi toohello Azure [portal](https://portal.azure.com), Azure interfaccia della riga di comando (CLI) o Azure PowerShell con un account di Azure. Se non si ha un account Azure, registrarsi per ottenere un [account per la versione di prova gratuita](https://azure.microsoft.com/free).
- Se l'utilizzo di PowerShell comandi toocomplete attività in questo articolo, [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di cmdlet di Azure PowerShell hello installato. Guida di tooget per i comandi di PowerShell, con esempi, digitare `get-help <command> -full`.
- Se tramite l'interfaccia della riga di comando (CLI) Azure comandi toocomplete attività in questo articolo, [installare e configurare hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Verificare di disporre di versione più recente di hello di hello Azure CLI installato. Guida di tooget per i comandi CLI, digitare `az <command> --help`. Anziché installare hello CLI e relativi prerequisiti, è possibile usare hello Shell di Cloud di Azure. Hello Azure Cloud Shell è una shell Bash gratuita che è possibile eseguire direttamente all'interno di hello portale di Azure. Ha hello CLI di Azure preinstallato e configurato toouse con l'account. hello toouse Shell Cloud, fare clic su hello Cloud Shell **> _** pulsante nella parte superiore di hello di hello [portale](https://portal.azure.com).

## <a name="about"></a>Interfacce di rete e macchine virtuali

È possibile aggiungere (allegare) un tooa di interfaccia di rete VM quando si crea hello VM, purché non sia già stato interfaccia di rete hello esistente associata tooanother macchina virtuale. È possibile aggiungere un'interfaccia di rete a o rimuovere (disconnettere) una rete interfaccia toofrom una macchina virtuale esistente, purché hello macchina virtuale è in hello arrestato (deallocato). Se si crea una macchina virtuale tramite il portale di Azure hello, portale hello crea un'interfaccia di rete con le impostazioni predefinite. portale Hello non consente di:

- Specificare un tooadd di interfaccia di rete esistente durante la creazione di hello VM
- Creare una VM con più interfacce di rete
- Specificare un nome per l'interfaccia di rete hello (portale hello crea l'interfaccia di rete hello con un nome predefinito)

È possibile utilizzare Azure PowerShell o hello CLI toocreate un'interfaccia di rete o macchina virtuale con tutti gli attributi precedenti hello che non è possibile utilizzare il portale di hello per. Prima di completare attività hello in hello nelle sezioni che seguono, prendere in considerazione seguente hello vincoli e i comportamenti:

- Tutte le dimensioni di macchina virtuale supportano almeno due interfacce di rete, ma alcune dimensioni di macchina virtuale ne supportano più di due. Hello precedenti, alcune VM dimensioni supportate in solo un'interfaccia di rete. toolearn il numero di interfacce di rete supporta ogni dimensione della macchina virtuale, leggere hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale. 
- In hello precedente, le interfacce di rete potrebbe essere solo aggiunti tooVMs supportati più interfacce di rete che sono stati creati con almeno due interfacce di rete. È Impossibile aggiungere un tooa di interfaccia di rete VM che è stato creato con un'interfaccia di rete, anche se hello dimensioni delle macchine Virtuali supportate più interfacce di rete. Al contrario, è possibile rimuovere solo le interfacce di rete da una macchina virtuale con almeno tre interfacce di rete, perché le macchine virtuali create con almeno due interfacce di rete è sempre stato toohave almeno due interfacce di rete. Attualmente non si applica alcuno di questi vincoli. È ora possibile creare una macchina virtuale con un numero qualsiasi di interfacce di rete (verso l'alto numero toohello supportato dal hello dimensioni delle macchine Virtuali) e aggiungere o rimuovere un numero qualsiasi di interfacce di rete (dallo stato di macchine virtuali in hello arrestato (deallocate)), purché hello VM ha sempre almeno un'interfaccia di rete.
- Per impostazione predefinita, l'interfaccia di rete in una macchina virtuale prima hello è definita come hello *primario* interfaccia di rete. Tutte le altre interfacce di rete VM hello sono *secondario* interfacce di rete.
- Interfacce di rete primarie sono assegnate un gateway predefinito dai server DHCP di Azure hello, ma non interfacce di rete secondarie. Poiché alle interfacce di rete secondarie non è assegnato un gateway predefinito, non possono comunicare con le risorse all'esterno della loro subnet per impostazione predefinita. interfacce di rete secondarie tooenable in toocommunicate una macchina virtuale di Windows con le risorse all'esterno le subnet, aggiungere route toohello sistema utilizzando hello `route add` comando dalla riga di comando di Windows. Per le macchine virtuali Linux, poiché il comportamento predefinito di hello utilizza host vulnerabile routing, è consigliabile limitare il traffico di rete secondarie interfacce tooa singola subnet. Se si richiedono la connettività all'esterno di subnet hello per le interfacce di rete secondaria, attivazione basata su criteri routing tooensure che in ingresso e il traffico in uscita utilizza hello stessa interfaccia di rete.
- Per impostazione predefinita, tutto il traffico in uscita dalla VM viene inviato all'indirizzo IP hello hello assegnato configurazione IP primaria toohello hello principale dell'interfaccia di rete. Controllare l'indirizzo IP utilizzato per il traffico in uscita all'interno del sistema operativo della macchina virtuale di hello, ma per impostazione predefinita, tramite l'interfaccia di rete primaria hello è.
- In hello precedenti, tutte le macchine virtuali all'interno di hello stesso set di disponibilità sono necessari toohave una rete di unica o più interfacce. Le macchine virtuali con un numero qualsiasi di interfacce ora possono essere presenti in rete hello stesso set di disponibilità, il numero di toohello supportati da hello dimensioni della macchina virtuale. È possibile aggiungere solo una disponibilità tooan VM impostato quando viene creato tramite. ulteriori informazioni sui set di disponibilità, leggere hello toolearn [gestione hello disponibilità delle macchine virtuali in Azure](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) articolo.
- Mentre le interfacce di rete hello stessa macchina virtuale può essere connesso toodifferent subnet all'interno di una rete virtuale, tutte le interfacce di rete hello devono essere connesso toohello stessa rete virtuale.
- È possibile aggiungere qualsiasi indirizzo IP per qualsiasi configurazione IP di qualsiasi pool tooan back-end di bilanciamento del carico di Azure interfaccia di rete primario o secondario. In hello precedente, solo hello indirizzo IP primario per l'interfaccia di rete primaria hello è possibile aggiungere pool back-end tooa. altre informazioni sulle configurazioni, leggere hello e gli indirizzi IP toolearn [aggiungere, modificare o rimuovere indirizzi](virtual-network-network-interface-addresses.md) articolo.
- L'eliminazione di una macchina virtuale non comporta l'eliminazione di hello le interfacce tooit associata. Quando viene eliminata una macchina virtuale, le interfacce di rete hello sono scollegate dall'hello macchina virtuale. È possibile aggiungere toodifferent interfacce di rete hello macchine virtuali o eliminarli.
- Se un'interfaccia di rete è un privato tooit indirizzo IPv6, è possibile collegarlo tooa macchina virtuale durante la creazione di hello VM. È possibile collegare un'interfaccia di rete con un tooa di indirizzo IPv6 assegnato VM dopo la creazione di hello macchina virtuale. Se si collega un'interfaccia di rete con un indirizzo IPv6 privato assegnato durante la creazione di una macchina virtuale, è possibile collegare solo rete interfaccia toohello macchina virtuale, indipendentemente dalle dimensioni della VM hello supportano quanti interfacce di rete. Vedere [gli indirizzi IP dell'interfaccia di rete](virtual-network-network-interface-addresses.md) toolearn ulteriori informazioni sull'assegnazione IP indirizzi toonetwork interfacce.

## <a name="vm-create"></a>Aggiungere tooa interfacce di rete esistente nuova macchina virtuale

Quando si crea una macchina virtuale tramite il portale di hello, portale hello crea un'interfaccia di rete con le impostazioni predefinite e la collega toohello macchina virtuale per l'utente. Non è possibile aggiungere tooa interfacce di rete esistente nuova macchina virtuale, o creare una macchina virtuale con più interfacce di rete utilizzando hello portale di Azure. È possibile utilizzare entrambe le utilizzando hello CLI o PowerShell. È possibile aggiungere come molte interfacce tooa macchina virtuale di rete come hello crei supporta dimensioni della macchina virtuale. toolearn ulteriori informazioni sulla rete quanti interfacce ogni supporta dimensioni di macchina virtuale, leggere hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale. interfacce di rete Hello è aggiungere tooa macchina virtuale non possono essere attualmente collegato tooanother macchina virtuale. ulteriori informazioni sulla creazione di interfacce di rete, leggere hello toolearn [gestire interfacce di rete](virtual-network-network-interface.md#create-a-network-interface) articolo.

> [!WARNING]
> Se un'interfaccia di rete dispone di un indirizzo IPv6 privato assegnato tooit, è possibile aggiungere la macchina virtuale hello rete interfaccia toohello solo quando si crea una macchina virtuale hello. È possibile collegare la macchina virtuale di toohello interfaccia di rete più quando si crea una macchina virtuale hello o dopo hello macchina virtuale viene creato, fino a quando la macchina virtuale tooa rete interfaccia collegata tooa assegnato un indirizzo IPv6. Vedere [gli indirizzi IP dell'interfaccia di rete](virtual-network-network-interface-addresses.md) toolearn ulteriori informazioni sull'assegnazione IP indirizzi toonetwork interfacce.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>Aggiungere un esistente tooan di interfaccia di rete VM esistente

È possibile aggiungere come molte interfacce tooa macchina virtuale di rete come hello dimensioni della macchina virtuale si stanno aggiungendo toosupports interfacce di rete. toolearn il numero di interfacce di rete supporta ogni dimensione della macchina virtuale, leggere hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale. Hello VM desiderato tooadd un toomust di interfaccia di rete supporta il numero di hello delle interfacce di rete desiderato tooadd e deve essere in hello arrestato (deallocato) dello stato. interfacce di rete Hello desiderato tooadd attualmente non possono essere collegato tooanother macchina virtuale. È possibile aggiungere tooan interfacce di rete VM utilizzando hello portale di Azure esistente. interfacce di rete tooadd tooan macchina virtuale esistente, è necessario utilizzare hello CLI o PowerShell. 

> [!WARNING]
> Se un'interfaccia di rete dispone di un indirizzo IPv6 privato assegnato tooit, non può essere aggiunto macchina virtuale esistente tooan. È possibile aggiungere un'interfaccia di rete con un'assegnato privata IPv6 indirizzo tooa macchina virtuale solo quando si crea una macchina virtuale. Vedere [gli indirizzi IP dell'interfaccia di rete](virtual-network-network-interface-addresses.md) toolearn ulteriori informazioni sull'assegnazione IP indirizzi toonetwork interfacce.

|Strumento|Comando|
|---|---|
|CLI|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (riferimento) o [passaggi dettagliati](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (riferimento) o [passaggi dettagliati](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a> Visualizzare le interfacce di rete di una macchina virtuale

È possibile visualizzare hello rete interfacce attualmente collegato tooa VM toolearn sulla configurazione di ogni interfaccia di rete e gli indirizzi IP di hello assegnati tooeach interfaccia di rete. 

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che viene assegnato hello ruolo di proprietario, collaboratore o collaboratore di rete per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *macchine virtuali*. Quando **macchine virtuali** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **macchine virtuali** pannello visualizzato, fare clic sul nome hello di hello desiderato tooview interfacce di rete per VM.
4. In hello **impostazioni** di hello pannello macchine virtuali che viene visualizzata per hello macchina virtuale è stata selezionata, fare clic su **interfacce di rete**. toolearn sulle impostazioni di interfaccia di rete e in che modo toochange usarle, vedere l'articolo hello [gestire interfacce di rete](virtual-network-network-interface.md) articolo. toolearn sull'aggiunta, modifica o rimozione di indirizzi IP assegnati tooa l'interfaccia di rete, vedere [gli indirizzi IP gestire](virtual-network-network-interface-addresses.md).

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a> Rimuovere l’interfaccia di rete da una macchina virtuale

Hello macchina virtuale si desidera tooremove (o scollegare) da un'interfaccia di rete deve essere hello arrestato (deallocato) e devono avere le interfacce di rete almeno due associati tooit. È possibile rimuovere alcuna interfaccia di rete, ma deve essere sempre presente almeno una rete interfaccia collegata tooit hello VM. Se si rimuove un'interfaccia di rete primario, Azure assegna hello attributo primario toohello interfaccia di rete è stata hello VM toohello collegati più lungo. 

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che viene assegnato hello ruolo di proprietario, collaboratore o collaboratore di rete per la sottoscrizione. vedere toolearn ulteriori informazioni sull'assegnazione di ruoli tooaccounts, [ruoli predefiniti per il controllo di accesso basato sui ruoli Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Nella casella hello contenente testo hello *individuare risorse* nella parte superiore di hello di hello portale di Azure, digitare *macchine virtuali*. Quando **macchine virtuali** viene visualizzato nei risultati della ricerca hello, selezionarlo.
3. In hello **macchine virtuali** pannello visualizzato, fare clic sul nome hello di hello desiderato tooremove un'interfaccia di rete per la VM.
4. In hello **impostazioni** di hello pannello macchine virtuali che viene visualizzata per hello macchina virtuale è stata selezionata, fare clic su **interfacce di rete**. toolearn sulle impostazioni di interfaccia di rete e in che modo toochange usarle, vedere l'articolo hello [gestire interfacce di rete](virtual-network-network-interface.md) articolo. toolearn sull'aggiunta, modifica o rimozione di indirizzi IP assegnati tooa l'interfaccia di rete, vedere [gli indirizzi IP gestire](virtual-network-network-interface-addresses.md).
5. Nel pannello interfacce rete hello che viene visualizzato, fare clic su hello **...**  toohello destra hello dell'interfaccia di rete che si desidera toodetach.
6. Fare clic su **Scollega**. Se è presente una sola rete interfaccia collegata toohello macchina virtuale, hello **scollegamento** opzione non è disponibile. Fare clic su **Sì** nella finestra di conferma hello.

**Comandi**

|Strumento|Comando|
|---|---|
|CLI|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (riferimento) o [passaggi dettagliati](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (riferimento) o [passaggi dettagliati](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>Passaggi successivi
toocreate una macchina virtuale con più interfacce di rete o degli indirizzi IP, leggere hello seguenti articoli:

**Comandi**

|Attività|Strumento|
|---|---|
|Creare una macchina virtuale con più NIC|[Interfaccia della riga di comando](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Creare una macchina virtuale con una singola scheda di interfaccia di rete e più indirizzi IPv4|[Interfaccia della riga di comando](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Creare una macchina virtuale con una singola scheda di interfaccia di rete con un indirizzo IPv6 privato (dietro un Azure Load Balancer)|[Interfaccia della riga di comando](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Modello di Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|

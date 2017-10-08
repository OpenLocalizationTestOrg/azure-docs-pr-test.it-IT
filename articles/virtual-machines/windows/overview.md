---
title: Panoramica delle macchine virtuali aaaWindows | Documenti Microsoft
description: Informazioni sulla creazione e gestione di macchine virtuali Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Panoramica delle macchine virtuali Windows in Azure

Le macchine virtuali (VM) di Azure sono uno dei vari tipi di [risorse di calcolo scalabili e su richiesta](../../app-service-web/choose-web-site-cloud-service-vm.md) offerte da Azure. In genere, si sceglie una macchina virtuale quando è necessario maggiore controllo sull'ambiente di elaborazione hello rispetto offrono hello altre opzioni. Questo articolo fornisce informazioni sugli aspetti da tenere in considerazione prima di creare una VM e sulla relativa modalità di creazione e gestione.

Fornisce una macchina virtuale di Azure è hello flessibilità della virtualizzazione senza toobuy e mantenere hardware fisico hello che lo esegue. Tuttavia, è comunque necessario toomaintain hello VM mediante l'esecuzione di attività, ad esempio la configurazione, l'applicazione di patch e dell'installazione software hello in esecuzione su di esso.

È possibile usare le macchine virtuali di Azure in vari modi. Di seguito sono riportati alcuni esempi:

* **Sviluppo e test** : macchine virtuali di Azure offrono una rapida e semplice toocreate un computer con configurazioni specifiche necessarie toocode e testare un'applicazione.
* **Le applicazioni nel cloud hello** : perché è richiesta per l'applicazione può variare, potrebbe essere consigliabile toorun su una macchina virtuale in Azure. È possibile pagare per VM aggiuntive quando sono necessarie e arrestarle quando non sono richieste.
* **Estesi datacenter** – macchine virtuali in una rete virtuale di Azure possono essere facilmente rete dell'organizzazione tooyour connesso.

numero di Hello di macchine virtuali che utilizza l'applicazione può applicare la scalabilità verticale e out toowhatever è toomeet necessari esigenze.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>Cosa è necessario toothink sulla prima di creare una macchina virtuale?
Quando si compila l'infrastruttura di un'applicazione in Azure, ci sono sempre numerose [considerazioni di progettazione](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) di cui tener conto. Questi aspetti di una macchina virtuale sono importanti toothink sulla prima di iniziare:

* nomi di Hello le risorse dell'applicazione
* percorso di Hello in cui sono archiviate risorse hello
* dimensioni Hello di hello VM
* numero massimo di Hello di macchine virtuali che possono essere creati
* sistema operativo Hello che hello VM viene eseguito
* configurazione di Hello di hello dopo l'avvio di VM
* risorse correlate Hello che hello che macchina virtuale

### <a name="naming"></a>Denominazione
Una macchina virtuale ha un [nome](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooit assegnato e prevede il nome di un computer configurato come parte del sistema operativo hello. nome Hello di una macchina virtuale può essere di too15 caratteri.

Se si utilizza Azure toocreate hello disco del sistema operativo nome computer hello e nome della macchina virtuale hello hello stesso. Se si [caricare e utilizzare la propria immagine](upload-generalized-managed.md) che contiene un sistema operativo configurato in precedenza e usarlo toocreate una macchina virtuale, i nomi di hello possono essere diversi. È consigliabile quando si carica un file di immagine, impostare nome del computer hello hello del sistema operativo e nome della macchina virtuale hello hello stesso.

### <a name="locations"></a>Località
Tutte le risorse create in Azure vengono distribuite tra più [aree geografiche](https://azure.microsoft.com/regions/) tutto il mondo hello. In genere, viene chiamato area hello **percorso** quando si crea una macchina virtuale. Per una macchina virtuale, il percorso di hello specifica in cui sono archiviati i dischi rigidi virtuali hello.

Questa tabella sono riportati alcuni dei modi hello che è possibile ottenere un elenco dei percorsi disponibili.

| Metodo | Description |
| --- | --- |
| Portale di Azure |Selezionare un percorso dall'elenco di hello quando si crea una macchina virtuale. |
| Azure PowerShell |Hello utilizzare [Get AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) comando. |
| API REST |Hello utilizzare [elenco delle posizioni](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) operazione. |

### <a name="vm-size"></a>Dimensioni macchina virtuale
Hello [dimensioni](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) di hello macchina virtuale che si utilizza è determinato dal carico di lavoro hello che si desidera toorun. dimensioni Hello scelto determinano quindi fattori, ad esempio capacità di archiviazione, memoria e potenza di elaborazione. Azure offre un'ampia gamma di dimensioni toosupport molti tipi di utilizzo.

Azure addebita un [costo orario](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) in base alle dimensioni della macchina virtuale di hello e del sistema operativo. Per le ore parziali, Azure addebita solo per i minuti di hello utilizzati. I costi di archiviazione vengono determinati e addebitati separatamente.

### <a name="vm-limits"></a>Limiti della VM
La sottoscrizione è predefinito [i limiti di quota](../../azure-subscription-service-limits.md) che potrebbe influire sulla distribuzione di hello di molte macchine virtuali per il progetto. il limite corrente di Hello su una base per ogni sottoscrizione è 20 macchine virtuali per ogni area. I limiti possono essere aumentati creando un ticket di supporto in cui si richiede tale incremento.

### <a name="operating-system-disks-and-images"></a>Immagini e dischi del sistema operativo
Macchine virtuali utilizzano [dischi rigidi virtuali (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore ai dati e il sistema operativo (sistema operativo). I dischi rigidi virtuali vengono utilizzati anche per le immagini di hello che è possibile scegliere tra tooinstall un sistema operativo. 

Azure offre molte [immagini marketplace](https://azure.microsoft.com/marketplace/virtual-machines/) toouse con diverse versioni e i tipi di sistemi operativi Windows Server. Le immagini Marketplace sono identificate dall'editore di immagini, dall'offerta, dalla SKU e dalla versione (in genere la versione viene specificata alla fine). 

Questa tabella vengono illustrati alcuni metodi che è possibile trovare informazioni hello per un'immagine.

| Metodo | Description |
| --- | --- |
| Portale di Azure |i valori Hello vengono specificati per l'utente automaticamente quando si seleziona un'immagine toouse. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -Location "location"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -Location "location" -Publisher "publisherName"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "location" -Publisher "publisherName" -Offer "offerName" |
| API REST |[List image publishers](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[List image offers](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[List image skus](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

È possibile scegliere troppo[caricare e utilizzare la propria immagine](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) e quando si esegue l'operazione, il nome di server di pubblicazione hello offerta e sku non utilizzate.

### <a name="extensions"></a>Estensioni
Le [estensioni](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) offrono alla VM funzionalità aggiuntive grazie a una configurazione post-distribuzione e ad attività automatiche.

È possibile eseguire le seguenti attività comuni tramite le estensioni:

* **Eseguire gli script personalizzati** : hello [estensione Script personalizzata](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) consente di configurare i carichi di lavoro nei hello VM eseguendo lo script una volta hello provisioning della macchina virtuale.
* **Distribuire e gestire le configurazioni** : hello [estensione PowerShell DSC Desired State Configuration ()](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) consente di installare DSC in una macchina virtuale toomanage configurazioni e ambienti.
* **Raccogliere dati di diagnostica** : hello [estensione diagnostica di Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) consente di configurare hello VM toocollect dati di diagnostica possono essere utilizzati toomonitor hello dello stato dell'applicazione.

### <a name="related-resources"></a>Risorse correlate
le risorse di Hello in questa tabella vengono utilizzate da hello VM e necessario tooexist o essere create quando viene creato hello VM.

| Risorsa | Obbligatorio | Description |
| --- | --- | --- |
| [Gruppo di risorse](../../azure-resource-manager/resource-group-overview.md) |Sì |Hello VM deve essere contenuta in un gruppo di risorse. |
| [Account di archiviazione](../../storage/common/storage-create-storage-account.md) |Sì |Hello VM deve toostore account di archiviazione hello i dischi rigidi virtuali. |
| [Rete virtuale](../../virtual-network/virtual-networks-overview.md) |Sì |Hello VM deve essere un membro di una rete virtuale. |
| [Indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |No |Hello macchina virtuale può avere un tooremotely tooit di indirizzo IP pubblico di accedervi. |
| [Interfaccia di rete](../../virtual-network/virtual-network-network-interface.md) |Sì |Hello VM deve toocommunicate di interfaccia di rete hello nella rete hello. |
| [Dischi dati](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |No |Hello VM può includere funzionalità di archiviazione tooexpand dischi dati. |

## <a name="how-do-i-create-my-first-vm"></a>Come creare la prima VM
Sono disponibili diverse opzioni per creare una VM. scelta Hello effettuata dipende dall'ambiente hello in. 

Questa tabella fornisce informazioni tooget per iniziare a creare la macchina virtuale.

| Metodo | Articolo |
| --- | --- |
| Portale di Azure |[Creare una macchina virtuale che esegue Windows usando il portale di hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Modelli |[Creare una macchina virtuale Windows con un modello di Gestione risorse](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[Creare una VM Windows tramite PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Client SDK |[Distribuire le risorse di Azure tramite C#](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| API REST |[Create or update a VM](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) (Creare o aggiornare una VM) |

Sebbene ci si auguri che non accada mai nulla, talvolta potrebbero verificarsi dei problemi. Se questa situazione si verifica tooyou, esaminare le informazioni di hello in [Gestione risorse di risolvere i problemi di distribuzione con la creazione di una macchina virtuale Windows in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Come è possibile gestire hello macchina virtuale che è stato creato?
Le VM possono essere gestite mediante un portale basato su browser, gli strumenti da riga di comando con il supporto per gli script o direttamente tramite l'API. Alcune attività di gestione comuni che è possibile eseguire sono recupero di informazioni su una macchina virtuale, l'accesso tooa macchina virtuale, la gestione della disponibilità e la creazione di backup.

### <a name="get-information-about-a-vm"></a>Visualizzare informazioni su una macchina virtuale
Questa tabella illustra alcuni dei modi hello che è possibile ottenere informazioni su una macchina virtuale.

| Metodo | Description |
| --- | --- |
| Portale di Azure |Nel menu hub hello, fare clic su **macchine virtuali** e quindi selezionare hello VM hello elenco. Nel Pannello di hello per hello VM, è necessario accedere alle informazioni toooverview, i valori delle impostazioni e le metriche di monitoraggio. |
| Azure PowerShell |Per informazioni sull'utilizzo di macchine virtuali toomanage di PowerShell, vedere [creare e gestire macchine virtuali di Windows con il modulo di Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| API REST |Hello utilizzare [informazioni recupera macchina virtuale](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) informazioni tooget operazione su una macchina virtuale. |
| Client SDK |Per informazioni sull'utilizzo di macchine virtuali toomanage c#, vedere [gestire macchine virtuali di Azure mediante Gestione risorse di Azure e c#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>Accedere toohello VM
Pulsante hello Connect nel portale di Azure hello troppo[avviare una sessione Desktop remoto (RDP)](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Le cose possono talvolta vanno errate durante il tentativo di toouse una connessione remota. Se questa situazione si verifica tooyou, consultare le informazioni della Guida hello in [tooan connessioni Desktop remoto di risolvere i problemi Azure macchina virtuale che esegue Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Gestire la disponibilità
È importante che si toounderstand come troppo[garantire un'elevata disponibilità](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) per l'applicazione. Questa configurazione prevede la creazione di più macchine virtuali tooensure dotato di almeno uno.

Affinché il tooqualify di distribuzione per il nostro 99.95 VM Service Level Agreement, è necessario toodeploy due o più macchine virtuali in esecuzione il carico di lavoro all'interno di un [set di disponibilità](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). In questo modo le VM vengono distribuite tra più domini di errore e anche in host con finestre di manutenzione diverse. Hello completo [SLA di Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) illustra hello garantita la disponibilità di Azure nel suo complesso.

### <a name="back-up-hello-vm"></a>Eseguire il backup hello VM
Oggetto [insieme di credenziali di servizi di ripristino](../../backup/backup-introduction-to-azure-backup.md) è tooprotect utilizzati dati e risorse in servizi di Backup di Azure e Azure Site Recovery. È possibile utilizzare anche un insieme di credenziali di servizi di ripristino[distribuire e gestire i backup per le macchine virtuali distribuite di gestione risorse con PowerShell](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Passaggi successivi
* Se si toowork con le macchine virtuali Linux, esaminare [Azure e Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Acquisire familiarità con le indicazioni di hello sulla configurazione dell'infrastruttura in hello [procedura dettagliata dell'infrastruttura di Azure di esempio](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

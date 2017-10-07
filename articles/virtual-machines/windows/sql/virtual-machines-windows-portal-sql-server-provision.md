---
title: una macchina virtuale di SQL Server aaaProvision | Documenti Microsoft
description: "Creazione e la connessione macchina virtuale di SQL Server tooa in Azure tramite il portale di hello. In questa esercitazione Usa la modalità di gestione risorse di hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Eseguire il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello
> [!div class="op_single_selector"]
> * [Portale](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

In questa esercitazione end-to-end viene illustrato come toouse hello tooprovision portale Azure una macchina virtuale che esegue SQL Server.

raccolta di macchine virtuali di Azure (VM) Hello include diverse immagini contenenti Microsoft SQL Server. Con pochi clic, è possibile selezionare una delle immagini VM SQL dalla raccolta hello hello ed effettuare il provisioning nell'ambiente Azure.

In questa esercitazione si apprenderà come:

* [Selezionare un'immagine di SQL VM dalla raccolta hello](#select-a-sql-vm-image-from-the-gallery)
* [Configurare e creare hello VM](#configure-the-vm)
* [Aprire hello VM con Desktop remoto](#open-the-vm-with-remote-desktop)
* [Connettersi tooSQL Server in modalità remota](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Selezionare un'immagine di SQL VM dalla raccolta hello

1. Accedi toohello [portale di Azure](https://portal.azure.com) con l'account.

   > [!NOTE]
   > Se non si dispone di un account Azure, provare la [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

2. Nel portale di Azure hello, fare clic su **New**. viene visualizzato il portale di Hello hello **New** finestra.

3. In hello **New** finestra, fare clic su **calcolo** e quindi fare clic su **tutti**.

   ![Finestre Nuovo e Calcolo](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. Nel campo di ricerca hello, digitare **SQL Server**, e premere INVIO.

5. Quindi fare clic su hello **filtro** sull'icona e selezionare **Microsoft** per server di pubblicazione hello. Fare clic su **eseguita** sui risultati di hello filtro finestra toofilter hello tooMicrosoft pubblicato le immagini di SQL Server.

   ![Finestra per macchine virtuali di Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Esaminare le immagini di SQL Server disponibili hello. Ogni immagine identifica una versione di SQL Server e un sistema operativo.

6. Immagine di hello selezionare denominata **licenza gratuita: SQL Server 2016 Developer SP1 in Windows Server 2016**.

   > [!TIP]
   > edizione Developer Hello viene utilizzato in questa esercitazione perché è una versione completa di SQL Server che è disponibile per lo sviluppo ai fini del test. Si paga solo per il costo di hello di esecuzione hello macchina virtuale. Sono tuttavia toochoose disponibile uno qualsiasi dei toouse immagini hello in questa esercitazione.

   > [!TIP]
   > Le immagini VM SQL includono sui costi delle licenze hello per SQL Server in hello al minuto prezzi di hello macchina virtuale creata (ad eccezione di hello Developer ed Express Edition). SQL Server per sviluppatori è gratuito per sviluppo/test (non per la produzione), mentre SQL Express è gratuito per carichi di lavoro leggeri (inferiori a 1 GB di memoria e a 10 GB di archiviazione). È presente un'altra opzione toobring-your-proprietari-licenza (BYOL) e pagare solo per hello macchina virtuale. Tali nomi di immagine hanno il prefisso {BYOL}. 
   >
   > Per altre informazioni su queste opzioni, vedere [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Guida ai prezzi per le VM di SQL Server in Azure).

7. In **Selezionare un modello di distribuzione** assicurarsi che l'opzione **Resource Manager** sia selezionata. Gestione risorse è hello consigliata il modello di distribuzione per le nuove macchine virtuali. 

8. Fare clic su **Crea**.

    ![Creare VM di SQL con Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Configurare hello VM
Per la configurazione di una macchina virtuale di SQL Server sono disponibili cinque finestre.

| Passaggio | Descrizione |
| --- | --- |
| **Nozioni di base** |[Configurare le impostazioni di base](#1-configure-basic-settings) |
| **Dimensione** |[Scegliere le dimensioni della macchina virtuale](#2-choose-virtual-machine-size) |
| **Impostazioni** |[Configurare le funzionalità facoltative](#3-configure-optional-features) |
| **Impostazioni di SQL Server** |[Configurare le impostazioni di SQL Server](#4-configure-sql-server-settings) |
| **Riepilogo** |[Riepilogo hello di revisione](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Configurare le impostazioni di base

In hello **nozioni di base** finestra forniscono hello le seguenti informazioni:

* Immettere un **Nome**univoco per la macchina virtuale.

* Selezionare **SSD** come tipo di disco della macchina virtuale per ottenere prestazioni ottimali.

* Specificare un **nome utente** per account di amministratore locale hello in hello macchina virtuale. Questo account viene aggiunto anche SQL Server toohello **sysadmin** ruolo predefinito del server.

* Specificare una **Password**complessa.

* Se si dispone di più sottoscrizioni, verificare che sia corretta per la sottoscrizione hello hello nuova macchina virtuale.

* In hello **gruppo di risorse** , digitare un nome per un nuovo gruppo di risorse. In alternativa, di scegliere un gruppo di risorse esistente di toouse **utilizzare esistente**. Un gruppo di risorse è una raccolta di risorse correlate in Azure, ovvero macchine virtuali, account di archiviazione, reti virtuali e così via.

  > [!NOTE]
  > L'uso di un nuovo gruppo di risorse risulta utile se si stanno solo eseguendo test o se si sta iniziando a usare le distribuzioni di SQL Server in Azure. Dopo aver completato il test, eliminare hello risorsa gruppo tooautomatically delete hello VM e tutte le risorse associate a tale gruppo di risorse. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).

* Selezionare un **percorso** per hello regione di Azure che ospiterà questa distribuzione.

* Fare clic su **OK** impostazioni hello toosave.

    ![Finestra Informazioni di base per SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Scegliere le dimensioni della macchina virtuale

In hello **dimensioni** passaggio, scegliere una dimensione di macchina virtuale in hello **scegliere una dimensione** finestra. finestra Hello vengono inizialmente visualizzate le dimensioni delle macchine consigliati in base a hello l'immagine selezionata.

> [!IMPORTANT]
> Hello stimato il costo mensile visualizzato su hello **scegliere una dimensione** finestra non include i costi di licenza di SQL Server. Questo è il costo di hello di hello VM autonoma. Per hello Express e Developer Edition di SQL Server, si tratta di costo stimato totale hello. Per altre edizioni, vedere hello [pagina dei prezzi delle macchine virtuali di Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) e selezionare l'edizione di destinazione di SQL Server. Vedere anche hello [prezzi linee guida per le macchine virtuali di SQL Server Azure](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opzioni per le dimensioni di VM di SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Per i carichi di lavoro, vedere hello consiglia le dimensioni della macchina e la configurazione in [prestazioni ottimali per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md). Se occorre una dimensione della macchina che non è elencata, fare clic su hello **visualizzare tutti** pulsante.

> [!NOTE]
> Per altre informazioni sulle dimensioni di macchine virtuali, vedere [Dimensioni delle macchine virtuali](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Scegliere le dimensioni della macchina virtuale e quindi fare clic su **Seleziona**.

## <a name="3-configure-optional-features"></a>3. Configurare le funzionalità facoltative

In hello **impostazioni** finestra, configurare l'archiviazione di Azure, servizi di rete e il monitoraggio per la macchina virtuale hello.

* In **Archiviazione** selezionare **Sì** sotto **Usa il servizio Managed Disks**.

   > [!NOTE]
   > Per SQL Server è consigliabile usare Managed Disks. Archivio di handle di dischi in background hello gestito. Inoltre, quando le macchine virtuali con dischi gestiti sono hello stesso set di disponibilità, Azure distribuisce hello risorse tooprovide appropriato la ridondanza dell'archiviazione. Per altre informazioni, vedere [Panoramica di Azure Managed Disks](../../../storage/storage-managed-disks-overview.md). Per informazioni dettagliate sull'uso di Managed Disks in un set di disponibilità, vedere [Usare Managed Disks per le macchine virtuali nel set di disponibilità](../manage-availability.md).

* In **rete**, è possibile accettare i valori hello popolato automaticamente. È anche possibile fare clic su ogni funzionalità toomanually configurare hello **rete virtuale**, **Subnet**, **indirizzo IP pubblico**, e **gruppodisicurezzadirete**. Per motivi di hello di questa esercitazione, mantenere i valori predefiniti di hello.

* Abilita Azure **monitoraggio** per impostazione predefinita con hello stesso account di archiviazione designato per hello macchina virtuale. Queste impostazioni possono essere modificate qui, se necessario.

* In **set di disponibilità**, è possibile lasciare predefinito hello **Nessuno** per questa esercitazione. Se si prevede di tooset i gruppi di disponibilità AlwaysOn SQL, configurare hello disponibilità tooavoid ricrea hello macchina virtuale.  Per ulteriori informazioni, vedere [Gestisci hello disponibilità delle macchine virtuali](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Al termine della configurazione di queste impostazioni, fare clic su **OK**.

## <a name="4-configure-sql-server-settings"></a>4. Configurare le impostazioni di SQL Server
In hello **impostazioni di SQL Server** finestra, configurare impostazioni specifiche e le ottimizzazioni per SQL Server. le impostazioni di Hello che è possibile configurare per SQL Server includono i seguenti hello.

| Impostazione |
| --- |
| [Connettività](#connectivity) |
| [Autenticazione](#authentication) |
| [Configurazione dell'archiviazione](#storage-configuration) |
| [Applicazione automatica delle patch](#automated-patching) |
| [Backup automatico](#automated-backup) |
| [Integrazione dell'insieme di credenziali delle chiavi di Azure](#azure-key-vault-integration) |
| [Servizi R](#r-services) |

### <a name="connectivity"></a>Connettività

In **connettività SQL**, specificare il tipo di hello di accesso desiderato toohello istanza di SQL Server in questa macchina virtuale. Ai fini di hello di questa esercitazione, selezionare **pubblico (internet)** tooallow connessioni tooSQL Server dal computer o i servizi in hello internet. Con questa opzione è selezionata, Azure configura automaticamente il firewall hello e hello sicurezza gruppo tooallow traffico sulla porta 1433.

![Opzioni di connettività di SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> Per impostazione predefinita, SQL Server è in ascolto su una porta nota, la porta **1433**. Per una maggiore sicurezza, modificare la porta di hello nel hello toolisten di finestra di dialogo precedente su una porta non predefinito, ad esempio 1401. In questo caso, è necessario usare tale porta per la connessione da qualsiasi strumento client, ad esempio SSMS.

tooconnect tooSQL Server tramite hello internet, è anche necessario abilitare l'autenticazione di SQL Server, descritto nella sezione successiva hello.

Se si preferisce toonot abilitare connessioni toohello motore di Database tramite hello internet, scegliere una delle seguenti opzioni hello:

* **Locale (all'interno di VM)** tooallow connessioni tooSQL Server solo da all'interno di hello macchina virtuale.
* **Private (all'interno di rete virtuale)** tooallow connessioni tooSQL Server da computer o i servizi in hello stessa rete virtuale.

Migliorare la sicurezza in generale, scegliendo la connettività di più restrittiva di hello, lo scenario lo consente. Tuttavia, tutte le opzioni di hello sono entità a protezione diretta tramite regole del gruppo di sicurezza di rete e l'autenticazione di Windows/SQL. È possibile modificare il gruppo di sicurezza di rete dopo la creazione della macchina virtuale hello. Per altre informazioni, vedere [Considerazioni relative alla sicurezza per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-security.md).

> [!NOTE]
> immagine di macchina virtuale Hello per SQL Server Express edition non abilita il protocollo TCP/IP hello automaticamente. Questo vale anche per hello connettività privati e pubblici opzioni. Per l'edizione Express, è necessario utilizzare Gestione configurazione SQL Server troppo[abilitare manualmente il protocollo TCP/IP hello](#configure-sql-server-to-listen-on-the-tcp-protocol) dopo la creazione di hello macchina virtuale.

### <a name="authentication"></a>Autenticazione

Se è necessaria l'autenticazione di SQL Server, fare clic su **Abilita** under **Autenticazione SQL**.

![Autenticazione di SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Se si prevede di SQL Server tooaccess su hello internet (ad esempio hello opzioni di connettività pubblico), è necessario abilitare l'autenticazione di SQL qui. Accesso pubblico toohello SQL Server richiede l'uso di hello di autenticazione di SQL Server.
> 
> 

Se si abilita l'autenticazione di SQL Server, specificare un **Nome di accesso** e una **Password**. Questo nome utente è configurato come account di accesso di autenticazione di SQL Server e un membro di hello **sysadmin** ruolo predefinito del server. Per altre informazioni sulle modalità di autenticazione, vedere [Scegliere una modalità di autenticazione](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) .

Se non si abilita l'autenticazione di SQL Server, è possibile utilizzare account di amministratore locale hello nell'istanza di SQL Server toohello tooconnect VM hello.

### <a name="storage-configuration"></a>Configurazione dell'archiviazione

Fare clic su **configurazione dell'archiviazione** toospecify i requisiti di archiviazione hello.

![Configurazione dell'archiviazione SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Se è stato configurato manualmente l'archiviazione standard toouse di macchina virtuale, questa opzione non è disponibile. L'ottimizzazione automatica delle risorse di archiviazione è disponibile solo per l'Archiviazione Premium.

> [!TIP]
> numero di Hello di arresto e i limiti superiori di hello di ogni dispositivo di scorrimento sono dipendenti dalle dimensioni hello della macchina virtuale selezionata. Una macchina virtuale più grande e più potente è in grado di tooscale ulteriormente verso l'alto.

È possibile specificare requisiti come operazioni di I/O al secondo, velocità effettiva in Mbps e dimensioni di archiviazione totali. Configurare questi valori con scale estendibile hello. È possibile modificare queste impostazioni di archiviazione in base al carico di lavoro. portale Hello calcola automaticamente hello numero di dischi tooattach e configurare in base a questi requisiti.

In **archiviazione ottimizzata per**, selezionare una delle seguenti opzioni hello:

* **Generale** è l'impostazione predefinita hello e supporta la maggior parte dei carichi di lavoro.
* **Transazionale** elaborazione Ottimizza l'archiviazione di hello per carichi di lavoro OLTP database tradizionale.
* **Il data warehousing** Ottimizza l'archiviazione di hello per carichi di lavoro di analisi e creazione report.

### <a name="automated-patching"></a>Applicazione automatica delle patch

**Automated patching** è abilitata per impostazione predefinita. L'applicazione di patch automatizzata consente tooautomatically Azure patch per SQL Server e hello del sistema operativo. Specificare un giorno della settimana hello, ora e la durata di una finestra di manutenzione. Durante la finestra di manutenzione Azure esegue l'applicazione delle patch. pianificazione della finestra di manutenzione Hello Usa impostazioni locali VM hello per volta. Se si desidera tooautomatically Azure patch per SQL Server e hello del sistema operativo, fare clic su **disabilitare**.  

![Applicazione automatica delle patch di SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Backup automatico

Abilitare i backup automatici dei database per tutti i database in **Backup automatico**. L'opzione Backup automatico è disabilitata per impostazione predefinita.

Quando si abilita il backup automatizzato SQL, è possibile configurare l'esempio hello:

* Periodo di conservazione (giorni) per i backup
* Toouse di account di archiviazione per i backup
* Opzione di crittografia e password per i backup
* Backup dei database di sistema
* Pianificazione dei backup

backup, fare clic su hello tooencrypt **abilitare**. Specificare quindi hello **Password**. Azure crea un certificato di backup hello tooencrypt e utilizza hello specificato password tooprotect tale certificato.

![Backup automatico di SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Per altre informazioni, vedere [Backup automatizzato per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Integrazione dell'insieme di credenziali delle chiavi di Azure

i segreti toostore protezione in Azure per la crittografia, fare clic su **integrazione di Azure dell'insieme di credenziali chiave** e fare clic su **abilitare**.

![Integrazione dell'insieme di credenziali delle chiavi di Azure per SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Hello nella tabella seguente sono elencati hello parametri necessari tooconfigure integrazione dell'insieme di credenziali chiave di Azure.

| PARAMETRO | Descrizione | ESEMPIO |
| --- | --- | --- |
| **URL dell'insieme di credenziali delle chiavi** |percorso di Hello dell'insieme di credenziali chiave hello. |https://contosokeyvault.vault.azure.net/ |
| **Nome dell'entità** |Nome dell'entità servizio di Azure Active Directory. Questo nome viene inoltre hello tooas cui ID Client. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Segreto dell'entità** |Nome dell'entità servizio di Azure Active Directory. Il segreto è anche noto tooas hello segreto Client. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Nome credenziali** |**Nome delle credenziali**: integrazione AKV crea una credenziale all'interno di SQL Server, consentendo di hello VM toohave accesso toohello chiave dell'insieme di credenziali. Scegliere un nome per la credenziale. |mycred1 |

Per altre informazioni, vedere [Configurare l'integrazione dell'insieme di credenziali delle chiavi di Azure per SQL Server in macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).

### <a name="r-services"></a>Servizi R

Si dispone di hello opzione tooenable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx). In questo modo è analitica toouse avanzate con SQL Server 2016. Fare clic su **abilitare** su hello **impostazioni di SQL Server** finestra.

> [!NOTE]
> Per SQL Server 2016 Developer Edition, questa opzione è disabilitata in modo non corretto dal portale hello. Per tale edizione è necessario abilitare manualmente i servizi R dopo la creazione della VM.

![Abilitare i servizi R di SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

Al termine della configurazione delle impostazioni di SQL Server, fare clic su **OK**.

## <a name="5-review-hello-summary"></a>5. Riepilogo hello di revisione

In hello **riepilogo** , revisione hello riepilogo e fare clic su **acquisto** toocreate SQL Server, gruppo di risorse e le risorse specificate per questa macchina virtuale.

È possibile monitorare la distribuzione di hello da hello portale di Azure. Hello **notifiche** pulsante in alto hello hello consente di visualizzare lo stato di base della distribuzione hello.

> [!NOTE]
> tooprovide con un'idea generale sulla distribuzione di volte, una regione di Stati Uniti orientali toohello VM SQL è stato distribuito con le impostazioni predefinite. Distribuzione di questo test ha richiesto un totale di minuti 26 toocomplete. È possibile che i tempi di distribuzione specifici siano minori o maggiori in base all'area in cui ci si trova e alle impostazioni selezionate.

## <a name="open-hello-vm-with-remote-desktop"></a>Aprire hello VM con Desktop remoto

Utilizzare hello seguente macchina virtuale SQL Server passaggi tooconnect toohello con Desktop remoto:

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Dopo aver connesso toohello macchina virtuale di SQL Server, è possibile avviare SQL Server Management Studio e connettersi con l'autenticazione di Windows utilizzando le credenziali di amministratore locale. Se è abilitata l'autenticazione di SQL Server, è anche possibile connettersi con l'autenticazione di SQL con account di accesso SQL hello e la password configurati durante il provisioning.

Macchina toohello accesso consente di toodirectly modifica macchina e le impostazioni di SQL Server in base alle esigenze. Ad esempio, è Impossibile configurare le impostazioni del firewall hello o modificare le impostazioni di configurazione di SQL Server.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>Abilitare TCP/IP per le edizioni Developer ed Express

Durante il provisioning di una nuova macchina virtuale di SQL Server, Azure non si attiva automaticamente protocollo TCP/IP hello per le edizioni Express e SQL Server Developer Edition. passaggi Hello riportati di seguito viene illustrato come toomanually abilitare TCP/IP in modo che è possibile connettersi in remoto utilizzando un indirizzo IP.

Hello seguenti utilizzano **Gestione configurazione SQL Server** il protocollo TCP/IP hello tooenable per sviluppatori di SQL Server e le edizioni Express.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a>Connettersi tooSQL Server in modalità remota

In questa esercitazione, è selezionato **pubblica** accesso per la macchina virtuale hello e **autenticazione di SQL Server**. Queste connessioni impostazioni hello configurata automaticamente la macchina virtuale tooallow SQL Server da qualsiasi client tramite hello internet (presupponendo che dispongono di account di accesso SQL corretto hello).

> [!NOTE]
> Se non è stata selezionata pubblico durante il provisioning, è possibile modificare le impostazioni di connettività SQL tramite il portale di hello dopo il provisioning. Per altre informazioni, vedere la sezione su come [modificare le impostazioni di connettività di SQL](virtual-machines-windows-sql-connect.md#change).

Hello le sezioni seguenti Mostra come istanza di SQL Server tooyour tooconnect nella macchina virtuale da un altro computer tramite hello internet.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'utilizzo di SQL Server in Azure, vedere [SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md) hello e [domande frequenti su](virtual-machines-windows-sql-server-iaas-faq.md).

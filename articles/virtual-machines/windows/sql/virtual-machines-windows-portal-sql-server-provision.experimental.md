---
title: una macchina virtuale di SQL Server aaaProvision | Documenti Microsoft
description: "Creazione e la connessione macchina virtuale di SQL Server tooa in Azure utilizzando hello portale. In questa esercitazione Usa la modalità di gestione risorse di hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
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

In questa esercitazione end-to-end viene illustrato come toouse hello Azure Portal tooprovision una macchina virtuale che esegue SQL Server.

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

2. Nel portale di Azure hello, fare clic su **New**. viene visualizzato il portale di Hello hello **New** blade. risorse di macchina virtuale SQL Server Hello sono hello **calcolo** gruppo di hello Marketplace.
3. In hello **New** pannello, fare clic su **calcolo** e quindi fare clic su **tutti**.
4. In hello **filtro** testo Casella tipo di SQL Server, quindi premere INVIO hello.

   ![Pannello Macchine virtuali di Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Esaminare le immagini di SQL Server disponibili hello. Ogni immagine identifica una versione di SQL Server e un sistema operativo. 
6. Selezionare l'immagine di hello per sviluppatori di SQL Server 2016 SP1 in Windows Server 2016.

   > [!TIP]
   > edizione Developer Hello viene utilizzato in questa esercitazione perché è una versione completa di SQL Server che è disponibile per lo sviluppo ai fini del test. Si paga solo per il costo di hello di esecuzione hello macchina virtuale.

   > [!NOTE]
   > Le immagini VM SQL includono sui costi delle licenze hello per SQL Server in hello al minuto prezzi di hello macchina virtuale creata (ad eccezione di hello Developer ed Express Edition). SQL Server per sviluppatori è gratuito per sviluppo/test (non per la produzione), mentre SQL Express è gratuito per carichi di lavoro leggeri (inferiori a 1 GB di memoria e a 10 GB di archiviazione).
   > È presente un'altra opzione toobring-your-proprietari-licenza (BYOL) e pagare solo per hello macchina virtuale. Tali nomi di immagine hanno il prefisso {BYOL}. Per altre informazioni su queste opzioni, vedere [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Guida ai prezzi per le VM di SQL Server in Azure).

7. In **Selezionare un modello di distribuzione** assicurarsi che l'opzione **Resource Manager** sia selezionata. Gestione risorse è hello consigliata il modello di distribuzione per le nuove macchine virtuali. Fare clic su **Crea**.

    ![Creare VM di SQL con Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Configurare hello VM
Sono disponibili cinque pannelli per la configurazione di una macchina virtuale di SQL Server.

| Passaggio | Descrizione |
| --- | --- |
| **Nozioni di base** |[Configurare le impostazioni di base](#1-configure-basic-settings) |
| **Dimensione** |[Scegliere le dimensioni della macchina virtuale](#2-choose-virtual-machine-size) |
| **Impostazioni** |[Configurare le funzionalità facoltative](#3-configure-optional-features) |
| **Impostazioni di SQL Server** |[Configurare le impostazioni di SQL Server](#4-configure-sql-server-settings) |
| **Riepilogo** |[Riepilogo hello di revisione](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Configurare le impostazioni di base
In hello **nozioni di base** pannello fornire hello le seguenti informazioni:

* Immettere un **Nome**univoco per la macchina virtuale.
* Specificare un **nome utente** per account di amministratore locale hello in hello macchina virtuale. Questo account viene aggiunto anche SQL Server toohello **sysadmin** ruolo predefinito del server.
* Specificare una **Password**complessa.
* Se si dispone di più sottoscrizioni, verificare che sia corretta per la sottoscrizione hello hello nuova macchina virtuale.
* In hello **gruppo di risorse** , digitare un nome per un nuovo gruppo di risorse. In alternativa, di scegliere un gruppo di risorse esistente di toouse **utilizzare esistente**. Un gruppo di risorse è una raccolta di risorse correlate in Azure, ovvero macchine virtuali, account di archiviazione, reti virtuali e così via.
  
  > [!NOTE]
  > L'uso di un nuovo gruppo di risorse risulta utile se si stanno solo eseguendo test o se si sta iniziando a usare le distribuzioni di SQL Server in Azure. Dopo aver completato il test, eliminare hello risorsa gruppo tooautomatically delete hello VM e tutte le risorse associate a tale gruppo di risorse. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).
  > 
  > 
* Selezionare una **Località** per la distribuzione.
* Fare clic su **OK** impostazioni hello toosave.
  
    ![Pannello Informazioni di base di SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Scegliere le dimensioni della macchina virtuale
In hello **dimensioni** passaggio, scegliere una dimensione di macchina virtuale in hello **scegliere una dimensione** blade. Pannello Hello vengono inizialmente visualizzate le dimensioni delle macchine consigliati in base a hello l'immagine selezionata.

> [!IMPORTANT]
> Hello stimato il costo mensile visualizzato su hello **scegliere una dimensione** blade non include i costi di licenza di SQL Server. Questo costo mensile stimato è il costo di hello di hello VM autonoma. Per hello Express e Developer Edition di SQL Server, si tratta di costo stimato totale hello. Per altre edizioni, vedere hello [pagina dei prezzi delle macchine virtuali di Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) e selezionare l'edizione di destinazione di SQL Server. Vedere anche hello [prezzi linee guida per le macchine virtuali di SQL Server Azure](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opzioni per le dimensioni di VM di SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Per carichi di lavoro di produzione, è consigliabile selezionare dimensioni della macchina virtuale che supportino [Archiviazione Premium](../../../storage/storage-premium-storage.md). Se non si richiede che il livello di prestazioni, utilizzare hello **visualizzare tutti** pulsante che mostra tutte le opzioni di dimensioni di macchina. Ad esempio, è possibile usare dimensioni di macchine virtuali minori per un ambiente di sviluppo o di test.

> [!NOTE]
> Per altre informazioni sulle dimensioni di macchine virtuali, vedere [Dimensioni delle macchine virtuali](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Per considerazioni sulle dimensioni della VM di SQL Server, vedere [Procedure consigliate per le prestazioni per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).

Scegliere le dimensioni della macchina virtuale e quindi fare clic su **Seleziona**.

## <a name="3-configure-optional-features"></a>3. Configurare le funzionalità facoltative
In hello **impostazioni** pannello, configurare l'archiviazione di Azure, servizi di rete e il monitoraggio per la macchina virtuale hello.

* In **Archiviazione** specificare un **Tipo di disco**, ad esempio Standard o Premium (unità SSD). Archiviazione Premium è l'impostazione consigliata per i carichi di lavoro di produzione.

> [!NOTE]
> Se si seleziona l'opzione Premium (SSD) per dimensioni della macchina virtuale che non supportano l'Archiviazione Premium, le dimensioni della macchina virtuale vengono modificate automaticamente.  
> 
> 

* In **account di archiviazione**, è possibile accettare il nome di account di hello automaticamente eseguito il provisioning di archiviazione. È anche possibile fare clic su **account di archiviazione** toochoose esistente dell'account e configurare il tipo di account di archiviazione hello. Per impostazione predefinita, Azure crea un nuovo account di archiviazione con archiviazione con ridondanza locale. Per altre informazioni sulle opzioni di archiviazione, vedere [Replica di Archiviazione di Azure](../../../storage/storage-redundancy.md).
* In **rete**, è possibile accettare i valori hello popolato automaticamente. È anche possibile fare clic su ogni funzionalità toomanually configurare hello **rete virtuale**, **Subnet**, **indirizzo IP pubblico**, e **gruppodisicurezzadirete**. Per motivi di hello di questa esercitazione, mantenere i valori predefiniti di hello.
* Abilita Azure **monitoraggio** per impostazione predefinita con hello stesso account di archiviazione designato per hello macchina virtuale. Queste impostazioni possono essere modificate qui, se necessario.
* In **Set di disponibilità**specificare un set di disponibilità. Ai fini di hello di questa esercitazione, è possibile selezionare **Nessuno**. Se si prevede di tooset i gruppi di disponibilità AlwaysOn SQL, configurare hello disponibilità tooavoid ricrea hello macchina virtuale.  Per ulteriori informazioni, vedere [Gestisci hello disponibilità delle macchine virtuali](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Al termine della configurazione di queste impostazioni, fare clic su **OK**.

## <a name="4-configure-sql-server-settings"></a>4. Configurare le impostazioni di SQL Server
In hello **impostazioni di SQL Server** pannello, configurare impostazioni specifiche e le ottimizzazioni per SQL Server. le impostazioni di Hello che è possibile configurare per SQL Server includono hello seguenti impostazioni.

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

tooconnect tooSQL Server tramite hello internet, è anche necessario abilitare l'autenticazione di SQL Server, descritto nella sezione successiva hello.

> [!NOTE]
> Si è tooadd possibili ulteriori restrizioni per tooyour le comunicazioni di rete hello macchina virtuale SQL Server. Dopo la creazione di hello VM, è possibile aggiungere ulteriori restrizioni da hello Modifica gruppo di sicurezza di rete. Per ulteriori informazioni, vedere [Che cos'è un gruppo di sicurezza di rete](../../../virtual-network/virtual-networks-nsg.md)
> 
> 

Se si preferisce toonot abilitare connessioni toohello motore di Database tramite hello internet, scegliere una delle seguenti opzioni hello:

* **Locale (all'interno di VM)** tooallow connessioni tooSQL Server solo da all'interno di hello macchina virtuale.
* **Private (all'interno di rete virtuale)** tooallow connessioni tooSQL Server da computer o i servizi in hello stessa rete virtuale.

> [!NOTE]
> immagine di macchina virtuale Hello per SQL Server Express edition non abilita il protocollo TCP/IP hello automaticamente. Questo vale anche per hello connettività privati e pubblici opzioni. Per l'edizione Express, è necessario utilizzare Gestione configurazione SQL Server troppo[abilitare manualmente il protocollo TCP/IP hello](#configure-sql-server-to-listen-on-the-tcp-protocol) dopo la creazione di hello macchina virtuale.
> 
> 

Migliorare la sicurezza in generale, scegliendo la connettività di più restrittiva di hello, lo scenario lo consente. Tuttavia, tutte le opzioni di hello sono entità a protezione diretta tramite regole del gruppo di sicurezza di rete e l'autenticazione di Windows/SQL.

**Porta** too1433 predefinite. ma è possibile specificare un numero di porta diverso.
Per ulteriori informazioni, vedere [connettersi tooa macchina virtuale di SQL Server (gestione delle risorse) | Microsoft Azure](virtual-machines-windows-sql-connect.md).

### <a name="authentication"></a>Autenticazione
Se è necessaria l'autenticazione di SQL Server, fare clic su **Abilita** under **Autenticazione SQL**.

![Autenticazione di SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Se si prevede di SQL Server tooaccess su hello internet (vale a dire hello opzioni di connettività pubblico), è necessario abilitare l'autenticazione di SQL qui. Accesso pubblico toohello SQL Server richiede l'uso di hello di autenticazione di SQL Server.
> 
> 

Se si abilita l'autenticazione di SQL Server, specificare un **Nome di accesso** e una **Password**. Questo nome utente è configurato come account di accesso di autenticazione di SQL Server e un membro di hello **sysadmin** ruolo predefinito del server. Per altre informazioni sulle modalità di autenticazione, vedere [Scegliere una modalità di autenticazione](http://msdn.microsoft.com/library/ms144284.aspx).

Se non si abilita l'autenticazione di SQL Server, è possibile utilizzare account di amministratore locale hello nell'istanza di SQL Server toohello tooconnect VM hello.

### <a name="storage-configuration"></a>Configurazione dell'archiviazione
Fare clic su **configurazione dell'archiviazione** toospecify i requisiti di archiviazione hello.

![Configurazione dell'archiviazione SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Se è stata selezionata l'archiviazione Standard, questa opzione non è disponibile. L'ottimizzazione automatica delle risorse di archiviazione è disponibile solo per l'Archiviazione Premium.
> 
> 

È possibile specificare requisiti come operazioni di I/O al secondo, velocità effettiva in Mbps e dimensioni di archiviazione totali. Configurare questi valori con scale estendibile hello. portale Hello calcola automaticamente il numero di hello di dischi in base a questi requisiti.

Per impostazione predefinita, Azure Ottimizza l'archiviazione di hello per 5000 IOPs, 200 MB e 1 TB di spazio di archiviazione. È possibile modificare queste impostazioni di archiviazione in base al carico di lavoro. In **archiviazione ottimizzata per**, selezionare una delle seguenti opzioni hello:

* **Generale** è l'impostazione predefinita hello e supporta la maggior parte dei carichi di lavoro.
* **Transazionale** elaborazione Ottimizza l'archiviazione di hello per carichi di lavoro OLTP database tradizionale.
* **Il data warehousing** Ottimizza l'archiviazione di hello per carichi di lavoro di analisi e creazione report.

> [!NOTE]
> i limiti superiori di Hello in dispositivi di scorrimento hello variano a seconda le dimensioni di macchina virtuale selezionata.
> 
> 

### <a name="automated-patching"></a>Applicazione automatica delle patch
**Automated patching** è abilitata per impostazione predefinita. L'applicazione di patch automatizzata consente tooautomatically Azure patch per SQL Server e hello del sistema operativo. Specificare un giorno della settimana hello, ora e la durata di una finestra di manutenzione. Durante la finestra di manutenzione Azure esegue l'applicazione delle patch. pianificazione della finestra di manutenzione Hello Usa impostazioni locali VM hello per volta. Se si desidera tooautomatically Azure patch per SQL Server e hello del sistema operativo, fare clic su **disabilitare**.  

![Applicazione automatica delle patch di SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Backup automatico
Abilitare i backup automatici dei database per tutti i database in **Backup automatico**. L'opzione Backup automatico è disabilitata per impostazione predefinita.

Quando si abilita il backup automatizzato SQL, è possibile configurare hello seguenti impostazioni:

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

Al termine della configurazione delle impostazioni di SQL Server, fare clic su **OK**.

### <a name="r-services"></a>Servizi R
È possibile abilitare i [Servizi R per SQL Server](https://msdn.microsoft.com/library/mt604845.aspx). SQL Server R Services consente analitica toouse avanzate con SQL Server 2016. Fare clic su **abilitare** su hello **impostazioni di SQL Server** blade.

![Abilitare i servizi R di SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a>5. Riepilogo hello di revisione
In hello **riepilogo** pannello revisione hello riepilogo e fare clic su **OK** toocreate SQL Server, gruppo di risorse e le risorse specificate per questa macchina virtuale.

È possibile monitorare la distribuzione di hello dal portale di azure hello. Hello **notifiche** pulsante in alto hello hello consente di visualizzare lo stato di base della distribuzione hello.

> [!NOTE]
> tooprovide con un'idea generale sulla distribuzione di volte, una regione di Stati Uniti orientali toohello VM SQL è stato distribuito con le impostazioni predefinite. Distribuzione di questo test ha richiesto un totale di minuti 26 toocomplete. È possibile che i tempi di distribuzione specifici siano minori o maggiori in base all'area in cui ci si trova e alle impostazioni selezionate.
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a>Aprire hello VM con Desktop remoto
Utilizzare hello seguendo i passaggi tooconnect toohello la macchina virtuale con Desktop remoto:

1. Dopo la macchina virtuale di Azure viene compilato, hello icona hello per hello VM viene visualizzato nel dashboard di Azure. È possibile trovarla anche esplorando le macchine virtuali esistenti. Fare clic sulla nuova macchina virtuale di SQL. I relativi dettagli vengono visualizzati nel pannello **Macchina virtuale** .
2. Nella parte superiore di hello di hello **macchina virtuale** pannello, fare clic su **Connetti**.
3. browser Hello scarica un file RDP per hello macchina virtuale. File RDP hello aperto.
    ![TooSQL Desktop remoto macchina virtuale](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)
4. Hello connessione Desktop remoto che informa che hello Impossibile identificare l'autore della connessione remota. Fare clic su **Connetti** toocontinue.
5. In hello **la sicurezza di Windows** finestra di dialogo, fare clic su **utilizza un altro account**.
6. Per **nome utente** tipo  **\<nome utente >**, dove <user name> è il nome utente di hello specificato quando è stato configurato hello macchina virtuale. È necessario tooadd una barra rovesciata iniziale prima del nome hello.
7. Hello tipo **Password** precedentemente configurato per questa macchina virtuale e quindi fare clic su **OK** tooconnect.
8. Se un altro **connessione Desktop remoto** finestra di dialogo viene chiesto se tooconnect, fare clic su **Sì**.

Dopo aver connesso toohello macchina virtuale di SQL Server, è possibile avviare SQL Server Management Studio e connettersi con l'autenticazione di Windows utilizzando le credenziali di amministratore locale. Se è abilitata l'autenticazione di SQL Server, è anche possibile connettersi con l'autenticazione di SQL con account di accesso SQL hello e la password configurati durante il provisioning.

Macchina toohello accesso consente di toodirectly modifica macchina e le impostazioni di SQL Server in base alle esigenze. Ad esempio, è Impossibile configurare le impostazioni del firewall hello o modificare le impostazioni di configurazione di SQL Server.

## <a name="connect-toosql-server-remotely"></a>Connettersi tooSQL Server in modalità remota
In questa esercitazione, è selezionato **pubblica** accesso per la macchina virtuale hello e **autenticazione di SQL Server**. Queste connessioni impostazioni hello configurata automaticamente la macchina virtuale tooallow SQL Server da qualsiasi client tramite hello internet (presupponendo che dispongono di account di accesso SQL corretto hello).

> [!NOTE]
> Se non è stata selezionata pubblico durante il provisioning, ulteriori passaggi sono necessari tooaccess l'istanza di SQL Server su hello internet. Per ulteriori informazioni, vedere [connessione macchina virtuale SQL Server tooa](virtual-machines-windows-sql-connect.md).
> 
> 

Hello le sezioni seguenti Mostra come istanza di SQL Server tooyour tooconnect nella macchina virtuale da un altro computer tramite hello internet.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'utilizzo di SQL Server in Azure, vedere [SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md) hello e [domande frequenti su](virtual-machines-windows-sql-server-iaas-faq.md).

Per una panoramica video di SQL Server in macchine virtuali di Azure, eseguire il controllo [macchina virtuale di Azure è migliore piattaforma di hello per SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).

[Esplorare hello percorso di apprendimento](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server in macchine virtuali di Azure.


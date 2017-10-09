---
title: aaaOverview di SQL Server in macchine virtuali di Azure | Documenti Microsoft
description: Informazioni su come toorun completo edizioni di SQL Server in macchine virtuali di Azure. Ottenere le immagini di macchina virtuale SQL Server tooall di collegamenti diretti e del relativo contenuto.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Panoramica di SQL Server in macchine virtuali di Azure
In questo argomento vengono descritte le opzioni per l'esecuzione di SQL Server in macchine virtuali di Azure (VM), insieme a [Collega immagini tooportal](#option-1-create-a-sql-vm-with-per-minute-licensing) e una panoramica della [comuni](#manage-your-sql-vm).

> [!NOTE]
> Se si ha già familiarità con SQL Server e si desidera toosee toodeploy una macchina virtuale di SQL Server, vedere [il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Panoramica
Se sei un amministratore del database o uno sviluppatore, macchine virtuali di Azure forniscono un toomove modo il toohello on-premise SQL Server i carichi di lavoro e le applicazioni Cloud. Hello seguente video viene fornita una panoramica tecnica di macchine virtuali di Azure di SQL Server.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Hello video vengono illustrate hello seguenti aree:

| Tempo | Area |
| --- | --- |
| 00:21 |Informazioni sulle VM di Azure |
| 01:45 |Sicurezza |
| 02:50 |Connettività |
| 03:30 |Affidabilità e prestazioni delle risorse di archiviazione |
| 05:20 |Dimensioni delle macchine virtuali |
| 05:54 |Disponibilità elevata e contratto di servizio |
| 07:30 |Supporto per la configurazione |
| 08:00 |Monitoraggio |
| 08:32 |Demo: creare una VM di SQL Server 2016 |

> [!NOTE]
> Hello video è incentrato su SQL Server 2016, ma Azure offre immagini di macchina virtuale per molte versioni di SQL Server, tra cui 2012, 2014 e 2016. 
> 
> 

## <a name="scenarios"></a>Scenari
Vi sono molti i motivi che è possibile scegliere toohost i dati in Azure. Se l'applicazione viene spostato tooAzure, è possibile migliorare le prestazioni tooalso spostare hello i dati. Esistono tuttavia altri vantaggi. Si dispone automaticamente di centri dati toomultiple di accesso per un ripristino di emergenza e presenza globale. dati Hello sono estremamente sicuro e durevole.

L'esecuzione di SQL Server in una VM di Azure costituisce un'opzione per archiviare i dati relazionali in Azure. È ideale per scenari diversi. Ad esempio, è consigliabile tooconfigure hello macchina virtuale di Azure come Analogamente come computer di SQL Server on-premise tooan possibili. È necessario toorun applicazioni e servizi aggiuntivi su hello stesso server di database. Esistono due risorse principali che consentono di valutare altri scenari e considerazioni:

* [SQL Server in macchine virtuali di Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/) viene fornita una panoramica degli scenari di hello migliore per l'utilizzo di SQL Server nelle macchine virtuali di Azure. 
* [Scegliere un'opzione di SQL Server cloud: database SQL di Azure (PaaS) o SQL Server in VM di Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) offre un confronto dettagliato tra database SQL ed esecuzione di SQL Server in una VM.

## <a name="create-a-new-sql-vm"></a>Creare una nuova VM di SQL
Hello sezioni seguenti forniscono collegamenti diretti toohello portale di Azure per le immagini della raccolta di macchina virtuale SQL Server hello. A seconda di hello l'immagine selezionata, è possibile entrambi pagare i costi di licenza di SQL Server in base al minuto, oppure è possibile trasferire la propria licenza (BYOL).

Trovare istruzioni dettagliate per la creazione di una nuova VM SQL in esercitazione hello [il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Inoltre, esaminare hello [procedure consigliate per le macchine virtuali di SQL Server](virtual-machines-windows-sql-performance.md), che illustra come un computer appropriato dallo hello tooselect dimensione e altre funzionalità disponibile durante il provisioning.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Opzione 1: Creare una VM di SQL con una licenza al minuto
Hello nella tabella seguente fornisce una matrice di immagini di SQL Server più recente di hello nella raccolta di macchine virtuali hello. Fare clic su qualsiasi toobegin di collegamento, creazione di una nuova VM SQL con la versione specificata, l'edizione e del sistema operativo. 

> [!TIP]
> hello toounderstand VM e prezzi di SQL per queste immagini, vedere [prezzi linee guida per le macchine virtuali di SQL Server Azure](virtual-machines-windows-sql-server-pricing-guidance.md).

| Versione | Sistema operativo | Edizione |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Elenco toothis, altre combinazioni di versioni di SQL Server e sistemi operativi sono inoltre disponibili. Trovare altre immagini tramite una ricerca di marketplace in hello portale di Azure. 

## <a id="BYOL"></a>Opzione 2: Creare una VM di SQL con una licenza esistente
È anche possibile scegliere l'opzione Bring Your Own License (BYOL). In questo scenario, si paga solo per hello VM senza costi aggiuntivi per le licenze di SQL Server. toouse la propria licenza, usare una matrice di hello di versioni di SQL Server, edizioni e i sistemi operativi seguenti. Nel portale di hello, questi nomi di immagine sono preceduti **{BYOL}**.

> [!TIP]
> L'opzione Bring Your Own License consente di risparmiare denaro nel tempo per i carichi di lavoro di produzione continui. Per altre informazioni, vedere [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Guida ai prezzi per le VM di SQL Server in Azure).

| Versione | Sistema operativo | Edizione |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Elenco toothis, altre combinazioni di versioni di SQL Server e sistemi operativi sono inoltre disponibili. Trovare altre immagini tramite una ricerca di marketplace in hello del portale di Azure (ricerca di "{BYOL} SQL Server").

> [!IMPORTANT]
> le immagini VM BYOL toouse, è necessario disporre di un contratto Enterprise Agreement con [mobilità delle licenze tramite Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). È inoltre necessaria una licenza valida per hello versione o edizione di SQL Server si desidera toouse. È necessario [fornire hello necessarie BYOL informazioni tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) all'interno di **10** giorni del provisioning di una macchina virtuale. 

> [!NOTE]
> Non è possibile toochange hello licenze della propria licenza di modello di toouse di macchina virtuale SQL Server un pagamento al minuto. In questo caso, è necessario creare una nuova VM BYOL e toohello il database di eseguire la migrazione nuova macchina virtuale. 

## <a name="manage-your-sql-vm"></a>Gestire la VM di SQL
Dopo il provisioning della VM di SQL Server, è possibile eseguire diverse attività di gestione facoltative. Per molti aspetti, la configurazione e la gestione di SQL Server sono identiche alla gestione di un'istanza di SQL Server locale. Tuttavia, alcune attività sono tooAzure specifico. Hello nelle sezioni seguenti vengono illustrano alcune di queste aree con informazioni toomore collegamenti.

### <a name="connect-toohello-vm"></a>Connettersi toohello VM
Una delle operazioni di gestione più semplice hello è tooconnect tooyour macchina virtuale SQL Server tramite gli strumenti, ad esempio SQL Server Management Studio (SSMS). Per istruzioni su come tooconnect tooyour nuovo Server SQL di macchina virtuale, vedere [connessione macchina virtuale di SQL Server in Azure tooa](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Migrare i dati
Se si dispone di un database esistente, è opportuno toomove che toohello appena effettuato il provisioning SQL VM. Per un elenco di opzioni di migrazione e istruzioni, vedere [la migrazione di un Server in una macchina virtuale Azure di tooSQL Database](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Configurare la disponibilità elevata
Se è necessaria la disponibilità elevata, è consigliabile configurare i gruppi di disponibilità di SQL Server. Ciò comporta più macchine virtuali di Azure in una rete virtuale. Hello portale di Azure dispone di un modello che consente di impostare questa configurazione. Per altre informazioni, vedere [Configurare automaticamente il gruppo di disponibilità AlwaysOn in macchine virtuali di Azure con Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Se si desidera toomanually configurare il gruppo di disponibilità e listener associati, vedere [configurare gruppi di disponibilità AlwaysOn nella macchina virtuale di Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Per ulteriori informazioni sulla disponibilità elevata, vedere [disponibilità elevata e ripristino di emergenza di SQL Server in macchine virtuali Azure](virtual-machines-windows-sql-high-availability-dr.md).

### <a name="back-up-your-data"></a>Eseguire il backup dei dati
Macchine virtuali di Azure possono sfruttare [Backup automatizzato](virtual-machines-windows-sql-automated-backup.md), che consente di creare regolarmente i backup dello spazio di archiviazione tooblob database. È anche possibile usare questa tecnica manualmente. Per altre informazioni, vedere [Usare Archiviazione di Azure per il backup e il ripristino di SQL Server](virtual-machines-windows-use-storage-sql-server-backup-restore.md). Per una panoramica di tutte le opzioni di backup e ripristino, vedere [Backup e ripristino per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md).

### <a name="automate-updates"></a>Automatizzare gli aggiornamenti
Macchine virtuali di Azure è possono utilizzare [patch automatizzate](virtual-machines-windows-sql-automated-patching.md) tooschedule una finestra di manutenzione per l'installazione importanti di windows e SQL Server viene aggiornato automaticamente.

### <a name="customer-experience-improvement-program-ceip"></a>Analisi utilizzo software
Hello analisi utilizzo software (CEIP) è abilitato per impostazione predefinita. Questo periodicamente invia report tooMicrosoft toohelp miglioramento di SQL Server. Vi è nessuna attività di gestione richiesta con analisi utilizzo software, a meno che non si desidera toodisable dopo il provisioning. È possibile personalizzare o disattivare Analisi utilizzo software hello connettendosi toohello VM con desktop remoto. Eseguire quindi hello **segnalazione errori di SQL Server e utilizzo** utilità. Seguire hello istruzioni toodisable reporting. 

Per ulteriori informazioni, vedere la sezione Analisi utilizzo software di hello hello [condizioni di licenza](https://msdn.microsoft.com/library/ms143343.aspx) argomento. 

## <a name="next-steps"></a>Passaggi successivi

Per domande sui prezzi, vedere [prezzi linee guida per le macchine virtuali di SQL Server Azure](virtual-machines-windows-sql-server-pricing-guidance.md) hello e [pagina dei prezzi Azure](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Selezionare l'edizione di destinazione di SQL Server in hello **del sistema operativo e Software** elenco. Quindi visualizzare i prezzi hello per le macchine virtuali diverse dimensioni.

Per altre domande, In primo luogo, vedere hello [SQL Server in domande frequenti su macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-faq.md). Ma anche di aggiungere le domande o commenti toohello nella parte inferiore di qualsiasi toointeract argomenti SQL VM con la community di Microsoft e hello.

---
title: Domande frequenti su SQL Server in macchine virtuali di Microsoft Azure| Microsoft Docs
description: Questo articolo offre risposta ad alcune domande frequenti sull'esecuzione di SQL Server in macchine virtuali di Azure.
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: troubleshooting
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 12/14/2017
ms.author: v-shysun
ms.openlocfilehash: 141dd1fe9e727f430b7c45dbb798f5471167c355
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-windows-azure-virtual-machines"></a>Domande frequenti su SQL Server in macchine virtuali di Microsoft Azure

> [!div class="op_single_selector"]
> * [Windows](virtual-machines-windows-sql-server-iaas-faq.md)
> * [Linux](../../linux/sql/sql-server-linux-faq.md)

In questo articolo vengono fornite le risposte ad alcune delle domande più comuni sull'esecuzione [SQL Server in macchine virtuali di Windows Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

> [!NOTE]
> Questo articolo illustra i problemi specifici di SQL Server in macchine virtuali di Windows. Se si esegue SQL Server in macchine virtuali Linux, vedere le [domande frequenti su Linux](../../linux/sql/sql-server-linux-faq.md).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a id="images"></a>Immagini

1. **Le immagini della raccolta macchina virtuale SQL Server sono disponibili?**

   Azure gestisce le immagini di macchina virtuale per tutte le versioni principali supportate di SQL Server in tutte le edizioni di Windows e Linux. Per ulteriori informazioni, vedere l'elenco completo dei [immagini di macchina virtuale Windows](virtual-machines-windows-sql-server-iaas-overview.md#payasyougo) e [immagini VM Linux](../../linux/sql/sql-server-linux-virtual-machines-overview.md#create).

1. **Immagini della raccolta macchina virtuale SQL Server esistenti vengono aggiornate?**

   Ogni due mesi, le immagini di SQL Server in una raccolta di macchine virtuali vengono aggiornate con le più recenti di Windows e Linux Aggiorna. Per le immagini Windows, include tutti gli aggiornamenti che sono contrassegnati come importanti in Windows Update, inclusi gli aggiornamenti di sicurezza di SQL Server importanti e service pack. Per le immagini Linux, include gli aggiornamenti più recenti del sistema. Gli aggiornamenti cumulativi di SQL Server vengono gestiti in modo diverso per Linux e Windows. Per Linux, gli aggiornamenti cumulativi di SQL Server sono inoltre inclusi nell'aggiornamento. Ma in questo momento, le macchine virtuali di Windows non vengono aggiornate con gli aggiornamenti cumulativi di SQL Server o Windows Server.

1. **Immagini di macchina virtuale di SQL Server possono ottenere rimosso dalla raccolta?**

   Sì. Azure gestisce solo un'immagine per ogni versione principale e l'edizione. Ad esempio, quando viene rilasciato un nuovo service pack di SQL Server, Azure aggiunge una nuova immagine per la raccolta per il service pack. L'immagine di SQL Server per il service pack precedente viene rimosso immediatamente dal portale di Azure. Tuttavia, è ancora disponibile per il provisioning di PowerShell per i successivi tre mesi. Dopo tre mesi, l'immagine precedente del Service pack non è più disponibile. Questi criteri di rimozione sono applicabile anche se una versione di SQL Server diventa non supportata quando viene raggiunta la fine del ciclo di vita.

1. **È possibile impostare configurazioni non visualizzate nella raccolta di macchine virtuali, ad esempio Windows 2008 R2 + SQL Server 2012?**

   di serie Per le raccolte di macchine virtuali che includono SQL Server è necessario selezionare una delle immagini disponibili.

## <a name="creation"></a>Creazione

1. **Come si crea una macchina virtuale di Azure con SQL Server?**

   La soluzione più semplice consiste nel creare una macchina virtuale che include SQL Server. Per un'esercitazione sull'iscrizione ad Azure e la creazione di una VM SQL dal portale, vedere [il provisioning di una macchina virtuale di SQL Server nel portale di Azure](virtual-machines-windows-portal-sql-server-provision.md). È possibile selezionare un'immagine di macchina virtuale che utilizza la licenza di SQL Server con costo al minuto oppure usare un'immagine che consente di trasferire la licenza di SQL Server dell'utente. È anche possibile installare manualmente in una macchina virtuale un'edizione di SQL Server con licenza gratuita (Developer o Express) o riutilizzando una licenza locale. Se si usa la funzionalità Bring Your Own License, è necessario avere [Mobilità delle licenze tramite Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). Per altre informazioni, vedere [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Guida ai prezzi per le VM di SQL Server in Azure).

1. **Come si esegue la migrazione di un database SQL Server locale nel cloud?**

   Creare prima una macchina virtuale di Azure con un'istanza di SQL Server, quindi eseguire la migrazione dei database locali in tale istanza. Per alcune strategie di migrazione dei dati, vedere [Eseguire la migrazione di un database di SQL Server a SQL Server in una macchina virtuale di Azure](virtual-machines-windows-migrate-sql.md).

## <a name="licensing"></a>Licenze

1. **Come si installa una copia di SQL Server con licenza in una VM di Azure?**

   Per eseguire questa operazione è possibile procedere in due modi: È possibile eseguire il provisioning di una delle [immagini di macchine virtuali che supporta le licenze](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Un'altra possibilità consiste nel copiare il supporto di installazione di SQL Server in una VM Windows Server, quindi installare SQL Server nella VM. Per motivi di licenza, è necessario avere [Mobilità delle licenze tramite Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). Per altre informazioni, vedere [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Guida ai prezzi per le VM di SQL Server in Azure).

1. **È possibile modificare una VM per l'uso di una licenza di SQL Server, se è stata creata da una delle immagini della raccolta con pagamento in base al consumo?**

   di serie Non è possibile passare dalla licenza con costo al minuto all'uso della propria licenza. Creare una nuova macchina virtuale di Azure usando una delle [immagini BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL) e quindi migrare i database nel nuovo server utilizzando le [tecniche di migrazione dei dati](virtual-machines-windows-migrate-sql.md) standard.

1. **È necessario pagare la licenza di SQL Server in una VM di Azure se viene utilizzata solo per standby/failover?**

   Se è disponibile Software Assurance e si usa la mobilità delle licenze come descritto in [Domande frequenti sulle licenze di Macchine virtuali](http://azure.microsoft.com/pricing/licensing-faq/), non è necessario pagare la licenza per un'istanza di SQL Server che funge da replica secondaria passiva in una distribuzione a disponibilità elevata. In caso contrario, è necessario pagare la licenza.


## <a name="administration"></a>Administration

1. **È possibile installare una seconda istanza di SQL Server nella stessa VM? È possibile modificare le funzionalità installate nell'istanza predefinita?**

   Sì. Il supporto di installazione di SQL Server si trova in una cartella nell'unità **C** . Eseguire **Setup.exe** da tale percorso per aggiungere nuove istanze di SQL Server o per modificare altre funzionalità di SQL Server installate nella macchina virtuale. Si noti che alcune funzionalità, ad esempio Backup automatizzato, Applicazione automatica delle patch e Integrazione di Azure Key Vault, funzionano solo nell'istanza predefinita.

1. **È possibile disinstallare l'istanza predefinita di SQL Server?**

   Sì. Sono tuttavia necessarie alcune considerazioni. Come indicato nella risposta precedente, le funzionalità che si basano sull'[estensione SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md) funzionano solo nell'istanza predefinita. Se si disinstalla l'istanza predefinita, l'estensione continua a cercarla e può generare errori del log eventi. Questi errori hanno le due origini seguenti: **Microsoft SQL Server Credential Management** e **Microsoft SQL Server IaaS Agent**. Uno degli errori potrebbe essere simile al seguente:

      Si è verificato un errore di rete o specifico dell'istanza mentre veniva stabilita la connessione a SQL Server. Il server non è stato trovato o non è accessibile.

   Se si decide di disinstallare l'istanza predefinita, disinstallare anche l'[estensione SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).
   
   >[!NOTE]
   >Una macchina virtuale di SQL Server Azure viene fatturata come descritto in [Guida ai prezzi per le VM di SQL Server in Azure](virtual-machines-windows-sql-server-pricing-guidance.md). Se si rimuove SQL Server, gli addebiti per l'utilizzo continuano. Se SQL Server non è più necessario, è possibile distribuire una nuova macchina virtuale ed eseguire la migrazione di dati e applicazioni alla nuova macchina virtuale. Sarà quindi possibile rimuovere la macchina virtuale di SQL Server.

## <a name="updating-and-patching"></a>L'aggiornamento e l'applicazione di patch

1. **Come si esegue l'aggiornamento a una nuova versione o a una nuova edizione di SQL Server in una VM di Azure?**

   Attualmente non è disponibile alcun aggiornamento sul posto per SQL Server in esecuzione in una VM di Azure. Creare una nuova macchina virtuale di Azure con la versione o l'edizione di SQL Server voluta, quindi eseguire la migrazione dei database nel nuovo server tramite [tecniche di migrazione dati](virtual-machines-windows-migrate-sql.md) standard.

1. **Come si applicano gli aggiornamenti e i Service Pack a una VM di SQL Server?**

   Le macchine virtuali consentono di controllare il computer host e di decidere quindi quando e come applicare gli aggiornamenti. Per il sistema operativo, è possibile applicare manualmente gli aggiornamenti di Windows oppure abilitare un servizio di pianificazione definito [Applicazione automatica delle patch](virtual-machines-windows-sql-automated-patching.md). Applicazione automatica delle patch installa tutti gli aggiornamenti contrassegnati come importanti, inclusi gli aggiornamenti di SQL Server in tale categoria. Gli aggiornamenti facoltativi di SQL Server devono essere installati manualmente.

## <a name="general"></a>Generale

1. **Le istanze del cluster di failover di SQL Server sono supportate nelle macchine virtuali di Azure?**

   Sì. È possibile [creare un cluster di failover di Windows in Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) e usare Spazi di archiviazione diretta (S2D) per l'archiviazione del cluster. In alternativa, è possibile usare soluzioni di clustering o archiviazione di terze parti come descritto in [Disponibilità elevata e ripristino di emergenza per SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Qual è la differenza tra VM di SQL Server e servizio Database SQL?**

   Dal punto di vista concettuale l'esecuzione di SQL Server in una macchina virtuale di Azure non è diversa dall'esecuzione di SQL Server in un centro dati remoto. Per contro, il servizio [Database SQL](../../../sql-database/sql-database-technical-overview.md) offre una soluzione DaaS (Database-as-a-service). Con Database SQL non si ha accesso ai computer che ospitano i database. Per un confronto completo, vedere [Scegliere un'opzione di SQL Server cloud: database SQL di Azure (PaaS) o SQL Server in VM di Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Come si installa SQL Server Data Tools in una VM di Azure?**

    Scaricare e installare SQL Server Data Tools da [Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Risorse

**Macchine virtuali Windows**:

* [Panoramica di SQL Server in una macchina virtuale Windows](virtual-machines-windows-sql-server-iaas-overview.md).
* [Effettuare il provisioning di una macchina virtuale Windows di SQL Server](virtual-machines-windows-portal-sql-server-provision.md)
* [Migrazione di un database a SQL Server su una macchina virtuale di Azure](virtual-machines-windows-migrate-sql.md)
* [Disponibilità elevata e ripristino di emergenza di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-high-availability-dr.md)
* [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md) (Procedure consigliate sulle prestazioni per SQL Server nelle macchine virtuali di Azure)
* [Modelli di applicazione e strategie di sviluppo per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md)

**Macchine virtuali Linux**:

* [Panoramica di SQL Server in una macchina virtuale Linux](../../linux/sql/sql-server-linux-virtual-machines-overview.md)
* [Effettuare il provisioning di una macchina virtuale Linux con SQL Server](../../linux/sql/provision-sql-server-linux-virtual-machine.md)
* [Domande frequenti (Linux)](../../linux/sql/sql-server-linux-faq.md)
* [Documentazione di SQL Server in Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-overview)

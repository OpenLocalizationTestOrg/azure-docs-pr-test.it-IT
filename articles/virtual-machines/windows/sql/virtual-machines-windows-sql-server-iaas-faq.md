---
title: aaaSQL Server in domande frequenti su macchine virtuali di Azure | Documenti Microsoft
description: In questo articolo vengono fornite le risposte toofrequently domande frequenti sull'esecuzione di SQL Server in macchine virtuali di Azure.
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Domande frequenti su SQL nelle macchine virtuali di Azure
Questo argomento vengono fornite le risposte toosome di hello domande più comuni sull'esecuzione [SQL Server in macchine virtuali di Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Domande frequenti

1. **Come si crea una macchina virtuale di Azure con SQL Server?**

    la soluzione più semplice di Hello è toocreate una macchina virtuale che includa SQL Server. Per un'esercitazione sull'iscrizione ad Azure e creare una VM SQL dal portale di hello, vedere [il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md). È possibile selezionare un'immagine di macchina virtuale che utilizza licenze di pagamento al minuto SQL Server oppure è possibile utilizzare un'immagine che consente di toobring la propria licenza di SQL Server. È anche possibile hello manualmente l'installazione di SQL Server in una macchina virtuale e il riutilizzo di una licenza in locale. Se si usa la funzionalità Bring Your Own License, è necessario avere [Mobilità delle licenze tramite Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). Per altre informazioni, vedere [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Guida ai prezzi per le VM di SQL Server in Azure).

1. **Qual è la differenza hello tra macchine virtuali SQL e hello servizio Database SQL?**

    Dal punto di vista concettuale l'esecuzione di SQL Server in una macchina virtuale di Azure non è diversa dall'esecuzione di SQL Server in un centro dati remoto. Per contro, il servizio [Database SQL](../../../sql-database/sql-database-technical-overview.md) offre una soluzione DaaS (Database-as-a-service). Con il Database SQL, non si dispone macchine toohello di accesso che ospitano i database. Per un confronto completo, vedere [Scegliere un'opzione di SQL Server cloud: database SQL di Azure (PaaS) o SQL Server in VM di Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Come è possibile eseguire la migrazione di my toohello di database di SQL Server on-premise Cloud?**

    Creare prima una macchina virtuale di Azure con un'istanza di SQL Server, Quindi, eseguire la migrazione toothat istanza database locale. Per strategie di migrazione dei dati, vedere [eseguire la migrazione di un tooSQL database Server SQL Server in una macchina virtuale Azure](virtual-machines-windows-migrate-sql.md).

1. **È possibile installare una seconda istanza di SQL Server su hello stessa macchina virtuale? È possibile modificare le funzionalità installate dell'istanza predefinita di hello?**

    Sì. Hello supporti di installazione di SQL Server si trova in una cartella hello **C** unità. Eseguire **Setup.exe** da tale posizione tooadd nuove istanze o SQL Server toochange altri installate funzionalità di SQL Server nel computer di hello. Si noti che alcune funzionalità, ad esempio Backup automatizzato, l'applicazione automatica di patch e integrazione dell'insieme di credenziali chiave di Azure, può essere utilizzato solo con l'istanza predefinita di hello.

1. **È possibile disinstallare l'istanza predefinita di hello di SQL Server?**

    Sì. Sono tuttavia necessarie alcune considerazioni. Come indicato nella risposta precedente hello, funzionalità che si basano su hello [estensione di SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md) funzionano solo in un'istanza predefinita di hello. Se si disinstalla l'istanza predefinita di hello, estensione hello continua toolook relativo e può generare errori nel log eventi. Questi errori sono le seguenti due origini hello: **gestione delle credenziali di Microsoft SQL Server** e **Microsoft SQL Server IaaS Agent**. Uno degli errori di hello potrebbe essere simile toohello seguenti:
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Se si decide l'istanza predefinita di hello toouninstall, disinstallarlo hello [estensione di SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md) anche.

1. **Come eseguire l'aggiornamento tooa/edizione della nuova versione di SQL Server in una macchina virtuale di Azure hello?**

    Attualmente non è disponibile alcun aggiornamento sul posto per SQL Server in esecuzione in una VM di Azure. Creare una nuova macchina virtuale Azure con versione o edizione di SQL Server hello desiderato e quindi eseguire la migrazione del database toohello nuovo server tramite standard [tecniche di migrazione dei dati](virtual-machines-windows-migrate-sql.md).

1. **Come si installa una copia di SQL Server con licenza in una VM di Azure?**

    Esistono due modi toodo questo. È possibile eseguire il provisioning di uno di hello [immagini di macchina virtuale che supporta le licenze](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Un'altra opzione è toocopy hello SQL Server installazione supporti tooa macchina virtuale Windows Server e quindi installare SQL Server in VM hello. Per motivi di licenza, è necessario avere [Mobilità delle licenze tramite Software Assurance in Azure](https://azure.microsoft.com/pricing/license-mobility/). Per altre informazioni, vedere [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Guida ai prezzi per le VM di SQL Server in Azure).

1. **È possibile modificare un toouse VM personale licenza di SQL Server se è stato creato da una delle immagini della raccolta prepagata hello?**

    No. È non possibile passare da toousing gestione licenze di pagamento al minuto la propria licenza. Creare una nuova macchina virtuale Azure utilizzando uno dei hello [immagini BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), quindi eseguire la migrazione del database toohello nuovo server tramite standard [tecniche di migrazione dei dati](virtual-machines-windows-migrate-sql.md).

1. **Le istanze del cluster di failover di SQL Server sono supportate nelle macchine virtuali di Azure?**

   Sì. È possibile [creare un Cluster di Failover di Windows in Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) e usare spazi di archiviazione è diretta (S2D) per l'archiviazione cluster hello. In alternativa, è possibile usare soluzioni di clustering o archiviazione di terze parti come descritto in [Disponibilità elevata e ripristino di emergenza per SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **È necessario toopay toolicense SQL Server in una macchina virtuale di Azure se viene utilizzato solo per il failover di standby /?**

    Non si dispone toopay toolicense un SQL Server che partecipano come replica secondaria passiva in una distribuzione a disponibilità elevata, se si dispone di Software Assurance e utilizzare mobilità delle licenze, come descritto in [domande frequenti sulle licenze di macchina virtuale](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Come si applicano gli aggiornamenti e i Service Pack a una VM di SQL Server?**

    Macchine virtuali consentono di controllare computer host hello e incluso quando e come applicare gli aggiornamenti. Per sistema operativo hello, è possibile applicare manualmente gli aggiornamenti di windows oppure è possibile abilitare un servizio di pianificazione denominato [patch automatizzate](virtual-machines-windows-sql-automated-patching.md). Applicazione automatica delle patch installa tutti gli aggiornamenti contrassegnati come importanti, inclusi gli aggiornamenti di SQL Server in tale categoria. Altri aggiornamenti facoltativi tooSQL che server deve essere installato manualmente.

1. **È possibile tooset le configurazioni non visualizzati nella raccolta di macchine virtuali hello (ad esempio Windows 2008 R2 + SQL Server 2012)?**

    No. Per le immagini della raccolta di macchina virtuale che includono SQL Server, è necessario selezionare una delle immagini fornita hello.

1. **Come si installa SQL Server Data Tools in una VM di Azure?**

     Scaricare e installare gli strumenti dati SQL hello da [Microsoft SQL Server Data Tools - Business Intelligence per Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Risorse

Per una panoramica di SQL Server in macchine virtuali di Azure, guardare il video di hello [macchina virtuale di Azure è migliore piattaforma di hello per SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). È inoltre possibile ottenere una buona introduzione in argomento hello [SQL Server in macchine virtuali di Azure Panoramica](virtual-machines-windows-sql-server-iaas-overview.md).

Altre risorse:

* [Eseguire il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md)
* [La migrazione di un tooSQL Database Server in una macchina virtuale di Azure](virtual-machines-windows-migrate-sql.md)
* [Disponibilità elevata e ripristino di emergenza di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-high-availability-dr.md)
* [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md) (Procedure consigliate sulle prestazioni per SQL Server nelle macchine virtuali di Azure)
* [Modelli di applicazione e strategie di sviluppo per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 
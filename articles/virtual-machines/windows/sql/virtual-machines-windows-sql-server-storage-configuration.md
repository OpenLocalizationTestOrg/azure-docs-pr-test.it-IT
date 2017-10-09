---
title: configurazione aaaStorage per le macchine virtuali di SQL Server | Documenti Microsoft
description: "Questo argomento descrive come viene configurata l'archiviazione da Azure per le VM di SQL Server durante il provisioning (modello di distribuzione di Resource Manager). Viene inoltre spiegato come è possibile configurare l'archiviazione per le VM di SQL Server esistenti."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>Configurazione dell'archiviazione per le VM di SQL Server
Quando si configura un'immagine di macchina virtuale di SQL Server in Azure, tooautomate hello portale consente la configurazione di archiviazione. Ciò include toohello archiviazione macchina virtuale, rendendo tale tooSQL accessibile archiviazione Server e configurarlo toooptimize per i requisiti di prestazioni specifici di collegamento.

Questo argomento illustra come viene configurata l'archiviazione da Azure per le VM di SQL Server, sia durante il provisioning che per le VM esistenti. Questa configurazione è basata su hello [consigliate per le prestazioni](virtual-machines-windows-sql-performance.md) per le macchine virtuali di Azure che esegue SQL Server.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Prerequisiti
hello toouse automatizzata le impostazioni di configurazione di archiviazione, la macchina virtuale richiede hello seguenti caratteristiche:

* Provisioning eseguito con un' [immagine della raccolta di SQL Server](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).
* Usa hello [il modello di distribuzione di gestione risorse](../../../azure-resource-manager/resource-manager-deployment-model.md).
* Uso dell' [archiviazione Premium](../../../storage/common/storage-premium-storage.md).

## <a name="new-vms"></a>Nuove VM
Hello sezioni seguenti descrivono come archiviazione tooconfigure per nuove macchine virtuali di SQL Server.

### <a name="azure-portal"></a>Portale di Azure
Durante il provisioning di una macchina virtuale di Azure usando un'immagine della raccolta di SQL Server, è possibile scegliere tooautomatically configurare l'archiviazione di hello per la nuova macchina virtuale. Specificare dimensioni di archiviazione hello, limiti sulle prestazioni e il tipo di carico di lavoro. Hello seguente schermata Mostra pannello di configurazione di archiviazione hello utilizzato durante la VM SQL provisioning.

![Configurazione dell'archiviazione per le VM di SQL Server durante il provisioning](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

In base alle scelte, Azure esegue hello seguente attività di configurazione di archiviazione dopo la creazione di hello VM:

* Crea e collega premium archiviazione macchina virtuale di dati dischi toohello.
* Configura hello dati dischi toobe accessibile tooSQL Server.
* Configura i dischi dati hello in uno spazio di archiviazione specificato alcun pool in base a hello requisiti (IOPS e la velocità effettiva) di dimensioni e prestazioni.
* Associa il pool di archiviazione hello con una nuova unità sulla macchina virtuale hello.
* Ottimizza la nuova unità in base al tipo di carico di lavoro specificato (data warehousing, elaborazione transazionale o generale).

Per ulteriori informazioni su come Azure Configura le impostazioni di archiviazione, vedere hello [sezione di configurazione dell'archiviazione](#storage-configuration). Per una procedura dettagliata completa di toocreate vedere una VM SQL Server nel portale di Azure, hello [hello provisioning esercitazione](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="resource-manage-templates"></a>Modelli di Resource Manager
Se si utilizza hello seguenti modelli di gestione risorse, per impostazione predefinita, senza alcuna configurazione di pool di archiviazione vengono collegati due dischi di dati premium. Tuttavia, è possibile personalizzare queste numero di hello toochange di modelli di dischi dati premium di macchina virtuale toohello associata.

* [Creare una VM con il backup automatico](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [Creare una VM con l'applicazione automatica delle patch](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [Creare una VM con l'integrazione di AKV](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>VM esistenti
Per SQL Server le macchine virtuali esistenti, è possibile modificare alcune impostazioni di archiviazione nel portale di Azure hello. Selezionare la macchina virtuale, andare toohello area delle impostazioni e quindi selezionare configurazione di SQL Server. Pannello di configurazione di SQL Server Hello viene illustrato l'utilizzo di archiviazione della macchina virtuale corrente hello. In questo grafico vengono visualizzate tutte le unità esistenti nella VM. Per ogni unità, consente di visualizzare lo spazio di archiviazione hello nelle quattro sezioni:

* Dati SQL
* Log SQL
* Altro (archiviazione non SQL)
* Disponibile

![Configurare l'archiviazione per le VM di SQL Server esistenti](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure hello archiviazione tooadd una nuova unità o estendere un'unità esistente, fare clic sul collegamento Modifica hello sopra il grafico hello.

opzioni di configurazione Hello visualizzate variano a seconda se si usa questa funzionalità prima. Quando si utilizza per hello prima volta, è possibile specificare i requisiti di archiviazione per una nuova unità. Se è stata utilizzata in precedenza questo toocreate funzionalità un'unità, è possibile scegliere tooextend archiviazione dell'unità.

### <a name="use-for-hello-first-time"></a>Utilizzo per la prima volta hello
Se è la prima volta che tramite questa funzionalità, è possibile specificare limiti di dimensioni e le prestazioni di archiviazione per una nuova unità hello. Questa esperienza è simile toowhat che verrà visualizzato in fase di provisioning. la differenza principale Hello è che non sono consentiti tipo di carico di lavoro toospecify hello. Questa restrizione impedisce che interrompere qualsiasi configurazione esistente di SQL Server nella macchina virtuale hello.

![Configurare i dispositivi di scorrimento delle opzioni per l'archiviazione di SQL Server](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Azure crea una nuova unità in base alle specifiche. In questo scenario, Azure esegue hello seguenti attività di configurazione di archiviazione:

* Crea e collega premium archiviazione macchina virtuale di dati dischi toohello.
* Configura hello dati dischi toobe accessibile tooSQL Server.
* Configura i dischi dati hello in uno spazio di archiviazione specificato alcun pool in base a hello requisiti (IOPS e la velocità effettiva) di dimensioni e prestazioni.
* Associa il pool di archiviazione hello con una nuova unità sulla macchina virtuale hello.

Per ulteriori informazioni su come Azure Configura le impostazioni di archiviazione, vedere hello [sezione di configurazione dell'archiviazione](#storage-configuration).

### <a name="add-a-new-drive"></a>Aggiungere una nuova unità
Se l'archiviazione è già stata configurata nella VM di SQL Server, per l'espansione dell'archiviazione diventano disponibili due nuove opzioni. Hello prima opzione è tooadd una nuova unità, che è possibile aumentare il livello di prestazioni hello della macchina virtuale.

![Aggiungere un nuovo tooa unità SQL VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

Dopo l'aggiunta di unità di hello, tuttavia, è necessario eseguire alcuni miglioramento delle prestazioni hello tooachieve configurazione manuale aggiuntiva.

### <a name="extend-hello-drive"></a>Estendere hello unità
Hello altre opzioni per l'espansione di archiviazione sono tooextend hello esistente unità. Questa opzione aumenta spazio di archiviazione disponibile hello per le unità, ma non aumenta le prestazioni. Con pool di archiviazione, è possibile modificare il numero di hello di colonne dopo la creazione di pool di archiviazione hello. numero di Hello colonne determina il numero di hello di scrittura in parallelo, che possono essere archiviati con striping nei dischi dati hello. Di conseguenza, qualsiasi disco dati aggiunto non consente di aumentare le prestazioni. Forniscono maggiore spazio di archiviazione solo per i dati di hello in corso la scrittura. Questa limitazione significa anche che, quando si estende unità hello, numero hello colonne determina il numero minimo di hello di dischi dati che è possibile aggiungere. Pertanto, se si crea un pool di archiviazione con dischi quattro dati, hello numero di colonne è inoltre quattro. Ogni volta che si estende archiviazione hello, è necessario aggiungere dischi dati almeno quattro.

![Estendere un'unità per una VM di SQL](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Configurazione dell'archiviazione
In questa sezione fornisce un riferimento per le modifiche di configurazione archiviazione hello che Azure esegue automaticamente durante il provisioning della VM SQL o la configurazione nel portale di Azure hello.

* Se sono stati selezionati meno di due TB di spazio di archiviazione per la VM, Azure non crea un pool di archiviazione.
* Se sono stati selezionati almeno due TB di spazio di archiviazione per la VM, Azure configura un pool di archiviazione. sezione successiva di Hello di questo argomento fornisce i dettagli di hello di configurazione del pool di archiviazione hello.
* Per la configurazione automatica dell'archiviazione vengono sempre usati dischi dati P30 di [archiviazione Premium](../../../storage/common/storage-premium-storage.md) . Di conseguenza, non esiste un mapping 1:1 tra il numero selezionato di terabyte e numero hello di dischi dati collegati tooyour macchina virtuale.

Per informazioni sui prezzi, vedere hello [prezzi di archiviazione](https://azure.microsoft.com/pricing/details/storage) pagina hello **archiviazione su disco** scheda.

### <a name="creation-of-hello-storage-pool"></a>Creazione di pool di archiviazione hello
Azure Usa hello seguente pool di archiviazione di impostazioni toocreate hello in macchine virtuali di SQL Server.

| Impostazione | Valore |
| --- | --- |
| Dimensioni di striping |256 KB (data warehousing); 64 KB (transazionale) |
| Dimensione disco |1 TB ciascuno |
| Cache |Lettura |
| Dimensioni allocazione |Dimensioni delle unità di allocazione NTFS = 64 KB |
| Inizializzazione file immediata |Enabled |
| Blocco di pagine in memoria |Enabled |
| Ripristino |Recupero con registrazione minima (nessuna resilienza) |
| Numero di colonne |Numero di dischi dati<sup>1</sup> |
| Percorso TempDB |Archiviato sui dischi dati<sup>2</sup> |

<sup>1</sup> dopo la creazione di pool di archiviazione hello, non è possibile modificare il numero di hello di colonne nel pool di archiviazione hello.

<sup>2</sup> questa impostazione si applica solo a toohello prima unità creata tramite funzionalità di configurazione di archiviazione hello.

## <a name="workload-optimization-settings"></a>Impostazioni di ottimizzazione del carico di lavoro
Hello nella tabella seguente vengono descritti hello del carico di lavoro tipo disponibili tre opzioni e le ottimizzazioni corrispondente:

| Tipo di carico di lavoro | Descrizione | Ottimizzazioni |
| --- | --- | --- |
| **Generale** |Impostazione predefinita che supporta la maggior parte dei carichi di lavoro |None |
| **Elaborazione transazionale** |Ottimizza l'archiviazione di hello per carichi di lavoro OLTP database tradizionale |Flag di traccia 1117<br/>Flag di traccia 1118 |
| **Data warehousing** |Ottimizza l'archiviazione di hello per carichi di lavoro di analisi e creazione report |Flag di traccia 610<br/>Flag di traccia 1117 |

> [!NOTE]
> È possibile specificare il tipo di carico di lavoro hello solo quando si esegue il provisioning di una macchina virtuale SQL selezionandolo nel passaggio di configurazione di archiviazione hello.
>
>

## <a name="next-steps"></a>Passaggi successivi
Per altri argomenti correlati toorunning SQL Server in macchine virtuali di Azure, vedere [SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).

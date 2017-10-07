---
title: aaaBack backup portale classico di DPM i carichi di lavoro tooAzure | Documenti Microsoft
description: Toobacking un'introduzione dei server DPM con il servizio di Azure Backup hello
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: System Center Data Protection Manager, data protection manager, backup di dpm
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Preparazione tooback dei carichi di lavoro tooAzure con Data Protection Manager
> [!div class="op_single_selector"]
> * [Server di backup di Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Server di Backup di Azure (classico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (classico)](backup-azure-dpm-introduction-classic.md)
>
>

Questo articolo fornisce un tooprotect di Microsoft Azure Backup toousing Introduzione i server di System Center Data Protection Manager (DPM) e i carichi di lavoro. Le informazioni dell'articolo riguardano:

* Il funzionamento del backup del server DPM di Azure
* Hello prerequisiti tooachieve un'esperienza uniforme di backup
* Hello tipico errori rilevati e in che modo toodeal con essi
* Scenari supportati

DPM di System Center esegue il backup di file e dati delle applicazioni. Dati sottoposti a backup tooDPM possono essere archiviati su nastro, disco, o backup tooAzure con Backup di Microsoft Azure. DPM interagisce con Backup di Azure nei modi seguenti:

* **DPM distribuito come macchina virtuale locale o server fisica** -se DPM viene distribuito come server fisico o come macchina virtuale Hyper-V locale è possibile eseguire il backup di Azure Backup con dati tooan credenziali inoltre toodisk e backup su nastro.
* **DPM distribuito come macchina virtuale di Azure** : a partire dalla versione di System Center 2012 R2 con aggiornamento 3, DPM può essere distribuito come macchina virtuale di Azure. Se DPM viene distribuito come macchina virtuale di Azure che è possibile eseguire il backup di dischi di dati tooAzure collegato toohello macchina virtuale di Azure di DPM oppure puoi eseguire l'offload archiviazione dei dati hello eseguendone il backup dell'insieme di credenziali di tooan Azure Backup.

## <a name="why-backup-your-dpm-servers"></a>Motivi per eseguire il backup dei server DPM
Hello business vantaggi dell'utilizzo di Azure Backup per il backup dei server DPM includono:

* Per la distribuzione di DPM in locale, è possibile utilizzare backup di Azure come un tootape distribuzione termine toolong alternativo.
* Per le distribuzioni DPM in Azure, Backup di Azure consente archiviazione toooffload dal disco di Azure, hello e tooscale backup archiviando i dati meno recenti in Backup di Azure e i nuovi dati sul disco.

## <a name="how-does-dpm-server-backup-work"></a>Funzionamento del backup del server DPM
tooback rapidamente una macchina virtuale, prima è necessario uno snapshot in un momento dei dati di hello. ora pianificata Hello Azure Backup service avvia hello processo di backup in hello e trigger hello estensione backup tootake uno snapshot. coordinate di estensione del backup Hello con hello guest VSS tooachieve coerenza del servizio e richiama l'API del servizio di archiviazione Azure hello snapshot del blob hello una volta raggiunta la coerenza. Si tratta di fatto tooget uno snapshot coerente dei dischi hello della macchina virtuale hello, senza dovere tooshut verso il basso.

Dopo che è stato eseguito snapshot hello, dati hello viene trasferiti dall'hello Azure Backup service toohello backup insieme di credenziali. servizio Hello si occupa di identificazione e il trasferimento solo i blocchi di hello che sono stati modificati dall'ultimo backup hello rendendo efficiente di rete e archiviazione di backup hello. Quando viene completato il trasferimento dei dati di hello, snapshot hello viene rimosso e viene creato un punto di ripristino. Questo punto di ripristino può essere visualizzato nel portale di Azure classico hello.

> [!NOTE]
> Per quanto riguarda le macchine virtuali Linux, è possibile eseguire soltanto backup coerenti a livello di file.
>
>

## <a name="prerequisites"></a>Prerequisiti
Preparare il Backup di Azure tooback backup dei dati DPM come segue:

1. **Creare un insieme di credenziali di backup**. Se è ancora stato creato un insieme di credenziali di Backup nella sottoscrizione, vedere hello Azure versione del portale di questo articolo - [preparare tooback backup tooAzure i carichi di lavoro con DPM](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.
  > È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
  >- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
  >- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
  >

2. **Scaricare l'insieme di credenziali** : In Azure Backup, carica certificato di gestione di hello creato toohello insieme di credenziali.
3. **Installare hello Azure Backup Agent e registrare il server di hello** : da Backup di Azure, installare l'agente di hello in ogni server DPM e registrare i server DPM hello nell'insieme di credenziali backup hello.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Requisiti e limitazioni
* DPM può essere eseguito come server fisico o come macchina virtuale Hyper-V installata in System Center 2012 SP1 o System Center 2012 R2. Inoltre, è possibile eseguirlo come macchina virtuale di Azure in System Center 2012 R2 (con almeno l'aggiornamento cumulativo 3 di DPM 2012 R2) oppure come macchina virtuale di Windows in VMware con System Center 2012 R2 e almeno il relativo aggiornamento cumulativo 5.
* Se DPM viene eseguito con System Center 2012 SP1, è necessario installare l'aggiornamento cumulativo 2 per System Center Data Protection Manager SP1. Ciò è necessario prima di poter installare hello Azure Backup Agent.
* server di Data Protection Manager Hello deve disporre di Windows PowerShell e .net Framework 4.5 installati.
* DPM può eseguire il backup la maggior parte dei carichi di lavoro tooAzure Backup. Per un elenco completo dei componenti supportati, vedere hello Backup di Azure supporta i seguenti elementi.
* Impossibile ripristinare i dati archiviati in Azure Backup con l'opzione "copia tootape" hello.
* È necessario un account Azure con funzionalità di Backup di Azure hello abilitata. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Informazioni sui [prezzi di Backup di Azure](https://azure.microsoft.com/pricing/details/backup/).
* Tramite Azure Backup richiede hello Azure Backup Agent toobe installato nei server di hello tooback da backup. Ogni server deve essere almeno il 10% della dimensione hello dati hello che viene eseguito il backup, disponibile come archiviazione locale disponibile. Ad esempio, il backup di 100 GB di dati richiede un minimo di 10 GB di spazio disponibile nel percorso di file temporanei di hello. Sebbene hello minimo è 10%, è consigliabile 15% di toobe di spazio libero di archiviazione locale utilizzato per il percorso della cache di hello.
* Verranno archiviati i dati in archiviazione di Azure dell'insieme di credenziali hello. Nessun importo toohello limite dei dati che è possibile eseguire il backup tooan Azure Backup vault ma dimensioni hello di un'origine dati (ad esempio una macchina virtuale o un database) non devono superare 54,400 GB.

Questi tipi di file sono supportati per eseguire il backup tooAzure:

* Crittografati (solo backup completi)
* Compressi (backup incrementali supportati)
* Sparse (backup incrementali supportati)
* Compressi e sparse (considerati come sparse)

Questi tipi di file non sono supportati:

* I server nei file system che distinguono fra minuscole e maiuscole non sono supportati.
* Collegamenti reali (ignorati)
* Reparse point (ignorati)
* Crittografati e compressi (ignorati)
* Crittografati e sparse (ignorati)
* Flusso compresso
* Flusso di tipo sparse

> [!NOTE]
> Da in System Center 2012 DPM con SP1 in poi, puoi eseguire il backup dei carichi di lavoro protetti da DPM tooAzure con Backup di Microsoft Azure.
>
>

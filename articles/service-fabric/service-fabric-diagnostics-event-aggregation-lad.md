---
title: Aggregazione di eventi di Service Fabric con diagnostica Azure per Linux aaaAzure | Documenti Microsoft
description: Informazioni sull'aggregazione e la raccolta di eventi con LAD per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Aggregazione e raccolta di eventi con Diagnostica di Azure per Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Quando si esegue un cluster di Azure Service Fabric, è un log di hello buona toocollect da tutti i nodi di hello in una posizione centrale. La presenza di log hello in una posizione centrale consente di analizzare e risolvere i problemi del cluster, o problemi in applicazioni hello e servizi in esecuzione in tale cluster.

Tooupload un modo e raccogliere i log è toouse estensione di diagnostica Azure Linux (LAD) hello, che carica i log tooAzure archiviazione e dispone inoltre di hello opzione toosend registri tooAzure Application Insights o hub eventi. È inoltre possibile utilizzare gli eventi di hello tooread un processo esterno dall'archivio e inserirle in un prodotto di piattaforma di analisi, ad esempio [OMS Log Analitica](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log.

## <a name="log-and-event-sources"></a>Origini di log ed eventi

### <a name="service-fabric-platform-events"></a>Eventi della piattaforma Service Fabric
Service Fabric emette alcuni registri pronti all'uso tramite [LTTng](http://lttng.org), inclusi gli eventi operativi o gli eventi di runtime. Questi log vengono archiviati nella posizione hello hello gestione delle risorse del cluster modello specifica. tooget o impostare i dettagli di account di archiviazione hello, cercare il tag di hello **AzureTableWinFabETWQueryable** e cercare **StoreConnectionString**.

### <a name="application-events"></a>Eventi dell'applicazione
 Eventi generati dal codice delle applicazioni e dei servizi come specificato dall'utente durante la strumentazione del software. È possibile usare qualsiasi soluzione di registrazione che scriva file di log basati su testo, ad esempio LTTng. Per ulteriori informazioni, vedere documentazione di LTTng hello nella traccia dell'applicazione.

[Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Distribuire l'estensione diagnostica hello
Hello primo passaggio per la raccolta di log è l'estensione di diagnostica toodeploy hello in ognuna delle macchine virtuali di hello in cluster di Service Fabric hello. Hello estensione di diagnostica raccoglie i log in ogni macchina virtuale e li carica toohello account di archiviazione specificato. passaggi di Hello variano in base che si utilizzi hello portale di Azure o Gestione risorse di Azure.

toodeploy hello diagnostica estensione toohello macchine virtuali in cluster hello come parte della creazione del cluster, impostare **diagnostica** troppo**su**. Dopo aver creato il cluster hello, è possibile modificare questa impostazione tramite il portale di hello.

Quindi, configurare diagnostica Azure Linux (LAD) toocollect hello file e inserirli in account di archiviazione. Questo processo viene illustrato come lo scenario 3 ("Carica i file di log") dell'articolo hello [toomonitor utilizzando LAD e diagnosticare le macchine virtuali Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Seguente ottiene questo processo è accedere toohello tracce. È possibile caricare Visualizzatore tooa tracce di hello di propria scelta.

È inoltre possibile distribuire l'estensione diagnostica hello usando Gestione risorse di Azure. Hello processo è analogo per Windows e Linux ed è documentato per cluster di Windows in [modalità di registrazione con diagnostica Azure toocollect](service-fabric-diagnostics-how-to-setup-wad.md).

È anche possibile usare Operations Management Suite, come descritto in [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) (Analisi dei log di Operations Management Suite con Linux).

Dopo aver completato questa configurazione, hello LAD agente monitoraggi hello i file di log specificato. Ogni volta che una nuova riga aggiunta toohello file, viene creata una voce syslog che è inviato toohello spazio di archiviazione specificato.

## <a name="next-steps"></a>Passaggi successivi

toounderstand in dettaglio gli eventi che è necessario esaminare durante la risoluzione dei problemi, vedere [LTTng documentazione](http://lttng.org/docs) e [LAD utilizzando](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

---
title: aaaCollect log tramite diagnostica Azure per Linux | Documenti Microsoft
description: In questo articolo viene descritto come tooset di diagnostica Azure toocollect log da un cluster di Service Fabric Linux in esecuzione in Azure.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Raccogliere log con Diagnostica di Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Quando si esegue un cluster di Azure Service Fabric, è un log di hello buona toocollect da tutti i nodi di hello in una posizione centrale. La presenza di log hello in una posizione centrale rende facile tooanalyze e risoluzione dei problemi, siano essi in servizi, l'applicazione o cluster hello stesso. Tooupload un modo e raccogliere i log è toouse hello l'estensione diagnostica Azure, quali caricamenti registra tooAzure archiviazione, Azure Application Insights o hub eventi di Azure. È anche possibile leggere gli eventi di hello dall'archiviazione o hub eventi e inserirli in un prodotto, ad esempio [Log Analitica](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log. In [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) è integrato un servizio completo di analisi e di ricerca dei log.

## <a name="log-sources-that-you-might-want-toocollect"></a>Origini di log che è possibile toocollect
* **I log di Service Fabric**: generato dalla piattaforma hello tramite [LTTng](http://lttng.org) e caricati tooyour account di archiviazione. I registri possono essere gli eventi operativi o genera eventi di runtime che hello piattaforma. Questi log vengono archiviati nel percorso hello manifesto del cluster che hello specifica. (tooget hello account di archiviazione dettagli, cercare il tag di hello **AzureTableWinFabETWQueryable** e cercare **StoreConnectionString**.)
* **Eventi dell'applicazione:** generati dal codice dei servizi. È possibile usare qualsiasi soluzione di registrazione che scriva file di log basati su testo, ad esempio LTTng. Per ulteriori informazioni, vedere documentazione di LTTng hello nella traccia dell'applicazione.  

## <a name="deploy-hello-diagnostics-extension"></a>Distribuire l'estensione diagnostica hello
Hello primo passaggio per la raccolta di log è l'estensione di diagnostica toodeploy hello in ognuna delle macchine virtuali di hello in cluster di Service Fabric hello. Hello estensione di diagnostica raccoglie i log in ogni macchina virtuale e li carica toohello account di archiviazione specificato. passaggi di Hello variano in base che si utilizzi hello portale di Azure o Gestione risorse di Azure.

toodeploy hello diagnostica estensione toohello macchine virtuali in cluster hello come parte della creazione del cluster, impostare **diagnostica** troppo**su**. Dopo aver creato il cluster hello, è possibile modificare questa impostazione tramite il portale di hello.

Quindi, configurare diagnostica Azure Linux (LAD) toocollect hello file e inserirli in account di archiviazione. Questo processo viene illustrato come lo scenario 3 ("Carica i file di log") dell'articolo hello [toomonitor utilizzando LAD e diagnosticare le macchine virtuali Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Seguente ottiene questo processo è accedere toohello tracce. È possibile caricare Visualizzatore tooa tracce di hello di propria scelta.

È inoltre possibile distribuire l'estensione diagnostica hello usando Gestione risorse di Azure. Hello processo è analogo per Windows e Linux ed è documentato per cluster di Windows in [modalità di registrazione con diagnostica Azure toocollect](service-fabric-diagnostics-how-to-setup-wad.md).

È anche possibile usare Operations Management Suite, come descritto in [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) (Analisi dei log di Operations Management Suite con Linux).

Dopo aver completato questa configurazione, hello LAD agente monitoraggi hello i file di log specificato. Ogni volta che una nuova riga aggiunta toohello file, viene creata una voce syslog che è inviato toohello spazio di archiviazione specificato.

## <a name="next-steps"></a>Passaggi successivi
toounderstand in dettaglio gli eventi che è necessario esaminare durante la risoluzione dei problemi, vedere [LTTng documentazione](http://lttng.org/docs) e [LAD utilizzando](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).


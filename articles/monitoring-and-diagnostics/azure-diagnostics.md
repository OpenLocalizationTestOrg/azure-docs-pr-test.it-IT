---
title: aaaOverview di diagnostica di Azure | Documenti Microsoft
description: Usare Diagnostica di Azure per debug, valutazione delle prestazioni, monitoraggio e analisi del traffico dei servizi cloud, delle macchine virtuali e di Service Fabric.
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>Informazioni sulla diagnostica di Azure
Diagnostica di Azure è possibilità hello all'interno di Azure che consente la raccolta hello dei dati di diagnostica in un'applicazione distribuita. È possibile utilizzare l'estensione diagnostica hello da un numero di origini diverse. Sono attualmente supportati i ruoli Web e di lavoro dei servizi cloud di Azure e le macchine virtuali di Azure che eseguono Microsoft Windows e Service Fabric. Altri servizi di Azure dispongono di propri strumenti di diagnostica separati.

## <a name="data-you-can-collect"></a>Dati che è possibile raccogliere
Diagnostica Azure può raccogliere hello seguenti tipi di dati:

| origine dati | Descrizione |
| --- | --- |
| Contatori delle prestazioni |Contatori delle prestazioni del sistema operativo e personalizzati |
| Log applicazioni |Messaggi di traccia scritti dall'applicazione |
| Registri eventi di Windows |Informazioni inviate sistema toohello la registrazione degli eventi di Windows |
| Origine dell'evento .NET |Scrittura di eventi tramite .NET hello codice [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) classe |
| Log di IIS |Informazioni sui siti Web di IIS |
| ETW basato su manifesto |Traccia di eventi per eventi Windows generati da qualsiasi processo |
| Dump di arresto anomalo del sistema |Informazioni sullo stato di hello del processo di hello nell'evento hello di un arresto anomalo dell'applicazione |
| Log degli errori personalizzati |Log creati dall'applicazione o dal servizio. |
| Log dell'infrastruttura diagnostica di Azure |Informazioni su Diagnostica |

Hello estensione diagnostica di Azure è possibile trasferire questa tooan dati account di archiviazione di Azure o inviarlo tooservices come [Application Insights](../application-insights/app-insights-cloudservices.md). È possibile utilizzare dati hello per il debug e risoluzione dei problemi, la misurazione delle prestazioni, il monitoraggio dell'utilizzo delle risorse, l'analisi del traffico e la pianificazione della capacità e il controllo.

## <a name="versioning"></a>Controllo delle versioni
Vedere [Cronologia delle versioni di Diagnostica di Azure](azure-diagnostics-versioning-history.md).

## <a name="next-steps"></a>Passaggi successivi
Scegliere il servizio che si sta tentando toocollect diagnostica e utilizzare hello seguenti articoli tooget avviato. Utilizzare i collegamenti di diagnostica di Azure generali hello per riferimento per attività specifiche.

## <a name="web-apps"></a>App Web
Si noti che le app Web non usano Diagnostica di Azure. Trovare informazioni equivalenti di hello in [App Web](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>Servizi cloud con Diagnostica di Azure
* Se si utilizza Visual Studio, vedere [tootrace usare Visual Studio un'applicazione di servizi Cloud](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget avviato. In alternativa, vedere
* [Come toomonitor Cloud services mediante la diagnostica di Azure](../cloud-services/cloud-services-how-to-monitor.md)
* [Configurare Diagnostica di Azure in un'applicazione di Servizi cloud](../cloud-services/cloud-services-dotnet-diagnostics.md)

Per argomenti più avanzati, vedere

* [Uso di Diagnostica di Azure con Application Insights per Servizi cloud](../application-insights/app-insights-cloudservices.md)
* [Flusso di hello traccia di un'applicazione di servizi Cloud con diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [Utilizzare PowerShell tooset di diagnostica nei servizi Cloud](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Macchine virtuali con Diagnostica di Azure
* Se si utilizza Visual Studio, vedere [tootrace usare Visual Studio macchine virtuali di Azure](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget avviato. In alternativa, vedere
* [Configurare Diagnostica di Azure in una macchina virtuale di Azure](../virtual-machines-dotnet-diagnostics.md)

Per argomenti più avanzati, vedere

* [Utilizzare PowerShell tooset di diagnostica nelle macchine virtuali di Azure](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Creare una macchina virtuale Windows con monitoraggio e diagnostica con un modello di Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Service Fabric con Diagnostica di Azure
Per un'introduzione, vedere [Monitorare un'applicazione di Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Molti altri articoli Service Fabric con diagnostica sono disponibili nell'albero di navigazione hello in hello dopo aver articolo toothis a sinistra.

## <a name="general-azure-diagnostics-articles"></a>Articoli su Diagnostica di Azure
* [Configurazione dello Schema di diagnostica Azure](https://msdn.microsoft.com/library/azure/mt634524.aspx) - informazioni su come toochange hello toocollect file dello schema e l'invio di dati di diagnostica. Si noti che è possibile utilizzare anche i file di schema hello toochange Visual Studio.
* [Archiviazione dei dati di diagnostica di Azure in archiviazione di Azure](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) -conoscere hello nomi di tabelle di hello e BLOB in cui vengono scritti i dati di diagnostica hello.
* Informazioni su troppo[utilizzare i contatori delle prestazioni in diagnostica Azure](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md).
* Informazioni su troppo[tooApplication informazioni di diagnostica Route Azure Insights](azure-diagnostics-configure-application-insights.md)
* In caso di problemi nell'avvio della diagnostica o nell'individuazione dei dati nelle tabelle di archiviazione di Azure, vedere [Risoluzione dei problemi di Diagnostica di Azure](azure-diagnostics-troubleshooting.md)

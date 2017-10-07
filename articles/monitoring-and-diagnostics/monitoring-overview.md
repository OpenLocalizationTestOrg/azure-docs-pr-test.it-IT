---
title: aaaMonitoring in Microsoft Azure | Documenti Microsoft
description: Opzioni quando si desidera toomonitor nulla in Microsoft Azure. Monitoraggio di Azure, Application Insights, Log Analytics
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Panoramica sul monitoraggio in Microsoft Azure
Questo articolo offre una panoramica degli strumenti disponibili per il monitoraggio di Microsoft Azure. Si applica troppo
- Applicazioni di monitoraggio eseguite in Microsoft Azure 
- Strumenti/servizi eseguiti all'esterno di Azure che possono monitorare oggetti in Azure 

Viene descritto hello vari prodotti e servizi disponibili e come interagiscono tra loro. Che può offrire toodetermine quali siano i più appropriata in quali casi.  

## <a name="why-use-monitoring-and-diagnostics"></a>Vantaggi del monitoraggio e della diagnostica

I problemi di prestazioni nell'app cloud possono avere un impatto sull'azienda. Con più componenti interconnessi e versioni frequenti, possono verificarsi in qualsiasi momento riduzioni delle prestazioni. Quando si sviluppa un'app, gli utenti in genere individuano problemi non trovati nei test. Si deve sapere immediatamente su questi problemi e di strumenti per la diagnosi e risoluzione dei problemi di hello. Microsoft Azure offre diversi strumenti per identificare i problemi.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Come monitorare le app cloud Azure

Per il monitoraggio delle applicazioni e dei servizi di Azure sono disponibili diversi strumenti, le cui funzionalità in parte si sovrappongono. Si tratta in parte per motivi cronologici e in parte dovuto toohello sfocatura tra lo sviluppo e l'operazione di un'applicazione. 

Di seguito sono strumenti principali hello:

-   **Monitoraggio di Azure** è lo strumento di base per il monitoraggio dei servizi eseguiti in Azure. Fornisce dati a livello di infrastruttura sulla velocità effettiva di hello di un servizio e hello circostanti ambiente. Se si gestiscono le App in Azure, decidere se tooscale verso l'alto o verso il basso le risorse, quindi il monitoraggio di Azure offre è utilizzare toostart.

-   **Application Insights** può essere usato per lo sviluppo e come soluzione di monitoraggio di produzione. Installa un pacchetto nell'app offrendo così una visione più interna delle attività eseguite. I dati includono i tempi di risposta delle dipendenze, le tracce delle eccezioni, gli snapshot per il debug e i profili di esecuzione. Fornisce potenti strumenti avanzati per l'analisi di tutti questi dati di telemetria entrambi toohelp si esegue il debug di un'app e toohelp comprendere cosa gli utenti con esso. È possibile indicare se un picco in tempi di risposta è in scadenza toosomething in un'app o un problema resourcing esterno. Se si utilizza Visual Studio e app hello causa l'errore, è possibile eseguire toohello destra problema righe di codice in modo è possibile correggere l'errore.  

-   **Log Analitica** per gli utenti che necessitano di tootune prestazioni e piano di manutenzione, alle applicazioni in esecuzione nell'ambiente di produzione. È basato su Azure Raccoglie e aggrega i dati da molte origini, anche se con un ritardo di 10 minuti too15. Offre una soluzione di gestione IT olistica per l'infrastruttura Azure, locale e basata sul cloud di terze parti (ad esempio, Amazon Web Services). Fornisce strumenti più completi i dati di tooanalyze in altre origini, consente di query complesse in tutti i log e può inviare un avviso in modo proattivo condizioni specifiche.  È anche possibile raccogliere dati personalizzati nel repository centrale per l'esecuzione di query e la visualizzazione. 

-   **System Center Operations Manager (SCOM)** è destinato alla gestione e al monitoraggio di installazioni cloud di grandi dimensioni. Può essere già noto come strumento di gestione per cloud locali basati su Windows Sever e Hyper-V, ma può anche essere integrato con app Azure e gestirle. Tra l'altro, può installare Application Insights in app attive esistenti.  L'eventuale inattività di un'app viene segnalata in pochi secondi. Si noti che Log Analytics non sostituisce SCOM, ma funziona bene insieme a questo strumento.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>L'accesso a monitoraggio in hello portale di Azure
Tutti i servizi di monitoraggio di Azure sono ora disponibili in un unico riquadro dell'interfaccia utente. Per ulteriori informazioni su come tooaccess quest'area, vedere [un'introduzione a Azure monitoraggio](monitoring-get-started.md). 

È anche possibile accedere alle funzioni di monitoraggio per risorse specifiche evidenziando tali risorse ed eseguendo il drill-down nelle relative opzioni di monitoraggio. 

## <a name="examples-of-when-toouse-which-tool"></a>Esempi di quando toouse quale strumento 

Hello le sezioni seguenti mostra alcuni scenari di base e degli strumenti devono essere utilizzati insieme. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Scenario 1: Correggere gli errori in un'applicazione Azure in fase di sviluppo   

**opzione migliore Hello è insieme toouse Application Insights, il monitoraggio di Azure e Visual Studio**

Azure offre ora potenzialità hello del debugger di Visual Studio hello nel cloud hello. Configurare il monitoraggio di Azure toosend telemetria tooApplication Insights. Abilitare hello tooinclude di Visual Studio Application Insights SDK nell'applicazione. Una volta in Application Insights, è possibile utilizzare toodiscover mappa applicazione hello visivamente le parti dell'applicazione in esecuzione sono integri o non. Per le parti non integre, errori ed eccezioni sono già disponibili per l'esplorazione. È possibile utilizzare hello analitica vari in Application Insights toogo più approfondita. Se non si è certi di errore hello, è possibile utilizzare tootrace debugger di Visual Studio hello in punto di codice e il pin ulteriormente un problema. 

Per ulteriori informazioni, vedere [monitoraggio applicazioni Web](../application-insights/app-insights-azure-web-apps.md) e fare riferimento a tabella toohello del sommario a sinistra di hello per istruzioni su vari tipi di applicazioni e linguaggi.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Scenario 2: Eseguire il debug di un'applicazione Web .NET di Azure per errori riscontrati solo in produzione 

> [!NOTE]
> Queste funzionalità sono disponibili in anteprima. 

**Hello migliore opzione toouse Application Insights e se possibile Visual Studio per hello completo esperienza di debug.**

Utilizzare hello Application Insights Snapshot Debugger toodebug l'app. Quando una determinata soglia di errore si verifica con i componenti di produzione, il sistema di hello acquisisce automaticamente i dati di telemetria in intervalli di tempo come "snapshot". Hello quantità acquisita è sicuro per un cloud di produzione in quanto è piccolo sufficiente non tooaffect prestazioni, ma la traccia tooallow sufficientemente elevato.  sistema Hello è possibile acquisire più snapshot. È possibile eseguire ricerche in un punto nel tempo nel portale di Azure hello o usare Visual Studio per un'esperienza completa hello. Con Visual Studio, gli sviluppatori possono esaminare in dettaglio lo snapshot come se stessero eseguendo il debug in tempo reale. Variabili locali, parametri, memoria e frame sono interamente disponibili. Gli sviluppatori devono essere concesso l'accesso ai dati di produzione toothis tramite un ruolo di accessi.  

Per altre informazioni, vedere l'articolo relativo al [debug di snapshot](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Scenario 3: Eseguire il debug di un'applicazione Azure che usa contenitori e microservizi 

**Come nello scenario 1: usare insieme Application Insights, Monitoraggio di Azure e Visual Studio** Application Insights supporta anche la raccolta di dati di telemetria da processi eseguiti all'interno di contenitori e da microservizi (Kubernetes, Docker, Azure Service Fabric). Per altre informazioni, [vedere questo video sul debug di contenitori e microservizi](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Scenario 4: Risolvere problemi di prestazioni nell'applicazione Azure

Hello [profiler Application Insights](../application-insights/app-insights-profiler.md) è progettato toohelp risolvere questi tipi di problemi. È possibile identificare e risolvere i problemi di prestazioni delle applicazioni eseguite in servizi app (app Web, app per la logica, app per dispositivi mobili e app per le API) e altre risorse di calcolo come macchine virtuali, set di scalabilità di macchine virtuali, servizi cloud e Service Fabric. 

> [!NOTE]
> Capacità tooprofile macchine virtuali, scala set di macchine virtuali (VMSS), servizi Cloud e infrastruttura di servizi è disponibile in anteprima.   

Inoltre, ricevono in modo proattivo una notifica tramite posta elettronica su alcuni tipi di errori, ad esempio tempi di caricamento pagina lento, dallo strumento di rilevamento intelligente hello.  Non è necessario toodo qualsiasi configurazione su questo strumento. Per altre informazioni, vedere [Rilevamento intelligente: anomalie nelle prestazioni](../application-insights/app-insights-proactive-performance-diagnostics.md) e questo [post di blog](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview) sullo stesso argomento.



## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su:

* [Monitoraggio di Azure in un video tratto dall'evento Ignite 2016](https://myignite.microsoft.com/videos/4977)
* [Introduzione a Monitoraggio di Azure](monitoring-get-started.md)
* [Diagnostica di Azure](../azure-diagnostics.md) se si siano tentando toodiagnose problemi nel servizio Cloud, la macchina virtuale, macchina virtuale scalare impostato o servizio applicazione di infrastruttura.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) se si siano tentando toodiagnostic problemi nell'applicazione servizio Web app.
* [Log Analitica](https://azure.microsoft.com/documentation/services/log-analytics/) hello e [Operations Management Suite](https://www.microsoft.com/oms/) produzione soluzione di monitoraggio
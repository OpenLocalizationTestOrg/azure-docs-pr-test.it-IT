---
title: aaaFix 502 gateway non valido, 503 Servizio non disponibili errori | Documenti Microsoft
description: Risoluzione degli errori "502 - Gateway non valido" e "503 - Servizio non disponibile" nelle app Web ospitate in un servizio App di Azure.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: 502 - Gateway non valido, 503 - Servizio non disponibile, errore 503, errore 502
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>Risolvere gli errori HTTP "502 - Gateway non valido" e "503 - Servizio non disponibile" nelle App Web di Azure
Gli errori "502 - Gateway non valido" e "503 - Servizio non disponibile" sono comuni nelle applicazioni Web ospitate in un [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Questo articolo fornisce informazioni utili per la risoluzione di questi errori.

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/). In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **supporto**.

## <a name="symptom"></a>Sintomo
Quando si passa toohello web app, viene restituito un HTTP un HTTP o errore "502 Gateway non valido" errore "503 Servizio non disponibile".

## <a name="cause"></a>Causa
Spesso la causa dell'errore deriva da problemi a livello dell'applicazione, ad esempio:

* le richieste impiegano troppo tempo
* utilizzo elevato di memoria/CPU da parte dell'applicazione
* applicazione di un arresto anomalo a causa di eccezione tooan.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>Risoluzione dei problemi relativi a operazioni toosolve "502 gateway non valido" e gli errori di "503 Servizio non disponibile"
La risoluzione dei problemi prevede tre attività distinte, in ordine sequenziale:

1. [Osservare e monitorare il comportamento dell'applicazione](#observe)
2. [Raccogliere i dati](#collect)
3. [Limitare i problemi di hello](#mitigate)

[app Web del servizio app](/services/app-service/web/) vengono presentate diverse opzioni per ogni passaggio.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Osservare e monitorare il comportamento dell'applicazione
#### <a name="track-service-health"></a>Tenere traccia dell'integrità del servizio
Microsoft Azure pubblica un annuncio ogni volta che si verifica un'interruzione del servizio o una riduzione delle prestazioni. È possibile tenere traccia dello stato di hello del servizio hello in hello [portale Azure](https://portal.azure.com/). Per altre informazioni, vedere [Tenere traccia dell’integrità del servizio](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Monitorare l'app Web
Questa opzione consente toofind out dell'applicazione in caso di eventuali problemi. Nel pannello dell'app web, fare clic su hello **richieste ed errori** riquadro. Hello **metrica** pannello è visualizzate tutte le metriche di hello è possibile aggiungere.

Sono riportate alcune delle metriche hello che potrebbe essere toomonitor per l'app web

* Working set della memoria medio
* Tempo di risposta medio
* Tempo CPU
* Working set della memoria
* Richieste

![monitorare le app Web per risolvere gli errori HTTP "502 - Gateway non valido" e "503 - Servizio non disponibile"](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

Per altre informazioni, vedere:

* [Eseguire il monitoraggio delle app Web nel servizio app di Azure](web-sites-monitor.md)
* [Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. Raccogliere i dati
#### <a name="use-hello-azure-app-service-support-portal"></a>Utilizzare hello portale di supporto del servizio App di Azure
App Web fornisce hello possibilità tootroubleshoot problemi correlati tooyour web app esaminando HTTP log, i registri eventi, i dump del processo e altro. È possibile accedere a tutte queste informazioni tramite il portale di supporto disponibile all'indirizzo **http://&lt;nome app>.scm.azurewebsites.net/Support**

portale di Azure App Service supportano Hello offre tre schede separate toosupport hello tre passaggi di uno scenario di risoluzione dei problemi più comune:

1. Osservare il comportamento corrente
2. Analizzare la raccolta di informazioni di diagnostica ed eseguendo hello analizzatori incorporati
3. Attenuare il problema

Se il problema di hello è in corso al momento, fare clic su **Analizza** > **diagnostica** > **diagnosticare ora** toocreate una sessione di diagnostica, che verranno raccolti HTTP registra, Visualizzatore eventi, memoria dump, log degli errori PHP e PHP report viene elaborato.

Una volta raccolti i dati di hello, inoltre, verranno eseguire un'analisi sui dati hello e fornire un rapporto HTML.

Nel caso in cui si desiderano i dati di hello toodownload, per impostazione predefinita, potrebbe essere archiviato nella cartella D:\home\data\DaaS hello.

Per ulteriori informazioni sul portale di Azure App Service supportano hello, vedere [tooSupport nuovi aggiornamenti estensione del sito per siti Web di Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Utilizzare hello Kudu Console di Debug
Il servizio App Web include una console di debug che è possibile usare per il debug, l'esplorazione e il caricamento di file, nonché endpoint JSON per ottenere informazioni sull'ambiente in uso. Si tratta di hello *Kudu Console* o hello *Dashboard SCM* per l'app web.

È possibile accedere a questo dashboard per passare toohello collegamento **https://&lt;nome dell'app >.scm.azurewebsites.net/**.

Sono riportate alcune delle operazioni hello Kudu offre:

* impostazioni di ambiente per l'applicazione
* log in streaming
* dump di diagnostica
* console di debug in cui è possibile eseguire cmdlet di PowerShell e comandi DOS di base.

Un'altra caratteristica utile di Kudu è che, nel caso in cui l'applicazione è la generazione di eccezioni first-chance, è possibile utilizzare Kudu e dump della memoria di hello SysInternals strumento Procdump toocreate. Le immagini della memoria sono snapshot dei processo hello e spesso consentono di risolvere i problemi più complessi con l'app web.

Per altre informazioni sulle funzionalità disponibili in Kudu, vedere il post di blog relativo agli [strumenti online di Siti Web di Azure che è opportuno conoscere](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Limitare i problemi di hello
#### <a name="scale-hello-web-app"></a>Scala hello web app
In Azure App Service, per migliorare le prestazioni e velocità effettiva, è possibile modificare la scala hello in corrispondenza del quale si esegue l'applicazione. La scalabilità verticale un'app web prevede due azioni correlate: modifica il maggiore livello di prezzo e la configurazione di determinate impostazioni dopo avere impostato toohello maggiore livello di prezzo tooa di piano di servizio App.

Per altre informazioni sul ridimensionamento, vedere [Ridimensionare un'app Web nel servizio app di Azure](web-sites-scale.md).

Inoltre, è possibile scegliere toorun l'applicazione in più di un'istanza. In questo modo, non solo si ottiene una maggiore capacità di elaborazione, ma si può usufruire della tolleranza di errore. Se hello processo diventa inattivo in un'istanza, hello altra istanza verrà comunque continuare risposta alle richieste.

È possibile impostare hello scalabilità toobe manuale o automatico.

#### <a name="use-autoheal"></a>Usare la funzionalità AutoHeal
AutoHeal Ricicla il processo di lavoro hello per l'app in base alle impostazioni selezionate (ad esempio, è necessario tooexecute una richiesta di modifiche alla configurazione, le richieste, basata sulla memoria limiti o il tempo di hello). La maggior parte dei casi hello Ricicla i processi di hello sono toorecover modo più veloce di hello da un problema. Anche se è sempre possibile riavviare un'app web hello da direttamente in hello portale di Azure, AutoHeal per l'esecuzione automatica per l'utente. È sufficiente toodo aggiungere alcuni trigger in Web. config radice hello per le app web. Si noti che queste impostazioni funzionerà in hello stesso modo, anche se l'applicazione non è di tipo .net uno.

Per altre informazioni, vedere il post di blog relativo alla [correzione automatica di Siti Web di Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Riavviare l'app web hello
Questo è spesso toorecover modo più semplice di hello da problemi occasionali. In hello [portale Azure](https://portal.azure.com/), nel pannello dell'app web, si dispone di hello opzioni toostop o riavviare l'app.

 ![riavviare gli errori di app toosolve HTTP 502 gateway non valido e 503 Servizio non disponibile](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

È anche possibile gestire l'app Web usando Azure PowerShell. Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md).


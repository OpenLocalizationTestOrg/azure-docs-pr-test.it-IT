---
title: App in Azure App Service aaaMonitor | Documenti Microsoft
description: Informazioni su come toomonitor App in Azure App Service tramite hello portale di Azure.
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>Procedura: Eseguire il monitoraggio delle app nel servizio app di Azure
[Servizio app](http://go.microsoft.com/fwlink/?LinkId=529714) fornisce funzionalità di monitoraggio incorporate hello [portale Azure](https://portal.azure.com).
Sono inclusi hello possibilità tooreview **quote** e **metriche** per un'app, nonché hello piano di servizio App, impostazione **avvisi** e anche **scalabilità** automaticamente in base queste metriche.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Informazioni su quote e metriche
### <a name="quotas"></a>Quote
Le applicazioni ospitate nel servizio App sono soggetto toocertain *limiti* sulle risorse possono utilizzare. Hello limiti sono definiti dai hello **piano di servizio App** associati hello app.

Se un'applicazione hello è ospitata in un **libero** o **Shared** piano, quindi hello limiti sulle risorse hello app hello è possibile utilizzare sono definiti dai **quote**.

Se un'applicazione hello è ospitata in un **base**, **Standard** o **Premium** piano, quindi i limiti di hello risorse hello possono utilizzare vengono impostati da hello **dimensioni** (Piccolo, medio, grande) e **numero** (1, 2, 3,...) di hello **piano di servizio App**.

Le **quote** per le app ospitate nel piano **gratuito** o **condiviso** sono:

* **CPU (breve)**
  * Quantità di CPU consentita per l'applicazione in un intervallo di 5 minuti. Questa quota viene reimpostata automaticamente ogni 5 minuti.
* **CPU (giorno)**
  * Quantità totale di CPU consentita per l'applicazione in un giorno. Questa quota viene reimpostata automaticamente ogni 24 ore a mezzanotte (ora UTC).
* **Memoria**
  * Quantità totale di memoria consentita per l'applicazione.
* **Larghezza di banda**
  * Quantità totale di larghezza di banda in uscita consentita per l'applicazione in un giorno.
    Questa quota viene reimpostata automaticamente ogni 24 ore a mezzanotte (ora UTC).
* **File system**
  * Quantità totale di spazio di archiviazione consentita.

Hello solo quota applicabile tooapps ospitato in **base**, **Standard** e **Premium** piani è **Filesystem**.

Ulteriori informazioni sulle quote specifiche di hello, limiti e funzionalità disponibili per hello diverse SKU di servizio App è reperibile qui: [i limiti del servizio di sottoscrizione Azure](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Imposizione della quota
Se un'applicazione nell'utilizzo supera hello **CPU (breve)**, **CPU (giorno)**, o **della larghezza di banda** quota quindi hello applicazione verrà arrestata fino a quando non imposta nuovamente quota hello. Durante questo periodo, per tutte le richieste in ingresso verrà restituito un errore di tipo **HTTP 403**.
![][http403]

Se hello applicazione **memoria** quota viene superata, quindi l'applicazione hello sarà riavviata.

Se hello **Filesystem** quota viene superata, quindi qualsiasi operazione avrà esito negativo, incluso scrittura toologs di scrittura.

È possibile aumentare o rimuovere le quote dall'app aggiornando il piano di servizio app.

### <a name="metrics"></a>Metrica
**Metriche** forniscono informazioni sull'applicazione hello o il comportamento del piano di servizio App.

Per un **applicazione**, hello disponibili sono:

* **Tempo medio di risposta**
  * Hello tempo medio per le richieste di tooserve app hello in ms.
* **Working set della memoria medio**
  * quantità media di Hello di memoria usata dall'app hello MIB.
* **Tempo CPU**
  * quantità di Hello di CPU in secondi usati da app hello. Per altre informazioni su questa metrica, vedere [Tempo CPU e percentuale CPU](#cpu-time-vs-cpu-percentage)
* **Dati in entrata**
  * quantità di Hello di larghezza di banda in ingresso utilizzata dall'applicazione hello in MIB.
* **Dati in uscita**
  * quantità di Hello di larghezza di banda in uscita utilizzata dall'applicazione hello in MIB.
* **Http 2xx**
  * Numero di richieste che hanno restituito un codice di stato HTTP >= 200 e < 300.
* **Http 3xx**
  * Numero di richieste che hanno restituito un codice di stato HTTP >= 300 e < 400.
* **Http 401**
  * Numero di richieste che hanno restituito un codice di stato HTTP 401.
* **Http 403**
  * Numero di richieste che hanno restituito un codice di stato HTTP 403.
* **Http 404**
  * Numero di richieste che hanno restituito un codice di stato HTTP 404.
* **Http 406**
  * Numero di richieste che hanno restituito un codice di stato HTTP 406.
* **Http 4xx**
  * Numero di richieste che hanno restituito un codice di stato HTTP >= 400 e < 500.
* **Errori server HTTP**
  * Numero di richieste che hanno restituito un codice di stato HTTP >= 500 e < 600.
* **Working set della memoria**
  * Quantità corrente di memoria utilizzata dall'applicazione hello in MIB.
* **Richieste**
  * Numero totale di richieste, indipendentemente dal codice di stato HTTP restituito.

Per un **piano di servizio App**, hello disponibili sono:

> [!NOTE]
> Le metriche del piano di servizio app sono disponibili solo per i piani nello SKU **Basic**, **Standard** e **Premium**.
> 
> 

* **Percentuale di CPU**
  * Hello utilizzo medio della CPU utilizzato da tutte le istanze del piano di hello.
* **Percentuale memoria**
  * Hello Media della memoria utilizzata in tutte le istanze del piano di hello.
* **Dati in entrata**
  * Hello in arrivo larghezza di banda media utilizzata in tutte le istanze del piano di hello.
* **Dati in uscita**
  * Media di Hello in uscita di larghezza di banda utilizzata in tutte le istanze del piano di hello.
* **Lunghezza coda disco**
  * numero medio di Hello di lettura sia richieste messe in coda di scrittura nell'archiviazione. Una coda del disco elevato è un'indicazione di un'applicazione che potrebbe rallentare a causa dei / o disco tooexcessive.
* **Lunghezza coda HTTP**
  * numero medio di Hello di richieste HTTP che ha toosit in coda hello prima sono soddisfatte. Una lunghezza coda HTTP elevata o in aumento indica che il piano si trova in condizioni di carico eccessivo.

### <a name="cpu-time-vs-cpu-percentage"></a>Tempo CPU e percentuale CPU
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

Le metriche che riflettono l'utilizzo della CPU sono due. **Tempo CPU** e **Percentuale CPU**

**Tempo di CPU** è utile per le app ospitate in **libero** o **Shared** piani perché una delle rispettive quote è definita in minuti della CPU usati dall'app hello.

**Percentuale CPU** su hello invece è utile per le app ospitate in **base**, **standard** e **premium** piani poiché può essere ampliati e questa metrica è una valida indicazione hello utilizzo complessivo per tutte le istanze.

## <a name="metrics-granularity-and-retention-policy"></a>Granularità delle metriche e criteri di conservazione
Le metriche per un piano di servizio app e di applicazione sono registrate e aggregate da servizio hello con hello seguenti criteri di conservazione e granularità:

* Le metriche di granularità **minuto** vengono mantenute per **48 ore**
* Le metriche di granularità **ora** vengono mantenute per **30 giorni**
* Le metriche di granularità **giorno** vengono mantenute per **90 giorni**

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Monitoraggio delle quote e le metriche nel portale di Azure hello.
È possibile esaminare lo stato di hello di hello diversi **quote** e **metriche** influire su un'applicazione hello [portale Azure](https://portal.azure.com).

Le ![][quotas]
**quote** sono disponibili in Impostazioni>**Quote**. Hello UX consente di esaminare: nome quote hello (1), (2) l'intervallo di ripristino, (3) il limite corrente e valore (4) corrente.

![][metrics]
**Metriche** è possibile accedere direttamente dal pannello della risorsa hello. È inoltre possibile personalizzare il grafico hello da: (1) **fare clic su** su di esso e (2) selezionare **Modifica grafico**.
Da qui è possibile modificare hello (3) **intervallo di tempo**, (4) **tipo di grafico**e (5) **metriche** toodisplay.  

Per altre informazioni sulle metriche, vedere [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) (Monitorare le metriche del servizio).

## <a name="alerts-and-autoscale"></a>Avvisi e scalabilità automatica
Le metriche per un piano di App o un servizio App può essere agganciato tooalerts, toolearn ulteriori informazioni, vedere [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

Le app del servizio app ospitate nei piani di servizio app Basic, Standard e Premium supportano la **scalabilità automatica**. In questo modo si tooconfigure regole che di monitorare le metriche del piano di servizio App e possono aumentare o diminuire il numero di istanze hello fornendo risorse aggiuntive in base alle esigenze o salvataggio money quando un'applicazione hello è effettuare il provisioning in eccesso. È possibile approfondire qui scalabilità automatica: [come tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) e qui [procedure consigliate per la scalabilità automatica di monitoraggio di Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png

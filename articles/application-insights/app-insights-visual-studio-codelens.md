---
title: dati di telemetria Insights in Visual Studio CodeLens aaaApplication | Documenti Microsoft
description: Accesso rapido ai dati di telemetria per richieste ed eccezioni di Application Insights con CodeLens in Visual Studio.
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Application Insights Telemetry in CodeLens di Visual Studio
I metodi nel codice hello dell'app web possono essere annotati con dati di telemetria relativi alle eccezioni in fase di esecuzione e richiedere tempi di risposta. Se si installa [Azure Application Insights](app-insights-overview.md) nell'applicazione, dati di telemetria hello viene visualizzato in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -hello note nella parte superiore di hello di ogni funzione in cui si è abituati tooseeing utile informazioni quali il numero di hello della funzione hello posizioni si fa riferimento o hello ultima persona che ha apportato la modifica.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights in CodeLens è disponibile in Visual Studio 2015 Update 3 e versioni successive o con una versione più recente di hello di [estensione strumenti di sviluppo Analitica](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens è disponibile in hello edizioni Enterprise e Professional di Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>In cui i dati di Application Insights toofind
Cercare i dati di telemetria di Application Insights negli indicatori di CodeLens hello dei metodi pubblici richiesta hello dell'applicazione web. Gli indicatori di CodeLens vengono visualizzati sopra il metodo e le altre dichiarazioni in codice C# e Visual Basic. Se i dati di Application Insights sono disponibili per un metodo, verranno visualizzati indicatori per richieste ed eccezioni, ad esempio "100 richieste, 1% non riuscite" oppure "10 eccezioni". Fare clic su un indicatore di CodeLens per altri dettagli. 

> [!TIP]
> Richiesta di Application Insights e gli indicatori di eccezione potrebbero richiedere alcuni secondi aggiuntivi tooload dopo altri indicatori di CodeLens.
> 
> 

## <a name="exceptions-in-codelens"></a>Eccezioni in CodeLens
![Da definire](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

indicatore di Hello eccezione CodeLens Mostra il numero di hello di eccezioni che si sono verificati in hello nelle ultime 24 ore da hello 15 la maggior parte delle eccezioni che si verificano spesso nell'applicazione in uso durante tale periodo, durante l'elaborazione richiesta hello servite dal metodo hello.

toosee ulteriori dettagli, fare clic su indicatori di CodeLens eccezioni hello:

* modifica della percentuale di Hello in numero di eccezioni da hello ultime 24 ore relativo toohello precedente 24 ore
* Scegliere **passare toocode** toonavigate toohello il codice sorgente per la funzione hello hello eccezioni
* Scegliere **ricerca** tooquery hello di tutte le istanze di questa eccezione che si sono verificati nelle ultime 24 ore
* Scegliere **tendenza** tooview una visualizzazione di tendenza per le occorrenze di questa eccezione in hello nelle ultime 24 ore
* Scegliere **Visualizza tutte le eccezioni in questa app** tooquery hello di tutte le eccezioni che si sono verificati nelle ultime 24 ore
* Scegliere **esplorare le tendenze di eccezione** tooview una visualizzazione di tendenza per tutte le eccezioni che si sono verificati in hello nelle ultime 24 ore. 

> [!TIP]
> Se si visualizza "di eccezioni 0" in CodeLens ma si conosce dovrebbero essere presenti eccezioni, controllare che sia selezionato risorsa di Application Insights destra hello in CodeLens toomake. tooselect un'altra risorsa, fare clic sul progetto in Esplora soluzioni hello e scegliere **Application Insights > Scegli origine dati di telemetria**. CodeLens viene visualizzato solo per hello 15 la maggior parte delle eccezioni che si verificano spesso nell'applicazione in hello nelle ultime 24 ore, pertanto, se un'eccezione è hello 16 più frequentemente o inferiore, verrà visualizzato "0 eccezioni". Eccezioni dalle viste ASP.NET non vengano visualizzati i metodi di controller hello da tali visualizzazioni generate.
> 
> [!TIP]
> Se viene visualizzato "? le eccezioni"in CodeLens, è necessario tooassociate che proprio account Azure con Visual Studio o le credenziali dell'account di Azure potrebbe essere scaduto. In entrambi i casi, fare clic su "? le eccezioni"e scegliere **aggiungere un account...**  tooenter le credenziali.
> 
> 

## <a name="requests-in-codelens"></a>Richieste in CodeLens
![Da definire](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Hello richiesta CodeLens Mostra indicatore hello numero HTTP richiede che stato serviti da un metodo di hello oltre 24 ore e percentuale di hello di tali richieste non riuscite.

Fare clic su ulteriori dettagli, toosee hello richiede indicatore CodeLens:

* Hello modifiche assoluto e percentuale in numero di richieste, le richieste non riuscite e tempi di risposta medio su hello oltre 24 ore rispetto toohello precedenti a 24 ore
* affidabilità di Hello del metodo hello, calcolato come percentuale hello di richieste che hanno avuto esito positivo in hello nelle ultime 24 ore
* Scegliere **ricerca** richieste o richieste non riuscite tooquery tutti hello richieste (non riuscite) che si sono verificati in hello nelle ultime 24 ore
* Scegliere **tendenza** tooview una visualizzazione di tendenza per le richieste, le richieste non riuscite o medio di risposta volte in hello nelle ultime 24 ore.
* Scegliere il nome di hello della risorsa di Application Insights hello in hello nell'angolo superiore sinistro della visualizzazione dei dettagli di hello CodeLens toochange la risorsa è origine hello per i dati CodeLens.

## <a name="next"></a>Passaggi successivi
|  |  |
| --- | --- |
| **[Uso di Application Insights in Visual Studio](app-insights-visual-studio.md)**<br/>Ricerca sui dati di telemetria, visualizzazione dei dati in CodeLens e configurazione di Application Insights. Tutto in Visual Studio. |![Fare clic sul progetto hello e scegliere di Application Insights, ricerca](./media/app-insights-visual-studio-codelens/34.png) |
| **[Aggiungere altri dati](app-insights-asp-net-more.md)**<br/>Monitorare l'utilizzo, la disponibilità, le dipendenze e le eccezioni, integrare le tracce dei framework di registrazione e scrivere telemetria personalizzata. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Utilizzo di portale Application Insights hello](app-insights-dashboards.md)**<br/>Dashboard, strumenti avanzati di diagnostica e di analisi, avvisi, mappa attiva delle dipendenze dell'applicazione ed esportazione dei dati di telemetria. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |


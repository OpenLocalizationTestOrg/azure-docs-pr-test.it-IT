---
title: aaaInteract con i report utilizzando l'API JavaScript hello | Documenti Microsoft
description: Power BI incorporato, interagire con i report utilizzando hello API JavaScript
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Interagire con i report di Power BI usando hello API JavaScript
Consente di API di Power BI JavaScript Hello è tooeasily incorporare i report di Power BI nelle applicazioni. Con hello API, le applicazioni a livello di codice possono interagire con gli elementi di report diverso come pagine e filtri. Grazie a questa interattività i report di Power BI si integrano ancora meglio nell'applicazione.

Incorporare un report di Power BI nell'applicazione usando un iframe ospitato come parte di un'applicazione hello. Hello iframe funge da confine tra l'applicazione e i report di hello, come può vedere nella seguente immagine hello. 

![Iframe di Power BI Embedded senza l'API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

Hello iframe rende hello incorporamento processo molto più semplice, ma senza hello API JavaScript hello report e l'applicazione non può interagire tra loro. La mancanza di interazione può rendere ha l'impressione hello report non è effettivamente parte di un'applicazione hello. applicazione e i report di hello è davvero necessario toocommunicate avanti e indietro, come illustrato di seguito immagine hello.

![Iframe di Power BI Embedded con l'API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

API di Power BI JavaScript Hello consente codice toowrite in modo sicuro può passare attraverso il limite di iframe hello. In questo modo l'applicazione tooprogrammatically eseguire un'azione in un report e toolisten per gli eventi da azioni che gli utenti all'interno di report hello.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>Cosa si può fare con l'API di Power BI JavaScript hello?
Con hello API JavaScript è possibile gestire i report, esplorare toopages in un report, filtrare un report e gestire gli eventi di incorporamento. Hello diagramma seguente mostra la struttura hello di hello API.

![Diagramma dell'API JavaScript per Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Gestire i report
Hello API Javascript consente toomanage comportamento a livello di pagina e report hello:

* Incorporare in modo sicuro un determinato Report di Power BI in un'applicazione - provare a hello [incorporare applicazione demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Impostare il token di accesso
* Configurare i report di hello
  * Abilitare e disabilitare il riquadro filtro hello e riquadro di spostamento - provare a hello [applicazione demo di impostazioni di aggiornamento](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Impostare i valori predefiniti per le pagine e filtri - provare a hello [demo di set di impostazioni predefinite](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Entrare e uscire dalla modalità schermo intero

[Altre informazioni sull'incorporamento di un report](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Passare toopages in un report
Hello API JavaScript enbales toodiscover per tutte le pagine nel report e tooset hello pagina corrente. Provare a hello [applicazione demo navigazione](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Altre informazioni sullo spostamento tra le pagine](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Filtrare un report
Hello API JavaScript fornisce una base e avanzate di filtraggio dei report incorporati e le pagine del report. Provare a hello [filtro applicazione demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)ed esaminare alcuni introduttivo qui il codice.  

#### <a name="basic-filters"></a>Filtri di base
Un filtro di base si trova in un livello di colonna o una gerarchia e contiene un elenco di valori tooinclude o exclude.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Filtri avanzati
Filtri avanzati utilizzano l'operatore logico hello e o OR e accettare le condizioni di uno o due, ognuna con i propri operatore e il valore. Le condizioni supportate sono:

* None
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contiene
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[Altre informazioni sui filtri](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Gestione degli eventi
Inoltre informazioni toosending in iframe hello, l'applicazione può anche ricevere informazioni su hello dopo gli eventi generati dalle hello iframe:

* Embed
  * loaded
  * error
* Report
  * pageChanged
  * dataSelected (presto disponibile)

[Altre informazioni sulla gestione degli eventi](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su hello API JavaScript di Power BI, vedere hello seguenti collegamenti:

* [JavaScript API Wiki (Wiki sull'API JavaScript)](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Object model reference (Informazioni di riferimento sul modello a oggetti)](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Esempi
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Live demo (Demo live)](https://microsoft.github.io/PowerBI-JavaScript/demo/)


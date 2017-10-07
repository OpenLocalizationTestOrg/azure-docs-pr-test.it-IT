---
title: ambiente di Azure ora serie Insights di aaaAdd riferimento set di dati tooyour | Documenti Microsoft
description: In questa esercitazione si aggiunta ambiente ora serie Insights tooyour set di dati di riferimento
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Creare un set di dati di riferimento per l'ambiente di tempo serie Insights utilizzando portale Ibiza hello

Un Set di dati di riferimento è una raccolta di elementi che sono dotati di eventi di hello dall'origine evento. Il motore in ingresso di Time Series Insights esegue il join di un evento dell'origine evento con un elemento del set di dati di riferimento. Questo evento aumentato sarà quindi disponibile per le query. Questo join è basato su chiavi hello definite nel set di dati di riferimento.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Tooadd passaggi dell'ambiente tooyour un set di dati di riferimento

1. Accedi toohello [portale Ibiza](https://portal.azure.com).
2. Fare clic su "Tutte le risorse" nel menu hello sul lato sinistro di hello del portale Ibiza hello.
3. Selezionare l'ambiente Time Series Insights.

    ![Creare set di dati di riferimento ora serie Insights hello](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Selezionare "Set di dati di riferimento" e fare clic su "+ Aggiungi".

    ![Creare set di dati riferimento ora serie Insights hello - dettagli](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Specificare il nome di hello hello riferimento del set di dati.
6. Specificare un nome della chiave hello e il relativo tipo. Questo nome e il tipo è proprietà corretta di hello toopick utilizzato dall'evento hello nell'origine evento. Ad esempio, se si forniscono come "DeviceId" nome della chiave e tipo "String", quindi hello ora serie Insights motore in ingresso esegue la ricerca di una proprietà con nome hello "DeviceId" di tipo "String" in caso di hello in arrivo. È possibile fornire più toojoin chiave evento hello. corrispondenza del nome di proprietà Hello è tra maiuscole e minuscole.

     ![Creare set di dati riferimento ora serie Insights hello - dettagli](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Fare clic su "Crea".

## <a name="next-steps"></a>Passaggi successivi

* [Gestire i dati di riferimento](time-series-insights-manage-reference-data-csharp.md) a livello di codice.
* Per hello riferimento completo alle API, vedere [API di dati di riferimento](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) documento.

---
title: aaaHow tooscale ambiente Azure ora serie Insights | Documenti Microsoft
description: Questa esercitazione sono trattati come tooscale l'ambiente Azure ora serie Insights
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Come tooscale ambiente ora serie Insights

Questa esercitazione sono trattati come tooscale ambiente ora serie Insights.

> [!NOTE]
> La scalabilità verticale tra i tipi di SKU non è consentita. Un ambiente con uno SKU S1 non può essere convertito in un ambiente S2.

## <a name="s1-sku-ingress-rates-and-capacities"></a>Capacità e velocità di ingresso dello SKU S1

| Capacità SKU S1 | Velocità in ingresso | Capacità massima di archiviazione
| --- | --- | --- |
| 1 | 1 GB (1 milione di eventi) | 30 GB (30 milioni di eventi) al mese |
| 10 | 10 GB (10 milioni di eventi) | 300 GB (300 milioni di eventi) al mese |

## <a name="s2-sku-ingress-rates-and-capacities"></a>Capacità e velocità di ingresso dello SKU S2

| Capacità SKU S2 | Velocità in ingresso | Capacità massima di archiviazione
| --- | --- | --- |
| 1 | 10 GB (10 milioni di eventi) | 300 GB (300 milioni di eventi) al mese |
| 10 | 100 GB (100 milioni di eventi) | 3 TB (3 miliardi di eventi) al mese |

La capacità ha una scalabilità lineare, pertanto uno SKU S1 con capacità 2 supporta una velocità in ingresso di 2 GB (2 milioni) di eventi al giorno e 60 GB (60 milioni) di eventi al mese.

## <a name="changing-hello-capacity-of-your-environment"></a>Capacità di hello dell'ambiente di modifica

1. Nel portale di Azure hello, selezionare hello ambiente la cui capacità desiderate toochange.
1. In Impostazioni fare clic su Configura.
1. Utilizzare hello capacità dispositivo di scorrimento tooselect hello capacità che soddisfa i requisiti di hello per le tariffe in ingresso e la capacità di archiviazione.

## <a name="next-steps"></a>Passaggi successivi

* Verificare che sia sufficiente nuova capacità di hello tooprevent la limitazione delle richieste. Per ulteriori informazioni, vedere hello *ambiente potrebbe essere recupero limitata* sezione [qui](time-series-insights-diagnose-and-solve-problems.md).

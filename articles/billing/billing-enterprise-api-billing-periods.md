---
title: aaaAzure fatturazione API Enterprise - periodi di fatturazione | Documenti Microsoft
description: Informazioni sulle API di creazione di report che consentono di dati relativi al consumo toopull clienti Azure Enterprise a livello di codice hello.
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>API di creazione report per clienti Enterprise - Periodi di fatturazione

API di periodi di fatturazione Hello restituisce un elenco di fatturazione periodi che dispongono di dati di utilizzo per hello specificato registrazione in ordine cronologico inverso. Ogni periodo contiene una proprietà che punta route API toohello per quattro set di dati - BalanceSummary, UsageDetails, gli addebiti Marktplace e PriceSheet di hello. Se il periodo di hello non dispone di dati, la proprietà corrispondente hello è null. 


##<a name="request"></a>Richiesta 
Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md). 

|Metodo | URI della richiesta|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.
>

## <a name="response"></a>Response
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**Definizioni delle proprietà di risposta**

|Nome proprietà| Tipo| Descrizione
|-|-|-|
|billingPeriodId| string| Hello Id univoco che rappresenta un determinato periodo di fatturazione|
|billingStart| datetime| Stringa ISO 8601 che rappresenta la data di inizio periodo hello|
|billingEnd| datetime| Stringa ISO 8601 che rappresenta la data di fine periodo hello|
|balanceSummary| string| percorso URL Hello che indirizza i dati di riepilogo saldi toohello per questo periodo|
|usageDetails| string| percorso URL Hello che indirizza i dati di utilizzo dettagli toohello per questo periodo|
|marketplaceCharges| string| percorso URL Hello che indirizza i dati di Marketplace addebiti toohello per questo periodo|
|priceSheet| string| percorso URL Hello che indirizza i dati di PriceSheet toohello per questo periodo|

<br/>
## <a name="see-also"></a>Vedere anche

* [API per saldi e riepilogo](billing-enterprise-api-balance-summary.md)

* [API per dettagli sull'uso](billing-enterprise-api-usage-detail.md) 

* [API per spese per il Marketplace Store](billing-enterprise-api-marketplace-storecharge.md) 

* [API per l'elenco prezzi](billing-enterprise-api-pricesheet.md)
---
title: aaaAzure fatturazione API Enterprise - PriceSheet | Documenti Microsoft
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>API di creazione di report per clienti Enterprise - Elenco prezzi

Hello prezzo foglio API fornisce tasso hello per ogni misuratore di hello dato periodo di fatturazione e di registrazione.

##<a name="request"></a>Richiesta
Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md). Se non viene specificato un periodo di fatturazione, dati di fatturazione corrente hello periodo viene quindi restituiti.

|Metodo | URI della richiesta|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet|

> [!Note]
> versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.
>

## <a name="response"></a>Response

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Se si utilizza hello anteprima API, il campo ID misuratore non è disponibile.
>

**Definizioni delle proprietà di risposta**

|Nome proprietà| Tipo| Descrizione
|-|-|-|
|id| string| Hello Id univoco che rappresenta un particolare elemento PriceSheet (misuratore dal periodo di fatturazione)|
|billingPeriodId| string| Hello Id univoco che rappresenta un determinato periodo di fatturazione|
|meterId| string| Identificatore Hello misuratore hello. Può essere mappato toohello ID misuratore di utilizzo.|
|meterName| string| nome del misuratore Hello|
|unitOfMeasure| string| Hello unità di misura per la misurazione servizio hello|
|includedQuantity| decimal| Quantità inclusa |
|partNumber| string| numero di parte Hello associato hello misuratore|
|unitPrice| decimal| prezzo unitario Hello per metro hello|
|currencyCode| string| codice di valuta Hello per unitPrice hello|
<br/>
## <a name="see-also"></a>Vedere anche

* [API per periodi di fatturazione](billing-enterprise-api-billing-periods.md)

* [API per dettagli sull'uso](billing-enterprise-api-usage-detail.md)

* [API per saldi e riepilogo](billing-enterprise-api-balance-summary.md)

* [API per spese per il Marketplace Store](billing-enterprise-api-marketplace-storecharge.md)

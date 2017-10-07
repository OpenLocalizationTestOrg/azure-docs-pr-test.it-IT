---
title: aaaAzure fatturazione API Enterprise - bilanciamento e riepilogo | Documenti Microsoft
description: Informazioni sull'utilizzo di fatturazione di Azure e APIs RateCard, che sono utilizzati tooprovide approfondite consumo delle risorse di Azure e le tendenze.
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>API di creazione report per clienti Enterprise - Saldi e riepilogo

Hello bilanciamento e API riepilogo offre un riepilogo di informazioni sulle saldi nuovi acquisti, Azure Marketplace spese, regolazioni e spese eccedenza mensile.


##<a name="request"></a>Richiesta 
Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md). Se non viene specificato un periodo di fatturazione, dati di fatturazione corrente hello periodo viene quindi restituiti.

|Metodo | URI della richiesta|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary|

> [!Note]
> versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.
>

## <a name="response"></a>Response

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


**Definizioni delle proprietà di risposta**

|Nome proprietà| Tipo| Descrizione
|-|-|-|
|id|string|Hello Id univoco per un determinato periodo di fatturazione e la registrazione|
|billingPeriodId|string |ID del periodo di fatturazione Hello|
|currencyCode|string |codice di valuta Hello|
|beginningBalance|decimal| Saldo iniziale Hello per periodo di fatturazione hello|
|endingBalance|decimal| Hello saldo finale per periodo di fatturazione hello (per periodi di aprire che questo verrà aggiornato quotidianamente)|
|newPurchases|decimal| Totale nuovo importo di acquisto|
|adjustments|decimal| Quantità totale rettificata|
|utilized|decimal| Uso totale dell'impegno|
|serviceOverage|decimal| Eccedenza per i servizi di Azure|
|chargesBilledSeparately|decimal| chargesBilledSeparately|
|totalOverage|decimal| serviceOverage + chargesBilledSeparately|
|totalUsage|decimal| Eccedenza totale + impegno servizio di Azure|
|azureMarketplaceServiceCharges|decimal| Spese totali per Azure Marketplace|
|newPurchasesDetails|Matrice di stringhe JSON di coppie nome-valore|Elenco di nuovi acquisti|
|adjustmentDetails|Matrice di stringhe JSON di coppie nome-valore|Elenco di modifiche (credito promo, credito SIE e così via) |


<br/>
## <a name="see-also"></a>Vedere anche

* [API per periodi di fatturazione](billing-enterprise-api-billing-periods.md)

* [API per dettagli sull'uso](billing-enterprise-api-usage-detail.md) 

* [API per spese per il Marketplace Store](billing-enterprise-api-marketplace-storecharge.md) 

* [API per l'elenco prezzi](billing-enterprise-api-pricesheet.md)
---
title: aaaAzure API Enterprise fatturazione - spese Marketplace | Documenti Microsoft
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>API di creazione report per clienti Enterprise - Spese per il Marketplace Store

Hello Marketplace archivio addebito API restituisce hello basata sull'utilizzo di marketplace addebiti suddivisione giorno per hello specificato il periodo di fatturazione o date di inizio e fine (non sono inclusi i costi di una volta).

##<a name="request"></a>Richiesta 
Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md). Se non viene specificato un periodo di fatturazione, dati di fatturazione corrente hello periodo viene quindi restituiti. Gli intervalli di tempo personalizzato possono essere specificati con inizio hello e terminano i parametri di data che sono in fase di hello formato AAAA-MM-GG, hello massimo supportato è compreso tra 36 mesi.  

|Metodo | URI della richiesta|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.
>

## <a name="response"></a>Response
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**Definizioni delle proprietà di risposta**

|Nome proprietà| Tipo| Descrizione
|-|-|-|
|id|string|Id univoco per l'elemento di addebito hello marketplace|
|subscriptionGuid|Guid|Hello Guid della sottoscrizione|
|subscriptionName|string|Nome della sottoscrizione Hello|
|meterId|string|ID per hello generato misuratore|
|usageStartDate|DateTime|Ora di inizio per i record di utilizzo hello|
|usageEndDate|DateTime|Ora di fine per il record di utilizzo hello|
|offerName|string|nome dell'offerta Hello|
|resourceGroup|string|risorsa Hello gruppo|
|instanceId|string|ID istanza|
|additionalInfo|string|Stringa JSON per informazioni aggiuntive|
|tags|string|Stringa JSON di tag|
|orderNumber|string|numero di ordine Hello|
|unitOfMeasure|string|Unità di misura del misuratore hello|
|costCenter|string|centro di costo Hello|
|accountId|int|account Hello Id|
|accountName|string |Nome dell'Account Hello|
|accountOwnerId|string|Hello Id proprietario di Account|
|departmentId|int|reparto di Hello Id|
|departmentName|string|nome del reparto Hello|
|publisherName|string|nome dell'autore Hello|
|planName|string|nome del piano di Hello|
|consumedQuantity|decimal|Quantità consumata durante il periodo di tempo|
|resourceRate|decimal|Prezzo unitario per metro hello|
|extendedCost|decimal|Spesa prevista in base alla quantità usata e al costo esteso|
<br/>
## <a name="see-also"></a>Vedere anche

* [API per periodi di fatturazione](billing-enterprise-api-billing-periods.md)

* [API per dettagli sull'uso](billing-enterprise-api-usage-detail.md) 

* [API per saldi e riepilogo](billing-enterprise-api-balance-summary.md)

* [API per l'elenco prezzi](billing-enterprise-api-pricesheet.md)
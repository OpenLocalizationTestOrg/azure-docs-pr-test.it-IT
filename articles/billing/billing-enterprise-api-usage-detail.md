---
title: aaaAzure fatturazione API Enterprise - dettagli | Documenti Microsoft
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>API di creazione di report per i clienti Enterprise - Dettagli di utilizzo

Hello API dettagli utilizzo offre una suddivisione giornaliera delle quantità consumate e spese stimate da una registrazione. risultato Hello include anche informazioni sulle istanze, misuratori e reparti. Hello API può essere determinata in base al periodo di fatturazione o da un inizio specificato e la data di fine. 
## <a name="consumption-apis"></a>API per l'uso


##<a name="request"></a>Richiesta 
Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md). Se non viene specificato un periodo di fatturazione, dati di fatturazione corrente hello periodo viene quindi restituiti. Gli intervalli di tempo personalizzato possono essere specificati con inizio hello e terminano i parametri di data in hello formato AAAA-MM-GG. intervallo di tempo supportato massimo Hello è 36 mesi.  

|Metodo | URI della richiesta|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails 
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.
>

## <a name="response"></a>Response

> A causa di toohello volume potenzialmente elevato di risultati hello data set viene eseguito il paging. proprietà nextLink Hello, se presente, specifica il collegamento hello per la pagina di dati successiva hello. Se il collegamento hello è vuoto, indica che è hello ultima pagina. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Definizioni delle proprietà di risposta**

|Nome proprietà| Tipo| Descrizione
|-|-|-|
|id| string| Hello Id univoco per la chiamata API hello. |
|data| Matrice JSON| Matrice di dettagli di utilizzo giornaliero per ogni instance\meter Hello.|
|nextLink| string| Quando sono presenti più pagine di dati hello nextLink punti toohello URL tooreturn hello pagina successiva di dati. |
|accountId| int| Campo obsoleto. Presente per compatibilità con le versioni precedenti. |
|productId| int| Campo obsoleto. Presente per compatibilità con le versioni precedenti. |
|resourceLocationId| int| Campo obsoleto. Presente per compatibilità con le versioni precedenti. |
|consumedServiceID| int| Campo obsoleto. Presente per compatibilità con le versioni precedenti. |
|departmentId| int| Campo obsoleto. Presente per compatibilità con le versioni precedenti. |
|accountOwnerEmail| string| Account di posta elettronica del proprietario dell'account hello. |
|accountName| string| Nome del cliente immesso dell'account hello. |
|serviceAdministratorId| string| Indirizzo di posta elettronica dell'amministratore del servizio. |
|subscriptionId| int| Campo obsoleto. Presente per compatibilità con le versioni precedenti. |
|subscriptionGuid| string| Identificatore univoco globale per la sottoscrizione di hello. |
|subscriptionName| string| Nome della sottoscrizione hello. |
|date| string| Data di Hello in cui si è verificato il consumo. |
|product| string| Ulteriori dettagli sul misuratore hello. Esempio: A1(VM)Windows - Asia Pacifico orientale|
|meterId| string| Identificatore Hello misuratore hello che emessi utilizzo. |
|meterCategory| string| Hello servizio piattaforma Azure che è stato utilizzato. |
|meterSubCategory| string| Definisce i tipo di servizio di Azure hello che possono influire sulla velocità di hello. Esempio: A1 VM (non Windows)|
|meterRegion| string| Identifica il percorso di hello del Data Center hello per alcuni servizi che i prezzi variano in base alla posizione Data Center. |
|meterName| string| Nome del misuratore hello. |
|consumedQuantity| double| quantità di Hello del misuratore hello che è stato utilizzato. |
|resourceRate| double| frequenza di Hello applicabile per unità fatturabile. |
|cost| double| addebito Hello che è stato sostenuto per metro hello. |
|resourceLocation| string| Identifica i Data Center hello in cui è in esecuzione misuratore hello. |
|consumedService| string| Hello servizio piattaforma Azure che è stato utilizzato. |
|instanceId| string| Questo identificatore è il nome di hello della risorsa di hello o hello completo di ID di risorsa. Per altre informazioni, vedere l'[API di Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|serviceInfo1| string| Metadati del servizio di Azure interno. |
|serviceInfo2| string| Ad esempio, un tipo di immagine per una macchina virtuale e un nome di ISP per ExpressRoute. |
|additionalInfo| string| Metadati specifici del servizio. Ad esempio un tipo di immagine per una macchina virtuale. |
|tags| string| Tag aggiunti dal cliente. Per altre informazioni, vedere [Organize your Azure resources with tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags) (Organizzare le risorse di Azure con i tag). |
|storeServiceIdentifier| string| Questa colonna non viene usata. Presente per compatibilità con le versioni precedenti. |
|departmentName| string| Nome del reparto hello. |
|costCenter| string| centro di costo Hello associato all'utilizzo di hello. |
|unitOfMeasure| string| Identifica le unità hello addebitato servizio hello. Esempio: GB, ore, decine di migliaia. |
|resourceGroup| string| gruppo di risorse Hello in cui hello misuratore distribuito è in esecuzione in. Per altre informazioni, vedere [Panoramica di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Vedere anche

* [API per periodi di fatturazione](billing-enterprise-api-billing-periods.md)

* [API per saldi e riepilogo](billing-enterprise-api-balance-summary.md)

* [API per spese per il Marketplace Store](billing-enterprise-api-marketplace-storecharge.md) 

* [API per l'elenco prezzi](billing-enterprise-api-pricesheet.md)

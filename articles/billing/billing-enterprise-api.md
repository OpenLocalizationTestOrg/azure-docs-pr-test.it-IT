---
title: aaaAzure fatturazione Enterprise API | Documenti Microsoft
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Panoramica delle API di creazione di report per i clienti Enterprise
Hello Reporting API abilitare Azure Enterprise clienti tooprogrammatically pull consumo e dati di fatturazione in strumenti di analisi di dati preferito. 

## <a name="enabling-data-access-toohello-api"></a>L'abilitazione delle API toohello di accesso ai dati
* **Generare o recuperare la chiave API hello** - Log in toohello Enterprise portal e seguire hello esercitazione nella Guida in linea - API di Reporting. Hello prima sezione in questo articolo illustra come toogenerate o recuperare chiave hello API hello specificato registrazione.
* **Passando le chiavi API hello** -chiave hello API deve toobe passato per ogni chiamata per l'autenticazione e autorizzazione. le proprietà seguenti Hello deve intestazioni HTTP toohello toobe

|Chiave intestazione necessaria | Valore|
|-|-|
|Authorization| Specificare il valore di hello nel formato: **bearer {API_KEY}** <br/> Esempio: bearer eyr....09|

## <a name="consumption-apis"></a>API per l'uso
È disponibile un endpoint Swagger [qui](https://consumption.azure.com/swagger/ui/index) per hello API descritte sotto delle quali deve abilitare introspezione semplice di hello API e SDK per applicazioni client toogenerate possibilità di hello utilizzando [AutoRest](https://github.com/Azure/AutoRest) o [ Swagger CodeGen](http://swagger.io/swagger-codegen/). I dati a partire dal 1° maggio 2014 sono disponibili tramite questa API. 

* **Saldo e riepilogo** : hello [bilanciamento e API riepilogo](billing-enterprise-api-balance-summary.md) offre un riepilogo di informazioni sulle saldi, nuovi acquisti, spese di servizio di Azure Marketplace, regolazioni e spese eccedenza mensile.

* **Dettagli utilizzo** : hello [API dettagli utilizzo](billing-enterprise-api-usage-detail.md) offre una suddivisione giornaliera delle quantità consumate e spese stimate da una registrazione. risultato Hello include anche informazioni sulle istanze, misuratori e reparti. Hello API può essere determinata in base al periodo di fatturazione o da un inizio specificato e la data di fine. 

* **Archivio Marketplace addebito** : hello [Marketplace archivio addebito API](billing-enterprise-api-marketplace-storecharge.md) restituisce suddivisione spese marketplace basata sull'utilizzo di hello al giorno per hello specificato il periodo di fatturazione o date di inizio e fine (non sono inclusi i costi di una volta) .

* **Prezzi** : hello [prezzo foglio API](billing-enterprise-api-pricesheet.md) fornisce tasso hello per ogni misuratore di hello dato periodo di fatturazione e di registrazione. 

## <a name="helper-apis"></a>API di supporto
 **Elenco di periodi di fatturazione** : hello [API periodi di fatturazione](billing-enterprise-api-billing-periods.md) restituisce un elenco di fatturazione periodi che dispongono di dati di utilizzo per hello specificato registrazione in ordine cronologico inverso. Ogni periodo contiene una proprietà che punta route API toohello per quattro set di dati - BalanceSummary, UsageDetails, Marketplace costi e prezzi di hello.


## <a name="api-response-codes"></a>Codici di risposta dell'API  
|Codice di stato della risposta|Message|Descrizione|
|-|-|-|
|200| OK|Nessun errore|
|401| Non autorizzata| Chiave API non trovata, non valida, scaduta e così via|
|404| Non disponibile| Endpoint del report non trovato|
|400| Bad Request| Parametri non validi (intervalli di date, numeri EA e così via)|
|500| Errore del server| Errore imprevisto nell'elaborazione della richiesta| 










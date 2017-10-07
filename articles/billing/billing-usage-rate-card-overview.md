---
title: aaaAzure fatturazione API | Documenti Microsoft
description: Informazioni sull'utilizzo di fatturazione di Azure e APIs RateCard, che sono utilizzati tooprovide approfondite consumo delle risorse di Azure e le tendenze.
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Utilizzare le API di fatturazione di Azure tooprogrammatically conoscenza approfondita dell'utilizzo di Azure
Utilizzare i dati di utilizzo e risorse toopull le API di fatturazione di Azure in strumenti di analisi di dati preferito. Hello dell'utilizzo delle risorse di Azure e RateCard APIs consente di prevedere con precisione e gestire i costi. Hello API vengono implementati come parte della famiglia di hello di API esposte dal hello Gestione risorse di Azure e Provider di risorse.  

## <a name="azure-invoice-download-api-preview"></a>API per il download della fattura in Azure (anteprima)
Una volta hello [opt-in è stata completata](billing-manage-access.md#opt-in), utilizzando la versione di anteprima hello di fatture di download [fattura API](/rest/api/billing). le funzionalità di Hello includono:

* **Role-based Access Control di Azure** -configurare l'accesso criteri su hello [portale di Azure](https://portal.azure.com) o tramite [cmdlet di Azure PowerShell](/powershell/azure/overview) toospecify possono accedere gli utenti o applicazioni dati sull'utilizzo della sottoscrizione toohello. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Aggiungere hello chiamante tooeither hello fatturazione lettura, lettura, proprietario o collaboratore ruolo tooget accesso toohello dati di utilizzo per una sottoscrizione di Azure specifico.
* **Filtro data** -hello utilizzare `$filter` tooget parametro tutte le fatture hello in ordine cronologico inverso da hello data di fine periodo di fatturazione. 

> [!NOTE]
> Questa funzionalità è nella prima versione di anteprima e potrebbe essere modifiche toobackward incompatibile soggetto. Attualmente, non è disponibile per alcune offerte di sottoscrizione, EA, CSP e AIO non sono supportati, e in Azure Germania.

## <a name="azure-resource-usage-api-preview"></a>API di utilizzo delle risorse di Azure (anteprima)
Hello utilizzare Azure [API di utilizzo delle risorse](https://msdn.microsoft.com/library/azure/mt219003) tooget i dati a consumo Azure stimato. Hello API include:

* **Role-based Access Control di Azure** -configurare l'accesso criteri su hello [portale di Azure](https://portal.azure.com) o tramite [cmdlet di Azure PowerShell](/powershell/azure/overview) toospecify possono accedere gli utenti o applicazioni dati sull'utilizzo della sottoscrizione toohello. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Aggiungere hello chiamante tooeither hello fatturazione lettura, lettura, proprietario o collaboratore ruolo tooget accesso toohello dati di utilizzo per una sottoscrizione di Azure specifico.
* **Aggregazioni orarie o giornaliere** : i chiamanti possono specificare se desiderano i dati di utilizzo di Azure in intervalli orari o giornalieri. valore predefinito di Hello è giornaliero.
* **I metadati dell'istanza (inclusi i tag delle risorse)** -ottenere i dettagli a livello di istanza come uri di risorsa completo hello (/Subscriptions/<ID {id sottoscrizione} /...), hello informazioni sul gruppo di risorse e i tag delle risorse. Questi metadati consentono in modo deterministico e allocare tag hello, per casi di utilizzo come Ricarica tra utilizzo a livello di codice.
* **I metadati di Resource** -Dettagli risorsa, ad esempio nome misuratore hello, misuratore categoria, sottocategoria misuratore, unità e area assegnare chiamante hello una migliore comprensione di ciò che è stato elaborato. Diverse anche collaborazioni terminologia dei metadati di risorsa tooalign hello portale di Azure, Azure-utilizzo CSV, EA CSV, di fatturazione e altre esperienze pubblico, toolet correlare dati esperienze.
* **Utilizzo per tutti i tipi di offerte** : i dati di utilizzo sono accessibili per tutti i tipi di offerta, tra cui il pagamento in base al consumo, MSDN, l’impegno monetario, il credito monetari ed EA.

## <a name="azure-resource-ratecard-api-preview"></a>API RateCard delle risorse di Azure (anteprima)
Hello utilizzare [API RateCard risorse di Azure](https://msdn.microsoft.com/library/azure/mt219005) tooget hello elenco risorse di Azure disponibili e le informazioni sui prezzi stimate per ogni. Hello API include:

* **Role-based Access Control di Azure** -configurazione dei criteri di accesso su hello [portale di Azure](https://portal.azure.com) o tramite [cmdlet di Azure PowerShell](/powershell/azure/overview) toospecify possono accedere gli utenti o applicazioni toohello RateCard dati. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Aggiungere hello chiamante tooeither hello lettore, il proprietario o collaboratore ruolo tooget accesso toohello dati di utilizzo per una sottoscrizione di Azure specifico.
* **Supporto delle offerte con pagamento in base al consumo, MSDN, impegno monetario e credito monetario (EA non supportato)** : questa API fornisce informazioni sulle tariffe a livello di offerta di Azure.  il chiamante Hello di questa API deve passare tariffe e i dettagli delle risorse hello offerta informazioni tooget. Siamo tariffe EA tooprovide attualmente non è possibile perché EA offre sono personalizzate le tariffe per la registrazione. 

## <a name="scenarios"></a>Scenari
Ecco alcuni degli scenari di hello che sono possibili con combinazione hello di hello utilizzo e hello RateCard APIs:

* **Spesa di Azure durante il mese di hello** -combinazione hello uso di hello informazioni sull'utilizzo e RateCard APIs tooget una visione migliore in cloud di spesa mese hello. È possibile analizzare hello oraria e giornaliera bucket di utilizzo e il relativo costo stimato.
* **Consente di impostare avvisi** : utilizzare hello utilizzo e hello RateCard APIs tooget stimato il consumo di cloud e le spese e consente di impostare avvisi basato su risorse o valuta.
* **Stimare i costi** – Get del consumo stimato e del cloud spesa e applicare di machine learning toopredict algoritmi quali costi hello sarebbe alla fine hello hello del ciclo di fatturazione.
* **Pre-utilizzo di analisi dei costi** : utilizzare hello API RateCard toopredict quanto fattura sarebbe per l'utilizzo previsto quando si sposta tooAzure i carichi di lavoro. Nel caso di carichi di lavoro esistenti in altri cloud o un cloud privato, è anche possibile mappare l'utilizzo con hello Azure tariffe tooget dedicare una stima più accurata di Azure. In questo modo di stima hello toopivot possibilità offerta, confronto e contrasto tra i tipi di offerta diversa hello oltre a pagamento a consumo, come un impegno monetario e credito monetario. Hello API fornisce inoltre hello possibilità toosee costo differenze per regione e consente toodo un toohelp analisi di simulazione costo di prendere decisioni di distribuzione.
* **Analisi di simulazione** -
  
  * È possibile determinare se è più conveniente toorun carichi di lavoro in un'altra area o in un'altra configurazione di hello risorse di Azure. Risorse di Azure i costi possono differire in base hello regione di Azure in uso.
  * È inoltre possibile determinare se un altro tipo di offerta di Azure offre una tariffa migliore per una risorsa di Azure.
  
## <a name="partner-solutions"></a>Soluzioni partner
[Utilizzo di Microsoft Azure e RateCard API abilitare Cloudyn tooProvide ITFM per i clienti](billing-usage-rate-card-partner-solution-cloudyn.md) descrive l'esperienza di integrazione hello offerto dal partner di API di fatturazione di Azure [Cloudyn](https://www.cloudyn.com/microsoft-azure/). In questo articolo si indica le proprie esperienze e include un video che illustra come è possibile utilizzare Cloudyn e hello insights tooget le API di fatturazione di Azure dai dati di utilizzo di Azure.

[Cloud Cruiser e integrazione di API di fatturazione di Microsoft Azure](billing-usage-rate-card-partner-solution-cloudcruiser.md) viene descritto come [Express del Cloud Cruiser per Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) funziona direttamente dal portale Windows Azure Pack (WAP) hello. Da una singola interfaccia utente, è possibile gestire facilmente gli aspetti operativi e finanziari entrambi hello hello Microsoft cloud di Azure ospitati o privati pubblico.   

## <a name="next-steps"></a>Passaggi successivi
* Vedere gli esempi di codice hello in GitHub:
  * [Esempio di codice API della fattura](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Uso del codice di esempio API](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Codice di esempio API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn ulteriori informazioni su hello Azure Resource Manager, vedere [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md). 

* Per ulteriori informazioni su suite hello degli strumenti spesa toohelp necessarie ottenere la comprensione del cloud, vedere articolo Gartner hello [mercato Guida per gli strumenti di gestione finanziaria IT (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).


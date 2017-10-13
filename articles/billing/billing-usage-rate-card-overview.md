---
title: API di fatturazione di Azure | Microsoft Docs
description: "Informazioni sull'utilizzo dell’API di fatturazione e dell’API RestCard di Azure, utilizzate per offrire informazioni sul consumo di risorse e sulle tendenze di Azure."
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
ms.date: 10/9/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: 26217d6f4e14166a89fbb561cb12d0af78ae6f4d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="use-azure-billing-apis-to-programmatically-get-insight-into-your-azure-usage"></a>Usare le API di fatturazione di Azure per ottenere informazioni approfondite sull'uso di Azure a livello di codice
Usare le API di fatturazione di Azure per raccogliere e immettere i dati di uso e delle risorse negli strumenti di analisi dei dati scelti. Le API di utilizzo delle risorse di Azure e RateCard possono aiutare a prevedere e gestire i costi con precisione. Le API vengono implementate come provider di risorse, nell’ambito della famiglia di API esposte da Azure Resource Manager.  

## <a name="azure-invoice-download-api-preview"></a>API per il download della fattura in Azure (anteprima)
Dopo aver [completato il consenso esplicito](billing-manage-access.md#opt-in), scaricare le fatture tramite la versione di anteprima di [API per le fatture](/rest/api/billing). Le funzionalità includono:

* **Controllo degli accessi in base al ruolo di Azure**: configurare i propri criteri di accesso nel [portale di Azure](https://portal.azure.com) o tramite i [cmdlet di Azure PowerShell](/powershell/azure/overview) per specificare quali utenti o applicazioni possono avere accesso ai dati di utilizzo della sottoscrizione. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Per ottenere l'accesso ai dati di uso per una determinata sottoscrizione di Azure aggiungere il chiamante al ruolo Lettore della fatturazione, Proprietario o Collaboratore.
* **Filtro data**: usare il parametro `$filter` per ottenere tutte le fatture in ordine cronologico inverso in base alla data di fine periodo di fatturazione. 

> [!NOTE]
> Questa funzionalità è nella prima versione di anteprima e può essere soggetta a modifiche incompatibili con le versioni precedenti. Attualmente, non è disponibile per alcune offerte di sottoscrizione, EA, CSP e AIO non sono supportati, e in Azure Germania.

## <a name="azure-resource-usage-api-preview"></a>API di utilizzo delle risorse di Azure (anteprima)
Per ottenere una stima dei dati di consumo di Azure usare l'[API di uso delle risorse](https://msdn.microsoft.com/library/azure/mt219003) di Azure. L'API include:

* **Controllo degli accessi in base al ruolo di Azure**: configurare i propri criteri di accesso nel [portale di Azure](https://portal.azure.com) o tramite i [cmdlet di Azure PowerShell](/powershell/azure/overview) per specificare quali utenti o applicazioni possono avere accesso ai dati di utilizzo della sottoscrizione. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Per ottenere l'accesso ai dati di uso per una determinata sottoscrizione di Azure aggiungere il chiamante al ruolo Lettore della fatturazione, Proprietario o Collaboratore.
* **Aggregazioni orarie o giornaliere** : i chiamanti possono specificare se desiderano i dati di utilizzo di Azure in intervalli orari o giornalieri. L’impostazione predefinita è rappresentata dagli intervalli giornalieri.
* **Metadati dell'istanza (inclusi i tag delle risorse)**: nella risposta vengono forniti i dettagli a livello di istanza, ad esempio l'URI della risorsa completo (/subscriptions/{subscription-id}/..), insieme alle informazioni sul gruppo di risorse e ai tag delle risorse. Tali metadati aiutano gli utenti ad allocare l’utilizzo in modo deterministico e programmatico in base ai tag, per casi di utilizzo come l’addebito delle tariffe.
* **Metadati delle risorse**: dettagli delle risorse, ad esempio il nome, la categoria e la sottocategoria del misuratore, l'unità e l'area, per fornire ai chiamanti una migliore comprensione delle risorse utilizzate. Stiamo inoltre lavorando per allineare la terminologia dei metadati delle risorse nel portale di Azure, il CSV di utilizzo di Azure, il CSV di fatturazione EA e altre esperienze pubbliche, per consentire agli utenti di correlare i dati delle diverse esperienze.
* **Utilizzo per differenti tipi di offerte**: i dati di utilizzo sono accessibili per tutti i tipi di offerta, tra cui il pagamento in base al consumo, MSDN, l’impegno monetario, il credito monetari ed EA, eccetto [CSP](https://docs.microsoft.com/azure/cloud-solution-provider/billing/azure-csp-invoice#retrieve-usage-data-for-a-specific-subscription).

## <a name="azure-resource-ratecard-api-preview"></a>API RateCard delle risorse di Azure (anteprima)
Per ottenere l'elenco delle risorse di Azure disponibili e una stima delle informazioni sul prezzo di ognuna di esse usare l'[API RateCard delle risorse di Azure](https://msdn.microsoft.com/library/azure/mt219005). L'API include:

* **Controllo degli accessi in base al ruolo di Azure**: configurare i propri criteri di accesso nel [portale di Azure](https://portal.azure.com) o tramite i [cmdlet di Azure PowerShell](/powershell/azure/overview) per specificare quali utenti o applicazioni possono avere accesso ai dati di RateCard. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Aggiungere il chiamante al ruolo Lettore, Proprietario o Collaboratore per ottenere l'accesso ai dati di utilizzo per una determinata sottoscrizione di Azure.
* **Supporto delle offerte con pagamento in base al consumo, MSDN, impegno monetario e credito monetario (EA e [CSP](https://docs.microsoft.com/azure/cloud-solution-provider/billing/azure-csp-pricelist#get-prices-by-using-the-azure-rate-card) non supportati)** : questa API fornisce informazioni sulle tariffe a livello di offerta di Azure.  Il chiamante di questa API deve passare le informazioni sull'offerta per dettagli e tariffe delle risorse. Dal momento che le offerte EA hanno tariffe personalizzate in base alla registrazione, al momento non è possibile fornire le tariffe EA. 

## <a name="scenarios"></a>Scenari
Di seguito sono illustrati alcuni scenari resi possibili con la combinazione di API di utilizzo e API RateCard:

* **Spesa di Azure durante il mese**: usare le API di utilizzo e RateCard per ottenere informazioni più approfondite sulle spese mensili legate al cloud. È possibile analizzare i bucket di utilizzo orari e giornalieri e le stime di addebito.
* **Impostare avvisi**: usare le API di utilizzo e RateCard per ottenere una stima dei consumi e degli addebiti legati al cloud e per impostare avvisi basati sulle risorse o sui costi.
* **Previsione delle fatture**: è possibile ottenere le stime sui consumi e sulle spese per il cloud e applicare algoritmi di Machine Learning per prevedere l’importo della fattura al termine del periodo di fatturazione.
* **Analisi dei costi prima del consumo**: usare l'API RateCard per prevedere l'importo della fattura per l'utilizzo quando si spostano i carichi di lavoro in Azure. Se si dispone di carichi di lavoro esistenti in altri cloud o nei cloud privati, è possibile inoltre eseguire il mapping dell'utilizzo con le tariffe di Azure per ottenere una stima più accurata della spesa stimata di Azure. Questa stima offre la possibilità di partire da un'offerta e di confrontarla con le altre disponibili oltre al pagamento in base al consumo, come l'impegno monetario e il credito monteraio. L'API, inoltre, offre la possibilità di visualizzare le differenze di costo per area geografica e consente di eseguire una simulazione dei costi per facilitare le decisioni legate alla distribuzione.
* **Analisi di simulazione** -
  
  * È possibile determinare se è più conveniente eseguire i propri carichi di lavoro in un'altra area o in un'altra configurazione della risorsa di Azure. I costi delle risorse di Azure possono variare in base all'area di Azure in uso.
  * È inoltre possibile determinare se un altro tipo di offerta di Azure offre una tariffa migliore per una risorsa di Azure.
  
## <a name="partner-solutions"></a>Soluzioni partner
In [Cloud Cruiser e integrazione dell'API di fatturazione di Microsoft Azure](billing-usage-rate-card-partner-solution-cloudcruiser.md) viene descritto come la [versione Express di Cloud Cruiser per Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) funzioni direttamente dal portale Windows Azure Pack (WAP), consentendo ai clienti di gestire senza problemi gli aspetti operativi e finanziari del cloud privato o pubblico di Microsoft Azure da una singola interfaccia utente.   

## <a name="next-steps"></a>Passaggi successivi
* Controllare gli esempi di codice su GitHub:
  * [Esempio di codice API della fattura](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Uso del codice di esempio API](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Codice di esempio API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* Per altre informazioni su Azure Resource Manager, vedere [Panoramica di Gestione risorse di Microsoft Azure](../azure-resource-manager/resource-group-overview.md). 

* Per altre informazioni sulla suite di strumenti necessari per conoscere la spesa relativa al cloud, vedere l'articolo di Gartner sulla [Guida di mercato agli strumenti ITFM](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).


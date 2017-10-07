---
title: "aaaLog funzionalità Analitica per i provider di servizi | Documenti Microsoft"
description: Log Analytics aiuta i provider dei servizi gestiti (MSP), le aziende di grandi dimensioni, i fornitori di software indipendenti (ISV) e i provider di servizi di hosting a gestire e monitorare i server nell'infrastruttura cloud o locale del cliente.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Funzionalità di Log Analytics per i provider di servizi
Log Analytics aiuta i provider dei servizi gestiti (MSP), le aziende di grandi dimensioni, i fornitori di software indipendenti (ISV) e i provider di servizi di hosting a gestire e monitorare i server nell'infrastruttura cloud o locale del cliente. 

Le aziende di grandi dimensioni hanno molti punti in comune con i provider di servizi, soprattutto quando c'è un team IT centralizzato che si occupa della gestione dell'IT per molte business unit diverse tra loro. Per semplicità, in questo documento viene utilizzato il termine di hello *provider di servizi* ma hello stessa funzionalità è disponibile anche per le organizzazioni e gli altri clienti.

## <a name="cloud-solution-provider"></a>Provider di soluzioni cloud
Per i partner e i provider di servizi che fanno parte di hello [il Provider di soluzioni Cloud (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) di programma, Log Analitica è uno dei hello Azure servizi disponibili in una sottoscrizione di CSP. 

Per i Log Analitica, hello seguenti funzionalità è abilitata in *Cloud Solution Provider* sottoscrizioni.

In qualità di *Provider di soluzioni cloud* è possibile:

* Creare le aree di lavoro di Log Analytics in una sottoscrizione di un tenant (cliente).
* Accedere alle aree di lavoro create dai tenant. 
* Aggiungere e rimuovere l'utente accesso toohello dell'area di lavoro utilizzando Gestione utente di Azure. Quando nell'area di lavoro di un tenant in hello OMS pagina di gestione di utenti del portale hello in impostazioni non è disponibile
  * Log Analitica non supporta l'accesso basato sui ruoli ancora - concessione a un utente `reader` autorizzazione nel portale di Azure hello consente modifiche alla configurazione toomake nel portale OMS hello

toolog nella sottoscrizione del tenant tooa, è necessario l'identificatore del tenant toospecify hello. Identificatore del tenant Hello è spesso quest'ultima parte di hello posta elettronica indirizzo utilizzato toosign in.

* Nel portale OMS hello, aggiungere `?tenant=contoso.com` hello URL portale hello. Ad esempio, `mms.microsoft.com/?tenant=contoso.com`
* In PowerShell, usare hello `-Tenant contoso.com` parametro quando si utilizza `Add-AzureRmAccount` cmdlet
* Identificatore del tenant Hello viene aggiunto automaticamente quando si utilizza hello `OMS portal` collegamento da hello tooopen portale Azure e di log nel portale OMS toohello per area di lavoro hello selezionato

In qualità di *cliente* di un provider di soluzioni cloud è possibile:

* Creare le aree di lavoro di Log Analytics in una sottoscrizione CSP
* Aree di lavoro di accesso creati da hello CSP
  * Hello utilizzare `OMS portal` collegamento da hello tooopen portale Azure e di log nel portale OMS toohello per area di lavoro hello selezionato
* Visualizzare e utilizzare una pagina di gestione utenti hello in impostazioni nel portale OMS hello

> [!NOTE]
> Hello incluso il Backup e le soluzioni di ripristino del sito per Analitica Log non sono in grado di tooconnect tooa servizi di ripristino archivio e non possono essere configurate in una sottoscrizione di CSP. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Gestione di più clienti che usano Log Analytics
È consigliabile creare un'area di lavoro Log Analytics per ogni cliente gestito. Un'area di lavoro di Log Analytics offre:

* Un'area geografica per toobe dati archiviati. 
* Granularità per la fatturazione 
* Isolamento dei dati 
* Configurazione univoca

Tramite la creazione di un'area di lavoro per ogni cliente, tookeep in grado di dati di ogni cliente separati che può anche tenere traccia dell'utilizzo di hello di ogni cliente.

Ulteriori dettagli su quando e perché toocreate più aree di lavoro descritto in [gestire accesso toolog analitica](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Creazione e configurazione delle aree di lavoro cliente possono essere automatizzate tramite [PowerShell](log-analytics-powershell-workspace-configuration.md), [modelli di gestione risorse](log-analytics-template-workspace-configuration.md), o tramite hello [API REST](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

uso di Hello di modelli di gestione risorse per la configurazione dell'area di lavoro consente toohave una configurazione di master che può essere utilizzati toocreate e configurare aree di lavoro. È possibile essere certi che come aree di lavoro vengono creati per i clienti che sono automaticamente configurati tooyour requisiti. Quando si aggiornano i requisiti, modello hello viene aggiornato e quindi riapplicato aree di lavoro esistenti hello. Questo processo assicura che le aree di lavoro esistenti siano conformi ai nuovi standard.    

Quando si gestiscono più aree di lavoro Log Analitica, è consigliabile che l'integrazione di ogni area di lavoro con il sistema di emissione di ticket esistente console operatore con hello [avvisi](log-analytics-alerts.md) funzionalità. Grazie all'integrazione con i sistemi esistenti, il personale di supporto possono continuare toofollow processi familiarità. Log Analitica regolarmente controlla ogni area di lavoro rispetto ai criteri di avviso hello specificati e genera un avviso quando è necessaria un'azione.

Per le visualizzazioni personalizzate dei dati, utilizzare hello [dashboard](../azure-portal/azure-portal-dashboards.md) funzionalità nel portale di Azure hello.  

Per il livello executive report per riepilogare i dati nelle aree di lavoro è possibile utilizzare hello integrazione tra Log Analitica e [PowerBI](log-analytics-powerbi.md). Se è necessario toointegrate con un altro sistema di creazione di report, è possibile utilizzare hello API di ricerca (tramite PowerShell o [REST](log-analytics-log-search-api.md)) toorun query ed Esporta i risultati di ricerca.

## <a name="next-steps"></a>Passaggi successivi
* Automatizzare la creazione e la configurazione delle aree di lavoro usando i [modelli di Resource Manager](log-analytics-template-workspace-configuration.md)
* Automatizzare la creazione delle aree di lavoro usando [PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Utilizzare [avvisi](log-analytics-alerts.md) toointegrate con i sistemi esistenti
* Generare report di riepilogo usando [Power BI](log-analytics-powerbi.md)


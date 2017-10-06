---
title: aaaUser azione avviata da Azure automazione Runbook nel Log Analitica | Documenti Microsoft
description: In questo articolo viene descritto come un runbook di automazione da un Log di Analitica toorun ricerca risultato su richiesta.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Eseguire operazioni con un runbook di automazione dai risultati della ricerca log di Log Analytics

Da un risultato di ricerca log in Analitica di Log di Azure, è ora possibile selezionare **intervenire** toorun un runbook di automazione.  Hello runbook può essere usato tooremediate hello problema o eseguire altre azioni, ad esempio raccogliere informazioni di risoluzione dei problemi, inviare un messaggio di posta elettronica o creare una richiesta di servizio. 

## <a name="components-and-features-used"></a>Componenti e le funzionalità usati
* [Account di automazione di Azure](../automation/automation-offering-get-started.md)
* [Area di lavoro di Log Analytics](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>runbook tooinitiate da ricerca di log

azione tootake su un evento e avviare un runbook dai risultati della ricerca log, iniziare creando una ricerca log e dai risultati di hello è possibile richiamare un runbook su richiesta.  Ciò può essere ottenuto dalla funzionalità di ricerca log hello in hello Azure o [portale OMS](../log-analytics/log-analytics-log-searches.md).  In questo esempio, si esegue una ricerca di log da hello portale di Azure con una dimostrazione di base di questa funzionalità.

1. Nel portale di Azure hello, nel menu Hub hello fare clic su **più servizi** e selezionare **Analitica Log**.  
2. Nel pannello Log Analitica hello, selezionare l'area di lavoro Log Analitica e nel pannello dell'area di lavoro hello selezionare **ricerca nei Log**.  
3. Nel Pannello di ricerca nei Log hello, eseguire una ricerca di log.  
4. Fare clic su hello ellisse toohello sinistro uno dei campi hello e dal popup hello, selezionare dai risultati di ricerca log hello, **agire**.<br><br> ![Selezione dell'azione di intervento dai risultati della ricerca](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Dal Pannello di azione intraprendere hello, selezionare **eseguire un runbook**e in hello **eseguire un runbook** pannello è possibile selezionare un toorun runbook.  È possibile selezionare qualsiasi runbook nell'account di automazione che è l'area di lavoro collegato toohello Log Analitica hello.  Si noti hello segue:

    * I runbook sono organizzati per tag
    * È possibile selezionare i valori dei parametri di input runbook direttamente dai campi hello del risultato della ricerca hello.  Verrà visualizzato un elenco di riepilogo a discesa la visualizzazione di tutti i campi disponibili hello da hello risultato tooselect da.  
    * È possibile scegliere toorun hello runbook su un [runbook worker ibrido](../automation/automation-hybrid-runbook-worker.md) che sono installati nel computer di hello che si è verificato il problema di hello se si dispone di un gruppo di lavoro ibridi per Runbook corrispondente che contiene solo la macchina come un membro.  Se il nome di hello del gruppo di lavoro ibridi hello corrisponde nome hello del computer hello nei risultati di ricerca log hello, gruppo hello viene selezionato automaticamente.    

6. Dopo aver fatto clic **eseguire**, pannello di processo runbook hello aprirà tooallow si tooreview hello lo stato del processo di hello.   

Se si seleziona un runbook che è stato configurato toobe [chiamato da un avviso di Log Analitica](../automation/automation-invoke-runbook-from-omsla-alert.md), ha un parametro di input denominato **WebhookData** ovvero **oggetto** tipo.  Se il parametro di input hello è obbligatorio, è necessario toopass hello ricerca risultati toohello runbook in modo da stringa in formato JSON hello può convertire in un tipo di oggetto consentono di toofilter per elementi specifici che verranno utilizzati come riferimento nelle attività di runbook.  Questo scopo, selezionare **(oggetto) risultati ricerca** dall'elenco a discesa hello.<br><br> ![Selezionare l'oggetto dati Webhook per il parametro del runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Passaggi successivi

* Hello revisione [riferimento alla ricerca di log Log Analitica](log-analytics-search-reference.md) tooview tutti hello cerca i campi e facet disponibile nel Log Analitica.
* come esaminare automaticamente, un runbook di automazione tooinvoke toolearn [chiamata di un runbook di automazione di Azure da un avviso di OMS Log Analitica](../automation/automation-invoke-runbook-from-omsla-alert.md).  

---
title: Funzioni di Azure aaaMonitoring | Documenti Microsoft
description: Informazioni su come toomonitor delle funzioni di Azure.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Monitoraggio di Funzioni di Azure

## <a name="overview"></a>Panoramica 


Hello **monitoraggio** scheda per ogni funzione consente tooreview ogni esecuzione di una funzione.

![Scheda Monitoraggio di Funzioni di Azure](./media/functions-monitoring/monitor-tab.png) 

Fare clic su un'esecuzione consente si tooreview hello durata, dati di input, gli errori e i file di log associati. Ciò risulta utile per il debug e per l'ottimizzazione delle prestazioni delle funzioni.


> [!IMPORTANT]
> Quando si utilizza hello [consumo piano di hosting](functions-overview.md#pricing) per le funzioni di Azure, hello **monitoraggio** riquadro nel pannello della panoramica App funzione hello non mostreranno alcun dato. In questo modo piattaforma hello viene ridimensionata in modo dinamico e gestisce le istanze di calcolo, pertanto queste metriche non sono significative in un piano di utilizzo. utilizzo di hello toomonitor delle app di funzione, si dovrebbero usare invece indicazioni hello in questo articolo.
> 
> Hello cattura di schermata seguente viene illustrato un esempio:
> 
> ![Il monitoraggio nel Pannello di risorse principale hello](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Monitoraggio in tempo reale

Il monitoraggio in tempo reale è disponibile selezionando il **flusso eventi live**, come illustrato di seguito. 

![Opzione di flusso di eventi per la scheda Monitoraggio hello Live](./media/functions-monitoring/monitor-tab-live-event-stream.png)

flusso di eventi in tempo reale di Hello verrà rappresentata in una nuova scheda del browser come illustrato di seguito. 

![Esempio di flusso eventi live](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Si verifica un problema noto che potrebbe causare il toobe toofail dati popolata. Se ciò si verifica, potrebbe essere necessario tooclose hello browser scheda contenente hello in tempo reale flusso di eventi e quindi fare clic su **flusso di eventi in tempo reale** nuovamente tooallow è tooproperly popolare i dati di flusso di eventi. 

flusso di eventi in tempo reale di Hello verrà graph hello statistiche per la funzione seguente:

* Esecuzioni avviate al secondo
* Esecuzioni completate al secondo
* Esecuzioni non riuscite al secondo
* Tempo di esecuzione medio in millisecondi

Queste statistiche sono in tempo reale, ma hello effettiva rappresentazione grafica dei dati di esecuzione hello dispone di latenza di circa 10 secondi.






## <a name="monitoring-log-files-from-a-command-line"></a>Monitoraggio dei file di log da una riga di comando


È possibile trasmettere sessione della riga di comando tooa i file di log in una workstation locale usando hello Azure interfaccia della riga di comando (CLI) o PowerShell.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Monitoraggio file di log di app di funzione con hello CLI di Azure

avviata, tooget [installare hello CLI di Azure](../cli-install-nodejs.md)

Accedere al proprio account Azure con i seguenti hello comando o uno qualsiasi di hello altre opzioni descritte, [Accedi tooAzure da hello Azure CLI](../xplat-cli-connect.md).

    azure login

Comando che segue hello di utilizzare la modalità di Gestione servizio CLI di Azure (ASM) tooenable:.

    azure config mode asm

Se si dispone di più sottoscrizioni, usare hello toolist i comandi seguenti, i set di hello sottoscrizione toohello sottoscrizione corrente che contiene l'app di funzione e le sottoscrizioni.

    azure account list
    azure account set <subscriptionNameOrId>

Hello comando riportato di seguito verrà al flusso di file di log hello della riga di comando funzione app toohello:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Monitoraggio dei file di log delle app per le funzioni tramite PowerShell

avviata, tooget [installare e configurare Azure PowerShell](/powershell/azure/overview).

Aggiungere l'account di Azure eseguendo hello comando seguente:

    PS C:\> Add-AzureAccount

Se si dispone di più sottoscrizioni, è possibile elencarli in base al nome con hello successivo comando toosee se hello corretto sottoscrizione è hello attualmente selezionato in base a `IsCurrent` proprietà:

    PS C:\> Get-AzureSubscription

Se è necessario tooset hello sottoscrizione attiva toohello quello contenente l'app di funzione, utilizzare hello comando seguente:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Sessione di PowerShell tooyour per i log di hello flusso con hello comando seguente:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Per ulteriori informazioni, vedere troppo[come: flusso di log per le app web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse:

* [Test di Funzioni di Azure](functions-test-a-function.md)
* [Scalabilità di Funzioni di Azure](functions-scale.md)


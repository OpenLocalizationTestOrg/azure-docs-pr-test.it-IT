---
title: un Runbook di automazione di Azure da un avviso di Log Analitica aaaCalling | Documenti Microsoft
description: In questo articolo viene fornita una panoramica di come tooinvoke un runbook di automazione da un avviso di Microsoft OMS Log Analitica.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Chiamata di un runbook di un Automazione di Azure da un avviso di OMS Log Analytics

Quando un avviso è configurato in toocreate Analitica Log un record di avviso se i risultati corrispondono a determinati criteri, ad esempio un picco nell'utilizzo del processore o una funzionalità di un'applicazione aziendale toohello critici un processo particolare applicazione prolungato ha esito negativo e scrive un evento corrispondente nel registro eventi di Windows hello, tale avviso è possibile eseguire automaticamente un runbook di automazione in un tentativo tooauto-correggere il problema di hello.  

Esistono due opzioni toocall un runbook quando si configura avviso hello.  ovvero:

1. Uso di un webhook.
   * Si tratta di hello unica opzione disponibile se l'area di lavoro OMS non è collegato tooan account di automazione.
   * Se si dispone già di un'area di lavoro OMS di automazione account collegato tooan, questa opzione è ancora disponibile.  

2. Selezione diretta di un runbook.
   * Questa opzione è disponibile solo quando l'area di lavoro OMS hello è collegato tooan account di automazione.  

## <a name="calling-a-runbook-using-a-webhook"></a>Chiamata di un runbook mediante un webhook

Un webhook consente toostart un determinato runbook in automazione di Azure tramite una singola richiesta HTTP.  Prima di configurare hello [avviso Analitica Log](../log-analytics/log-analytics-alerts.md#alert-rules) toocall hello runbook utilizzando un webhook come un'azione di avviso, sarà necessario toofirst creare un webhook per runbook hello che verrà chiamato questo metodo.  Esaminare e seguire i passaggi hello hello [creare un webhook](automation-webhooks.md#creating-a-webhook) articolo e ricordare l'URL del webhook toorecord hello in modo che sia possibile utilizzarlo come riferimento durante la configurazione della regola di avviso hello.   

## <a name="calling-a-runbook-directly"></a>Chiamata diretta di un runbook

Se si dispone di hello automazione & offerta controllo installato e configurato nell'area di lavoro OMS, quando si configura l'opzione di azioni hello Runbook per l'avviso hello, è possibile visualizzare tutti i runbook da hello **selezionare un runbook** elenco a discesa Selezionare hello specifico del runbook desiderato toorun nell'avviso toohello di risposta.  Hello selezionato runbook può eseguire in un'area di lavoro in hello cloud di Azure o in un runbook worker ibrido.  Quando l'avviso di hello viene creato utilizzando l'opzione runbook hello, verrà creato un webhook per hello runbook.  Se si passa toohello account di automazione e passa toohello webhook pannello dei runbook hello selezionata, è possibile visualizzare hello webhook.  Se si elimina l'avviso hello, hello webhook non viene eliminato, ma l'utente hello può eliminare il webhook hello manualmente.  Non è un problema se hello webhook non è stato eliminato, è solo un elemento orfano che sarà necessario toobe eliminato nell'ordine toomaintain organizzata di un account di automazione.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Caratteristiche di un runbook (per entrambe le opzioni)

Entrambi i metodi per chiamare hello runbook da avviso Log Analitica hello hanno caratteristiche di un comportamento diverso che è necessario comprendere prima di configurare le regole di avviso toobe.  

* È necessario avere un parametro di input del runbook denominato **WebhookData**, di tipo **Object**.  Questo parametro può essere obbligatorio o facoltativo.  avviso di Hello passa hello ricerca risultati toohello runbook utilizzando il parametro di input.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  È necessario disporre di oggetto di codice tooconvert hello WebhookData tooa PowerShell.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* sarà una matrice di oggetti; ogni oggetto contiene campi hello con i valori di un risultato di ricerca

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData incoerenze tra runbook e hello webhook opzione

* Quando si configura un avviso toocall un Webhook, immettere un URL del webhook creato per un runbook e fare clic su hello **Webhook Test** pulsante.  Hello WebhookData risulta inviato toohello runbook non contiene *. SearchResult* o *. SearchResults*.

*  Se si salva tale avviso, quando l'avviso hello attiva e chiama webhook hello, hello WebhookData inviati toohello runbook contiene *. SearchResult*.
* Se si crea un avviso e configurarlo toocall un runbook (che crea anche un webhook), quando hello allarmi invia WebhookData toohello runbook che contiene *. SearchResults*.

Nell'esempio di codice hello sopra, sarà pertanto necessario tooget *. SearchResult* se chiama un webhook avviso hello e sarà necessario tooget *. SearchResults* se avviso hello chiama un runbook direttamente.

## <a name="example-walkthrough"></a>Procedura dettagliata di esempio

Verrà illustrato il funzionamento tramite hello seguente runbook grafico di esempio, che avvia un servizio Windows.<br><br> ![Avviare il runbook grafico per il servizio di Windows](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Hello runbook dispone di un parametro di input di tipo **oggetto** che viene chiamato **WebhookData** e include dati webhook hello passati da hello avviso contenente *. SearchResults*.<br><br> ![Parametri di input dei runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

Per questo esempio, negli Analitica di Log sono stati creati due campi personalizzati, *SvcDisplayName_CF* e *SvcState_CF*, tooextract hello servizio Visualizza nome e hello lo stato del servizio hello (ad esempio in esecuzione o arrestato) evento hello scritto toohello registro eventi di sistema.  È quindi creare una regola di avviso con hello seguenti query di ricerca: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` in modo che è possibile rilevare quando hello servizio Spooler di stampa è stato arrestato sul sistema di Windows hello.  Può trattarsi di qualsiasi servizio di interesse, ma per questo esempio si sta facendo riferimento a uno dei servizi preesistenti di hello inclusi con sistema operativo Windows hello.  Azione avviso Hello è tooexecute configurato il runbook usato in questo esempio ed eseguire in hello Runbook Worker ibrido, che sono abilitati sui sistemi di destinazione hello.   

attività del runbook codice Hello **ottenere il nome di servizio da LA** convertirà stringa hello in formato JSON in un tipo di oggetto e il filtro sull'elemento hello *SvcDisplayName_CF* nome visualizzato di hello tooextract di hello Servizio di Windows e passare la variabile nell'attività successiva hello verificherà hello servizio viene arrestato prima di tentare di toorestart è.  *SvcDisplayName_CF* è un [campo personalizzato](../log-analytics/log-analytics-custom-fields.md) creato nel Log Analitica toodemonstrate in questo esempio.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

Quando si arresta il servizio di hello, regola di avviso nel Log Analitica hello rileverà una corrispondenza e attivare il runbook hello e inviare hello al contesto dell'avviso toohello runbook. Hello runbook eseguirà l'azione tooverify hello servizio viene arrestato, e, se così toorestart tentativo hello servizio e verificare è stato avviato correttamente e risultati di hello di output.     

In alternativa se non si dispone di automazione account collegato tooyour OMS area di lavoro, si sarebbe configurare la regola di avviso hello con un runbook di webhook azione tootrigger hello e configurare hello runbook tooconvert hello stringa in formato JSON e filtrare *. SearchResult* istruzioni disponibili hello indicato in precedenza.    

## <a name="next-steps"></a>Passaggi successivi

* ulteriori informazioni sugli avvisi nel registro Analitica toolearn e toocreate uno, vedere [gli avvisi nel registro Analitica](../log-analytics/log-analytics-alerts.md).

* i runbook tootrigger utilizzando un webhook, vedere toounderstand [webhook di automazione di Azure](automation-webhooks.md).

---
title: aaaGuidance per lo sviluppo di funzioni di Azure | Documenti Microsoft
description: "Informazioni su concetti di Azure funzioni hello e le tecniche che è necessario toodevelop funzioni in Azure, in tutti i linguaggi di programmazione e le associazioni."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: manuale dello sviluppatore, funzioni di azure, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Manuale dello sviluppatore di Funzioni di Azure
Nelle funzioni di Azure, le funzioni specifiche condividono alcuni concetti tecnici e i componenti, indipendentemente dal linguaggio di hello o associazione che si utilizza. Prima di passare in apprendimento tooa di dettagli specifici lingua o il binding specificato, essere tooread che tramite questa panoramica che applica tooall di essi.

Questo articolo si presuppone che sia già stata letta hello [panoramica delle funzioni di Azure](functions-overview.md) e si ha familiarità con [concetti WebJobs SDK, ad esempio trigger, associazioni e hello JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md). Funzioni di Azure si basa su hello WebJobs SDK. 

## <a name="function-code"></a>Codice di funzione
Oggetto *funzione* hello concetto primario nelle funzioni di Azure. Scrivere codice per una funzione in un linguaggio di propria scelta e salvare codice hello e dei file di configurazione hello stessa cartella. configurazione di Hello viene denominata `function.json`, che contiene i dati di configurazione JSON. Sono supportate varie lingue, e ogni ha un toowork leggermente diversa esperienza con ottimizzazione per la soluzione ottimale per tale lingua. 

file function.json Hello definisce l'associazione di funzione hello e altre impostazioni di configurazione. Hello runtime utilizza questo toomonitor gli eventi di file toodetermine hello e come toopass e dati restituiti dalla funzionano esecuzione. Hello di seguito è riportato un esempio di file function.json.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Set hello `disabled` proprietà troppo`true` funzione hello tooprevent venga eseguito.

Hello `bindings` proprietà è possibile configurare sia i trigger e le associazioni. Ogni associazione condivide alcune impostazioni comuni e alcune impostazioni, che sono specifici tooa particolare tipo di associazione. Ogni associazione richiede hello seguenti impostazioni:

| Proprietà | Valori/tipi | Commenti |
| --- | --- | --- |
| `type` |stringa |Tipo di associazione. Ad esempio, `queueTrigger`. |
| `direction` |'in', 'out' |Indica se l'associazione di hello è per la ricezione di dati nella funzione hello o l'invio dei dati dalla funzione hello. |
| `name` |string |nome Hello utilizzato per hello i dati associati in funzione hello. Per c#, si tratta di un nome di argomento. per JavaScript, una chiave di hello in un elenco di chiave/valore tra del. |

## <a name="function-app"></a>App per le funzioni
Un'app per le funzioni è costituita da una o più singole funzioni che vengono gestite insieme dal servizio app di Azure. Tutte le funzioni hello in una condivisione di app di funzione hello stesso prezzi piano, la distribuzione continua e la versione di runtime. Le funzioni scritte in più lingue possono che condividono hello stessa funzione app. Pensare a un'app di funzione come un modo di tooorganize e gestire collettivamente delle funzioni. 

## <a name="runtime-script-host-and-web-host"></a>Runtime (host di script e host Web)
runtime Hello o script host, è host WebJobs SDK sottostante hello che resta in attesa di eventi, che raccoglie e invia i dati e infine esegue il codice. 

i trigger toofacilitate HTTP, è inoltre disponibile un host web che è progettato toosit davanti a host di script hello negli scenari di produzione. Con due host consente di tooisolate hello script host hello front-end traffico gestito da hello web host.

## <a name="folder-structure"></a>Struttura di cartelle
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Quando la configurazione di un progetto per la distribuzione funzioni tooa funzione app in Azure App Service, è possibile considerare questa struttura di cartelle e il codice del sito. È possibile usare gli strumenti esistenti come l' integrazione e la distribuzione continue o gli script di distribuzione personalizzata per l'installazione del pacchetto di distribuzione o la transpilazione del codice.

> [!NOTE]
> Verificare che toodeploy il `host.json` cartelle di file e la funzione direttamente toohello `wwwroot` cartella. Non includere hello `wwwroot` cartella nelle distribuzioni. In caso contrario, verranno create le cartelle `wwwroot\wwwroot`. 
> 
> 

## <a id="fileupdate"></a>Funzionamento di file dell'app tooupdate
editor di funzione Hello incorporata hello portale di Azure consente di aggiornare hello *function.json* file e file di codice hello per una funzione. tooupload o aggiornamento di altri file, ad esempio *package. JSON* o *Project* o dipendenze, si dispone di toouse altri metodi di distribuzione.

App di funzione sono incorporate nel servizio App, quindi tutti hello [App web toostandard disponibili le opzioni di distribuzione](../app-service-web/web-sites-deploy.md) sono anche disponibili per App di funzione. Ecco alcuni metodi è possibile utilizzare tooupload o aggiornare i file di app di funzione. 

#### <a name="toouse-app-service-editor"></a>toouse Editor di servizio App
1. Nel portale di Azure funzioni hello, fare clic su **funzione impostazioni app**.
2. In hello **impostazioni avanzate** fare clic su **passare le impostazioni del servizio tooApp**.
3. Fare clic su **Editor del servizio app** nel menu di navigazione dell'applicazione in **DEVELOPMENT TOOLS** (STRUMENTI DI SVILUPPO).
4. Fare clic su **Vai**.
   
   Dopo il caricamento dell'Editor di servizio App, si noterà hello *host.json* cartelle di file e la funzione in *wwwroot*. 
5. Tooedit file aperti, o trascinamento della selezione da file tooupload computer di sviluppo.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>endpoint di Gestione controllo servizi (Kudu) dell'applicazione di toouse hello (funzione)
1. Accedere a `https://<function_app_name>.scm.azurewebsites.net`.
2. Fare clic su **Debug Console (Console di debug) > CMD**.
3. Passare troppo`D:\home\site\wwwroot\` tooupdate *host.json* o `D:\home\site\wwwroot\<function_name>` tooupdate i file di una funzione.
4. Trascinare un file che si desidera tooupload nella cartella appropriata di hello nella griglia file hello. Ci sono due aree nella griglia file hello in cui è possibile eliminare un file. Per *zip* file, verrà visualizzata una finestra con etichetta hello "Trascinare qui tooupload e decomprimere." Per altri tipi di file, eliminare nella griglia file hello ma all'esterno di casella "decomprimere" hello.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>distribuzione continua toouse
Seguire le istruzioni di hello in argomento hello [distribuzione continua per le funzioni di Azure](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Esecuzione parallela
Quando si verificano più velocemente di quanto un runtime a thread singolo (funzione) possono essere elaborati dal più eventi di attivazione, hello runtime può richiamare la funzione hello più volte in parallelo.  Se un'app di funzione utilizza hello [consumo piano di hosting](functions-scale.md#how-the-consumption-plan-works), hello funzione app può essere scalata automaticamente.  Ogni istanza di applicazione di funzione hello, se l'applicazione hello eseguita su hello consumo hosting piano o una normale [servizio App di piano di hosting](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), potrebbe elaborare chiamate di funzione simultanee in parallelo utilizzando più thread.  numero massimo di Hello di chiamate di funzione simultanee in ogni istanza di applicazione (funzione) varia in base al tipo di hello del trigger in uso, nonché risorse hello usate da altre funzioni all'interno di app di funzione hello.

## <a name="functions-runtime-versioning"></a>Controllo delle versioni del runtime di Funzioni

È possibile configurare una versione di hello del runtime di funzioni hello utilizzando hello `FUNCTIONS_EXTENSION_VERSION` impostazione dell'app. Ad esempio, il valore di hello "~ 1" indica che l'App di funzione utilizzano 1 perché la versione principale. Le app di funzione sono aggiornati tooeach nuova versione secondaria non appena vengono rilasciate. È possibile visualizzare versione esatta di hello dell'App in funzione in hello **impostazioni** scheda hello portale di Azure.

## <a name="repositories"></a>Repository
codice Hello per le funzioni di Azure è open source e archiviati nel repository GitHub:

* [Runtime di Funzioni di Azure](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Portale Funzioni di Azure](https://github.com/projectkudu/AzureFunctionsPortal)
* [Modelli di Funzioni di Azure](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/)
* [Estensioni Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Associazioni
La tabella riportata di seguito elenca tutte le associazioni supportate.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Segnalazione di problemi
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello seguenti risorse:

* [Best Practices for Azure Functions](functions-best-practices.md) (Procedure consigliate per Funzioni di Azure)
* [Guida di riferimento per gli sviluppatori C# di Funzioni di Azure](functions-reference-csharp.md)
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#](functions-reference-fsharp.md)
* [Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure](functions-reference-node.md)
* [Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md)
* [Funzioni di Azure: hello viaggio](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) sul blog del team di Azure App Service hello. Storia dello sviluppo di Funzioni di Azure.


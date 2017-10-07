---
title: aaaCreate un'API senza server utilizzando le funzioni di Azure | Documenti Microsoft
description: Come toocreate un'API senza server utilizzando le funzioni di Azure
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Creare un'API senza server mediante Funzioni di Azure

In questa esercitazione verrà illustrato come le funzioni di Azure consente toobuild API altamente scalabili. Funzioni di Azure include una raccolta incorporata HTTP e le associazioni che rendono facilmente tooauthor un endpoint in una vasta gamma di linguaggi, tra cui Node.JS, c# e altro ancora. In questa esercitazione si personalizzerà un azioni specifiche di HTTP trigger toohandle nella progettazione delle API. Ci si preparerà inoltre a far crescere l'API integrandola con i proxy di Funzioni di Azure e a configurare API fittizie. Tutto ciò avviene su hello funzioni senza ambiente di calcolo, in modo non si dispone di tooworry sulla scalabilità delle risorse: è possibile concentrarsi solo alla logica di API.

## <a name="prerequisites"></a>Prerequisiti 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

funzione risultante Hello da utilizzare per il resto di hello di questa esercitazione.

### <a name="sign-in-tooazure"></a>Accedi tooAzure

Hello aprirlo portale di Azure. toodo, accedi troppo[https://portal.azure.com](https://portal.azure.com) con l'account di Azure.

## <a name="customize-your-http-function"></a>Personalizzare la funzione HTTP

Per impostazione predefinita, la funzione di attivazione HTTP è configurato tooaccept qualsiasi metodo HTTP. È inoltre disponibile un URL predefinito del modulo di hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Se si sono seguite Guide rapide hello, quindi `<funcname>` probabilmente ha un aspetto simile al seguente "HttpTriggerJS1". In questa sezione, si modificherà hello funzione toorespond tooGET solo delle richieste pervenute `/api/hello` invece di routing. 

Passare la funzione tooyour in hello portale di Azure. Selezionare **integrazione** nel riquadro di spostamento sinistro hello.

![Personalizzazione di una funzione HTTP](./media/functions-create-serverless-api/customizing-http.png)

Utilizzare le impostazioni di trigger HTTP come specificato nella tabella hello.

| Campo | Valore di esempio | Descrizione |
|---|---|---|
| Metodi HTTP consentiti | Metodi selezionati | Determina quali metodi HTTP possono essere utilizzato tooinvoke questa funzione |
| Metodi HTTP selezionati | GET | Consente solo toobe metodi HTTP selezionato usati tooinvoke questa funzione |
| Modello di route | /hello | Determina la route è tooinvoke utilizzata questa funzione |

Si noti che non include hello `/api` prefisso di percorso nel modello di route hello, di base come questa operazione viene gestita da un'impostazione globale.

Fare clic su **Salva**.

Altre informazioni sulla personalizzazione delle funzioni HTTP sono riportate in [Binding Azure HTTP e webhook di Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Testare l'API

Quindi, testarlo toosee la funzione utilizzo superficie dell'API nuovo hello.

Passare pagina sviluppo toohello indietro facendo clic sul nome della funzione hello in hello riquadro di spostamento sinistro.

Fare clic su **ottenere l'URL di funzione** e copiare l'URL di hello. Si noterà che usa hello `/api/hello` indirizzare ora.

Copiare l'URL di hello in una nuova scheda del browser o un client REST preferito. I browser useranno GET per impostazione predefinita.

Eseguire la funzione hello e confermare che è in corso. Parametro "name" di hello tooprovide potrebbe essere necessario un codice di avvio rapido query stringa toosatisfy hello.

È anche possibile richiamare l'endpoint di hello con un altro tooconfirm di metodo HTTP che la funzione hello non viene eseguita. A tale scopo, è necessario un client REST, ad esempio cURL, Postman o Fiddler toouse.

## <a name="proxies-overview"></a>Panoramica dei proxy

Nella sezione successiva hello, verrà di superficie dell'API tramite un proxy. Proxy di funzioni di Azure è una funzionalità di anteprima che consente di tooforward richieste tooother risorse. Si definisce un endpoint HTTP nello stesso modo con trigger HTTP, ma invece di scrivere codice tooexecute quando viene chiamato tale endpoint, si fornisce un'implementazione di URL tooa remota. In questo modo toocompose API più origini in una singola superficie API semplice per i client tooconsume. Ciò è particolarmente utile se si desidera toobuild dell'API come microservizi.

Un proxy può puntare risorsa tooany HTTP, ad esempio:
- Funzioni di Azure 
- App per le API in [Servizio app di Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Contenitori docker in [Servizio App in Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Qualsiasi altra API in hosting

toolearn ulteriori informazioni sui proxy, vedere [utilizzo di proxy di funzioni di Azure (anteprima)].

## <a name="create-your-first-proxy"></a>Creare il primo proxy

In questa sezione verrà creato un nuovo proxy che viene utilizzata come un front-end tooyour API complessiva. 

### <a name="setting-up-hello-frontend-environment"></a>Impostazione di ambiente front-end hello

Ripetere i passaggi di hello troppo[creare un'app di funzione](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate una nuova app di funzione in cui verrà creato il proxy. Questa nuova applicazione verrà utilizzato come server front-end hello per API e app di funzione hello in precedenza, che si stava modificando fungerà da un back-end.

Passare tooyour nuovo front-end funzione app nel portale di hello.

Selezionare **Impostazioni**. Passare quindi **abilitare i proxy di funzioni di Azure (anteprima)** troppo "On".

Selezionare **Impostazioni piattaforma** e scegliere **Impostazioni applicazione**.

Scorrere verso il basso troppo**impostazioni App** e creare una nuova impostazione con la chiave "HELLO_HOST". Impostare il relativo host toohello valore della funzione app back-end, ad esempio `<YourApp>.azurewebsites.net`. Questo fa parte dell'URL hello copiato in precedenza durante il test di una funzione HTTP. Riferimento a questa impostazione nella configurazione hello in un secondo momento.

> [!NOTE] 
> Le impostazioni dell'App sono consigliate per hello host configurazione tooprevent una dipendenza hardcoded di ambiente per il proxy di hello. Utilizzando le impostazioni dell'app indica che è possibile spostare la configurazione del proxy hello tra gli ambienti e verranno applicate le impostazioni specifiche dell'ambiente app hello.

Fare clic su **Salva**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Creazione di un proxy in front-end hello

Spostarsi indietro tooyour front-end funzione app nel portale di hello.

Nella finestra di navigazione a sinistra di hello, fare clic su hello segno successivo '+' troppo "Proxy (anteprima)".

![Creazione di un proxy](./media/functions-create-serverless-api/creating-proxy.png)

Utilizzare le impostazioni del proxy come specificato nella tabella hello.

| Campo | Valore di esempio | Descrizione |
|---|---|---|
| Nome | HelloProxy | Nome descrittivo utilizzato solo per la gestione |
| Modello di route | /api/hello | Determina la route è tooinvoke usato questo proxy |
| URL back-end | https://%HELLO_HOST%/api/hello | Specifica richiesta di hello endpoint toowhich hello deve essere elaborata |

Si noti che proxy non fornisce hello `/api` prefisso di percorso di base e questo deve essere incluso nel modello di route hello.

Hello `%HELLO_HOST%` sintassi farà riferimento impostazione app hello creato in precedenza. Hello risolto che URL punterà tooyour di funzione originale.

Fare clic su **Crea**.

È possibile provare il nuovo proxy copiando hello URL del Proxy e testarlo nel browser hello o con il client HTTP preferito.

## <a name="create-a-mock-api"></a>Creare un'API fittizia

Successivamente, si utilizzerà un toocreate proxy un'API fittizia per la soluzione. In questo modo lo sviluppo di client tooprogress, senza la necessità di back-end hello implementata completamente. In un secondo momento in fase di sviluppo, è possibile creare una nuova app di funzione che supporta questa logica e reindirizzare tooit il proxy.

toocreate questo modello API, si creerà un nuovo proxy, questa volta utilizzando hello [Editor di servizio App](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget avviato, passare tooyour funzione app nel portale di hello. Selezionare **Funzionalità della piattaforma** e trovare **Editor del servizio app**. Facendo clic su questa, hello Editor di servizio App verrà aperto in una nuova scheda.

Selezionare `proxies.json` nel riquadro di spostamento sinistro hello. Si tratta di file hello che memorizza la configurazione di hello per tutti i proxy. Se si utilizza uno di hello [funzioni metodi di distribuzione](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), si tratta di file hello verranno mantenuti nel controllo del codice sorgente. toolearn informazioni su questo file, vedere [configurazione avanzata proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Se è stato seguito fino a questo punto, il proxies.json dovrebbe essere simile hello seguenti:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Ora si aggiungerà l'API fittizia. Sostituire il file proxies.json con seguenti hello:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Aggiunge un nuovo proxy "GetUserByName", senza la proprietà backendUri hello. Invece di chiamare un'altra risorsa, viene modificata in risposta predefinita hello dal proxy utilizzando una sostituzione di risposta. È possibile anche usare gli override di richiesta e risposta in combinazione con un URL di back-end. Ciò è particolarmente utile quando l'inoltro dei dati tooa sistema legacy, in cui potrebbe essere necessario toomodify intestazioni, i parametri di query, toolearn e così via. ulteriori informazioni sulla richiesta e risposta sostituzioni, vedere [modifica richieste e risposte in proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Per testare l'API fittizio hello chiamante `/api/users/{username}` endpoint utilizzando un browser o un client REST preferito. Tooreplace assicurarsi di essere _{username}_ con un valore stringa che rappresenta un nome utente.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, si è appreso come toobuild e personalizzare un'API sulle funzioni di Azure. È stato inoltre descritto come toobring più le API, inclusi mocks, insieme come una superficie API unificata. È possibile utilizzare queste tecniche toobuild all'API di qualsiasi complessità, tutte durante l'esecuzione in modalità hello calcolo modello fornito dalle funzioni di Azure.

Hello riferimenti seguenti possono essere utili quando si sviluppa ulteriormente l'API:

- [Binding HTTP e webhook di Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [utilizzo di proxy di funzioni di Azure (anteprima)]
- [Documentazione di un'API di Funzioni di Azure (anteprima)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[utilizzo di proxy di funzioni di Azure (anteprima)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies

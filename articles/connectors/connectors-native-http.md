---
title: aaaCommunicate con qualsiasi endpoint su HTTP, le app di logica di Azure | Documenti Microsoft
description: Creare app per la logica in grado di comunicare con qualsiasi endpoint su HTTP
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>Introduzione a hello azione HTTP

Con hello azione HTTP, è possibile estendere i flussi di lavoro per l'organizzazione e comunicare tooany endpoint su HTTP.

È possibile:

* Creare flussi di lavoro con app per la logica che si attivano (trigger) quando un sito Web gestito diventa inattivo.
* Comunicare tooany endpoint tramite HTTP tooextend i flussi di lavoro ad altri servizi.

tooget avviato utilizzando l'azione di hello HTTP in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Utilizzare trigger hello HTTP
Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica. [Altre informazioni sui trigger](connectors-overview.md).

Di seguito è riportata una sequenza di esempio di come trigger tooset backup hello HTTP hello progettazione applicazione logica.

1. Aggiungere trigger di hello HTTP nell'app logica.
2. Specificare i parametri di hello per endpoint hello HTTP che si desidera toopoll.
3. Modificare l'intervallo di ricorrenza hello sulla frequenza con cui deve eseguire il polling.

   Hello logica app viene ora attivato con il contenuto restituito durante ogni controllo.

   ![Trigger HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Funzionamento di trigger HTTP hello

trigger di Hello HTTP invia un endpoint tooHTTP chiamata su un intervallo di ricorrenza. Per impostazione predefinita, il codice di risposta HTTP che è inferiore a 300 provoca un toorun app logica. toospecify se deve generare hello logica app, è possibile modificare hello logica app nella visualizzazione codice e aggiungere una condizione che restituisce hello dopo la chiamata HTTP. Di seguito è riportato un esempio di un trigger HTTP che viene generato quando hello restituito codice di stato è maggiore o uguale a troppo`400`.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

Per maggiori informazioni sui parametri trigger hello HTTP, disponibile in [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Utilizzare l'azione di hello HTTP

Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica. 
[Altre informazioni sulle azioni](connectors-overview.md).

1. Scegliere **Nuovo passaggio** > **Aggiungi un'azione**.
3. Nella casella di ricerca azione hello, digitare **http** azioni hello HTTP toolist.
   
    ![Selezionare l'azione di hello HTTP](./media/connectors-native-http/using-action-1.png)

4. Aggiungere i parametri richiesti per la chiamata hello HTTP.
   
    ![Hello completo azione HTTP](./media/connectors-native-http/using-action-2.png)

5. Sulla barra degli strumenti della finestra di progettazione hello, fare clic su **salvare**. L'app logica viene salvato e pubblicato (attivato) hello contemporaneamente.

## <a name="http-trigger"></a>Trigger HTTP
Ecco i dettagli di hello per trigger hello che supporta il connettore. Connettore HTTP Hello include un trigger.

| Trigger | Descrizione |
| --- | --- |
| HTTP |Effettua una chiamata HTTP e restituisce contenuto della risposta hello. |

## <a name="http-action"></a>Azione HTTP
Ecco hello dettagli per l'azione di hello che supporta questo connettore. Connettore HTTP Hello è un'opzione possibile.

| Azione | Descrizione |
| --- | --- |
| HTTP |Effettua una chiamata HTTP e restituisce contenuto della risposta hello. |

## <a name="http-details"></a>Dettagli di HTTP
Hello nelle tabelle seguenti vengono descritti hello necessarie e i campi di input facoltativi per azione di hello e i dettagli di output corrispondenti hello associati mediante l'azione di hello.

#### <a name="http-request"></a>Richiesta HTTP
di seguito Hello sono campi di input per l'azione di hello, che esegue una richiesta HTTP in uscita.
Un asterisco (*) indica che è un campo obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Metodo* |statico |toouse verbo HTTP Hello |
| URI* |Uri |Hello URI per la richiesta HTTP hello |
| Headers |headers |Un oggetto JSON di tooinclude intestazioni HTTP |
| Corpo |body |Hello corpo della richiesta HTTP |
| Autenticazione |authentication |Dettagli hello [autenticazione](#authentication) sezione |

<br>

#### <a name="output-details"></a>Dettagli dell'output
di seguito Hello sono i dettagli di output per hello risposta HTTP.

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| headers |object |Intestazioni della risposta |
| Corpo |object |Oggetto della risposta |
| Codice di stato |int |Stato codice HTTP |

## <a name="authentication"></a>Autenticazione
funzionalità di App per la logica di Hello consente toouse diversi tipi di autenticazione a fronte di endpoint HTTP. È possibile utilizzare l'autenticazione con hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, e  **[HTTP Webhook](connectors-native-webhook.md)**  connettori. Hello seguenti tipi di autenticazione possono essere configurata:

* [Autenticazione di base](#basic-authentication)
* [Autenticazione con certificato client](#client-certificate-authentication)
* [Autenticazione OAuth di Azure Active Directory (Azure AD)](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Autenticazione di base

Hello segue l'oggetto di autenticazione è necessaria l'autenticazione di base.
Un asterisco (*) indica che è un campo obbligatorio.

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| Type* |type |Tipo di autenticazione (deve essere `Basic` per l'autenticazione di base) |
| Username* |username |Tooauthenticate nome utente |
| Password* |password |Password tooauthenticate |

> [!TIP]
> Se si desidera toouse una password che non può essere recuperata dalla definizione di hello, utilizzare un `securestring` parametro e hello `@parameters()`  
>  [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs).

ad esempio:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Autenticazione con certificato client

oggetto di autenticazione seguenti Hello è necessaria per l'autenticazione del certificato client. Un asterisco (*) indica che è un campo obbligatorio.

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| Type* |type |tipo di autenticazione Hello (deve essere `ClientCertificate` per i certificati client SSL) |
| PFX* |pfx |contenuto con codifica Base64 Hello del file di scambio di informazioni personali (PFX) hello |
| Password* |password |Hello password tooaccess hello file PFX |

> [!TIP]
> un parametro che non sarà leggibile nella definizione di hello dopo il salvataggio di hello logica app toouse, è possibile utilizzare un `securestring` parametro e hello `@parameters()`  
>  [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs).

ad esempio:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Autenticazione OAuth di Azure AD
Hello segue l'oggetto di autenticazione è necessaria per l'autenticazione OAuth di Active Directory di Azure. Un asterisco (*) indica che è un campo obbligatorio.

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| Type* |type |tipo di autenticazione Hello (deve essere `ActiveDirectoryOAuth` per OAuth di Active Directory di Azure) |
| Tenant* |tenant |Identificatore del tenant Hello per tenant hello Azure AD |
| Pubblico* |audience |risorsa Hello toouse autorizzazione richiesta. Ad esempio: `https://management.core.windows.net/` |
| ID cliente* |clientId |Hello identificatore client per un'applicazione hello Azure AD |
| Segreto* |secret |segreto Hello del client hello che sta richiedendo hello token |

> [!TIP]
> È possibile utilizzare un `securestring` parametro e hello `@parameters()` [funzione di definizione del flusso di lavoro](http://aka.ms/logicappdocs) toouse un parametro che non sarà leggibile nella definizione di hello dopo il salvataggio.
> 
> 

ad esempio:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Passaggi successivi
A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md). È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).


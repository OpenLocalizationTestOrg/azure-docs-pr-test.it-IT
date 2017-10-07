---
title: aaaHow tooadd operazioni tooan API in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come tooadd operazioni tooan API in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>Come tooadd operazioni tooan API in Gestione API di Azure
Prima di poter usare un'API in Gestione API, è necessario aggiungervi le operazioni. Questa guida viene illustrato come tooadd e configurare diversi tipi di operazioni tooan API in Gestione API.

## <a name="add-operation"></a>Aggiungere un'operazione
Le operazioni vengono aggiunte e configurate tooan API nel portale di server di pubblicazione hello. Fare clic su portale, server di pubblicazione di hello tooaccess **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.

![Portale di pubblicazione][api-management-management-console]

> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Seleziona hello desiderati API nel portale di pubblicazione hello e quindi seleziona hello **operazioni** scheda. 

![Operazioni][api-management-operations]

Fare clic su **operazione Add** tooadd una nuova operazione. Hello **nuova operazione** verranno visualizzati e hello **firma** scheda verrà selezionata per impostazione predefinita.

![Aggiungi operazione][api-management-add-operation]

Specificare hello **verbo HTTP** scegliendo dall'elenco a discesa hello.

![Metodo HTTP][api-management-http-method]

<a name="url-template"></a>

Definire il modello di URL hello digitando in un frammento di URL costituita da uno o più segmenti di percorso di URL e zero o più parametri di stringa di query. modello di URL Hello, accodato toohello URL di base di hello API, identifica una singola operazione HTTP. Può contenere una o più parti variabili denominate identificate da parentesi graffe. Queste parti variabili sono denominate parametri di modello e vengono assegnate dinamicamente i valori estratti dall'URL della richiesta di hello durante l'elaborazione richiesta hello dalla piattaforma di gestione API hello.

> modello di URL di Hello può includere modelli jolly. Ad esempio, specificando `/*` inoltrare tutte le richieste di nuovo tale toohello di metodo HTTP terminerà servizio.

![Modello di URL][api-management-url-template]

<a name="rewrite-url-template"></a>

Se si desidera, specificare hello **modello di riscrittura URL**. In questo modo è modello di URL toouse hello standard per l'elaborazione delle richieste in ingresso sul front-end hello, durante la chiamata hello back-end tramite un URL convertito in base toohello riscrivere modello. Parametri di modello dal modello di URL hello devono essere utilizzati nel modello di riscrittura hello. Hello riportato di seguito il tipo di contenuto come codificato come segmento di percorso nel servizio web hello dall'esempio precedente hello può essere fornito come parametro di query in hello che API pubblicata tramite hello utilizzando i modelli URL hello piattaforma di gestione API.

![Riscrittura modello di URL][api-management-url-template-rewrite]

Operazione toohello chiamanti viene utilizzato il formato di hello `/customers?customerid=ALFKI` e questo verrà mappato troppo`/Customers('ALFKI')` quando viene richiamata servizio back-end hello.

**Visualizzazione** nome e **descrizione** fornire una descrizione dell'operazione di hello e è utilizzate tooprovide documentazione sviluppatori toohello uso dell'API nel portale per sviluppatori hello.

![Descrizione][api-management-description]

Descrizione dell'operazione Hello può essere specificato come testo normale o HTML in hello **descrizione** casella di testo.

## <a name="operation-caching"></a>Memorizzazione nella cache di un'operazione
Risposta la memorizzazione nella cache riduce la latenza percepita dagli utenti hello API, ridurre il consumo di larghezza di banda e diminuisce hello carico sull'implementazione del servizio web di hello HTTP hello API. 

tooeasily e abilitare rapidamente la memorizzazione nella cache per l'operazione di hello hello seleziona **la memorizzazione nella cache** e controllare hello **abilitare** casella di controllo.

![Memorizzazione nella cache][api-management-caching-tab]

**Durata** specifica hello periodo di tempo durante cui hello in risposta all'operazione rimane nella cache di hello. valore predefinito di Hello è 3600 secondi o 1 ora.

Chiavi della cache sono utilizzati toodifferentiate tra le risposte risposta hello corrispondente chiave di cache diversa tooeach verrà visualizzato il proprio valore memorizzato nella cache separate. Facoltativamente, immettere i parametri di stringa di query specifico e/o toobe di intestazioni HTTP utilizzata nel calcolo di valori di chiave di cache di hello **possono variare dai parametri di stringa di query** e **possono variare dalle intestazioni** rispettivamente caselle di testo. Quando nessuna è l'URL della richiesta specificato, completo e hello seguente i valori dell'intestazione HTTP viene utilizzato la generazione delle chiavi della cache: **Accept** e **Accept-Charset**.

> Per ulteriori informazioni sulla memorizzazione nella cache e i criteri di memorizzazione nella cache, vedere [la vista dei risultati in Gestione API di Azure operazione toocache][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"></a>Parametri della richiesta
Parametri dell'operazione vengono gestiti nella scheda parametri hello. I parametri specificati in hello **modello di URL** su hello **firma** scheda vengono aggiunti automaticamente e possono essere modificate solo modificando il modello di URL hello. È possibile immettere i parametri aggiuntivi manualmente.

Fare clic su un nuovo parametro di query, tooadd **Aggiungi parametro di Query** e immettere hello le seguenti informazioni:

* **Nome** : nome del parametro.
* **Descrizione** -una breve descrizione del parametro hello (facoltativo).
* **Tipo** -tipo di parametro, selezionato nel hello elenco a discesa.
* **I valori** -valori che possono essere assegnati toothis parametro. Uno dei valori hello possa essere contrassegnato come predefinite (facoltativo).
* **Richiesto** -rendere obbligatorio parametro hello selezionando la casella di controllo hello. 

![Parametri della richiesta][api-management-request-parameters]

## <a name="request-body"></a>Corpo della richiesta
Se l'operazione di hello consente (ad esempio PUT, POST) e richiede un corpo è possibile fornire un esempio di in tutti i hello supportati i formati di rappresentazione (ad esempio json, XML). 

> corpo della richiesta Hello viene utilizzato solo ai fini della documentazione e non viene convalidato.
> 
> 

tooenter un corpo della richiesta, passare toohello **corpo** scheda.

Fare clic su **aggiungere rappresentazione**, iniziare a digitare il nome di tipo di contenuto desiderato (ad esempio application/json), selezionarlo nell'elenco a discesa hello e Incolla hello desiderato di esempio di corpo della richiesta nel formato selezionato hello nella casella di testo hello. 

![Corpo della richiesta][api-management-request-body]

In toorepresentations aggiuntivi, è inoltre possibile specificare una descrizione facoltativa in formato testo nella hello **descrizione** casella di testo.

## <a name="responses"> </a>Risposte
È una buona norma tooprovide ad esempio per tutti i codici di stato che può generare l'operazione di hello. Ogni codice di stato può avere più di un esempio di corpo di risposta, uno per ognuno dei hello i tipi di contenuto supportati. 

Fare clic su una risposta, tooadd **Aggiungi** e iniziare a digitare il codice di stato hello desiderato. In questo esempio di stato hello è codice **200 OK**. Una volta nell'elenco a discesa hello viene visualizzato il codice di hello, selezionarlo e codice di risposta hello viene creato e aggiunto tooyour operazione.

![Codice della risposta][api-management-response-code]

Fare clic su **aggiungere rappresentazione**, iniziare a digitare il nome di tipo di contenuto desiderato hello (ad esempio application/json) e quindi selezionare in hello elenco a discesa.

![Tipo di contenuto del corpo][api-management-response-body-content-type]

Incollare l'esempio di corpo di risposta hello nel formato selezionato hello nella casella di testo di hello. 

![Corpo della risposta][api-management-response-body]

Se si desidera, aggiungere una descrizione facoltativa in hello **descrizione** casella di testo.

Dopo aver configurato l'operazione di hello, fare clic su **salvare**.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver aggiungono le operazioni di hello tooan API, passaggio successivo hello è tooassociate hello API con un prodotto e pubblicarlo in modo che gli sviluppatori possono chiamare le operazioni.

* [Come toocreate e pubblicazione di un prodotto][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md

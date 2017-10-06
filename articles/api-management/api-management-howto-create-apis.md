---
title: aaaHow toocreate API di gestione API di Azure
description: Informazioni su come toocreate e configurare le API di gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>Come toocreate API di gestione API di Azure
Un'API in Gestione API rappresenta un set di operazioni che possono essere richiamate dalle applicazioni client. Vengono create nuove API nel portale di pubblicazione hello e quindi hello lo si desidera aggiungere le operazioni. Dopo aver aggiungono le operazioni di hello, hello API viene aggiunto tooa prodotto e può essere pubblicato. Dopo aver pubblicata un'API, può essere sottoscritto tooand utilizzato dagli sviluppatori.

Questa guida illustra innanzitutto hello nel processo di hello: modalità toocreate e configurare una nuova API di gestione API. Per ulteriori informazioni sull'aggiunta di operazioni e sulla pubblicazione di un prodotto, vedere [come tooadd operazioni tooan API] [ How tooadd operations tooan API] e [come toocreate e pubblicazione di un prodotto] [ How toocreate and publish a product].

## <a name="create-new-api"></a>Creare una nuova API
API create e configurate nel portale di pubblicazione hello. Fare clic su portale, server di pubblicazione di hello tooaccess **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.

![Portale di pubblicazione][api-management-management-console]

> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **aggiungere API**.

![Create API][api-management-create-api]

Hello utilizzare **aggiungere una nuova API** tooconfigure finestra hello nuova API.

![Add new API][api-management-add-new-api]

Hello seguente i campi è utilizzati tooconfigure hello nuova API.

* **Nome API Web** fornisce un nome descrittivo e univoco per hello API. Viene visualizzato nei portali di hello developer e server di pubblicazione.
* **URL servizio Web** riferimenti hello servizio HTTP implementazione hello API. Gestione API inoltra le richieste toothis indirizzo.
* **Suffisso URL dell'API Web** è l'URL di base per il servizio Gestione API hello toohello aggiunto. URL di base Hello è comune per tutte le API ospitate da un'istanza del servizio Gestione API. Gestione API consente di distinguere le API per il suffisso e pertanto suffisso hello deve essere univoco per tutte le API per un server di pubblicazione specificato.
* **Lo schema dell'URL di API Web** determina quali protocolli possono essere utilizzati tooaccess hello API. Per impostazione predefinita è specificato il valore HTTPs.
* toooptionally aggiungere questo nuovo prodotto tooa API, fare clic su hello **prodotti (facoltativi)** elenco a discesa e selezionare un prodotto. Questo passaggio può essere ripetuto più volte tooadd hello API toomultiple prodotti.

Una volta hello lo si desidera che i valori sono configurati, fare clic su **salvare**. Una volta creato, hello nuova API hello pagina Riepilogo per l'API di hello viene visualizzato nel portale di pubblicazione hello.

![Riepilogo dell'API][api-management-api-summary]

## <a name="configure-api-settings"></a>Configurare le impostazioni API
È possibile utilizzare hello **impostazioni** scheda tooverify e modificare la configurazione di hello per un'API. **Nome API Web**, **URL servizio Web**, e **suffisso URL di Web API** vengono inizialmente impostate qui quando hello API viene creato e può essere modificato. **Descrizione** fornisce una descrizione opzionale e **lo schema dell'URL di Web API** determina quali protocolli possono essere utilizzati tooaccess hello API.

![Impostazioni API][api-management-api-settings]

l'autenticazione del gateway tooconfigure per hello back-end del servizio API di hello implementazione, selezionare hello **sicurezza** hello scheda **con credenziali** elenco a discesa può essere utilizzati tooconfigure **HTTP base** o **i certificati Client** l'autenticazione. l'autenticazione di base toouse HTTP, è sufficiente immettere le credenziali di hello desiderato. Per informazioni sull'utilizzo di autenticazione del certificato client, vedere [toosecure servizi di back-end tramite client come certificato di autenticazione in Gestione API di Azure][How toosecure back-end services using client certificate authentication in Azure API Management].

Hello **sicurezza** scheda può essere anche usato tooconfigure **l'autorizzazione utente** mediante OAuth 2.0. Per ulteriori informazioni, vedere [modalità sviluppatore tooauthorize degli account con OAuth 2.0 in Gestione API di Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Impostazioni dell'autenticazione di base][api-management-api-settings-credentials]

Fare clic su **salvare** toosave le modifiche apportate toohello le impostazioni dell'API.

## <a name="next-steps"></a>Passaggi successivi
Dopo che viene creata un'API impostazioni hello configurate, passaggi successivi hello tooadd hello operazioni toohello API, aggiungere hello API tooa prodotto e pubblicarlo in modo che sia disponibile per gli sviluppatori. Per ulteriori informazioni, vedere hello seguenti articoli.

* [Come tooadd operazioni tooan API][How tooadd operations tooan API]
* [Come toocreate e pubblicazione di un prodotto][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md

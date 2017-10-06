---
title: la memorizzazione nella cache le prestazioni di tooimprove in Gestione API di Azure aaaAdd | Documenti Microsoft
description: Informazioni su come caricare il servizio web, il consumo di larghezza di banda e latenza hello tooimprove per le chiamate al servizio Gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Aggiungere la memorizzazione nella cache delle prestazioni tooimprove in Gestione API di Azure
Le operazioni in Gestione API possono essere configurate per la memorizzazione nella cache della risposta. La memorizzazione nella cache della risposta può ridurre significativamente la latenza delle API, il consumo di larghezza di banda e il carico del servizio Web per i dati che non vengono modificati di frequente.

Questa guida illustra come risposta tooadd la memorizzazione nella cache per l'API e configurare i criteri per le operazioni dell'API di Echo esempio hello. È quindi possibile chiamare l'operazione di hello dalla hello memorizzazione nella cache tooverify portale per sviluppatori in azione.

> [!NOTE]
> Per informazioni sul caching degli elementi in base alla chiave usando espressioni di criteri, vedere [Caching personalizzato in Gestione API di Azure](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Prima di hello seguente passaggi in questa Guida, è necessario disporre di un'istanza del servizio Gestione API con un'API e un prodotto configurato. Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.

## <a name="configure-caching"></a>Configurare un'operazione per la memorizzazione nella cache
In questo passaggio si esamineranno hello la memorizzazione nella cache le impostazioni di hello **ottenere risorse (cache)** operazione dell'esempio hello Echo API.

> [!NOTE]
> Ogni istanza del servizio Gestione API preconfigurato con un'API Echo che possono essere tooexperiment utilizzati con e acquisire informazioni su gestione API. Per altre informazioni, vedere [Introduzione a Gestione API di Azure][Get started with Azure API Management].
> 
> 

tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API. Consente di procedere toohello portale di pubblicazione di gestione API.

![Portale di pubblicazione][api-management-management-console]

Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **API Echo**.

![API Echo][api-management-echo-api]

Fare clic su hello **operazioni** scheda e quindi fare clic su hello **ottenere risorse (cache)** operazione hello **operazioni** elenco.

![Operazioni dell'API Echo][api-management-echo-api-operations]

Fare clic su hello **la memorizzazione nella cache** hello tooview scheda Impostazioni per l'operazione di memorizzazione nella cache.

![Scheda Memorizzazione nella cache][api-management-caching-tab]

tooenable la memorizzazione nella cache per un'operazione, seleziona hello **abilitare** casella di controllo. In questo esempio, il caching è abilitato.

Ogni risposta di operazione con chiave, in base ai valori hello hello **possono variare dai parametri di stringa di query** e **possono variare dalle intestazioni** campi. Se si desidera toocache più risposte in base a parametri di stringa di query o le intestazioni, è possibile configurare loro questi due campi.

**Durata** specifica l'intervallo di scadenza hello delle risposte hello memorizzati nella cache. In questo esempio, è l'intervallo hello **3600** secondi, ovvero ora tooone equivalente.

Utilizza la memorizzazione nella cache di configurazione in questo esempio hello, hello prima richiesta toohello **ottenere risorse (cache)** operazione restituisce una risposta dal servizio back-end hello. Questa risposta nella cache, con chiave fornita da hello specificato parametri di stringa di query e le intestazioni. Le chiamate successive operazione toohello, con i corrispondenti parametri, sarà necessario hello memorizzati nella cache di risposta restituito, fino a quando l'intervallo di durata della cache di hello è scaduto.

## <a name="caching-policies"></a>Hello rivedere i criteri di memorizzazione nella cache
In questo passaggio è esaminare la memorizzazione nella cache le impostazioni per hello hello **ottenere risorse (cache)** operazione dell'esempio hello Echo API.

Quando le impostazioni della cache sono configurate per un'operazione su hello **la memorizzazione nella cache** scheda, la memorizzazione nella cache vengono aggiunti i criteri per l'operazione di hello. Questi criteri possono essere visualizzati e modificati nell'editor Criteri di hello.

Fare clic su **criteri** da hello **gestione API** menu hello a sinistra e quindi seleziona **API Echo / ottenere una risorsa (cache)** da hello **operazione**elenco a discesa.

![Operazione nell'ambito dei criteri][api-management-operation-dropdown]

Consente di visualizzare i criteri per questa operazione hello editor Criteri di hello.

![Editor dei criteri di Gestione API][api-management-policy-editor]

definizione dei criteri Hello per questa operazione include hello criteri che definiscono una configurazione di cache di hello e che sono stati controllati tramite hello **la memorizzazione nella cache** scheda nel passaggio precedente hello.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Toohello le modifiche apportate nell'editor Criteri di hello i criteri di memorizzazione nella cache verrà riflesse nella hello **la memorizzazione nella cache** scheda di un'operazione e viceversa.
> 
> 

## <a name="test-operation"></a>Chiamare un'operazione e verificare la memorizzazione nella cache di hello
hello toosee la memorizzazione nella cache in azione, è possibile chiamare operazione hello dal portale per sviluppatori hello. Fare clic su **portale per sviluppatori** nel menu in alto destra hello.

![Portale per sviluppatori][api-management-developer-portal-menu]

Fare clic su **API** in hello menu superiore e quindi selezionare **API Echo**.

![API Echo][api-management-apis-echo-api]

> Se si dispone di un solo API configurata o account tooyour visibile, quindi fare clic su API consente di passare direttamente toohello operazioni dell'API.
> 
> 

Seleziona hello **ottenere risorse (cache)** operazione e quindi fare clic su **aprire la Console di**.

![Open console][api-management-open-console]

console Hello consente operazioni di tooinvoke direttamente dal portale per sviluppatori hello.

![Console][api-management-console]

Mantenere i valori predefiniti di hello per **param1** e **param2**.

Selezionare hello chiave desiderato da hello **chiave di sottoscrizione** elenco a discesa. Se l'account ha una sola sottoscrizione, sarà già selezionata automaticamente.

Immettere **sampleheader:value1** in hello **le intestazioni di richiesta** casella di testo.

Fare clic su **HTTP Get** e prendere nota di hello intestazioni di risposta.

Immettere **sampleheader:value2** in hello **le intestazioni di richiesta** casella di testo e quindi fare clic su **HTTP Get**.

Si noti il valore di hello di **sampleheader** è ancora **value1** in risposta hello. Provare alcuni valori diversi e viene restituito si noti che la risposta memorizzata nella cache dalla prima chiamata hello hello.

Immettere **25** in hello **param2** campo e quindi fare clic su **HTTP Get**.

Si noti il valore di hello di **sampleheader** in hello risposta è ora **value2**. Poiché i risultati dell'operazione hello vengono codificati dalla stringa di query, risposta memorizzata nella cache di hello precedente non è stato restituito.

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni sulla memorizzazione nella cache i criteri, vedere [criteri di memorizzazione nella cache] [ Caching policies] in hello [riferimento ai criteri di gestione API][API Management policy reference].
* Per informazioni sul caching degli elementi in base alla chiave usando espressioni di criteri, vedere [Caching personalizzato in Gestione API di Azure](api-management-sample-cache-by-key.md).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps

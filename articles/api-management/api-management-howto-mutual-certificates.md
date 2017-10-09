---
title: servizi back-end aaaSecure utilizzando l'autenticazione del certificato client - Gestione API di Azure | Documenti Microsoft
description: Informazioni su come i servizi di back-end toosecure tramite client certificato di autenticazione in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Servizi back-end toosecure tramite client come certificato di autenticazione in Gestione API di Azure
Gestione API fornisce hello funzionalità toosecure accesso toohello back-end servizio di un'API tramite certificati client. Questa guida viene spiegato come toomanage certificati nel portale di pubblicazione hello API e come tooconfigure un'API toouse tooaccess un certificato il servizio back-end.

Per informazioni sulla gestione dei certificati con hello API REST gestione API, vedere [entità Certificate dell'API REST gestione API Azure][Azure API Management REST API Certificate entity].

## <a name="prerequisites"></a>Prerequisiti
Questa guida viene spiegato come tooconfigure l'API Gestione servizio istanza toouse client certificato autenticazione tooaccess hello servizio back-end per un'API. Prima di hello seguente passaggi in questo argomento, è necessario installare il servizio back-end configurato per l'autenticazione del certificato client ([tooconfigure certificato di autenticazione in siti Web di Azure vedere l'articolo toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), e hanno accesso toohello certificato e hello password hello certificato per il caricamento nel portale di pubblicazione di gestione API hello.

## <a name="step1"></a>Caricare un certificato client
tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API. Consente di procedere toohello portale di pubblicazione di gestione API.

![Portale di pubblicazione delle API][api-management-management-console]

> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Fare clic su **sicurezza** da hello **gestione API** menu a sinistra di hello e fare clic su **i certificati Client**.

![Certificati client][api-management-security-client-certificates]

Fare clic su un nuovo certificato, tooupload **carica certificato**.

![Caricamento del certificato][api-management-upload-certificate]

Sfoglia tooyour certificato e quindi immettere la password di hello per certificato hello.

> Hello del certificato deve essere **PFX** formato. Sono consentiti i certificati autofirmati.
> 
> 

![Caricamento del certificato][api-management-upload-certificate-form]

Fare clic su **caricare** certificato hello tooupload.

> password del certificato Hello viene convalidata in questo momento. Se non è corretta, viene visualizzato un messaggio di errore.
> 
> 

![Certificato caricato][api-management-certificate-uploaded]

Una volta caricato il certificato di hello, essa viene visualizzata nella hello **i certificati Client** scheda. Se si dispone di più certificati, prendere nota del soggetto hello o hello ultimi quattro caratteri dell'identificazione digitale hello, che sono certificati hello tooselect usato quando toouse un'API di configurazione dei certificati, come illustrato nella seguente hello [configura un API toouse un certificato client per l'autenticazione del gateway] [ Configure an API toouse a client certificate for gateway authentication] sezione.

> tooturn disattivare la convalida della catena di certificati quando si utilizza, ad esempio, un certificato autofirmato, seguire i passaggi di hello descritti in queste domande frequenti [elemento](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"></a>Eliminare un certificato client
Fare clic su un certificato, toodelete **eliminare** accanto a certificato desiderato hello.

![Eliminazione di un certificato][api-management-certificate-delete]

Fare clic su **Sì, eliminarlo** tooconfirm.

![Conferma dell'eliminazione][api-management-confirm-delete]

Se il certificato di hello è in uso da un'API, viene visualizzata una schermata di avviso. certificato di hello toodelete è necessario innanzitutto rimuovere hello certificati da qualsiasi API che sono configurati toouse.

![Conferma dell'eliminazione][api-management-confirm-delete-policy]

## <a name="step2"></a>Configurare un certificato client per l'autenticazione del gateway di toouse API
Fare clic su **API** da hello **gestione API** hello menu a sinistra, fare clic sul nome hello dell'API di hello desiderato e scegliere hello **sicurezza** scheda.

![Sicurezza API][api-management-api-security]

Selezionare **i certificati Client** da hello **con credenziali** elenco a discesa.

![Certificati client][api-management-mutual-certificates]

Selezionare hello certificato desiderato dall'hello **certificato Client** elenco a discesa. Se sono presenti più certificati, è possibile esaminare soggetto hello o hello ultimi quattro caratteri dell'identificazione digitale hello come indicato nel certificato corretto di hello precedente sezione toodetermine hello.

![Selezione del certificato][api-management-select-certificate]

Fare clic su **salvare** toosave hello configurazione modifica toohello API.

> Questa modifica ha validità immediata, e chiamate toooperations di tale API utilizzerà hello tooauthenticate certificato sul server back-end di hello.
> 
> 

![Salvataggio delle modifiche API][api-management-save-api]

> Quando si specifica un certificato per l'autenticazione del gateway per il servizio back-end hello di un'API, diventa parte dei criteri di hello dell'API e possono essere visualizzato in editor Criteri di hello.
> 
> 

![Criteri dei certificati][api-management-certificate-policy]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su altri modi di toosecure servizio back-end, ad esempio di base o condiviso segreto autenticazione HTTP, vedere hello video seguenti.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps




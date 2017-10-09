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
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="06b10-103">Servizi back-end toosecure tramite client come certificato di autenticazione in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="06b10-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="06b10-104">Gestione API fornisce hello funzionalità toosecure accesso toohello back-end servizio di un'API tramite certificati client.</span><span class="sxs-lookup"><span data-stu-id="06b10-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="06b10-105">Questa guida viene spiegato come toomanage certificati nel portale di pubblicazione hello API e come tooconfigure un'API toouse tooaccess un certificato il servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="06b10-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="06b10-106">Per informazioni sulla gestione dei certificati con hello API REST gestione API, vedere [entità Certificate dell'API REST gestione API Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="06b10-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="06b10-107"><a name="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="06b10-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="06b10-108">Questa guida viene spiegato come tooconfigure l'API Gestione servizio istanza toouse client certificato autenticazione tooaccess hello servizio back-end per un'API.</span><span class="sxs-lookup"><span data-stu-id="06b10-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="06b10-109">Prima di hello seguente passaggi in questo argomento, è necessario installare il servizio back-end configurato per l'autenticazione del certificato client ([tooconfigure certificato di autenticazione in siti Web di Azure vedere l'articolo toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), e hanno accesso toohello certificato e hello password hello certificato per il caricamento nel portale di pubblicazione di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="06b10-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="06b10-110"><a name="step1"></a>Caricare un certificato client</span><span class="sxs-lookup"><span data-stu-id="06b10-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="06b10-111">tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="06b10-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="06b10-112">Consente di procedere toohello portale di pubblicazione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="06b10-112">This takes you toohello API Management publisher portal.</span></span>

![Portale di pubblicazione delle API][api-management-management-console]

> <span data-ttu-id="06b10-114">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="06b10-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="06b10-115">Fare clic su **sicurezza** da hello **gestione API** menu a sinistra di hello e fare clic su **i certificati Client**.</span><span class="sxs-lookup"><span data-stu-id="06b10-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Certificati client][api-management-security-client-certificates]

<span data-ttu-id="06b10-117">Fare clic su un nuovo certificato, tooupload **carica certificato**.</span><span class="sxs-lookup"><span data-stu-id="06b10-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Caricamento del certificato][api-management-upload-certificate]

<span data-ttu-id="06b10-119">Sfoglia tooyour certificato e quindi immettere la password di hello per certificato hello.</span><span class="sxs-lookup"><span data-stu-id="06b10-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="06b10-120">Hello del certificato deve essere **PFX** formato.</span><span class="sxs-lookup"><span data-stu-id="06b10-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="06b10-121">Sono consentiti i certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="06b10-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Caricamento del certificato][api-management-upload-certificate-form]

<span data-ttu-id="06b10-123">Fare clic su **caricare** certificato hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="06b10-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="06b10-124">password del certificato Hello viene convalidata in questo momento.</span><span class="sxs-lookup"><span data-stu-id="06b10-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="06b10-125">Se non è corretta, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="06b10-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificato caricato][api-management-certificate-uploaded]

<span data-ttu-id="06b10-127">Una volta caricato il certificato di hello, essa viene visualizzata nella hello **i certificati Client** scheda. Se si dispone di più certificati, prendere nota del soggetto hello o hello ultimi quattro caratteri dell'identificazione digitale hello, che sono certificati hello tooselect usato quando toouse un'API di configurazione dei certificati, come illustrato nella seguente hello [configura un API toouse un certificato client per l'autenticazione del gateway] [ Configure an API toouse a client certificate for gateway authentication] sezione.</span><span class="sxs-lookup"><span data-stu-id="06b10-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="06b10-128">tooturn disattivare la convalida della catena di certificati quando si utilizza, ad esempio, un certificato autofirmato, seguire i passaggi di hello descritti in queste domande frequenti [elemento](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="06b10-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="06b10-129"><a name="step1a"></a>Eliminare un certificato client</span><span class="sxs-lookup"><span data-stu-id="06b10-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="06b10-130">Fare clic su un certificato, toodelete **eliminare** accanto a certificato desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="06b10-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Eliminazione di un certificato][api-management-certificate-delete]

<span data-ttu-id="06b10-132">Fare clic su **Sì, eliminarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="06b10-132">Click **Yes, delete it** tooconfirm.</span></span>

![Conferma dell'eliminazione][api-management-confirm-delete]

<span data-ttu-id="06b10-134">Se il certificato di hello è in uso da un'API, viene visualizzata una schermata di avviso.</span><span class="sxs-lookup"><span data-stu-id="06b10-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="06b10-135">certificato di hello toodelete è necessario innanzitutto rimuovere hello certificati da qualsiasi API che sono configurati toouse.</span><span class="sxs-lookup"><span data-stu-id="06b10-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Conferma dell'eliminazione][api-management-confirm-delete-policy]

## <span data-ttu-id="06b10-137"><a name="step2"></a>Configurare un certificato client per l'autenticazione del gateway di toouse API</span><span class="sxs-lookup"><span data-stu-id="06b10-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="06b10-138">Fare clic su **API** da hello **gestione API** hello menu a sinistra, fare clic sul nome hello dell'API di hello desiderato e scegliere hello **sicurezza** scheda.</span><span class="sxs-lookup"><span data-stu-id="06b10-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![Sicurezza API][api-management-api-security]

<span data-ttu-id="06b10-140">Selezionare **i certificati Client** da hello **con credenziali** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="06b10-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Certificati client][api-management-mutual-certificates]

<span data-ttu-id="06b10-142">Selezionare hello certificato desiderato dall'hello **certificato Client** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="06b10-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="06b10-143">Se sono presenti più certificati, è possibile esaminare soggetto hello o hello ultimi quattro caratteri dell'identificazione digitale hello come indicato nel certificato corretto di hello precedente sezione toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="06b10-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Selezione del certificato][api-management-select-certificate]

<span data-ttu-id="06b10-145">Fare clic su **salvare** toosave hello configurazione modifica toohello API.</span><span class="sxs-lookup"><span data-stu-id="06b10-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="06b10-146">Questa modifica ha validità immediata, e chiamate toooperations di tale API utilizzerà hello tooauthenticate certificato sul server back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="06b10-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Salvataggio delle modifiche API][api-management-save-api]

> <span data-ttu-id="06b10-148">Quando si specifica un certificato per l'autenticazione del gateway per il servizio back-end hello di un'API, diventa parte dei criteri di hello dell'API e possono essere visualizzato in editor Criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="06b10-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Criteri dei certificati][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="06b10-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06b10-150">Next steps</span></span>
<span data-ttu-id="06b10-151">Per ulteriori informazioni su altri modi di toosecure servizio back-end, ad esempio di base o condiviso segreto autenticazione HTTP, vedere hello video seguenti.</span><span class="sxs-lookup"><span data-stu-id="06b10-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

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




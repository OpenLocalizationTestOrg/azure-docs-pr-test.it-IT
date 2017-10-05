---
title: Proteggere i servizi back-end usando l'autenticazione con certificati client - Gestione API di Azure | Documentazione Microsoft
description: Come proteggere i servizi back-end usando l'autenticazione con certificati client in Gestione API di Azure.
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
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="126bc-103">Come proteggere i servizi back-end usando l'autenticazione con certificati client in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="126bc-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="126bc-104">Gestione API offre la possibilità di proteggere l'accesso al servizio back-end di un'API usando i certificati client.</span><span class="sxs-lookup"><span data-stu-id="126bc-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="126bc-105">Questa guida illustra come gestire i certificati nel portale di pubblicazione delle API e come configurare un'API per l'uso di un certificato per accedere al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="126bc-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="126bc-106">Per informazioni sulla gestione dei certificati con l'API REST di Gestione API, vedere [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity] (Entità certificato dell'API REST di Gestione API di Azure).</span><span class="sxs-lookup"><span data-stu-id="126bc-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="126bc-107"><a name="prerequisites"> </a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="126bc-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="126bc-108">In questa guida viene illustrato come configurare un'istanza del servizio di Gestione API per l'uso dell'autenticazione con certificati client per accedere al servizio back-end di un'API.</span><span class="sxs-lookup"><span data-stu-id="126bc-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="126bc-109">Prima di seguire i passaggi indicati in questo argomento è necessario aver configurato il servizio back-end per l'autenticazione del certificato client ([per la configurazione dell'autenticazione del certificato client nei siti Web di Azure, vedere questo articolo ][to configure certificate authentication in Azure WebSites refer to this article]) e avere l'accesso al certificato e alla relativa password per il caricamento nel portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="126bc-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="126bc-110"><a name="step1"> </a>Caricare un certificato client</span><span class="sxs-lookup"><span data-stu-id="126bc-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="126bc-111">Per iniziare, fare clic sul **portale di pubblicazione** nel Portale di Azure relativo al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="126bc-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="126bc-112">Verrà visualizzato il portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="126bc-112">This takes you to the API Management publisher portal.</span></span>

![Portale di pubblicazione delle API][api-management-management-console]

> <span data-ttu-id="126bc-114">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="126bc-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="126bc-115">Fare clic su **Sicurezza** dal menu **Gestione API** a sinistra, quindi scegliere **Certificati client**.</span><span class="sxs-lookup"><span data-stu-id="126bc-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Certificati client][api-management-security-client-certificates]

<span data-ttu-id="126bc-117">Per caricare un nuovo certificato, fare clic su **Carica certificato**.</span><span class="sxs-lookup"><span data-stu-id="126bc-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Carica certificato][api-management-upload-certificate]

<span data-ttu-id="126bc-119">Passare al certificato e immettere la relativa password.</span><span class="sxs-lookup"><span data-stu-id="126bc-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="126bc-120">Il certificato deve essere nel formato **.pfx** .</span><span class="sxs-lookup"><span data-stu-id="126bc-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="126bc-121">Sono consentiti i certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="126bc-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Carica certificato][api-management-upload-certificate-form]

<span data-ttu-id="126bc-123">Fare clic su **Carica** per caricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="126bc-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="126bc-124">A questo punto la password del certificato viene convalidata.</span><span class="sxs-lookup"><span data-stu-id="126bc-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="126bc-125">Se non è corretta, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="126bc-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificato caricato][api-management-certificate-uploaded]

<span data-ttu-id="126bc-127">Una volta caricato il certificato, questo viene visualizzato nella scheda **Certificati client** .</span><span class="sxs-lookup"><span data-stu-id="126bc-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="126bc-128">Se si hanno più certificati, prendere nota dell'oggetto o degli ultimi quattro caratteri dell'identificazione personale, che vengono usati per selezionare il certificato quando si configura un'API per l'uso dei certificati, come illustrato nella sezione [Configurare un'API per l'uso di un certificato client per l'autenticazione gateway][Configure an API to use a client certificate for gateway authentication] che segue.</span><span class="sxs-lookup"><span data-stu-id="126bc-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="126bc-129">Per disattivare la convalida della catena di certificati quando si usa, ad esempio, un certificato autofirmato, seguire i passaggi descritti in questa [voce](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end) delle Domande frequenti.</span><span class="sxs-lookup"><span data-stu-id="126bc-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="126bc-130"><a name="step1a"> </a>Eliminare un certificato client</span><span class="sxs-lookup"><span data-stu-id="126bc-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="126bc-131">Per eliminare un certificato, fare clic su **Elimina** accanto al certificato desiderato.</span><span class="sxs-lookup"><span data-stu-id="126bc-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Eliminazione di un certificato][api-management-certificate-delete]

<span data-ttu-id="126bc-133">Fare clic su **Sì, elimina** per confermare.</span><span class="sxs-lookup"><span data-stu-id="126bc-133">Click **Yes, delete it** to confirm.</span></span>

![Conferma dell'eliminazione][api-management-confirm-delete]

<span data-ttu-id="126bc-135">Se il certificato è in uso da parte di un'API, verrà visualizzata una schermata di avviso.</span><span class="sxs-lookup"><span data-stu-id="126bc-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="126bc-136">Per eliminare il certificato è necessario prima rimuoverlo da tutte le API configurate per il suo uso.</span><span class="sxs-lookup"><span data-stu-id="126bc-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Conferma dell'eliminazione][api-management-confirm-delete-policy]

## <span data-ttu-id="126bc-138"><a name="step2"> </a>Configurare un'API per l'uso di un certificato client per l'autenticazione gateway</span><span class="sxs-lookup"><span data-stu-id="126bc-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="126bc-139">Fare clic su **API** dal menu **Gestione API** a sinistra, fare clic sul nome dell'API desiderata, quindi sulla scheda **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="126bc-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![Sicurezza API][api-management-api-security]

<span data-ttu-id="126bc-141">Selezionare **Certificati client** dall'elenco a discesa **Con credenziali**.</span><span class="sxs-lookup"><span data-stu-id="126bc-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Certificati client][api-management-mutual-certificates]

<span data-ttu-id="126bc-143">Selezionare il certificato desiderato dall'elenco a discesa **Certificato client** .</span><span class="sxs-lookup"><span data-stu-id="126bc-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="126bc-144">Se esistono diversi certificati, fare riferimento all'oggetto o agli ultimi quattro caratteri dell'identificazione personale, come spiegato nella sezione precedente, per determinare il certificato corretto.</span><span class="sxs-lookup"><span data-stu-id="126bc-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Selezione del certificato][api-management-select-certificate]

<span data-ttu-id="126bc-146">Fare clic su **Salva** per salvare la modifica di configurazione nell'API.</span><span class="sxs-lookup"><span data-stu-id="126bc-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="126bc-147">Questa modifica ha effetto immediato e le chiamate alle operazioni di quell'API useranno il certificato per autenticarsi sul server back-end.</span><span class="sxs-lookup"><span data-stu-id="126bc-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Salvataggio delle modifiche API][api-management-save-api]

> <span data-ttu-id="126bc-149">Quando un certificato è specificato per l'autenticazione gateway del servizio back-end di un'API, diventa parte dei criteri di quell'API e può essere visualizzato nell'editor dei criteri.</span><span class="sxs-lookup"><span data-stu-id="126bc-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Criteri dei certificati][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="126bc-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="126bc-151">Next steps</span></span>
<span data-ttu-id="126bc-152">Per ulteriori informazioni su altri modi per proteggere il servizio back-end, ad esempio autenticazione HTTP di base o segreto condiviso, vedere il video seguente.</span><span class="sxs-lookup"><span data-stu-id="126bc-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

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



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps




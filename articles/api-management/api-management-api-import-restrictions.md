---
title: importare aaaRestrictions e problemi noti in Azure API di gestione | Documenti Microsoft
description: Dettagli di problemi noti e le restrizioni sull'importazione in Gestione API di Azure mediante i formati di API aperta, WSDL o WADL hello.
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="ca9da-103">Problemi noti e limitazioni dell'importazione dell'API</span><span class="sxs-lookup"><span data-stu-id="ca9da-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="ca9da-104">Informazioni sull'elenco</span><span class="sxs-lookup"><span data-stu-id="ca9da-104">About this list</span></span>
<span data-ttu-id="ca9da-105">Mentre ogni impegno tooensure che l'API di importazione in Gestione API di Azure non è più semplice e senza problemi possibili, è talvolta imporre restrizioni o identificare i problemi che saranno necessario toobe alla correzione dell'errore prima di poter importare correttamente.</span><span class="sxs-lookup"><span data-stu-id="ca9da-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="ca9da-106">Questo articolo sono descritti questi elementi, organizzate dal formato di importazione hello di hello API.</span><span class="sxs-lookup"><span data-stu-id="ca9da-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="ca9da-107"><a name="open-api"></a>Aprire l'API/Swagger</span><span class="sxs-lookup"><span data-stu-id="ca9da-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="ca9da-108">In generale, se si ricevono errori durante l'importazione del documento API aperta, verificare - sia stato convalidato utilizzando Progettazione hello in hello nuovo portale di Azure (progettazione - Front-End - Apri Editor di API specifica) oppure con un 3rd party strumento, ad esempio <a href="http://www.swagger.io"> Swagger Editor</a>.</span><span class="sxs-lookup"><span data-stu-id="ca9da-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="ca9da-109">**Nome host** è necessario un attributo per il nome host.</span><span class="sxs-lookup"><span data-stu-id="ca9da-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="ca9da-110">**Percorso base** è necessario un attributo per il percorso base.</span><span class="sxs-lookup"><span data-stu-id="ca9da-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="ca9da-111">**Schemi** è necessaria una matrice di schemi.</span><span class="sxs-lookup"><span data-stu-id="ca9da-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="ca9da-112"><a name="wsdl"></a>WSDL</span><span class="sxs-lookup"><span data-stu-id="ca9da-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="ca9da-113">File WSDL sono toogenerate utilizzate le API SOAP di pass-through o fungono hello back-end di un'API SOAP-a-REST.</span><span class="sxs-lookup"><span data-stu-id="ca9da-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="ca9da-114">**WSDL:Import**: le API che usano questo attributo non sono attualmente supportate.</span><span class="sxs-lookup"><span data-stu-id="ca9da-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="ca9da-115">I clienti è necessario unire gli elementi importato hello in un unico documento.</span><span class="sxs-lookup"><span data-stu-id="ca9da-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="ca9da-116">**Messaggi con più parti**: non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="ca9da-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="ca9da-117">I servizi SOAP **wsHttpBinding di WCF** creati con Windows Communication Foundation devono usare basicHttpBinding in quanto wsHttpBinding non è supportato.</span><span class="sxs-lookup"><span data-stu-id="ca9da-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="ca9da-118">**MTOM**: i servizi che usano MTOM <em>potrebbero</em> funzionare.</span><span class="sxs-lookup"><span data-stu-id="ca9da-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="ca9da-119">Al momento il supporto ufficiale non è previsto.</span><span class="sxs-lookup"><span data-stu-id="ca9da-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="ca9da-120">**Ricorsione** tipi che sono definiti in modo ricorsivo (ad esempio, fare riferimento la matrice tooan di per sé) non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="ca9da-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="ca9da-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="ca9da-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="ca9da-122">Attualmente non sono noti problemi di importazione del formato WADL.</span><span class="sxs-lookup"><span data-stu-id="ca9da-122">There are no known WADL import issues currently.</span></span>


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

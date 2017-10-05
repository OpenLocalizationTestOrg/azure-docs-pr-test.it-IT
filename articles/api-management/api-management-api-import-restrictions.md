---
title: Limitazioni e problemi noti dell'importazione dell'API di Gestione API di Azure | Microsoft Docs
description: Dettagli di problemi noti e limitazioni relative all'importazione in Gestione API di Azure con i formati Open API, WSDL o WADL.
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
ms.openlocfilehash: ac799d66b5038c207413086b0fa71239ff2a332f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="b6ec1-103">Problemi noti e limitazioni dell'importazione dell'API</span><span class="sxs-lookup"><span data-stu-id="b6ec1-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="b6ec1-104">Informazioni sull'elenco</span><span class="sxs-lookup"><span data-stu-id="b6ec1-104">About this list</span></span>
<span data-ttu-id="b6ec1-105">Mentre viene compiuto ogni sforzo per garantire che l'importazione dell'API in Gestione API di Azure sia la più semplice e priva di problemi possibile, talvolta si impongono limitazioni o si identificano problemi che dovranno essere risolti per poter eseguire correttamente l'importazione.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-105">While every effort is made to ensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need to be rectified before you can successfully import.</span></span> <span data-ttu-id="b6ec1-106">L'articolo illustra questi aspetti, organizzati in base al formato di importazione dell'API.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-106">This article documents these, organised by the import format of the API.</span></span>

## <span data-ttu-id="b6ec1-107"><a name="open-api"> </a>Aprire l'API/Swagger</span><span class="sxs-lookup"><span data-stu-id="b6ec1-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="b6ec1-108">In generale, se si ricevono errori durante l'importazione del documento Open API, assicurarsi che sia stato convalidato: usare la finestra di progettazione nel nuovo portale di Azure (Progettazione - Front End - Aprire l'editor della specifica API) o usare uno strumento di terze parti come <a href="http://www.swagger.io">Swagger Editor</a>.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using the designer in the new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="b6ec1-109">**Nome host** è necessario un attributo per il nome host.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="b6ec1-110">**Percorso base** è necessario un attributo per il percorso base.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="b6ec1-111">**Schemi** è necessaria una matrice di schemi.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="b6ec1-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="b6ec1-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="b6ec1-113">I file WSDL vengono usati per generare le API SOAP pass-through o come back-end dell'API SOAP-REST.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-113">WSDL files are used to generate SOAP Pass-through APIs, or serve as the backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="b6ec1-114">**WSDL:Import**: le API che usano questo attributo non sono attualmente supportate.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="b6ec1-115">I clienti devono unire gli elementi importati in un solo documento.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-115">Customers should merge the imported elements into one document.</span></span>
* <span data-ttu-id="b6ec1-116">**Messaggi con più parti**: non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="b6ec1-117">I servizi SOAP **wsHttpBinding di WCF** creati con Windows Communication Foundation devono usare basicHttpBinding in quanto wsHttpBinding non è supportato.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="b6ec1-118">**MTOM**: i servizi che usano MTOM <em>potrebbero</em> funzionare.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="b6ec1-119">Al momento il supporto ufficiale non è previsto.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="b6ec1-120">Non sono supportati i tipi **ricorsivi** che sono definiti in modo ricorsivo, ad esempio che fanno riferimento a una matrice di se stessi.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-120">**Recursion** types that are defined recursively (e.g. refer to an array of themselves) are not supported.</span></span>

## <span data-ttu-id="b6ec1-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="b6ec1-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="b6ec1-122">Attualmente non sono noti problemi di importazione del formato WADL.</span><span class="sxs-lookup"><span data-stu-id="b6ec1-122">There are no known WADL import issues currently.</span></span>


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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md

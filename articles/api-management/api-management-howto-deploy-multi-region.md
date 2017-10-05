---
title: "Distribuire servizi di Gestione API di Azure in più aree di Azure | Documentazione Microsoft"
description: "Informazioni su come distribuire un'istanza del servizio Gestione API di Azure in più aree di Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="8ec91-103">Come distribuire un'istanza del servizio Gestione API di Azure in più aree di Azure</span><span class="sxs-lookup"><span data-stu-id="8ec91-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="8ec91-104">Gestione API supporta la distribuzione in più aree che consente agli autori di API di distribuire un solo servizio Gestione API in qualsiasi numero di aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec91-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="8ec91-105">Ciò consente di ridurre la latenza delle richieste percepita dagli utenti dell'API distribuiti geograficamente, oltre a migliorare la disponibilità del servizio se un'area viene portata offline.</span><span class="sxs-lookup"><span data-stu-id="8ec91-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="8ec91-106">Quando un servizio di gestione API viene creato, inizialmente contiene una sola [unità][unit] e si trova in una sola area di Azure, designata come area primaria.</span><span class="sxs-lookup"><span data-stu-id="8ec91-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="8ec91-107">È possibile aggiungere facilmente altre aree tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec91-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="8ec91-108">Un server gateway di gestione API viene distribuito in ogni area e il traffico delle chiamate verrà indirizzato al gateway più vicino.</span><span class="sxs-lookup"><span data-stu-id="8ec91-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="8ec91-109">Quando un'area passa offline, il traffico viene automaticamente reindirizzato al gateway successivo più vicino.</span><span class="sxs-lookup"><span data-stu-id="8ec91-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8ec91-110">La distribuzione in più aree è disponibile solo nel livello **[Premium][Premium]**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="8ec91-111"><a name="add-region"> </a>Distribuire un'istanza del servizio Gestione API in una nuova area</span><span class="sxs-lookup"><span data-stu-id="8ec91-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="8ec91-112">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8ec91-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="8ec91-113">Passare alla pagina **Scalabilità** nel portale di Azure per l'istanza del servizio di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="8ec91-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Scheda Scalabilità][api-management-scale-service]

<span data-ttu-id="8ec91-115">Per distribuire una nuova area, fare clic su **+ Aggiungi area** dalla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="8ec91-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Aggiungere un'area][api-management-add-region]

<span data-ttu-id="8ec91-117">Selezionare la posizione dall'elenco a discesa e impostare il numero di unità con il dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="8ec91-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Specificare le unità][api-management-select-location-units]

<span data-ttu-id="8ec91-119">Fare clic su **Aggiungi** per inserire la selezione nella tabella Posizioni.</span><span class="sxs-lookup"><span data-stu-id="8ec91-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="8ec91-120">Ripetere l'operazione per configurare tutte le posizioni e fare clic su **Salva** dalla barra degli strumenti per avviare il processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8ec91-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="8ec91-121"><a name="remove-region"> </a>Eliminare un'istanza del servizio di Gestione API da una posizione</span><span class="sxs-lookup"><span data-stu-id="8ec91-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="8ec91-122">Passare alla pagina **Scalabilità** nel portale di Azure per l'istanza del servizio di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="8ec91-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Scheda Scalabilità][api-management-scale-service]

<span data-ttu-id="8ec91-124">Per la località che si vuole rimuovere aprire il menu di scelta rapida usando il pulsante **...** sul lato destro della tabella.</span><span class="sxs-lookup"><span data-stu-id="8ec91-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="8ec91-125">Selezionare l'opzione **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-125">Select the **Delete** option.</span></span>

![Rimuovere un'area][api-management-remove-region]

<span data-ttu-id="8ec91-127">Confermare l'eliminazione e fare clic su **Salva** per applicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="8ec91-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/


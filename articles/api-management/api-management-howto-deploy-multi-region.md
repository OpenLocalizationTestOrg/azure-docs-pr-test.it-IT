---
title: Gestione API di Azure aaaDeploy services toomultiple Azure aree | Documenti Microsoft
description: Informazioni su come toodeploy un'API di Azure Management service toomultiple istanza Azure aree.
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
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="96f2a-103">Come toodeploy un'API di Azure Management service toomultiple istanza Azure aree</span><span class="sxs-lookup"><span data-stu-id="96f2a-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="96f2a-104">API di gestione supporta la distribuzione di più aree che consente di API editori toodistribute un singolo servizio di gestione API in un numero qualsiasi di aree di Azure desiderate.</span><span class="sxs-lookup"><span data-stu-id="96f2a-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="96f2a-105">Ciò consente di ridurre la latenza delle richieste percepita dagli utenti dell'API distribuiti geograficamente, oltre a migliorare la disponibilità del servizio se un'area viene portata offline.</span><span class="sxs-lookup"><span data-stu-id="96f2a-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="96f2a-106">Quando viene creato inizialmente un servizio di gestione API, contiene solo una [unità] [ unit] e si trova in una singola regione di Azure, definita come hello area primaria.</span><span class="sxs-lookup"><span data-stu-id="96f2a-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="96f2a-107">È possibile aggiungere facilmente aree aggiuntive tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="96f2a-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="96f2a-108">Un server gateway di gestione API è distribuito tooeach area e chiamata traffico verrà indirizzato toohello più vicino gateway.</span><span class="sxs-lookup"><span data-stu-id="96f2a-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="96f2a-109">Se un'area è offline, il traffico di hello è gateway più vicino successivo toohello reindirizzata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="96f2a-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="96f2a-110">Distribuzione con più aree è disponibile solo in hello  **[Premium] [ Premium]**  livello.</span><span class="sxs-lookup"><span data-stu-id="96f2a-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="96f2a-111"><a name="add-region"></a>Distribuire un'API Gestione servizio istanza tooa nuova area</span><span class="sxs-lookup"><span data-stu-id="96f2a-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="96f2a-112">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96f2a-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="96f2a-113">Nel portale di Azure hello passare toohello **scala e prezzi** pagina per l'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="96f2a-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Scheda Scalabilità][api-management-scale-service]

<span data-ttu-id="96f2a-115">nuova area tooa toodeploy, fare clic su **+ Aggiungi area** dalla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="96f2a-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Aggiungere un'area][api-management-add-region]

<span data-ttu-id="96f2a-117">Selezionare il percorso di hello dall'elenco a discesa hello e impostare il numero di hello di unità per con dispositivo di scorrimento hello.</span><span class="sxs-lookup"><span data-stu-id="96f2a-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Specificare le unità][api-management-select-location-units]

<span data-ttu-id="96f2a-119">Fare clic su **Aggiungi** tooplace la selezione nella tabella delle posizioni di hello.</span><span class="sxs-lookup"><span data-stu-id="96f2a-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="96f2a-120">Ripetere questo processo fino a quando non si dispone di tutte le località configurate e fare clic su **salvare** dal processo di distribuzione hello toostart hello barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="96f2a-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="96f2a-121"><a name="remove-region"> </a>Eliminare un'istanza del servizio di Gestione API da una posizione</span><span class="sxs-lookup"><span data-stu-id="96f2a-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="96f2a-122">Nel portale di Azure hello passare toohello **scala e prezzi** pagina per l'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="96f2a-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Scheda Scalabilità][api-management-scale-service]

<span data-ttu-id="96f2a-124">Per percorso hello desiderato tooremove aprire il menu di scelta rapida hello utilizzando hello **...**  pulsante all'hello estremità destra della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="96f2a-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="96f2a-125">Seleziona hello **eliminare** opzione.</span><span class="sxs-lookup"><span data-stu-id="96f2a-125">Select hello **Delete** option.</span></span>

![Rimuovere un'area][api-management-remove-region]

<span data-ttu-id="96f2a-127">Confermare l'eliminazione di hello e fare clic su **salvare** modifiche hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="96f2a-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/


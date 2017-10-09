---
title: hello aaaUsing tooaccess API REST del servizio API di Azure Mobile Engagement
description: Viene descritto come toouse hello API REST di Engagement Mobile tooaccess servizio API di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="b4d87-103">Utilizzando tooaccess REST API dei servizi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b4d87-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="b4d87-104">Azure Mobile Engagement fornisce hello [API REST di Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) automaticamente toomanage dispositivi, le campagne di copertura o il Push e così via.</span><span class="sxs-lookup"><span data-stu-id="b4d87-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="b4d87-105">servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti.</span><span class="sxs-lookup"><span data-stu-id="b4d87-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="b4d87-106">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="b4d87-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="b4d87-107">Se non si desidera direttamente toouse hello API REST, è inoltre possibile usare un [file Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) che è possibile utilizzare con strumenti SDK toogenerate per la lingua preferita.</span><span class="sxs-lookup"><span data-stu-id="b4d87-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="b4d87-108">È consigliabile utilizzare hello [AutoRest](https://github.com/Azure/AutoRest) strumento toogenerate del SDK da questo file Swagger.</span><span class="sxs-lookup"><span data-stu-id="b4d87-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="b4d87-109">È stato creato un SDK di .NET in modo simile, che consente di toointeract con queste API tramite un wrapper di c# e non è necessario toodo hello negoziazione del token di autenticazione e aggiornare manualmente.</span><span class="sxs-lookup"><span data-stu-id="b4d87-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="b4d87-110">Vedere [esempio di servizio API .NET SDK](mobile-engagement-dotnet-sdk-service-api.md) toolearn come toouse hello .net SDK per le API</span><span class="sxs-lookup"><span data-stu-id="b4d87-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>

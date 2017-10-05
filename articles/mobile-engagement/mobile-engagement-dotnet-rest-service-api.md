---
title: Uso dell'API REST per accedere alle API del servizio Azure Mobile Engagement
description: Descrive come usare le API REST di Mobile Engagement per accedere alle API del servizio Azure Mobile Engagement
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
ms.openlocfilehash: 4b21bca6fee7012ce1dba96950ae075eded414f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-rest-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="274bc-103">Uso di REST per accedere alle API del servizio Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="274bc-103">Using REST to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="274bc-104">Azure Mobile Engagement offre l'[API REST per Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) che consente di gestire i dispositivi, le campagne push e di copertura e così via.</span><span class="sxs-lookup"><span data-stu-id="274bc-104">Azure Mobile Engagement provides the [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you to manage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="274bc-105">Il servizio Azure Mobile Engagement verrà ritirato a marzo 2018 ed è attualmente disponibile solo per i clienti esistenti.</span><span class="sxs-lookup"><span data-stu-id="274bc-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="274bc-106">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="274bc-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="274bc-107">Per chi non vuole usare le API REST direttamente è disponibile un [file Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) che è possibile usare con gli strumenti per la generazione degli SDK per la lingua preferita.</span><span class="sxs-lookup"><span data-stu-id="274bc-107">If you do not want to use the REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="274bc-108">Per generare l'SDK dal file Swagger è consigliabile usare lo strumento [AutoRest](https://github.com/Azure/AutoRest).</span><span class="sxs-lookup"><span data-stu-id="274bc-108">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span> <span data-ttu-id="274bc-109">In modo simile è stato creato un .NET SDK che consente di interagire con queste API tramite un wrapper C#. Non è necessario eseguire manualmente la negoziazione di token di autenticazione e l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="274bc-109">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="274bc-110">Vedere l'[esempio di API del servizio .NET SDK](mobile-engagement-dotnet-sdk-service-api.md) per informazioni su come usare .NET SDK per l'API</span><span class="sxs-lookup"><span data-stu-id="274bc-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) to learn how to use the .net SDK for API</span></span>

---
title: "Servizio app di Azure: scalabilità delle applicazioni nel servizio app"
description: "Informazioni su vantaggi e svantaggi della scalabilità dell'applicazione nel servizio app."
keywords: servizio app, servizio app di azure, scala, scalabile, piano di servizio app, costo del servizio app
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="94ac6-104">Servizio app di Azure: scalabilità delle applicazioni nel servizio app</span><span class="sxs-lookup"><span data-stu-id="94ac6-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="94ac6-105">Le applicazioni ospitate nel servizio app di Azure possono [raggiungere un livello di scalabilità elevato](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="94ac6-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="94ac6-106">Tuttavia, la scalabilità di un'applicazione è un problema complesso senza una soluzione valida per tutti i casi.</span><span class="sxs-lookup"><span data-stu-id="94ac6-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="94ac6-107">Per ridimensionare correttamente l'applicazione occorre considerare 3 aree chiave che contribuiranno al corretto funzionamento delle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="94ac6-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="94ac6-108">Comprendere l'architettura dell'applicazione e i relativi punti deboli.</span><span class="sxs-lookup"><span data-stu-id="94ac6-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="94ac6-109">Si tratta di un'applicazione con stato</span><span class="sxs-lookup"><span data-stu-id="94ac6-109">Is your Application Stateful?</span></span> <span data-ttu-id="94ac6-110">o senza stato?</span><span class="sxs-lookup"><span data-stu-id="94ac6-110">Stateless?</span></span>
   * <span data-ttu-id="94ac6-111">Quali sono i componenti dell'applicazione?</span><span class="sxs-lookup"><span data-stu-id="94ac6-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="94ac6-112">Dove sono i colli di bottiglia nell'applicazione?</span><span class="sxs-lookup"><span data-stu-id="94ac6-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="94ac6-113">Quando si applica il carico all'app, quali elementi vengono interrotti per primi?</span><span class="sxs-lookup"><span data-stu-id="94ac6-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="94ac6-114">Comprendere i requisiti di carico e prestazioni previsti.</span><span class="sxs-lookup"><span data-stu-id="94ac6-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="94ac6-115">L'applicazione deve servire 1000 utenti o un milione?</span><span class="sxs-lookup"><span data-stu-id="94ac6-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="94ac6-116">Il traffico proviene da un'unica area geografica o a livello globale?</span><span class="sxs-lookup"><span data-stu-id="94ac6-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="94ac6-117">Sono presenti variazioni stagionali o picchi di traffico?</span><span class="sxs-lookup"><span data-stu-id="94ac6-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="94ac6-118">Con quale velocità deve rispondere l'applicazione?</span><span class="sxs-lookup"><span data-stu-id="94ac6-118">How fast should the app respond?</span></span> <span data-ttu-id="94ac6-119">Un secondo?</span><span class="sxs-lookup"><span data-stu-id="94ac6-119">1 second?</span></span> <span data-ttu-id="94ac6-120">Un millisecondo?</span><span class="sxs-lookup"><span data-stu-id="94ac6-120">1 millisecond?</span></span>
3. <span data-ttu-id="94ac6-121">Comprendere e sfruttare correttamente la piattaforma di hosting dell'app.</span><span class="sxs-lookup"><span data-stu-id="94ac6-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="94ac6-122">Quali funzionalità è necessario sfruttare per raggiungere gli obiettivi di scalabilità?</span><span class="sxs-lookup"><span data-stu-id="94ac6-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="94ac6-123">Questa sezione consente di comprendere tutti i fattori e definire una strategia che sfrutti le funzionalità del servizio app necessarie per raggiungere i propri obiettivi di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="94ac6-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]


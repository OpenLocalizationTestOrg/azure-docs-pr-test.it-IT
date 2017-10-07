---
title: "Servizio app di Azure: scalabilità delle applicazioni nel servizio app"
description: "Informazioni su vantaggi e svantaggi hello di scalabilità dell'applicazione di servizio App."
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
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="bc483-104">Servizio app di Azure: scalabilità delle applicazioni nel servizio app</span><span class="sxs-lookup"><span data-stu-id="bc483-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="bc483-105">Le applicazioni ospitate nel servizio app di Azure possono [raggiungere un livello di scalabilità elevato](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="bc483-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="bc483-106">Tuttavia, la scalabilità di un'applicazione è un problema complesso senza una soluzione valida per tutti i casi.</span><span class="sxs-lookup"><span data-stu-id="bc483-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="bc483-107">toocorrectly ridimensionare l'applicazione sono presenti 3 aree chiave che contribuiranno tooyour esito positivo di applicazioni:</span><span class="sxs-lookup"><span data-stu-id="bc483-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="bc483-108">Comprendere l'architettura dell'applicazione e i relativi punti deboli.</span><span class="sxs-lookup"><span data-stu-id="bc483-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="bc483-109">Si tratta di un'applicazione con stato</span><span class="sxs-lookup"><span data-stu-id="bc483-109">Is your Application Stateful?</span></span> <span data-ttu-id="bc483-110">o senza stato?</span><span class="sxs-lookup"><span data-stu-id="bc483-110">Stateless?</span></span>
   * <span data-ttu-id="bc483-111">Quali sono tutti i componenti dell'applicazione hello?</span><span class="sxs-lookup"><span data-stu-id="bc483-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="bc483-112">Dove si trovano i colli di bottiglia hello in un'applicazione hello?</span><span class="sxs-lookup"><span data-stu-id="bc483-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="bc483-113">Quando carico è applicato tooyour app, ciò che verrà interrotta prima?</span><span class="sxs-lookup"><span data-stu-id="bc483-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="bc483-114">Hello comprensione prevede requisiti di carico e delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="bc483-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="bc483-115">Un'applicazione hello necessita tooserve 1000 utenti? o di un milione?</span><span class="sxs-lookup"><span data-stu-id="bc483-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="bc483-116">Il traffico proviene da un'unica area geografica o a livello globale?</span><span class="sxs-lookup"><span data-stu-id="bc483-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="bc483-117">Sono presenti variazioni stagionali o picchi di traffico?</span><span class="sxs-lookup"><span data-stu-id="bc483-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="bc483-118">La velocità con cui deve rispondere l'applicazione hello?</span><span class="sxs-lookup"><span data-stu-id="bc483-118">How fast should hello app respond?</span></span> <span data-ttu-id="bc483-119">Un secondo?</span><span class="sxs-lookup"><span data-stu-id="bc483-119">1 second?</span></span> <span data-ttu-id="bc483-120">Un millisecondo?</span><span class="sxs-lookup"><span data-stu-id="bc483-120">1 millisecond?</span></span>
3. <span data-ttu-id="bc483-121">Comprensione e correttamente sfruttano hello piattaforma che ospita l'app.</span><span class="sxs-lookup"><span data-stu-id="bc483-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="bc483-122">Quali funzionalità devono sfruttare appieno tooachieve miei obiettivi di scalabilità?</span><span class="sxs-lookup"><span data-stu-id="bc483-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="bc483-123">In questa sezione aiutano a comprendere tutti i fattori di hello e della Guida mettere a punto una strategia che sfrutta tooachieve funzionalità di servizio App necessarie hello gli obiettivi di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="bc483-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]


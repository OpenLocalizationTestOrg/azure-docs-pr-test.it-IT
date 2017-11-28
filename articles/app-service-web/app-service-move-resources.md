---
title: Spostamento di risorse di app Web a un altro gruppo di risorse
description: "Descrive gli scenari dove è possibile spostare le app Web e servizi app da un gruppo di risorse a un altro."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="93577-103">Configurazioni di spostamento supportate</span><span class="sxs-lookup"><span data-stu-id="93577-103">Supported Move Configurations</span></span>
<span data-ttu-id="93577-104">È possibile spostare le risorse di App Web di Azure usando l'[API di spostamento delle risorse di Resource Manager](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="93577-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="93577-105">App Web di Microsoft Azure supporta attualmente i seguenti scenari di spostamento:</span><span class="sxs-lookup"><span data-stu-id="93577-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="93577-106">Spostamento dell'intero contenuto di un gruppo di risorse (app Web, piani di servizio app e certificati) in un altro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="93577-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="93577-107">In questo scenario il gruppo di risorse di destinazione non può contenere alcuna risorsa Microsoft.Web.</span><span class="sxs-lookup"><span data-stu-id="93577-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="93577-108">Spostamento di singole app Web in un altro gruppo di risorse. Le app Web rimangono tuttavia ospitate nel relativo piano di servizio app (il piano di servizio app rimane nel gruppo di risorse precedente).</span><span class="sxs-lookup"><span data-stu-id="93577-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>



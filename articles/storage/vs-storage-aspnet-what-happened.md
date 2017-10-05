---
title: "Cosa è successo a un progetto ASP.NET? | Microsoft Docs"
description: Viene descritto cosa succede dopo l'aggiunta di archiviazione di Azure a un progetto ASP.NET utilizzando i servizi connessi a Visual Studio
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e1fe1b6d-4e3d-476d-8b2f-f7ade050515e
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e2cdc2ff4df85f0224352bd32a3ec62480c3e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="545b8-104">Cosa è successo a un progetto ASP.NET (servizio connesso a Visual Studio Archiviazione di Azure)?</span><span class="sxs-lookup"><span data-stu-id="545b8-104">What happened to my ASP.NET project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="545b8-105">Aggiunta di riferimenti</span><span class="sxs-lookup"><span data-stu-id="545b8-105">References added</span></span>
<span data-ttu-id="545b8-106">Il pacchetto NuGet per l'Archiviazione di Azure è stato aggiunto al progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="545b8-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="545b8-107">Il pacchetto aggiunge i riferimenti a .NET seguenti:</span><span class="sxs-lookup"><span data-stu-id="545b8-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="545b8-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="545b8-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="545b8-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="545b8-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="545b8-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="545b8-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="545b8-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="545b8-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="545b8-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="545b8-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="545b8-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="545b8-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="545b8-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="545b8-114">**System.Data**</span></span>
* <span data-ttu-id="545b8-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="545b8-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="545b8-116">Aggiunta di stringa di connessione per l'Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="545b8-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="545b8-117">Nel file web.config del progetto è stato creato un elemento con la stringa di connessione e la chiave dell'account di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="545b8-117">In the web.config file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="545b8-118">Per altre informazioni, vedere [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="545b8-118">For more information, see [ASP.NET](http://www.asp.net).</span></span>


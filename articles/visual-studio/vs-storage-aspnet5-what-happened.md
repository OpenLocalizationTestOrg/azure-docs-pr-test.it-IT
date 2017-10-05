---
title: "Cosa è successo a un progetto ASP.NET 5? (Servizi connessi di Visual Studio)| Documentazione Microsoft"
description: 'Viene descritto cosa succede dopo la connessione a un account di archiviazione di Azure in un progetto di Visual Studio ASP.NET 5 utilizzando i servizi connessi a Visual Studio '
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2a25c24fd7625374d269622a805f386fcd52bb5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="2f077-103">Cosa è successo a un progetto ASP.NET 5 (servizi connessi a Visual Studio Archiviazione di Azure)?</span><span class="sxs-lookup"><span data-stu-id="2f077-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="2f077-104">Aggiunta di riferimenti</span><span class="sxs-lookup"><span data-stu-id="2f077-104">References added</span></span>
<span data-ttu-id="2f077-105">Il pacchetto NuGet per l'Archiviazione di Azure è stato aggiunto al progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f077-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="2f077-106">Il pacchetto aggiunge i riferimenti a .NET seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f077-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="2f077-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="2f077-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="2f077-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="2f077-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="2f077-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="2f077-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="2f077-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="2f077-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="2f077-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="2f077-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="2f077-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="2f077-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="2f077-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="2f077-113">**System.Data**</span></span>
* <span data-ttu-id="2f077-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="2f077-114">**System.Spatial**</span></span>

<span data-ttu-id="2f077-115">È stato anche aggiunto il pacchetto NuGet **Microsoft.Framework.Configuration.Json** .</span><span class="sxs-lookup"><span data-stu-id="2f077-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="2f077-116">Aggiunta di stringa di connessione per l'Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2f077-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="2f077-117">Nel file config.json del progetto è stato creato un elemento con la stringa di connessione e la chiave dell'account di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="2f077-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="2f077-118">Per altre informazioni, vedere [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="2f077-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>


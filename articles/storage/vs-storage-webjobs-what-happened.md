---
title: "Cosa è successo al progetto Webjob (servizio connesso a Visual Studio Archiviazione di Azure)? | Microsoft Docs"
description: Viene descritto cosa succede in un progetto Webjob di Azure dopo la connessione a un account di archiviazione utilizzando i servizi connessi a Visual Studio
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3b28ddeadc87937941d60b16fae817e59a220b22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="ebcc5-104">Cosa è successo al progetto Webjob (servizio connesso a Visual Studio Archiviazione di Azure)?</span><span class="sxs-lookup"><span data-stu-id="ebcc5-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="ebcc5-105">Aggiunta di riferimenti</span><span class="sxs-lookup"><span data-stu-id="ebcc5-105">References Added</span></span>
<span data-ttu-id="ebcc5-106">Il pacchetto NuGet per l'Archiviazione di Azure è stato aggiunto o aggiornato nel progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebcc5-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="ebcc5-107">Il pacchetto aggiunge i riferimenti a .NET seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebcc5-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="ebcc5-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="ebcc5-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="ebcc5-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="ebcc5-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="ebcc5-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="ebcc5-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="ebcc5-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-114">**System.Data**</span></span>
* <span data-ttu-id="ebcc5-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="ebcc5-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="ebcc5-116">Aggiunta di stringa di connessione per l'Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ebcc5-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="ebcc5-117">Nel file App.config del progetto gli elementi **AzureWebJobsStorage** e **AzureWebJobsDashboard** sono stati aggiornati con la stringa di connessione e la chiave dell'account di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="ebcc5-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="ebcc5-118">Per altre informazioni, vedere [Risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="ebcc5-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>


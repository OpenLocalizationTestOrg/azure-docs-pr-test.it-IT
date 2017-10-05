---
title: "Cosa è successo a un progetto di servizi di cloud? | Microsoft Docs"
description: 'Viene descritto cosa succede in un progetto di servizi di cloud dopo la connessione a un account di archiviazione di Azure utilizzando i servizi connessi a Visual Studio '
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 4c9de56f6daf07097c0f593db37d14dce3bce05f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="208d0-104">Cosa è successo a un progetto di servizi di cloud (servizio connesso a Visual Studio Archiviazione di Azure)?</span><span class="sxs-lookup"><span data-stu-id="208d0-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="208d0-105">Aggiunta di riferimenti</span><span class="sxs-lookup"><span data-stu-id="208d0-105">References added</span></span>
<span data-ttu-id="208d0-106">Il pacchetto NuGet per l'Archiviazione di Azure è stato aggiunto al progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="208d0-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="208d0-107">Il pacchetto aggiunge i riferimenti a .NET seguenti:</span><span class="sxs-lookup"><span data-stu-id="208d0-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="208d0-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="208d0-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="208d0-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="208d0-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="208d0-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="208d0-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="208d0-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="208d0-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="208d0-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="208d0-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="208d0-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="208d0-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="208d0-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="208d0-114">**System.Data**</span></span>
* <span data-ttu-id="208d0-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="208d0-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="208d0-116">Aggiunta di stringa di connessione per l'Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="208d0-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="208d0-117">Sono stati creati elementi con la stringa di connessione e la chiave dell'account di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="208d0-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="208d0-118">Sono state apportate modifiche ai file seguenti:</span><span class="sxs-lookup"><span data-stu-id="208d0-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="208d0-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="208d0-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="208d0-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="208d0-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="208d0-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="208d0-121">**ServiceConfiguration.Local.cscfg**</span></span>


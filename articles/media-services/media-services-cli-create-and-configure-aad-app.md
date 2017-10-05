---
title: Usare l'interfaccia della riga di comando 2.0 per creare un'app Azure AD e configurarla per l'accesso all'API Servizi multimediali di Azure | Microsoft Docs
description: Questo argomento illustra come usare l'interfaccia della riga di comando 2.0 per creare un'app Azure AD e configurarla per l'accesso all'API Servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 01a2bb6d99776feec936315bc882c3097ce832d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-cli-20-to-create-an-aad-app-and-configure-it-to-access-azure-media-services-api"></a><span data-ttu-id="fc665-103">Usare l'interfaccia della riga di comando 2.0 per creare un'app AAD e configurarla per l'accesso all'API Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="fc665-103">Use CLI 2.0 to create an AAD app and configure it to access Azure Media Services API</span></span>

<span data-ttu-id="fc665-104">Questo argomento illustra come usare l'interfaccia della riga di comando 2.0 per creare un'applicazione e un'entità servizio di Azure Active Directory (Azure AD) per accedere alle risorse di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc665-104">This topic shows you how to use CLI 2.0 to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fc665-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fc665-105">Prerequisites</span></span>

- <span data-ttu-id="fc665-106">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="fc665-106">An Azure account.</span></span> <span data-ttu-id="fc665-107">Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc665-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="fc665-108">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="fc665-108">A Media Services account.</span></span> <span data-ttu-id="fc665-109">Per altre informazioni, vedere [Creare un account Servizi multimediali di Azure con il portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="fc665-109">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-the-azure-cloud-shell"></a><span data-ttu-id="fc665-110">Usare Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="fc665-110">Use the Azure Cloud Shell</span></span>

1. <span data-ttu-id="fc665-111">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fc665-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fc665-112">Avviare Cloud Shell dal riquadro di spostamento superiore del portale.</span><span class="sxs-lookup"><span data-stu-id="fc665-112">Launch the Cloud Shell from the upper navigation pane of the portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="fc665-114">Per altre informazioni, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc665-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-to-the-media-account-with-cli-20"></a><span data-ttu-id="fc665-115">Creare un'app Azure AD e configurare l'accesso all'account multimediale con l'interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="fc665-115">Create an Azure AD app and configure access to the media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="fc665-116">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fc665-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="fc665-117">In questo esempio l'**ambito** è il percorso completo delle risorse per l'account dei servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="fc665-117">In this example, the **scope** is the full resource path for the media services account.</span></span> <span data-ttu-id="fc665-118">Tuttavia, l'**ambito** può essere definito a qualsiasi livello.</span><span class="sxs-lookup"><span data-stu-id="fc665-118">However, the **scope** can be at any level.</span></span>

<span data-ttu-id="fc665-119">Ad esempio, può essere definito a uno dei livelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="fc665-119">For example, it could be one of the following levels:</span></span>
 
* <span data-ttu-id="fc665-120">Il livello **sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="fc665-120">The **subscription** level.</span></span>
* <span data-ttu-id="fc665-121">Il livello **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="fc665-121">The **resource group** level.</span></span>
* <span data-ttu-id="fc665-122">Il livello **risorsa** (ad esempio, un account multimediale).</span><span class="sxs-lookup"><span data-stu-id="fc665-122">The **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="fc665-123">Per altre informazioni, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="fc665-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="fc665-124">Vedere anche [Gestire il controllo degli accessi in base al ruolo con l'interfaccia della riga di comando di Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fc665-124">Also see [Manage Role-Based Access Control with the Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fc665-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fc665-125">Next steps</span></span>

<span data-ttu-id="fc665-126">Introduzione al [caricamento di file nell'account](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="fc665-126">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>

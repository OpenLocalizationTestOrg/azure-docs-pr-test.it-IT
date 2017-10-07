---
title: toocreate aaaUse CLI 2.0 un'app di Azure AD e configurarlo tooaccess API di servizi multimediali di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come toocreate toouse CLI 2.0 un'app di Azure AD e configurarlo tooaccess API di servizi multimediali di Azure.
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
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="4a8ae-103">Utilizzare toocreate CLI 2.0 un'app di Azure ad e configurarlo tooaccess API di servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="4a8ae-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="4a8ae-104">Questo argomento viene illustrato come toocreate toouse CLI 2.0 un'applicazione Azure Active Directory (Azure AD) e tooaccess dell'entità servizio servizi multimediali di Azure le risorse.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4a8ae-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4a8ae-105">Prerequisites</span></span>

- <span data-ttu-id="4a8ae-106">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-106">An Azure account.</span></span> <span data-ttu-id="4a8ae-107">Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a8ae-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="4a8ae-108">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-108">A Media Services account.</span></span> <span data-ttu-id="4a8ae-109">Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="4a8ae-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="4a8ae-110">Utilizzare hello Shell di Cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="4a8ae-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="4a8ae-111">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4a8ae-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4a8ae-112">Avviare hello Shell Cloud dal riquadro di spostamento superiore hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="4a8ae-114">Per altre informazioni, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a8ae-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="4a8ae-115">Creare un'app di Azure AD e configurare account di accesso toohello multimediali con 2.0 CLI</span><span class="sxs-lookup"><span data-stu-id="4a8ae-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="4a8ae-116">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4a8ae-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="4a8ae-117">In questo esempio hello **ambito** è il percorso completo della risorsa hello per i supporti hello account di servizi.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="4a8ae-118">Tuttavia, hello **ambito** può essere qualsiasi livello.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="4a8ae-119">Ad esempio, potrebbe essere uno dei seguenti livelli di hello:</span><span class="sxs-lookup"><span data-stu-id="4a8ae-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="4a8ae-120">Hello **sottoscrizione** livello.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-120">hello **subscription** level.</span></span>
* <span data-ttu-id="4a8ae-121">Hello **gruppo di risorse** livello.</span><span class="sxs-lookup"><span data-stu-id="4a8ae-121">hello **resource group** level.</span></span>
* <span data-ttu-id="4a8ae-122">Hello **risorse** livello (ad esempio, un account di supporto).</span><span class="sxs-lookup"><span data-stu-id="4a8ae-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="4a8ae-123">Per altre informazioni, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="4a8ae-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="4a8ae-124">Vedere anche [Manage Role-Based il controllo di accesso con l'interfaccia della riga di comando di Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4a8ae-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a8ae-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a8ae-125">Next steps</span></span>

<span data-ttu-id="4a8ae-126">Introduzione a [caricamento file account tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="4a8ae-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>

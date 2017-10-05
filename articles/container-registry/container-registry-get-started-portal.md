---
title: Creare un registro per contenitori Docker privati - Portale di Azure | Microsoft Docs
description: Introduzione alla creazione e gestione dei registri per contenitori Docker privati con il portale di Azure
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7fbbb56d775ee96c9a44363a4e41d4fc3c630582
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-portal"></a><span data-ttu-id="fd94c-103">Creare un registro per contenitori Docker privati con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fd94c-103">Create a private Docker container registry using the Azure portal</span></span>
<span data-ttu-id="fd94c-104">Usare il portale di Azure per creare un registro contenitori e gestirne le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="fd94c-104">Use the Azure portal to create a container registry and manage its settings.</span></span> <span data-ttu-id="fd94c-105">È anche possibile creare e gestire registri di contenitori usando i comandi dell'[interfaccia della riga di comando di Azure 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) oppure, a livello di codice, con l'[API REST](https://go.microsoft.com/fwlink/p/?linkid=834376) del servizio Registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="fd94c-105">You can also create and manage container registries using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="fd94c-106">Per informazioni di base e concetti, vedere la [panoramica](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="fd94c-106">For background and concepts, see [the overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="fd94c-107">Creare un registro contenitori</span><span class="sxs-lookup"><span data-stu-id="fd94c-107">Create a container registry</span></span>
1. <span data-ttu-id="fd94c-108">Nel [portale di Azure](https://portal.azure.com) fare clic su **+ Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="fd94c-108">In the [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="fd94c-109">Cercare **Registro contenitori di Azure** nel Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fd94c-109">Search the marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="fd94c-110">Selezionare **Registro contenitori di Azure** pubblicato da **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="fd94c-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="fd94c-111">![Servizio Registro contenitori in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="fd94c-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="fd94c-112">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fd94c-112">Click **Create**.</span></span> <span data-ttu-id="fd94c-113">Verrà visualizzato il pannello **Registro contenitori di Azure**.</span><span class="sxs-lookup"><span data-stu-id="fd94c-113">The **Azure Container Registry** blade appears.</span></span>

    ![Impostazioni di Registro contenitori](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="fd94c-115">Nel pannello **Registro contenitori di Azure** immettere le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="fd94c-115">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="fd94c-116">Al termine dell'operazione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fd94c-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="fd94c-117">a.</span><span class="sxs-lookup"><span data-stu-id="fd94c-117">a.</span></span> <span data-ttu-id="fd94c-118">**Registry name** (Nome registro): nome di dominio di primo livello univoco globale per il registro.</span><span class="sxs-lookup"><span data-stu-id="fd94c-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="fd94c-119">Il nome del registro negli esempi è *myRegistry01*, ma è necessario sostituirlo con un nome univoco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="fd94c-119">In this example, the registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="fd94c-120">Il nome può contenere solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="fd94c-120">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="fd94c-121">b.</span><span class="sxs-lookup"><span data-stu-id="fd94c-121">b.</span></span> <span data-ttu-id="fd94c-122">**Resource group** (Gruppo di risorse): selezionare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) esistente o specificare il nome di un nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="fd94c-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="fd94c-123">c.</span><span class="sxs-lookup"><span data-stu-id="fd94c-123">c.</span></span> <span data-ttu-id="fd94c-124">**Location** (Posizione): selezionare la posizione di un data center di Azure in cui il servizio è [disponibile](https://azure.microsoft.com/regions/services/), ad esempio **Stati Uniti centro-meridionali**.</span><span class="sxs-lookup"><span data-stu-id="fd94c-124">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="fd94c-125">d.</span><span class="sxs-lookup"><span data-stu-id="fd94c-125">d.</span></span> <span data-ttu-id="fd94c-126">**Admin user** (Utente amministratore): consentire eventualmente a un utente amministratore di accedere al registro.</span><span class="sxs-lookup"><span data-stu-id="fd94c-126">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="fd94c-127">È possibile modificare questa impostazione dopo aver creato il registro.</span><span class="sxs-lookup"><span data-stu-id="fd94c-127">You can change this setting after creating the registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="fd94c-128">Oltre a consentire l'accesso tramite un account utente amministratore, i registri dei contenitori supportano l'autenticazione basata sulle entità servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd94c-128">In addition to providing access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="fd94c-129">Per altre informazioni e considerazioni, vedere [Authenticate with the container registry](container-registry-authentication.md) (Eseguire l'autenticazione al registro contenitori).</span><span class="sxs-lookup"><span data-stu-id="fd94c-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="fd94c-130">e.</span><span class="sxs-lookup"><span data-stu-id="fd94c-130">e.</span></span> <span data-ttu-id="fd94c-131">**Storage account** (Account di archiviazione): usare l'impostazione predefinita per creare un [account di archiviazione](../storage/common/storage-introduction.md) oppure selezionarne uno esistente nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="fd94c-131">**Storage account**: Use the default setting to create a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in the same location.</span></span> <span data-ttu-id="fd94c-132">Archiviazione Premium non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="fd94c-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="fd94c-133">Gestire le impostazioni del registro</span><span class="sxs-lookup"><span data-stu-id="fd94c-133">Manage registry settings</span></span>
<span data-ttu-id="fd94c-134">Dopo aver creato il registro, trovare le impostazioni iniziando dal pannello **Container Registries** (Registri dei contenitori) nel portale.</span><span class="sxs-lookup"><span data-stu-id="fd94c-134">After creating the registry, find the registry settings by starting at the **Container Registries** blade in the portal.</span></span> <span data-ttu-id="fd94c-135">Le impostazioni potrebbero essere ad esempio necessarie per accedere al registro o abilitare o disabilitare l'utente amministratore.</span><span class="sxs-lookup"><span data-stu-id="fd94c-135">For example, you might need the settings to log in to your registry, or you might want to enable or disable the admin user.</span></span>

1. <span data-ttu-id="fd94c-136">Nel pannello **Container Registries** (Registri dei contenitori) fare clic sul nome del registro.</span><span class="sxs-lookup"><span data-stu-id="fd94c-136">On the **Container Registries** blade, click the name of your registry.</span></span>

    ![Pannello Container Registries (Registri dei contenitori)](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="fd94c-138">Per gestire le impostazioni di accesso, fare clic su **Access key** (Chiave di accesso).</span><span class="sxs-lookup"><span data-stu-id="fd94c-138">To manage access settings, click **Access key**.</span></span>

    ![Accesso al registro contenitori](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="fd94c-140">Si notino le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd94c-140">Note the following settings:</span></span>

   * <span data-ttu-id="fd94c-141">**Login server** (Server di accesso): nome completo usato per accedere al registro.</span><span class="sxs-lookup"><span data-stu-id="fd94c-141">**Login server** - The fully qualified name you use to log in to the registry.</span></span> <span data-ttu-id="fd94c-142">In questo esempio si tratta di `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="fd94c-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="fd94c-143">**Admin user** (Utente amministratore): abilita o disabilita l'account utente amministratore per il registro.</span><span class="sxs-lookup"><span data-stu-id="fd94c-143">**Admin user** - Toggle to enable or disable the registry's admin user account.</span></span>
   * <span data-ttu-id="fd94c-144">**Username** (Nome utente) e **Password**: credenziali dell'account utente amministratore (se abilitato) che può essere usato per accedere al registro.</span><span class="sxs-lookup"><span data-stu-id="fd94c-144">**Username** and **Password** - The credentials of the admin user account (if enabled) you can use to log in to the registry.</span></span> <span data-ttu-id="fd94c-145">È facoltativamente possibile rigenerare le password.</span><span class="sxs-lookup"><span data-stu-id="fd94c-145">You can optionally regenerate the passwords.</span></span> <span data-ttu-id="fd94c-146">Vengono create due password in modo da mantenere le connessioni al registro usando una password mentre si rigenera l'altra.</span><span class="sxs-lookup"><span data-stu-id="fd94c-146">Two passwords are created so that you can maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="fd94c-147">Per eseguire invece l'autenticazione con un'entità servizio, vedere [Eseguire l'autenticazione con un registro contenitori Docker privato](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fd94c-147">To authenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd94c-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd94c-148">Next steps</span></span>
* [<span data-ttu-id="fd94c-149">Effettuare il push della prima immagine tramite l'interfaccia della riga di comando di Docker</span><span class="sxs-lookup"><span data-stu-id="fd94c-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)

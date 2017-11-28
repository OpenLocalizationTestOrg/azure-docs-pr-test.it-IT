---
title: aaaCreate privata Docker Registro di sistema - portale di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello portale di Azure
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
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="71c11-103">Creare un registro di sistema contenitore Docker privata mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="71c11-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="71c11-104">Utilizzare hello toocreate portale Azure del Registro di sistema un contenitore e gestire le relative impostazioni.</span><span class="sxs-lookup"><span data-stu-id="71c11-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="71c11-105">È anche possibile creare e gestire i registri di contenitore usando hello [comandi CLI di Azure 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) o a livello di codice con hello contenitore del Registro di sistema [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="71c11-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="71c11-106">Per lo sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="71c11-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="71c11-107">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="71c11-107">Create a container registry</span></span>
1. <span data-ttu-id="71c11-108">In hello [portale di Azure](https://portal.azure.com), fare clic su **+ nuovo**.</span><span class="sxs-lookup"><span data-stu-id="71c11-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="71c11-109">Marketplace hello ricerca per **Registro di sistema di contenitore di Azure**.</span><span class="sxs-lookup"><span data-stu-id="71c11-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="71c11-110">Selezionare **Registro contenitori di Azure** pubblicato da **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="71c11-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="71c11-111">![Servizio Registro contenitori in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="71c11-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="71c11-112">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="71c11-112">Click **Create**.</span></span> <span data-ttu-id="71c11-113">Hello **Registro di sistema di Azure contenitore** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="71c11-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Impostazioni di Registro contenitori](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="71c11-115">In hello **Registro di sistema di Azure contenitore** pannello, immettere le seguenti informazioni hello.</span><span class="sxs-lookup"><span data-stu-id="71c11-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="71c11-116">Al termine dell'operazione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="71c11-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="71c11-117">a.</span><span class="sxs-lookup"><span data-stu-id="71c11-117">a.</span></span> <span data-ttu-id="71c11-118">**Registry name** (Nome registro): nome di dominio di primo livello univoco globale per il registro.</span><span class="sxs-lookup"><span data-stu-id="71c11-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="71c11-119">In questo esempio, nome del Registro di sistema hello è *myRegistry01*, ma sostituire un nome univoco del proprio.</span><span class="sxs-lookup"><span data-stu-id="71c11-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="71c11-120">Hello nome può contenere solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="71c11-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="71c11-121">b.</span><span class="sxs-lookup"><span data-stu-id="71c11-121">b.</span></span> <span data-ttu-id="71c11-122">**Gruppo di risorse**: selezionare un oggetto esistente [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="71c11-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="71c11-123">c.</span><span class="sxs-lookup"><span data-stu-id="71c11-123">c.</span></span> <span data-ttu-id="71c11-124">**Percorso**: selezionare un Data Center di Azure posizione servizio hello [disponibile](https://azure.microsoft.com/regions/services/), ad esempio **centro-meridionali**.</span><span class="sxs-lookup"><span data-stu-id="71c11-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="71c11-125">d.</span><span class="sxs-lookup"><span data-stu-id="71c11-125">d.</span></span> <span data-ttu-id="71c11-126">**L'utente amministratore**: se si desidera, attivare del Registro di sistema hello tooaccess utente amministratore.</span><span class="sxs-lookup"><span data-stu-id="71c11-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="71c11-127">È possibile modificare questa impostazione dopo la creazione del Registro di sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="71c11-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="71c11-128">Inoltre l'accesso a tooproviding tramite un account utente di amministratore, i registri di contenitore supportano l'autenticazione supportato da entità di servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71c11-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="71c11-129">Per altre informazioni e considerazioni, vedere [Authenticate with the container registry](container-registry-authentication.md) (Eseguire l'autenticazione al registro contenitori).</span><span class="sxs-lookup"><span data-stu-id="71c11-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="71c11-130">e.</span><span class="sxs-lookup"><span data-stu-id="71c11-130">e.</span></span> <span data-ttu-id="71c11-131">**Account di archiviazione**: utilizzare hello predefinito impostazione toocreate un [account di archiviazione](../storage/common/storage-introduction.md), oppure selezionare un account di archiviazione esistente nell'hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="71c11-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="71c11-132">Archiviazione Premium non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="71c11-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="71c11-133">Gestire le impostazioni del registro</span><span class="sxs-lookup"><span data-stu-id="71c11-133">Manage registry settings</span></span>
<span data-ttu-id="71c11-134">Dopo la creazione del Registro di sistema di hello, trovare hello le impostazioni del Registro di sistema iniziando dalla hello **contenitore registri** pannello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="71c11-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="71c11-135">Ad esempio, potrebbe essere necessario hello impostazioni toolog nel Registro di sistema tooyour o si potrebbe desidera tooenable o disabilitare l'utente amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="71c11-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="71c11-136">In hello **contenitore registri** pannello, fare clic sul nome di hello del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="71c11-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Pannello Container Registries (Registri dei contenitori)](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="71c11-138">Fare clic su impostazioni di accesso toomanage, **tasto**.</span><span class="sxs-lookup"><span data-stu-id="71c11-138">toomanage access settings, click **Access key**.</span></span>

    ![Accesso al registro contenitori](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="71c11-140">Si noti hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="71c11-140">Note hello following settings:</span></span>

   * <span data-ttu-id="71c11-141">**Server di accesso** -nome completo di hello è utilizzare toolog toohello del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="71c11-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="71c11-142">In questo esempio si tratta di `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="71c11-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="71c11-143">**L'utente amministratore** - tooenable di attivare o disattivare o disabilitare l'account amministratore del Registro di sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="71c11-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="71c11-144">**Nome utente** e **Password** -hello credenziali dell'account utente di amministrazione hello (se abilitati) è possibile utilizzare toolog toohello del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="71c11-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="71c11-145">È facoltativamente possibile rigenerare le password hello.</span><span class="sxs-lookup"><span data-stu-id="71c11-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="71c11-146">Le due password vengono create in modo che sia possibile gestire Registro di sistema toohello connessioni con una password, mentre si rigenera hello altre password.</span><span class="sxs-lookup"><span data-stu-id="71c11-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="71c11-147">tooauthenticate con un'entità servizio, vedere [eseguire l'autenticazione con un registro di sistema di contenitore Docker privata](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="71c11-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71c11-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71c11-148">Next steps</span></span>
* [<span data-ttu-id="71c11-149">La prima immagine usando Docker CLI hello push</span><span class="sxs-lookup"><span data-stu-id="71c11-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)

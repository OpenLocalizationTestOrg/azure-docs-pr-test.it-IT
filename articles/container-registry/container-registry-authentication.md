---
title: aaaAuthenticate con un registro di sistema del contenitore di Azure | Documenti Microsoft
description: Come toolog nel Registro di sistema di contenitore di Azure tooan usando Azure Active Directory service principale o un account amministratore
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="02b59-103">Eseguire l'autenticazione con un registro contenitori Docker privato</span><span class="sxs-lookup"><span data-stu-id="02b59-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="02b59-104">toowork con immagini contenitore nel Registro di sistema contenitore di Azure, si accede tramite hello `docker login` comando.</span><span class="sxs-lookup"><span data-stu-id="02b59-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="02b59-105">È possibile accedere usando un'**[entità servizio di Azure Active Directory](../active-directory/active-directory-application-objects.md)** o un **account amministratore** specifico del registro.</span><span class="sxs-lookup"><span data-stu-id="02b59-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="02b59-106">In questo articolo vengono fornite maggiori informazioni su tali identità.</span><span class="sxs-lookup"><span data-stu-id="02b59-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="02b59-107">Entità servizio</span><span class="sxs-lookup"><span data-stu-id="02b59-107">Service principal</span></span>

<span data-ttu-id="02b59-108">È possibile [assegnare un'entità servizio](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour Registro di sistema e utilizzarlo per l'autenticazione di base Docker.</span><span class="sxs-lookup"><span data-stu-id="02b59-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="02b59-109">È consigliabile usare un'entità servizio per la maggior parte degli scenari.</span><span class="sxs-lookup"><span data-stu-id="02b59-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="02b59-110">Fornire l'ID app hello e la password di hello servizio principale toohello `docker login` comando, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="02b59-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="02b59-111">Una volta effettuato l'accesso, Docker memorizza nella cache le credenziali di hello, pertanto non è necessario l'ID dell'app tooremember hello.</span><span class="sxs-lookup"><span data-stu-id="02b59-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="02b59-112">Se si desidera, è possibile rigenerare la password di hello di un'entità servizio eseguendo hello `az ad sp reset-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="02b59-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="02b59-113">Consentono l'entità servizio [accesso basato sui ruoli](../active-directory/role-based-access-control-configure.md) tooa Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="02b59-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="02b59-114">I ruoli disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="02b59-114">Available roles are:</span></span>
  * <span data-ttu-id="02b59-115">Lettore (solo accesso pull).</span><span class="sxs-lookup"><span data-stu-id="02b59-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="02b59-116">Collaboratore (accesso pull e push).</span><span class="sxs-lookup"><span data-stu-id="02b59-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="02b59-117">Proprietario (pull, push e assegnare ruoli tooother utenti).</span><span class="sxs-lookup"><span data-stu-id="02b59-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="02b59-118">L'accesso anonimo non è disponibile nei registri contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="02b59-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="02b59-119">Per le immagini pubbliche è possibile utilizzare [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="02b59-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="02b59-120">È possibile assegnare più entità di servizio tooa del Registro di sistema, che consente di accedere a toodefine per diversi utenti o applicazioni.</span><span class="sxs-lookup"><span data-stu-id="02b59-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="02b59-121">Le entità servizio abilitare anche "headless" connettività tooa nel Registro di sistema per sviluppatori o DevOps scenari, ad esempio hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="02b59-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="02b59-122">Distribuzioni di contenitori da sistemi di tooorchestration un registro di sistema inclusi controller di dominio/OS, Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="02b59-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="02b59-123">È possibile anche effettuare il pull toorelated registri contenitore Servizi di Azure, ad esempio [servizio contenitore](../container-service/index.yml), [servizio App](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/)e altri.</span><span class="sxs-lookup"><span data-stu-id="02b59-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="02b59-124">Continua integrazione e distribuzione di soluzioni (ad esempio Visual Studio Team Services o Jenkins) che compilano le immagini contenitore e inviarli tooa Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="02b59-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="02b59-125">Account amministratore</span><span class="sxs-lookup"><span data-stu-id="02b59-125">Admin account</span></span>
<span data-ttu-id="02b59-126">Per ogni registro che si crea viene creato automaticamente un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="02b59-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="02b59-127">Per impostazione predefinita account hello è disabilitata, ma è possibile abilitare e gestire le credenziali di hello, ad esempio tramite hello [portale](container-registry-get-started-portal.md#manage-registry-settings) o tramite hello [comandi CLI di Azure 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="02b59-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="02b59-128">Ogni account amministratore dispone di due password, ognuna rigenerabile.</span><span class="sxs-lookup"><span data-stu-id="02b59-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="02b59-129">due password Hello consentono del Registro di sistema di toomaintain connessioni toohello utilizzando una password mentre si rigenera hello altre password.</span><span class="sxs-lookup"><span data-stu-id="02b59-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="02b59-130">Se hello account è abilitato, è possibile passare il nome di utente hello ed entrambi toohello password `docker login` comando del Registro di sistema di autenticazione di base toohello.</span><span class="sxs-lookup"><span data-stu-id="02b59-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="02b59-131">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02b59-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="02b59-132">account amministratore Hello è progettato per un singolo utente tooaccess hello del Registro di sistema, principalmente per scopi di test.</span><span class="sxs-lookup"><span data-stu-id="02b59-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="02b59-133">Non è consigliabile credenziali dell'account amministratore hello tooshare tra altri utenti.</span><span class="sxs-lookup"><span data-stu-id="02b59-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="02b59-134">Tutti gli utenti vengono visualizzati come un registro di sistema toohello utente singolo.</span><span class="sxs-lookup"><span data-stu-id="02b59-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="02b59-135">La modifica o la disattivazione di questo account Disabilita accesso Registro di sistema per tutti gli utenti che utilizzano le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="02b59-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="02b59-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02b59-136">Next steps</span></span>
* <span data-ttu-id="02b59-137">[La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="02b59-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="02b59-138">Per ulteriori informazioni sull'autenticazione in anteprima di hello contenitore del Registro di sistema, vedere hello [post di blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="02b59-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>

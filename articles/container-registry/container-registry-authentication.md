---
title: Eseguire l'autenticazione con un registro contenitori di Azure | Microsoft Docs
description: "Come accedere a un registro contenitori di Azure usando un'entità servizio di Azure Active Directory o un account amministratore"
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="3d44a-103">Eseguire l'autenticazione con un registro contenitori Docker privato</span><span class="sxs-lookup"><span data-stu-id="3d44a-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="3d44a-104">Per usare le immagini contenitore nel registro contenitori di Azure, accedere usando il comando `docker login`.</span><span class="sxs-lookup"><span data-stu-id="3d44a-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="3d44a-105">È possibile accedere usando un'**[entità servizio di Azure Active Directory](../active-directory/active-directory-application-objects.md)** o un **account amministratore** specifico del registro.</span><span class="sxs-lookup"><span data-stu-id="3d44a-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="3d44a-106">In questo articolo vengono fornite maggiori informazioni su tali identità.</span><span class="sxs-lookup"><span data-stu-id="3d44a-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="3d44a-107">Entità servizio</span><span class="sxs-lookup"><span data-stu-id="3d44a-107">Service principal</span></span>

<span data-ttu-id="3d44a-108">È possibile [assegnare un'entità servizio](container-registry-get-started-azure-cli.md#assign-a-service-principal) nel registro e usarla per eseguire l'autenticazione Docker di base.</span><span class="sxs-lookup"><span data-stu-id="3d44a-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="3d44a-109">È consigliabile usare un'entità servizio per la maggior parte degli scenari.</span><span class="sxs-lookup"><span data-stu-id="3d44a-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="3d44a-110">Fornire l'ID app e la password dell'entità servizio per il comando `docker login`, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3d44a-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="3d44a-111">Dopo aver effettuato l'accesso, Docker memorizza nella cache le credenziali, così da non doversi ricordare l'ID app.</span><span class="sxs-lookup"><span data-stu-id="3d44a-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="3d44a-112">Se lo si desidera, è possibile rigenerare la password di un'entità servizio eseguendo il comando `az ad sp reset-credentials`.</span><span class="sxs-lookup"><span data-stu-id="3d44a-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="3d44a-113">Le entità servizio consentono l'[accesso basato su ruoli](../active-directory/role-based-access-control-configure.md) a un registro.</span><span class="sxs-lookup"><span data-stu-id="3d44a-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="3d44a-114">I ruoli disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="3d44a-114">Available roles are:</span></span>
  * <span data-ttu-id="3d44a-115">Lettore (solo accesso pull).</span><span class="sxs-lookup"><span data-stu-id="3d44a-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="3d44a-116">Collaboratore (accesso pull e push).</span><span class="sxs-lookup"><span data-stu-id="3d44a-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="3d44a-117">Proprietario (accesso pull e push e facoltà di assegnare ruoli ad altri utenti).</span><span class="sxs-lookup"><span data-stu-id="3d44a-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="3d44a-118">L'accesso anonimo non è disponibile nei registri contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d44a-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="3d44a-119">Per le immagini pubbliche è possibile utilizzare [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="3d44a-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="3d44a-120">È possibile assegnare più entità di servizio a un registro, così da poter definire l'accesso per utenti o applicazioni differenti.</span><span class="sxs-lookup"><span data-stu-id="3d44a-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="3d44a-121">Le entità servizio abilitano anche la connettività "headless" a un registro negli scenari DevOps o per sviluppatori, come gli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d44a-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="3d44a-122">Distribuzioni di contenitori da un registro ai sistemi di orchestrazione, tra cui DC/OS, Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="3d44a-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="3d44a-123">È anche possibile eseguire il pull dei registri contenitori a servizi di Azure correlati, come [Servizio contenitore](../container-service/index.yml), [Servizio App](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) e altri.</span><span class="sxs-lookup"><span data-stu-id="3d44a-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="3d44a-124">Soluzioni di distribuzione e integrazione continua (ad esempio Visual Studio Team Services o Jenkins) che creano immagini contenitore e le inviano a un registro.</span><span class="sxs-lookup"><span data-stu-id="3d44a-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="3d44a-125">Account amministratore</span><span class="sxs-lookup"><span data-stu-id="3d44a-125">Admin account</span></span>
<span data-ttu-id="3d44a-126">Per ogni registro che si crea viene creato automaticamente un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="3d44a-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="3d44a-127">Per impostazione predefinita l'account è disabilitato, ma è possibile abilitarlo e gestirne le credenziali, ad esempio tramite il [portale](container-registry-get-started-portal.md#manage-registry-settings) o con i [comandi dell'interfaccia della riga di comando di Azure 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="3d44a-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="3d44a-128">Ogni account amministratore dispone di due password, ognuna rigenerabile.</span><span class="sxs-lookup"><span data-stu-id="3d44a-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="3d44a-129">Le due password consentono di mantenere le connessioni al registro usando una password mentre si rigenera l'altra.</span><span class="sxs-lookup"><span data-stu-id="3d44a-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="3d44a-130">Se l'account è abilitato, è possibile passare il nome utente e la password al comando `docker login` per l'autenticazione di base per accedere al registro.</span><span class="sxs-lookup"><span data-stu-id="3d44a-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="3d44a-131">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3d44a-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="3d44a-132">L'account amministratore è pensato per l'accesso di un singolo utente al registro, principalmente per fare dei test.</span><span class="sxs-lookup"><span data-stu-id="3d44a-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="3d44a-133">Non è consigliabile condividere le credenziali dell'account amministratore con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="3d44a-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="3d44a-134">Tutti gli utenti vengono visualizzati come un singolo utente nel registro.</span><span class="sxs-lookup"><span data-stu-id="3d44a-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="3d44a-135">La modifica o la disattivazione di questo account disabilita l'accesso al registro da parte di tutti gli utenti che usano quelle credenziali.</span><span class="sxs-lookup"><span data-stu-id="3d44a-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="3d44a-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d44a-136">Next steps</span></span>
* <span data-ttu-id="3d44a-137">[Eseguire il push della prima immagine con l'interfaccia della riga di comando di Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3d44a-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="3d44a-138">Per altre informazioni sull'autenticazione nell'anteprima del registro contenitori, vedere il [post di blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="3d44a-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>

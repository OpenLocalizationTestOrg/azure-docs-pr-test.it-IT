---
title: Credenziali per la distribuzione del Servizio app di Azure | Microsoft Docs
description: Informazioni su come usare le credenziali per la distribuzione del Servizio app di Azure.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="da2b6-103">Configurazione delle credenziali per la distribuzione del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="da2b6-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="da2b6-104">Il [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) supporta due tipi di credenziali per la [distribuzione di GIT locale](app-service-deploy-local-git.md) e la [distribuzione FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="da2b6-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="da2b6-105">Queste credenziali non corrispondono alle credenziali di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da2b6-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="da2b6-106">**Credenziali a livello di utente**: un insieme di credenziali per tutto l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="da2b6-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="da2b6-107">Può essere usato per distribuire il Servizio app per qualsiasi app, in tutte le sottoscrizioni a cui l'account di Azure è autorizzato ad accedere.</span><span class="sxs-lookup"><span data-stu-id="da2b6-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="da2b6-108">Si tratta dell'insieme di credenziali predefinito configurabile in **Servizi app** > **&lt;nome_app>** > **Credenziali per la distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="da2b6-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="da2b6-109">Si tratta inoltre dell'insieme predefinito indicato nella GUI del portale, ad esempio **Panoramica** e **Proprietà** nel [pannello risorse](../azure-resource-manager/resource-group-portal.md#manage-resources) dell'app.</span><span class="sxs-lookup"><span data-stu-id="da2b6-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="da2b6-110">Quando si delega l'accesso alle risorse di Azure tramite controllo degli accessi in base al ruolo o autorizzazioni di coamministratore, ogni utente Azure che riceve l'accesso a un'app può usare le sue credenziali a livello utente fino a quando l'accesso non viene revocato.</span><span class="sxs-lookup"><span data-stu-id="da2b6-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="da2b6-111">Queste credenziali di distribuzione non devono essere condivise con altri utenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="da2b6-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="da2b6-112">**Credenziali a livello di applicazione**: un insieme di credenziali per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="da2b6-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="da2b6-113">Può essere usato per distribuire solo in quella app.</span><span class="sxs-lookup"><span data-stu-id="da2b6-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="da2b6-114">Le credenziali per ogni app sono generate automaticamente alla creazione dell'app stessa e si trovano nel suo profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="da2b6-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="da2b6-115">Non è possibile configurare manualmente le credenziali per un'applicazione, ma è possibile reimpostarle in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="da2b6-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="da2b6-116">Per consentire a un utente di accedere a queste credenziali tramite il controllo degli accessi in base al ruolo, è necessario assegnare all'utente il ruolo di collaboratore o un ruolo superiore per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="da2b6-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="da2b6-117">Poiché non hanno l'autorizzazione per la pubblicazione, i lettori non possono accedere a queste credenziali.</span><span class="sxs-lookup"><span data-stu-id="da2b6-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="da2b6-118"><a name="userscope"></a>Impostare e reimpostare le credenziali a livello di utente</span><span class="sxs-lookup"><span data-stu-id="da2b6-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="da2b6-119">È possibile configurare le credenziali a livello di utente nel [pannello risorse](../azure-resource-manager/resource-group-portal.md#manage-resources) di ogni app.</span><span class="sxs-lookup"><span data-stu-id="da2b6-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="da2b6-120">Indipendentemente dall'app, le credenziali configurate si applicano a tutte le app e a tutte le sottoscrizioni nell'account di Azure dell'utente.</span><span class="sxs-lookup"><span data-stu-id="da2b6-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="da2b6-121">Per configurare le credenziali a livello di utente:</span><span class="sxs-lookup"><span data-stu-id="da2b6-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="da2b6-122">Nel [portale di Azure](https://portal.azure.com), fare clic su Servizio app > **&lt;qualsiasi_app>** > **Credenziali per la distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="da2b6-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="da2b6-123">È necessario disporre di almeno un'app nel portale prima di poter accedere al pannello delle credenziali per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="da2b6-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="da2b6-124">Tuttavia, con l'[interfaccia della riga di comando di Azure](app-service-web-app-azure-resource-manager-xplat-cli.md) è possibile configurare le credenziali a livello di utente senza un'app esistente.</span><span class="sxs-lookup"><span data-stu-id="da2b6-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="da2b6-125">Configurare il nome utente e la password e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="da2b6-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="da2b6-126">Dopo aver impostato le credenziali per la distribuzione, è possibile trovare il nome utente per la distribuzione di *GIT* nella **Panoramica** dell'app,</span><span class="sxs-lookup"><span data-stu-id="da2b6-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="da2b6-127">oltre a un nome utente per la distribuzione *FTP* nelle **Proprietà** dell'app.</span><span class="sxs-lookup"><span data-stu-id="da2b6-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="da2b6-128">Azure non mostra la password di distribuzione a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="da2b6-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="da2b6-129">Se si dimentica la password, non è possibile recuperarla.</span><span class="sxs-lookup"><span data-stu-id="da2b6-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="da2b6-130">Tuttavia, è possibile reimpostare le credenziali seguendo i passaggi descritti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="da2b6-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="da2b6-131"><a name="appscope"></a>Ottenere e reimpostare le credenziali a livello di utente</span><span class="sxs-lookup"><span data-stu-id="da2b6-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="da2b6-132">Per ogni app nel servizio app, le credenziali a livello di app vengono archiviate nel file XML del profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="da2b6-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="da2b6-133">Per ottenere le credenziali a livello di app:</span><span class="sxs-lookup"><span data-stu-id="da2b6-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="da2b6-134">Nel [portale di Azure](https://portal.azure.com), fare clic su Servizio app > **&lt;qualsiasi_app>** > **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="da2b6-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="da2b6-135">Fare clic su **...More** (...Altro) > **Recupera profilo di pubblicazione** per avviare il download di un file .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="da2b6-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="da2b6-136">Aprire il file .PublishSettings e trovare il tag `<publishProfile>` con l'attributo `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="da2b6-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="da2b6-137">Quindi, ottenere i relativi attributi `userName` e `password`.</span><span class="sxs-lookup"><span data-stu-id="da2b6-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="da2b6-138">Si tratta delle credenziali a livello di app.</span><span class="sxs-lookup"><span data-stu-id="da2b6-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="da2b6-139">Come per le credenziali a livello di utente, il nome utente di distribuzione dell'FTP è nel formato `<app_name>\<username>`, mentre quello della distribuzione è Git è solo `<username>` senza `<app_name>\` a precedere.</span><span class="sxs-lookup"><span data-stu-id="da2b6-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="da2b6-140">Per reimpostare le credenziali a livello di app:</span><span class="sxs-lookup"><span data-stu-id="da2b6-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="da2b6-141">Nel [portale di Azure](https://portal.azure.com), fare clic su Servizio app >  **&lt;qualsiasi_app>** > **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="da2b6-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="da2b6-142">Fare clic su **...More** (...Altro) > **Reimposta profilo di pubblicazione**.</span><span class="sxs-lookup"><span data-stu-id="da2b6-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="da2b6-143">Fare clic su **Sì** per confermare la reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="da2b6-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="da2b6-144">L'operazione di reimpostazione invalida qualsiasi file .PublishSettings scaricato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="da2b6-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da2b6-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da2b6-145">Next steps</span></span>

<span data-ttu-id="da2b6-146">Informazioni su come usare queste credenziali per distribuire l'app da [GIT locale](app-service-deploy-local-git.md) o usando [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="da2b6-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>

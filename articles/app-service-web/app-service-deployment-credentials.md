---
title: le credenziali di distribuzione di servizio App aaaAzure | Documenti Microsoft
description: Informazioni su come toouse hello le credenziali di distribuzione di servizio App di Azure.
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
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="a6346-103">Configurazione delle credenziali per la distribuzione del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a6346-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="a6346-104">Il [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) supporta due tipi di credenziali per la [distribuzione di GIT locale](app-service-deploy-local-git.md) e la [distribuzione FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="a6346-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="a6346-105">Questi non sono hello stesso come credenziali di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6346-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="a6346-106">**Le credenziali a livello di utente**: un insieme di credenziali per l'intero account Azure di hello.</span><span class="sxs-lookup"><span data-stu-id="a6346-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="a6346-107">Può essere utilizzato toodeploy tooApp servizio per qualsiasi app, in tutte le sottoscrizioni, hello account Azure dispone di autorizzazione tooaccess.</span><span class="sxs-lookup"><span data-stu-id="a6346-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="a6346-108">Si tratta di set di credenziali predefinito hello configurate in **servizi App** > **&lt;nome_app >** > **lecredenzialididistribuzione**.</span><span class="sxs-lookup"><span data-stu-id="a6346-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="a6346-109">Questo è anche hello set predefinito che viene esposto in portale hello GUI (ad esempio hello **Panoramica** e **proprietà** della tua app [pannello della risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="a6346-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a6346-110">Quando si delegano tooAzure di accedere alle risorse tramite basato sui ruoli accesso controllo (RBAC) o le autorizzazioni di co-amministratore, ogni utente di Azure che riceve l'accesso tooan app può utilizzare proprie credenziali a livello di utente personali fino a quando non viene revocato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a6346-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="a6346-111">Queste credenziali di distribuzione non devono essere condivise con altri utenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6346-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="a6346-112">**Credenziali a livello di applicazione**: un insieme di credenziali per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6346-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="a6346-113">Può essere utilizzato toodeploy toothat app solo.</span><span class="sxs-lookup"><span data-stu-id="a6346-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="a6346-114">le credenziali di Hello per ogni app viene generato automaticamente al momento della creazione di app ed è disponibile dell'applicazione hello profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a6346-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="a6346-115">Non è possibile configurare manualmente le credenziali di hello, ma è possibile reimpostarle per un'app in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="a6346-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a6346-116">In ordine toogive un utente l'accesso le credenziali toothese tramite basato sui ruoli accesso controllo (RBAC), è necessario toomake li collaboratore o versione successiva hello App Web.</span><span class="sxs-lookup"><span data-stu-id="a6346-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="a6346-117">I lettori non sono consentiti toopublish e pertanto non è possibile accedere a tali credenziali.</span><span class="sxs-lookup"><span data-stu-id="a6346-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="a6346-118"><a name="userscope"></a>Impostare e reimpostare le credenziali a livello di utente</span><span class="sxs-lookup"><span data-stu-id="a6346-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="a6346-119">È possibile configurare le credenziali a livello di utente nel [pannello risorse](../azure-resource-manager/resource-group-portal.md#manage-resources) di ogni app.</span><span class="sxs-lookup"><span data-stu-id="a6346-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="a6346-120">Indipendentemente dal fatto che nella quale app configurare queste credenziali, viene applicato tooall App e per tutte le sottoscrizioni di Azure dell'account.</span><span class="sxs-lookup"><span data-stu-id="a6346-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="a6346-121">tooconfigure le credenziali a livello di utente:</span><span class="sxs-lookup"><span data-stu-id="a6346-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="a6346-122">In hello [portale di Azure](https://portal.azure.com), fare clic su servizio App >  **&lt;any_app >** > **le credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="a6346-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a6346-123">Nel portale di hello, è necessario disporre di almeno un'app prima di poter accedere pannello credenziali di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="a6346-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="a6346-124">Tuttavia, con hello [CLI di Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), è possibile configurare le credenziali a livello di utente senza un'app esistente.</span><span class="sxs-lookup"><span data-stu-id="a6346-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="a6346-125">Configurare il nome di utente hello e una password e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="a6346-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="a6346-126">Dopo aver impostato le credenziali di distribuzione, è possibile trovare hello *Git* nome utente di distribuzione dell'app **Panoramica**,</span><span class="sxs-lookup"><span data-stu-id="a6346-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="a6346-127">oltre a un nome utente per la distribuzione *FTP* nelle **Proprietà** dell'app.</span><span class="sxs-lookup"><span data-stu-id="a6346-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="a6346-128">Azure non mostra la password di distribuzione a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="a6346-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="a6346-129">Se si dimentica la password di hello, non possono essere recuperati.</span><span class="sxs-lookup"><span data-stu-id="a6346-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="a6346-130">Tuttavia, è possibile reimpostare le credenziali seguendo i passaggi di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="a6346-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="a6346-131"><a name="appscope"></a>Ottenere e reimpostare le credenziali a livello di utente</span><span class="sxs-lookup"><span data-stu-id="a6346-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="a6346-132">Per ogni applicazione nel servizio App, le credenziali a livello di applicazione vengono archiviate in hello XML profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a6346-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="a6346-133">credenziali a livello di applicazione hello tooget:</span><span class="sxs-lookup"><span data-stu-id="a6346-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="a6346-134">In hello [portale di Azure](https://portal.azure.com), fare clic su servizio App >  **&lt;any_app >** > **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="a6346-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="a6346-135">Fare clic su **...More** (...Altro) > **Recupera profilo di pubblicazione** per avviare il download di un file .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="a6346-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="a6346-136">Aprire hello. Trovare hello e file PublishSettings `<publishProfile>` tag con attributo hello `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="a6346-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="a6346-137">Quindi, ottenere i relativi attributi `userName` e `password`.</span><span class="sxs-lookup"><span data-stu-id="a6346-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="a6346-138">Si tratta di credenziali a livello di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a6346-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="a6346-139">Credenziali a livello di utente toohello analoghe, nome utente di distribuzione FTP hello è nel formato di hello delle `<app_name>\<username>`, e nome utente di distribuzione Git hello è semplicemente `<username>` senza hello precedente `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="a6346-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="a6346-140">credenziali a livello di applicazione hello tooreset:</span><span class="sxs-lookup"><span data-stu-id="a6346-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="a6346-141">In hello [portale di Azure](https://portal.azure.com), fare clic su servizio App >  **&lt;any_app >** > **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="a6346-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="a6346-142">Fare clic su **...More** (...Altro) > **Reimposta profilo di pubblicazione**.</span><span class="sxs-lookup"><span data-stu-id="a6346-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="a6346-143">Fare clic su **Sì** tooconfirm hello Reimposta.</span><span class="sxs-lookup"><span data-stu-id="a6346-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="a6346-144">l'azione reset Hello invalida qualsiasi scaricati in precedenza. File PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="a6346-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6346-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6346-145">Next steps</span></span>

<span data-ttu-id="a6346-146">Scoprire come toouse toodeploy queste credenziali l'app da [Git locale](app-service-deploy-local-git.md) o tramite [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="a6346-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>

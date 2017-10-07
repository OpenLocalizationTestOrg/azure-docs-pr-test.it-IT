---
title: un'app di Azure line-of-business con l'autenticazione di Azure Active Directory aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un ASP.NET MVC line-of-business app in Azure App Service che esegue l'autenticazione con Azure Active Directory
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="d0b3a-103">Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0b3a-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="d0b3a-104">In questo articolo illustra come app toocreate un .NET line-of-business in [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) utilizzando hello [autenticazione / autorizzazione](../app-service/app-service-authentication-overview.md) funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="d0b3a-105">Viene inoltre illustrato come hello toouse [API di Graph di Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery dati della directory in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="d0b3a-106">tenant di Azure Active Directory Hello in uso può essere una directory di Azure-only.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="d0b3a-107">In alternativa, può essere [sincronizzati con Active Directory locale](../active-directory/active-directory-aadconnect.md) toocreate un'esperienza single sign-on per i processi di lavoro locali e remoti.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="d0b3a-108">In questo articolo Usa directory predefinita hello per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="d0b3a-109">Obiettivo di compilazione</span><span class="sxs-lookup"><span data-stu-id="d0b3a-109">What you will build</span></span>
<span data-ttu-id="d0b3a-110">Si creerà una semplice applicazione di line-of-business Create-lettura, aggiornamento ed eliminazione (CRUD) nelle App Web di servizio App che tiene traccia elementi di lavoro con hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="d0b3a-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="d0b3a-111">Autenticazione degli utenti con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0b3a-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="d0b3a-112">Esecuzione di query su utenti e gruppi della directory tramite l' [API Graph di Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="d0b3a-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="d0b3a-113">Utilizzare hello ASP.NET MVC *Nessuna autenticazione* modello</span><span class="sxs-lookup"><span data-stu-id="d0b3a-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="d0b3a-114">Se è necessario il Controllo degli accessi in base al ruolo per l'applicazione line-of-business in Azure, vedere il [passaggio successivo](#next).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="d0b3a-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="d0b3a-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="d0b3a-116">È necessario hello seguenti toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="d0b3a-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="d0b3a-117">Un tenant di Azure Active Directory con utenti in diversi gruppi</span><span class="sxs-lookup"><span data-stu-id="d0b3a-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="d0b3a-118">Autorizzazioni toocreate applicazioni nel tenant di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="d0b3a-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="d0b3a-119">Visual Studio 2013 Update 4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="d0b3a-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="d0b3a-120">Azure SDK 2.8.1 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="d0b3a-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="d0b3a-121">Creare e distribuire un tooAzure app web</span><span class="sxs-lookup"><span data-stu-id="d0b3a-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="d0b3a-122">In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="d0b3a-123">Selezionare **Applicazione Web ASP.NET**, assegnare un nome al progetto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="d0b3a-124">Seleziona hello **MVC** modello, quindi modificare anche l'autenticazione di hello**Nessuna autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="d0b3a-125">Assicurarsi che **Host nel Cloud hello** è selezionata e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="d0b3a-126">In hello **Crea servizio App** finestra di dialogo, fare clic su **aggiungere un account** (e quindi **aggiungere un account** nell'elenco a discesa hello) toolog in tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="d0b3a-127">Dopo aver eseguito l'accesso, configurare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-127">Once logged in configure your web app.</span></span> <span data-ttu-id="d0b3a-128">Creare un gruppo di risorse e un nuovo piano di servizio App facendo clic sul rispettivo hello **New** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="d0b3a-129">Fare clic su **esplorare servizi di Azure aggiuntivi** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="d0b3a-130">In hello **servizi** scheda, fare clic su  **+**  tooadd un Database SQL per l'app.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="d0b3a-131">In **configurare il Database SQL**, fare clic su **New** toocreate un'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="d0b3a-132">In **Configura SQL Server**configurare l'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="d0b3a-133">Quindi, fare clic su **OK**, **OK**, e **crea** tookick off della creazione dell'app hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="d0b3a-134">In **attività di servizio App di Azure**, è possibile visualizzare al termine della creazione dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="d0b3a-135">Fare clic su  **pubblica &lt;* appname*> toothis App Web adesso * *, quindi fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="d0b3a-136">Al termine del processo di Visual Studio, viene aperto hello pubblicare app nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="d0b3a-137">Configurare l'autenticazione e l'accesso alla directory</span><span class="sxs-lookup"><span data-stu-id="d0b3a-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="d0b3a-138">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d0b3a-139">Scegliere dal menu a sinistra hello **servizi App** > **&lt;*appname*> * * > **autenticazione / autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="d0b3a-140">Attivare l'autenticazione di Azure Active Directory facendo clic su **Attivato** > **Azure Active Directory** > **Rapida** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="d0b3a-141">Fare clic su **salvare** nella barra dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="d0b3a-142">Una volta che le impostazioni di autenticazione hello vengono salvate correttamente, tenta di spostarsi app tooyour nuovamente nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="d0b3a-143">Le impostazioni predefinite imporre l'autenticazione al hello intera app.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="d0b3a-144">Se non già effettuato l'accesso, verrà reindirizzato tooa schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="d0b3a-145">Dopo aver effettuato l'accesso, verrà visualizzata l'app protetta tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="d0b3a-146">Successivamente, è necessario accedere a tooenable toodirectory dati.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="d0b3a-147">Passare toohello [portale classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="d0b3a-148">Scegliere dal menu a sinistra hello **Active Directory** > **Directory predefinita** > **applicazioni**  >   **&lt;* appname*> * *.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="d0b3a-149">Si tratta di un'applicazione hello Azure Active Directory creati per si tooenable hello autorizzazione servizio App o funzionalità di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="d0b3a-150">Fare clic su **utenti** e **gruppi** toomake certi di disporre di alcuni utenti e gruppi nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="d0b3a-151">In caso contrario, creare alcuni utenti e gruppi di test.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="d0b3a-152">Fare clic su **configura** tooconfigure questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="d0b3a-153">Scorrere verso il basso toohello **chiavi** sezione e aggiungere una chiave, selezionare una durata.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="d0b3a-154">Fare quindi clic su **Autorizzazioni delegate** e selezionare **Leggi i dati della directory**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="d0b3a-155">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="d0b3a-156">Una volta che le impostazioni vengono salvate, scorre all'indietro toohello **chiavi** sezione e fare clic su hello **copia** chiave del pulsante toocopy hello client.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="d0b3a-157">Se si abbandona questa pagina a questo punto, non sarà in grado di tooaccess chiave mai più di questo client.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="d0b3a-158">Successivamente, è necessario tooconfigure app web con questa chiave.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="d0b3a-159">Accedi toohello [Esplora inventario risorse di Azure](https://resources.azure.com) con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="d0b3a-160">Nella parte superiore di hello della pagina hello, fare clic su **lettura/scrittura** modifiche toomake hello Esplora inventario risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="d0b3a-161">Trovare le impostazioni di autenticazione per l'app, si trova in sottoscrizioni di hello >  **&lt;* subscriptionname*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * > **provider** > **Microsoft**  >  **siti** > **&lt;*appname*> * * > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="d0b3a-162">Fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="d0b3a-163">Nel riquadro di modifica di hello, impostare hello `clientSecret` e `additionalLoginParams` proprietà come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="d0b3a-164">Fare clic su **inserire** in hello toosubmit superiore le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="d0b3a-165">A questo punto, tootest se si dispone dell'autorizzazione di hello token tooaccess hello API di Graph di Azure Active Directory, semplicemente passare a  **https://&lt;*appname*>.azurewebsites.net/.auth/me** nel Browser.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="d0b3a-166">Se è stato configurato tutto correttamente, si noterà hello `access_token` proprietà hello risposta JSON.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="d0b3a-167">Hello `~/.auth/me` percorso dell'URL è gestito dall'autenticazione del servizio App / toogive di autorizzazione per tutte le informazioni di hello correlati sessione tooyour autenticato.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="d0b3a-168">Per altre informazioni, vedere [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d0b3a-169">Hello `access_token` ha un periodo di scadenza.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="d0b3a-170">L'autenticazione/autorizzazione del servizio app offre tuttavia funzionalità di aggiornamento del token con `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="d0b3a-171">Per ulteriori informazioni su come toouse, vedere [archivio dei Token di servizio App](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="d0b3a-172">Ora si eseguirà un'operazione utile con i dati della directory.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="d0b3a-173">Aggiungere app tooyour funzionalità line-of-business</span><span class="sxs-lookup"><span data-stu-id="d0b3a-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="d0b3a-174">Verrà creato un semplice progetto di gestione degli elementi di lavoro CRUD.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="d0b3a-175">Nella cartella ~\Models hello, creare un file di classe denominato WorkItem.cs e sostituire `public class WorkItem {...}` con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="d0b3a-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="d0b3a-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="d0b3a-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="d0b3a-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="d0b3a-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="d0b3a-178">}</span><span class="sxs-lookup"><span data-stu-id="d0b3a-178">}</span></span>
   
     <span data-ttu-id="d0b3a-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="d0b3a-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="d0b3a-180">}</span><span class="sxs-lookup"><span data-stu-id="d0b3a-180">}</span></span>
2. <span data-ttu-id="d0b3a-181">Creare hello progetto toomake una nuova logica di scaffolding toohello accessibile di modello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="d0b3a-182">Aggiungere un nuovo elemento di scaffolding `WorkItemsController` toohello ~\Controllers cartella (fare doppio clic su **controller**, punto troppo**Aggiungi**e selezionare **nuovo elemento di scaffolding**).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="d0b3a-183">Selezionare **Controller MVC 5 con visualizzazioni, che usa Entity Framework** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="d0b3a-184">Modello selezionare hello creato, quindi fare clic su  **+**  e quindi **Aggiungi** tooadd un contesto dei dati, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="d0b3a-185">In ~\Views\WorkItems\Create.cshtml (un elemento di scaffolding automaticamente), trovare hello `Html.BeginForm` metodo di supporto e hello modifiche evidenziate di seguito:</span><span class="sxs-lookup"><span data-stu-id="d0b3a-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="d0b3a-186">Si noti che `token` e `tenant` vengono utilizzati da hello `AadPicker` toomake oggetto chiamate API di Graph di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="d0b3a-187">Si aggiungerà `AadPicker` in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="d0b3a-188">È anche possibile ottenere `token` e `tenant` dal lato client hello con `~/.auth/me`, ma che potrebbe essere una chiamata di server aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="d0b3a-189">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0b3a-189">For example:</span></span>
   > 
   > <span data-ttu-id="d0b3a-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="d0b3a-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="d0b3a-191">Modificare hello stesso con ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="d0b3a-192">Hello `AadPicker` oggetto è definito in uno script che è necessario tooadd tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="d0b3a-193">Fare clic sulla cartella ~\Scripts hello, scegliere troppo**Aggiungi**, fare clic su **file JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="d0b3a-194">Tipo `AadPickerLibrary` filename hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="d0b3a-195">Copiare il contenuto di hello da [qui](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) in ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="d0b3a-196">Nello script hello, hello `AadPicker` object chiama [API di Graph di Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch per utenti e gruppi corrispondenti hello input.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="d0b3a-197">~\Scripts\AadPickerLibrary.js utilizza inoltre hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="d0b3a-198">Pertanto, è necessario tooadd jQuery dell'interfaccia utente tooyour project.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="d0b3a-199">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="d0b3a-200">In Gestione pacchetti NuGet hello, fare clic su Sfoglia, tipo **jquery ui** in hello barra di ricerca, quindi fare clic su **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="d0b3a-201">Nel riquadro di destra hello, fare clic su **installare**, quindi fare clic su **OK** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="d0b3a-202">Aprire ~\App_Start\BundleConfig.cs e apportare hello modifiche evidenziate di seguito:</span><span class="sxs-lookup"><span data-stu-id="d0b3a-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="d0b3a-203">Sono presenti più efficiente modi toomanage JavaScript e il file CSS nell'app.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="d0b3a-204">Tuttavia, per motivi di semplicità si deve toopiggyback in bundle hello che vengono caricati con ogni visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="d0b3a-205">Infine, in ~ \Global.asax, aggiungere hello successiva riga di codice in hello `Application_Start()` metodo.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="d0b3a-206">`Ctrl`+`.`su ogni errore di risoluzione dei nomi troppo risolvere questo problema.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="d0b3a-207">È necessario questa riga di codice perché il modello MVC predefinito hello utilizza <code>[ValidateAntiForgeryToken]</code> effetti su alcune delle azioni hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="d0b3a-208">A causa di toohello comportamento descritto dalla [Brock Allen](https://twitter.com/BrockLAllen) in [MVC 4, AntiForgeryToken e attestazioni](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) POST HTTP potrebbe non riuscire convalida token antifalsificazione perché:</span><span class="sxs-lookup"><span data-stu-id="d0b3a-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="d0b3a-209">Azure Active Directory non invia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, è richiesto per impostazione predefinita dal token antifalsificazione hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="d0b3a-210">Se Azure Active Directory è una directory è stata sincronizzata con AD FS, trust hello ADFS per impostazione predefinita non inviare hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider attestazione, sebbene sia possibile configurare manualmente ADFS toosend questa attestazione.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="d0b3a-211">`ClaimTypes.NameIdentifies`Specifica l'attestazione hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, che fornisce funzionalità di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="d0b3a-212">A questo punto, pubblicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-212">Now, publish your changes.</span></span> <span data-ttu-id="d0b3a-213">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="d0b3a-214">Fare clic su **impostazioni**, assicurarsi che vi sia un tooyour di stringa di connessione del Database SQL, selezionare **aggiornamento Database** toomake hello modifiche dello schema per il modello e fare clic su **pubblica** .</span><span class="sxs-lookup"><span data-stu-id="d0b3a-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="d0b3a-215">In browser hello passare toohttps: / /&lt;*appname*>.azurewebsites.net/workitems e fare clic su **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="d0b3a-216">Fare clic nella hello **AssignedToName** casella.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="d0b3a-217">Gli utenti e i gruppi del tenant di Azure Active Directory verranno visualizzati in un elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="d0b3a-218">È possibile digitare toofilter o utilizzare hello `Up` o `Down` oppure fare clic tooselect hello utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="d0b3a-219">Fare clic su **crea** modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="d0b3a-220">Quindi, fare clic su **modifica** lavoro hello creato elemento tooobserve hello stesso comportamento.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="d0b3a-221">A questo punto è in esecuzione un'app line-of-business in Azure con accesso alla directory.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="d0b3a-222">È molto più che è possibile eseguire con hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="d0b3a-223">Vedere [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)(Informazioni di riferimento sull'API Graph di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="d0b3a-224">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="d0b3a-224">Next Step</span></span>
<span data-ttu-id="d0b3a-225">Se è necessario il controllo di accesso basato sui ruoli (RBAC) per l'app line-of-business in azure, vedere [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) per un esempio del team di Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="d0b3a-226">Viene illustrato come tooenable ruoli per l'applicazione in Azure Active Directory e quindi autorizzare gli utenti con hello `[Authorize]` effetto.</span><span class="sxs-lookup"><span data-stu-id="d0b3a-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="d0b3a-227">Se l'app line-of-business deve accedere a dati locali tooon, vedere [accesso risorse locali mediante connessioni ibride in Azure App Service](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0b3a-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="d0b3a-228">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="d0b3a-228">Further resources</span></span>
* [<span data-ttu-id="d0b3a-229">Autenticazione e autorizzazione nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="d0b3a-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="d0b3a-230">Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure</span><span class="sxs-lookup"><span data-stu-id="d0b3a-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="d0b3a-231">Creare un'app line-of-business in Azure con l'autenticazione di AD FS</span><span class="sxs-lookup"><span data-stu-id="d0b3a-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="d0b3a-232">Autenticazione del servizio App e hello API Azure AD Graph</span><span class="sxs-lookup"><span data-stu-id="d0b3a-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="d0b3a-233">Esempi e documentazione su Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0b3a-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="d0b3a-234">Token e tipi di attestazioni supportati di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0b3a-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)

---
title: Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory | Documentazione Microsoft
description: Informazioni su come creare un'applicazione line-of-business ASP.NET MVC nel servizio app di Azure che esegue l'autenticazione con Azure Active Directory
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
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="a8e79-103">Creare un'app line-of-business in Azure con l'autenticazione di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8e79-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="a8e79-104">Questo articolo illustra come creare un'app line-of-business .NET nelle [app Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando la funzionalità [Autenticazione/Autorizzazione](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8e79-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="a8e79-105">Spiega inoltre come usare l' [API Graph di Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) per eseguire query sui dati della directory nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8e79-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="a8e79-106">Il tenant di Azure Active Directory usato può essere una directory solo di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e79-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="a8e79-107">In alternativa, può essere [sincronizzato con l'istanza di Active Directory locale](../active-directory/active-directory-aadconnect.md) per creare un'unica esperienza Single Sign-On per gli utenti locali e remoti.</span><span class="sxs-lookup"><span data-stu-id="a8e79-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="a8e79-108">In questo articolo si usa la directory predefinita per l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e79-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="a8e79-109">Obiettivo di compilazione</span><span class="sxs-lookup"><span data-stu-id="a8e79-109">What you will build</span></span>
<span data-ttu-id="a8e79-110">Verrà compilata una semplice applicazione CRUD (Create-Read-Update-Delete) line-of-business nelle app Web di Servizio app di Azure per tenere traccia degli elementi di lavoro con le seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="a8e79-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="a8e79-111">Autenticazione degli utenti con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8e79-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="a8e79-112">Esecuzione di query su utenti e gruppi della directory tramite l' [API Graph di Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8e79-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="a8e79-113">Usare il modello MVC ASP.NET *Nessuna autenticazione*</span><span class="sxs-lookup"><span data-stu-id="a8e79-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="a8e79-114">Se è necessario il Controllo degli accessi in base al ruolo per l'applicazione line-of-business in Azure, vedere il [passaggio successivo](#next).</span><span class="sxs-lookup"><span data-stu-id="a8e79-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="a8e79-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="a8e79-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="a8e79-116">Per completare questa esercitazione sarà necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a8e79-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="a8e79-117">Un tenant di Azure Active Directory con utenti in diversi gruppi</span><span class="sxs-lookup"><span data-stu-id="a8e79-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="a8e79-118">Autorizzazioni per la creazione di applicazioni nel tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8e79-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="a8e79-119">Visual Studio 2013 Update 4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a8e79-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="a8e79-120">Azure SDK 2.8.1 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a8e79-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="a8e79-121">Creare e distribuire un'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="a8e79-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="a8e79-122">In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="a8e79-123">Selezionare **Applicazione Web ASP.NET**, assegnare un nome al progetto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="a8e79-124">Selezionare il modello **MVC**, quindi modificare l'autenticazione in **Nessuna autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="a8e79-125">Assicurarsi che **Host nel cloud** sia selezionata e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="a8e79-126">Nella finestra di dialogo **Crea servizio App** fare clic su **Aggiungi un account** e quindi su **Aggiungi un account** nell'elenco a discesa per accedere al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e79-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="a8e79-127">Dopo aver eseguito l'accesso, configurare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="a8e79-127">Once logged in configure your web app.</span></span> <span data-ttu-id="a8e79-128">Creare un gruppo di risorse e un nuovo piano di servizio app facendo clic sul pulsante **Nuovo** corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a8e79-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="a8e79-129">Fare clic su **Esplorare servizi di Azure aggiuntivi** per continuare.</span><span class="sxs-lookup"><span data-stu-id="a8e79-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="a8e79-130">Nella scheda **Servizi** fare clic su **+** per aggiungere un database SQL per l'app.</span><span class="sxs-lookup"><span data-stu-id="a8e79-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="a8e79-131">In **Configura database SQL** fare clic su **Nuovo** per creare un'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8e79-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="a8e79-132">In **Configura SQL Server**configurare l'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8e79-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="a8e79-133">Fare clic su **OK**, **OK** e su **Crea** per avviare la creazione dell'app in Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e79-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="a8e79-134">In **Attività del servizio app di Azure**è possibile vedere quando termina la creazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a8e79-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="a8e79-135">Fare clic su **Pubblica &lt;*nomeapp*> in questa app Web adesso**, quindi fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="a8e79-136">Al termine del processo di Visual Studio, nel browser verrà aperta l'app pubblicata.</span><span class="sxs-lookup"><span data-stu-id="a8e79-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="a8e79-137">Configurare l'autenticazione e l'accesso alla directory</span><span class="sxs-lookup"><span data-stu-id="a8e79-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="a8e79-138">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a8e79-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a8e79-139">Nel menu a sinistra fare clic su **Servizi app** > **&lt;*nomeapp*>** > **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="a8e79-140">Attivare l'autenticazione di Azure Active Directory facendo clic su **Attivato** > **Azure Active Directory** > **Rapida** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="a8e79-141">Fare clic su **Salva** nella barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a8e79-141">Click **Save** in the command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="a8e79-142">Dopo aver salvato le impostazioni di autenticazione, provare a passare di nuovo all'app nel browser.</span><span class="sxs-lookup"><span data-stu-id="a8e79-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="a8e79-143">Le impostazioni predefinite applicano l'autenticazione all'intera app.</span><span class="sxs-lookup"><span data-stu-id="a8e79-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="a8e79-144">Se non si è già connessi, si viene reindirizzati a una schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="a8e79-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="a8e79-145">Dopo aver effettuato l'accesso, verrà visualizzata l'app protetta tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a8e79-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="a8e79-146">Quindi, è necessario abilitare l'accesso ai dati della directory.</span><span class="sxs-lookup"><span data-stu-id="a8e79-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="a8e79-147">Passare al [portale classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a8e79-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="a8e79-148">Nel menu a sinistra fare clic su **Active Directory** > **Directory predefinita** > **Applicazioni** > **&lt;*nomeapp*>**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="a8e79-149">Questa è l'applicazione Azure Active Directory creata automaticamente dal servizio app per abilitare la Autorizzazione/Autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a8e79-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="a8e79-150">Fare clic su **Utenti** e **Gruppi** per assicurarsi di avere alcuni utenti e gruppi nella directory.</span><span class="sxs-lookup"><span data-stu-id="a8e79-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="a8e79-151">In caso contrario, creare alcuni utenti e gruppi di test.</span><span class="sxs-lookup"><span data-stu-id="a8e79-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="a8e79-152">Fare clic su **Configura** per configurare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8e79-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="a8e79-153">Scorrere verso il basso fino alla sezione **Chiavi** e aggiungere una chiave selezionando una durata.</span><span class="sxs-lookup"><span data-stu-id="a8e79-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="a8e79-154">Fare quindi clic su **Autorizzazioni delegate** e selezionare **Leggi i dati della directory**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="a8e79-155">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="a8e79-156">Dopo aver salvato le impostazioni, scorrere tornando alla sezione **Chiavi** e fare clic su **Copia** per copiare la chiave client.</span><span class="sxs-lookup"><span data-stu-id="a8e79-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="a8e79-157">Se si esce dalla pagina ora, non sarà mai più possibile accedere a questa chiave client.</span><span class="sxs-lookup"><span data-stu-id="a8e79-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="a8e79-158">Configurare quindi l'app Web con questa chiave.</span><span class="sxs-lookup"><span data-stu-id="a8e79-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="a8e79-159">Accedere a [Esplora risorse di Azure](https://resources.azure.com) con il proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e79-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="a8e79-160">Nella parte superiore della pagina fare clic su **Lettura/Scrittura** per apportare modifiche in Esplora risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e79-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="a8e79-161">Trovare le impostazioni di autenticazione per l'app disponibili in sottoscrizioni > **&lt;*nomesottoscrizione*>** > **gruppidirisorse** > **&lt;*nomegruppodirisorse*>** > **provider** > **Microsoft.Web** > **siti** > **&lt;*nomeapp*>** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="a8e79-162">Fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="a8e79-163">Nel riquadro di modifica impostare le proprietà `clientSecret` e `additionalLoginParams` come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a8e79-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="a8e79-164">Fare clic su **Put** nella parte superiore per inviare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a8e79-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="a8e79-165">A questo punto, per verificare se è disponibile il token di autorizzazione per accedere all'API Graph di Azure Active Directory, passare a **https://&lt;*nomeapp*>.azurewebsites.net/.auth/me** nel browser.</span><span class="sxs-lookup"><span data-stu-id="a8e79-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="a8e79-166">Se è stato configurato tutto correttamente, nella risposta JSON verrà visualizzata la proprietà `access_token` .</span><span class="sxs-lookup"><span data-stu-id="a8e79-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="a8e79-167">Il percorso URL `~/.auth/me` è gestito dall'autenticazione/autorizzazione del servizio app per fornire all'utente tutte le informazioni relative alla sessione autenticata.</span><span class="sxs-lookup"><span data-stu-id="a8e79-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="a8e79-168">Per altre informazioni, vedere [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8e79-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a8e79-169">Il percorso URL `access_token` ha un periodo di scadenza.</span><span class="sxs-lookup"><span data-stu-id="a8e79-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="a8e79-170">L'autenticazione/autorizzazione del servizio app offre tuttavia funzionalità di aggiornamento del token con `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="a8e79-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="a8e79-171">Per altre informazioni sull'uso, vedere [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/)(Archivio Token del servizio app).</span><span class="sxs-lookup"><span data-stu-id="a8e79-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="a8e79-172">Ora si eseguirà un'operazione utile con i dati della directory.</span><span class="sxs-lookup"><span data-stu-id="a8e79-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="a8e79-173">Aggiungere funzionalità line-of-business all'app</span><span class="sxs-lookup"><span data-stu-id="a8e79-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="a8e79-174">Verrà creato un semplice progetto di gestione degli elementi di lavoro CRUD.</span><span class="sxs-lookup"><span data-stu-id="a8e79-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="a8e79-175">Nella cartella ~\Models creare un file di classe denominato WorkItem.cs e sostituire `public class WorkItem {...}` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a8e79-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="a8e79-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="a8e79-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="a8e79-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="a8e79-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="a8e79-178">}</span><span class="sxs-lookup"><span data-stu-id="a8e79-178">}</span></span>
   
     <span data-ttu-id="a8e79-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="a8e79-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="a8e79-180">}</span><span class="sxs-lookup"><span data-stu-id="a8e79-180">}</span></span>
2. <span data-ttu-id="a8e79-181">Compilare il progetto per rendere accessibile il nuovo modello alla logica di scaffolding in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8e79-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="a8e79-182">Aggiungere un nuovo elemento di scaffolding `WorkItemsController` nella cartella ~\Controllers. Fare clic con il pulsante destro del mouse su **Controller**, scegliere **Aggiungi** e selezionare **Nuovo elemento di scaffolding**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="a8e79-183">Selezionare **Controller MVC 5 con visualizzazioni, che usa Entity Framework** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="a8e79-184">Selezionare il modello creato, fare clic su **+**, quindi su **Aggiungi** per aggiungere un contesto dei dati e infine fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="a8e79-185">In ~\Views\WorkItems\Create.cshtml (un elemento sottoposto automaticamente a scaffolding) individuare il metodo helper `Html.BeginForm` e apportare le modifiche evidenziate di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8e79-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
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
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
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
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="a8e79-186">Si noti che `token` e `tenant` vengono usati dall'oggetto `AadPicker` per eseguire chiamate all'API Graph di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8e79-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="a8e79-187">Si aggiungerà `AadPicker` in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a8e79-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="a8e79-188">È anche possibile ottenere `token` e `tenant` dal lato client con `~/.auth/me`, ma si tratterebbe di una chiamata server aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="a8e79-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="a8e79-189">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a8e79-189">For example:</span></span>
   > 
   > <span data-ttu-id="a8e79-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="a8e79-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="a8e79-191">Apportare le stesse modifiche con ~\Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="a8e79-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="a8e79-192">L'oggetto `AadPicker` è definito in uno script che è necessario aggiungere al progetto.</span><span class="sxs-lookup"><span data-stu-id="a8e79-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="a8e79-193">Fare clic con il pulsante destro del mouse sulla cartella ~\Scripts, scegliere **Aggiungi** e fare clic sul **file JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="a8e79-194">Digitare `AadPickerLibrary` come nome file e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="a8e79-195">Copiare il contenuto da [qui](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) in ~\Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="a8e79-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="a8e79-196">Nello script l'oggetto `AadPicker` chiama l' [API Graph di Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) per cercare gli utenti e i gruppi corrispondenti all'input.</span><span class="sxs-lookup"><span data-stu-id="a8e79-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="a8e79-197">Anche ~\Scripts\AadPickerLibrary.js usa il [widget di completamento automatico dell'interfaccia utente jQuery](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="a8e79-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="a8e79-198">È quindi necessario aggiungere l'interfaccia utente di jQuery al progetto.</span><span class="sxs-lookup"><span data-stu-id="a8e79-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="a8e79-199">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="a8e79-200">In Gestione pacchetti NuGet fare clic su Sfoglia, digitare **jquery-ui** nella barra di ricerca e fare clic su **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="a8e79-201">Nel riquadro di destra fare clic su **Installa**, quindi fare clic su **OK** per continuare.</span><span class="sxs-lookup"><span data-stu-id="a8e79-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="a8e79-202">Aprire ~\App_Start\BundleConfig.cs e apportare le modifiche evidenziate di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8e79-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
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
    
    <span data-ttu-id="a8e79-203">Sono disponibili altri modi più efficienti per gestire i file CSS e JavaScript nell'app.</span><span class="sxs-lookup"><span data-stu-id="a8e79-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="a8e79-204">Tuttavia, per semplicità, sarà sufficiente occuparsi dei bundle caricati con ogni visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="a8e79-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="a8e79-205">In ~\Global.asax aggiungere infine la riga di codice seguente al metodo `Application_Start()`.</span><span class="sxs-lookup"><span data-stu-id="a8e79-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="a8e79-206">`Ctrl`+`.` su ogni errore di risoluzione dei nomi per correggerlo.</span><span class="sxs-lookup"><span data-stu-id="a8e79-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="a8e79-207">Questa riga di codice è necessaria perché il modello MVC predefinito usa <code>[ValidateAntiForgeryToken]</code> in alcune azioni.</span><span class="sxs-lookup"><span data-stu-id="a8e79-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="a8e79-208">A causa del comportamento descritto da [Brock Allen](https://twitter.com/BrockLAllen) nella pagina [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) (MVC 4, AntiForgeryToken e attestazioni), è possibile che la convalida del token antifalsificazione con HTTP POST non riesca per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8e79-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="a8e79-209">Azure Active Directory non invia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, richiesto per impostazione predefinita dal token antifalsificazione.</span><span class="sxs-lookup"><span data-stu-id="a8e79-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="a8e79-210">Se Azure Active Directory prevede la sincronizzazione della directory con AD FS, l'attendibilità AD FS non invia per impostazione predefinita l'attestazione http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, anche se è possibile configurare manualmente AD FS per l'invio di questa attestazione.</span><span class="sxs-lookup"><span data-stu-id="a8e79-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="a8e79-211">`ClaimTypes.NameIdentifies` specifica l'attestazione `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, che non viene fornita da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8e79-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="a8e79-212">A questo punto, pubblicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a8e79-212">Now, publish your changes.</span></span> <span data-ttu-id="a8e79-213">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="a8e79-214">Fare clic su **Impostazioni**, assicurarsi che sia disponibile una stringa di connessione al database SQL, selezionare **Aggiorna database** per apportare le modifiche allo schema per il modello e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="a8e79-215">Nel browser passare a https://&lt;*nomeapp*>.azurewebsites.net/workitems e fare clic su **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="a8e79-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="a8e79-216">Fare clic sulla casella **AssignedToName** .</span><span class="sxs-lookup"><span data-stu-id="a8e79-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="a8e79-217">Gli utenti e i gruppi del tenant di Azure Active Directory verranno visualizzati in un elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="a8e79-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="a8e79-218">È possibile digitare per filtrare o usare la chiave `Up` o `Down` oppure fare clic per selezionare l'utente o il gruppo.</span><span class="sxs-lookup"><span data-stu-id="a8e79-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="a8e79-219">Fare clic su **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a8e79-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="a8e79-220">Quindi, fare clic su **Modifica** nell'elemento di lavoro creato per osservare lo stesso comportamento.</span><span class="sxs-lookup"><span data-stu-id="a8e79-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="a8e79-221">A questo punto è in esecuzione un'app line-of-business in Azure con accesso alla directory.</span><span class="sxs-lookup"><span data-stu-id="a8e79-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="a8e79-222">Con l'API Graph è possibile fare molto di più.</span><span class="sxs-lookup"><span data-stu-id="a8e79-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="a8e79-223">Vedere [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)(Informazioni di riferimento sull'API Graph di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8e79-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="a8e79-224">passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="a8e79-224">Next Step</span></span>
<span data-ttu-id="a8e79-225">Se è necessario il controllo degli accessi in base al ruolo per l'app line-of-business in Azure, vedere [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) per un esempio del team di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8e79-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="a8e79-226">Viene illustrato come abilitare i ruoli per un'applicazione Azure Active Directory e quindi autorizzare gli utenti con `[Authorize]` .</span><span class="sxs-lookup"><span data-stu-id="a8e79-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="a8e79-227">Se l'app line-of-business deve accedere a dati locali, vedere [Accedere alle risorse locali usando connessioni ibride nel servizio app di Azure](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a8e79-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="a8e79-228">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="a8e79-228">Further resources</span></span>
* [<span data-ttu-id="a8e79-229">Autenticazione e autorizzazione nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a8e79-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="a8e79-230">Eseguire l'autenticazione con l'istanza locale di Active Directory nell'app Azure</span><span class="sxs-lookup"><span data-stu-id="a8e79-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="a8e79-231">Creare un'app line-of-business in Azure con l'autenticazione di AD FS</span><span class="sxs-lookup"><span data-stu-id="a8e79-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="a8e79-232">App Service Auth and the Azure AD Graph API (Autenticazione del servizio app e API Graph di Azure AD)</span><span class="sxs-lookup"><span data-stu-id="a8e79-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="a8e79-233">Esempi e documentazione su Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8e79-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="a8e79-234">Token e tipi di attestazioni supportati di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8e79-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)

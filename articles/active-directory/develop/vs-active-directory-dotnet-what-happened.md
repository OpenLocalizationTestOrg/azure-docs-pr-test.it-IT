---
title: Modifiche apportate a un progetto MVC quando ci si connette ad Azure AD | Microsoft Docs
description: Viene descritto cosa succede al progetto MVC quando ci si connette ad Azure AD mediante i servizi relazionati di Visual Studio.
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="4ec17-103">Cosa è successo a un progetto MVC (servizio connesso a Visual Studio Azure Active Directory)?</span><span class="sxs-lookup"><span data-stu-id="4ec17-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ec17-104">Per iniziare</span><span class="sxs-lookup"><span data-stu-id="4ec17-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="4ec17-105">Risultati</span><span class="sxs-lookup"><span data-stu-id="4ec17-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="4ec17-106">Sono stati aggiunti riferimenti</span><span class="sxs-lookup"><span data-stu-id="4ec17-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="4ec17-107">Riferimenti al pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="4ec17-107">NuGet package references</span></span>
* <span data-ttu-id="4ec17-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="4ec17-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="4ec17-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="4ec17-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="4ec17-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="4ec17-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="4ec17-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="4ec17-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="4ec17-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="4ec17-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="4ec17-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="4ec17-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="4ec17-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="4ec17-114">**Owin**</span></span>
* <span data-ttu-id="4ec17-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="4ec17-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="4ec17-116">Riferimenti a .NET</span><span class="sxs-lookup"><span data-stu-id="4ec17-116">.NET references</span></span>
* <span data-ttu-id="4ec17-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="4ec17-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="4ec17-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="4ec17-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="4ec17-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="4ec17-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="4ec17-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="4ec17-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="4ec17-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="4ec17-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="4ec17-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="4ec17-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="4ec17-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="4ec17-123">**Owin**</span></span>
* <span data-ttu-id="4ec17-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="4ec17-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="4ec17-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="4ec17-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="4ec17-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="4ec17-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="4ec17-127">È stato aggiunto codice</span><span class="sxs-lookup"><span data-stu-id="4ec17-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="4ec17-128">Sono stati aggiunti file di codice al progetto</span><span class="sxs-lookup"><span data-stu-id="4ec17-128">Code files were added to your project</span></span>
<span data-ttu-id="4ec17-129">Al progetto è stata aggiunta una classe di avvio di autenticazione **App_Start/Startup.Auth.cs** contenente la logica di avvio per l'autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ec17-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="4ec17-130">È stata anche aggiunta una classe controller, Controllers/AccountController.cs che include i metodi **SignIn()** e **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="4ec17-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="4ec17-131">È stata infine aggiunta una visualizzazione parziale, **Views/Shared/_LoginPartial.cshtml** che include un collegamento azione per SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="4ec17-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="4ec17-132">È stato aggiunto un codice di avvio al progetto</span><span class="sxs-lookup"><span data-stu-id="4ec17-132">Startup code was added to your project</span></span>
<span data-ttu-id="4ec17-133">Se nel progetto è già presente una classe Startup, il metodo **Configuration** è stato aggiornato includendo una chiamata a **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="4ec17-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="4ec17-134">In caso contrario, una classe Startup è stata aggiunta al progetto.</span><span class="sxs-lookup"><span data-stu-id="4ec17-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="4ec17-135">Il file app.config o web.config include nuovi valori di configurazione</span><span class="sxs-lookup"><span data-stu-id="4ec17-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="4ec17-136">Sono state aggiunte le voci di configurazione seguenti.</span><span class="sxs-lookup"><span data-stu-id="4ec17-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="4ec17-137">È stata creata un'app Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="4ec17-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="4ec17-138">Un'app Azure AD è stata creata nella directory selezionata nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="4ec17-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="4ec17-139">Se è stata selezionata l'opzione *Disabilitare l'autenticazione dell'account utente*, quali altre modifiche sono state apportate al progetto?</span><span class="sxs-lookup"><span data-stu-id="4ec17-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="4ec17-140">Sono stati rimossi i riferimenti del pacchetto NuGet, i file sono stati rimossi e viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="4ec17-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="4ec17-141">A seconda dello stato del progetto, è necessario rimuovere riferimenti aggiuntivi o i file manualmente o modificare codice in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="4ec17-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="4ec17-142">Riferimenti del pacchetto NuGet rimossi (per coloro che sono presenti)</span><span class="sxs-lookup"><span data-stu-id="4ec17-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="4ec17-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="4ec17-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="4ec17-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="4ec17-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="4ec17-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="4ec17-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="4ec17-146">È stato eseguito il backup dei file di codice e sono stati rimossi (per quelli presenti)</span><span class="sxs-lookup"><span data-stu-id="4ec17-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="4ec17-147">Per ognuno dei seguenti file è stato eseguito il backup e rimosso dal progetto.</span><span class="sxs-lookup"><span data-stu-id="4ec17-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="4ec17-148">I File di backup si trovano in una cartella 'Backup' alla radice della directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="4ec17-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="4ec17-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="4ec17-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="4ec17-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="4ec17-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="4ec17-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="4ec17-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="4ec17-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="4ec17-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="4ec17-153">Backup dei file di codice (per coloro che presenti)</span><span class="sxs-lookup"><span data-stu-id="4ec17-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="4ec17-154">Per ognuno dei seguenti file è stato eseguito il backup prima della sostituzione.</span><span class="sxs-lookup"><span data-stu-id="4ec17-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="4ec17-155">I File di backup si trovano in una cartella 'Backup' alla radice della directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="4ec17-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="4ec17-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="4ec17-156">**Startup.cs**</span></span>
* <span data-ttu-id="4ec17-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="4ec17-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="4ec17-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="4ec17-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="4ec17-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="4ec17-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="4ec17-160">Quali modifiche aggiuntive sono state apportate al progetto dopo aver selezionato *Leggi i dati della directory*?</span><span class="sxs-lookup"><span data-stu-id="4ec17-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="4ec17-161">Sono stati aggiunti riferimenti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="4ec17-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="4ec17-162">Riferimenti al pacchetto NuGet aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="4ec17-162">Additional NuGet package references</span></span>
* <span data-ttu-id="4ec17-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="4ec17-163">**EntityFramework**</span></span>
* <span data-ttu-id="4ec17-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="4ec17-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="4ec17-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="4ec17-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="4ec17-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="4ec17-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="4ec17-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="4ec17-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="4ec17-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="4ec17-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="4ec17-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="4ec17-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="4ec17-170">Riferimenti .NET aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="4ec17-170">Additional .NET references</span></span>
* <span data-ttu-id="4ec17-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="4ec17-171">**EntityFramework**</span></span>
* <span data-ttu-id="4ec17-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="4ec17-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="4ec17-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="4ec17-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="4ec17-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="4ec17-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="4ec17-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="4ec17-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="4ec17-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="4ec17-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="4ec17-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="4ec17-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="4ec17-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="4ec17-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="4ec17-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="4ec17-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="4ec17-180">Sono stati aggiunti altri file di codice al progetto</span><span class="sxs-lookup"><span data-stu-id="4ec17-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="4ec17-181">Per supportare la memorizzazione nella cache token sono stati aggiunti due file: **Models\ADALTokenCache.cs** e **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="4ec17-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="4ec17-182">Sono stati aggiunti un controller e una visualizzazione per illustrare l'accesso alle informazioni relative al profilo utente tramite le API Graph di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec17-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="4ec17-183">Questi file sono **Controllers\UserProfileController.cs** e **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="4ec17-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="4ec17-184">È stato aggiunto un altro codice di avvio al progetto</span><span class="sxs-lookup"><span data-stu-id="4ec17-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="4ec17-185">Nel file **startup.auth.cs** è stato aggiunto un nuovo oggetto **OpenIdConnectAuthenticationNotifications** al membro **Notifiche** di **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="4ec17-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="4ec17-186">Serve ad abilitare la ricezione del codice OAuth e scambiarlo con un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="4ec17-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="4ec17-187">Sono state apportate altre modifiche al file app.config o web.config</span><span class="sxs-lookup"><span data-stu-id="4ec17-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="4ec17-188">Sono state aggiunte le voci di configurazione aggiuntive seguenti.</span><span class="sxs-lookup"><span data-stu-id="4ec17-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="4ec17-189">Sono state aggiunte le sezioni di configurazione e la stringa di connessione seguenti.</span><span class="sxs-lookup"><span data-stu-id="4ec17-189">The following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="4ec17-190">È stata aggiornata l'app Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ec17-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="4ec17-191">L'app Azure Active Directory è stata aggiornata per includere l'autorizzazione *Leggi i dati della directory* ed è stata creata una chiave aggiuntiva che è stata quindi usata come *ida:ClientSecret* nel file **web.config**.</span><span class="sxs-lookup"><span data-stu-id="4ec17-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ec17-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ec17-192">Next steps</span></span>
- [<span data-ttu-id="4ec17-193">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ec17-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)


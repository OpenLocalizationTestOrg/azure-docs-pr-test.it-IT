---
title: tooa aaaChanges apportate MVC progetto quando ci si connette AD tooAzure | Documenti Microsoft
description: Viene descritto cosa succede progetto MVC tooyour quando ci si connette AD tooAzure mediante i servizi di Visual Studio connesso
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
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="b1a20-103">Selezionare il progetto MVC verificato anomalo toomy (servizio connesso di Visual Studio Azure Active Directory)?</span><span class="sxs-lookup"><span data-stu-id="b1a20-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1a20-104">Per iniziare</span><span class="sxs-lookup"><span data-stu-id="b1a20-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="b1a20-105">Risultati</span><span class="sxs-lookup"><span data-stu-id="b1a20-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="b1a20-106">Sono stati aggiunti riferimenti</span><span class="sxs-lookup"><span data-stu-id="b1a20-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="b1a20-107">Riferimenti al pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="b1a20-107">NuGet package references</span></span>
* <span data-ttu-id="b1a20-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="b1a20-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="b1a20-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="b1a20-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="b1a20-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="b1a20-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="b1a20-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="b1a20-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="b1a20-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="b1a20-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="b1a20-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="b1a20-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="b1a20-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="b1a20-114">**Owin**</span></span>
* <span data-ttu-id="b1a20-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="b1a20-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="b1a20-116">Riferimenti a .NET</span><span class="sxs-lookup"><span data-stu-id="b1a20-116">.NET references</span></span>
* <span data-ttu-id="b1a20-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="b1a20-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="b1a20-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="b1a20-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="b1a20-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="b1a20-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="b1a20-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="b1a20-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="b1a20-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="b1a20-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="b1a20-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="b1a20-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="b1a20-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="b1a20-123">**Owin**</span></span>
* <span data-ttu-id="b1a20-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="b1a20-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="b1a20-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="b1a20-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="b1a20-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="b1a20-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="b1a20-127">È stato aggiunto codice</span><span class="sxs-lookup"><span data-stu-id="b1a20-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="b1a20-128">File di codice sono stati aggiunti tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="b1a20-128">Code files were added tooyour project</span></span>
<span data-ttu-id="b1a20-129">Una classe di avvio, l'autenticazione **App_Start/Startup.Auth.cs** tooyour progetto che contiene la logica di avvio per l'autenticazione di Azure AD è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="b1a20-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="b1a20-130">È stata anche aggiunta una classe controller, Controllers/AccountController.cs che include i metodi **SignIn()** e **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="b1a20-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="b1a20-131">È stata infine aggiunta una visualizzazione parziale, **Views/Shared/_LoginPartial.cshtml** che include un collegamento azione per SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="b1a20-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="b1a20-132">Codice di avvio è stato aggiunto il progetto tooyour</span><span class="sxs-lookup"><span data-stu-id="b1a20-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="b1a20-133">Se si dispone già di una classe di avvio del progetto, hello **configurazione** tooinclude aggiornata una chiamata di metodo troppo**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="b1a20-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="b1a20-134">In caso contrario, una classe di avvio è stato aggiunto il progetto tooyour.</span><span class="sxs-lookup"><span data-stu-id="b1a20-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="b1a20-135">Il file app.config o web.config include nuovi valori di configurazione</span><span class="sxs-lookup"><span data-stu-id="b1a20-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="b1a20-136">Hello seguenti voci di configurazione è state aggiunte.</span><span class="sxs-lookup"><span data-stu-id="b1a20-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="b1a20-137">È stata creata un'app Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="b1a20-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="b1a20-138">Un'applicazione Azure AD è stata creata nella directory hello selezionate nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="b1a20-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="b1a20-139">Se è stata selezionata *disabilitare l'autenticazione di account utente*, le altre modifiche apportate toomy progetto?</span><span class="sxs-lookup"><span data-stu-id="b1a20-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="b1a20-140">Sono stati rimossi i riferimenti del pacchetto NuGet, i file sono stati rimossi e viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="b1a20-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="b1a20-141">A seconda dello stato hello del progetto, è possibile toomanually rimuovere file o i riferimenti aggiuntivi o modificare codice nel modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="b1a20-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="b1a20-142">Riferimenti del pacchetto NuGet rimossi (per coloro che sono presenti)</span><span class="sxs-lookup"><span data-stu-id="b1a20-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="b1a20-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="b1a20-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="b1a20-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="b1a20-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="b1a20-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="b1a20-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="b1a20-146">È stato eseguito il backup dei file di codice e sono stati rimossi (per quelli presenti)</span><span class="sxs-lookup"><span data-stu-id="b1a20-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="b1a20-147">Ogni file seguente è stato eseguito il backup e rimosso dal progetto hello.</span><span class="sxs-lookup"><span data-stu-id="b1a20-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="b1a20-148">I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="b1a20-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="b1a20-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="b1a20-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="b1a20-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="b1a20-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="b1a20-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="b1a20-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="b1a20-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="b1a20-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="b1a20-153">Backup dei file di codice (per coloro che presenti)</span><span class="sxs-lookup"><span data-stu-id="b1a20-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="b1a20-154">Per ognuno dei seguenti file è stato eseguito il backup prima della sostituzione.</span><span class="sxs-lookup"><span data-stu-id="b1a20-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="b1a20-155">I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="b1a20-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="b1a20-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="b1a20-156">**Startup.cs**</span></span>
* <span data-ttu-id="b1a20-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="b1a20-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="b1a20-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="b1a20-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="b1a20-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="b1a20-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="b1a20-160">Se è stata selezionata *lettura dati directory*, le altre modifiche apportate toomy progetto?</span><span class="sxs-lookup"><span data-stu-id="b1a20-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="b1a20-161">Sono stati aggiunti riferimenti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="b1a20-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="b1a20-162">Riferimenti al pacchetto NuGet aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="b1a20-162">Additional NuGet package references</span></span>
* <span data-ttu-id="b1a20-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="b1a20-163">**EntityFramework**</span></span>
* <span data-ttu-id="b1a20-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="b1a20-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="b1a20-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="b1a20-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="b1a20-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="b1a20-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="b1a20-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="b1a20-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="b1a20-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="b1a20-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="b1a20-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="b1a20-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="b1a20-170">Riferimenti .NET aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="b1a20-170">Additional .NET references</span></span>
* <span data-ttu-id="b1a20-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="b1a20-171">**EntityFramework**</span></span>
* <span data-ttu-id="b1a20-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="b1a20-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="b1a20-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="b1a20-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="b1a20-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="b1a20-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="b1a20-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="b1a20-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="b1a20-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="b1a20-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="b1a20-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="b1a20-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="b1a20-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="b1a20-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="b1a20-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="b1a20-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="b1a20-180">File di codice aggiuntivi sono stati aggiunti tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="b1a20-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="b1a20-181">Due file sono stati aggiunti toosupport la memorizzazione nella cache token: **Models\ADALTokenCache.cs** e **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="b1a20-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="b1a20-182">Un ulteriore controller e Visualizza sono stati aggiunti tooillustrate l'accesso a informazioni sul profilo utente utilizzando le API di graph di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a20-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="b1a20-183">Questi file sono **Controllers\UserProfileController.cs** e **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="b1a20-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="b1a20-184">Tooyour progetto è stato aggiunto altro codice di avvio</span><span class="sxs-lookup"><span data-stu-id="b1a20-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="b1a20-185">In hello **startup.auth.cs** file, un nuovo **OpenIdConnectAuthenticationNotifications** toohello è stato aggiunto l'oggetto **notifiche** membro di hello  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="b1a20-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="b1a20-186">Si tratta di tooenable hello OAuth codice e ottenerne la un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="b1a20-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="b1a20-187">Sono state apportate modifiche aggiuntive tooyour file app. config o Web. config</span><span class="sxs-lookup"><span data-stu-id="b1a20-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="b1a20-188">Hello voci di configurazione aggiuntive seguenti sono state aggiunte.</span><span class="sxs-lookup"><span data-stu-id="b1a20-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="b1a20-189">Hello seguenti sezioni di configurazione e di stringa di connessione sono state aggiunte.</span><span class="sxs-lookup"><span data-stu-id="b1a20-189">hello following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="b1a20-190">È stata aggiornata l'app Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1a20-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="b1a20-191">L'App di Azure Active Directory è stato aggiornato tooinclude hello *lettura dati directory* autorizzazione e un'altra chiave è stato creato che è stato utilizzato come hello *ida: ClientSecret* in hello  **Web. config** file.</span><span class="sxs-lookup"><span data-stu-id="b1a20-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1a20-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1a20-192">Next steps</span></span>
- [<span data-ttu-id="b1a20-193">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1a20-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)


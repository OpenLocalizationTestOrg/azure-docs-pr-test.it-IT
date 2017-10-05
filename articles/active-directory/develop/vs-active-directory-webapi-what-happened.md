---
title: Modifiche apportate a un progetto WebApi quando ci si connette ad Azure AD | Documentazione Microsoft
description: L'articolo descrive l'impatto della connessione ad Azure AD con Visual Studio su un progetto Web Api
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 086e5a9622cad681cd282345d97e0c28ee7de2fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="3e856-103">Cosa è successo a un progetto WebApi (servizio connesso a Visual Studio Azure Active Directory)?</span><span class="sxs-lookup"><span data-stu-id="3e856-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e856-104">Per iniziare</span><span class="sxs-lookup"><span data-stu-id="3e856-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="3e856-105">Risultati</span><span class="sxs-lookup"><span data-stu-id="3e856-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="3e856-106">Sono stati aggiunti riferimenti</span><span class="sxs-lookup"><span data-stu-id="3e856-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="3e856-107">Riferimenti al pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="3e856-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="3e856-108">Riferimenti a .NET</span><span class="sxs-lookup"><span data-stu-id="3e856-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="3e856-109">Modifiche al codice</span><span class="sxs-lookup"><span data-stu-id="3e856-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="3e856-110">Sono stati aggiunti file di codice al progetto</span><span class="sxs-lookup"><span data-stu-id="3e856-110">Code files were added to your project</span></span>
<span data-ttu-id="3e856-111">Al progetto è stata aggiunta una classe di avvio di autenticazione **App_Start/Startup.Auth.cs** contenente la logica di avvio per l'autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e856-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="3e856-112">È stato aggiunto un codice di avvio al progetto</span><span class="sxs-lookup"><span data-stu-id="3e856-112">Startup code was added to your project</span></span>
<span data-ttu-id="3e856-113">Se nel progetto è già presente una classe Startup, il metodo **Configuration** è stato aggiornato includendo una chiamata a `ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="3e856-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="3e856-114">In caso contrario, una classe Startup è stata aggiunta al progetto.</span><span class="sxs-lookup"><span data-stu-id="3e856-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="3e856-115">Il file app.config o web.config include nuovi valori di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e856-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="3e856-116">Sono state aggiunte le voci di configurazione seguenti.</span><span class="sxs-lookup"><span data-stu-id="3e856-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="3e856-117">È stata creata un'app Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e856-117">An Azure AD App was created</span></span>
<span data-ttu-id="3e856-118">Un'app Azure AD è stata creata nella directory selezionata nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="3e856-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="3e856-119">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e856-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="3e856-120">Se è stata selezionata l'opzione *Disabilitare l'autenticazione dell'account utente*, quali altre modifiche sono state apportate al progetto?</span><span class="sxs-lookup"><span data-stu-id="3e856-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="3e856-121">Sono stati rimossi i riferimenti del pacchetto NuGet, i file sono stati rimossi e viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="3e856-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="3e856-122">A seconda dello stato del progetto, è necessario rimuovere riferimenti aggiuntivi o i file manualmente o modificare codice in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="3e856-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="3e856-123">Riferimenti del pacchetto NuGet rimossi (per coloro che sono presenti)</span><span class="sxs-lookup"><span data-stu-id="3e856-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="3e856-124">È stato eseguito il backup dei file di codice e sono stati rimossi (per quelli presenti)</span><span class="sxs-lookup"><span data-stu-id="3e856-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="3e856-125">Per ognuno dei seguenti file è stato eseguito il backup e rimosso dal progetto.</span><span class="sxs-lookup"><span data-stu-id="3e856-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="3e856-126">I File di backup si trovano in una cartella 'Backup' alla radice della directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="3e856-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="3e856-127">Backup dei file di codice (per coloro che presenti)</span><span class="sxs-lookup"><span data-stu-id="3e856-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="3e856-128">Per ognuno dei seguenti file è stato eseguito il backup prima della sostituzione.</span><span class="sxs-lookup"><span data-stu-id="3e856-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="3e856-129">I File di backup si trovano in una cartella 'Backup' alla radice della directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="3e856-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="3e856-130">Quali modifiche aggiuntive sono state apportate al progetto dopo aver selezionato *Leggi i dati della directory*?</span><span class="sxs-lookup"><span data-stu-id="3e856-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="3e856-131">Sono state apportate altre modifiche al file app.config o web.config</span><span class="sxs-lookup"><span data-stu-id="3e856-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="3e856-132">Sono state aggiunte le voci di configurazione aggiuntive seguenti.</span><span class="sxs-lookup"><span data-stu-id="3e856-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="3e856-133">È stata aggiornata l'app Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e856-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="3e856-134">L'app Azure Active Directory è stata aggiornata per includere l'autorizzazione *Leggi i dati della directory* ed è stata creata una chiave aggiuntiva che è stata quindi usata come *ida:Password* nel file `web.config`.</span><span class="sxs-lookup"><span data-stu-id="3e856-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e856-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e856-135">Next steps</span></span>
- [<span data-ttu-id="3e856-136">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e856-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)


---
title: aaaChanges apportate tooa WebApi progetto quando ci si connette AD tooAzure | Documenti Microsoft
description: Viene descritto cosa succede tooyour WebApi progetto quando ci si connette AD tooAzure tramite Visual Studio
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
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="37658-103">Selezionare il progetto WebApi verificato anomalo toomy (servizio connesso di Visual Studio Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="37658-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37658-104">Per iniziare</span><span class="sxs-lookup"><span data-stu-id="37658-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="37658-105">Risultati</span><span class="sxs-lookup"><span data-stu-id="37658-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="37658-106">Sono stati aggiunti riferimenti</span><span class="sxs-lookup"><span data-stu-id="37658-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="37658-107">Riferimenti al pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="37658-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="37658-108">Riferimenti a .NET</span><span class="sxs-lookup"><span data-stu-id="37658-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="37658-109">Modifiche al codice</span><span class="sxs-lookup"><span data-stu-id="37658-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="37658-110">File di codice sono stati aggiunti tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="37658-110">Code files were added tooyour project</span></span>
<span data-ttu-id="37658-111">Una classe di avvio, l'autenticazione **App_Start/Startup.Auth.cs** tooyour progetto che contiene la logica di avvio per l'autenticazione di Azure AD è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="37658-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="37658-112">Codice di avvio è stato aggiunto il progetto tooyour</span><span class="sxs-lookup"><span data-stu-id="37658-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="37658-113">Se si dispone già di una classe di avvio del progetto, hello **configurazione** tooinclude aggiornata una chiamata di metodo troppo`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="37658-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="37658-114">In caso contrario, una classe di avvio è stato aggiunto il progetto tooyour.</span><span class="sxs-lookup"><span data-stu-id="37658-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="37658-115">Il file app.config o web.config include nuovi valori di configurazione.</span><span class="sxs-lookup"><span data-stu-id="37658-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="37658-116">Hello seguenti voci di configurazione è state aggiunte.</span><span class="sxs-lookup"><span data-stu-id="37658-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="37658-117">È stata creata un'app Azure AD</span><span class="sxs-lookup"><span data-stu-id="37658-117">An Azure AD App was created</span></span>
<span data-ttu-id="37658-118">Un'applicazione Azure AD è stata creata nella directory hello selezionate nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="37658-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="37658-119">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37658-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="37658-120">Se è stata selezionata *disabilitare l'autenticazione di account utente*, le altre modifiche apportate toomy progetto?</span><span class="sxs-lookup"><span data-stu-id="37658-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="37658-121">Sono stati rimossi i riferimenti del pacchetto NuGet, i file sono stati rimossi e viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="37658-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="37658-122">A seconda dello stato hello del progetto, è possibile toomanually rimuovere file o i riferimenti aggiuntivi o modificare codice nel modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="37658-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="37658-123">Riferimenti del pacchetto NuGet rimossi (per coloro che sono presenti)</span><span class="sxs-lookup"><span data-stu-id="37658-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="37658-124">È stato eseguito il backup dei file di codice e sono stati rimossi (per quelli presenti)</span><span class="sxs-lookup"><span data-stu-id="37658-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="37658-125">Ogni file seguente è stato eseguito il backup e rimosso dal progetto hello.</span><span class="sxs-lookup"><span data-stu-id="37658-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="37658-126">I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="37658-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="37658-127">Backup dei file di codice (per coloro che presenti)</span><span class="sxs-lookup"><span data-stu-id="37658-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="37658-128">Per ognuno dei seguenti file è stato eseguito il backup prima della sostituzione.</span><span class="sxs-lookup"><span data-stu-id="37658-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="37658-129">I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="37658-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="37658-130">Se è stata selezionata *lettura dati directory*, le altre modifiche apportate toomy progetto?</span><span class="sxs-lookup"><span data-stu-id="37658-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="37658-131">Sono state apportate modifiche aggiuntive tooyour file app. config o Web. config</span><span class="sxs-lookup"><span data-stu-id="37658-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="37658-132">Hello voci di configurazione aggiuntive seguenti sono state aggiunte.</span><span class="sxs-lookup"><span data-stu-id="37658-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="37658-133">È stata aggiornata l'app Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37658-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="37658-134">L'App di Azure Active Directory è stato aggiornato tooinclude hello *lettura dati directory* autorizzazione e un'altra chiave è stato creato che è stato utilizzato come hello *ida: Password* in hello `web.config` file.</span><span class="sxs-lookup"><span data-stu-id="37658-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37658-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37658-135">Next steps</span></span>
- [<span data-ttu-id="37658-136">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37658-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)


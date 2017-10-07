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
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>Selezionare il progetto WebApi verificato anomalo toomy (servizio connesso di Visual Studio Azure Active Directory)
> [!div class="op_single_selector"]
> * [Per iniziare](vs-active-directory-webapi-getting-started.md)
> * [Risultati](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Sono stati aggiunti riferimenti
### <a name="nuget-package-references"></a>Riferimenti al pacchetto NuGet
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>Riferimenti a .NET
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Modifiche al codice
### <a name="code-files-were-added-tooyour-project"></a>File di codice sono stati aggiunti tooyour progetto
Una classe di avvio, l'autenticazione **App_Start/Startup.Auth.cs** tooyour progetto che contiene la logica di avvio per l'autenticazione di Azure AD è stato aggiunto.

### <a name="startup-code-was-added-tooyour-project"></a>Codice di avvio è stato aggiunto il progetto tooyour
Se si dispone già di una classe di avvio del progetto, hello **configurazione** tooinclude aggiornata una chiamata di metodo troppo`ConfigureAuth(app)`. In caso contrario, una classe di avvio è stato aggiunto il progetto tooyour.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Il file app.config o web.config include nuovi valori di configurazione.
Hello seguenti voci di configurazione è state aggiunte.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>È stata creata un'app Azure AD
Un'applicazione Azure AD è stata creata nella directory hello selezionate nella procedura guidata hello.

[Altre informazioni su Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Se è stata selezionata *disabilitare l'autenticazione di account utente*, le altre modifiche apportate toomy progetto?
Sono stati rimossi i riferimenti del pacchetto NuGet, i file sono stati rimossi e viene eseguito il backup. A seconda dello stato hello del progetto, è possibile toomanually rimuovere file o i riferimenti aggiuntivi o modificare codice nel modo appropriato.

### <a name="nuget-package-references-removed-for-those-present"></a>Riferimenti del pacchetto NuGet rimossi (per coloro che sono presenti)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>È stato eseguito il backup dei file di codice e sono stati rimossi (per quelli presenti)
Ogni file seguente è stato eseguito il backup e rimosso dal progetto hello. I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Backup dei file di codice (per coloro che presenti)
Per ognuno dei seguenti file è stato eseguito il backup prima della sostituzione. I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Se è stata selezionata *lettura dati directory*, le altre modifiche apportate toomy progetto?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Sono state apportate modifiche aggiuntive tooyour file app. config o Web. config
Hello voci di configurazione aggiuntive seguenti sono state aggiunte.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>È stata aggiornata l'app Azure Active Directory
L'App di Azure Active Directory è stato aggiornato tooinclude hello *lettura dati directory* autorizzazione e un'altra chiave è stato creato che è stato utilizzato come hello *ida: Password* in hello `web.config` file.

## <a name="next-steps"></a>Passaggi successivi
- [Altre informazioni su Azure Active Directory](https://azure.microsoft.com/services/active-directory/)


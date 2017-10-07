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
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>Selezionare il progetto MVC verificato anomalo toomy (servizio connesso di Visual Studio Azure Active Directory)?
> [!div class="op_single_selector"]
> * [Per iniziare](vs-active-directory-dotnet-getting-started.md)
> * [Risultati](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Sono stati aggiunti riferimenti
### <a name="nuget-package-references"></a>Riferimenti al pacchetto NuGet
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>Riferimenti a .NET
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>È stato aggiunto codice
### <a name="code-files-were-added-tooyour-project"></a>File di codice sono stati aggiunti tooyour progetto
Una classe di avvio, l'autenticazione **App_Start/Startup.Auth.cs** tooyour progetto che contiene la logica di avvio per l'autenticazione di Azure AD è stato aggiunto. È stata anche aggiunta una classe controller, Controllers/AccountController.cs che include i metodi **SignIn()** e **SignOut()**. È stata infine aggiunta una visualizzazione parziale, **Views/Shared/_LoginPartial.cshtml** che include un collegamento azione per SignIn/SignOut.

### <a name="startup-code-was-added-tooyour-project"></a>Codice di avvio è stato aggiunto il progetto tooyour
Se si dispone già di una classe di avvio del progetto, hello **configurazione** tooinclude aggiornata una chiamata di metodo troppo**ConfigureAuth(app)**. In caso contrario, una classe di avvio è stato aggiunto il progetto tooyour.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>Il file app.config o web.config include nuovi valori di configurazione
Hello seguenti voci di configurazione è state aggiunte.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>È stata creata un'app Azure Active Directory (AD)
Un'applicazione Azure AD è stata creata nella directory hello selezionate nella procedura guidata hello.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Se è stata selezionata *disabilitare l'autenticazione di account utente*, le altre modifiche apportate toomy progetto?
Sono stati rimossi i riferimenti del pacchetto NuGet, i file sono stati rimossi e viene eseguito il backup. A seconda dello stato hello del progetto, è possibile toomanually rimuovere file o i riferimenti aggiuntivi o modificare codice nel modo appropriato.

### <a name="nuget-package-references-removed-for-those-present"></a>Riferimenti del pacchetto NuGet rimossi (per coloro che sono presenti)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>È stato eseguito il backup dei file di codice e sono stati rimossi (per quelli presenti)
Ogni file seguente è stato eseguito il backup e rimosso dal progetto hello. I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>Backup dei file di codice (per coloro che presenti)
Per ognuno dei seguenti file è stato eseguito il backup prima della sostituzione. I file di backup si trovano in una cartella "Backup" hello radice della directory del progetto hello.

* **Startup.cs**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Se è stata selezionata *lettura dati directory*, le altre modifiche apportate toomy progetto?
Sono stati aggiunti riferimenti aggiuntivi.

### <a name="additional-nuget-package-references"></a>Riferimenti al pacchetto NuGet aggiuntivi
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Riferimenti .NET aggiuntivi
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>File di codice aggiuntivi sono stati aggiunti tooyour progetto
Due file sono stati aggiunti toosupport la memorizzazione nella cache token: **Models\ADALTokenCache.cs** e **Models\ApplicationDbContext.cs**.  Un ulteriore controller e Visualizza sono stati aggiunti tooillustrate l'accesso a informazioni sul profilo utente utilizzando le API di graph di Azure.  Questi file sono **Controllers\UserProfileController.cs** e **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>Tooyour progetto è stato aggiunto altro codice di avvio
In hello **startup.auth.cs** file, un nuovo **OpenIdConnectAuthenticationNotifications** toohello è stato aggiunto l'oggetto **notifiche** membro di hello  **OpenIdConnectAuthenticationOptions**.  Si tratta di tooenable hello OAuth codice e ottenerne la un token di accesso.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Sono state apportate modifiche aggiuntive tooyour file app. config o Web. config
Hello voci di configurazione aggiuntive seguenti sono state aggiunte.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Hello seguenti sezioni di configurazione e di stringa di connessione sono state aggiunte.

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


### <a name="your-azure-active-directory-app-was-updated"></a>È stata aggiornata l'app Azure Active Directory
L'App di Azure Active Directory è stato aggiornato tooinclude hello *lettura dati directory* autorizzazione e un'altra chiave è stato creato che è stato utilizzato come hello *ida: ClientSecret* in hello  **Web. config** file.

## <a name="next-steps"></a>Passaggi successivi
- [Altre informazioni su Azure Active Directory](https://azure.microsoft.com/services/active-directory/)


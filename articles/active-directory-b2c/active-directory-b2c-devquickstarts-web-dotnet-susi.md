---
title: Active Directory B2C aaaAzure | Documenti Microsoft
description: Come toobuild un'applicazione web con sign-configurazione/Accedi, profilare, modifica e la password reimpostato tramite Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="7db84-103">Creare un'app Web ASP.NET con criteri di iscrizione, accesso, modifica del profilo e reimpostazione della password di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="7db84-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="7db84-104">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="7db84-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7db84-105">Aggiungere app web di Azure Active Directory B2C identità funzionalità tooyour</span><span class="sxs-lookup"><span data-stu-id="7db84-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="7db84-106">Registrare l'app Web nella directory Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7db84-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="7db84-107">Creare criteri di iscrizione/accesso, modifica del profilo e reimpostazione della password per l'app Web</span><span class="sxs-lookup"><span data-stu-id="7db84-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7db84-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7db84-108">Prerequisites</span></span>

- <span data-ttu-id="7db84-109">È necessario connettere l'account di Azure di tooan B2C Tenant.</span><span class="sxs-lookup"><span data-stu-id="7db84-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="7db84-110">È possibile creare un account Azure gratuito [qui](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="7db84-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="7db84-111">È necessario [Microsoft Visual Studio](https://www.visualstudio.com/) o programma tooview e modificare il codice di esempio hello simili.</span><span class="sxs-lookup"><span data-stu-id="7db84-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="7db84-112">Creare una directory Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7db84-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="7db84-113">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="7db84-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="7db84-114">Una directory è un contenitore per utenti, app, gruppi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="7db84-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="7db84-115">Se non è già stato fatto, creare una directory B2C prima di continuare con questa guida.</span><span class="sxs-lookup"><span data-stu-id="7db84-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="7db84-116">È necessario tooconnect hello B2C Tenant tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7db84-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="7db84-117">Dopo aver selezionato **crea**selezionare hello **toomy collegamento un esistente AD B2C Azure Tenant sottoscrizione di Azure** opzione e quindi in hello **Tenant di Azure Active Directory B2C** elenco a discesa, selezionare tenant Hello desiderato tooassociate.</span><span class="sxs-lookup"><span data-stu-id="7db84-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="7db84-118">Creare e registrare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="7db84-118">Create and register an application</span></span>

<span data-ttu-id="7db84-119">Successivamente, è necessario toocreate e registrare app hello nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7db84-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="7db84-120">Fornisce informazioni che Azure Active Directory B2C deve toosecurely comunicare con l'app.</span><span class="sxs-lookup"><span data-stu-id="7db84-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="7db84-121">Al termine, le impostazioni dell'applicazione includeranno un'API e un'applicazione nativa.</span><span class="sxs-lookup"><span data-stu-id="7db84-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="7db84-122">Creare criteri nel tenant B2C</span><span class="sxs-lookup"><span data-stu-id="7db84-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="7db84-123">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="7db84-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="7db84-124">Questo esempio di codice contiene tre esperienze di identità: **iscrizione e accesso**, **modifica del profilo** e **reimpostazione della password**.</span><span class="sxs-lookup"><span data-stu-id="7db84-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="7db84-125">È necessario toocreate un criterio di ogni tipo, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7db84-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="7db84-126">Per ogni criterio, essere attributo del nome visualizzato hello tooselect o attestazioni e toocopy verso il basso nome hello dei criteri per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="7db84-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="7db84-127">Aggiungere i provider di identità</span><span class="sxs-lookup"><span data-stu-id="7db84-127">Add your identity providers</span></span>

<span data-ttu-id="7db84-128">Dalle impostazioni selezionare **Provider di identità** e scegliere l'iscrizione tramite nome utente o posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7db84-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="7db84-129">Creare criteri di iscrizione e di accesso</span><span class="sxs-lookup"><span data-stu-id="7db84-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="7db84-130">Creare i criteri di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="7db84-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="7db84-131">Creare i criteri di reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="7db84-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="7db84-132">Dopo aver creato i criteri, si è pronti toobuild l'app.</span><span class="sxs-lookup"><span data-stu-id="7db84-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="7db84-133">Scaricare il codice di esempio hello</span><span class="sxs-lookup"><span data-stu-id="7db84-133">Download hello sample code</span></span>

<span data-ttu-id="7db84-134">codice Hello per questa esercitazione viene mantenuto nel [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="7db84-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="7db84-135">È possibile clonare: esempio hello eseguendo:</span><span class="sxs-lookup"><span data-stu-id="7db84-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="7db84-136">Dopo aver scaricato il codice di esempio hello, verrà avviato tooget file con estensione sln di hello aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7db84-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="7db84-137">file di soluzione Hello contiene due progetti: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="7db84-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="7db84-138">`TaskWebApp`è hello applicazione web MVC hello utente interagisce con.</span><span class="sxs-lookup"><span data-stu-id="7db84-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="7db84-139">`TaskService`è l'API web back-end dell'applicazione hello che archivia l'elenco di attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="7db84-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="7db84-140">Questo articolo viene illustrato solo hello `TaskWebApp` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7db84-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="7db84-141">toolearn come toobuild `TaskService` tramite Azure Active Directory B2C, vedere [l'esercitazione di api web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7db84-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="7db84-142">Aggiornare toouse codice i criteri e i tenant</span><span class="sxs-lookup"><span data-stu-id="7db84-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="7db84-143">L'esempio è configurato toouse hello criteri e i client ID dei nostri tenant dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="7db84-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="7db84-144">tooconnect è tooyour proprio tenant occorre tooopen `web.config` in hello `TaskWebApp` progetti e sostituire hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="7db84-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="7db84-145">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="7db84-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="7db84-146">`ida:ClientId` con l'ID dell'applicazione di tipo app Web</span><span class="sxs-lookup"><span data-stu-id="7db84-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="7db84-147">`ida:ClientSecret` con la chiave privata dell'app Web</span><span class="sxs-lookup"><span data-stu-id="7db84-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="7db84-148">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="7db84-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="7db84-149">`ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"</span><span class="sxs-lookup"><span data-stu-id="7db84-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="7db84-150">`ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"</span><span class="sxs-lookup"><span data-stu-id="7db84-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="7db84-151">Avviare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7db84-151">Launch hello app</span></span>
<span data-ttu-id="7db84-152">All'interno di Visual Studio, avviare app hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="7db84-153">Spostarsi sulla scheda elenco toohello e hello nota URl è: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="7db84-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="7db84-154">Iscriversi per l'applicazione hello utilizzando il nome utente o indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7db84-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="7db84-155">Disconnettersi, quindi accedere di nuovo e modificare il profilo di hello o reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="7db84-156">Disconnettersi ed eseguire l'accesso usando un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="7db84-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="7db84-157">Aggiungere i provider di identità per i social network</span><span class="sxs-lookup"><span data-stu-id="7db84-157">Add social IDPs</span></span>

<span data-ttu-id="7db84-158">App hello supporta attualmente solo utente per l'abbonamento e Accedi con **gli account locali**; gli account archiviati nella directory B2C che utilizzano un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="7db84-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="7db84-159">Tramite Azure AD B2C è possibile aggiungere il supporto per altri **provider di identità** (IdP) senza modificare il codice.</span><span class="sxs-lookup"><span data-stu-id="7db84-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="7db84-160">tooadd social IDPs tooyour app, iniziare eseguendo hello dettagliate negli articoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="7db84-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="7db84-161">Per ogni provider di identità toosupport, è necessario tooregister un'applicazione in tale sistema e ottenere un ID client.</span><span class="sxs-lookup"><span data-stu-id="7db84-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="7db84-162">Configurare Facebook come provider di identità</span><span class="sxs-lookup"><span data-stu-id="7db84-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="7db84-163">Configurare Google come provider di identità</span><span class="sxs-lookup"><span data-stu-id="7db84-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="7db84-164">Configurare Amazon come provider di identità</span><span class="sxs-lookup"><span data-stu-id="7db84-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="7db84-165">Configurare LinkedIn come provider di identità</span><span class="sxs-lookup"><span data-stu-id="7db84-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="7db84-166">Dopo aver aggiunto hello identity provider tooyour directory B2C, modifica il tooinclude tre criteri hello IDPs nuovo, come descritto in hello [articolo di riferimento dei criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7db84-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="7db84-167">Dopo aver salvato i criteri, eseguire l'applicazione hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="7db84-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="7db84-168">Dovrebbe essere hello che idps nuovo aggiunto come opzioni di accesso ed effettuare l'iscrizione in ognuna delle proprie esperienze di identità.</span><span class="sxs-lookup"><span data-stu-id="7db84-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="7db84-169">È possibile sperimentare i criteri e osservare l'effetto di hello nella tua app dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="7db84-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="7db84-170">Aggiungere o rimuovere provider di identità, manipolare le attestazioni dell'applicazione o modificare gli attributi per l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="7db84-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="7db84-171">Fare delle prove fino a quando non è chiaro il modo in cui criteri, richieste di autenticazione e OWIN sono collegati tra loro.</span><span class="sxs-lookup"><span data-stu-id="7db84-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="7db84-172">Procedura dettagliata per il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="7db84-172">Sample code walkthrough</span></span>
<span data-ttu-id="7db84-173">Hello le sezioni seguenti illustrano la configurazione del codice dell'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="7db84-174">È possibile usare queste sezioni come guida per lo sviluppo dell'app.</span><span class="sxs-lookup"><span data-stu-id="7db84-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="7db84-175">Aggiungere il supporto per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="7db84-175">Add authentication support</span></span>

<span data-ttu-id="7db84-176">È ora possibile configurare il toouse app Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7db84-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="7db84-177">L'app comunica con Azure AD B2C inviando richieste di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="7db84-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="7db84-178">le richieste di Hello prevedono esperienza utente hello app desidera tooexecute specificando criteri hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="7db84-179">È possibile utilizzare toosend libreria di Microsoft OWIN queste richieste, eseguire i criteri, gestire le sessioni utente e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="7db84-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="7db84-180">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="7db84-180">Install OWIN</span></span>

<span data-ttu-id="7db84-181">toobegin, aggiungere il progetto toohello pacchetti NuGet di hello OWIN middleware utilizzando hello Console di gestione di pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7db84-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="7db84-182">Aggiungere una classe di avvio OWIN</span><span class="sxs-lookup"><span data-stu-id="7db84-182">Add an OWIN startup class</span></span>

<span data-ttu-id="7db84-183">Aggiunge un toohello di classe di avvio OWIN API denominata `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="7db84-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="7db84-184">Fare clic su progetto hello, selezionare **Aggiungi** e **nuovo elemento**e quindi cercare OWIN.</span><span class="sxs-lookup"><span data-stu-id="7db84-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="7db84-185">middleware OWIN Hello richiamerà hello `Configuration(…)` metodo all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="7db84-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="7db84-186">In questo esempio, è stato modificato la dichiarazione di classe hello anche`public partial class Startup` e implementato hello altra parte della classe hello in `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="7db84-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="7db84-187">Inside hello `Configuration` (metodo), è stata aggiunta una chiamata troppo`ConfigureAuth`, definito in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="7db84-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="7db84-188">Dopo le modifiche di hello, `Startup.cs` sarà simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="7db84-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="7db84-189">Configurare il middleware di autenticazione hello</span><span class="sxs-lookup"><span data-stu-id="7db84-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="7db84-190">File aperti hello `App_Start\Startup.Auth.cs` e implementare hello `ConfigureAuth(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="7db84-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="7db84-191">parametri che vengono forniti in Hello `OpenIdConnectAuthenticationOptions` fungono da coordinate per toocommunicate l'app con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7db84-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="7db84-192">Se non si specifica determinati parametri, verrà utilizzato il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="7db84-193">Ad esempio, è stato specificato hello `ResponseType` nell'esempio hello hello così il valore predefinito `code id_token` verrà utilizzato in ogni tooAzure richiesta in uscita di Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7db84-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="7db84-194">È inoltre necessario tooset di autenticazione dei cookie.</span><span class="sxs-lookup"><span data-stu-id="7db84-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="7db84-195">il middleware di OpenID Connect Hello utilizza le sessioni utente toomaintain i cookie, tra l'altro.</span><span class="sxs-lookup"><span data-stu-id="7db84-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="7db84-196">In `OpenIdConnectAuthenticationOptions` sopra, è possibile definire un set di funzioni di callback per determinate notifiche ricevute dal middleware di OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="7db84-197">Questi comportamenti vengono definiti utilizzando un `OpenIdConnectAuthenticationNotifications` dell'oggetto e archiviati in hello `Notifications` variabile.</span><span class="sxs-lookup"><span data-stu-id="7db84-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="7db84-198">In questo esempio, è possibile definire tre callback diversi a seconda evento hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="7db84-199">Uso di criteri diversi</span><span class="sxs-lookup"><span data-stu-id="7db84-199">Using different policies</span></span>

<span data-ttu-id="7db84-200">Hello `RedirectToIdentityProvider` notifica viene attivata ogni volta che una richiesta tooAzure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7db84-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="7db84-201">Nella funzione di callback hello `OnRedirectToIdentityProvider`, controlliamo in hello in uscita chiamata se lo si desidera toouse criteri diversi.</span><span class="sxs-lookup"><span data-stu-id="7db84-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="7db84-202">In ordine toodo reimpostare o modificare un profilo di una password, è necessario toouse criterio corrispondente di hello, ad esempio criteri anziché hello "Iscrizione o accesso" criterio di reimpostazione password hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="7db84-203">In questo esempio, quando un utente richiede la password di hello tooreset o modificare il profilo di hello, aggiungiamo criteri hello preferiamo toouse nel contesto OWIN hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="7db84-204">Che può essere eseguita effettuando hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7db84-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="7db84-205">Ed è possibile implementare la funzione di callback hello `OnRedirectToIdentityProvider` eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7db84-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="7db84-206">Gestione dei codici di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="7db84-206">Handling authorization codes</span></span>

<span data-ttu-id="7db84-207">Hello `AuthorizationCodeReceived` notifica viene attivata quando viene ricevuto un codice di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="7db84-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="7db84-208">il middleware di OpenID Connect Hello non supporta lo scambio di codici per i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="7db84-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="7db84-209">È possibile scambiare manualmente il codice hello per token hello in una funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="7db84-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="7db84-210">Per ulteriori informazioni, consultare hello [documentazione](active-directory-b2c-devquickstarts-web-api-dotnet.md) che spiega come.</span><span class="sxs-lookup"><span data-stu-id="7db84-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="7db84-211">Gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="7db84-211">Handling errors</span></span>

<span data-ttu-id="7db84-212">Hello `AuthenticationFailed` notifica viene attivata quando l'autenticazione non riesce.</span><span class="sxs-lookup"><span data-stu-id="7db84-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="7db84-213">Nel relativo metodo di callback, è possibile gestire gli errori di hello nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="7db84-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="7db84-214">È tuttavia necessario aggiungere un controllo del codice di errore hello `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="7db84-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="7db84-215">Durante l'esecuzione di hello del criterio "Iscrizione o accesso" hello, utente hello è hello opportunità tooselect un **password dimenticata?** collegamento.</span><span class="sxs-lookup"><span data-stu-id="7db84-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="7db84-216">In questo caso, Azure Active Directory B2C invia l'app di tale codice di errore che indica che l'app deve effettuare una richiesta di usare i criteri di reimpostazione password hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="7db84-217">Inviare le richieste di autenticazione tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="7db84-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="7db84-218">L'app è configurato correttamente toocommunicate con Azure Active Directory B2C tramite protocollo di autenticazione OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="7db84-219">OWIN gestisce i dettagli di hello di creazione di messaggi di autenticazione, convalida dei token da Azure AD B2C e la gestione sessione utente.</span><span class="sxs-lookup"><span data-stu-id="7db84-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="7db84-220">Che rimane è tooinitiate del flusso di ciascun utente.</span><span class="sxs-lookup"><span data-stu-id="7db84-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="7db84-221">Quando un utente seleziona **Sign up/Sign in**, **Modifica profilo**, o **reimpostazione password** hello web App, viene richiamata l'azione di hello associata `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="7db84-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="7db84-222">È anche possibile utilizzare toosign OWIN utente hello dall'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="7db84-223">In `Controllers\AccountController.cs` c'è:</span><span class="sxs-lookup"><span data-stu-id="7db84-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="7db84-224">In aggiunta tooexplicitly richiamare un criterio, è possibile utilizzare un `[Authorize]` tag nei controller di che viene eseguito un criterio se hello utente non è registrato.</span><span class="sxs-lookup"><span data-stu-id="7db84-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="7db84-225">Aprire `Controllers\HomeController.cs` e aggiungere hello `[Authorize]` toohello tag attestazioni controller.</span><span class="sxs-lookup"><span data-stu-id="7db84-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="7db84-226">OWIN Seleziona ultimo criterio hello configurato quando hello `[Authorize]` tag viene raggiunto.</span><span class="sxs-lookup"><span data-stu-id="7db84-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="7db84-227">Visualizzare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="7db84-227">Display user information</span></span>

<span data-ttu-id="7db84-228">Quando si autenticano gli utenti tramite OpenID Connect, Azure AD B2C restituisce un'app toohello token ID contenente **attestazioni**.</span><span class="sxs-lookup"><span data-stu-id="7db84-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="7db84-229">Questi sono asserzioni relative utente hello.</span><span class="sxs-lookup"><span data-stu-id="7db84-229">These are assertions about hello user.</span></span> <span data-ttu-id="7db84-230">È possibile utilizzare le attestazioni toopersonalize l'app.</span><span class="sxs-lookup"><span data-stu-id="7db84-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="7db84-231">Aprire hello `Controllers\HomeController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7db84-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="7db84-232">È possibile accedere attestazioni utente nei controller di tramite hello `ClaimsPrincipal.Current` oggetto entità di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7db84-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="7db84-233">È possibile accedere a tutte le attestazioni che l'applicazione riceve in hello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="7db84-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="7db84-234">Un elenco di tutte le attestazioni hello riceve app hello è disponibile per l'utente in hello **attestazioni** pagina.</span><span class="sxs-lookup"><span data-stu-id="7db84-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>

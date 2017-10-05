---
title: Azure Active Directory B2C | Documentazione Microsoft
description: "Come compilare un'applicazione Web con funzionalità di registrazione, accesso, modifica del profilo e reimpostazione della password usando Azure Active Directory B2C."
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
ms.openlocfilehash: 3144ced01b524abb035dc1c6f0cdf764bec46804
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="f9335-103">Creare un'app Web ASP.NET con criteri di iscrizione, accesso, modifica del profilo e reimpostazione della password di Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="f9335-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="f9335-104">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="f9335-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9335-105">Aggiungere funzionalità di identità di Azure AD B2C all'app Web</span><span class="sxs-lookup"><span data-stu-id="f9335-105">Add Azure AD B2C identity features to your web app</span></span>
> * <span data-ttu-id="f9335-106">Registrare l'app Web nella directory Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f9335-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="f9335-107">Creare criteri di iscrizione/accesso, modifica del profilo e reimpostazione della password per l'app Web</span><span class="sxs-lookup"><span data-stu-id="f9335-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9335-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f9335-108">Prerequisites</span></span>

- <span data-ttu-id="f9335-109">È necessario connettere il tenant B2C a un account Azure.</span><span class="sxs-lookup"><span data-stu-id="f9335-109">You must connect your B2C Tenant to an Azure account.</span></span> <span data-ttu-id="f9335-110">È possibile creare un account Azure gratuito [qui](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="f9335-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="f9335-111">Per visualizzare e modificare il codice di esempio, è necessario [Microsoft Visual Studio](https://www.visualstudio.com/) o un programma simile.</span><span class="sxs-lookup"><span data-stu-id="f9335-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program to view and modify the sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="f9335-112">Creare una directory Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f9335-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="f9335-113">Prima di poter usare Azure AD B2C, è necessario creare una directory, o tenant.</span><span class="sxs-lookup"><span data-stu-id="f9335-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="f9335-114">Una directory è un contenitore per utenti, app, gruppi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f9335-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="f9335-115">Se non è già stato fatto, creare una directory B2C prima di continuare con questa guida.</span><span class="sxs-lookup"><span data-stu-id="f9335-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="f9335-116">È necessario connettere il tenant B2C alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9335-116">You need to connect the B2C Tenant to your Azure subscription.</span></span> <span data-ttu-id="f9335-117">Dopo aver selezionato **Crea**, selezionare l'opzione **Collega un tenant Azure AD B2C esistente alla sottoscrizione di Azure** e quindi selezionare il tenant che si vuole associare nell'elenco a discesa **Tenant Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="f9335-117">After selecting **Create**, select the **Link an existing Azure AD B2C Tenant to my Azure subscription** option, and then in the **Azure AD B2C Tenant** drop down, select the tenant you want to associate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="f9335-118">Creare e registrare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="f9335-118">Create and register an application</span></span>

<span data-ttu-id="f9335-119">È quindi necessario creare e registrare l'app nella directory B2C.</span><span class="sxs-lookup"><span data-stu-id="f9335-119">Next, you need to create and register the app in your B2C directory.</span></span> <span data-ttu-id="f9335-120">In questo modo, si forniscono ad Azure AD B2C le informazioni necessarie per comunicare in modo sicuro con l'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-120">This provides information that Azure AD B2C needs to securely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="f9335-121">Al termine, le impostazioni dell'applicazione includeranno un'API e un'applicazione nativa.</span><span class="sxs-lookup"><span data-stu-id="f9335-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="f9335-122">Creare criteri nel tenant B2C</span><span class="sxs-lookup"><span data-stu-id="f9335-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="f9335-123">In Azure AD B2C ogni esperienza utente è definita da [criteri](active-directory-b2c-reference-policies.md)specifici.</span><span class="sxs-lookup"><span data-stu-id="f9335-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f9335-124">Questo esempio di codice contiene tre esperienze di identità: **iscrizione e accesso**, **modifica del profilo** e **reimpostazione della password**.</span><span class="sxs-lookup"><span data-stu-id="f9335-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="f9335-125">È necessario creare i criteri per ogni tipo, come descritto nell' [articolo di riferimento per i criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f9335-125">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f9335-126">Per ogni criterio, assicurarsi di selezionare l'attributo o attestazione per il nome visualizzato e di copiare il nome del criterio per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="f9335-126">For each policy, be sure to select the Display name attribute or claim, and to copy down the name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="f9335-127">Aggiungere i provider di identità</span><span class="sxs-lookup"><span data-stu-id="f9335-127">Add your identity providers</span></span>

<span data-ttu-id="f9335-128">Dalle impostazioni selezionare **Provider di identità** e scegliere l'iscrizione tramite nome utente o posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="f9335-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="f9335-129">Creare criteri di iscrizione e di accesso</span><span class="sxs-lookup"><span data-stu-id="f9335-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="f9335-130">Creare i criteri di modifica del profilo</span><span class="sxs-lookup"><span data-stu-id="f9335-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="f9335-131">Creare i criteri di reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="f9335-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="f9335-132">Dopo aver creato i criteri è possibile passare alla compilazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-132">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="f9335-133">Scaricare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="f9335-133">Download the sample code</span></span>

<span data-ttu-id="f9335-134">Il codice per questa esercitazione è salvato su [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="f9335-134">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="f9335-135">È possibile clonare l'esempio eseguendo:</span><span class="sxs-lookup"><span data-stu-id="f9335-135">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="f9335-136">Dopo aver scaricato il codice di esempio, aprire il file SLN di Visual Studio per iniziare.</span><span class="sxs-lookup"><span data-stu-id="f9335-136">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="f9335-137">Il file della soluzione contiene due progetti: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="f9335-137">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="f9335-138">`TaskWebApp` è l'applicazione Web MVC con cui l'utente interagisce.</span><span class="sxs-lookup"><span data-stu-id="f9335-138">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="f9335-139">`TaskService` è l'API Web back-end dell'app in cui viene archiviato l'elenco attività di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="f9335-139">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="f9335-140">Questo articolo illustra solo l'applicazione `TaskWebApp`.</span><span class="sxs-lookup"><span data-stu-id="f9335-140">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="f9335-141">Per informazioni su come compilare `TaskService` usando Azure AD B2C, vedere l'[esercitazione sulle API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f9335-141">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-to-use-your-tenant-and-policies"></a><span data-ttu-id="f9335-142">Aggiornare il codice per usare il tenant e i criteri</span><span class="sxs-lookup"><span data-stu-id="f9335-142">Update code to use your tenant and policies</span></span>

<span data-ttu-id="f9335-143">L'esempio è configurato per l'uso dei criteri e dell'ID client del tenant demo.</span><span class="sxs-lookup"><span data-stu-id="f9335-143">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="f9335-144">Per connetterlo al tenant, è necessario aprire `web.config` nel progetto `TaskWebApp` e sostituire i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9335-144">To connect it to your own tenant, you need to open `web.config` in the `TaskWebApp` project and replace the following values:</span></span>

* <span data-ttu-id="f9335-145">`ida:Tenant` con il nome del tenant</span><span class="sxs-lookup"><span data-stu-id="f9335-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="f9335-146">`ida:ClientId` con l'ID dell'applicazione di tipo app Web</span><span class="sxs-lookup"><span data-stu-id="f9335-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="f9335-147">`ida:ClientSecret` con la chiave privata dell'app Web</span><span class="sxs-lookup"><span data-stu-id="f9335-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="f9335-148">`ida:SignUpSignInPolicyId` con il nome del criterio "Iscrizione o accesso"</span><span class="sxs-lookup"><span data-stu-id="f9335-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="f9335-149">`ida:EditProfilePolicyId` con il nome del criterio "Modifica profilo"</span><span class="sxs-lookup"><span data-stu-id="f9335-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="f9335-150">`ida:ResetPasswordPolicyId` con il nome del criterio "Reimposta password"</span><span class="sxs-lookup"><span data-stu-id="f9335-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-the-app"></a><span data-ttu-id="f9335-151">Avviare l'app</span><span class="sxs-lookup"><span data-stu-id="f9335-151">Launch the app</span></span>
<span data-ttu-id="f9335-152">Avviare l'app da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9335-152">From within Visual Studio, launch the app.</span></span> <span data-ttu-id="f9335-153">Passare alla scheda Elenco attività e notare che l'URI è: https://login.microsoftonline.com/*NomeTenant*/oauth2/v2.0/authorize?p=*NomeCriterioIscrizione*&client_id=*IDClient*.....</span><span class="sxs-lookup"><span data-stu-id="f9335-153">Navigate to the To-Do List tab, and note the URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="f9335-154">Effettuare l'iscrizione all'app usando un indirizzo e-mail o un nome utente.</span><span class="sxs-lookup"><span data-stu-id="f9335-154">Sign up for the app by using your email address or user name.</span></span> <span data-ttu-id="f9335-155">Disconnettersi, quindi accedere di nuovo e modificare il profilo o reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="f9335-155">Sign out, then sign in again and edit the profile or reset the password.</span></span> <span data-ttu-id="f9335-156">Disconnettersi ed eseguire l'accesso usando un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="f9335-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="f9335-157">Aggiungere i provider di identità per i social network</span><span class="sxs-lookup"><span data-stu-id="f9335-157">Add social IDPs</span></span>

<span data-ttu-id="f9335-158">Attualmente l'app supporta solo l'iscrizione e l'accesso dell'utente con **account locali**, ovvero gli account archiviati nella directory B2C che usano un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="f9335-158">Currently, the app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="f9335-159">Tramite Azure AD B2C è possibile aggiungere il supporto per altri **provider di identità** (IdP) senza modificare il codice.</span><span class="sxs-lookup"><span data-stu-id="f9335-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="f9335-160">Per aggiungere provider di identità per i social media all'applicazione, seguire le istruzioni dettagliate fornite in questi articoli.</span><span class="sxs-lookup"><span data-stu-id="f9335-160">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="f9335-161">Per ogni provider di identità che si vuole supportare, è necessario registrare un'applicazione nel relativo sistema e ottenere un ID client.</span><span class="sxs-lookup"><span data-stu-id="f9335-161">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="f9335-162">Configurare Facebook come provider di identità</span><span class="sxs-lookup"><span data-stu-id="f9335-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="f9335-163">Configurare Google come provider di identità</span><span class="sxs-lookup"><span data-stu-id="f9335-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="f9335-164">Configurare Amazon come provider di identità</span><span class="sxs-lookup"><span data-stu-id="f9335-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="f9335-165">Configurare LinkedIn come provider di identità</span><span class="sxs-lookup"><span data-stu-id="f9335-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="f9335-166">Dopo aver aggiunto i provider di identità alla directory B2C, modificare ognuno dei tre criteri per includere i nuovi provider di identità, come descritto nelle [informazioni di riferimento sui criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f9335-166">After you add the identity providers to your B2C directory, edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f9335-167">Dopo aver salvato i criteri, eseguire nuovamente l'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-167">After you save your policies, run the app again.</span></span>  <span data-ttu-id="f9335-168">I nuovi provider di identità dovrebbero essere stati aggiunti tra le opzioni di accesso e iscrizione in ognuna delle esperienze per l'identità.</span><span class="sxs-lookup"><span data-stu-id="f9335-168">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="f9335-169">Provare a usare i criteri e osservare gli effetti sull'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="f9335-169">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="f9335-170">Aggiungere o rimuovere provider di identità, manipolare le attestazioni dell'applicazione o modificare gli attributi per l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="f9335-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="f9335-171">Fare delle prove fino a quando non è chiaro il modo in cui criteri, richieste di autenticazione e OWIN sono collegati tra loro.</span><span class="sxs-lookup"><span data-stu-id="f9335-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="f9335-172">Procedura dettagliata per il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="f9335-172">Sample code walkthrough</span></span>
<span data-ttu-id="f9335-173">Le sezioni seguenti mostrano la configurazione del codice dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="f9335-173">The following sections show you how the sample application code is configured.</span></span> <span data-ttu-id="f9335-174">È possibile usare queste sezioni come guida per lo sviluppo dell'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="f9335-175">Aggiungere il supporto per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="f9335-175">Add authentication support</span></span>

<span data-ttu-id="f9335-176">È ora possibile configurare l'app per l'uso di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f9335-176">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="f9335-177">L'app comunica con Azure AD B2C inviando richieste di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f9335-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="f9335-178">Le richieste determinano l'esperienza dell'utente che l'app desidera eseguire specificando i criteri.</span><span class="sxs-lookup"><span data-stu-id="f9335-178">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="f9335-179">È possibile usare la libreria OWIN di Microsoft per inviare queste richieste, eseguire criteri, gestire le sessioni utente e così via.</span><span class="sxs-lookup"><span data-stu-id="f9335-179">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="f9335-180">Installare OWIN</span><span class="sxs-lookup"><span data-stu-id="f9335-180">Install OWIN</span></span>

<span data-ttu-id="f9335-181">Per iniziare, aggiungere i pacchetti NuGet del middleware OWIN al progetto usando la Console di Gestione pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9335-181">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="f9335-182">Aggiungere una classe di avvio OWIN</span><span class="sxs-lookup"><span data-stu-id="f9335-182">Add an OWIN startup class</span></span>

<span data-ttu-id="f9335-183">Aggiungere una classe di avvio OWIN all'API denominata `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="f9335-183">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="f9335-184">Fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** e quindi **Nuovo elemento** e cercare "OWIN".</span><span class="sxs-lookup"><span data-stu-id="f9335-184">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="f9335-185">Il middleware OWIN richiamerà il metodo `Configuration(…)` all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-185">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="f9335-186">In questo esempio la dichiarazione di classe è stata modificata in `public partial class Startup` ed è stata implementata l'altra parte della classe in `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="f9335-186">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="f9335-187">Nel metodo `Configuration` è stata aggiunta una chiamata a `ConfigureAuth`, definita in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="f9335-187">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="f9335-188">Dopo le modifiche, `Startup.cs` ha un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="f9335-188">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="f9335-189">Configurazione del middleware di autenticazione</span><span class="sxs-lookup"><span data-stu-id="f9335-189">Configure the authentication middleware</span></span>

<span data-ttu-id="f9335-190">Aprire il file `App_Start\Startup.Auth.cs` e implementare il metodo `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="f9335-190">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="f9335-191">I parametri indicati in `OpenIdConnectAuthenticationOptions` fungono da coordinate per consentire all'app di comunicare con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f9335-191">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="f9335-192">Se non si specificano determinati parametri, verrà usato il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="f9335-192">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="f9335-193">Ad esempio, nell'esercitazione non viene specificato `ResponseType`, pertanto il valore predefinito `code id_token` verrà usato in ciascuna richiesta in uscita per Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f9335-193">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="f9335-194">È necessario configurare anche l'autenticazione tramite cookie.</span><span class="sxs-lookup"><span data-stu-id="f9335-194">You also need to set up cookie authentication.</span></span> <span data-ttu-id="f9335-195">Il middleware OpenID Connect usa i cookie per gestire, tra l'altro, le sessioni utente.</span><span class="sxs-lookup"><span data-stu-id="f9335-195">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

<span data-ttu-id="f9335-196">In `OpenIdConnectAuthenticationOptions` sopra, si definisce un set di funzioni di callback per le notifiche specifiche che vengono ricevute dal middleware OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f9335-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="f9335-197">Questi comportamenti vengono definiti usando un oggetto `OpenIdConnectAuthenticationNotifications` memorizzato nella variabile `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="f9335-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="f9335-198">Nell'esempio vengono definiti tre diversi callback a seconda dell'evento.</span><span class="sxs-lookup"><span data-stu-id="f9335-198">In our sample, we define three different callbacks depending on the event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="f9335-199">Uso di criteri diversi</span><span class="sxs-lookup"><span data-stu-id="f9335-199">Using different policies</span></span>

<span data-ttu-id="f9335-200">La notifica `RedirectToIdentityProvider` viene attivata ogni volta che viene effettuata una richiesta per Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f9335-200">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="f9335-201">Nella funzione di callback `OnRedirectToIdentityProvider`, se si desidera usare criteri diversi è necessario controllare la chiamata in uscita.</span><span class="sxs-lookup"><span data-stu-id="f9335-201">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="f9335-202">Per reimpostare la password o modificare un profilo, è necessario usare i criteri corrispondenti, ad esempio i criteri di reimpostazione della password anziché i criteri predefiniti di "registrazione o accesso".</span><span class="sxs-lookup"><span data-stu-id="f9335-202">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="f9335-203">Nell'esempio quando un utente desidera reimpostare la password o modificare il profilo, vengono aggiunti i criteri che si desidera usare nel contesto di OWIN.</span><span class="sxs-lookup"><span data-stu-id="f9335-203">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="f9335-204">È possibile fare tutto questo effettuando le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9335-204">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="f9335-205">È inoltre possibile implementare la funzione di callback `OnRedirectToIdentityProvider` effettuando le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9335-205">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
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

### <a name="handling-authorization-codes"></a><span data-ttu-id="f9335-206">Gestione dei codici di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="f9335-206">Handling authorization codes</span></span>

<span data-ttu-id="f9335-207">La notifica `AuthorizationCodeReceived` viene attivata quando si riceve un codice di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="f9335-207">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="f9335-208">Il middleware OpenID Connect non supporta lo scambio di codici per i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="f9335-208">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="f9335-209">È possibile scambiare manualmente il codice per il token in una funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="f9335-209">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="f9335-210">Per altre informazioni, consultare la [documentazione](active-directory-b2c-devquickstarts-web-api-dotnet.md) che spiega la procedura.</span><span class="sxs-lookup"><span data-stu-id="f9335-210">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="f9335-211">Gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="f9335-211">Handling errors</span></span>

<span data-ttu-id="f9335-212">La notifica `AuthenticationFailed` viene attivata quando l'autenticazione non ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f9335-212">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="f9335-213">Nel metodo di callback è possibile gestire gli errori in base alle necessità.</span><span class="sxs-lookup"><span data-stu-id="f9335-213">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="f9335-214">È tuttavia necessario aggiungere un controllo del codice di errore `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="f9335-214">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="f9335-215">Durante l'esecuzione dei criteri di iscrizione o accesso, l'utente può fare clic sul collegamento **Password dimenticata?**.</span><span class="sxs-lookup"><span data-stu-id="f9335-215">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to select a **Forgot your password?** link.</span></span> <span data-ttu-id="f9335-216">In questo caso, Azure AD B2C invia all'app il codice di errore che indica che l'app deve effettuare una richiesta usando i criteri di reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="f9335-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
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

### <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="f9335-217">Inviare richieste di autenticazione ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9335-217">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="f9335-218">L'app è ora configurata correttamente per comunicare con Azure AD B2C usando il protocollo di autenticazione OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f9335-218">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="f9335-219">OWIN gestisce i dettagli relativi alla creazione dei messaggi di autenticazione, alla convalida dei token da Azure AD B2C e alla gestione della sessione utente.</span><span class="sxs-lookup"><span data-stu-id="f9335-219">OWIN manages the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="f9335-220">A questo punto, non resta che avviare ogni flusso utente.</span><span class="sxs-lookup"><span data-stu-id="f9335-220">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="f9335-221">Quando un utente seleziona **Accedi/Iscriviti**, **Modifica profilo** o **Reimposta password** nell'app Web, l'azione associata viene richiamata in `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="f9335-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="f9335-222">È anche possibile usare OWIN per disconnettere l'utente dell'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-222">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="f9335-223">In `Controllers\AccountController.cs` c'è:</span><span class="sxs-lookup"><span data-stu-id="f9335-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="f9335-224">Oltre a richiamare in modo esplicito i criteri, è possibile usare un tag `[Authorize]` nei controller per l'esecuzione dei criteri se l'utente non ha effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="f9335-224">In addition to explicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if the user is not signed in.</span></span> <span data-ttu-id="f9335-225">Aprire `Controllers\HomeController.cs` e aggiungere il tag `[Authorize]` al controller delle attestazioni.</span><span class="sxs-lookup"><span data-stu-id="f9335-225">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="f9335-226">Quando viene raggiunto il tag `[Authorize]` , OWIN seleziona l'ultimo criterio configurato.</span><span class="sxs-lookup"><span data-stu-id="f9335-226">OWIN selects the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="f9335-227">Visualizzare le informazioni utente</span><span class="sxs-lookup"><span data-stu-id="f9335-227">Display user information</span></span>

<span data-ttu-id="f9335-228">Quando si autenticano gli utenti usando OpenID Connect, Azure AD B2C restituisce un token ID all'app che contiene le **attestazioni**.</span><span class="sxs-lookup"><span data-stu-id="f9335-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="f9335-229">Si tratta di asserzioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="f9335-229">These are assertions about the user.</span></span> <span data-ttu-id="f9335-230">È possibile usare le attestazioni per personalizzare l'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-230">You can use claims to personalize your app.</span></span>

<span data-ttu-id="f9335-231">Aprire il file `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="f9335-231">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="f9335-232">È possibile accedere alle attestazioni utente nei controller tramite l'oggetto entità di sicurezza `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="f9335-232">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="f9335-233">È possibile accedere a qualsiasi attestazione ricevuta dall'applicazione nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="f9335-233">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="f9335-234">Nella pagina **Attestazioni** è disponibile un elenco di tutte le attestazioni ricevute dall'app.</span><span class="sxs-lookup"><span data-stu-id="f9335-234">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>

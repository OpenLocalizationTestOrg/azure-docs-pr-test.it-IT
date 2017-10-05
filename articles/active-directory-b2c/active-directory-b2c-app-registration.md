---
title: 'Azure Active Directory B2C: registrazione dell''applicazione | Documentazione Microsoft'
description: Come registrare l'applicazione con Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: 3d4fe2fa10d848c8b29e4d22d284c0d378f07ae0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="bdc88-103">Azure Active Directory B2C: registrare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="bdc88-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="bdc88-104">Questa esercitazione introduttiva consente di registrare un'applicazione in un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="bdc88-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="bdc88-105">Al termine, l'applicazione viene registrata per l'uso nel tenant di Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="bdc88-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc88-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bdc88-106">Prerequisites</span></span>

<span data-ttu-id="bdc88-107">Per compilare un'applicazione che accetta l'iscrizione e l'accesso dell'utente, è necessario innanzi tutto registrarla con tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="bdc88-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="bdc88-108">Per ottenere il tenant, seguire la procedura illustrata in [Azure Active Directory B2C: creare un tenant di Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdc88-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="bdc88-109">Le applicazioni create dal pannello Azure AD B2C nel portale di Azure devono essere gestite dalla stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="bdc88-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="bdc88-110">Le applicazioni B2C, se vengono modificate usando PowerShell o un altro portale, non sono più supportate e non funzionano con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bdc88-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="bdc88-111">Per altri dettagli, vedere la sezione [App con errori](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="bdc88-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="bdc88-112">Passare alle impostazioni di B2C</span><span class="sxs-lookup"><span data-stu-id="bdc88-112">Navigate to B2C settings</span></span>

<span data-ttu-id="bdc88-113">Accedere al [portale di Azure](https://portal.azure.com/) come amministratore globale del tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="bdc88-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="bdc88-114">Scegliere i passaggi successivi in base al tipo di applicazione da registrare:</span><span class="sxs-lookup"><span data-stu-id="bdc88-114">Choose next steps based on the application type you are registering:</span></span>

* [<span data-ttu-id="bdc88-115">Registrare un'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="bdc88-115">Register a web application</span></span>](#register-a-web-app)
* <span data-ttu-id="bdc88-116">[Registrare un'API Web](#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="bdc88-116">[Register a web API](#register-a-web-api)</span></span>
* [<span data-ttu-id="bdc88-117">Registrare un'applicazione per dispositivi mobili o nativa</span><span class="sxs-lookup"><span data-stu-id="bdc88-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="bdc88-118">Registrare un'app Web</span><span class="sxs-lookup"><span data-stu-id="bdc88-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="bdc88-119">Se l'applicazione Web chiama un'API Web protetta da Azure AD B2C, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bdc88-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="bdc88-120">Creare un segreto dell'applicazione passando al pannello **Chiavi** e facendo clic sul pulsante **Genera chiave**.</span><span class="sxs-lookup"><span data-stu-id="bdc88-120">Create an application secret by going to the **Keys** blade and clicking the **Generate Key** button.</span></span> <span data-ttu-id="bdc88-121">Annotare il valore di **Chiave dell'app**.</span><span class="sxs-lookup"><span data-stu-id="bdc88-121">Make note of the **App key** value.</span></span> <span data-ttu-id="bdc88-122">Questo valore viene usato come segreto dell'applicazione nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdc88-122">You use the value as the application secret in your application's code.</span></span>
   2. <span data-ttu-id="bdc88-123">Fare clic su **Accesso all'API**, quindi su **Aggiungi** e selezionare l'API Web e gli ambiti (autorizzazioni).</span><span class="sxs-lookup"><span data-stu-id="bdc88-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="bdc88-124">Un **segreto dell'applicazione** è una credenziale di sicurezza importante e deve essere protetto in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="bdc88-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="bdc88-125">Andare a **Passaggi successivi**</span><span class="sxs-lookup"><span data-stu-id="bdc88-125">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="bdc88-126">Registrare un'API Web</span><span class="sxs-lookup"><span data-stu-id="bdc88-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="bdc88-127">Fare clic su **Ambiti pubblicati** per aggiungere altri ambiti in base alla necessità.</span><span class="sxs-lookup"><span data-stu-id="bdc88-127">Click **Published scopes** to add more scopes as necessary.</span></span> <span data-ttu-id="bdc88-128">Per impostazione predefinita, viene definito l'ambito "user_impersonation",</span><span class="sxs-lookup"><span data-stu-id="bdc88-128">By default, the "user_impersonation" scope is defined.</span></span> <span data-ttu-id="bdc88-129">che consente ad altre applicazioni di accedere a questa API per conto dell'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="bdc88-129">The user_impersonation scope gives other applications the ability to access this api on behalf of the signed-in user.</span></span> <span data-ttu-id="bdc88-130">Se necessario, è possibile rimuovere l'ambito user_impersonation.</span><span class="sxs-lookup"><span data-stu-id="bdc88-130">If you wish, the user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="bdc88-131">Andare a **Passaggi successivi**</span><span class="sxs-lookup"><span data-stu-id="bdc88-131">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="bdc88-132">Registrare un'app per dispositivi mobili o nativa</span><span class="sxs-lookup"><span data-stu-id="bdc88-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="bdc88-133">Andare a **Passaggi successivi**</span><span class="sxs-lookup"><span data-stu-id="bdc88-133">Jump to **next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="bdc88-134">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="bdc88-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="bdc88-135">Scelta di un URL di risposta per un'API o un'app Web</span><span class="sxs-lookup"><span data-stu-id="bdc88-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="bdc88-136">Attualmente, le app registrate con Azure AD B2C sono limitate a un set specifico di valori di URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="bdc88-136">Currently, apps that are registered with Azure AD B2C are restricted to a limited set of reply URL values.</span></span> <span data-ttu-id="bdc88-137">Gli URL di risposta per le app e i servizi Web devono iniziare con lo schema `https` e tutti i valori degli URL di risposta devono condividere un singolo dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="bdc88-137">The reply URL for web apps and services must begin with the scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="bdc88-138">Non è possibile ad esempio registrare un'app Web con uno degli URL di risposta seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdc88-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="bdc88-139">Il sistema di registrazione confronta l'intero nome DNS dell'URL di risposta esistente con il nome DNS dell'URL di risposta che si sta aggiungendo.</span><span class="sxs-lookup"><span data-stu-id="bdc88-139">The registration system compares the whole DNS name of the existing reply URL to the DNS name of the reply URL that you are adding.</span></span> <span data-ttu-id="bdc88-140">La richiesta di aggiungere il nome DNS non viene soddisfatta se si verificano le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdc88-140">The request to add the DNS name fails if either of the following conditions is true:</span></span>

* <span data-ttu-id="bdc88-141">Il nome DNS intero del nuovo URL di risposta non corrisponde al nome DNS dell'URL di risposta esistente.</span><span class="sxs-lookup"><span data-stu-id="bdc88-141">The whole DNS name of the new reply URL does not match the DNS name of the existing reply URL.</span></span>
* <span data-ttu-id="bdc88-142">Il nome DNS intero del nuovo URL di risposta non è un sottodominio secondario dell'URL di risposta esistente.</span><span class="sxs-lookup"><span data-stu-id="bdc88-142">The whole DNS name of the new reply URL is not a subdomain of the existing reply URL.</span></span>

<span data-ttu-id="bdc88-143">Se ad esempio l'applicazione ha questo URL di risposta:</span><span class="sxs-lookup"><span data-stu-id="bdc88-143">For example, if the app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="bdc88-144">è possibile eseguire un'aggiunta analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="bdc88-144">You can add to it, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="bdc88-145">In questo caso, il nome DNS corrisponde esattamente.</span><span class="sxs-lookup"><span data-stu-id="bdc88-145">In this case, the DNS name matches exactly.</span></span> <span data-ttu-id="bdc88-146">In alternativa, è possibile eseguire un'aggiunta analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="bdc88-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="bdc88-147">In questo caso, si fa riferimento a un sottodominio DNS di login.contoso.com. Se si desidera un'app con URL di risposta login-east.contoso.com e login-west.contoso.com, è necessario aggiungere tali URL nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="bdc88-147">In this case, you're referring to a DNS subdomain of login.contoso.com. If you want to have an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="bdc88-148">Gli ultimi due URL possono essere aggiunti perché si tratta di sottodomini del primo URL di risposta, ovvero contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bdc88-148">You can add the latter two because they are subdomains of the first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="bdc88-149">Scelta di un URI di reindirizzamento per un'app nativa</span><span class="sxs-lookup"><span data-stu-id="bdc88-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="bdc88-150">Quando si sceglie un URI di reindirizzamento per applicazioni per dispositivi mobili/native, occorre tenere presenti due considerazioni importanti:</span><span class="sxs-lookup"><span data-stu-id="bdc88-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="bdc88-151">**Univocità**: lo schema dell'URI di reindirizzamento deve essere univoco per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdc88-151">**Unique**: The scheme of the redirect URI should be unique for every application.</span></span> <span data-ttu-id="bdc88-152">Nel nostro esempio (com.onmicrosoft.contoso.appname://redirect/path) viene usato com.onmicrosoft.contoso.appname come schema.</span><span class="sxs-lookup"><span data-stu-id="bdc88-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as the scheme.</span></span> <span data-ttu-id="bdc88-153">È consigliabile seguire questo modello.</span><span class="sxs-lookup"><span data-stu-id="bdc88-153">We recommend following this pattern.</span></span> <span data-ttu-id="bdc88-154">Se due applicazioni condividono lo stesso schema, viene visualizzata una finestra di dialogo di selezione dell'app.</span><span class="sxs-lookup"><span data-stu-id="bdc88-154">If two applications share the same scheme, the user sees a "choose app" dialog.</span></span> <span data-ttu-id="bdc88-155">Se la scelta dell'utente non è corretta, non è possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="bdc88-155">If the user makes an incorrect choice, the login fails.</span></span>
* <span data-ttu-id="bdc88-156">**Completezza**: l'URI di reindirizzamento deve avere uno schema e un percorso.</span><span class="sxs-lookup"><span data-stu-id="bdc88-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="bdc88-157">Il percorso deve contenere almeno una barra rovesciata dopo il dominio, ad esempio, //contoso/ funziona e //contoso ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="bdc88-157">The path must contain at least one forward slash after the domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="bdc88-158">Verificare che nell'URI di reindirizzamento non siano presenti caratteri speciali come caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="bdc88-158">Ensure there are no special characters like underscores in the redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="bdc88-159">App con errori</span><span class="sxs-lookup"><span data-stu-id="bdc88-159">Faulted apps</span></span>

<span data-ttu-id="bdc88-160">Le applicazioni B2C NON devono essere modificate:</span><span class="sxs-lookup"><span data-stu-id="bdc88-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="bdc88-161">In altri portali di gestione delle applicazioni, tra cui il [portale di Azure classico](https://manage.windowsazure.com/) o il [portale di registrazione delle applicazioni](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="bdc88-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="bdc88-162">Usando l'API Graph o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdc88-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="bdc88-163">Se si modifica l'applicazione B2C in uno di questi modi e si prova a modificarla di nuovo nel pannello delle funzionalità di Azure AD B2C nel portale di Azure, l'app si danneggia e non può più essere usata con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bdc88-163">If you edit the B2C application as described above and try to edit it again in the Azure AD B2C features blade on the Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="bdc88-164">A questo punto, è necessario eliminare l'applicazione e crearla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="bdc88-164">You have to delete the application and create it again.</span></span>

<span data-ttu-id="bdc88-165">Per eliminare l'app, passare al [portale di registrazione delle applicazioni](https://apps.dev.microsoft.com/) ed eliminarla nel portale.</span><span class="sxs-lookup"><span data-stu-id="bdc88-165">To delete the app, go to the [Application Registration Portal](https://apps.dev.microsoft.com/) and delete the application there.</span></span> <span data-ttu-id="bdc88-166">Per rendere l'applicazione visibile, è necessario essere il proprietario dell'applicazione (e non solo un amministratore del tenant).</span><span class="sxs-lookup"><span data-stu-id="bdc88-166">In order for the application to be visible, you need to be the owner of the application (and not just an admin of the tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdc88-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bdc88-167">Next steps</span></span>

<span data-ttu-id="bdc88-168">Dopo aver creato un'applicazione registrata con Azure AD B2C, è possibile completare una delle [esercitazioni di avvio rapido](active-directory-b2c-overview.md#get-started) per essere subito operativi.</span><span class="sxs-lookup"><span data-stu-id="bdc88-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) to get up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bdc88-169">Creare un'app Web ASP.NET con iscrizione, accesso e reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="bdc88-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
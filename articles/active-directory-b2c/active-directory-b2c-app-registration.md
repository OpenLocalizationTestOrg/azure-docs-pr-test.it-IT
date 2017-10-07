---
title: 'Azure Active Directory B2C: registrazione dell''applicazione | Documentazione Microsoft'
description: Come tooregister l'applicazione con Azure Active Directory B2C
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
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="d6e30-103">Azure Active Directory B2C: registrare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="d6e30-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="d6e30-104">Questa esercitazione introduttiva consente di registrare un'applicazione in un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d6e30-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="d6e30-105">Al termine, l'applicazione è registrata per l'uso nel tenant di Azure B2C hello.</span><span class="sxs-lookup"><span data-stu-id="d6e30-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6e30-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d6e30-106">Prerequisites</span></span>

<span data-ttu-id="d6e30-107">toobuild un'applicazione che accetta consumer per l'abbonamento e l'accesso, è necessario innanzitutto un'applicazione hello tooregister con un tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d6e30-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d6e30-108">Ottenere il proprio tenant utilizzando i passaggi descritti nella procedura hello [creare un tenant di Azure Active Directory B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6e30-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="d6e30-109">Le applicazioni create dal Pannello di Azure Active Directory B2C hello in hello portale di Azure devono essere gestite da hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="d6e30-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="d6e30-110">Se si modificano applicazioni B2C hello tramite PowerShell o un altro portale, essi diventano non supportati e non funzionano con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d6e30-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="d6e30-111">Visualizzare i dettagli di hello [errore app](#faulted-apps) sezione.</span><span class="sxs-lookup"><span data-stu-id="d6e30-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="d6e30-112">Passare a impostazioni tooB2C</span><span class="sxs-lookup"><span data-stu-id="d6e30-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="d6e30-113">Accedi toohello [portale di Azure](https://portal.azure.com/) come amministratore globale del tenant hello B2C hello.</span><span class="sxs-lookup"><span data-stu-id="d6e30-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="d6e30-114">Scegliere i passaggi successivi in base al tipo di applicazione hello che registrazione:</span><span class="sxs-lookup"><span data-stu-id="d6e30-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="d6e30-115">Registrare un'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="d6e30-115">Register a web application</span></span>](#register-a-web-app)
* <span data-ttu-id="d6e30-116">[Registrare un'API Web](#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="d6e30-116">[Register a web API](#register-a-web-api)</span></span>
* [<span data-ttu-id="d6e30-117">Registrare un'applicazione per dispositivi mobili o nativa</span><span class="sxs-lookup"><span data-stu-id="d6e30-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="d6e30-118">Registrare un'app Web</span><span class="sxs-lookup"><span data-stu-id="d6e30-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="d6e30-119">Se l'applicazione Web chiama un'API Web protetta da Azure AD B2C, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d6e30-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="d6e30-120">Creare un segreto dell'applicazione da passare toohello **chiavi** blade e facendo clic su hello **Genera chiave** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d6e30-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="d6e30-121">Prendere nota di hello **chiave App** valore.</span><span class="sxs-lookup"><span data-stu-id="d6e30-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="d6e30-122">Valore di hello è utilizzato come segreto dell'applicazione hello nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d6e30-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="d6e30-123">Fare clic su **Accesso all'API**, quindi su **Aggiungi** e selezionare l'API Web e gli ambiti (autorizzazioni).</span><span class="sxs-lookup"><span data-stu-id="d6e30-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="d6e30-124">Un **segreto dell'applicazione** è una credenziale di sicurezza importante e deve essere protetto in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="d6e30-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="d6e30-125">Passare troppo**passaggi successivi**</span><span class="sxs-lookup"><span data-stu-id="d6e30-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="d6e30-126">Registrare un'API Web</span><span class="sxs-lookup"><span data-stu-id="d6e30-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="d6e30-127">Fare clic su **pubblicati ambiti** tooadd più ambiti in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="d6e30-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="d6e30-128">Per impostazione predefinita, l'ambito "user_impersonation" hello è definito.</span><span class="sxs-lookup"><span data-stu-id="d6e30-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="d6e30-129">ambito user_impersonation Hello offre altri tooaccess possibilità di hello applicazioni questa api per conto di utente connesso di hello.</span><span class="sxs-lookup"><span data-stu-id="d6e30-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="d6e30-130">Se si desidera, è possibile rimuovere ambito user_impersonation hello.</span><span class="sxs-lookup"><span data-stu-id="d6e30-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="d6e30-131">Passare troppo**passaggi successivi**</span><span class="sxs-lookup"><span data-stu-id="d6e30-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="d6e30-132">Registrare un'app per dispositivi mobili o nativa</span><span class="sxs-lookup"><span data-stu-id="d6e30-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="d6e30-133">Passare troppo**passaggi successivi**</span><span class="sxs-lookup"><span data-stu-id="d6e30-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="d6e30-134">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="d6e30-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="d6e30-135">Scelta di un URL di risposta per un'API o un'app Web</span><span class="sxs-lookup"><span data-stu-id="d6e30-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="d6e30-136">Le applicazioni che sono registrate con Azure Active Directory B2C non sono attualmente limitate tooa limitato set di valori di URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="d6e30-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="d6e30-137">Hello reply URL per le applicazioni web e servizi deve iniziare con lo schema di hello `https`, e Rispondi a tutti i valori di URL devono condividere un singolo dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="d6e30-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="d6e30-138">Non è possibile ad esempio registrare un'app Web con uno degli URL di risposta seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6e30-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="d6e30-139">sistema di registrazione Hello Confronta hello intero DNS nome di hello esistente reply URL toohello DNS hello dell'URL di risposta che si sta aggiungendo.</span><span class="sxs-lookup"><span data-stu-id="d6e30-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="d6e30-140">hello tooadd di Hello richiesta nome DNS non riesce se viene soddisfatta una delle seguenti condizioni hello:</span><span class="sxs-lookup"><span data-stu-id="d6e30-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="d6e30-141">intero nome DNS Hello hello nuovo dell'URL di risposta non corrisponde il nome DNS hello hello esistente dell'URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="d6e30-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="d6e30-142">intero nome DNS Hello hello nuovo dell'URL di risposta non è un sottodominio hello esistente dell'URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="d6e30-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="d6e30-143">Ad esempio, se hello app è l'URL di risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="d6e30-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="d6e30-144">È possibile aggiungere tooit, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d6e30-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="d6e30-145">In questo caso, il nome DNS hello corrisponde esattamente.</span><span class="sxs-lookup"><span data-stu-id="d6e30-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="d6e30-146">In alternativa, è possibile eseguire un'aggiunta analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="d6e30-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="d6e30-147">In questo caso, si fa riferimento il sottodominio DNS tooa di login.contoso.com. Se si desidera toohave un'applicazione che dispone di account di accesso east.contoso.com e west.contoso.com account di accesso come URL di risposta, è necessario aggiungere tali URL di risposta in questo ordine:</span><span class="sxs-lookup"><span data-stu-id="d6e30-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="d6e30-148">È possibile aggiungere queste ultime hello perché sono sottodomini hello prima dell'URL di risposta, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d6e30-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="d6e30-149">Scelta di un URI di reindirizzamento per un'app nativa</span><span class="sxs-lookup"><span data-stu-id="d6e30-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="d6e30-150">Quando si sceglie un URI di reindirizzamento per applicazioni per dispositivi mobili/native, occorre tenere presenti due considerazioni importanti:</span><span class="sxs-lookup"><span data-stu-id="d6e30-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="d6e30-151">**Univoco**: schema hello dell'URI di reindirizzamento hello deve essere univoco per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="d6e30-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="d6e30-152">Nel nostro esempio (com.onmicrosoft.contoso.appname://redirect/path), utilizziamo com.onmicrosoft.contoso.appname lo schema di hello.</span><span class="sxs-lookup"><span data-stu-id="d6e30-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="d6e30-153">È consigliabile seguire questo modello.</span><span class="sxs-lookup"><span data-stu-id="d6e30-153">We recommend following this pattern.</span></span> <span data-ttu-id="d6e30-154">Se due applicazioni condividono hello stesso schema, hello utente visualizza una finestra di dialogo "Scegli app".</span><span class="sxs-lookup"><span data-stu-id="d6e30-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="d6e30-155">Se l'utente hello effettua una scelta errata, l'account di accesso hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d6e30-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="d6e30-156">**Completezza**: l'URI di reindirizzamento deve avere uno schema e un percorso.</span><span class="sxs-lookup"><span data-stu-id="d6e30-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="d6e30-157">percorso di Hello deve contenere almeno una barra rovesciata dopo dominio hello (ad esempio, //contoso/ works e ha esito negativo //contoso).</span><span class="sxs-lookup"><span data-stu-id="d6e30-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="d6e30-158">Verificare che non sono presenti caratteri speciali come carattere di sottolineatura hello uri di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="d6e30-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="d6e30-159">App con errori</span><span class="sxs-lookup"><span data-stu-id="d6e30-159">Faulted apps</span></span>

<span data-ttu-id="d6e30-160">Le applicazioni B2C NON devono essere modificate:</span><span class="sxs-lookup"><span data-stu-id="d6e30-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="d6e30-161">In altri portali di gestione delle applicazioni, tra cui il [portale di Azure classico](https://manage.windowsazure.com/) o il [portale di registrazione delle applicazioni](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d6e30-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="d6e30-162">Usando l'API Graph o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6e30-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="d6e30-163">Se si modifica un'applicazione hello B2C come descritto in precedenza e provare tooedit nuovamente nel Pannello di Azure Active Directory B2C hello funzionalità nel portale di Azure di hello, diventa un'app di errore e l'applicazione non è più utilizzabile con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d6e30-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="d6e30-164">Si dispone di un'applicazione hello toodelete e crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="d6e30-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="d6e30-165">app hello toodelete, andare toohello [portale di registrazione applicazione](https://apps.dev.microsoft.com/) ed eliminare l'applicazione hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="d6e30-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="d6e30-166">Affinché toobe applicazione hello visibile, è necessario proprietario hello toobe dell'applicazione hello (e non solo un amministratore del tenant hello).</span><span class="sxs-lookup"><span data-stu-id="d6e30-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6e30-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6e30-167">Next steps</span></span>

<span data-ttu-id="d6e30-168">Dopo aver creato un'applicazione registrata con Azure Active Directory B2C, è possibile completare una delle [le esercitazioni introduttive](active-directory-b2c-overview.md#get-started) tooget attivo e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d6e30-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6e30-169">Creare un'app Web ASP.NET con iscrizione, accesso e reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="d6e30-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
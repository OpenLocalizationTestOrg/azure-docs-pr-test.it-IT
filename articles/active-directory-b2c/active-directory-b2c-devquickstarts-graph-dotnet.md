---
title: 'Azure Active B2C di Directory: Hello di utilizzare API Graph | Documenti Microsoft'
description: "Come toocall hello API Graph per un tenant B2C tramite un processo di hello tooautomate identità dell'applicazione."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="79554-103">Azure Active Directory B2C: Utilizzare hello API Graph</span><span class="sxs-lookup"><span data-stu-id="79554-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="79554-104">Tenant di Azure Active Directory (Azure AD) B2C tendono toobe molto grandi.</span><span class="sxs-lookup"><span data-stu-id="79554-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="79554-105">Ciò significa che molte attività comuni di gestione tenant necessario toobe eseguita a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="79554-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="79554-106">ad esempio la gestione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="79554-106">A primary example is user management.</span></span> <span data-ttu-id="79554-107">Potrebbe essere necessario toomigrate un tenant B2C tooa di archivio utente esistente.</span><span class="sxs-lookup"><span data-stu-id="79554-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="79554-108">È possibile desidera toohost registrazione dell'utente nella propria pagina e creare gli account utente nella directory di Azure Active Directory B2C background hello.</span><span class="sxs-lookup"><span data-stu-id="79554-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="79554-109">Questi tipi di attività richiedono hello possibilità toocreate, lettura, aggiornamento ed eliminare account utente.</span><span class="sxs-lookup"><span data-stu-id="79554-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="79554-110">Queste attività eseguibili tramite l'API di Azure AD Graph hello.</span><span class="sxs-lookup"><span data-stu-id="79554-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="79554-111">Per i tenant B2C, esistono due modalità principali della comunicazione con l'API Graph hello.</span><span class="sxs-lookup"><span data-stu-id="79554-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="79554-112">Per le attività interattive, Esegui una volta, deve agire come un account di amministratore nel tenant B2C hello quando si eseguono attività hello.</span><span class="sxs-lookup"><span data-stu-id="79554-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="79554-113">Questa modalità richiede toosign un amministratore con le credenziali prima che gli amministratori possono eseguire qualsiasi toohello chiamate API Graph.</span><span class="sxs-lookup"><span data-stu-id="79554-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="79554-114">Per attività automatizzata, continua, utilizzare un tipo di account di servizio fornito con attività di gestione tooperform hello dei privilegi necessari.</span><span class="sxs-lookup"><span data-stu-id="79554-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="79554-115">In Azure AD, è possibile farlo registrando un'applicazione e l'autenticazione tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79554-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="79554-116">Questa operazione viene eseguita utilizzando un **ID applicazione** che utilizza hello [concessione di credenziali client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="79554-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="79554-117">In questo caso, un'applicazione hello funge da se stesso, non come un utente, hello toocall API Graph.</span><span class="sxs-lookup"><span data-stu-id="79554-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="79554-118">In questo articolo verrà trattato come tooperform hello caso d'uso automatizzata.</span><span class="sxs-lookup"><span data-stu-id="79554-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="79554-119">toodemonstrate, verrà creato un .NET 4.5 `B2CGraphClient` che esegue utente creare, leggere, aggiornare e l'eliminazione (CRUD).</span><span class="sxs-lookup"><span data-stu-id="79554-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="79554-120">client Hello avrà un'interfaccia di Windows della riga di comando (CLI) che consente di tooinvoke diversi metodi.</span><span class="sxs-lookup"><span data-stu-id="79554-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="79554-121">Tuttavia, hello codice toobehave in modo automatico non interattivo.</span><span class="sxs-lookup"><span data-stu-id="79554-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="79554-122">Ottenere un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="79554-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="79554-123">Prima di poter creare applicazioni o utenti, o interagire con Azure AD a, è necessario un account di amministratore globale nel tenant di hello e di un tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="79554-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="79554-124">Se non è già disponibile un tenant vedere l' [introduzione ad Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="79554-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="79554-125">Registrare l'applicazione nel tenant</span><span class="sxs-lookup"><span data-stu-id="79554-125">Register your application in your tenant</span></span>
<span data-ttu-id="79554-126">Dopo aver creato un tenant B2C, è necessario tooregister l'applicazione tramite hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79554-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79554-127">API di Graph toouse hello con il tenant B2C, sarà necessario tooregister un'applicazione dedicata utilizzando hello generico *registrazioni di App* pannello nel portale di Azure, hello **non** Azure Active Directory B2C  *Applicazioni* blade.</span><span class="sxs-lookup"><span data-stu-id="79554-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="79554-128">Non è possibile riutilizzare hello già esistenti B2C applicazioni registrate in Azure Active Directory B2C hello *applicazioni* blade.</span><span class="sxs-lookup"><span data-stu-id="79554-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="79554-129">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79554-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="79554-130">Scegliere il tenant di Azure Active Directory B2C, selezionare l'account in hello angolo superiore destro della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="79554-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="79554-131">Nel riquadro di navigazione a sinistra di hello, scegliere **più servizi**, fare clic su **registrazioni di App**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="79554-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="79554-132">Seguire le istruzioni di hello e creare una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="79554-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="79554-133">Selezionare **App Web / API** come tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="79554-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="79554-134">Fornire **qualsiasi URI di reindirizzamento** (ad esempio https://B2CGraphAPI) in quanto non è rilevante per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="79554-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="79554-135">Hello applicazione verranno ora visualizzati nell'elenco di hello delle applicazioni, fare clic su di esso hello tooobtain **ID applicazione** (noto anche come ID Client).</span><span class="sxs-lookup"><span data-stu-id="79554-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="79554-136">Copiarlo in quanto sarà necessario in una sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="79554-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="79554-137">Nel pannello impostazioni hello, fare clic su **chiavi** e aggiungere una nuova chiave (noto anche come segreto client).</span><span class="sxs-lookup"><span data-stu-id="79554-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="79554-138">Copiare anche questa per usarla in una sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="79554-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="79554-139">Configurare le autorizzazioni creare, leggere e aggiornare per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="79554-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="79554-140">È possibile procedere tooconfigure tooget l'applicazione che Hello tutti necessarie autorizzazioni toocreate, leggere, aggiornare ed eliminare gli utenti.</span><span class="sxs-lookup"><span data-stu-id="79554-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="79554-141">Continuare a hello pannello registrazioni di App del portale di Azure, selezionare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="79554-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="79554-142">Nel pannello impostazioni hello, fare clic su **delle autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="79554-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="79554-143">Nel Pannello di hello delle autorizzazioni necessarie, fare clic su **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79554-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="79554-144">Nel Pannello di hello Abilita l'accesso, selezionare hello **lettura e scrittura dati directory** autorizzazioni **autorizzazioni applicazione** e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="79554-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="79554-145">Infine, nel Pannello di hello delle autorizzazioni necessarie, fare clic su hello **concedere autorizzazioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="79554-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="79554-146">Ora è un'applicazione con autorizzazioni toocreate, lettura e aggiornamento gli utenti dal tenant B2C.</span><span class="sxs-lookup"><span data-stu-id="79554-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="79554-147">Configurare le autorizzazioni di eliminazione per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="79554-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="79554-148">Attualmente, hello *lettura e scrittura dati directory* autorizzazione **non** includono hello possibilità toodo le eliminazioni ad esempio l'eliminazione di utenti.</span><span class="sxs-lookup"><span data-stu-id="79554-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="79554-149">Se si desidera toogive toodelete utenti applicazione hello possibilità, è necessario toodo questi passaggi aggiuntivi che comportano PowerShell, in caso contrario, è possibile ignorare toohello nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="79554-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="79554-150">Innanzitutto, scaricare e installare hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="79554-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="79554-151">Quindi scaricare e installare hello [modulo di Azure Active Directory a 64 bit per Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="79554-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="79554-152">Dopo aver installato il modulo di PowerShell hello, aprire PowerShell e connettersi tooyour B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="79554-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="79554-153">Dopo aver eseguito `Get-Credential`, verrà richiesto di un nome utente e password, immettere il nome utente hello e una password dell'account di amministratore tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="79554-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79554-154">È necessario l'account di amministratore di tenant toouse un B2C è **locale** toohello B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="79554-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="79554-155">Questi account hanno un aspetto simile a questo: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="79554-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="79554-156">Ora si userà hello **ID applicazione** nello script hello sotto tooassign hello applicazione hello account amministratore ruolo utente che ne consentono agli utenti di toodelete.</span><span class="sxs-lookup"><span data-stu-id="79554-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="79554-157">Questi ruoli sono identificatori noti, pertanto è sufficiente toodo è di input del **ID applicazione** in script hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="79554-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="79554-158">A questo punto l'applicazione ha anche le autorizzazioni toodelete utenti dal tenant B2C.</span><span class="sxs-lookup"><span data-stu-id="79554-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="79554-159">Scaricare, configurare e compilare il codice di esempio hello</span><span class="sxs-lookup"><span data-stu-id="79554-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="79554-160">Innanzitutto, scaricare il codice di esempio hello e l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="79554-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="79554-161">Esaminare quindi il codice.</span><span class="sxs-lookup"><span data-stu-id="79554-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="79554-162">È possibile [scaricare codice di esempio hello come file con estensione zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="79554-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="79554-163">È anche possibile clonarlo nella directory desiderata:</span><span class="sxs-lookup"><span data-stu-id="79554-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="79554-164">Aprire hello `B2CGraphClient\B2CGraphClient.sln` soluzione di Visual Studio in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79554-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="79554-165">In hello `B2CGraphClient` progetto, il file aperto hello `App.config`.</span><span class="sxs-lookup"><span data-stu-id="79554-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="79554-166">Sostituire le impostazioni dell'app tre hello con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="79554-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="79554-167">Successivamente, fare clic su hello `B2CGraphClient` : esempio hello soluzione e ricompilare.</span><span class="sxs-lookup"><span data-stu-id="79554-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="79554-168">Se l'operazione riesce, sarà disponibile un file eseguibile `B2C.exe` in `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="79554-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="79554-169">Compilare le operazioni CRUD utente tramite l'API Graph hello</span><span class="sxs-lookup"><span data-stu-id="79554-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="79554-170">hello toouse B2CGraphClient, aprire un `cmd` Windows comando Chiedi conferma prima di modificare la directory toohello `Debug` directory.</span><span class="sxs-lookup"><span data-stu-id="79554-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="79554-171">Eseguire quindi hello `B2C Help` comando.</span><span class="sxs-lookup"><span data-stu-id="79554-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="79554-172">Verrà visualizzata una breve descrizione di ogni comando.</span><span class="sxs-lookup"><span data-stu-id="79554-172">This will display a brief description of each command.</span></span> <span data-ttu-id="79554-173">Ogni volta che si richiama uno di questi comandi, `B2CGraphClient` rende toohello una richiesta API di Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="79554-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="79554-174">Ottenere un token di accesso</span><span class="sxs-lookup"><span data-stu-id="79554-174">Get an access token</span></span>
<span data-ttu-id="79554-175">Qualsiasi toohello richiesta API Graph richiede un token di accesso per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="79554-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="79554-176">`B2CGraphClient`Usa hello open source Active Directory Authentication Library (ADAL) toohelp acquisire i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="79554-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="79554-177">ADAL semplifica l'acquisizione del token fornendo un'API semplice e avendo cura di alcuni dettagli importanti, come la memorizzazione nella cache dei token di accesso.</span><span class="sxs-lookup"><span data-stu-id="79554-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="79554-178">Token ADAL tooget toouse, non è tuttavia.</span><span class="sxs-lookup"><span data-stu-id="79554-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="79554-179">È anche possibile ottenere i token creando richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="79554-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="79554-180">In questo esempio di codice Usa ADAL v2 in ordine toocommunicate con hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="79554-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="79554-181">Nei token di accesso tooget ordine, che può essere usato con hello API Azure AD Graph, è necessario usare ADAL versione 2 o 3.</span><span class="sxs-lookup"><span data-stu-id="79554-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="79554-182">Quando `B2CGraphClient` viene eseguita, crea un'istanza di hello `B2CGraphClient` classe.</span><span class="sxs-lookup"><span data-stu-id="79554-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="79554-183">costruttore Hello per questa classe imposta lo scaffolding di un'autenticazione ADAL:</span><span class="sxs-lookup"><span data-stu-id="79554-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="79554-184">Si userà hello `B2C Get-User` comando come esempio.</span><span class="sxs-lookup"><span data-stu-id="79554-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="79554-185">Quando `B2C Get-User` viene richiamato senza alcun input aggiuntivi, hello CLI chiamate hello `B2CGraphClient.GetAllUsers(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="79554-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="79554-186">Questo metodo chiama `B2CGraphClient.SendGraphGetRequest(...)`, che invia un toohello di richiesta HTTP GET API Graph.</span><span class="sxs-lookup"><span data-stu-id="79554-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="79554-187">Prima di `B2CGraphClient.SendGraphGetRequest(...)` invia hello richiesta GET, innanzitutto Ottiene un token di accesso tramite ADAL:</span><span class="sxs-lookup"><span data-stu-id="79554-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="79554-188">È possibile ottenere un accesso token per hello API Graph dal chiamante hello ADAL `AuthenticationContext.AcquireToken(...)` metodo.</span><span class="sxs-lookup"><span data-stu-id="79554-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="79554-189">ADAL restituisce quindi un `access_token` che rappresenta l'identità dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="79554-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="79554-190">Leggere gli utenti</span><span class="sxs-lookup"><span data-stu-id="79554-190">Read users</span></span>
<span data-ttu-id="79554-191">Quando si desidera tooget un elenco di utenti o ottiene un utente specifico da hello API Graph, è possibile inviare un HTTP `GET` richiesta toohello `/users` endpoint.</span><span class="sxs-lookup"><span data-stu-id="79554-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="79554-192">Una richiesta per tutti gli utenti di hello in un tenant è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="79554-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="79554-193">toosee questa richiesta, eseguire:</span><span class="sxs-lookup"><span data-stu-id="79554-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="79554-194">Esistono due aspetti importanti toonote:</span><span class="sxs-lookup"><span data-stu-id="79554-194">There are two important things toonote:</span></span>

* <span data-ttu-id="79554-195">Hello token di accesso acquisito tramite la libreria ADAL viene aggiunto toohello `Authorization` intestazione usando hello `Bearer` schema.</span><span class="sxs-lookup"><span data-stu-id="79554-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="79554-196">Per i tenant B2C, è necessario utilizzare il parametro di query hello `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="79554-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="79554-197">Entrambi questi dettagli vengono gestiti in hello `B2CGraphClient.SendGraphGetRequest(...)` metodo:</span><span class="sxs-lookup"><span data-stu-id="79554-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="79554-198">Creare account utente consumer</span><span class="sxs-lookup"><span data-stu-id="79554-198">Create consumer user accounts</span></span>
<span data-ttu-id="79554-199">Quando si creano l'account utente nel tenant di B2C, è possibile inviare un HTTP `POST` richiesta toohello `/users` endpoint:</span><span class="sxs-lookup"><span data-stu-id="79554-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="79554-200">La maggior parte di queste proprietà in questa richiesta è necessario toocreate degli utenti.</span><span class="sxs-lookup"><span data-stu-id="79554-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="79554-201">toolearn più, fare clic su [qui](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="79554-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="79554-202">Si noti che hello `//` commenti sono stati inclusi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="79554-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="79554-203">Non includerli in una richiesta effettiva.</span><span class="sxs-lookup"><span data-stu-id="79554-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="79554-204">richiesta di hello toosee, eseguire uno dei seguenti comandi hello:</span><span class="sxs-lookup"><span data-stu-id="79554-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="79554-205">Hello `Create-User` comando accetta un file con estensione JSON come parametro di input.</span><span class="sxs-lookup"><span data-stu-id="79554-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="79554-206">Il file include una rappresentazione JSON di un oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="79554-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="79554-207">Sono disponibili due file con estensione JSON di esempio nel codice di esempio hello: `usertemplate-email.json` e `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="79554-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="79554-208">È possibile modificare questi file toosuit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="79554-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="79554-209">Inoltre toohello richiesto campi sopra indicati, sono inclusi numerosi campi facoltativi che è possibile utilizzare questi file.</span><span class="sxs-lookup"><span data-stu-id="79554-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="79554-210">Sono disponibili informazioni dettagliate su campi facoltativi hello in hello [riferimento all'entità di Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="79554-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="79554-211">È possibile visualizzare la richiesta POST hello viene costruito in `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="79554-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="79554-212">Collega un toohello token di accesso `Authorization` intestazione della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="79554-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="79554-213">Imposta `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="79554-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="79554-214">Include l'oggetto utente di hello JSON nel corpo di hello di hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="79554-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="79554-215">Se hello account che si desidera toomigrate da un archivio utente esistente è la complessità della password inferiore rispetto a hello [forza una password complessa applicata da Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), è possibile disabilitare il requisito di una password complessa hello utilizzando hello `DisableStrongPassword`valore hello `passwordPolicies` proprietà.</span><span class="sxs-lookup"><span data-stu-id="79554-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="79554-216">Ad esempio, è possibile modificare hello creare una richiesta utente fornita in precedenza, come indicato di seguito: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="79554-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="79554-217">Aggiornare gli account utente consumer</span><span class="sxs-lookup"><span data-stu-id="79554-217">Update consumer user accounts</span></span>
<span data-ttu-id="79554-218">Quando si aggiornano gli oggetti utente, il processo di hello è simile toohello uno che si utilizzano gli oggetti utente toocreate.</span><span class="sxs-lookup"><span data-stu-id="79554-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="79554-219">Ma questo processo Usa hello HTTP `PATCH` metodo:</span><span class="sxs-lookup"><span data-stu-id="79554-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="79554-220">Provare a un utente tooupdate aggiornando i file JSON con i nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="79554-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="79554-221">È quindi possibile utilizzare `B2CGraphClient` toorun uno di questi comandi:</span><span class="sxs-lookup"><span data-stu-id="79554-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="79554-222">Controllare hello `B2CGraphClient.SendGraphPatchRequest(...)` metodo per informazioni dettagliate su come toosend questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="79554-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="79554-223">Cercare gli utenti</span><span class="sxs-lookup"><span data-stu-id="79554-223">Search users</span></span>
<span data-ttu-id="79554-224">È possibile cercare gli utenti nel tenant di B2C in due modi:</span><span class="sxs-lookup"><span data-stu-id="79554-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="79554-225">Uno, usando l'ID oggetto dell'utente hello o due, utilizzare l'identificatore di accesso dell'utente hello (ad esempio, hello `signInNames` proprietà).</span><span class="sxs-lookup"><span data-stu-id="79554-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="79554-226">Eseguire uno dei seguenti comandi toosearch per un utente specifico hello:</span><span class="sxs-lookup"><span data-stu-id="79554-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="79554-227">Ecco alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="79554-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="79554-228">Eliminare gli utenti</span><span class="sxs-lookup"><span data-stu-id="79554-228">Delete users</span></span>
<span data-ttu-id="79554-229">il processo di Hello per l'eliminazione di un utente è semplice.</span><span class="sxs-lookup"><span data-stu-id="79554-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="79554-230">Hello utilizzare HTTP `DELETE` (metodo) e creare URL hello con hello correggere l'ID di oggetto:</span><span class="sxs-lookup"><span data-stu-id="79554-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="79554-231">toosee ad esempio, immettere questo comando e visualizzazione hello richiesta di eliminazione che viene stampato toohello console:</span><span class="sxs-lookup"><span data-stu-id="79554-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="79554-232">Controllare hello `B2CGraphClient.SendGraphDeleteRequest(...)` metodo per informazioni dettagliate su come toosend questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="79554-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="79554-233">È possibile eseguire molte altre operazioni con Azure AD Graph API hello in Gestione toouser aggiunta.</span><span class="sxs-lookup"><span data-stu-id="79554-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="79554-234">Le [informazioni di riferimento sull'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) illustrano i dettagli di ogni azione, insieme a richieste di esempio.</span><span class="sxs-lookup"><span data-stu-id="79554-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="79554-235">Usare gli attributi personalizzati</span><span class="sxs-lookup"><span data-stu-id="79554-235">Use custom attributes</span></span>
<span data-ttu-id="79554-236">La maggior parte delle applicazioni consumer necessario toostore alcuni tipi di informazioni sul profilo utente personalizzato.</span><span class="sxs-lookup"><span data-stu-id="79554-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="79554-237">A tale scopo, è un attributo personalizzato nel tenant di B2C toodefine.</span><span class="sxs-lookup"><span data-stu-id="79554-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="79554-238">È quindi possibile trattare hello tale attributo allo stesso modo, si considera di qualsiasi altra proprietà in un oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="79554-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="79554-239">È possibile aggiornare l'attributo hello, attributo hello di eliminazione, query dall'attributo hello, inviare attributo hello come attestazione nel token di accesso e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="79554-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="79554-240">toodefine un attributo personalizzato nel tenant di B2C, vedere hello [riferimento di attributo personalizzato B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="79554-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="79554-241">È possibile visualizzare gli attributi personalizzati di hello definiti nel tenant di B2C utilizzando `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="79554-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="79554-242">output di Hello di queste funzioni rivela dettagli hello di ogni attributo personalizzato, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="79554-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="79554-243">È possibile utilizzare hello nome completo, ad esempio `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, come una proprietà per gli oggetti utente.</span><span class="sxs-lookup"><span data-stu-id="79554-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="79554-244">Aggiornare il file con estensione JSON con una nuova proprietà hello e un valore per proprietà hello e quindi eseguire:</span><span class="sxs-lookup"><span data-stu-id="79554-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="79554-245">Se si usa `B2CGraphClient`, si ha a disposizione un'applicazione di servizio che può gestire gli utenti del tenant di B2C a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="79554-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="79554-246">`B2CGraphClient`Usa il proprio toohello tooauthenticate di identità applicazione API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="79554-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="79554-247">Acquisisce anche i token usando un segreto client.</span><span class="sxs-lookup"><span data-stu-id="79554-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="79554-248">Quando si incorpora questa funzionalità nell'applicazione, tenere presenti alcuni punti chiave per le applicazioni B2C:</span><span class="sxs-lookup"><span data-stu-id="79554-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="79554-249">È necessario toogrant hello applicazione hello delle autorizzazioni appropriate nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="79554-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="79554-250">Per il momento, è necessario i token di accesso tooget toouse ADAL (non MSAL).</span><span class="sxs-lookup"><span data-stu-id="79554-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="79554-251">È anche possibile inviare direttamente messaggi di protocollo, senza usare una raccolta.</span><span class="sxs-lookup"><span data-stu-id="79554-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="79554-252">Quando si chiama l'API Graph hello, utilizzare `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="79554-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="79554-253">Quando si creano e aggiornano utenti consumer, sono necessarie alcune proprietà, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="79554-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="79554-254">Se si hanno domande o richieste di azioni che si desidera tooperform tramite API Graph hello in tenant B2C lascia un commento in questo articolo o segnalare un problema nel repository di esempio hello GitHub codice.</span><span class="sxs-lookup"><span data-stu-id="79554-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>


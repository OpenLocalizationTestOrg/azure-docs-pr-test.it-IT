---
title: 'Azure Active Directory B2C: usare l''API Graph | Microsoft Docs'
description: "Come chiamare l'API Graph per un tenant di B2C usando l'identità di un'applicazione per automatizzare il processo."
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
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="d360f-103">Azure AD B2C: usare l'API Graph</span><span class="sxs-lookup"><span data-stu-id="d360f-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="d360f-104">I tenant di Azure Active Directory (Azure AD) B2C tendono ad avere dimensioni molto grandi,</span><span class="sxs-lookup"><span data-stu-id="d360f-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="d360f-105">il che significa che molte attività comuni di gestione dei tenant devono essere eseguite a livello di programmazione,</span><span class="sxs-lookup"><span data-stu-id="d360f-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="d360f-106">ad esempio la gestione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d360f-106">A primary example is user management.</span></span> <span data-ttu-id="d360f-107">Potrebbe essere necessario eseguire la migrazione di un archivio utenti esistente in un tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="d360f-108">Potrebbe essere necessario ospitare la registrazione degli utenti nella propria pagina e creare gli account utente nella directory Azure AD B2C in background.</span><span class="sxs-lookup"><span data-stu-id="d360f-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="d360f-109">Questi tipi di attività richiedono la possibilità di creare, leggere, aggiornare ed eliminare gli account utente.</span><span class="sxs-lookup"><span data-stu-id="d360f-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="d360f-110">È possibile eseguire queste attività usando l'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360f-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="d360f-111">Per i tenant di B2C esistono essenzialmente due modalità di comunicazione con l'API Graph.</span><span class="sxs-lookup"><span data-stu-id="d360f-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="d360f-112">Per le attività interattive da eseguire una sola volta, è consigliabile eseguire le attività con un account amministratore nel tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="d360f-113">Questa modalità richiede che un amministratore acceda con le credenziali prima di effettuare chiamate all'API Graph.</span><span class="sxs-lookup"><span data-stu-id="d360f-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="d360f-114">Per le attività automatizzate e continue è consigliabile usare un account del servizio a cui assegnare i privilegi necessari per eseguire le attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="d360f-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="d360f-115">In Azure AD è possibile ottenere questo risultato registrando un'applicazione ed effettuando l'autenticazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360f-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="d360f-116">A questo scopo usare un **ID applicazione** che usa la [concessione delle credenziali client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="d360f-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="d360f-117">In questo caso l'applicazione agisce autonomamente, non come utente, per chiamare l'API Graph.</span><span class="sxs-lookup"><span data-stu-id="d360f-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="d360f-118">In questo articolo verrà illustrato come eseguire il caso di uso automatizzato.</span><span class="sxs-lookup"><span data-stu-id="d360f-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="d360f-119">A scopo dimostrativo, verrà compilato un `B2CGraphClient` .NET 4.5 che esegue operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD, Create, Read, Update, Delete) di utenti.</span><span class="sxs-lookup"><span data-stu-id="d360f-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="d360f-120">Il client avrà un'interfaccia della riga di comando di Windows che consente di richiamare diversi metodi.</span><span class="sxs-lookup"><span data-stu-id="d360f-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="d360f-121">Tuttavia, il codice viene scritto affinché si comporti in modo automatico e non interattivo.</span><span class="sxs-lookup"><span data-stu-id="d360f-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d360f-122">Ottenere un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d360f-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="d360f-123">Prima di creare applicazioni o utenti oppure di interagire con Azure AD, saranno necessari un tenant di Azure AD B2C e un account amministratore globale in tale tenant.</span><span class="sxs-lookup"><span data-stu-id="d360f-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="d360f-124">Se non è già disponibile un tenant vedere l' [introduzione ad Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d360f-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="d360f-125">Registrare l'applicazione nel tenant</span><span class="sxs-lookup"><span data-stu-id="d360f-125">Register your application in your tenant</span></span>
<span data-ttu-id="d360f-126">Dopo aver creato un tenant B2C, è necessario registrare l'applicazione tramite il [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d360f-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d360f-127">Per usare l'API Graph con il tenant B2C, sarà necessario registrare un'applicazione dedicata usando il pannello generico *Registrazioni per l'app* nel portale di Azure, **NON** il pannello *Applicazioni* di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="d360f-128">Non è possibile usare nuovamente le applicazioni B2C già esistenti che sono state registrate nel pannello *Applicazioni* di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="d360f-129">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d360f-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d360f-130">Scegliere il tenant di Azure AD B2C selezionando l'account nell'angolo superiore destro della pagina.</span><span class="sxs-lookup"><span data-stu-id="d360f-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="d360f-131">Nel riquadro di spostamento a sinistra scegliere **More Services** (Altri servizi), fare clic su **Registrazioni per l'app** e quindi su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d360f-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="d360f-132">Seguire le istruzioni e creare una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d360f-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="d360f-133">Selezionare **App Web/API** come Tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="d360f-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="d360f-134">Fornire **qualsiasi URI di reindirizzamento** (ad esempio https://B2CGraphAPI) in quanto non è rilevante per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="d360f-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="d360f-135">L'applicazione verrà mostrata nell'elenco delle applicazioni, fare clic su di essa per ottenere l'**ID applicazione** (noto anche come ID Client).</span><span class="sxs-lookup"><span data-stu-id="d360f-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="d360f-136">Copiarlo in quanto sarà necessario in una sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="d360f-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="d360f-137">Nel pannello delle Impostazioni, fare clic su **Chiavi** e aggiungere una nuova chiave (nota anche come segreto client).</span><span class="sxs-lookup"><span data-stu-id="d360f-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="d360f-138">Copiare anche questa per usarla in una sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="d360f-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="d360f-139">Configurare le autorizzazioni creare, leggere e aggiornare per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="d360f-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="d360f-140">A questo punto è necessario configurare l'applicazione per ottenere tutte le autorizzazioni necessarie per creare, leggere, aggiornare ed eliminare gli utenti.</span><span class="sxs-lookup"><span data-stu-id="d360f-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="d360f-141">Continuando nel pannello Registrazioni per l'app del portale di Azure, selezionare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d360f-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="d360f-142">Nel pannello delle Impostazioni fare clic su **Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="d360f-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="d360f-143">Nel pannello delle Autorizzazioni necessarie, fare clic su **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d360f-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="d360f-144">Nel Pannello Abilita accesso selezionare l'autorizzazione **Legge e scrive i dati della directory** da **Autorizzazioni dell'applicazione** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d360f-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="d360f-145">Infine, nel pannello delle Autorizzazioni necessarie fare clic sul pulsante **Concedi autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="d360f-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="d360f-146">A questo punto è disponibile un'applicazione con le autorizzazioni per creare, leggere e aggiornare gli utenti dal tenant B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="d360f-147">Configurare le autorizzazioni di eliminazione per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="d360f-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="d360f-148">L'autorizzazione *Legge e scrive i dati della directory* attualmente **NON** include la possibilità di eseguire le eliminazioni, ad esempio l'eliminazione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d360f-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="d360f-149">Se si desidera assegnare all'applicazione la possibilità di eliminare gli utenti, è necessario eseguire questi passaggi aggiuntivi che coinvolgono PowerShell. In caso contrario, è possibile passare alla sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="d360f-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="d360f-150">Scaricare e installare prima l' [Assistente per l'accesso ai Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="d360f-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="d360f-151">Scaricare e installare quindi il [modulo di Azure Active Directory a 64 bit per Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="d360f-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="d360f-152">Dopo aver installato il modulo di PowerShell, aprire PowerShell e connettersi al tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="d360f-153">Dopo avere eseguito `Get-Credential`, verranno richiesti un nome utente e una password. Immettere il nome utente e la password dell'account amministratore del tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d360f-154">È necessario usare un account di amministratore tenant B2C che sia **locale** in relazione al tenant B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="d360f-155">Questi account hanno un aspetto simile a questo: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d360f-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="d360f-156">A questo punto si userà l'**ID applicazione** nello script seguente per assegnare all'applicazione il ruolo di amministratore account utente che consentirà di eliminare gli utenti.</span><span class="sxs-lookup"><span data-stu-id="d360f-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="d360f-157">Questi ruoli hanno identificatori noti, pertanto è sufficiente eseguire l'input dell'**ID applicazione** nello script seguente.</span><span class="sxs-lookup"><span data-stu-id="d360f-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="d360f-158">Ora l'applicazione dispone anche delle autorizzazioni per eliminare gli utenti dal tenant B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="d360f-159">Scaricare, configurare e compilare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="d360f-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="d360f-160">Scaricare prima di tutto il codice di esempio ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="d360f-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="d360f-161">Esaminare quindi il codice.</span><span class="sxs-lookup"><span data-stu-id="d360f-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="d360f-162">È possibile [scaricare il codice di esempio come file ZIP](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="d360f-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="d360f-163">È anche possibile clonarlo nella directory desiderata:</span><span class="sxs-lookup"><span data-stu-id="d360f-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="d360f-164">Aprire la soluzione Visual Studio `B2CGraphClient\B2CGraphClient.sln` in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d360f-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="d360f-165">Nel progetto `B2CGraphClient`, aprire il file `App.config`.</span><span class="sxs-lookup"><span data-stu-id="d360f-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="d360f-166">Sostituire le tre impostazioni dell'app con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="d360f-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="d360f-167">Fare quindi clic con il pulsante destro del mouse sulla soluzione `B2CGraphClient` e ricompilare l'esempio.</span><span class="sxs-lookup"><span data-stu-id="d360f-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="d360f-168">Se l'operazione riesce, sarà disponibile un file eseguibile `B2C.exe` in `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="d360f-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="d360f-169">Creare operazioni CRUD utente usando l'API Graph</span><span class="sxs-lookup"><span data-stu-id="d360f-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="d360f-170">Per usare B2CGraphClient aprire un prompt dei comandi `cmd` di Windows e passare alla directory `Debug`.</span><span class="sxs-lookup"><span data-stu-id="d360f-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="d360f-171">Eseguire quindi il comando `B2C Help` .</span><span class="sxs-lookup"><span data-stu-id="d360f-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="d360f-172">Verrà visualizzata una breve descrizione di ogni comando.</span><span class="sxs-lookup"><span data-stu-id="d360f-172">This will display a brief description of each command.</span></span> <span data-ttu-id="d360f-173">Ogni volta che si richiama uno di questi comandi, `B2CGraphClient` invia una richiesta all'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360f-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="d360f-174">Ottenere un token di accesso</span><span class="sxs-lookup"><span data-stu-id="d360f-174">Get an access token</span></span>
<span data-ttu-id="d360f-175">Qualsiasi richiesta per l'API Graph necessita di un token di accesso per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d360f-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="d360f-176">`B2CGraphClient` usa Active Directory Authentication Library (ADAL) open source per semplificare l'acquisizione di token di accesso.</span><span class="sxs-lookup"><span data-stu-id="d360f-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="d360f-177">ADAL semplifica l'acquisizione del token fornendo un'API semplice e avendo cura di alcuni dettagli importanti, come la memorizzazione nella cache dei token di accesso.</span><span class="sxs-lookup"><span data-stu-id="d360f-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="d360f-178">Non è tuttavia necessario usare ADAL per ottenere i token.</span><span class="sxs-lookup"><span data-stu-id="d360f-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="d360f-179">È anche possibile ottenere i token creando richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="d360f-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="d360f-180">Questo esempio di codice usa ADAL v2 per comunicare con l'API Graph.</span><span class="sxs-lookup"><span data-stu-id="d360f-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="d360f-181">Per ottenere token di accesso utilizzabili con l'API Graph di Azure AD, è necessario usare ADAL versione 2 o 3.</span><span class="sxs-lookup"><span data-stu-id="d360f-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="d360f-182">Quando si esegue `B2CGraphClient`, si crea un'istanza della classe `B2CGraphClient`.</span><span class="sxs-lookup"><span data-stu-id="d360f-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="d360f-183">Il costruttore per questa classe imposta uno scaffolding di autenticazione di ADAL:</span><span class="sxs-lookup"><span data-stu-id="d360f-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="d360f-184">Verrà usato come esempio il comando `B2C Get-User` .</span><span class="sxs-lookup"><span data-stu-id="d360f-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="d360f-185">Quando si richiama `B2C Get-User` senza input aggiuntivi, l’interfaccia della riga di comando chiama il metodo `B2CGraphClient.GetAllUsers(...)`.</span><span class="sxs-lookup"><span data-stu-id="d360f-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="d360f-186">Questo metodo chiama `B2CGraphClient.SendGraphGetRequest(...)`, che invia una richiesta HTTP GET all'API Graph.</span><span class="sxs-lookup"><span data-stu-id="d360f-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="d360f-187">Prima di inviare la richiesta GET, `B2CGraphClient.SendGraphGetRequest(...)` ottiene un token di accesso usando ADAL:</span><span class="sxs-lookup"><span data-stu-id="d360f-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="d360f-188">È possibile ottenere un token di accesso per l'API Graph chiamando il metodo `AuthenticationContext.AcquireToken(...)` di ADAL.</span><span class="sxs-lookup"><span data-stu-id="d360f-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="d360f-189">ADAL restituisce quindi un valore `access_token` che rappresenta l'identità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d360f-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="d360f-190">Leggere gli utenti</span><span class="sxs-lookup"><span data-stu-id="d360f-190">Read users</span></span>
<span data-ttu-id="d360f-191">Quando si vuole ottenere un elenco di utenti oppure un utente specifico dall'API Graph, è possibile inviare una richiesta HTTP `GET` all'endpoint `/users`.</span><span class="sxs-lookup"><span data-stu-id="d360f-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="d360f-192">Una richiesta per tutti gli utenti in un tenant ha un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="d360f-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d360f-193">Per visualizzare questa richiesta, eseguire:</span><span class="sxs-lookup"><span data-stu-id="d360f-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="d360f-194">Esistono due aspetti importanti da notare:</span><span class="sxs-lookup"><span data-stu-id="d360f-194">There are two important things to note:</span></span>

* <span data-ttu-id="d360f-195">Il token di accesso acquisito tramite ADAL viene aggiunto all'intestazione `Authorization` usando lo schema `Bearer`.</span><span class="sxs-lookup"><span data-stu-id="d360f-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="d360f-196">Per i tenant B2C, è necessario usare il parametro della query `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d360f-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="d360f-197">Entrambi questi dettagli vengono gestiti con il metodo `B2CGraphClient.SendGraphGetRequest(...)` :</span><span class="sxs-lookup"><span data-stu-id="d360f-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="d360f-198">Creare account utente consumer</span><span class="sxs-lookup"><span data-stu-id="d360f-198">Create consumer user accounts</span></span>
<span data-ttu-id="d360f-199">Quando si creano account utente nel tenant di B2C, è possibile inviare una richiesta HTTP `POST` all'endpoint `/users`:</span><span class="sxs-lookup"><span data-stu-id="d360f-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="d360f-200">La maggior parte delle proprietà di questa richiesta è necessaria per creare utenti consumer.</span><span class="sxs-lookup"><span data-stu-id="d360f-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="d360f-201">Per altre informazioni, fare clic [qui](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="d360f-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="d360f-202">I commenti `//` sono stati inclusi a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="d360f-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="d360f-203">Non includerli in una richiesta effettiva.</span><span class="sxs-lookup"><span data-stu-id="d360f-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="d360f-204">Per visualizzare la richiesta, eseguire uno dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d360f-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d360f-205">Il comando `Create-User` accetta un file con estensione json come parametro di input.</span><span class="sxs-lookup"><span data-stu-id="d360f-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="d360f-206">Il file include una rappresentazione JSON di un oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="d360f-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="d360f-207">Nel codice di esempio sono presenti due file con estensione json: `usertemplate-email.json` e `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="d360f-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="d360f-208">È possibile modificare questi file per adeguarli alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d360f-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="d360f-209">Oltre ai campi obbligatori precedenti, questi file includono alcuni campi facoltativi che possono essere usati.</span><span class="sxs-lookup"><span data-stu-id="d360f-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="d360f-210">Per informazioni dettagliate sui campi facoltativi, vedere le [informazioni di riferimento sull'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="d360f-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="d360f-211">Per informazioni sul modo in cui viene costruita la richiesta POST, vedere `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="d360f-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="d360f-212">Collega un token di accesso all'intestazione `Authorization` della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d360f-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="d360f-213">Imposta `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d360f-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="d360f-214">Include l'oggetto utente JSON nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d360f-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="d360f-215">Se gli account di cui si vuole eseguire la migrazione da un archivio utenti esistente hanno un livello di complessità della password inferiore al [livello avanzato di complessità della password applicato da Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), è possibile disabilitare il requisito per la password complessa usando il valore `DisableStrongPassword` nella proprietà `passwordPolicies`.</span><span class="sxs-lookup"><span data-stu-id="d360f-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="d360f-216">È ad esempio possibile modificare la richiesta di creazione utente indicata in precedenza come segue: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="d360f-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="d360f-217">Aggiornare gli account utente consumer</span><span class="sxs-lookup"><span data-stu-id="d360f-217">Update consumer user accounts</span></span>
<span data-ttu-id="d360f-218">Quando si aggiornano gli oggetti utente, il processo è simile a quello per la creazione di oggetti utente,</span><span class="sxs-lookup"><span data-stu-id="d360f-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="d360f-219">ma questo processo usa il metodo HTTP `PATCH`:</span><span class="sxs-lookup"><span data-stu-id="d360f-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="d360f-220">Provare ad aggiornare un utente aggiornando i file JSON con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="d360f-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="d360f-221">È quindi possibile usare `B2CGraphClient` per eseguire uno di questi comandi:</span><span class="sxs-lookup"><span data-stu-id="d360f-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d360f-222">Esaminare il metodo `B2CGraphClient.SendGraphPatchRequest(...)` per informazioni dettagliate su come inviare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="d360f-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="d360f-223">Cercare gli utenti</span><span class="sxs-lookup"><span data-stu-id="d360f-223">Search users</span></span>
<span data-ttu-id="d360f-224">È possibile cercare gli utenti nel tenant di B2C in due modi:</span><span class="sxs-lookup"><span data-stu-id="d360f-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="d360f-225">con l'ID oggetto dell'utente oppure con l'identificatore di accesso dell'utente, ovvero la proprietà `signInNames`.</span><span class="sxs-lookup"><span data-stu-id="d360f-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="d360f-226">Eseguire uno dei comandi seguenti per cercare un utente specifico:</span><span class="sxs-lookup"><span data-stu-id="d360f-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="d360f-227">Ecco alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="d360f-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="d360f-228">Eliminare gli utenti</span><span class="sxs-lookup"><span data-stu-id="d360f-228">Delete users</span></span>
<span data-ttu-id="d360f-229">Il processo per l'eliminazione di un utente è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="d360f-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="d360f-230">Usare il metodo HTTP `DELETE` e costruire l'URL con l'ID oggetto corretto:</span><span class="sxs-lookup"><span data-stu-id="d360f-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d360f-231">Per visualizzare un esempio, immettere questo comando e visualizzare la richiesta di eliminazione stampata nella console:</span><span class="sxs-lookup"><span data-stu-id="d360f-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="d360f-232">Esaminare il metodo `B2CGraphClient.SendGraphDeleteRequest(...)` per informazioni dettagliate su come inviare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="d360f-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="d360f-233">È possibile eseguire molte altre azioni con l'API Graph di Azure AD, oltre alla gestione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d360f-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="d360f-234">Le [informazioni di riferimento sull'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) illustrano i dettagli di ogni azione, insieme a richieste di esempio.</span><span class="sxs-lookup"><span data-stu-id="d360f-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="d360f-235">Usare gli attributi personalizzati</span><span class="sxs-lookup"><span data-stu-id="d360f-235">Use custom attributes</span></span>
<span data-ttu-id="d360f-236">La maggior parte delle applicazioni consumer deve archiviare alcune informazioni del profilo utente personalizzate.</span><span class="sxs-lookup"><span data-stu-id="d360f-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="d360f-237">Per eseguire questa operazione è ad esempio possibile definire un attributo personalizzato nel tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="d360f-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="d360f-238">È quindi possibile gestire l'attributo nello stesso modo in cui si gestisce qualsiasi altra proprietà in un oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="d360f-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="d360f-239">È possibile aggiornare l'attributo, eliminarlo, eseguire una query in base all'attributo, inviarlo come attestazione in un token di accesso e così via.</span><span class="sxs-lookup"><span data-stu-id="d360f-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="d360f-240">Per definire un attributo personalizzato nel tenant di B2C, vedere le [informazioni di riferimento sugli attributi personalizzati di B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="d360f-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="d360f-241">È possibile visualizzare gli attributi personalizzati definiti nel tenant di B2C usando `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="d360f-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="d360f-242">L'output di queste funzioni rivela i dettagli di ogni attributo personalizzato, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d360f-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="d360f-243">È possibile usare il nome completo, ad esempio `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, come proprietà per gli oggetti utente.</span><span class="sxs-lookup"><span data-stu-id="d360f-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="d360f-244">Aggiornare il file con estensione json con la nuova proprietà e un valore per la proprietà, quindi eseguire:</span><span class="sxs-lookup"><span data-stu-id="d360f-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="d360f-245">Se si usa `B2CGraphClient`, si ha a disposizione un'applicazione di servizio che può gestire gli utenti del tenant di B2C a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="d360f-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="d360f-246">`B2CGraphClient` usa la propria identità di applicazione per l'autenticazione all'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360f-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="d360f-247">Acquisisce anche i token usando un segreto client.</span><span class="sxs-lookup"><span data-stu-id="d360f-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="d360f-248">Quando si incorpora questa funzionalità nell'applicazione, tenere presenti alcuni punti chiave per le applicazioni B2C:</span><span class="sxs-lookup"><span data-stu-id="d360f-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="d360f-249">È necessario concedere all'applicazione le autorizzazioni appropriate nel tenant.</span><span class="sxs-lookup"><span data-stu-id="d360f-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="d360f-250">Attualmente è necessario usare ADAL (non MSAL) per ottenere i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="d360f-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="d360f-251">È anche possibile inviare direttamente messaggi di protocollo, senza usare una raccolta.</span><span class="sxs-lookup"><span data-stu-id="d360f-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="d360f-252">Quando si chiama l'API Graph, usare `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d360f-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="d360f-253">Quando si creano e aggiornano utenti consumer, sono necessarie alcune proprietà, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d360f-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="d360f-254">In caso di domande o richieste relative ad azioni che si vorrebbe eseguire mediante l'API Graph nel tenant di B2C, inserire un commento a questo articolo o inviare una richiesta nel repository di esempi di codice di GitHub.</span><span class="sxs-lookup"><span data-stu-id="d360f-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>


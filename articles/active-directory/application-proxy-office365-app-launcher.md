---
title: una home page personalizzata per le app pubblicate usando il Proxy di applicazione AD Azure aaaSet | Documenti Microsoft
description: Nozioni fondamentali di hello include informazioni sui connettori Proxy di applicazione di Azure AD
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="f487c-103">Impostare una home page personalizzata per le app pubblicate tramite il proxy applicazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f487c-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="f487c-104">Questo articolo illustra come tooconfigure App toodirect utenti tooa home page personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f487c-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="f487c-105">Quando si pubblica un'applicazione con Proxy dell'applicazione, si imposta un URL interno, ma che viene visualizzata agli utenti dovrebbe essere prima pagina di hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="f487c-106">Impostare una home page personalizzata in modo che gli utenti Vai a pagina destra toohello quando accedono alle App hello da hello Pannello di accesso di Azure Active Directory o l'utilità di avvio applicazione hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="f487c-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="f487c-107">Quando gli utenti avviano l'applicazione hello, gli si indirizzati dall'URL di dominio radice toohello predefinito per l'app pubblicata hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="f487c-108">pagina di destinazione Hello viene in genere impostato come URL della home page hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="f487c-109">Utilizzare gli URL home page personalizzata di hello Azure AD PowerShell modulo toodefine quando si desidera tooland agli utenti di app in una pagina specifica all'interno di app hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="f487c-110">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f487c-110">For example:</span></span>
- <span data-ttu-id="f487c-111">All'interno della rete azienda, gli utenti andare troppo*https://ExpenseApp/login/login.aspx* toosign in e accedere all'app.</span><span class="sxs-lookup"><span data-stu-id="f487c-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="f487c-112">Poiché si dispone di altre risorse come le immagini che il Proxy di applicazione deve tooaccess hello primo livello della struttura di cartelle hello, si pubblica l'applicazione hello con *https://ExpenseApp* come hello URL interno.</span><span class="sxs-lookup"><span data-stu-id="f487c-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="f487c-113">URL esterno predefinito è Hello *https://ExpenseApp-contoso.msappproxy.net*, che non accetta le credenziali di utenti toohello nella pagina.</span><span class="sxs-lookup"><span data-stu-id="f487c-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="f487c-114">Impostare *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* toogive URL pagina iniziale come hello agli utenti un'esperienza senza problemi.</span><span class="sxs-lookup"><span data-stu-id="f487c-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="f487c-115">Quando si concedono l'accesso agli utenti le app toopublished, hello App vengono visualizzate in hello [Pannello di accesso AD Azure](active-directory-saas-access-panel-introduction.md) hello e [avvio app di Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="f487c-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f487c-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="f487c-116">Before you start</span></span>

<span data-ttu-id="f487c-117">Prima di impostare l'URL della home page di hello, tenere hello presente i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f487c-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="f487c-118">Verificare che si specifica il percorso di hello è un percorso di sottodominio di hello URL radice del dominio.</span><span class="sxs-lookup"><span data-stu-id="f487c-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="f487c-119">Se l'URL del dominio radice hello è, ad esempio, https://apps.contoso.com/app1/, URL della home page hello configurate deve iniziare con https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="f487c-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="f487c-120">Se si apporta una modifica toohello pubblicare app, modifica hello potrebbe reimpostare il valore di hello dell'URL della home page hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="f487c-121">Quando si aggiorna l'applicazione hello in hello future, si deve ricontrollare e, se necessario, aggiornare l'URL della home page hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="f487c-122">Modifica hello home page di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f487c-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="f487c-123">Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f487c-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="f487c-124">Passare troppo**Azure Active Directory** > **registrazioni di App** e selezionare l'applicazione hello elenco.</span><span class="sxs-lookup"><span data-stu-id="f487c-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="f487c-125">Selezionare **proprietà** dalle impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="f487c-126">Hello aggiornamento **URL della Home page** campo con il nuovo percorso.</span><span class="sxs-lookup"><span data-stu-id="f487c-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Fornire nuovi URL della home page](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="f487c-128">Selezionare **Salva**</span><span class="sxs-lookup"><span data-stu-id="f487c-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="f487c-129">Modificare hello home page con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f487c-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="f487c-130">Installare il modulo di Azure AD PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="f487c-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="f487c-131">Prima di definire un URL della home page personalizzata tramite PowerShell, è possibile installare il modulo di Azure AD PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="f487c-132">È possibile scaricare i pacchetti hello da hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), che utilizza hello endpoint dell'API Graph.</span><span class="sxs-lookup"><span data-stu-id="f487c-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="f487c-133">tooinstall hello del pacchetto, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="f487c-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="f487c-134">Aprire una finestra di PowerShell di standard e quindi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f487c-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="f487c-135">Se si esegue il comando hello come un utente non amministratore, utilizzare hello `-scope currentuser` opzione.</span><span class="sxs-lookup"><span data-stu-id="f487c-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="f487c-136">Durante l'installazione di hello, selezionare **Y** tooinstall due pacchetti da Nuget.org. Sono necessari entrambi i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f487c-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="f487c-137">Trovare hello ObjectID dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f487c-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="f487c-138">Ottenere hello ObjectID dell'applicazione hello e quindi eseguire la ricerca per l'applicazione hello relativa home page.</span><span class="sxs-lookup"><span data-stu-id="f487c-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="f487c-139">Aprire PowerShell e importare il modulo di hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f487c-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="f487c-140">Accedi toohello modulo di Azure AD come amministratore tenant hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="f487c-141">Trovare l'applicazione hello in base all'URL della pagina iniziale.</span><span class="sxs-lookup"><span data-stu-id="f487c-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="f487c-142">È possibile trovare hello URL nel portale di hello passando troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f487c-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="f487c-143">Questo esempio usa *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="f487c-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="f487c-144">È necessario ottenere un risultato simile toohello uno qui.</span><span class="sxs-lookup"><span data-stu-id="f487c-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="f487c-145">Copiare hello toouse ObjectID GUID nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="f487c-146">Aggiornare l'URL della home page hello</span><span class="sxs-lookup"><span data-stu-id="f487c-146">Update hello home page URL</span></span>

<span data-ttu-id="f487c-147">Hello stesso modulo di PowerShell utilizzati per il passaggio 1, l'esecuzione hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f487c-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="f487c-148">Verificare di avere hello correggere app e sostituire *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* con hello ObjectID copiata nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="f487c-149">Ora che è stato confermato app hello, sei pronto tooupdate hello home page come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f487c-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="f487c-150">Creare un toohold oggetto applicazione vuota modifiche hello che si desidera toomake.</span><span class="sxs-lookup"><span data-stu-id="f487c-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="f487c-151">Questa variabile contiene i valori hello che si desidera tooupdate.</span><span class="sxs-lookup"><span data-stu-id="f487c-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="f487c-152">Non viene creato nulla in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="f487c-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="f487c-153">Impostare hello homepage URL toohello valore desiderato.</span><span class="sxs-lookup"><span data-stu-id="f487c-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="f487c-154">il valore di Hello deve essere un percorso di sottodominio di app pubblicata hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="f487c-155">Ad esempio, se si modifica hello URL della home page da *https://sharepoint-iddemo.msappproxy.net/* troppo*https://sharepoint-iddemo.msappproxy.net/hybrid/*, gli utenti di app andare direttamente toohello personalizzato pagina iniziale.</span><span class="sxs-lookup"><span data-stu-id="f487c-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="f487c-156">Rendere hello aggiornamento utilizzando hello GUID (ObjectID) che è stato copiato in "passaggio 1: trovare hello ObjectID dell'applicazione hello."</span><span class="sxs-lookup"><span data-stu-id="f487c-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="f487c-157">tooconfirm che modifica hello è stata completata correttamente, riavviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f487c-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="f487c-158">Le modifiche apportate app toohello potrebbero reimpostata hello URL della home page.</span><span class="sxs-lookup"><span data-stu-id="f487c-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="f487c-159">Se viene reimpostato l'URL della home page, ripetere il passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="f487c-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f487c-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f487c-160">Next steps</span></span>

- [<span data-ttu-id="f487c-161">Abilitare accesso remoto tooSharePoint con Proxy dell'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="f487c-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="f487c-162">Abilitare il Proxy di applicazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="f487c-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)

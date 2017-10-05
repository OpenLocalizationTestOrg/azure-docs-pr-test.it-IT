---
title: Impostare una home page personalizzata per le app pubblicate tramite il proxy applicazione di Azure AD | Microsoft Docs
description: Tratta i fondamenti dei connettori del proxy applicazione di Azure AD
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
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="3e023-103">Impostare una home page personalizzata per le app pubblicate tramite il proxy applicazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e023-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="3e023-104">In questo articolo viene illustrato come configurare le app per indirizzare gli utenti a una home page personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3e023-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="3e023-105">Quando si pubblica un'applicazione con Proxy dell'applicazione, si imposta un URL interno ma a volte non è la pagina che gli utenti dovrebbero vedere per prima.</span><span class="sxs-lookup"><span data-stu-id="3e023-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="3e023-106">Impostare una home page personalizzata in modo che gli utenti passino alla pagina corretta quando accedono alle app dal Pannello di accesso di Azure Active Directory o dall'utilità di avvio di app di Office 365.</span><span class="sxs-lookup"><span data-stu-id="3e023-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="3e023-107">Quando gli utenti avviano le app, per impostazione predefinita vengono indirizzati all'URL del dominio radice dell'app pubblicata.</span><span class="sxs-lookup"><span data-stu-id="3e023-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="3e023-108">La pagina di destinazione viene impostata in genere sull'URL della home page.</span><span class="sxs-lookup"><span data-stu-id="3e023-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="3e023-109">Usare il modulo PowerShell di Azure AD per definire l'URL della home page personalizzata quando si desidera che gli utenti dell'app arrivino ad una pagina specifica all'interno dell'app.</span><span class="sxs-lookup"><span data-stu-id="3e023-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="3e023-110">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3e023-110">For example:</span></span>
- <span data-ttu-id="3e023-111">All'interno della rete aziendale, gli utenti passano a *https://ExpenseApp/login/login.aspx* per registrarsi e accedere all'app.</span><span class="sxs-lookup"><span data-stu-id="3e023-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="3e023-112">Poiché si dispone di altre risorse come le immagini a cui il Proxy dell'applicazione deve accedere al livello superiore della struttura della cartella, si pubblica l'app con *https://ExpenseApp* come URL interno.</span><span class="sxs-lookup"><span data-stu-id="3e023-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="3e023-113">L'URL esterno predefinito è *https://ExpenseApp-contoso.msappproxy.net*, che non richiede agli utenti di registrarsi alla pagina.</span><span class="sxs-lookup"><span data-stu-id="3e023-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="3e023-114">Impostare *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* come URL della home page per offrire agli utenti un'esperienza senza problemi.</span><span class="sxs-lookup"><span data-stu-id="3e023-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="3e023-115">Quando si fornisce agli utenti l'accesso alle app pubblicate, le app vengono visualizzate nel [pannello di accesso di Azure AD](active-directory-saas-access-panel-introduction.md) e nell'[icona di avvio delle app di Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="3e023-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3e023-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3e023-116">Before you start</span></span>

<span data-ttu-id="3e023-117">Prima di impostare l'URL della home page, tenere presente i requisiti presenti:</span><span class="sxs-lookup"><span data-stu-id="3e023-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="3e023-118">Assicurarsi che il percorso specificato sia un percorso di sottodominio dell'URL del dominio radice.</span><span class="sxs-lookup"><span data-stu-id="3e023-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="3e023-119">Se l'URL del dominio radice è https://apps.contoso.com/app1/, l'URL della home page configurato deve iniziare con https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="3e023-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="3e023-120">Se si apporta una modifica all'app pubblicata, la modifica potrebbe reimpostare il valore dell'URL della home page.</span><span class="sxs-lookup"><span data-stu-id="3e023-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="3e023-121">Quando si decide di aggiornare l'app è quindi necessario verificare ed eventualmente aggiornare l'URL della home page.</span><span class="sxs-lookup"><span data-stu-id="3e023-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="3e023-122">Cambiare la home page nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3e023-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="3e023-123">Accedere al [portale di Azure](https://portal.azure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3e023-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="3e023-124">Passare ad **Azure Active Directory** > **Registrazioni per l'app** e scegliere l'applicazione dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="3e023-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="3e023-125">Selezionare **Proprietà** dalle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="3e023-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="3e023-126">Aggiornare il campo **URL della home page** con il nuovo percorso.</span><span class="sxs-lookup"><span data-stu-id="3e023-126">Update the **Home page URL** field with your new path.</span></span> 

   ![Fornire nuovi URL della home page](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="3e023-128">Selezionare **Salva**</span><span class="sxs-lookup"><span data-stu-id="3e023-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="3e023-129">Modificare la home page con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e023-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="3e023-130">Installare il modulo Azure AD PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e023-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="3e023-131">Prima di definire l'URL di una home page personalizzata tramite PowerShell è necessario installare il modulo Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e023-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="3e023-132">È possibile scaricare il pacchetto da [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), che usa l'endpoint API Graph.</span><span class="sxs-lookup"><span data-stu-id="3e023-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="3e023-133">Per installare il pacchetto, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3e023-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="3e023-134">Aprire una finestra di PowerShell standard ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="3e023-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="3e023-135">Se il comando non viene eseguito come amministratore, usare l'opzione `-scope currentuser`.</span><span class="sxs-lookup"><span data-stu-id="3e023-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="3e023-136">Durante l'installazione selezionare **Y** per installare due pacchetti da Nuget.org. Sono necessari entrambi i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3e023-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="3e023-137">Trovare il valore ObjectID dell'app</span><span class="sxs-lookup"><span data-stu-id="3e023-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="3e023-138">Ottenere il valore ObjectID dell'app e quindi cercare l'app tramite la relativa home page.</span><span class="sxs-lookup"><span data-stu-id="3e023-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="3e023-139">Aprire PowerShell e importare il modulo di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e023-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="3e023-140">Accedere al modulo di Azure AD come amministratore del tenant.</span><span class="sxs-lookup"><span data-stu-id="3e023-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="3e023-141">Individuare l'app in base all'URL della home page.</span><span class="sxs-lookup"><span data-stu-id="3e023-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="3e023-142">È possibile trovare l'URL nel portale passando ad **Azure Active Directory** > **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e023-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="3e023-143">Questo esempio usa *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="3e023-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="3e023-144">Viene visualizzato un risultato simile a quello illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3e023-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="3e023-145">Copiare il GUID di ObjectID da usare nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="3e023-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="3e023-146">Aggiornare l'URL della home page</span><span class="sxs-lookup"><span data-stu-id="3e023-146">Update the home page URL</span></span>

<span data-ttu-id="3e023-147">Nello stesso modulo PowerShell usato per il passaggio 1, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e023-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="3e023-148">Verificare che l'app sia corretta e sostituire *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* con il valore ObjectID copiato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="3e023-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="3e023-149">Ora che è stata verificata l'app, è possibile aggiornare la home page come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3e023-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="3e023-150">Creare un oggetto applicazione vuoto per le modifiche da apportare.</span><span class="sxs-lookup"><span data-stu-id="3e023-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="3e023-151">Questa variabile contiene i valori che si desidera aggiornare.</span><span class="sxs-lookup"><span data-stu-id="3e023-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="3e023-152">Non viene creato nulla in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="3e023-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="3e023-153">Impostare l'URL della home page sul valore desiderato.</span><span class="sxs-lookup"><span data-stu-id="3e023-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="3e023-154">Il valore deve essere un percorso di sottodominio dell'app pubblicata.</span><span class="sxs-lookup"><span data-stu-id="3e023-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="3e023-155">Se ad esempio si modifica l'URL della home page da *https://sharepoint-iddemo.msappproxy.net/* a *https://sharepoint-iddemo.msappproxy.net/hybrid/*, gli utenti vengono indirizzati direttamente alla home page personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3e023-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="3e023-156">Eseguire l'aggiornamento usando il GUID (ObjectID) copiato in "Passaggio 1: trovare il valore ObjectID dell'app".</span><span class="sxs-lookup"><span data-stu-id="3e023-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="3e023-157">Verificare che la modifica sia stata completata riavviando l'app.</span><span class="sxs-lookup"><span data-stu-id="3e023-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="3e023-158">Le modifiche apportate all'app possono reimpostare l'URL della home page.</span><span class="sxs-lookup"><span data-stu-id="3e023-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="3e023-159">Se viene reimpostato l'URL della home page, ripetere il passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="3e023-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e023-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e023-160">Next steps</span></span>

- [<span data-ttu-id="3e023-161">Abilitare l'accesso remoto a SharePoint con il proxy applicazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e023-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="3e023-162">Abilitare il proxy di applicazione nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3e023-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)

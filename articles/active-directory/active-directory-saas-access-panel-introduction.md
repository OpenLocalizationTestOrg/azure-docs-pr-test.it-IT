---
title: "Che cos'è il pannello di accesso in Azure Active Directory? | Microsoft Docs"
description: Informazioni su come usare le varianti del pannello di accesso (Web browser, app per Android e app per iPhone e iPad) per accedere alle app SaaS.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd9066c251188c0f18fe1a9403baa2beaeeb987c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-access-panel"></a><span data-ttu-id="533cc-104">Che cos'è il pannello di accesso?</span><span class="sxs-lookup"><span data-stu-id="533cc-104">What is the access panel?</span></span>

<span data-ttu-id="533cc-105">Il pannello di accesso è un portale basato sul Web.</span><span class="sxs-lookup"><span data-stu-id="533cc-105">The access panel is a web-based portal.</span></span> <span data-ttu-id="533cc-106">Il pannello consente a un utente con un account aziendale o dell'istituto di istruzione in Azure Active Directory di visualizzare e avviare applicazioni basate sul cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="533cc-106">It enables a user with a work or school account in Azure Active Directory to view and start cloud-based applications an Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="533cc-107">Tramite il pannello di accesso è anche possibile usare le funzionalità di gestione self-service di gruppi e app.</span><span class="sxs-lookup"><span data-stu-id="533cc-107">You can also use self-service group and app management capabilities through the access panel.</span></span>

<span data-ttu-id="533cc-108">Il pannello di accesso è separato dal portale di Azure e non richiede una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="533cc-108">The access panel is separate from the Azure portal and does not you to have an Azure subscription.</span></span>

![Pannello di accesso][1]

<span data-ttu-id="533cc-110">Il pannello di accesso consente di modificare alcune impostazioni del profilo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="533cc-110">The access panel enables you to edit some of your profile settings, including the ability to:</span></span>

- <span data-ttu-id="533cc-111">Cambiare la password associata a un account aziendale o dell'istituto di istruzione</span><span class="sxs-lookup"><span data-stu-id="533cc-111">Change the password associated with a work or school account</span></span>

- <span data-ttu-id="533cc-112">Modificare le impostazioni di ripristino password</span><span class="sxs-lookup"><span data-stu-id="533cc-112">Edit password reset settings</span></span>

- <span data-ttu-id="533cc-113">Modificare le impostazioni di preferenze e contatti relative a Multi-Factor Authentication (per gli account per cui un amministratore ne ha richiesto l'uso)</span><span class="sxs-lookup"><span data-stu-id="533cc-113">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator)</span></span>

- <span data-ttu-id="533cc-114">Visualizzare i dettagli dell'account, ad esempio l'ID utente, l'indirizzo di posta elettronica alternativo, i numeri del cellulare e dell'ufficio e i dispositivi</span><span class="sxs-lookup"><span data-stu-id="533cc-114">View account details, such as user ID, alternate email, and mobile and office phone numbers, and devices</span></span>

- <span data-ttu-id="533cc-115">Visualizzare e avviare applicazioni basate su cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="533cc-115">View and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="533cc-116">Per altre informazioni sul pannello di accesso dal punto di vista dell'utente, vedere Uso del pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="533cc-116">For more information about the access panel from the users’ perspective, see Using the access panel.</span></span> 

- <span data-ttu-id="533cc-117">Gestire i gruppi in modalità self-service.</span><span class="sxs-lookup"><span data-stu-id="533cc-117">Self-manage groups.</span></span> <span data-ttu-id="533cc-118">In particolare, l'amministratore può creare e gestire gruppi di sicurezza e richiedere appartenenze a gruppi di sicurezza in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="533cc-118">More specifically, the administrator can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="533cc-119">Per altre informazioni, vedere [Gestione dei gruppi in modalità self-service per gli utenti in Azure AD](active-directory-accessmanagement-self-service-group-management.md) e [Gestione dei gruppi](active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="533cc-119">For more information, see [Self-service group management for users in Azure AD](active-directory-accessmanagement-self-service-group-management.md) and [Manage your groups](active-directory-manage-groups.md).</span></span>




## <a name="accessing-the-access-panel"></a><span data-ttu-id="533cc-120">Apertura del pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="533cc-120">Accessing the access panel</span></span>

<span data-ttu-id="533cc-121">Per usare il pannello di accesso, aprire l'URL seguente in un Web browser: `http://myapps.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="533cc-121">You can access the access panel by visiting the following URL in a web browser: `http://myapps.microsoft.com`</span></span>

<span data-ttu-id="533cc-122">Se sono state configurate impostazioni di personalizzazione per la pagina di accesso, è possibile caricarle aggiungendo il dominio dell'organizzazione alla fine dell'URL: `http://myapps.microsoft.com/<your domain>.com`</span><span class="sxs-lookup"><span data-stu-id="533cc-122">If you have custom branding configured for your sign-in page, you can load this branding by appending your organization’s domain to the end of the URL: `http://myapps.microsoft.com/<your domain>.com`</span></span>

<span data-ttu-id="533cc-123">In questo caso, è possibile usare qualsiasi nome di dominio attivo o verificato che sia stato configurato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="533cc-123">In this case, you can use any active or verified domain name that has been configured in your Azure portal.</span></span>

![Nome di dominio di Wingtip Toys][2]  

<span data-ttu-id="533cc-125">Questo URL deve essere distribuito a tutti gli utenti che eseguiranno l'accesso ad applicazioni integrate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="533cc-125">You need to distribute the URL to all users who will sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="533cc-126">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="533cc-126">Authentication</span></span>

<span data-ttu-id="533cc-127">Per raggiungere il pannello di accesso, è necessario essere autenticati in Azure AD con un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="533cc-127">To reach the access panel, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="533cc-128">È possibile essere autenticati direttamente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="533cc-128">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="533cc-129">In alternativa, se un'organizzazione ha configurato la federazione con Active Directory Federation Services (AD FS) o altre tecnologie, è possibile essere autenticati con Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="533cc-129">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="533cc-130">Se si ha una sottoscrizione di Azure oppure un abbonamento a Office 365 ed è stato usato il portale di Azure o un'applicazione di Office 365, è possibile visualizzare l'elenco di applicazioni senza dover eseguire di nuovo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="533cc-130">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can see the list of applications without signing-in again.</span></span> <span data-ttu-id="533cc-131">Se non si è autenticati, viene chiesto di accedere usando il nome utente e la password dell'account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="533cc-131">If you are are not authenticated you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="533cc-132">Se l'organizzazione ha configurato la federazione, sarà sufficiente digitare il nome utente.</span><span class="sxs-lookup"><span data-stu-id="533cc-132">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="533cc-133">Dopo l'autenticazione, è possibile interagire con le applicazioni che l'amministratore ha integrato con la directory.</span><span class="sxs-lookup"><span data-stu-id="533cc-133">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="533cc-134">Per informazioni su come integrare le applicazioni con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="533cc-134">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="533cc-135">Requisiti del Web browser</span><span class="sxs-lookup"><span data-stu-id="533cc-135">Web browser requirements</span></span>

<span data-ttu-id="533cc-136">Il pannello di accesso richiede almeno un browser che supporti JavaScript e abbia CSS abilitato.</span><span class="sxs-lookup"><span data-stu-id="533cc-136">At a minimum, the access panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="533cc-137">Affinché gli utenti possano accedere alle applicazioni tramite l'accesso Single Sign-On (SSO) basato su password, è necessario installare l'estensione del pannello di accesso nel browser.</span><span class="sxs-lookup"><span data-stu-id="533cc-137">For the user to be signed in to applications through password-based single sign-on (SSO), the access panel extension must be installed in your browser.</span></span> <span data-ttu-id="533cc-138">Questa estensione viene scaricata automaticamente quando si seleziona un'applicazione configurata per l'accesso SSO basato su password.</span><span class="sxs-lookup"><span data-stu-id="533cc-138">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="533cc-139">L'estensione del pannello di accesso è attualmente disponibile per i browser Internet Explorer 8 e versioni successive, Microsoft Edge, Chrome e Firefox.</span><span class="sxs-lookup"><span data-stu-id="533cc-139">The access panel extension is currently available for Internet Explorer 8 and later, Edge, Chrome, and Firefox browsers.</span></span>

## <a name="mobile-app-support"></a><span data-ttu-id="533cc-140">Supporto per app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="533cc-140">Mobile app support</span></span>

<span data-ttu-id="533cc-141">Il team di Azure Active Directory pubblica l'app per dispositivi mobili App personali.</span><span class="sxs-lookup"><span data-stu-id="533cc-141">The Azure Active Directory team publishes the my apps mobile app.</span></span> <span data-ttu-id="533cc-142">Quando si installa l'app, è possibile accedere alle applicazioni SSO basate su password da dispositivi iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="533cc-142">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="533cc-143">È possibile accedere alle applicazioni che supportano la federazione con Azure AD (tra cui Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 e più di 70 altre applicazioni) praticamente in qualsiasi Web browser, su qualsiasi dispositivo, senza necessità di un plug-in o di un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="533cc-143">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="533cc-144">Tutte le altre [esperienze del pannello di accesso](https://myapps.microsoft.com/) non richiedono l'uso dell'app per dispositivi mobili App personali in un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="533cc-144">All other [access panel experiences](https://myapps.microsoft.com/) do also not require the my apps mobile app to be used on a mobile device.</span></span>
>
>

### <a name="my-apps-for-android"></a><span data-ttu-id="533cc-145">App personali per Android</span><span class="sxs-lookup"><span data-stu-id="533cc-145">My apps for Android</span></span>

<span data-ttu-id="533cc-146">App personali per Android è supportata su qualsiasi dispositivo Android che esegue Android 4.1 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="533cc-146">My apps for Android is supported on any Android device that is running Android version 4.1 and later.</span></span>  
<span data-ttu-id="533cc-147">È disponibile in [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span><span class="sxs-lookup"><span data-stu-id="533cc-147">It is available in the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span></span>

![App personali per Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="533cc-149">App personali per iPhone e iPad</span><span class="sxs-lookup"><span data-stu-id="533cc-149">My apps for iPhone and iPad</span></span>

<span data-ttu-id="533cc-150">App personali per iOS è supportata su qualsiasi iPhone o iPad che esegue iOS 7 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="533cc-150">My apps for iOS is supported on any iPhone or iPad that is running iOS version 7 and later.</span></span>  
<span data-ttu-id="533cc-151">È disponibile nell'[App Store di Apple](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span><span class="sxs-lookup"><span data-stu-id="533cc-151">It is available in the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![App personali per iOS][4]    



## <a name="managed-browser-for-my-apps"></a><span data-ttu-id="533cc-153">Managed browser per App personali</span><span class="sxs-lookup"><span data-stu-id="533cc-153">Managed browser for my apps</span></span>

<span data-ttu-id="533cc-154">App personali si integra anche in Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="533cc-154">My apps is also integrated in the Intune Managed Browser.</span></span> <span data-ttu-id="533cc-155">Intune Managed Browser per dispositivi iOS e Android svolge un ruolo fondamentale nel garantire la sicurezza dei dati nei dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="533cc-155">The Intune Managed Browser for iOS and Android devices plays a key role in ensuring that data on mobile devices stays secure.</span></span> <span data-ttu-id="533cc-156">Consente di visualizzare ed esplorare in tutta sicurezza pagine Web che potrebbero contenere informazioni aziendali e garantisce un'esperienza di esplorazione Web sicura.</span><span class="sxs-lookup"><span data-stu-id="533cc-156">It lets you safely view and navigate web pages that might contain company information, and provides a secure web-browsing experience.</span></span>  
<span data-ttu-id="533cc-157">È possibile accedere rapidamente ad App personali nella home page di Managed Browser e dai segnalibri, per poter aprire qualsiasi applicazione desiderata con un numero minore di clic.</span><span class="sxs-lookup"><span data-stu-id="533cc-157">You find quick access to my apps on your Managed Browser homepage and in your bookmarks, giving you fewer clicks to reach any application you want to access.</span></span>

<span data-ttu-id="533cc-158">Questo strumento è disponibile nell'[App Store di Apple](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e in [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span><span class="sxs-lookup"><span data-stu-id="533cc-158">It is available in the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span></span>

![Managed Browser per App personali][5]    





## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="533cc-160">Suggerimenti per testare l'esperienza utente</span><span class="sxs-lookup"><span data-stu-id="533cc-160">Tips for testing the user experience</span></span>

<span data-ttu-id="533cc-161">Gli amministratori di Azure che hanno eseguito l'accesso al portale di Azure usando un account nella directory accedono automaticamente al pannello di accesso con l'account corrente.</span><span class="sxs-lookup"><span data-stu-id="533cc-161">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the access panel as your current account.</span></span> <span data-ttu-id="533cc-162">In questo caso, potranno visualizzare tutte le applicazioni che sono state loro assegnate.</span><span class="sxs-lookup"><span data-stu-id="533cc-162">In this case, you can see all applications that have been assigned to you.</span></span>

<span data-ttu-id="533cc-163">**Per testare un account utente *diverso*:**</span><span class="sxs-lookup"><span data-stu-id="533cc-163">**To test as a *different* user account:**</span></span>

1. <span data-ttu-id="533cc-164">Fare clic sul menu utente nell'angolo superiore destro del portale di Azure o del pannello di accesso e selezionare **Disconnetti**.</span><span class="sxs-lookup"><span data-stu-id="533cc-164">Click the user menu in the upper-right corner of the Azure portal or the access panel, and then select **Sign Out**.</span></span> 
2. <span data-ttu-id="533cc-165">Passare al [pannello di accesso](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="533cc-165">Go to the [access panel](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="533cc-166">Nella pagina di accesso immettere il nome utente e la password dell'account nella directory da testare.</span><span class="sxs-lookup"><span data-stu-id="533cc-166">On the sign-in page, type the username and password for the account in your directory you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="533cc-167">Avvio delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="533cc-167">Starting applications</span></span>

<span data-ttu-id="533cc-168">Nel pannello di accesso possono essere visualizzati diversi tipi di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="533cc-168">Several types of applications can appear on the access panel.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="533cc-169">Applicazioni di Office 365</span><span class="sxs-lookup"><span data-stu-id="533cc-169">Office 365 applications</span></span>

<span data-ttu-id="533cc-170">Se l'organizzazione usa applicazioni di Office 365 di cui si ha la licenza, tali applicazioni vengono visualizzate nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="533cc-170">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your access panel.</span></span>

<span data-ttu-id="533cc-171">Quando si fa clic sul riquadro di un'applicazione di Office 365, si viene reindirizzati a tale applicazione e l'accesso viene eseguito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="533cc-171">When you click an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="533cc-172">Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione</span><span class="sxs-lookup"><span data-stu-id="533cc-172">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="533cc-173">L'amministratore può aggiungere applicazioni nella sezione Active Directory del portale di Azure con la modalità SSO impostata su **Single Sign-On di Microsoft Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="533cc-173">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="533cc-174">È possibile visualizzare le applicazioni solo se l'amministratore ha concesso l'accesso a tali applicazioni in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="533cc-174">You can only see these applications if your administrator has explicitly granted you access to the applications.</span></span>

<span data-ttu-id="533cc-175">Quando si fa clic su un riquadro di una di queste applicazioni, si viene reindirizzati a tale applicazione e l'accesso viene eseguito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="533cc-175">When you click a tile for one of these applications, you are redirected and automatically signed in to the application.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="533cc-176">Single Sign-On basato su password senza provisioning delle identità</span><span class="sxs-lookup"><span data-stu-id="533cc-176">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="533cc-177">L'amministratore può aggiungere applicazioni nella sezione Active Directory del portale di Azure con la modalità SSO impostata su **Accesso Single Sign-On basato su password**.</span><span class="sxs-lookup"><span data-stu-id="533cc-177">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="533cc-178">Tutti gli utenti della directory possono visualizzare tutte le applicazioni configurate in questa modalità.</span><span class="sxs-lookup"><span data-stu-id="533cc-178">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="533cc-179">La prima volta che si fa clic su un riquadro di una di queste applicazioni, viene chiesto di installare il plug-in per l'accesso Single Sign-On basato su password per Internet Explorer o Chrome.</span><span class="sxs-lookup"><span data-stu-id="533cc-179">The first time, you click a tile for one of these applications, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="533cc-180">L'installazione potrebbe richiedere il riavvio del Web browser.</span><span class="sxs-lookup"><span data-stu-id="533cc-180">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="533cc-181">Quando si torna al pannello di accesso e si fa clic di nuovo sul riquadro dell'applicazione, viene chiesto di specificare un nome utente e una password per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="533cc-181">When you return to the access panel and click the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="533cc-182">Dopo l'immissione di nome utente e password, queste credenziali vengono archiviate in modo sicuro e collegate all'account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="533cc-182">When you have entered your username and password, these credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="533cc-183">La volta successiva che si fa clic sul riquadro dell'applicazione, l'accesso all'applicazione viene eseguito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="533cc-183">The next time you click the application tile, you are automatically signed in to the application.</span></span>  
<span data-ttu-id="533cc-184">Non è necessario immettere nuovamente le credenziali e/o installare il plug-in per l'accesso SSO basato su password.</span><span class="sxs-lookup"><span data-stu-id="533cc-184">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="533cc-185">Se le credenziali sono cambiate nell'applicazione di destinazione di terze parti, è necessario aggiornare anche le credenziali archiviate in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="533cc-185">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="533cc-186">**Per aggiornare le credenziali:**</span><span class="sxs-lookup"><span data-stu-id="533cc-186">**To update credentials:**</span></span>

1. <span data-ttu-id="533cc-187">Selezionare l'icona nel riquadro dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="533cc-187">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="533cc-188">Selezionare **Aggiorna credenziali** per immettere di nuovo nome utente e password per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="533cc-188">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="533cc-189">Single Sign-On basato su password con provisioning delle identità</span><span class="sxs-lookup"><span data-stu-id="533cc-189">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="533cc-190">L'amministratore può aggiungere applicazioni nella sezione **Active Directory** del portale di Azure con la modalità SSO impostata su **Accesso Single Sign-On basato su password**, insieme al provisioning delle identità.</span><span class="sxs-lookup"><span data-stu-id="533cc-190">Your administrator can add applications in the **Active Directory** section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="533cc-191">La prima volta che si fa clic su un riquadro di una di queste applicazioni, viene chiesto di installare il **plug-in per l'accesso SSO basato su password per Internet Explorer o Chrome**.</span><span class="sxs-lookup"><span data-stu-id="533cc-191">The first time, you click an application tile for one of these applications, you are prompted to install the **Password SSO plug-in for Internet Explorer or Chrome**.</span></span> <span data-ttu-id="533cc-192">L'installazione potrebbe richiedere il riavvio del Web browser.</span><span class="sxs-lookup"><span data-stu-id="533cc-192">The installation might require you to restart your web browser.</span></span>  
<span data-ttu-id="533cc-193">Quando si torna nel pannello di accesso e si fa clic di nuovo sul riquadro dell'applicazione, l'accesso all'applicazione viene eseguito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="533cc-193">When you return to the access panel and click the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="533cc-194">Alcune applicazioni potrebbero richiedere di cambiare la password al primo accesso.</span><span class="sxs-lookup"><span data-stu-id="533cc-194">Some applications might require you to change your password on the first sign-in.</span></span> <span data-ttu-id="533cc-195">Se le credenziali sono cambiate nell'applicazione di destinazione di terze parti, è necessario aggiornare anche le credenziali archiviate in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="533cc-195">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="533cc-196">**Per aggiornare le credenziali:**</span><span class="sxs-lookup"><span data-stu-id="533cc-196">**To update credentials:**</span></span>

1. <span data-ttu-id="533cc-197">Selezionare l'icona nel riquadro dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="533cc-197">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="533cc-198">Selezionare **Aggiorna credenziali** per immettere di nuovo nome utente e password per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="533cc-198">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="533cc-199">Applicazione con soluzioni Single Sign-On esistenti</span><span class="sxs-lookup"><span data-stu-id="533cc-199">Application with existing SSO solutions</span></span>

<span data-ttu-id="533cc-200">Per configurare l'accesso SSO per un'applicazione, il portale di Azure fornisce una terza opzione, ovvero **Accesso Single Sign-On esistente**.</span><span class="sxs-lookup"><span data-stu-id="533cc-200">To configure SSO for an application, the Azure portal provides a third option called **Existing Single Sign-On**.</span></span> <span data-ttu-id="533cc-201">Questa opzione consente all'amministratore di creare un collegamento a un'applicazione e di inserirlo nel pannello di accesso per gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="533cc-201">This option enables your administrator to create a link to an application and place it on the access panel for selected users.</span></span>

<span data-ttu-id="533cc-202">Se, ad esempio, un'applicazione è configurata per l'autenticazione degli utenti tramite AD FS 2.0, l'amministratore può usare l'opzione **Accesso Single Sign-On esistente** per creare un collegamento nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="533cc-202">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the **Existing Single Sign-On** option to create a link to it on the access panel.</span></span> <span data-ttu-id="533cc-203">Quando si accede al collegamento, viene eseguita l'autenticazione tramite AD FS 2.0 o qualunque soluzione SSO fornita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="533cc-203">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="533cc-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="533cc-204">Next steps</span></span>

- <span data-ttu-id="533cc-205">Per visualizzare un elenco di tutti gli argomenti relativi alla gestione delle applicazioni, vedere [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md).</span><span class="sxs-lookup"><span data-stu-id="533cc-205">To see a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="533cc-206">Per informazioni su come integrare un'app SaaS in Azure AD, vedere l'[elenco di esercitazioni sull'integrazione di app SaaS](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="533cc-206">To learn how to integrate a SaaS app into Azure AD, see the [list of tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>
 
- <span data-ttu-id="533cc-207">Per altre informazioni sulla gestione di app con Azure AD, vedere l'[introduzione a Single Sign-On e alla gestione dell'accesso alle app con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="533cc-207">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>
 
- <span data-ttu-id="533cc-208">Per altre informazioni sul provisioning degli utenti, vedere [Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="533cc-208">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png

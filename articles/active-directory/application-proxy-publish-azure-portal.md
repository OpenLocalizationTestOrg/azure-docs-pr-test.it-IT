---
title: Pubblicare app con il proxy di applicazione di Azure AD | Documentazione Microsoft
description: Pubblicare applicazioni locali nel cloud con il proxy dell'applicazione di Azure AD nel portale di Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: e00a939f2b20ab8e0a2ddf0ff91e59db440213ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="f2ffe-103">Pubblicare applicazioni mediante il proxy di applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="f2ffe-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2ffe-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f2ffe-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="f2ffe-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="f2ffe-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="f2ffe-106">Il proxy dell'applicazione di Azure Active Directory (AD) consente di supportare lavoratori remoti pubblicando applicazioni locali in modo che siano accessibili tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="f2ffe-107">Tramite il portale di Azure è possibile pubblicare queste applicazioni per fornire un accesso remoto sicuro dall'esterno della rete.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-107">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="f2ffe-108">Questo articolo illustra tutti i passaggi per pubblicare un'app locale con il proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="f2ffe-109">Dopo aver completato questo articolo, gli utenti potranno accedere all'app in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-109">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="f2ffe-110">E sarà possibile configurare funzionalità extra per l'applicazione con accesso Single Sign-On, informazioni personalizzate e requisiti di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-110">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="f2ffe-111">Se non si ha familiarità con le funzionalità offerte dal proxy dell'applicazione, per altre informazioni vedere [Come fornire l'accesso remoto sicuro alle applicazioni locali](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f2ffe-111">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="f2ffe-112">Pubblicare un'applicazione locale per l'accesso remoto</span><span class="sxs-lookup"><span data-stu-id="f2ffe-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="f2ffe-113">Seguire questa procedura per pubblicare le app con il proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-113">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="f2ffe-114">Se non è ancora stato scaricato e configurato un connettore per l'organizzazione, passare ad [Attività iniziali del proxy di applicazione e installazione del connettore](active-directory-application-proxy-enable.md) in primo luogo e quindi pubblicare l'app.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-114">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="f2ffe-115">Se è la prima volta che si prova il proxy dell'applicazione, scegliere un'applicazione già configurata per l'autenticazione basata su password.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-115">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="f2ffe-116">Il proxy dell'applicazione supporta altri tipi di autenticazione, ma le app basate su password sono le più facili da configurare ed eseguire con rapidità.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-116">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="f2ffe-117">Accedere come amministratore al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f2ffe-117">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f2ffe-118">Selezionare **Azure Active Directory** > **Applicazioni aziendali** > **Nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Aggiungere un'applicazione aziendale](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="f2ffe-120">Selezionare **Tutte** quindi scegliere **Applicazione locale**.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Aggiungere una propria applicazione](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="f2ffe-122">Specificare le informazioni relative all'applicazione elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-122">Provide the following information about your application:</span></span>

   - <span data-ttu-id="f2ffe-123">**Nome**: il nome dell'applicazione che verrà visualizzato nel pannello di accesso e nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-123">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="f2ffe-124">**URL interno**: URL usato per accedere all'applicazione dall'interno della rete privata.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-124">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="f2ffe-125">È possibile indicare un percorso specifico nel server back-end per la pubblicazione, mentre il resto del server non è pubblicato.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="f2ffe-126">In questo modo, si possono pubblicare siti diversi nello stesso server come app differenti, assegnando a ognuno un nome e regole di accesso specifici.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-126">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="f2ffe-127">Se si pubblica un percorso, verificare che includa tutte le immagini, gli script e i fogli di stile necessari per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="f2ffe-128">Se l'app si trova in https://yourapp/app e usa immagini che si trovano in https://yourapp/media, si dovrà pubblicare come percorso https://yourapp/.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="f2ffe-129">Questo URL interno non deve necessariamente corrispondere alla pagina di destinazione visualizzata dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-129">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="f2ffe-130">Per altre informazioni, vedere [Impostare una home page personalizzata per le app pubblicate tramite il proxy applicazione di Azure AD](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="f2ffe-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="f2ffe-131">**URL esterno**: l'indirizzo immesso dagli utenti per accedere all'app dall'esterno della rete.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-131">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="f2ffe-132">Se non si desidera usare il dominio del Proxy di applicazione predefinito, trovare informazioni sui [domini personalizzati nel Proxy dell'applicazione di Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="f2ffe-132">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="f2ffe-133">**Metodo di autenticazione preliminare**: come il proxy dell'applicazione verifica gli utenti prima di concedere loro l'accesso all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-133">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="f2ffe-134">Azure Active Directory: il proxy di applicazione reindirizza gli utenti in modo che eseguano l'accesso con Azure AD, che ne autentica le autorizzazioni per la directory e l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-134">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="f2ffe-135">È consigliabile lasciare questa opzione come impostazione predefinita, in modo da poter usufruire delle funzionalità di sicurezza di Azure AD come l'accesso condizionale e l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-135">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="f2ffe-136">Passthrough: gli utenti non devono eseguire l'autenticazione ad Azure Active Directory per accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-136">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="f2ffe-137">È comunque possibile configurare i requisiti di autenticazione sul back-end.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-137">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="f2ffe-138">**Gruppo di connettori**: i connettori elaborano l'accesso remoto all'applicazione, mentre i gruppi di connettori aiutano a organizzare connettori e app in base all'area geografica, alla rete o allo scopo.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-138">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="f2ffe-139">Se ancora non si dispone di tutti i gruppi connettore creati, l'app viene assegnata a **Impostazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-139">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

   ![Configurare l'applicazione](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="f2ffe-141">Se necessario, configurare le impostazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="f2ffe-142">Per la maggior parte delle applicazioni, è consigliabile mantenere queste impostazioni nei rispettivi stati predefiniti.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="f2ffe-143">**Timeout applicazione back-end**: impostare questo valore su **Lungo** solo se l'applicazione è lenta nell'autenticazione e nella connessione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-143">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="f2ffe-144">**Convertire l'URL nelle intestazioni**: mantenere questo valore su **Sì**, a meno che l'applicazione non richieda l'intestazione host originale nella richiesta di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="f2ffe-145">**Convertire gli URL nel corpo dell'applicazione**: mantenere questo valore su **No**, a meno che non si sia in possesso di collegamenti HTML hardcoded ad altre applicazioni locali e non si usino domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="f2ffe-146">Per altre informazioni, vedere [Reindirizzare i collegamenti hardcoded per le app pubblicate con il proxy di app di Azure AD](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="f2ffe-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Configurare l'applicazione](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="f2ffe-148">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="f2ffe-149">Aggiungere un utente di test</span><span class="sxs-lookup"><span data-stu-id="f2ffe-149">Add a test user</span></span> 

<span data-ttu-id="f2ffe-150">Per verificare che l'app sia stata pubblicata correttamente, aggiungere un account utente di prova.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-150">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="f2ffe-151">Verificare che questo account disponga già delle autorizzazioni per accedere all'app dall'interno della rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-151">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="f2ffe-152">Nel pannello di avvio rapido selezionare **Assign a user for testing** (Assegna utente per il test).</span><span class="sxs-lookup"><span data-stu-id="f2ffe-152">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![Assegna utente per il test](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="f2ffe-154">Nel pannello Utenti e gruppi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-154">On the Users and groups blade, select **Add**.</span></span>

  ![Aggiungere un utente o gruppo](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="f2ffe-156">Nel pannello Aggiungi assegnazione selezionare **Utenti e gruppi**, quindi scegliere l'account da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-156">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="f2ffe-157">Selezionare **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="f2ffe-158">Testare l'app pubblicata</span><span class="sxs-lookup"><span data-stu-id="f2ffe-158">Test your published app</span></span>

<span data-ttu-id="f2ffe-159">Nel browser passare all'URL esterno configurato durante la fase di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-159">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="f2ffe-160">Dovrebbe essere visualizzata la schermata iniziale in cui accedere con l'account test configurato.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-160">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![Testare l'app pubblicata](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="f2ffe-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2ffe-162">Next steps</span></span>
- <span data-ttu-id="f2ffe-163">[Scaricare connettori](active-directory-application-proxy-enable.md) e [creare gruppi di connettori](active-directory-application-proxy-connectors-azure-portal.md) per pubblicare applicazioni in reti e posizioni separate.</span><span class="sxs-lookup"><span data-stu-id="f2ffe-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="f2ffe-164">[Configurare l'accesso Single Sign-On](application-proxy-sso-azure-portal.md) per l'app appena pubblicata</span><span class="sxs-lookup"><span data-stu-id="f2ffe-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>

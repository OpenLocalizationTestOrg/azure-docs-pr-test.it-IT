---
title: App aaaPublish con Proxy dell'applicazione Azure AD | Documenti Microsoft
description: Pubblicare cloud toohello di applicazioni on-premise con Proxy dell'applicazione Azure Active Directory nel portale di Azure hello.
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
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="1ef05-103">Pubblicare applicazioni mediante il proxy di applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="1ef05-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ef05-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1ef05-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="1ef05-105">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="1ef05-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="1ef05-106">Proxy dell'applicazione Azure Active Directory (AD) consente di supportare gli utenti remoti mediante la pubblicazione toobe applicazioni locale accessibili tramite hello internet.</span><span class="sxs-lookup"><span data-stu-id="1ef05-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="1ef05-107">È possibile pubblicare queste applicazioni tramite hello tooprovide portale Azure l'accesso remoto sicuro dall'esterno della rete.</span><span class="sxs-lookup"><span data-stu-id="1ef05-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="1ef05-108">In questo articolo illustra hello passaggi toopublish un'app locale con Proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ef05-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="1ef05-109">Dopo aver completato questo articolo, gli utenti verranno essere in grado di tooaccess l'app in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="1ef05-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="1ef05-110">E sarà pronto tooconfigure caratteristiche aggiuntive per un'applicazione hello come single sign-on, informazioni personalizzate e requisiti di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1ef05-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="1ef05-111">Se si tooApplication nuovo Proxy, ulteriori informazioni su questa funzionalità con articolo hello [come tooprovide proteggere l'accesso remoto applicazioni locali tooon](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1ef05-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="1ef05-112">Pubblicare un'applicazione locale per l'accesso remoto</span><span class="sxs-lookup"><span data-stu-id="1ef05-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="1ef05-113">Seguire questi toopublish passaggi le applicazioni con Proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ef05-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="1ef05-114">Se ancora stato già scaricato e configurato un connettore per l'organizzazione, andare troppo[iniziare con Proxy dell'applicazione e installare il connettore hello](active-directory-application-proxy-enable.md) primo e quindi pubblicare l'app.</span><span class="sxs-lookup"><span data-stu-id="1ef05-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="1ef05-115">Se si sta testando il Proxy dell'applicazione per hello prima volta, scegliere un'applicazione che è configurata per l'autenticazione basata su password.</span><span class="sxs-lookup"><span data-stu-id="1ef05-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="1ef05-116">Proxy dell'applicazione supporta altri tipi di autenticazione, ma le app basate su password sono hello tooget più semplice backup ed eseguire rapidamente.</span><span class="sxs-lookup"><span data-stu-id="1ef05-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="1ef05-117">Accedere come amministratore in hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1ef05-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ef05-118">Selezionare **Azure Active Directory** > **Applicazioni aziendali** > **Nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="1ef05-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Aggiungere un'applicazione aziendale](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="1ef05-120">Selezionare **Tutte** quindi scegliere **Applicazione locale**.</span><span class="sxs-lookup"><span data-stu-id="1ef05-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Aggiungere una propria applicazione](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="1ef05-122">Fornire le seguenti informazioni sull'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="1ef05-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="1ef05-123">**Nome**: nome hello dell'applicazione hello che verrà visualizzato nel Pannello di accesso hello e nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1ef05-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="1ef05-124">**URL interno**: hello URL utilizzato da un'applicazione hello tooaccess all'interno della rete privata.</span><span class="sxs-lookup"><span data-stu-id="1ef05-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="1ef05-125">È possibile fornire un percorso specifico in hello toopublish di server back-end, mentre il resto di hello del server hello è pubblicato.</span><span class="sxs-lookup"><span data-stu-id="1ef05-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="1ef05-126">In questo modo, è possibile pubblicare i siti diversi hello nello stesso server applicazioni diversi e assegnare a ognuno di essi proprie regole di accesso e nome.</span><span class="sxs-lookup"><span data-stu-id="1ef05-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="1ef05-127">Se si pubblica un percorso, assicurarsi che includa tutte le immagini necessarie hello, script e fogli di stile per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ef05-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="1ef05-128">Ad esempio, se l'app in https://yourapp/app e Usa le immagini che si trova in https://yourapp/media, è necessario pubblicare https://yourapp/ come percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="1ef05-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="1ef05-129">Pagina di destinazione hello toobe che agli utenti di vedere non dispone di questo URL interno.</span><span class="sxs-lookup"><span data-stu-id="1ef05-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="1ef05-130">Per altre informazioni, vedere [Impostare una home page personalizzata per le app pubblicate tramite il proxy applicazione di Azure AD](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="1ef05-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="1ef05-131">**URL esterno**: hello indirizzo agli utenti verranno inviata tooin ordine tooaccess app hello dall'esterno della rete.</span><span class="sxs-lookup"><span data-stu-id="1ef05-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="1ef05-132">Se non si desidera dominio Proxy di applicazione predefinito di hello toouse, conoscenza [domini personalizzati in Azure AD applicazione Proxy](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="1ef05-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="1ef05-133">**Pre-autenticazione**: come Proxy di applicazione verifica gli utenti prima di concedere loro accesso tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ef05-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="1ef05-134">Azure Active Directory: Proxy applicazione reindirizza toosign gli utenti con Azure AD, che autentica le autorizzazioni per directory hello e applicazione.</span><span class="sxs-lookup"><span data-stu-id="1ef05-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="1ef05-135">È consigliabile lasciare questa opzione come impostazione predefinita di hello, in modo che è possibile usufruire delle funzionalità di sicurezza di Azure AD come accesso condizionale e multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="1ef05-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="1ef05-136">Pass-through: Gli utenti non hanno tooauthenticate rispetto a un'applicazione hello tooaccess Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ef05-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="1ef05-137">È comunque possibile impostare i requisiti di autenticazione nel back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1ef05-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="1ef05-138">**Gruppo di connettori**: un'applicazione tooyour connettori processo hello accesso remoto e i gruppi di connettori consentono di organizzare i connettori e le App per area, rete o scopo.</span><span class="sxs-lookup"><span data-stu-id="1ef05-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="1ef05-139">Se non si dispone di tutti i gruppi connettore ancora creati, l'app viene assegnato troppo**predefinito**.</span><span class="sxs-lookup"><span data-stu-id="1ef05-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Configurare l'applicazione](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="1ef05-141">Se necessario, configurare le impostazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="1ef05-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="1ef05-142">Per la maggior parte delle applicazioni, è consigliabile mantenere queste impostazioni nei rispettivi stati predefiniti.</span><span class="sxs-lookup"><span data-stu-id="1ef05-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="1ef05-143">**Timeout applicazione back-end**: impostare questo valore troppo**lungo** solo se l'applicazione è lento tooauthenticate e connettersi.</span><span class="sxs-lookup"><span data-stu-id="1ef05-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="1ef05-144">**Convertire gli URL nelle intestazioni**: mantenere il valore come **Sì** , a meno che l'applicazione necessaria l'intestazione dell'host nella richiesta di autenticazione hello originale hello.</span><span class="sxs-lookup"><span data-stu-id="1ef05-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="1ef05-145">**Convertire gli URL nel corpo di applicazione**: mantenere il valore come **n** a meno che non si dispone di applicazioni di on-premise tooother collegamenti HTML hardcoded e non usare i domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1ef05-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="1ef05-146">Per altre informazioni, vedere [Reindirizzare i collegamenti hardcoded per le app pubblicate con il proxy di app di Azure AD](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="1ef05-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Configurare l'applicazione](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="1ef05-148">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1ef05-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="1ef05-149">Aggiungere un utente di test</span><span class="sxs-lookup"><span data-stu-id="1ef05-149">Add a test user</span></span> 

<span data-ttu-id="1ef05-150">tootest che l'app è stato pubblicato correttamente, aggiungere un account utente di prova.</span><span class="sxs-lookup"><span data-stu-id="1ef05-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="1ef05-151">Verificare che l'account disponga già di autorizzazioni tooaccess hello dell'applicazione all'interno di hello alla rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="1ef05-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="1ef05-152">Nel pannello avvio rapido hello selezionare **assegnare un utente per il testing**.</span><span class="sxs-lookup"><span data-stu-id="1ef05-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Assegna utente per il test](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="1ef05-154">Gli utenti di hello e blade gruppi, selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1ef05-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Aggiungere un utente o gruppo](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="1ef05-156">Nel Pannello di assegnazione di hello Aggiungi, selezionare **utenti e gruppi** scegliere account hello da tooadd.</span><span class="sxs-lookup"><span data-stu-id="1ef05-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="1ef05-157">Selezionare **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="1ef05-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="1ef05-158">Testare l'app pubblicata</span><span class="sxs-lookup"><span data-stu-id="1ef05-158">Test your published app</span></span>

<span data-ttu-id="1ef05-159">Nel browser passare toohello URL esterno configurato hello durante la fase di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="1ef05-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="1ef05-160">Dovrebbe essere schermata start hello ed essere in grado di toosign con account di prova hello impostati.</span><span class="sxs-lookup"><span data-stu-id="1ef05-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Testare l'app pubblicata](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="1ef05-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ef05-162">Next steps</span></span>
- <span data-ttu-id="1ef05-163">[Scaricare i connettori](active-directory-application-proxy-enable.md) e [creare gruppi di connettori](active-directory-application-proxy-connectors-azure-portal.md) toopublish applicazioni su reti separate e percorsi.</span><span class="sxs-lookup"><span data-stu-id="1ef05-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="1ef05-164">[Configurare l'accesso Single Sign-On](application-proxy-sso-azure-portal.md) per l'app appena pubblicata</span><span class="sxs-lookup"><span data-stu-id="1ef05-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>

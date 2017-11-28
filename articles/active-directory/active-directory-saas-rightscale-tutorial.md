---
title: 'Esercitazione: Integrazione di Azure Active Directory con Rightscale | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Rightscale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="5d7be-103">Esercitazione: Integrazione di Azure Active Directory con Rightscale</span><span class="sxs-lookup"><span data-stu-id="5d7be-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="5d7be-104">In questa esercitazione, è illustrato come toointegrate Rightscale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d7be-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d7be-105">Integrazione Rightscale con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5d7be-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d7be-106">È possibile controllare in Azure AD che ha accesso tooRightscale</span><span class="sxs-lookup"><span data-stu-id="5d7be-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="5d7be-107">È possibile abilitare l'utenti tooautomatically get connesso tooRightscale (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d7be-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d7be-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5d7be-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5d7be-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d7be-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d7be-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5d7be-110">Prerequisites</span></span>

<span data-ttu-id="5d7be-111">integrazione di Azure AD con Rightscale tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5d7be-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="5d7be-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d7be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d7be-113">Sottoscrizione di Rightscale abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5d7be-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d7be-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5d7be-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d7be-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5d7be-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d7be-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5d7be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d7be-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d7be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d7be-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5d7be-118">Scenario description</span></span>
<span data-ttu-id="5d7be-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5d7be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d7be-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5d7be-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d7be-121">Aggiunta di Rightscale dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5d7be-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="5d7be-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d7be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="5d7be-123">Aggiunta di Rightscale dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5d7be-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="5d7be-124">integrazione hello tooconfigure di Rightscale in Azure AD, è necessario tooadd Rightscale dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5d7be-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d7be-125">**tooadd Rightscale dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d7be-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d7be-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5d7be-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d7be-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d7be-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5d7be-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5d7be-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5d7be-133">Nella casella di ricerca hello, digitare **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-133">In hello search box, type **Rightscale**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="5d7be-135">Nel riquadro dei risultati hello, selezionare **Rightscale**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5d7be-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d7be-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d7be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d7be-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Rightscale in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5d7be-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d7be-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Rightscale è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d7be-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="5d7be-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Rightscale deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5d7be-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="5d7be-141">In Rightscale, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5d7be-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d7be-142">tooconfigure e prova AD Azure single sign-on con Rightscale, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5d7be-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d7be-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5d7be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d7be-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d7be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d7be-145">**[Creazione di un utente test Rightscale](#creating-a-rightscale-test-user)**  -toohave un equivalente di Britta Simon in Rightscale che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5d7be-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d7be-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5d7be-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d7be-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5d7be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d7be-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d7be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d7be-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Rightscale.</span><span class="sxs-lookup"><span data-stu-id="5d7be-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="5d7be-150">**Azure AD tooconfigure single sign-on con Rightscale, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d7be-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d7be-151">Nel portale di Azure su hello hello **Rightscale** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5d7be-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5d7be-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="5d7be-155">In hello **Rightscale dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP** non si dispone tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7be-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="5d7be-157">In hello **Rightscale dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5d7be-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="5d7be-159">a.</span><span class="sxs-lookup"><span data-stu-id="5d7be-159">a.</span></span> <span data-ttu-id="5d7be-160">Fare clic su hello **Mostra URL impostazioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="5d7be-161">b.</span><span class="sxs-lookup"><span data-stu-id="5d7be-161">b.</span></span> <span data-ttu-id="5d7be-162">In hello **URL di accesso** casella di testo, digitare l'URL hello:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="5d7be-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="5d7be-163">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5d7be-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="5d7be-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5d7be-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5d7be-167">In hello **Rightscale configurazione** fare clic su **configurare Rightscale** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5d7be-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5d7be-168">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5d7be-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="5d7be-169">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="5d7be-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="5d7be-170">tooget SSO configurato per l'applicazione, è necessario toosign-on tooyour RightScale tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5d7be-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="5d7be-171">a.</span><span class="sxs-lookup"><span data-stu-id="5d7be-171">a.</span></span> <span data-ttu-id="5d7be-172">Scegliere hello hello menu in alto hello **impostazioni** e selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="5d7be-174">b.</span><span class="sxs-lookup"><span data-stu-id="5d7be-174">b.</span></span> <span data-ttu-id="5d7be-175">Fare clic su hello "**nuova**" pulsante tooadd **del provider di identità SAML**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="5d7be-177">c.</span><span class="sxs-lookup"><span data-stu-id="5d7be-177">c.</span></span> <span data-ttu-id="5d7be-178">Nella casella di testo hello di **nome visualizzato**, immettere il nome della società.</span><span class="sxs-lookup"><span data-stu-id="5d7be-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="5d7be-180">d.</span><span class="sxs-lookup"><span data-stu-id="5d7be-180">d.</span></span> <span data-ttu-id="5d7be-181">Selezionare **SSO avviato da consentire RightScale utilizzando un hint di individuazione** e input del **nome di dominio** in hello sotto casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5d7be-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="5d7be-183">e.</span><span class="sxs-lookup"><span data-stu-id="5d7be-183">e.</span></span> <span data-ttu-id="5d7be-184">Incollare il valore di hello di **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure in **SAML SSO Endpoint** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="5d7be-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="5d7be-186">f.</span><span class="sxs-lookup"><span data-stu-id="5d7be-186">f.</span></span> <span data-ttu-id="5d7be-187">Incollare il valore di hello di **ID entità SAML** che è stato copiato dal portale di Azure in **EntityID SAML** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="5d7be-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="5d7be-189">g.</span><span class="sxs-lookup"><span data-stu-id="5d7be-189">g.</span></span> <span data-ttu-id="5d7be-190">Fare clic su **Browser** pulsante tooupload hello certificato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7be-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="5d7be-192">h.</span><span class="sxs-lookup"><span data-stu-id="5d7be-192">h.</span></span> <span data-ttu-id="5d7be-193">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="5d7be-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5d7be-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d7be-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5d7be-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d7be-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d7be-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d7be-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d7be-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d7be-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d7be-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5d7be-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d7be-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d7be-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5d7be-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d7be-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d7be-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5d7be-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d7be-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5d7be-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d7be-209">a.</span><span class="sxs-lookup"><span data-stu-id="5d7be-209">a.</span></span> <span data-ttu-id="5d7be-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d7be-211">b.</span><span class="sxs-lookup"><span data-stu-id="5d7be-211">b.</span></span> <span data-ttu-id="5d7be-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d7be-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d7be-213">c.</span><span class="sxs-lookup"><span data-stu-id="5d7be-213">c.</span></span> <span data-ttu-id="5d7be-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5d7be-215">d.</span><span class="sxs-lookup"><span data-stu-id="5d7be-215">d.</span></span> <span data-ttu-id="5d7be-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="5d7be-217">Creazione di un utente di test di Rightscale</span><span class="sxs-lookup"><span data-stu-id="5d7be-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="5d7be-218">In questa sezione viene creato un utente chiamato Britta Simon in RightScale.</span><span class="sxs-lookup"><span data-stu-id="5d7be-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="5d7be-219">Lavorare con [team di supporto Rightscale Client](mailto:support@rightscale.com) utenti hello tooadd nella piattaforma RightScale hello.</span><span class="sxs-lookup"><span data-stu-id="5d7be-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5d7be-220">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d7be-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5d7be-221">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRightscale.</span><span class="sxs-lookup"><span data-stu-id="5d7be-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5d7be-223">**tooassign Britta Simon tooRightscale, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d7be-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d7be-224">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5d7be-226">Nell'elenco di applicazioni hello, selezionare **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-226">In hello applications list, select **Rightscale**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="5d7be-228">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5d7be-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-230">Click **Add** button.</span></span> <span data-ttu-id="5d7be-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5d7be-233">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5d7be-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d7be-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d7be-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5d7be-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d7be-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5d7be-236">Testing single sign-on</span></span>

<span data-ttu-id="5d7be-237">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5d7be-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5d7be-238">Quando si fa clic su riquadro RightScale hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour RightScale applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d7be-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d7be-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5d7be-239">Additional resources</span></span>

* [<span data-ttu-id="5d7be-240">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d7be-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d7be-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d7be-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png


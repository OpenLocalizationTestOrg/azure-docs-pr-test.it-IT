---
title: 'Esercitazione: Integrazione di Azure Active Directory con LiquidFiles | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e LiquidFiles.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="3e69e-103">Esercitazione: Integrazione di Azure Active Directory con LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="3e69e-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="3e69e-104">In questa esercitazione, è illustrato come toointegrate LiquidFiles con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e69e-104">In this tutorial, you learn how toointegrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e69e-105">Integrazione LiquidFiles con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3e69e-105">Integrating LiquidFiles with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e69e-106">È possibile controllare in Azure AD che ha accesso tooLiquidFiles</span><span class="sxs-lookup"><span data-stu-id="3e69e-106">You can control in Azure AD who has access tooLiquidFiles</span></span>
- <span data-ttu-id="3e69e-107">È possibile abilitare l'utenti tooautomatically get connesso tooLiquidFiles (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e69e-107">You can enable your users tooautomatically get signed-on tooLiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e69e-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3e69e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3e69e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e69e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e69e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3e69e-110">Prerequisites</span></span>

<span data-ttu-id="3e69e-111">integrazione di Azure AD con LiquidFiles tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3e69e-111">tooconfigure Azure AD integration with LiquidFiles, you need hello following items:</span></span>

- <span data-ttu-id="3e69e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e69e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e69e-113">Sottoscrizione di LiquidFiles abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e69e-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e69e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="3e69e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e69e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="3e69e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e69e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3e69e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e69e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e69e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e69e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3e69e-118">Scenario description</span></span>
<span data-ttu-id="3e69e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3e69e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e69e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="3e69e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e69e-121">Aggiunta di LiquidFiles dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e69e-121">Adding LiquidFiles from hello gallery</span></span>
2. <span data-ttu-id="3e69e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e69e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-hello-gallery"></a><span data-ttu-id="3e69e-123">Aggiunta di LiquidFiles dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e69e-123">Adding LiquidFiles from hello gallery</span></span>
<span data-ttu-id="3e69e-124">integrazione hello tooconfigure di LiquidFiles in Azure AD, è necessario tooadd LiquidFiles dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3e69e-124">tooconfigure hello integration of LiquidFiles into Azure AD, you need tooadd LiquidFiles from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e69e-125">**tooadd LiquidFiles dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e69e-125">**tooadd LiquidFiles from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e69e-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3e69e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e69e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e69e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3e69e-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3e69e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3e69e-133">Nella casella di ricerca hello, digitare **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-133">In hello search box, type **LiquidFiles**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="3e69e-135">Nel riquadro dei risultati hello, selezionare **LiquidFiles**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e69e-135">In hello results panel, select **LiquidFiles**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e69e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e69e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e69e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LiquidFiles usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3e69e-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e69e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LiquidFiles è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e69e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LiquidFiles is tooa user in Azure AD.</span></span> <span data-ttu-id="3e69e-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in LiquidFiles deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="3e69e-140">In other words, a link relationship between an Azure AD user and hello related user in LiquidFiles needs toobe established.</span></span>

<span data-ttu-id="3e69e-141">In LiquidFiles, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="3e69e-141">In LiquidFiles, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3e69e-142">tooconfigure e prova AD Azure single sign-on con LiquidFiles, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="3e69e-142">tooconfigure and test Azure AD single sign-on with LiquidFiles, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e69e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3e69e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e69e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e69e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e69e-145">**[Creazione di un utente test LiquidFiles](#creating-a-liquidfiles-test-user)**  -toohave un equivalente di Britta Simon in LiquidFiles che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3e69e-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - toohave a counterpart of Britta Simon in LiquidFiles that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e69e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e69e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e69e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e69e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e69e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e69e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e69e-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="3e69e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="3e69e-150">**Azure AD tooconfigure single sign-on con LiquidFiles, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e69e-150">**tooconfigure Azure AD single sign-on with LiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e69e-151">Nel portale di Azure su hello hello **LiquidFiles** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-151">In hello Azure portal, on hello **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3e69e-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e69e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="3e69e-155">In hello **LiquidFiles dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e69e-155">On hello **LiquidFiles Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="3e69e-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e69e-157">a.</span></span> <span data-ttu-id="3e69e-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="3e69e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="3e69e-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e69e-159">b.</span></span> <span data-ttu-id="3e69e-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="3e69e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="3e69e-161">c.</span><span class="sxs-lookup"><span data-stu-id="3e69e-161">c.</span></span> <span data-ttu-id="3e69e-162">b.</span><span class="sxs-lookup"><span data-stu-id="3e69e-162">b.</span></span> <span data-ttu-id="3e69e-163">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="3e69e-163">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e69e-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="3e69e-164">These values are not real.</span></span> <span data-ttu-id="3e69e-165">Aggiornamento di questi valori con hello URL di accesso effettiva, identificatore e l'URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="3e69e-165">Update these values with hello actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="3e69e-166">Contatto [team di supporto LiquidFiles Client](https://www.liquidfiles.com/support.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="3e69e-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="3e69e-167">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="3e69e-167">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="3e69e-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3e69e-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e69e-171">In hello **LiquidFiles configurazione** fare clic su **configurare LiquidFiles** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="3e69e-171">On hello **LiquidFiles Configuration** section, click **Configure LiquidFiles** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3e69e-172">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="3e69e-172">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="3e69e-174">Sito dell'azienda LiquidFiles tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3e69e-174">Sign-on tooyour LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="3e69e-175">Fare clic su **Single Sign-On** in hello **amministrazione > configurazione** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="3e69e-175">Click **Single Sign-On** in hello **Admin > Configuration** from hello menu.</span></span>

9. <span data-ttu-id="3e69e-176">In hello **configurazione Single Sign-On** hello seguendo i passaggi da eseguire</span><span class="sxs-lookup"><span data-stu-id="3e69e-176">On hello **Single Sign-On Configuration** page, perform hello following steps</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="3e69e-178">a.</span><span class="sxs-lookup"><span data-stu-id="3e69e-178">a.</span></span> <span data-ttu-id="3e69e-179">In **Single Sign On Method** (Metodo Single Sign-On) selezionare **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="3e69e-180">b.</span><span class="sxs-lookup"><span data-stu-id="3e69e-180">b.</span></span> <span data-ttu-id="3e69e-181">In hello **IDP Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e69e-181">In hello **IDP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3e69e-182">c.</span><span class="sxs-lookup"><span data-stu-id="3e69e-182">c.</span></span> <span data-ttu-id="3e69e-183">In hello **IDP Logout URL** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e69e-183">In hello **IDP Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3e69e-184">d.</span><span class="sxs-lookup"><span data-stu-id="3e69e-184">d.</span></span> <span data-ttu-id="3e69e-185">In hello **IDP Cert Fingerprint** casella di testo, incollare hello **identificazione personale** valore a cui è stato copiato dal portale di Azure...</span><span class="sxs-lookup"><span data-stu-id="3e69e-185">In hello **IDP Cert Fingerprint** textbox, paste hello **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="3e69e-186">e.</span><span class="sxs-lookup"><span data-stu-id="3e69e-186">e.</span></span> <span data-ttu-id="3e69e-187">Nella casella di testo Name Identifier Format hello, digitare il valore di hello **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-187">In hello Name Identifier Format textbox, type hello value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="3e69e-188">f.</span><span class="sxs-lookup"><span data-stu-id="3e69e-188">f.</span></span> <span data-ttu-id="3e69e-189">Nella casella di testo il contesto di autenticazione hello, digitare il valore di hello **urn: oasis: nomi: tc: SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-189">In hello Authn Context textbox, type hello value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="3e69e-190">g.</span><span class="sxs-lookup"><span data-stu-id="3e69e-190">g.</span></span> <span data-ttu-id="3e69e-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="3e69e-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="3e69e-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e69e-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3e69e-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e69e-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e69e-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e69e-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e69e-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e69e-196">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3e69e-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3e69e-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e69e-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e69e-199">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3e69e-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e69e-201">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e69e-203">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="3e69e-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e69e-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e69e-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e69e-207">a.</span><span class="sxs-lookup"><span data-stu-id="3e69e-207">a.</span></span> <span data-ttu-id="3e69e-208">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e69e-209">b.</span><span class="sxs-lookup"><span data-stu-id="3e69e-209">b.</span></span> <span data-ttu-id="3e69e-210">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e69e-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e69e-211">c.</span><span class="sxs-lookup"><span data-stu-id="3e69e-211">c.</span></span> <span data-ttu-id="3e69e-212">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3e69e-213">d.</span><span class="sxs-lookup"><span data-stu-id="3e69e-213">d.</span></span> <span data-ttu-id="3e69e-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="3e69e-215">Creazione di un utente test di LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="3e69e-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="3e69e-216">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in LiquidFiles toocreate.</span><span class="sxs-lookup"><span data-stu-id="3e69e-216">hello objective of this section is toocreate a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="3e69e-217">Funziona con i tooget di amministratore di server LiquidFiles manualmente aggiunto come utente prima di accedere tooyour LiquidFiles applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e69e-217">Work with your LiquidFiles server administrator tooget yourself added as a user before logging in tooyour LiquidFiles application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3e69e-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e69e-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3e69e-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="3e69e-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLiquidFiles.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3e69e-221">**tooassign Britta Simon tooLiquidFiles, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e69e-221">**tooassign Britta Simon tooLiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e69e-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3e69e-224">Nell'elenco di applicazioni hello, selezionare **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-224">In hello applications list, select **LiquidFiles**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="3e69e-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3e69e-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-228">Click **Add** button.</span></span> <span data-ttu-id="3e69e-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3e69e-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3e69e-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e69e-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e69e-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e69e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e69e-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e69e-234">Testing single sign-on</span></span>

<span data-ttu-id="3e69e-235">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3e69e-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3e69e-236">Quando si fa clic hello LiquidFiles riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour LiquidFiles applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e69e-236">When you click hello LiquidFiles tile in hello Access Panel, you should get automatically signed-on tooyour LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e69e-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3e69e-237">Additional resources</span></span>

* [<span data-ttu-id="3e69e-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e69e-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e69e-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e69e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png


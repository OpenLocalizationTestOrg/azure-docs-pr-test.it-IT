---
title: 'Esercitazione: Integrazione di Azure Active Directory con ITRP | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ITRP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="2d068-103">Esercitazione: Integrazione di Azure Active Directory con ITRP</span><span class="sxs-lookup"><span data-stu-id="2d068-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="2d068-104">In questa esercitazione, è illustrato come toointegrate ITRP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d068-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d068-105">Integrazione di ITRP con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2d068-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d068-106">È possibile controllare in Azure AD che ha accesso tooITRP</span><span class="sxs-lookup"><span data-stu-id="2d068-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="2d068-107">È possibile abilitare l'utenti tooautomatically get connesso tooITRP (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d068-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d068-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2d068-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2d068-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d068-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d068-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2d068-110">Prerequisites</span></span>

<span data-ttu-id="2d068-111">integrazione di Azure AD con ITRP tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="2d068-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="2d068-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d068-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d068-113">Sottoscrizione di ITRP abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2d068-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d068-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2d068-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d068-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="2d068-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d068-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2d068-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d068-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d068-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d068-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2d068-118">Scenario description</span></span>
<span data-ttu-id="2d068-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2d068-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d068-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="2d068-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d068-121">Aggiunta di ITRP dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2d068-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="2d068-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d068-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="2d068-123">Aggiunta di ITRP dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2d068-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="2d068-124">integrazione hello tooconfigure di ITRP in tooAzure Active Directory, è necessario tooadd ITRP dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2d068-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d068-125">**tooadd ITRP dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d068-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d068-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2d068-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d068-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2d068-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2d068-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d068-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2d068-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2d068-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2d068-133">Nella casella di ricerca hello, digitare **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="2d068-133">In hello search box, type **ITRP**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="2d068-135">Nel riquadro dei risultati hello, selezionare **ITRP**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2d068-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d068-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d068-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2d068-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ITRP usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2d068-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2d068-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ITRP è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d068-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="2d068-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ITRP richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="2d068-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="2d068-141">In ITRP, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="2d068-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2d068-142">tooconfigure e test Azure single sign-on AD con ITRP, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="2d068-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d068-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2d068-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d068-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d068-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d068-145">**[Creazione di un ITRP utente test](#creating-an-itrp-test-user)**  -toohave un equivalente di Britta Simon in ITRP che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2d068-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d068-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d068-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d068-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2d068-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d068-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d068-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d068-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ITRP.</span><span class="sxs-lookup"><span data-stu-id="2d068-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="2d068-150">**Azure AD tooconfigure single sign-on con ITRP, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d068-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d068-151">Nel portale di Azure su hello hello **ITRP** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2d068-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2d068-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d068-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="2d068-155">In hello **ITRP dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d068-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="2d068-157">a.</span><span class="sxs-lookup"><span data-stu-id="2d068-157">a.</span></span> <span data-ttu-id="2d068-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="2d068-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="2d068-159">b.</span><span class="sxs-lookup"><span data-stu-id="2d068-159">b.</span></span> <span data-ttu-id="2d068-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="2d068-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d068-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="2d068-161">These values are not real.</span></span> <span data-ttu-id="2d068-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="2d068-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2d068-163">Contatto [team di supporto Client di ITRP](https://www.itrp.com/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="2d068-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="2d068-164">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="2d068-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="2d068-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2d068-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2d068-168">In hello **ITRP configurazione** fare clic su **configurare ITRP** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="2d068-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2d068-169">Hello copia **SAML Single Sign-On Service URL e Sign-Out URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="2d068-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="2d068-171">In una finestra del web browser, accedere come amministratore nel sito della società ITRP di tooyour.</span><span class="sxs-lookup"><span data-stu-id="2d068-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="2d068-172">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d068-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="2d068-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="2d068-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="2d068-174">Nel riquadro di spostamento a sinistra di hello, selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2d068-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="2d068-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2d068-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="2d068-176">Nella sezione di configurazione di Single Sign-On hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d068-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d068-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2d068-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="2d068-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2d068-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="2d068-179">a.</span><span class="sxs-lookup"><span data-stu-id="2d068-179">a.</span></span> <span data-ttu-id="2d068-180">Fare clic su **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="2d068-180">Click **Enable**.</span></span>

    <span data-ttu-id="2d068-181">b.</span><span class="sxs-lookup"><span data-stu-id="2d068-181">b.</span></span> <span data-ttu-id="2d068-182">In **Log Out URL remoto** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d068-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2d068-183">c.</span><span class="sxs-lookup"><span data-stu-id="2d068-183">c.</span></span> <span data-ttu-id="2d068-184">In **URL SSO SAML** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d068-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2d068-185">d.In **Certificate Fingerprint** casella di testo, incollare hello **identificazione personale** valore del certificato, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d068-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="2d068-186">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2d068-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2d068-187">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="2d068-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2d068-188">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="2d068-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2d068-189">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d068-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d068-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d068-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d068-191">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2d068-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2d068-193">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d068-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d068-194">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2d068-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d068-196">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="2d068-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d068-198">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="2d068-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d068-200">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d068-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d068-202">a.</span><span class="sxs-lookup"><span data-stu-id="2d068-202">a.</span></span> <span data-ttu-id="2d068-203">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d068-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d068-204">b.</span><span class="sxs-lookup"><span data-stu-id="2d068-204">b.</span></span> <span data-ttu-id="2d068-205">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d068-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d068-206">c.</span><span class="sxs-lookup"><span data-stu-id="2d068-206">c.</span></span> <span data-ttu-id="2d068-207">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="2d068-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2d068-208">d.</span><span class="sxs-lookup"><span data-stu-id="2d068-208">d.</span></span> <span data-ttu-id="2d068-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2d068-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="2d068-210">Creazione di un utente di test di ITRP</span><span class="sxs-lookup"><span data-stu-id="2d068-210">Creating an ITRP test user</span></span>

<span data-ttu-id="2d068-211">toolog agli utenti di Azure AD tooenable in tooITRP, è necessario eseguirne il provisioning in tooITRP.</span><span class="sxs-lookup"><span data-stu-id="2d068-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="2d068-212">Nel caso di hello di ITRP, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="2d068-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="2d068-213">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d068-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d068-214">Accedi tooyour **ITRP** tenant.</span><span class="sxs-lookup"><span data-stu-id="2d068-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="2d068-215">Nella barra degli strumenti hello in primo piano hello, fare clic su **record**.</span><span class="sxs-lookup"><span data-stu-id="2d068-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="2d068-216">![Amministratore](./media/active-directory-saas-itrp-tutorial/ic775575.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="2d068-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="2d068-217">Dal menu di scelta rapida hello, selezionare **persone**.</span><span class="sxs-lookup"><span data-stu-id="2d068-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="2d068-218">![Persone](./media/active-directory-saas-itrp-tutorial/ic775587.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="2d068-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="2d068-219">Fare clic su **Aggiungi nuova persona** ("+").</span><span class="sxs-lookup"><span data-stu-id="2d068-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="2d068-220">![Amministratore](./media/active-directory-saas-itrp-tutorial/ic775576.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="2d068-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="2d068-221">Nella finestra di dialogo Aggiungi nuovo utente hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d068-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d068-222">![Utente](./media/active-directory-saas-itrp-tutorial/ic775577.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="2d068-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="2d068-223">a.</span><span class="sxs-lookup"><span data-stu-id="2d068-223">a.</span></span> <span data-ttu-id="2d068-224">Hello tipo **nome**, **posta elettronica** di un account aAd di cui si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="2d068-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="2d068-225">b.</span><span class="sxs-lookup"><span data-stu-id="2d068-225">b.</span></span> <span data-ttu-id="2d068-226">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2d068-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="2d068-227">È possibile usare qualsiasi altro ITRP utente account strumento di creazione o le API fornite da ITRP tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="2d068-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2d068-228">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d068-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2d068-229">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooITRP.</span><span class="sxs-lookup"><span data-stu-id="2d068-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2d068-231">**tooassign Britta Simon tooITRP, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d068-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d068-232">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d068-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2d068-234">Nell'elenco di applicazioni hello, selezionare **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="2d068-234">In hello applications list, select **ITRP**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="2d068-236">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2d068-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2d068-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d068-238">Click **Add** button.</span></span> <span data-ttu-id="2d068-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2d068-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2d068-241">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="2d068-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2d068-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2d068-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d068-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2d068-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d068-244">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2d068-244">Testing single sign-on</span></span>

<span data-ttu-id="2d068-245">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2d068-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2d068-246">Quando si fa clic hello ITRP riquadro in hello Pannello di accesso, è necessario ottenere applicazione ITRP tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="2d068-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="2d068-247">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d068-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d068-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2d068-248">Additional resources</span></span>

* [<span data-ttu-id="2d068-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d068-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d068-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d068-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con O.C. Tanner - AppreciateHub | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e O.C. Tanner - AppreciateHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="1a632-105">Esercitazione: Integrazione di Azure Active Directory con O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="1a632-106">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="1a632-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="1a632-107">In questa esercitazione, è illustrato come toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="1a632-108">Tanner - AppreciateHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a632-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a632-109">L'integrazione di O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-109">Integrating O.C.</span></span> <span data-ttu-id="1a632-110">Sarà Tonon - AppreciateHub con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1a632-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1a632-111">È possibile controllare in Azure AD che ha accesso tooO.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="1a632-112">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="1a632-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="1a632-113">È possibile abilitare il get tooautomatically utenti connesso tooO.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="1a632-114">Tanner - AppreciateHub (Single Sign-On) con i relativi account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a632-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a632-115">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1a632-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1a632-116">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a632-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a632-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1a632-117">Prerequisites</span></span>

<span data-ttu-id="1a632-118">integrazione di Azure AD con O.C. tooconfigure</span><span class="sxs-lookup"><span data-stu-id="1a632-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="1a632-119">Sarà Tonon - AppreciateHub, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1a632-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="1a632-120">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a632-120">An Azure AD subscription</span></span>
- <span data-ttu-id="1a632-121">Sottoscrizione di O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-121">A O.C.</span></span> <span data-ttu-id="1a632-122">Sottoscrizione di Tanner - AppreciateHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1a632-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a632-123">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1a632-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a632-124">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1a632-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a632-125">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1a632-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a632-126">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a632-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a632-127">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1a632-127">Scenario description</span></span>
<span data-ttu-id="1a632-128">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1a632-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a632-129">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1a632-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a632-130">Aggiunta di O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-130">Adding O.C.</span></span> <span data-ttu-id="1a632-131">Sarà Tonon - AppreciateHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1a632-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="1a632-132">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a632-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="1a632-133">Aggiunta di O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-133">Adding O.C.</span></span> <span data-ttu-id="1a632-134">Sarà Tonon - AppreciateHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1a632-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="1a632-135">integrazione di hello tooconfigure di O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="1a632-136">Sarà Tonon - AppreciateHub in Azure AD, è necessario tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="1a632-137">Sarà Tonon - AppreciateHub dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1a632-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1a632-138">**tooadd O.C. Sarà Tonon - AppreciateHub dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1a632-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a632-139">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1a632-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a632-141">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1a632-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1a632-142">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1a632-142">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1a632-144">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1a632-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1a632-146">Nella casella di ricerca hello, digitare **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="1a632-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="1a632-148">Nel riquadro dei risultati hello, selezionare **O.C. Sarà Tonon - AppreciateHub**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1a632-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a632-150">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a632-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a632-151">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="1a632-152">Tanner - AppreciateHub in base a un utente test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1a632-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a632-153">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="1a632-154">Sarà Tonon - AppreciateHub è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a632-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="1a632-155">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="1a632-156">Sarà Tonon - AppreciateHub deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1a632-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="1a632-157">In O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-157">In O.C.</span></span> <span data-ttu-id="1a632-158">Sarà Tonon - AppreciateHub, assegnare hello un valore di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1a632-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1a632-159">tooconfigure e prova AD Azure single sign-on con O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="1a632-160">Sarà Tonon - AppreciateHub, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1a632-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1a632-161">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1a632-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1a632-162">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a632-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a632-163">**[Creazione di un utente test di O.C. Sarà Tonon - utente test AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave un equivalente di Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="1a632-164">Sarà Tonon - AppreciateHub che è collegato toohello rappresentazione in forma di Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1a632-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a632-165">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a632-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a632-166">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1a632-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a632-167">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a632-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a632-168">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="1a632-169">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="1a632-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="1a632-170">**Azure AD tooconfigure single sign-on con O.C. Sarà Tonon - AppreciateHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1a632-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a632-171">Nel portale di Azure su hello hello **O.C. Tanner - AppreciateHub** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1a632-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1a632-173">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a632-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="1a632-175">In hello **O.C. Sarà Tonon - URL e il dominio AppreciateHub** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1a632-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="1a632-177">a.</span><span class="sxs-lookup"><span data-stu-id="1a632-177">a.</span></span> <span data-ttu-id="1a632-178">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="1a632-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a632-179">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="1a632-179">This value is not real.</span></span> <span data-ttu-id="1a632-180">Aggiornare questo valore con l'URL di risposta effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="1a632-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="1a632-181">Contattare il [team. Sarà Tonon - team di supporto AppreciateHub](mailto:sso@octanner.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="1a632-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="1a632-182">b.</span><span class="sxs-lookup"><span data-stu-id="1a632-182">b.</span></span> <span data-ttu-id="1a632-183">File di metadati hello aprire utilizzando hello seguente collegamento: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="1a632-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="1a632-184">c.</span><span class="sxs-lookup"><span data-stu-id="1a632-184">c.</span></span> <span data-ttu-id="1a632-185">Individuare hello **md:AssertionConsumerService** nodo.</span><span class="sxs-lookup"><span data-stu-id="1a632-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="1a632-186">d.</span><span class="sxs-lookup"><span data-stu-id="1a632-186">d.</span></span> <span data-ttu-id="1a632-187">Copiare il valore di hello di hello **percorso** attributo.</span><span class="sxs-lookup"><span data-stu-id="1a632-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![Configurare le impostazioni dell'app][12]
   
    <span data-ttu-id="1a632-189">e.</span><span class="sxs-lookup"><span data-stu-id="1a632-189">e.</span></span> <span data-ttu-id="1a632-190">In hello **URL di accesso** casella di testo, oltre il valore di hello hanno ottenuto nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="1a632-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="1a632-191">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1a632-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="1a632-193">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1a632-193">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a632-195">tooconfigure single sign-on sul **O.C. Sarà Tonon - AppreciateHub** lato, è necessario hello toosend scaricato **Metadata XML** troppo[O.C. Tanner - AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="1a632-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="1a632-196">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1a632-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1a632-197">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1a632-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1a632-198">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a632-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a632-199">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a632-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a632-200">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1a632-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1a632-202">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1a632-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a632-203">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1a632-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a632-205">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1a632-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a632-207">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1a632-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a632-209">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1a632-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a632-211">a.</span><span class="sxs-lookup"><span data-stu-id="1a632-211">a.</span></span> <span data-ttu-id="1a632-212">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a632-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a632-213">b.</span><span class="sxs-lookup"><span data-stu-id="1a632-213">b.</span></span> <span data-ttu-id="1a632-214">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a632-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a632-215">c.</span><span class="sxs-lookup"><span data-stu-id="1a632-215">c.</span></span> <span data-ttu-id="1a632-216">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1a632-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1a632-217">d.</span><span class="sxs-lookup"><span data-stu-id="1a632-217">d.</span></span> <span data-ttu-id="1a632-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1a632-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="1a632-219">Creazione di un utente test di O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-219">Creating a O.C.</span></span> <span data-ttu-id="1a632-220">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="1a632-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="1a632-221">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in O.C. toocreate</span><span class="sxs-lookup"><span data-stu-id="1a632-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="1a632-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="1a632-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="1a632-223">**toocreate un utente denominato Britta Simon in O.C. Sarà Tonon - AppreciateHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1a632-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="1a632-224">Chiedere al [team. Sarà Tonon - team di supporto AppreciateHub](mailto:sso@octanner.com) toocreate un utente che ha come hello attributo nameID lo stesso valore nome utente hello di Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a632-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1a632-225">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a632-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1a632-226">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooO.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="1a632-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="1a632-227">Tanner - AppreciateHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1a632-229">**tooassign Britta Simon tooO.C. Sarà Tonon - AppreciateHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1a632-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a632-230">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1a632-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1a632-232">Nell'elenco di applicazioni hello, selezionare **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="1a632-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="1a632-234">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1a632-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1a632-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1a632-236">Click **Add** button.</span></span> <span data-ttu-id="1a632-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1a632-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1a632-239">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1a632-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1a632-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1a632-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a632-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1a632-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a632-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1a632-242">Testing single sign-on</span></span>

<span data-ttu-id="1a632-243">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1a632-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="1a632-244">Quando si fa clic su hello O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-244">When you click hello O.C.</span></span> <span data-ttu-id="1a632-245">Sarà Tonon - riquadro AppreciateHub in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="1a632-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="1a632-246">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="1a632-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a632-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1a632-247">Additional resources</span></span>

* [<span data-ttu-id="1a632-248">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a632-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a632-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a632-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png


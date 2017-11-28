---
title: 'Esercitazione: Integrazione di Azure Active Directory con Marketo | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Marketo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="d13d9-103">Esercitazione: Integrazione di Azure Active Directory con Marketo</span><span class="sxs-lookup"><span data-stu-id="d13d9-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="d13d9-104">In questa esercitazione, è illustrato come toointegrate Marketo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d13d9-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d13d9-105">Integrazione di Marketo con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d13d9-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d13d9-106">È possibile controllare in Azure AD che ha accesso tooMarketo</span><span class="sxs-lookup"><span data-stu-id="d13d9-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="d13d9-107">È possibile abilitare l'utenti tooautomatically get connesso tooMarketo (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d13d9-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d13d9-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d13d9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d13d9-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d13d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d13d9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d13d9-110">Prerequisites</span></span>

<span data-ttu-id="d13d9-111">integrazione di Azure AD con Marketo tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d13d9-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="d13d9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d13d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d13d9-113">Sottoscrizione di Marketo abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d13d9-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d13d9-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d13d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d13d9-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d13d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d13d9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d13d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d13d9-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d13d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d13d9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d13d9-118">Scenario description</span></span>
<span data-ttu-id="d13d9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d13d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d13d9-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d13d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d13d9-121">Aggiunta di Marketo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d13d9-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="d13d9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d13d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="d13d9-123">Aggiunta di Marketo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d13d9-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="d13d9-124">integrazione hello tooconfigure di Marketo in Azure AD, è necessario tooadd Marketo dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d13d9-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d13d9-125">**tooadd Marketo dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d13d9-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d13d9-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d13d9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d13d9-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d13d9-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d13d9-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d13d9-133">Nella casella di ricerca hello, digitare **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-133">In hello search box, type **Marketo**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="d13d9-135">Nel riquadro dei risultati hello, selezionare **Marketo**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d13d9-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d13d9-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d13d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d13d9-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Marketo mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d13d9-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d13d9-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Marketo è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d13d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="d13d9-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Marketo deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d13d9-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="d13d9-141">In Marketo, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d13d9-142">tooconfigure e prova AD Azure single sign-on con Marketo, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d13d9-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d13d9-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d13d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d13d9-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d13d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d13d9-145">**[Creazione di un utente test Marketo](#creating-a-marketo-test-user)**  -toohave un equivalente di Britta Simon in Marketo che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d13d9-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d13d9-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d13d9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d13d9-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d13d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d13d9-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d13d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d13d9-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Marketo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="d13d9-150">**Azure AD tooconfigure single sign-on con Marketo, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d13d9-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="d13d9-151">Nel portale di Azure su hello hello **Marketo** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d13d9-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d13d9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="d13d9-155">In hello **dominio Marketo e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d13d9-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="d13d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="d13d9-157">a.</span></span> <span data-ttu-id="d13d9-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="d13d9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="d13d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="d13d9-159">b.</span></span> <span data-ttu-id="d13d9-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="d13d9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d13d9-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d13d9-161">These values are not real.</span></span> <span data-ttu-id="d13d9-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d13d9-163">Contatto [team di supporto di Marketo](http://investors.marketo.com/contactus.cfm) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="d13d9-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="d13d9-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d13d9-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="d13d9-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d13d9-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d13d9-168">In hello **Marketo configurazione** fare clic su **configurare Marketo** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="d13d9-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d13d9-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d13d9-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="d13d9-171">tooget Munchkin Id dell'applicazione, accedere tooMarketo usando credenziali di amministratore ed eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="d13d9-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="d13d9-172">a.</span><span class="sxs-lookup"><span data-stu-id="d13d9-172">a.</span></span> <span data-ttu-id="d13d9-173">Accedi app tooMarketo usando credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="d13d9-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="d13d9-174">b.</span><span class="sxs-lookup"><span data-stu-id="d13d9-174">b.</span></span> <span data-ttu-id="d13d9-175">Fare clic su hello **Admin** pulsante nel riquadro di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="d13d9-177">c.</span><span class="sxs-lookup"><span data-stu-id="d13d9-177">c.</span></span> <span data-ttu-id="d13d9-178">Passare dal menu di integrazione toohello e fare clic su hello **collegamento Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="d13d9-180">d.</span><span class="sxs-lookup"><span data-stu-id="d13d9-180">d.</span></span> <span data-ttu-id="d13d9-181">Copiare l'Id Munchkin mostrato nella schermata di hello hello e completare l'URL di risposta nella configurazione guidata di hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d13d9-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="d13d9-183">tooconfigure hello SSO nell'applicazione hello, seguire hello passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d13d9-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="d13d9-184">a.</span><span class="sxs-lookup"><span data-stu-id="d13d9-184">a.</span></span> <span data-ttu-id="d13d9-185">Accedi app tooMarketo usando credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="d13d9-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="d13d9-186">b.</span><span class="sxs-lookup"><span data-stu-id="d13d9-186">b.</span></span> <span data-ttu-id="d13d9-187">Fare clic su hello **Admin** pulsante nel riquadro di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="d13d9-189">c.</span><span class="sxs-lookup"><span data-stu-id="d13d9-189">c.</span></span> <span data-ttu-id="d13d9-190">Passare dal menu di integrazione toohello e fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="d13d9-192">d.</span><span class="sxs-lookup"><span data-stu-id="d13d9-192">d.</span></span> <span data-ttu-id="d13d9-193">Fare clic su tooenable hello impostazioni SAML, **modifica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d13d9-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="d13d9-195">e.</span><span class="sxs-lookup"><span data-stu-id="d13d9-195">e.</span></span> <span data-ttu-id="d13d9-196">Impostazioni dell'accesso Single Sign-On **abilitate**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="d13d9-197">f.</span><span class="sxs-lookup"><span data-stu-id="d13d9-197">f.</span></span> <span data-ttu-id="d13d9-198">Hello Incolla **ID entità SAML**, in hello **ID autorità di certificazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="d13d9-199">g.</span><span class="sxs-lookup"><span data-stu-id="d13d9-199">g.</span></span> <span data-ttu-id="d13d9-200">In hello **ID entità** casella di testo, immettere l'URL di hello come `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="d13d9-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="d13d9-201">h.</span><span class="sxs-lookup"><span data-stu-id="d13d9-201">h.</span></span> <span data-ttu-id="d13d9-202">Hello seleziona User ID Location come **Name Identifier element**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="d13d9-204">Se l'identificatore utente non è il valore UPN valore hello modifica nella scheda attributi hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="d13d9-205">i.</span><span class="sxs-lookup"><span data-stu-id="d13d9-205">i.</span></span> <span data-ttu-id="d13d9-206">Caricare il certificato hello, che è stato scaricato dalla configurazione guidata di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d13d9-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="d13d9-207">**Salvare** hello impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d13d9-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="d13d9-208">j.</span><span class="sxs-lookup"><span data-stu-id="d13d9-208">j.</span></span> <span data-ttu-id="d13d9-209">Modificare le impostazioni di reindirizzamento pagine hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="d13d9-210">k.</span><span class="sxs-lookup"><span data-stu-id="d13d9-210">k.</span></span> <span data-ttu-id="d13d9-211">Hello Incolla **SAML Single Sign-On Service URL** in hello **URL di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="d13d9-212">l.</span><span class="sxs-lookup"><span data-stu-id="d13d9-212">l.</span></span> <span data-ttu-id="d13d9-213">Hello Incolla **Sign-Out URL** in hello **Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="d13d9-214">m.</span><span class="sxs-lookup"><span data-stu-id="d13d9-214">m.</span></span> <span data-ttu-id="d13d9-215">In hello **URL errori**, copia il **URL dell'istanza Marketo** e fare clic su **salvare** pulsante toosave impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d13d9-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="d13d9-217">tooenable hello SSO per gli utenti, hello completa le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d13d9-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="d13d9-218">a.</span><span class="sxs-lookup"><span data-stu-id="d13d9-218">a.</span></span> <span data-ttu-id="d13d9-219">Accedi app tooMarketo usando credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="d13d9-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="d13d9-220">b.</span><span class="sxs-lookup"><span data-stu-id="d13d9-220">b.</span></span> <span data-ttu-id="d13d9-221">Fare clic su hello **Admin** pulsante nel riquadro di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="d13d9-223">c.</span><span class="sxs-lookup"><span data-stu-id="d13d9-223">c.</span></span> <span data-ttu-id="d13d9-224">Passare toohello **sicurezza** menu e fare clic su **impostazioni di accesso**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="d13d9-226">d.</span><span class="sxs-lookup"><span data-stu-id="d13d9-226">d.</span></span> <span data-ttu-id="d13d9-227">Controllare hello **richiedono SSO** opzione e **salvare** hello impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d13d9-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="d13d9-229">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d13d9-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d13d9-230">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d13d9-231">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d13d9-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d13d9-232">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d13d9-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="d13d9-233">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d13d9-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d13d9-235">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d13d9-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d13d9-236">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d13d9-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d13d9-238">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d13d9-240">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d13d9-242">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d13d9-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d13d9-244">a.</span><span class="sxs-lookup"><span data-stu-id="d13d9-244">a.</span></span> <span data-ttu-id="d13d9-245">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d13d9-246">b.</span><span class="sxs-lookup"><span data-stu-id="d13d9-246">b.</span></span> <span data-ttu-id="d13d9-247">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d13d9-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d13d9-248">c.</span><span class="sxs-lookup"><span data-stu-id="d13d9-248">c.</span></span> <span data-ttu-id="d13d9-249">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d13d9-250">d.</span><span class="sxs-lookup"><span data-stu-id="d13d9-250">d.</span></span> <span data-ttu-id="d13d9-251">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="d13d9-252">Creazione di un utente test di Marketo</span><span class="sxs-lookup"><span data-stu-id="d13d9-252">Creating a Marketo test user</span></span>

<span data-ttu-id="d13d9-253">In questa sezione viene creato un utente chiamato Britta Simon in Marketo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="d13d9-254">Seguire questi toocreate passaggi, un utente nella piattaforma di Marketo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="d13d9-255">Accedi app tooMarketo usando credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="d13d9-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="d13d9-256">Fare clic su hello **Admin** pulsante nel riquadro di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="d13d9-258">Passare toohello **sicurezza** menu e fare clic su **utenti e ruoli**</span><span class="sxs-lookup"><span data-stu-id="d13d9-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="d13d9-260">Fare clic su hello **Invita nuovo utente** collegamento nella scheda utenti hello</span><span class="sxs-lookup"><span data-stu-id="d13d9-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="d13d9-262">In hello riempimento guidata invitare nuovi utenti di hello le seguenti informazioni</span><span class="sxs-lookup"><span data-stu-id="d13d9-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="d13d9-263">a.</span><span class="sxs-lookup"><span data-stu-id="d13d9-263">a.</span></span> <span data-ttu-id="d13d9-264">Immettere nome utente hello **posta elettronica** indirizzo nella casella di testo hello</span><span class="sxs-lookup"><span data-stu-id="d13d9-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="d13d9-266">b.</span><span class="sxs-lookup"><span data-stu-id="d13d9-266">b.</span></span> <span data-ttu-id="d13d9-267">Immettere hello **nome** nella casella di testo hello</span><span class="sxs-lookup"><span data-stu-id="d13d9-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="d13d9-268">c.</span><span class="sxs-lookup"><span data-stu-id="d13d9-268">c.</span></span> <span data-ttu-id="d13d9-269">Immettere hello **cognome** nella casella di testo hello</span><span class="sxs-lookup"><span data-stu-id="d13d9-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="d13d9-270">d.</span><span class="sxs-lookup"><span data-stu-id="d13d9-270">d.</span></span> <span data-ttu-id="d13d9-271">Fare clic su **Avanti**</span><span class="sxs-lookup"><span data-stu-id="d13d9-271">Click **Next**</span></span>

6. <span data-ttu-id="d13d9-272">In hello **autorizzazioni** scheda, seleziona hello **userRoles** e fare clic su **successivo**</span><span class="sxs-lookup"><span data-stu-id="d13d9-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="d13d9-274">Fare clic su hello **inviare** pulsante invito di toosend hello utente</span><span class="sxs-lookup"><span data-stu-id="d13d9-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="d13d9-276">Utente riceve una notifica di posta elettronica hello e hello tooclick collegamento e modificare hello password tooactivate hello account.</span><span class="sxs-lookup"><span data-stu-id="d13d9-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d13d9-277">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d13d9-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d13d9-278">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMarketo.</span><span class="sxs-lookup"><span data-stu-id="d13d9-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d13d9-280">**tooassign Britta Simon tooMarketo, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d13d9-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="d13d9-281">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d13d9-283">Nell'elenco di applicazioni hello, selezionare **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-283">In hello applications list, select **Marketo**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="d13d9-285">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d13d9-287">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-287">Click **Add** button.</span></span> <span data-ttu-id="d13d9-288">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d13d9-290">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d13d9-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d13d9-291">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d13d9-292">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d13d9-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d13d9-293">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d13d9-293">Testing single sign-on</span></span>

<span data-ttu-id="d13d9-294">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d13d9-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d13d9-295">Quando si fa clic su riquadro Marketo hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Marketo applicazione.</span><span class="sxs-lookup"><span data-stu-id="d13d9-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d13d9-296">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d13d9-296">Additional resources</span></span>

* [<span data-ttu-id="d13d9-297">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d13d9-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d13d9-298">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d13d9-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png


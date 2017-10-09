---
title: 'Esercitazione: Integrazione di Azure Active Directory con Wingspan eTMF | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Wingspan eTMF.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: ed5fda5318a0d3841af8b2db4fb74db550befaea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="cdda5-103">Esercitazione: Integrazione di Azure Active Directory con Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="cdda5-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="cdda5-104">In questa esercitazione, è illustrato come toointegrate Wingspan eTMF con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cdda5-104">In this tutorial, you learn how toointegrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cdda5-105">Integrazione Wingspan eTMF con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cdda5-105">Integrating Wingspan eTMF with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cdda5-106">È possibile controllare in Azure AD che ha accesso tooWingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="cdda5-106">You can control in Azure AD who has access tooWingspan eTMF</span></span>
- <span data-ttu-id="cdda5-107">È possibile abilitare l'utenti tooautomatically get connesso tooWingspan eTMF (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdda5-107">You can enable your users tooautomatically get signed-on tooWingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cdda5-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cdda5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cdda5-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cdda5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdda5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cdda5-110">Prerequisites</span></span>

<span data-ttu-id="cdda5-111">integrazione di Azure AD con Wingspan eTMF tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cdda5-111">tooconfigure Azure AD integration with Wingspan eTMF, you need hello following items:</span></span>

- <span data-ttu-id="cdda5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdda5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cdda5-113">Sottoscrizione di Wingspan eTMF abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cdda5-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cdda5-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cdda5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cdda5-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cdda5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cdda5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cdda5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cdda5-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdda5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cdda5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cdda5-118">Scenario description</span></span>
<span data-ttu-id="cdda5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cdda5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cdda5-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cdda5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cdda5-121">Aggiunta di Wingspan eTMF dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cdda5-121">Adding Wingspan eTMF from hello gallery</span></span>
2. <span data-ttu-id="cdda5-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdda5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-hello-gallery"></a><span data-ttu-id="cdda5-123">Aggiunta di Wingspan eTMF dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cdda5-123">Adding Wingspan eTMF from hello gallery</span></span>
<span data-ttu-id="cdda5-124">integrazione hello tooconfigure di Wingspan eTMF in Azure AD, è necessario tooadd Wingspan eTMF dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cdda5-124">tooconfigure hello integration of Wingspan eTMF into Azure AD, you need tooadd Wingspan eTMF from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cdda5-125">**tooadd Wingspan eTMF dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cdda5-125">**tooadd Wingspan eTMF from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdda5-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cdda5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cdda5-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cdda5-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="cdda5-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cdda5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="cdda5-133">Nella casella di ricerca hello, digitare **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-133">In hello search box, type **Wingspan eTMF**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="cdda5-135">Nel riquadro dei risultati hello, selezionare **Wingspan eTMF**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cdda5-135">In hello results panel, select **Wingspan eTMF**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cdda5-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdda5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cdda5-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Wingspan eTMF in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cdda5-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cdda5-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Wingspan eTMF è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdda5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wingspan eTMF is tooa user in Azure AD.</span></span> <span data-ttu-id="cdda5-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Wingspan eTMF deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cdda5-140">In other words, a link relationship between an Azure AD user and hello related user in Wingspan eTMF needs toobe established.</span></span>

<span data-ttu-id="cdda5-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="cdda5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="cdda5-142">tooconfigure e prova AD Azure single sign-on con Wingspan eTMF, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cdda5-142">tooconfigure and test Azure AD single sign-on with Wingspan eTMF, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cdda5-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cdda5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cdda5-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cdda5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cdda5-145">**[Creazione di un utente di test eTMF Wingspan](#creating-a-wingspan-etmf-test-user)**  -toohave un equivalente di Britta Simon in eTMF Wingspan che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cdda5-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - toohave a counterpart of Britta Simon in Wingspan eTMF that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cdda5-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cdda5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cdda5-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cdda5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cdda5-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdda5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cdda5-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="cdda5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="cdda5-150">**Azure AD tooconfigure single sign-on con eTMF Wingspan, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cdda5-150">**tooconfigure Azure AD single sign-on with Wingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdda5-151">Nel portale di Azure su hello hello **Wingspan eTMF** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-151">In hello Azure portal, on hello **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="cdda5-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cdda5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="cdda5-155">In hello **Wingspan eTMF dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cdda5-155">On hello **Wingspan eTMF Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="cdda5-157">a.</span><span class="sxs-lookup"><span data-stu-id="cdda5-157">a.</span></span> <span data-ttu-id="cdda5-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="cdda5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="cdda5-159">b.</span><span class="sxs-lookup"><span data-stu-id="cdda5-159">b.</span></span> <span data-ttu-id="cdda5-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="cdda5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="cdda5-161">c.</span><span class="sxs-lookup"><span data-stu-id="cdda5-161">c.</span></span> <span data-ttu-id="cdda5-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="cdda5-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="cdda5-163">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="cdda5-163">These values are not hello real.</span></span> <span data-ttu-id="cdda5-164">Aggiornare questi valori con URL di risposta, identificatore e Sign-On URL effettivo hello inclusi hello nome effettivo del cliente e il nome di istanza.</span><span class="sxs-lookup"><span data-stu-id="cdda5-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL including hello actual customer name and instance name.</span></span> <span data-ttu-id="cdda5-165">Contatto [team di supporto Client eTMF Wingspan](http://www.wingspan.com/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="cdda5-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="cdda5-166">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cdda5-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="cdda5-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cdda5-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cdda5-170">tooconfigure single sign-on sul **Wingspan eTMF** lato, è necessario hello toosend scaricato **Metadata XML** troppo[supporto eTMF Wingspan](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="cdda5-170">tooconfigure single sign-on on **Wingspan eTMF** side, you need toosend hello downloaded **Metadata XML** too[Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="cdda5-171">Essi configurazione hello toohave connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="cdda5-171">They set this up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cdda5-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="cdda5-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cdda5-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="cdda5-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cdda5-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cdda5-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cdda5-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdda5-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="cdda5-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cdda5-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="cdda5-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cdda5-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdda5-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cdda5-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cdda5-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cdda5-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="cdda5-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cdda5-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cdda5-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cdda5-187">a.</span><span class="sxs-lookup"><span data-stu-id="cdda5-187">a.</span></span> <span data-ttu-id="cdda5-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cdda5-189">b.</span><span class="sxs-lookup"><span data-stu-id="cdda5-189">b.</span></span> <span data-ttu-id="cdda5-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cdda5-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cdda5-191">c.</span><span class="sxs-lookup"><span data-stu-id="cdda5-191">c.</span></span> <span data-ttu-id="cdda5-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cdda5-193">d.</span><span class="sxs-lookup"><span data-stu-id="cdda5-193">d.</span></span> <span data-ttu-id="cdda5-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="cdda5-195">Creazione di un utente test di Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="cdda5-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="cdda5-196">In questa sezione si crea un utente di nome Britta Simon in Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="cdda5-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="cdda5-197">Lavorare con [supporto eTMF Wingspan](http://www.wingspan.com/contact-us/) tooadd utenti hello hello applicazione eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="cdda5-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) tooadd hello users in hello Wingspan eTMF application.</span></span> <span data-ttu-id="cdda5-198">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cdda5-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cdda5-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdda5-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cdda5-200">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="cdda5-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWingspan eTMF.</span></span>

![Assegna utente][200] 

<span data-ttu-id="cdda5-202">**tooassign Britta Simon tooWingspan eTMF, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cdda5-202">**tooassign Britta Simon tooWingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="cdda5-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cdda5-205">Nell'elenco di applicazioni hello, selezionare **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-205">In hello applications list, select **Wingspan eTMF**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="cdda5-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="cdda5-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-209">Click **Add** button.</span></span> <span data-ttu-id="cdda5-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="cdda5-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="cdda5-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cdda5-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cdda5-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cdda5-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cdda5-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cdda5-215">Testing single sign-on</span></span>

<span data-ttu-id="cdda5-216">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cdda5-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="cdda5-217">Fare clic sul riquadro di eTMF Wingspan hello in hello Pannello di accesso, sarà reindirizzato tooOrganization della pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="cdda5-217">Click hello Wingspan eTMF tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="cdda5-218">Dopo aver eseguito l'accesso, sarà connesso tooyour applicazione eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="cdda5-218">After successful login, you will be signed-on tooyour Wingspan eTMF application.</span></span> <span data-ttu-id="cdda5-219">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="cdda5-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cdda5-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cdda5-220">Additional resources</span></span>

* [<span data-ttu-id="cdda5-221">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cdda5-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cdda5-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cdda5-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png


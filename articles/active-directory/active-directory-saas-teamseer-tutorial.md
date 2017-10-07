---
title: 'Esercitazione: Integrazione di Azure Active Directory con TeamSeer | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TeamSeer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="1d452-103">Esercitazione: Integrazione di Azure Active Directory con TeamSeer</span><span class="sxs-lookup"><span data-stu-id="1d452-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="1d452-104">In questa esercitazione, è illustrato come toointegrate TeamSeer con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d452-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d452-105">Integrazione TeamSeer con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1d452-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1d452-106">È possibile controllare in Azure AD che ha accesso tooTeamSeer</span><span class="sxs-lookup"><span data-stu-id="1d452-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="1d452-107">È possibile abilitare l'utenti tooautomatically get connesso tooTeamSeer (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d452-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d452-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d452-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1d452-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d452-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d452-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d452-110">Prerequisites</span></span>

<span data-ttu-id="1d452-111">integrazione di Azure AD con TeamSeer tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1d452-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="1d452-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d452-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d452-113">Sottoscrizione di TeamSeer abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1d452-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d452-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1d452-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d452-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1d452-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d452-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1d452-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d452-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d452-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d452-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1d452-118">Scenario description</span></span>
<span data-ttu-id="1d452-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1d452-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d452-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1d452-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d452-121">Aggiunta di TeamSeer dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1d452-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="1d452-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d452-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="1d452-123">Aggiunta di TeamSeer dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1d452-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="1d452-124">integrazione hello tooconfigure di TeamSeer in tooAzure Active Directory, è necessario tooadd TeamSeer dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1d452-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1d452-125">**tooadd TeamSeer dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d452-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d452-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1d452-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d452-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1d452-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1d452-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d452-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1d452-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1d452-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1d452-133">Nella casella di ricerca hello, digitare **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="1d452-133">In hello search box, type **TeamSeer**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="1d452-135">Nel riquadro dei risultati hello, selezionare **TeamSeer**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1d452-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d452-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d452-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d452-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TeamSeer usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1d452-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1d452-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TeamSeer è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d452-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="1d452-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TeamSeer deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1d452-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="1d452-141">In TeamSeer, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1d452-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1d452-142">tooconfigure e prova AD Azure single sign-on con TeamSeer, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1d452-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1d452-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1d452-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1d452-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d452-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d452-145">**[Creazione di un utente test TeamSeer](#creating-a-teamseer-test-user)**  -toohave un equivalente di Britta Simon in TeamSeer che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1d452-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d452-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d452-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d452-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1d452-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d452-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d452-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d452-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="1d452-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="1d452-150">**Azure AD tooconfigure single sign-on con TeamSeer, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d452-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d452-151">Nel portale di Azure su hello hello **TeamSeer** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1d452-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1d452-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d452-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="1d452-155">In hello **TeamSeer dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d452-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="1d452-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="1d452-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1d452-158">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="1d452-158">hello value is not real.</span></span> <span data-ttu-id="1d452-159">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1d452-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1d452-160">Contatto [team di supporto TeamSeer Client](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="1d452-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="1d452-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1d452-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="1d452-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1d452-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d452-165">In hello **TeamSeer configurazione** fare clic su **configurare TeamSeer** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1d452-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1d452-166">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1d452-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="1d452-168">In una finestra del web browser, accedere come amministratore nel sito della società TeamSeer di tooyour.</span><span class="sxs-lookup"><span data-stu-id="1d452-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="1d452-169">Andare troppo**HR Admin**.</span><span class="sxs-lookup"><span data-stu-id="1d452-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="1d452-170">![Amministratore risorse umane](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Amministratore risorse umane")</span><span class="sxs-lookup"><span data-stu-id="1d452-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="1d452-171">Fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="1d452-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="1d452-172">![Installazione](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="1d452-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="1d452-173">Fare clic su **Configura dettagli del provider SAML**.</span><span class="sxs-lookup"><span data-stu-id="1d452-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="1d452-174">![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="1d452-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="1d452-175">Nella sezione dettagli di provider SAML hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d452-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1d452-176">![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="1d452-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="1d452-177">a.</span><span class="sxs-lookup"><span data-stu-id="1d452-177">a.</span></span> <span data-ttu-id="1d452-178">Hello Incolla **URL servizio Single Sign-On** valore toohello **URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1d452-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="1d452-179">b.</span><span class="sxs-lookup"><span data-stu-id="1d452-179">b.</span></span> <span data-ttu-id="1d452-180">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto negli Appunti tooyour e quindi incollarlo toohello **IdP Public Certificate** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1d452-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="1d452-181">hello toocomplete configurazione del provider SAML, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d452-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="1d452-182">![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="1d452-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="1d452-183">a.</span><span class="sxs-lookup"><span data-stu-id="1d452-183">a.</span></span> <span data-ttu-id="1d452-184">In hello **indirizzi di posta elettronica di Test**, digitare l'indirizzo di posta elettronica dell'utente test hello.</span><span class="sxs-lookup"><span data-stu-id="1d452-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="1d452-185">b.</span><span class="sxs-lookup"><span data-stu-id="1d452-185">b.</span></span> <span data-ttu-id="1d452-186">In hello **dell'autorità di certificazione** casella di testo, hello tipo URL autorità di certificazione hello provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="1d452-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="1d452-187">c.</span><span class="sxs-lookup"><span data-stu-id="1d452-187">c.</span></span> <span data-ttu-id="1d452-188">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1d452-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1d452-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1d452-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1d452-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1d452-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1d452-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d452-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d452-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d452-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d452-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1d452-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1d452-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d452-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d452-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1d452-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d452-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d452-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d452-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1d452-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d452-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d452-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d452-204">a.</span><span class="sxs-lookup"><span data-stu-id="1d452-204">a.</span></span> <span data-ttu-id="1d452-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d452-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d452-206">b.</span><span class="sxs-lookup"><span data-stu-id="1d452-206">b.</span></span> <span data-ttu-id="1d452-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1d452-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d452-208">c.</span><span class="sxs-lookup"><span data-stu-id="1d452-208">c.</span></span> <span data-ttu-id="1d452-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1d452-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1d452-210">d.</span><span class="sxs-lookup"><span data-stu-id="1d452-210">d.</span></span> <span data-ttu-id="1d452-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1d452-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="1d452-212">Creazione di un utente di test di TeamSeer</span><span class="sxs-lookup"><span data-stu-id="1d452-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="1d452-213">toolog agli utenti di Azure AD tooenable in tooTeamSeer, è necessario eseguirne il provisioning in tooShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="1d452-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="1d452-214">Nel caso di hello di TeamSeer, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="1d452-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="1d452-215">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d452-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d452-216">Accedi tooyour **TeamSeer** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1d452-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="1d452-217">Eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d452-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="1d452-218">![Amministratore risorse umane](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Amministratore risorse umane")</span><span class="sxs-lookup"><span data-stu-id="1d452-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="1d452-219">a.</span><span class="sxs-lookup"><span data-stu-id="1d452-219">a.</span></span> <span data-ttu-id="1d452-220">Andare troppo**HR Admin \> utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d452-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="1d452-221">b.</span><span class="sxs-lookup"><span data-stu-id="1d452-221">b.</span></span> <span data-ttu-id="1d452-222">Fare clic su **eseguire Creazione guidata nuovo utente hello**.</span><span class="sxs-lookup"><span data-stu-id="1d452-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="1d452-223">In hello **dettagli utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d452-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1d452-224">![Dettagli utente](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Dettagli utente")</span><span class="sxs-lookup"><span data-stu-id="1d452-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="1d452-225">a.</span><span class="sxs-lookup"><span data-stu-id="1d452-225">a.</span></span> <span data-ttu-id="1d452-226">Hello tipo **nome**, **Surname**, **nome utente (indirizzo di posta elettronica)** di un account aAd di cui si desidera tooprovision in toohello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="1d452-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="1d452-227">b.</span><span class="sxs-lookup"><span data-stu-id="1d452-227">b.</span></span> <span data-ttu-id="1d452-228">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1d452-228">Click **Next**.</span></span>

4. <span data-ttu-id="1d452-229">Seguire hello istruzioni per l'aggiunta di un nuovo utente e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="1d452-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="1d452-230">È possibile usare qualsiasi altro TeamSeer utente account strumento di creazione o le API fornite da TeamSeer tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d452-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1d452-231">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d452-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1d452-232">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTeamSeer.</span><span class="sxs-lookup"><span data-stu-id="1d452-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1d452-234">**tooassign Britta Simon tooTeamSeer, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d452-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d452-235">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d452-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1d452-237">Nell'elenco di applicazioni hello, selezionare **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="1d452-237">In hello applications list, select **TeamSeer**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="1d452-239">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d452-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1d452-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1d452-241">Click **Add** button.</span></span> <span data-ttu-id="1d452-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1d452-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1d452-244">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1d452-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1d452-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d452-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d452-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1d452-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d452-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1d452-247">Testing single sign-on</span></span>

<span data-ttu-id="1d452-248">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="1d452-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="1d452-249">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1d452-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d452-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1d452-250">Additional resources</span></span>

* [<span data-ttu-id="1d452-251">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d452-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d452-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d452-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con CloudPassage | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e CloudPassage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="135df-103">Esercitazione: Integrazione di Azure Active Directory con CloudPassage</span><span class="sxs-lookup"><span data-stu-id="135df-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="135df-104">In questa esercitazione, è illustrato come toointegrate CloudPassage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="135df-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="135df-105">Integrazione CloudPassage con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="135df-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="135df-106">È possibile controllare in Azure AD che ha accesso tooCloudPassage</span><span class="sxs-lookup"><span data-stu-id="135df-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="135df-107">È possibile abilitare l'utenti tooautomatically get connesso tooCloudPassage (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="135df-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="135df-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="135df-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="135df-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="135df-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="135df-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="135df-110">Prerequisites</span></span>

<span data-ttu-id="135df-111">integrazione di Azure AD con CloudPassage tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="135df-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="135df-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="135df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="135df-113">Sottoscrizione di CloudPassage abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="135df-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="135df-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="135df-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="135df-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="135df-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="135df-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="135df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="135df-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="135df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="135df-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="135df-118">Scenario description</span></span>
<span data-ttu-id="135df-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="135df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="135df-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="135df-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="135df-121">Aggiunta di CloudPassage dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="135df-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="135df-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="135df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="135df-123">Aggiunta di CloudPassage dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="135df-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="135df-124">integrazione hello tooconfigure di CloudPassage in Azure AD, è necessario tooadd CloudPassage dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="135df-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="135df-125">**tooadd CloudPassage dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="135df-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="135df-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="135df-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="135df-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="135df-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="135df-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="135df-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="135df-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="135df-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="135df-133">Nella casella di ricerca hello, digitare **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="135df-133">In hello search box, type **CloudPassage**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="135df-135">Nel riquadro dei risultati hello, selezionare **CloudPassage**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="135df-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="135df-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="135df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="135df-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con CloudPassage mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="135df-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="135df-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in CloudPassage è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="135df-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="135df-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in CloudPassage deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="135df-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="135df-141">In CloudPassage, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="135df-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="135df-142">tooconfigure e prova AD Azure single sign-on con CloudPassage, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="135df-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="135df-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="135df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="135df-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="135df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="135df-145">**[Creazione di un utente test CloudPassage](#creating-a-cloudpassage-test-user)**  -toohave un equivalente di Britta Simon in CloudPassage che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="135df-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="135df-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="135df-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="135df-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="135df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="135df-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="135df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="135df-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="135df-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="135df-150">**Azure AD tooconfigure single sign-on con CloudPassage, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="135df-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="135df-151">Nel portale di Azure su hello hello **CloudPassage** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="135df-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="135df-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="135df-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="135df-155">In hello **CloudPassage dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="135df-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="135df-157">a.</span><span class="sxs-lookup"><span data-stu-id="135df-157">a.</span></span> <span data-ttu-id="135df-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="135df-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="135df-159">b.</span><span class="sxs-lookup"><span data-stu-id="135df-159">b.</span></span> <span data-ttu-id="135df-160">In hello **URL di risposta** casella di testo, digitare un URL con modello di hello: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="135df-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="135df-161">È possibile ottenere il valore per questo attributo, fare clic su **documentazione del programma di installazione SSO** in hello **Single Sign-on Settings** sezione del portale CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="135df-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="135df-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="135df-163">These values are not real.</span></span> <span data-ttu-id="135df-164">Aggiornare questi valori con l'URL di risposta effettivo hello e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="135df-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="135df-165">Contatto [team di supporto CloudPassage Client](https://www.cloudpassage.com/company/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="135df-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="135df-166">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="135df-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="135df-168">L'applicazione CloudPassage prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="135df-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="135df-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="135df-169">hello following screenshot shows an example for this.</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="135df-171">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="135df-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="135df-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="135df-172">Attribute Name</span></span> | <span data-ttu-id="135df-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="135df-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="135df-174">firstname</span><span class="sxs-lookup"><span data-stu-id="135df-174">firstname</span></span> |<span data-ttu-id="135df-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="135df-175">user.givenname</span></span> |
    | <span data-ttu-id="135df-176">lastname</span><span class="sxs-lookup"><span data-stu-id="135df-176">lastname</span></span> |<span data-ttu-id="135df-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="135df-177">user.surname</span></span> |
    | <span data-ttu-id="135df-178">email</span><span class="sxs-lookup"><span data-stu-id="135df-178">email</span></span> |<span data-ttu-id="135df-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="135df-179">user.mail</span></span> |
    
    <span data-ttu-id="135df-180">a.</span><span class="sxs-lookup"><span data-stu-id="135df-180">a.</span></span> <span data-ttu-id="135df-181">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="135df-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="135df-184">b.</span><span class="sxs-lookup"><span data-stu-id="135df-184">b.</span></span> <span data-ttu-id="135df-185">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="135df-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="135df-186">c.</span><span class="sxs-lookup"><span data-stu-id="135df-186">c.</span></span> <span data-ttu-id="135df-187">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="135df-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="135df-188">d.</span><span class="sxs-lookup"><span data-stu-id="135df-188">d.</span></span> <span data-ttu-id="135df-189">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="135df-189">Click **Ok**.</span></span>

7. <span data-ttu-id="135df-190">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="135df-190">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="135df-192">In hello **CloudPassage configurazione** fare clic su **configurare CloudPassage** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="135df-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="135df-193">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="135df-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="135df-195">In un'altra finestra del browser del sito di accesso tooyour CloudPassage aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="135df-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="135df-196">Scegliere dal menu hello in primo piano hello **impostazioni**e quindi fare clic su **amministrazione sito**.</span><span class="sxs-lookup"><span data-stu-id="135df-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configura accesso Single Sign-On][12]

11. <span data-ttu-id="135df-198">Fare clic su hello **le impostazioni di autenticazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="135df-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Configura accesso Single Sign-On][13]

12. <span data-ttu-id="135df-200">In hello **Single Sign-on Settings** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="135df-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Configura accesso Single Sign-On][14]

    <span data-ttu-id="135df-202">a.</span><span class="sxs-lookup"><span data-stu-id="135df-202">a.</span></span> <span data-ttu-id="135df-203">Selezionare la casella di controllo **Enable Single sign-on(SSO)(SSO Setup Documentation)** (Abilita Single Sign-On (SSO) (Documentazione di configurazione di SSO).</span><span class="sxs-lookup"><span data-stu-id="135df-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="135df-204">b.</span><span class="sxs-lookup"><span data-stu-id="135df-204">b.</span></span> <span data-ttu-id="135df-205">Incolla **ID entità SAML** in hello **SAML issuer URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="135df-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="135df-206">c.</span><span class="sxs-lookup"><span data-stu-id="135df-206">c.</span></span> <span data-ttu-id="135df-207">Incolla **SAML Single Sign-On Service URL** in hello **URL dell'endpoint SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="135df-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="135df-208">d.</span><span class="sxs-lookup"><span data-stu-id="135df-208">d.</span></span> <span data-ttu-id="135df-209">Incolla **Sign-Out URL** in hello **pagina di destinazione di disconnessione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="135df-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="135df-210">e.</span><span class="sxs-lookup"><span data-stu-id="135df-210">e.</span></span> <span data-ttu-id="135df-211">Aprire il certificato scaricato nel blocco note, hello copia del contenuto del certificato scaricata negli Appunti e quindi incollarlo hello **certificato X509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="135df-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="135df-212">f.</span><span class="sxs-lookup"><span data-stu-id="135df-212">f.</span></span> <span data-ttu-id="135df-213">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="135df-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="135df-214">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="135df-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="135df-215">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="135df-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="135df-216">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="135df-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="135df-217">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="135df-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="135df-218">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="135df-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="135df-220">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="135df-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="135df-221">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="135df-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="135df-223">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="135df-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="135df-225">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="135df-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="135df-227">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="135df-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="135df-229">a.</span><span class="sxs-lookup"><span data-stu-id="135df-229">a.</span></span> <span data-ttu-id="135df-230">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="135df-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="135df-231">b.</span><span class="sxs-lookup"><span data-stu-id="135df-231">b.</span></span> <span data-ttu-id="135df-232">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="135df-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="135df-233">c.</span><span class="sxs-lookup"><span data-stu-id="135df-233">c.</span></span> <span data-ttu-id="135df-234">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="135df-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="135df-235">d.</span><span class="sxs-lookup"><span data-stu-id="135df-235">d.</span></span> <span data-ttu-id="135df-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="135df-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="135df-237">Creazione di un utente test CloudPassage</span><span class="sxs-lookup"><span data-stu-id="135df-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="135df-238">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in CloudPassage toocreate.</span><span class="sxs-lookup"><span data-stu-id="135df-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="135df-239">**un utente denominato Britta Simon in CloudPassage, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="135df-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="135df-240">Sign-on tooyour **CloudPassage** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="135df-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="135df-241">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**, quindi fare clic su **amministrazione sito**.</span><span class="sxs-lookup"><span data-stu-id="135df-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Creazione di un utente test CloudPassage][22] 

3. <span data-ttu-id="135df-243">Fare clic su hello **utenti** scheda e quindi fare clic su **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="135df-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Creazione di un utente test CloudPassage][23]

4. <span data-ttu-id="135df-245">In hello **Add New User** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="135df-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![Creazione di un utente test CloudPassage][24]
    
    <span data-ttu-id="135df-247">a.</span><span class="sxs-lookup"><span data-stu-id="135df-247">a.</span></span> <span data-ttu-id="135df-248">In hello **nome** casella di testo, digitare Laura.</span><span class="sxs-lookup"><span data-stu-id="135df-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="135df-249">b.</span><span class="sxs-lookup"><span data-stu-id="135df-249">b.</span></span> <span data-ttu-id="135df-250">In hello **cognome** casella di testo, digitare Simon.</span><span class="sxs-lookup"><span data-stu-id="135df-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="135df-251">c.</span><span class="sxs-lookup"><span data-stu-id="135df-251">c.</span></span> <span data-ttu-id="135df-252">In hello **Username** casella di testo, hello **posta elettronica** casella di testo e hello **digitare di nuovo messaggio di posta elettronica** casella di testo, digitare nome utente di Laura in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="135df-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="135df-253">d.</span><span class="sxs-lookup"><span data-stu-id="135df-253">d.</span></span> <span data-ttu-id="135df-254">In **Access Type** (Tipo di accesso) selezionare **Enable Halo Portal Access** (Abilita accesso portale Halo).</span><span class="sxs-lookup"><span data-stu-id="135df-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="135df-255">e.</span><span class="sxs-lookup"><span data-stu-id="135df-255">e.</span></span> <span data-ttu-id="135df-256">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="135df-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="135df-257">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="135df-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="135df-258">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCloudPassage.</span><span class="sxs-lookup"><span data-stu-id="135df-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![Assegna utente][200] 

<span data-ttu-id="135df-260">**tooassign Britta Simon tooCloudPassage, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="135df-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="135df-261">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="135df-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="135df-263">Nell'elenco di applicazioni hello, selezionare **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="135df-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="135df-265">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="135df-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="135df-267">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="135df-267">Click **Add** button.</span></span> <span data-ttu-id="135df-268">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="135df-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="135df-270">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="135df-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="135df-271">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="135df-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="135df-272">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="135df-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="135df-273">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="135df-273">Testing single sign-on</span></span>

<span data-ttu-id="135df-274">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="135df-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="135df-275">Quando si fa clic su riquadro CloudPassage hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour CloudPassage applicazione.</span><span class="sxs-lookup"><span data-stu-id="135df-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="135df-276">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="135df-276">Additional resources</span></span>

* [<span data-ttu-id="135df-277">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="135df-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="135df-278">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="135df-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con ScaleX Enterprise | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ScaleX Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="bd44b-103">Esercitazione: Integrazione di Azure Active Directory con ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="bd44b-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="bd44b-104">In questa esercitazione, è illustrato come toointegrate ScaleX Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd44b-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd44b-105">Integrazione di ScaleX Enterprise con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="bd44b-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd44b-106">È possibile controllare in Azure AD che ha accesso tooScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="bd44b-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="bd44b-107">È possibile abilitare l'utenti tooautomatically get connesso tooScaleX Enterprise (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44b-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd44b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bd44b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd44b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="bd44b-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="bd44b-110">Informazioni sull'accesso alle applicazioni e Single Sign-On con [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd44b-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd44b-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd44b-111">Prerequisites</span></span>

<span data-ttu-id="bd44b-112">integrazione di Azure AD con ScaleX Enterprise tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="bd44b-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="bd44b-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd44b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="bd44b-114">Sottoscrizione di ScaleX Enterprise abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd44b-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd44b-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bd44b-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd44b-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="bd44b-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd44b-117">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bd44b-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="bd44b-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd44b-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd44b-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bd44b-119">Scenario description</span></span>
<span data-ttu-id="bd44b-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bd44b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd44b-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="bd44b-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd44b-122">Aggiunta di ScaleX Enterprise dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bd44b-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="bd44b-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44b-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="bd44b-124">Aggiunta di ScaleX Enterprise dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bd44b-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="bd44b-125">integrazione hello tooconfigure di ScaleX Enterprise in tooAzure Active Directory, è necessario tooadd ScaleX Enterprise dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bd44b-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd44b-126">**tooadd ScaleX Enterprise dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd44b-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd44b-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bd44b-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd44b-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd44b-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="bd44b-132">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="bd44b-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="bd44b-134">Nella casella di ricerca hello, digitare **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="bd44b-136">Nel riquadro dei risultati hello, selezionare **ScaleX Enterprise**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bd44b-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd44b-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd44b-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ScaleX Enterprise con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bd44b-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bd44b-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ScaleX Enterprise è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd44b-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="bd44b-141">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in ScaleX Enterprise richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="bd44b-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="bd44b-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bd44b-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="bd44b-143">tooconfigure e prova AD Azure single sign-on con ScaleX Enterprise, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="bd44b-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd44b-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bd44b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd44b-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd44b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd44b-146">**[Creazione di un utente test ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave un equivalente di Britta Simon in azienda ScaleX che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bd44b-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd44b-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bd44b-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd44b-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bd44b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd44b-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd44b-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in applicazioni aziendali ScaleX.</span><span class="sxs-lookup"><span data-stu-id="bd44b-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="bd44b-151">**Azure AD tooconfigure single sign-on con ScaleX Enterprise, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd44b-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd44b-152">Nel portale di Azure su hello hello **ScaleX Enterprise** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="bd44b-154">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bd44b-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="bd44b-156">In hello **ScaleX Enterprise dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="bd44b-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="bd44b-158">a.</span><span class="sxs-lookup"><span data-stu-id="bd44b-158">a.</span></span> <span data-ttu-id="bd44b-159">In hello **identificatore** casella di testo, valore di tipo hello utilizzando hello modello:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="bd44b-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="bd44b-160">b.</span><span class="sxs-lookup"><span data-stu-id="bd44b-160">b.</span></span> <span data-ttu-id="bd44b-161">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="bd44b-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="bd44b-162">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="bd44b-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="bd44b-164">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="bd44b-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bd44b-165">Non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="bd44b-165">These are not hello real values.</span></span> <span data-ttu-id="bd44b-166">Aggiornare questi valori con hello identificatore effettivo, l'URL di risposta o URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="bd44b-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="bd44b-167">Contatto [team di supporto Client Enterprise ScaleX](http://info.rescale.com/contact_sales) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="bd44b-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="bd44b-168">L'applicazione ScaleX prevede asserzioni SAML hello in un formato specifico, che richiede di toomodify attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="bd44b-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="bd44b-169">Fare clic su **visualizzare e modificare tutti gli altri attributi utente** hello tooopen casella di controllo personalizzato di attributi delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="bd44b-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="bd44b-171">a.</span><span class="sxs-lookup"><span data-stu-id="bd44b-171">a.</span></span> <span data-ttu-id="bd44b-172">Fare clic con il pulsante destro attributo hello **nome** e fare clic su Elimina.</span><span class="sxs-lookup"><span data-stu-id="bd44b-172">Right click hello attribute **name** and click delete.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="bd44b-174">b.</span><span class="sxs-lookup"><span data-stu-id="bd44b-174">b.</span></span> <span data-ttu-id="bd44b-175">Fare clic su **emailaddress** finestra Modifica attributo hello tooopen di attributo.</span><span class="sxs-lookup"><span data-stu-id="bd44b-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="bd44b-176">Modificare il relativo valore da **user.mail** troppo**User** e fare clic su Ok.</span><span class="sxs-lookup"><span data-stu-id="bd44b-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="bd44b-178">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bd44b-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="bd44b-180">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bd44b-180">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bd44b-182">In hello **configurazione aziendale ScaleX** fare clic su **configurare ScaleX Enterprise** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="bd44b-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bd44b-183">Hello copia **ID entità SAML** e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="bd44b-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="bd44b-185">tooconfigure single sign-on sul **ScaleX Enterprise** lato, sito Web aziendale di account di accesso toohello ScaleX Enterprise come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bd44b-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="bd44b-186">Fare clic sul menu hello hello superiore, destro e selezionare **amministrazione Contoso**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd44b-187">Contoso è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="bd44b-187">Contoso is just an example.</span></span> <span data-ttu-id="bd44b-188">Deve essere il nome effettivo della società.</span><span class="sxs-lookup"><span data-stu-id="bd44b-188">This should be your actual Company Name.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="bd44b-190">Selezionare **integrazioni** dal menu in alto hello e selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="bd44b-192">Completare il modulo hello come segue:</span><span class="sxs-lookup"><span data-stu-id="bd44b-192">Complete hello form as follows:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="bd44b-194">a.</span><span class="sxs-lookup"><span data-stu-id="bd44b-194">a.</span></span> <span data-ttu-id="bd44b-195">Selezionare **Create any user who can authenticate with SSO** (Crea un utente qualsiasi che può eseguire l'autenticazione con SSO).</span><span class="sxs-lookup"><span data-stu-id="bd44b-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="bd44b-196">b.</span><span class="sxs-lookup"><span data-stu-id="bd44b-196">b.</span></span> <span data-ttu-id="bd44b-197">**Provider del servizio saml**: incollare il valore di hello ***urn: oasis: nomi: tc: SAML:2.0:nameid-formato: persistente***</span><span class="sxs-lookup"><span data-stu-id="bd44b-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="bd44b-198">c.</span><span class="sxs-lookup"><span data-stu-id="bd44b-198">c.</span></span> <span data-ttu-id="bd44b-199">**Nome del campo messaggio di posta elettronica di Provider di identità in risposta ACS**: incollare il valore di hello`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="bd44b-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="bd44b-200">d.</span><span class="sxs-lookup"><span data-stu-id="bd44b-200">d.</span></span> <span data-ttu-id="bd44b-201">**ID entità EntityDescriptor Provider di identità:** hello Incolla **ID entità SAML** valore copiato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bd44b-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="bd44b-202">e.</span><span class="sxs-lookup"><span data-stu-id="bd44b-202">e.</span></span> <span data-ttu-id="bd44b-203">**Identity Provider URL SingleSignOnService:** hello Incolla **SAML Single Sign-On Service URL** da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd44b-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="bd44b-204">f.</span><span class="sxs-lookup"><span data-stu-id="bd44b-204">f.</span></span> <span data-ttu-id="bd44b-205">**Certificato X509 pubblico di Provider di identità:** certificato aprire hello X509 scaricato da hello Azure nel blocco note e incollare contenuto hello in questa casella.</span><span class="sxs-lookup"><span data-stu-id="bd44b-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="bd44b-206">Verificare che siano che non interruzioni di riga hello intermedia hello contenuto del certificato.</span><span class="sxs-lookup"><span data-stu-id="bd44b-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="bd44b-207">g.</span><span class="sxs-lookup"><span data-stu-id="bd44b-207">g.</span></span> <span data-ttu-id="bd44b-208">Controllare hello seguenti caselle di controllo: **Enabled, crittografare NameID e AuthnRequests Sign.**</span><span class="sxs-lookup"><span data-stu-id="bd44b-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="bd44b-209">h.</span><span class="sxs-lookup"><span data-stu-id="bd44b-209">h.</span></span> <span data-ttu-id="bd44b-210">Fare clic su **le impostazioni di aggiornamento SSO** impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="bd44b-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="bd44b-211">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="bd44b-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd44b-212">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="bd44b-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd44b-213">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd44b-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd44b-214">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44b-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd44b-215">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bd44b-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="bd44b-217">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd44b-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd44b-218">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bd44b-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd44b-220">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="bd44b-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd44b-222">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bd44b-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd44b-224">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bd44b-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd44b-226">a.</span><span class="sxs-lookup"><span data-stu-id="bd44b-226">a.</span></span> <span data-ttu-id="bd44b-227">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd44b-228">b.</span><span class="sxs-lookup"><span data-stu-id="bd44b-228">b.</span></span> <span data-ttu-id="bd44b-229">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd44b-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd44b-230">c.</span><span class="sxs-lookup"><span data-stu-id="bd44b-230">c.</span></span> <span data-ttu-id="bd44b-231">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd44b-232">d.</span><span class="sxs-lookup"><span data-stu-id="bd44b-232">d.</span></span> <span data-ttu-id="bd44b-233">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="bd44b-234">Creazione di un utente test ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="bd44b-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="bd44b-235">toolog agli utenti di Azure AD tooenable in tooScaleX Enterprise, è necessario eseguirne il provisioning in tooScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bd44b-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="bd44b-236">Nel caso di hello di ScaleX Enterprise, il provisioning è un'attività automatica e non manuali sono necessari passaggi.</span><span class="sxs-lookup"><span data-stu-id="bd44b-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="bd44b-237">Tutti gli utenti possono eseguire l'autenticazione con credenziali SSO verranno automaticamente eseguito il provisioning in hello ScaleX lato.</span><span class="sxs-lookup"><span data-stu-id="bd44b-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd44b-238">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd44b-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd44b-239">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo Enterprise tooScaleX di accesso utente.</span><span class="sxs-lookup"><span data-stu-id="bd44b-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Assegna utente][200] 

<span data-ttu-id="bd44b-241">**tooassign Britta Simon tooScaleX Enterprise, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd44b-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd44b-242">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bd44b-244">Nell'elenco di applicazioni hello, selezionare **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="bd44b-246">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="bd44b-248">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-248">Click **Add** button.</span></span> <span data-ttu-id="bd44b-249">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="bd44b-251">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="bd44b-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd44b-252">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd44b-253">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd44b-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="bd44b-254">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd44b-254">Testing single sign-on</span></span>

<span data-ttu-id="bd44b-255">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bd44b-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd44b-256">Fare clic su hello ScaleX Enterprise riquadro in hello Pannello di accesso, si otterranno automaticamente firmato in tooyour applicazione ScaleX aziendale.</span><span class="sxs-lookup"><span data-stu-id="bd44b-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="bd44b-257">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="bd44b-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bd44b-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bd44b-258">Additional resources</span></span>

* [<span data-ttu-id="bd44b-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd44b-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd44b-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd44b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png


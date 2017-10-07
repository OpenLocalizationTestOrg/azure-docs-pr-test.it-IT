---
title: 'Esercitazione: Integrazione di Azure Active Directory con Clever | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Clever.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="8ba06-103">Esercitazione: Integrazione di Azure Active Directory con Clever</span><span class="sxs-lookup"><span data-stu-id="8ba06-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="8ba06-104">In questa esercitazione, è illustrato come toointegrate Clever con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ba06-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ba06-105">Integrazione Clever con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8ba06-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ba06-106">È possibile controllare in Azure AD che ha accesso tooClever.</span><span class="sxs-lookup"><span data-stu-id="8ba06-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="8ba06-107">È possibile abilitare l'utenti tooautomatically get connesso tooClever (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ba06-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8ba06-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba06-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8ba06-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ba06-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ba06-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8ba06-110">Prerequisites</span></span>

<span data-ttu-id="8ba06-111">integrazione di Azure AD con Clever tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8ba06-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="8ba06-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ba06-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ba06-113">Sottoscrizione di Clever abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8ba06-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ba06-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8ba06-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ba06-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8ba06-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ba06-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8ba06-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ba06-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ba06-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ba06-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8ba06-118">Scenario description</span></span>
<span data-ttu-id="8ba06-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8ba06-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ba06-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8ba06-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ba06-121">Aggiunta di Clever dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8ba06-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="8ba06-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba06-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="8ba06-123">Aggiunta di Clever dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8ba06-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="8ba06-124">integrazione hello tooconfigure di Clever in Azure AD, è necessario tooadd Clever dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8ba06-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ba06-125">**tooadd Clever dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ba06-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba06-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8ba06-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="8ba06-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ba06-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="8ba06-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8ba06-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="8ba06-133">Nella casella di ricerca hello, digitare **Clever**selezionare **Clever** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ba06-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello intelligente](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8ba06-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba06-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8ba06-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Clever usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8ba06-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ba06-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Clever è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ba06-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="8ba06-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Clever deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8ba06-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="8ba06-139">In Clever, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8ba06-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8ba06-140">tooconfigure e prova AD Azure single sign-on con Clever, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8ba06-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ba06-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8ba06-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ba06-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ba06-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ba06-143">**[Creare un utente test intelligente](#create-a-clever-test-user)**  -toohave un equivalente di Britta Simon in Clever che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8ba06-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ba06-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8ba06-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ba06-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8ba06-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8ba06-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba06-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8ba06-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione appositamente.</span><span class="sxs-lookup"><span data-stu-id="8ba06-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="8ba06-148">**Azure AD tooconfigure single sign-on con Clever, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ba06-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba06-149">Nel portale di Azure su hello hello **Clever** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="8ba06-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8ba06-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="8ba06-153">In hello **appositamente dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ba06-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="8ba06-155">a.</span><span class="sxs-lookup"><span data-stu-id="8ba06-155">a.</span></span> <span data-ttu-id="8ba06-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8ba06-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="8ba06-157">b.</span><span class="sxs-lookup"><span data-stu-id="8ba06-157">b.</span></span> <span data-ttu-id="8ba06-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8ba06-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ba06-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8ba06-159">These values are not real.</span></span> <span data-ttu-id="8ba06-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="8ba06-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8ba06-161">Contatto [team di supporto Client intelligenti](https://clever.com/about/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="8ba06-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="8ba06-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8ba06-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="8ba06-164">Hello appositamente applicazione prevede di asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi Token SAML** configurazione.</span><span class="sxs-lookup"><span data-stu-id="8ba06-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="8ba06-165">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="8ba06-165">hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="8ba06-167">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ba06-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8ba06-168">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8ba06-168">Attribute Name</span></span>  | <span data-ttu-id="8ba06-169">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8ba06-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="8ba06-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="8ba06-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="8ba06-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8ba06-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="8ba06-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="8ba06-172">Firstname</span></span>  | <span data-ttu-id="8ba06-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8ba06-173">user.givenname</span></span> |
    | <span data-ttu-id="8ba06-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="8ba06-174">Lastname</span></span>  | <span data-ttu-id="8ba06-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="8ba06-175">user.surname</span></span> |    

    <span data-ttu-id="8ba06-176">a.</span><span class="sxs-lookup"><span data-stu-id="8ba06-176">a.</span></span> <span data-ttu-id="8ba06-177">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8ba06-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8ba06-180">b.</span><span class="sxs-lookup"><span data-stu-id="8ba06-180">b.</span></span> <span data-ttu-id="8ba06-181">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8ba06-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="8ba06-182">c.</span><span class="sxs-lookup"><span data-stu-id="8ba06-182">c.</span></span> <span data-ttu-id="8ba06-183">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8ba06-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="8ba06-184">d.</span><span class="sxs-lookup"><span data-stu-id="8ba06-184">d.</span></span> <span data-ttu-id="8ba06-185">Lasciare hello **Namespace** casella di testo vuoto.</span><span class="sxs-lookup"><span data-stu-id="8ba06-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="8ba06-186">d.</span><span class="sxs-lookup"><span data-stu-id="8ba06-186">d.</span></span> <span data-ttu-id="8ba06-187">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="8ba06-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8ba06-188">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8ba06-190">hello toogenerate **metadati** url, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ba06-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="8ba06-191">a.</span><span class="sxs-lookup"><span data-stu-id="8ba06-191">a.</span></span> <span data-ttu-id="8ba06-192">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-192">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="8ba06-194">b.</span><span class="sxs-lookup"><span data-stu-id="8ba06-194">b.</span></span> <span data-ttu-id="8ba06-195">Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8ba06-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="8ba06-197">c.</span><span class="sxs-lookup"><span data-stu-id="8ba06-197">c.</span></span> <span data-ttu-id="8ba06-198">Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="8ba06-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="8ba06-200">d.</span><span class="sxs-lookup"><span data-stu-id="8ba06-200">d.</span></span> <span data-ttu-id="8ba06-201">Ora passare pagina delle proprietà toohello **Clever** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="8ba06-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="8ba06-203">e.</span><span class="sxs-lookup"><span data-stu-id="8ba06-203">e.</span></span> <span data-ttu-id="8ba06-204">Generare hello **URL dei metadati** utilizzando hello seguente motivo:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="8ba06-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="8ba06-205">In una finestra del web browser, accedere come amministratore nel sito della società appositamente tooyour.</span><span class="sxs-lookup"><span data-stu-id="8ba06-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="8ba06-206">Nella barra degli strumenti hello, fare clic su **accesso istantaneo**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="8ba06-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="8ba06-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="8ba06-208">In hello **accesso istantaneo** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ba06-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="8ba06-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="8ba06-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="8ba06-210">a.</span><span class="sxs-lookup"><span data-stu-id="8ba06-210">a.</span></span> <span data-ttu-id="8ba06-211">Hello tipo **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="8ba06-212">Hello **URL di accesso** è un valore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8ba06-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="8ba06-213">Contatto [team di supporto Client intelligenti](https://clever.com/about/contact/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="8ba06-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="8ba06-214">b.</span><span class="sxs-lookup"><span data-stu-id="8ba06-214">b.</span></span> <span data-ttu-id="8ba06-215">Per **Identity System** (Sistema di identità) scegliere **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="8ba06-216">c.</span><span class="sxs-lookup"><span data-stu-id="8ba06-216">c.</span></span> <span data-ttu-id="8ba06-217">Hello tipo **URL dei metadati** in hello **URL dei metadati** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8ba06-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="8ba06-218">d.</span><span class="sxs-lookup"><span data-stu-id="8ba06-218">d.</span></span> <span data-ttu-id="8ba06-219">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8ba06-220">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8ba06-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ba06-221">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8ba06-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ba06-222">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ba06-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8ba06-223">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba06-223">Create an Azure AD test user</span></span>

<span data-ttu-id="8ba06-224">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ba06-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="8ba06-226">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ba06-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba06-227">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8ba06-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8ba06-229">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8ba06-231">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8ba06-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8ba06-233">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8ba06-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8ba06-235">a.</span><span class="sxs-lookup"><span data-stu-id="8ba06-235">a.</span></span> <span data-ttu-id="8ba06-236">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ba06-237">b.</span><span class="sxs-lookup"><span data-stu-id="8ba06-237">b.</span></span> <span data-ttu-id="8ba06-238">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ba06-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8ba06-239">c.</span><span class="sxs-lookup"><span data-stu-id="8ba06-239">c.</span></span> <span data-ttu-id="8ba06-240">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="8ba06-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8ba06-241">d.</span><span class="sxs-lookup"><span data-stu-id="8ba06-241">d.</span></span> <span data-ttu-id="8ba06-242">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="8ba06-243">Creare un utente di test di Clever</span><span class="sxs-lookup"><span data-stu-id="8ba06-243">Create a Clever test user</span></span>

<span data-ttu-id="8ba06-244">toolog agli utenti di Azure AD tooenable in tooClever, è necessario eseguirne il provisioning in Clever.</span><span class="sxs-lookup"><span data-stu-id="8ba06-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="8ba06-245">In caso di Clever, lavorare con [team di supporto Client intelligenti](https://clever.com/about/contact/) per aggiungere gli utenti di hello nella piattaforma appositamente hello.</span><span class="sxs-lookup"><span data-stu-id="8ba06-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="8ba06-246">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8ba06-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="8ba06-247">È possibile usare qualsiasi altro strumento di creazione utente appositamente account o le API fornite da tooprovision intelligente degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ba06-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8ba06-248">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba06-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8ba06-249">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooClever.</span><span class="sxs-lookup"><span data-stu-id="8ba06-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="8ba06-251">**tooassign Britta Simon tooClever, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8ba06-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba06-252">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8ba06-254">Nell'elenco di applicazioni hello, selezionare **Clever**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-254">In hello applications list, select **Clever**.</span></span>

    ![Hello Clever collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="8ba06-256">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="8ba06-258">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-258">Click **Add** button.</span></span> <span data-ttu-id="8ba06-259">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="8ba06-261">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8ba06-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ba06-262">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ba06-263">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8ba06-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8ba06-264">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8ba06-264">Test single sign-on</span></span>

<span data-ttu-id="8ba06-265">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8ba06-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ba06-266">Quando si fa clic sul riquadro appositamente hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour appositamente applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ba06-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="8ba06-267">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ba06-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8ba06-268">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8ba06-268">Additional resources</span></span>

* [<span data-ttu-id="8ba06-269">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ba06-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ba06-270">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ba06-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png


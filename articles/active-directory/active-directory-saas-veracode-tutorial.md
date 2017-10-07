---
title: 'Esercitazione: Integrazione di Azure Active Directory con Veracode | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Veracode.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="338b1-103">Esercitazione: Integrazione di Azure Active Directory con Veracode</span><span class="sxs-lookup"><span data-stu-id="338b1-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="338b1-104">In questa esercitazione, è illustrato come toointegrate Veracode con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="338b1-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="338b1-105">Integrazione Veracode con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="338b1-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="338b1-106">È possibile controllare in Azure AD che ha accesso tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="338b1-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="338b1-107">È possibile abilitare l'utenti tooautomatically get connesso tooVeracode (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="338b1-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="338b1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="338b1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="338b1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="338b1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="338b1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="338b1-110">Prerequisites</span></span>

<span data-ttu-id="338b1-111">integrazione di Azure AD con Veracode tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="338b1-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="338b1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="338b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="338b1-113">Sottoscrizione di Veracode abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="338b1-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="338b1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="338b1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="338b1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="338b1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="338b1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="338b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="338b1-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="338b1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="338b1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="338b1-118">Scenario description</span></span>
<span data-ttu-id="338b1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="338b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="338b1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="338b1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="338b1-121">Aggiungere Veracode dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="338b1-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="338b1-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="338b1-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="338b1-123">Aggiungere Veracode dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="338b1-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="338b1-124">integrazione hello tooconfigure di Veracode in Azure AD, è necessario tooadd Veracode dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="338b1-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="338b1-125">**tooadd Veracode dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="338b1-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="338b1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="338b1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="338b1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="338b1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="338b1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="338b1-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="338b1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="338b1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="338b1-133">Nella casella di ricerca hello, digitare **Veracode**selezionare **Veracode** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="338b1-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="338b1-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="338b1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="338b1-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Veracode usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="338b1-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="338b1-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Veracode è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="338b1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="338b1-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Veracode deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="338b1-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="338b1-139">In Veracode, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="338b1-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="338b1-140">tooconfigure e prova AD Azure single sign-on con Veracode, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="338b1-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="338b1-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="338b1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="338b1-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="338b1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="338b1-143">**[Creare un utente test Veracode](#create-a-veracode-test-user)**  -toohave un equivalente di Britta Simon in Veracode che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="338b1-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="338b1-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="338b1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="338b1-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="338b1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="338b1-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="338b1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="338b1-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Veracode.</span><span class="sxs-lookup"><span data-stu-id="338b1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="338b1-148">**Azure AD tooconfigure single sign-on con Veracode, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="338b1-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="338b1-149">Nel portale di Azure su hello hello **Veracode** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="338b1-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="338b1-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="338b1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="338b1-153">In hello **Veracode dominio e gli URL** sezione, l'utente non dispone di tooperform tutte le operazioni di applicazione hello è già pre-integrata con Azure.</span><span class="sxs-lookup"><span data-stu-id="338b1-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="338b1-155">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="338b1-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="338b1-157">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooVeracode con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="338b1-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="338b1-158">L'applicazione Veracode prevede asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi token saml** configurazione.</span><span class="sxs-lookup"><span data-stu-id="338b1-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="338b1-159">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="338b1-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="338b1-160">![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="338b1-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="338b1-161">mapping di attributi tooadd hello necessario, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="338b1-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="338b1-162">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="338b1-162">Attribute Name</span></span> | <span data-ttu-id="338b1-163">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="338b1-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="338b1-164">firstname</span><span class="sxs-lookup"><span data-stu-id="338b1-164">firstname</span></span> |<span data-ttu-id="338b1-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="338b1-165">User.givenname</span></span> |
    | <span data-ttu-id="338b1-166">lastname</span><span class="sxs-lookup"><span data-stu-id="338b1-166">lastname</span></span> |<span data-ttu-id="338b1-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="338b1-167">User.surname</span></span> |
    | <span data-ttu-id="338b1-168">email</span><span class="sxs-lookup"><span data-stu-id="338b1-168">email</span></span> |<span data-ttu-id="338b1-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="338b1-169">User.mail</span></span> |
    
    <span data-ttu-id="338b1-170">a.</span><span class="sxs-lookup"><span data-stu-id="338b1-170">a.</span></span> <span data-ttu-id="338b1-171">Per ogni riga di dati della tabella hello precedente, fare clic su **Aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="338b1-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="338b1-172">![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="338b1-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="338b1-173">![Attributi](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="338b1-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="338b1-174">b.</span><span class="sxs-lookup"><span data-stu-id="338b1-174">b.</span></span> <span data-ttu-id="338b1-175">In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="338b1-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="338b1-176">c.</span><span class="sxs-lookup"><span data-stu-id="338b1-176">c.</span></span> <span data-ttu-id="338b1-177">In hello **valore dell'attributo** casella di testo, il valore di attributo hello selezionare mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="338b1-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="338b1-178">d.</span><span class="sxs-lookup"><span data-stu-id="338b1-178">d.</span></span> <span data-ttu-id="338b1-179">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="338b1-179">Click **Ok**.</span></span>

7. <span data-ttu-id="338b1-180">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="338b1-180">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="338b1-182">In hello **Veracode configurazione** fare clic su **configurare Veracode** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="338b1-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="338b1-183">Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="338b1-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="338b1-185">In un'altra finestra del Web browser accedere al sito aziendale di Veracode come amministratore.</span><span class="sxs-lookup"><span data-stu-id="338b1-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="338b1-186">Scegliere hello menu in alto hello **impostazioni**, quindi fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="338b1-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="338b1-187">![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802911.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="338b1-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="338b1-188">Fare clic su hello **SAML** scheda.</span><span class="sxs-lookup"><span data-stu-id="338b1-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="338b1-189">In hello **impostazioni SAML organizzazione** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="338b1-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="338b1-190">![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802912.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="338b1-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="338b1-191">a.</span><span class="sxs-lookup"><span data-stu-id="338b1-191">a.</span></span>  <span data-ttu-id="338b1-192">In **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="338b1-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="338b1-193">b.</span><span class="sxs-lookup"><span data-stu-id="338b1-193">b.</span></span> <span data-ttu-id="338b1-194">il certificato scaricato dal portale di Azure, fare clic su tooupload **Scegli File**.</span><span class="sxs-lookup"><span data-stu-id="338b1-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="338b1-195">c.</span><span class="sxs-lookup"><span data-stu-id="338b1-195">c.</span></span> <span data-ttu-id="338b1-196">Selezionare **Abilita la registrazione automatica**.</span><span class="sxs-lookup"><span data-stu-id="338b1-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="338b1-197">In hello **Impostazioni registrazione automatica** sezione, eseguire hello alla procedura seguente e quindi fare clic su **salvare**:</span><span class="sxs-lookup"><span data-stu-id="338b1-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="338b1-198">![Amministrazione](./media/active-directory-saas-veracode-tutorial/ic802913.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="338b1-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="338b1-199">a.</span><span class="sxs-lookup"><span data-stu-id="338b1-199">a.</span></span> <span data-ttu-id="338b1-200">In **New User Activation** (Attivazione nuovo utente) selezionare **No Activation Required** (Nessuna attivazione richiesta).</span><span class="sxs-lookup"><span data-stu-id="338b1-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="338b1-201">b.</span><span class="sxs-lookup"><span data-stu-id="338b1-201">b.</span></span> <span data-ttu-id="338b1-202">In **User Data Updates** (Aggiornamenti dati utenti) selezionare **Preference Veracode User Data** (Dati utenti Veracode di preferenza).</span><span class="sxs-lookup"><span data-stu-id="338b1-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="338b1-203">c.</span><span class="sxs-lookup"><span data-stu-id="338b1-203">c.</span></span> <span data-ttu-id="338b1-204">Per **dettagli sugli attributi SAML**, selezionare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="338b1-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="338b1-205">**User Roles**</span><span class="sxs-lookup"><span data-stu-id="338b1-205">**User Roles**</span></span>
      * <span data-ttu-id="338b1-206">**Policy Administrator**</span><span class="sxs-lookup"><span data-stu-id="338b1-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="338b1-207">**Reviewer**</span><span class="sxs-lookup"><span data-stu-id="338b1-207">**Reviewer**</span></span>
      * <span data-ttu-id="338b1-208">**Security Lead**</span><span class="sxs-lookup"><span data-stu-id="338b1-208">**Security Lead**</span></span>
      * <span data-ttu-id="338b1-209">**Executive**</span><span class="sxs-lookup"><span data-stu-id="338b1-209">**Executive**</span></span>
      * <span data-ttu-id="338b1-210">**Submitter**</span><span class="sxs-lookup"><span data-stu-id="338b1-210">**Submitter**</span></span>
      * <span data-ttu-id="338b1-211">**Creator**</span><span class="sxs-lookup"><span data-stu-id="338b1-211">**Creator**</span></span>
      * <span data-ttu-id="338b1-212">**All Scan Types**</span><span class="sxs-lookup"><span data-stu-id="338b1-212">**All Scan Types**</span></span>
      * <span data-ttu-id="338b1-213">**Team Memberships**</span><span class="sxs-lookup"><span data-stu-id="338b1-213">**Team Memberships**</span></span>
      * <span data-ttu-id="338b1-214">**Default Team**</span><span class="sxs-lookup"><span data-stu-id="338b1-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="338b1-215">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="338b1-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="338b1-216">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="338b1-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="338b1-217">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="338b1-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="338b1-218">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="338b1-218">Create an Azure AD test user</span></span>

<span data-ttu-id="338b1-219">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="338b1-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="338b1-221">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="338b1-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="338b1-222">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="338b1-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="338b1-224">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="338b1-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="338b1-226">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="338b1-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="338b1-228">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="338b1-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="338b1-230">a.</span><span class="sxs-lookup"><span data-stu-id="338b1-230">a.</span></span> <span data-ttu-id="338b1-231">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="338b1-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="338b1-232">b.</span><span class="sxs-lookup"><span data-stu-id="338b1-232">b.</span></span> <span data-ttu-id="338b1-233">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="338b1-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="338b1-234">c.</span><span class="sxs-lookup"><span data-stu-id="338b1-234">c.</span></span> <span data-ttu-id="338b1-235">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="338b1-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="338b1-236">d.</span><span class="sxs-lookup"><span data-stu-id="338b1-236">d.</span></span> <span data-ttu-id="338b1-237">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="338b1-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="338b1-238">Creare un utente di test di Veracode</span><span class="sxs-lookup"><span data-stu-id="338b1-238">Create a Veracode test user</span></span>
<span data-ttu-id="338b1-239">In ordine tooenable Azure AD utenti toolog in Veracode, è necessario eseguirne il provisioning in Veracode.</span><span class="sxs-lookup"><span data-stu-id="338b1-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="338b1-240">Nel caso di hello di Veracode, il provisioning è un'attività automatica.</span><span class="sxs-lookup"><span data-stu-id="338b1-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="338b1-241">Non è necessario eseguire alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="338b1-241">There is no action item for you.</span></span> <span data-ttu-id="338b1-242">Gli utenti vengono creati automaticamente se necessario, durante hello primo single sign-on tentativo.</span><span class="sxs-lookup"><span data-stu-id="338b1-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="338b1-243">È possibile usare qualsiasi altro Veracode utente account strumento di creazione o le API fornite da Veracode tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="338b1-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="338b1-244">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="338b1-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="338b1-245">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="338b1-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="338b1-247">**tooassign Britta Simon tooVeracode, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="338b1-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="338b1-248">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="338b1-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="338b1-250">Nell'elenco di applicazioni hello, selezionare **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="338b1-250">In hello applications list, select **Veracode**.</span></span>

    ![collegamento Veracode Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="338b1-252">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="338b1-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="338b1-254">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="338b1-254">Click **Add** button.</span></span> <span data-ttu-id="338b1-255">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="338b1-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="338b1-257">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="338b1-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="338b1-258">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="338b1-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="338b1-259">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="338b1-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="338b1-260">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="338b1-260">Test single sign-on</span></span>

<span data-ttu-id="338b1-261">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="338b1-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="338b1-262">Quando si fa clic su riquadro Veracode hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Veracode applicazione.</span><span class="sxs-lookup"><span data-stu-id="338b1-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="338b1-263">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="338b1-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="338b1-264">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="338b1-264">Additional resources</span></span>

* [<span data-ttu-id="338b1-265">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="338b1-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="338b1-266">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="338b1-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png


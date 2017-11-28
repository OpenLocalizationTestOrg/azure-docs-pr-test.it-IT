---
title: 'Esercitazione: Integrazione di Azure Active Directory con ADP eTime | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ADP eTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="6ed50-103">Esercitazione: Integrazione di Azure Active Directory con ADP eTime</span><span class="sxs-lookup"><span data-stu-id="6ed50-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="6ed50-104">In questa esercitazione, è illustrato come eTime toointegrate ADP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ed50-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ed50-105">Integrazione ADP eTime con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6ed50-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6ed50-106">È possibile controllare in Azure AD che ha accesso tooADP eTime</span><span class="sxs-lookup"><span data-stu-id="6ed50-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="6ed50-107">È possibile abilitare l'utenti tooautomatically get connesso tooADP eTime (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed50-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ed50-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6ed50-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6ed50-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6ed50-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ed50-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6ed50-110">Prerequisites</span></span>

<span data-ttu-id="6ed50-111">integrazione di Azure AD con ADP eTime tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6ed50-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="6ed50-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ed50-113">Sottoscrizione di ADP eTime abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6ed50-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ed50-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6ed50-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ed50-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6ed50-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ed50-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6ed50-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ed50-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6ed50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ed50-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6ed50-118">Scenario description</span></span>
<span data-ttu-id="6ed50-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6ed50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ed50-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6ed50-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ed50-121">Aggiunta di eTime ADP dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6ed50-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="6ed50-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="6ed50-123">Aggiunta di eTime ADP dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6ed50-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="6ed50-124">integrazione hello tooconfigure di eTime ADP in Azure AD, è necessario tooadd ADP eTime dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6ed50-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6ed50-125">**eTime tooadd ADP dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6ed50-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed50-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6ed50-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ed50-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6ed50-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6ed50-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6ed50-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6ed50-133">Nella casella di ricerca hello, digitare **eTime ADP**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-133">In hello search box, type **ADP eTime**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="6ed50-135">Nel riquadro dei risultati hello, selezionare **ADP eTime**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6ed50-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ed50-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ed50-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ADP eTime in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6ed50-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6ed50-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ADP eTime è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ed50-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="6ed50-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in eTime ADP deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6ed50-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="6ed50-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="6ed50-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="6ed50-142">tooconfigure e prova AD Azure single sign-on con eTime ADP, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6ed50-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6ed50-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6ed50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6ed50-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6ed50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ed50-145">**[Creazione di un utente di test ADP eTime](#creating-an-adp-etime-test-user)**  -toohave un equivalente di Britta Simon in eTime ADP che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6ed50-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ed50-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6ed50-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ed50-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ed50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ed50-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ed50-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="6ed50-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="6ed50-150">**Azure AD tooconfigure single sign-on con eTime ADP, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6ed50-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed50-151">Nel portale di Azure su hello hello **ADP eTime** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6ed50-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6ed50-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="6ed50-155">In hello **eTime ADP dominio e gli URL** seguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="6ed50-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="6ed50-157">a.</span><span class="sxs-lookup"><span data-stu-id="6ed50-157">a.</span></span> <span data-ttu-id="6ed50-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="6ed50-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="6ed50-159">b.</span><span class="sxs-lookup"><span data-stu-id="6ed50-159">b.</span></span> <span data-ttu-id="6ed50-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="6ed50-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="6ed50-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="6ed50-161">These values are not hello real.</span></span> <span data-ttu-id="6ed50-162">Aggiornare questi valori con l'URL di risposta effettivo hello e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="6ed50-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="6ed50-163">Contatto [team di supporto eTime ADP](https://www.adp.com/contact-us/overview.aspx) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="6ed50-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="6ed50-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6ed50-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="6ed50-166">applicazione eTime ADP Hello prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="6ed50-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="6ed50-167">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="6ed50-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="6ed50-168">Hello attestazione nome sarà sempre **"PersonImmutableID"** e il valore di hello di cui è stato eseguito il mapping tooExtensionAttribute2 contenente hello EmployeeID dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="6ed50-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="6ed50-169">In questo caso non verrà eseguito il mapping utente hello da Azure AD tooADP eTime per hello EmployeeID, ma è possibile eseguire il mapping di questo valore diversi tooa anche in base alle impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6ed50-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="6ed50-170">Pertanto si prega di lavoro con [team di supporto eTime ADP](https://www.adp.com/contact-us/overview.aspx) toouse prima hello identificativo corretto di un utente ed eseguire il mapping di tale valore con hello **"PersonImmutableID"** attestazione.</span><span class="sxs-lookup"><span data-stu-id="6ed50-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="6ed50-172">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6ed50-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6ed50-173">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="6ed50-173">Attribute Name</span></span> | <span data-ttu-id="6ed50-174">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="6ed50-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6ed50-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="6ed50-175">PersonImmutableID</span></span> | <span data-ttu-id="6ed50-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="6ed50-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="6ed50-177">a.</span><span class="sxs-lookup"><span data-stu-id="6ed50-177">a.</span></span> <span data-ttu-id="6ed50-178">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6ed50-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6ed50-181">b.</span><span class="sxs-lookup"><span data-stu-id="6ed50-181">b.</span></span> <span data-ttu-id="6ed50-182">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6ed50-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="6ed50-183">c.</span><span class="sxs-lookup"><span data-stu-id="6ed50-183">c.</span></span> <span data-ttu-id="6ed50-184">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6ed50-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6ed50-185">d.</span><span class="sxs-lookup"><span data-stu-id="6ed50-185">d.</span></span> <span data-ttu-id="6ed50-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ed50-187">Prima di poter configurare l'asserzione SAML hello, è necessario toocontact il [team di supporto eTime ADP](https://www.adp.com/contact-us/overview.aspx) e valore hello dell'attributo dell'identificatore univoco hello per le richieste per il tenant.</span><span class="sxs-lookup"><span data-stu-id="6ed50-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="6ed50-188">È necessario l'attestazione personalizzata di hello tooconfigure valore per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6ed50-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="6ed50-189">In hello **eTime ADP configurazione** fare clic su **configurare ADP eTime** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="6ed50-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="6ed50-191">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6ed50-191">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="6ed50-193">tooconfigure single sign-on sul **ADP eTime** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto eTime ADP](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ed50-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="6ed50-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6ed50-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6ed50-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6ed50-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6ed50-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ed50-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ed50-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed50-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ed50-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6ed50-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6ed50-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6ed50-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed50-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6ed50-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ed50-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ed50-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6ed50-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ed50-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6ed50-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ed50-209">a.</span><span class="sxs-lookup"><span data-stu-id="6ed50-209">a.</span></span> <span data-ttu-id="6ed50-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ed50-211">b.</span><span class="sxs-lookup"><span data-stu-id="6ed50-211">b.</span></span> <span data-ttu-id="6ed50-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6ed50-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ed50-213">c.</span><span class="sxs-lookup"><span data-stu-id="6ed50-213">c.</span></span> <span data-ttu-id="6ed50-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6ed50-215">d.</span><span class="sxs-lookup"><span data-stu-id="6ed50-215">d.</span></span> <span data-ttu-id="6ed50-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="6ed50-217">Creazione di un utente di test di ADP eTime</span><span class="sxs-lookup"><span data-stu-id="6ed50-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="6ed50-218">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in eTime ADP toocreate.</span><span class="sxs-lookup"><span data-stu-id="6ed50-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="6ed50-219">Lavorare con [team di supporto eTime ADP](https://www.adp.com/contact-us/overview.aspx) utenti hello tooadd nell'account eTime hello ADP.</span><span class="sxs-lookup"><span data-stu-id="6ed50-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6ed50-220">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed50-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6ed50-221">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="6ed50-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6ed50-223">**tooassign Britta Simon tooADP eTime, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6ed50-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ed50-224">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6ed50-226">Nell'elenco di applicazioni hello, selezionare **eTime ADP**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="6ed50-228">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6ed50-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-230">Click **Add** button.</span></span> <span data-ttu-id="6ed50-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6ed50-233">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6ed50-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6ed50-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ed50-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6ed50-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ed50-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6ed50-236">Testing single sign-on</span></span>

<span data-ttu-id="6ed50-237">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6ed50-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6ed50-238">Quando si fa clic hello ADP eTime porzione hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour ADP eTime applicazione.</span><span class="sxs-lookup"><span data-stu-id="6ed50-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="6ed50-239">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6ed50-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6ed50-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6ed50-240">Additional resources</span></span>

* [<span data-ttu-id="6ed50-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ed50-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ed50-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ed50-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png


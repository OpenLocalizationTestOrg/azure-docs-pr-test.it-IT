---
title: 'Esercitazione: Integrazione di Azure Active Directory con Learningpool Act | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e agisce in Learningpool.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="6fa69-103">Esercitazione: Integrazione di Azure Active Directory con Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="6fa69-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="6fa69-104">In questa esercitazione, è illustrato come eseguire operazioni di Learningpool toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6fa69-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6fa69-105">Integrazione di Learningpool Act con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6fa69-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6fa69-106">È possibile controllare in Azure AD che ha accesso tooLearningpool Act</span><span class="sxs-lookup"><span data-stu-id="6fa69-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="6fa69-107">È possibile abilitare l'utenti tooautomatically get connesso tooLearningpool Act (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fa69-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6fa69-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6fa69-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6fa69-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6fa69-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fa69-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6fa69-110">Prerequisites</span></span>

<span data-ttu-id="6fa69-111">integrazione di Azure AD con Learningpool operano tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6fa69-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="6fa69-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fa69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6fa69-113">Sottoscrizione di Learningpool Act abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6fa69-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6fa69-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6fa69-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6fa69-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6fa69-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6fa69-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6fa69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6fa69-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6fa69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6fa69-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6fa69-118">Scenario description</span></span>
<span data-ttu-id="6fa69-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6fa69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6fa69-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6fa69-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6fa69-121">Aggiunta di Learningpool Act dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6fa69-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="6fa69-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fa69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="6fa69-123">Aggiunta di Learningpool Act dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6fa69-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="6fa69-124">integrazione hello tooconfigure di Learningpool Act in Azure AD, è necessario tooadd Learningpool Act dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6fa69-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6fa69-125">**tooadd Learningpool Act dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6fa69-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fa69-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6fa69-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6fa69-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6fa69-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6fa69-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6fa69-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6fa69-133">Nella casella di ricerca hello, digitare **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="6fa69-135">Nel riquadro dei risultati hello, selezionare **Learningpool Act**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6fa69-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6fa69-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fa69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6fa69-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Learningpool Act in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6fa69-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6fa69-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Learningpool Act è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fa69-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="6fa69-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Learningpool Act deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6fa69-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="6fa69-141">In Learningpool Act, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6fa69-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6fa69-142">tooconfigure e prova AD Azure single sign-on con Learningpool Act, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6fa69-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6fa69-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6fa69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6fa69-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fa69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6fa69-145">**[Creazione di un utente test Learningpool Act](#creating-a-learningpool-act-test-user)**  -toohave un equivalente di Britta Simon in Learningpool Act che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6fa69-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6fa69-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6fa69-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6fa69-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6fa69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6fa69-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fa69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6fa69-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="6fa69-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="6fa69-150">**Azure AD tooconfigure single sign-on con Learningpool Act, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6fa69-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fa69-151">Nel portale di Azure su hello hello **Learningpool Act** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6fa69-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6fa69-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="6fa69-155">In hello **Learningpool Act dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6fa69-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="6fa69-157">a.</span><span class="sxs-lookup"><span data-stu-id="6fa69-157">a.</span></span> <span data-ttu-id="6fa69-158">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="6fa69-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="6fa69-159">b.</span><span class="sxs-lookup"><span data-stu-id="6fa69-159">b.</span></span> <span data-ttu-id="6fa69-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="6fa69-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="6fa69-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="6fa69-161">These values are not real.</span></span> <span data-ttu-id="6fa69-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="6fa69-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6fa69-163">Contatto [team di supporto di Learningpool Act Client](https://www.Learningpool.com/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="6fa69-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="6fa69-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6fa69-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="6fa69-166">Applicazione di Learningpool Act prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="6fa69-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="6fa69-167">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="6fa69-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="6fa69-168">È possibile gestire i valori hello di questi attributi da hello **"Atrribute"** scheda dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6fa69-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="6fa69-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="6fa69-169">hello following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="6fa69-171">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6fa69-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6fa69-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="6fa69-172">Attribute Name</span></span> | <span data-ttu-id="6fa69-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="6fa69-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="6fa69-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="6fa69-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="6fa69-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="6fa69-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="6fa69-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="6fa69-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="6fa69-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="6fa69-177">user.givenname</span></span> |
    | <span data-ttu-id="6fa69-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="6fa69-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="6fa69-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="6fa69-179">user.mail</span></span> |    
    | <span data-ttu-id="6fa69-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="6fa69-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="6fa69-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="6fa69-181">user.surname</span></span> |
    
    <span data-ttu-id="6fa69-182">a.</span><span class="sxs-lookup"><span data-stu-id="6fa69-182">a.</span></span> <span data-ttu-id="6fa69-183">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6fa69-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6fa69-186">b.</span><span class="sxs-lookup"><span data-stu-id="6fa69-186">b.</span></span> <span data-ttu-id="6fa69-187">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6fa69-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="6fa69-188">c.</span><span class="sxs-lookup"><span data-stu-id="6fa69-188">c.</span></span> <span data-ttu-id="6fa69-189">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="6fa69-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="6fa69-190">d.</span><span class="sxs-lookup"><span data-stu-id="6fa69-190">d.</span></span> <span data-ttu-id="6fa69-191">Lasciare hello **Namespace** vuoto.</span><span class="sxs-lookup"><span data-stu-id="6fa69-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="6fa69-192">e.</span><span class="sxs-lookup"><span data-stu-id="6fa69-192">e.</span></span> <span data-ttu-id="6fa69-193">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-193">Click **Ok**.</span></span>

7. <span data-ttu-id="6fa69-194">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6fa69-194">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6fa69-196">tooconfigure single sign-on sul **Learningpool Act** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="6fa69-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="6fa69-197">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="6fa69-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6fa69-198">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6fa69-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6fa69-199">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6fa69-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6fa69-200">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6fa69-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6fa69-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fa69-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="6fa69-202">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6fa69-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6fa69-204">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6fa69-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fa69-205">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6fa69-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6fa69-207">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6fa69-209">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6fa69-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6fa69-211">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6fa69-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6fa69-213">a.</span><span class="sxs-lookup"><span data-stu-id="6fa69-213">a.</span></span> <span data-ttu-id="6fa69-214">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6fa69-215">b.</span><span class="sxs-lookup"><span data-stu-id="6fa69-215">b.</span></span> <span data-ttu-id="6fa69-216">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6fa69-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6fa69-217">c.</span><span class="sxs-lookup"><span data-stu-id="6fa69-217">c.</span></span> <span data-ttu-id="6fa69-218">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6fa69-219">d.</span><span class="sxs-lookup"><span data-stu-id="6fa69-219">d.</span></span> <span data-ttu-id="6fa69-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="6fa69-221">Creazione di un utente test di Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="6fa69-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="6fa69-222">toolog agli utenti di Azure AD tooenable in tooLearningpool Act, è necessario eseguirne il provisioning in Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="6fa69-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="6fa69-223">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="6fa69-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="6fa69-224">Gli utenti devono toobe creati il [team di supporto di Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="6fa69-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="6fa69-225">È possibile usare qualsiasi altro Learningpool Act utente account strumento di creazione o le API fornite da Learningpool Act tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="6fa69-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6fa69-226">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fa69-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6fa69-227">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="6fa69-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6fa69-229">**tooassign Britta Simon tooLearningpool Act, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6fa69-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fa69-230">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6fa69-232">Nell'elenco di applicazioni hello, selezionare **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="6fa69-234">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6fa69-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-236">Click **Add** button.</span></span> <span data-ttu-id="6fa69-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6fa69-239">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6fa69-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6fa69-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6fa69-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6fa69-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6fa69-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6fa69-242">Testing single sign-on</span></span>

<span data-ttu-id="6fa69-243">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6fa69-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6fa69-244">Quando si fa clic hello Learningpool Act riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="6fa69-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6fa69-245">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6fa69-245">Additional resources</span></span>

* [<span data-ttu-id="6fa69-246">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fa69-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6fa69-247">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fa69-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Boomi | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="fa3eb-103">Esercitazione: Integrazione di Azure Active Directory con Boomi</span><span class="sxs-lookup"><span data-stu-id="fa3eb-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="fa3eb-104">In questa esercitazione, è illustrato come toointegrate Boomi con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa3eb-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa3eb-105">Integrazione di Boomi con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fa3eb-106">È possibile controllare in Azure AD che ha accesso tooBoomi</span><span class="sxs-lookup"><span data-stu-id="fa3eb-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="fa3eb-107">È possibile abilitare l'utenti tooautomatically get connesso tooBoomi (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa3eb-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa3eb-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fa3eb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fa3eb-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa3eb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa3eb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fa3eb-110">Prerequisites</span></span>

<span data-ttu-id="fa3eb-111">integrazione di Azure AD con Boomi tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="fa3eb-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa3eb-113">Sottoscrizione di Boomi abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fa3eb-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa3eb-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa3eb-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa3eb-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa3eb-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa3eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa3eb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fa3eb-118">Scenario description</span></span>
<span data-ttu-id="fa3eb-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa3eb-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa3eb-121">Aggiunta di Boomi dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fa3eb-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="fa3eb-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa3eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="fa3eb-123">Aggiunta di Boomi dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fa3eb-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="fa3eb-124">integrazione hello tooconfigure di Boomi in Azure AD, è necessario tooadd Boomi dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fa3eb-125">**tooadd Boomi dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa3eb-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3eb-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa3eb-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fa3eb-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="fa3eb-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="fa3eb-133">Nella casella di ricerca hello, digitare **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-133">In hello search box, type **Boomi**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="fa3eb-135">Nel riquadro dei risultati hello, selezionare **Boomi**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa3eb-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa3eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa3eb-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Boomi in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fa3eb-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa3eb-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Boomi è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="fa3eb-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Boomi deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="fa3eb-141">In Boomi, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fa3eb-142">tooconfigure e prova AD Azure single sign-on con Boomi, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fa3eb-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fa3eb-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa3eb-145">**[Creazione di un utente test Boomi](#creating-a-boomi-test-user)**  -toohave un equivalente di Britta Simon in Boomi che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa3eb-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa3eb-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa3eb-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa3eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa3eb-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Boomi.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="fa3eb-150">**Azure AD tooconfigure single sign-on con Boomi, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa3eb-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3eb-151">Nel portale di Azure su hello hello **Boomi** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fa3eb-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="fa3eb-155">In hello **Boomi dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="fa3eb-157">a.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-157">a.</span></span> <span data-ttu-id="fa3eb-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="fa3eb-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="fa3eb-159">b.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-159">b.</span></span> <span data-ttu-id="fa3eb-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="fa3eb-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa3eb-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="fa3eb-161">These values are not real.</span></span> <span data-ttu-id="fa3eb-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="fa3eb-163">Contatto [team di supporto di Boomi](https://boomi.com/company/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="fa3eb-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="fa3eb-166">Applicazione di Boomi prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="fa3eb-167">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="fa3eb-168">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="fa3eb-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="fa3eb-171">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, per ogni riga nella tabella hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="fa3eb-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="fa3eb-172">Attribute Name</span></span> | <span data-ttu-id="fa3eb-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="fa3eb-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="fa3eb-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="fa3eb-174">FEDERATION_ID</span></span> | <span data-ttu-id="fa3eb-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="fa3eb-175">user.mail</span></span> |
    
    <span data-ttu-id="fa3eb-176">a.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-176">a.</span></span> <span data-ttu-id="fa3eb-177">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="fa3eb-180">b.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-180">b.</span></span> <span data-ttu-id="fa3eb-181">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="fa3eb-182">c.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-182">c.</span></span> <span data-ttu-id="fa3eb-183">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fa3eb-184">d.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-184">d.</span></span> <span data-ttu-id="fa3eb-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-185">Click **Ok**.</span></span>

6. <span data-ttu-id="fa3eb-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fa3eb-186">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="fa3eb-188">In hello **Boomi configurazione** fare clic su **configurare Boomi** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fa3eb-189">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="fa3eb-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="fa3eb-191">In un'altra finestra del Web browser accedere al sito aziendale di Boomi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="fa3eb-192">Passare troppo**nome società** e andare troppo**impostare**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="fa3eb-193">Fare clic su hello **opzioni SSO** scheda ed eseguire i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="fa3eb-195">a.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-195">a.</span></span> <span data-ttu-id="fa3eb-196">Selezionare la casella di controllo **Abilita Single Sign-On SAML**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="fa3eb-197">b.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-197">b.</span></span> <span data-ttu-id="fa3eb-198">Fare clic su **importazione** hello tooupload scaricato certificato da Azure AD troppo**Identity Provider Certificate**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="fa3eb-199">c.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-199">c.</span></span> <span data-ttu-id="fa3eb-200">In hello **Identity Provider Login URL** casella di testo, inserire il valore di hello di **SAML Single Sign-On Service URL** dalla finestra di configurazione dell'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="fa3eb-201">d.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-201">d.</span></span> <span data-ttu-id="fa3eb-202">Come **Federation Id Location** selezionare il pulsante di opzione **Federation Id is in FEDERATION_ID Attribute element**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="fa3eb-203">e.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-203">e.</span></span> <span data-ttu-id="fa3eb-204">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fa3eb-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="fa3eb-205">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="fa3eb-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fa3eb-206">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fa3eb-207">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fa3eb-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa3eb-208">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa3eb-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa3eb-209">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="fa3eb-211">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa3eb-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3eb-212">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa3eb-214">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa3eb-216">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa3eb-218">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa3eb-220">a.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-220">a.</span></span> <span data-ttu-id="fa3eb-221">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa3eb-222">b.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-222">b.</span></span> <span data-ttu-id="fa3eb-223">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa3eb-224">c.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-224">c.</span></span> <span data-ttu-id="fa3eb-225">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fa3eb-226">d.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-226">d.</span></span> <span data-ttu-id="fa3eb-227">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="fa3eb-228">Creazione di un utente test di Boomi</span><span class="sxs-lookup"><span data-stu-id="fa3eb-228">Creating a Boomi test user</span></span>

<span data-ttu-id="fa3eb-229">In ordine tooenable Azure AD utenti toolog in tooBoomi, è necessario eseguirne il provisioning in Boomi.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="fa3eb-230">Nel caso di hello di Boomi, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="fa3eb-231">tooprovision un account utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa3eb-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="fa3eb-232">Accedi tooyour sito della società Boomi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="fa3eb-233">Dopo aver effettuato l'accesso, cercare troppo**Gestione utenti** e andare troppo**utenti**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="fa3eb-234">![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="fa3eb-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="fa3eb-235">Fare clic su  **+**  icona e hello **ruoli utente di aggiungere/Gestisci** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="fa3eb-236">![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="fa3eb-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="fa3eb-237">![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="fa3eb-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="fa3eb-238">a.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-238">a.</span></span> <span data-ttu-id="fa3eb-239">In hello **indirizzo di posta elettronica utente** casella Tipo hello email dell'utente come BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="fa3eb-240">b.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-240">b.</span></span> <span data-ttu-id="fa3eb-241">In hello **nome** casella Tipo hello nome dell'utente come Laura.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="fa3eb-242">c.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-242">c.</span></span> <span data-ttu-id="fa3eb-243">In hello **cognome** casella di testo, digitare hello cognome dell'utente come Simon.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="fa3eb-244">d.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-244">d.</span></span> <span data-ttu-id="fa3eb-245">Immettere dell'utente hello **ID federazione**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="fa3eb-246">Ogni utente deve avere un ID di federazione che identifica in modo univoco l'utente hello nell'account hello.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="fa3eb-247">e.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-247">e.</span></span> <span data-ttu-id="fa3eb-248">Assegnare hello **utente Standard** utente toohello ruolo.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="fa3eb-249">Non assegnare il ruolo di amministratore hello perché in tal quest'ultimo accesso atmosfera normale, nonché l'accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="fa3eb-250">f.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-250">f.</span></span> <span data-ttu-id="fa3eb-251">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fa3eb-252">utente Hello non riceverà un messaggio di notifica iniziale contenente la password che può essere utilizzati toolog in toohello AtomSphere account perché la password viene gestita mediante il provider di identità hello.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="fa3eb-253">È possibile utilizzare qualsiasi altro Boomi utente account strumento di creazione o le API fornite da Boomi tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fa3eb-254">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa3eb-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fa3eb-255">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBoomi.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Assegna utente][200] 

<span data-ttu-id="fa3eb-257">**tooassign Britta Simon tooBoomi, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa3eb-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa3eb-258">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fa3eb-260">Nell'elenco di applicazioni hello, selezionare **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-260">In hello applications list, select **Boomi**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="fa3eb-262">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="fa3eb-264">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-264">Click **Add** button.</span></span> <span data-ttu-id="fa3eb-265">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="fa3eb-267">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fa3eb-268">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa3eb-269">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa3eb-270">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fa3eb-270">Testing single sign-on</span></span>

<span data-ttu-id="fa3eb-271">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fa3eb-272">Quando si fa clic su riquadro Boomi hello in hello Pannello di accesso, è necessario ottenere applicazione Boomi tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="fa3eb-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa3eb-273">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fa3eb-273">Additional resources</span></span>

* [<span data-ttu-id="fa3eb-274">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa3eb-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa3eb-275">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa3eb-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png


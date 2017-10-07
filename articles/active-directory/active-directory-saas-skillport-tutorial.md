---
title: 'Esercitazione: Integrazione di Azure Active Directory con Skillport | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Skillport.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="777a4-103">Esercitazione: Integrazione di Azure Active Directory con Skillport</span><span class="sxs-lookup"><span data-stu-id="777a4-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="777a4-104">In questa esercitazione, è illustrato come toointegrate Skillport con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="777a4-104">In this tutorial, you learn how toointegrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="777a4-105">Integrazione Skillport con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="777a4-105">Integrating Skillport with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="777a4-106">È possibile controllare in Azure AD che ha accesso tooSkillport</span><span class="sxs-lookup"><span data-stu-id="777a4-106">You can control in Azure AD who has access tooSkillport</span></span>
- <span data-ttu-id="777a4-107">È possibile abilitare l'utenti tooautomatically get connesso tooSkillport (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="777a4-107">You can enable your users tooautomatically get signed-on tooSkillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="777a4-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="777a4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="777a4-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="777a4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="777a4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="777a4-110">Prerequisites</span></span>

<span data-ttu-id="777a4-111">integrazione di Azure AD con Skillport tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="777a4-111">tooconfigure Azure AD integration with Skillport, you need hello following items:</span></span>

- <span data-ttu-id="777a4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="777a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="777a4-113">Sottoscrizione di Skillport abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="777a4-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="777a4-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="777a4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="777a4-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="777a4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="777a4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="777a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="777a4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="777a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="777a4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="777a4-118">Scenario description</span></span>
<span data-ttu-id="777a4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="777a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="777a4-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="777a4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="777a4-121">Aggiunta di Skillport dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="777a4-121">Adding Skillport from hello gallery</span></span>
2. <span data-ttu-id="777a4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="777a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-hello-gallery"></a><span data-ttu-id="777a4-123">Aggiunta di Skillport dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="777a4-123">Adding Skillport from hello gallery</span></span>
<span data-ttu-id="777a4-124">integrazione hello tooconfigure di Skillport in Azure AD, è necessario tooadd Skillport dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="777a4-124">tooconfigure hello integration of Skillport into Azure AD, you need tooadd Skillport from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="777a4-125">**tooadd Skillport dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="777a4-125">**tooadd Skillport from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="777a4-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="777a4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="777a4-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="777a4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="777a4-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="777a4-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="777a4-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="777a4-131">Click **New Application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="777a4-133">Nella casella di ricerca hello, digitare **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="777a4-133">In hello search box, type **Skillport**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="777a4-135">Nel riquadro dei risultati hello, selezionare **Skillport**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="777a4-135">In hello results panel, select **Skillport**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="777a4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="777a4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="777a4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Skillport usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="777a4-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="777a4-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Skillport è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="777a4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skillport is tooa user in Azure AD.</span></span> <span data-ttu-id="777a4-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Skillport deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="777a4-140">In other words, a link relationship between an Azure AD user and hello related user in Skillport needs toobe established.</span></span>

<span data-ttu-id="777a4-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Skillport.</span><span class="sxs-lookup"><span data-stu-id="777a4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Skillport.</span></span>

<span data-ttu-id="777a4-142">tooconfigure e prova AD Azure single sign-on con Skillport, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="777a4-142">tooconfigure and test Azure AD single sign-on with Skillport, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="777a4-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="777a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="777a4-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="777a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="777a4-145">**[Creazione di un utente test Skillport](#creating-a-skillport-test-user)**  -toohave un equivalente di Britta Simon in Skillport che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="777a4-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - toohave a counterpart of Britta Simon in Skillport that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="777a4-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="777a4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="777a4-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="777a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="777a4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="777a4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="777a4-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Skillport.</span><span class="sxs-lookup"><span data-stu-id="777a4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="777a4-150">**Azure AD tooconfigure single sign-on con Skillport, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="777a4-150">**tooconfigure Azure AD single sign-on with Skillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="777a4-151">Nel portale di Azure su hello hello **Skillport** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="777a4-151">In hello Azure  portal, on hello **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="777a4-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="777a4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="777a4-155">In hello **Skillport dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="777a4-155">On hello **Skillport Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="777a4-157">a.</span><span class="sxs-lookup"><span data-stu-id="777a4-157">a.</span></span> <span data-ttu-id="777a4-158">In hello **Sign-on URL** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="777a4-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span>
      
      <span data-ttu-id="777a4-159">Data center UE: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="777a4-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="777a4-160">Data center USA: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="777a4-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="777a4-161">b.</span><span class="sxs-lookup"><span data-stu-id="777a4-161">b.</span></span> <span data-ttu-id="777a4-162">In hello **URL di risposta** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="777a4-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span>
    
      <span data-ttu-id="777a4-163">Data center UE: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="777a4-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="777a4-164">Data center USA: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="777a4-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="777a4-165">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="777a4-165">These values are not hello real.</span></span> <span data-ttu-id="777a4-166">Aggiornare questi valori con l'URL di risposta effettivo hello e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="777a4-166">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="777a4-167">Contatto [team di supporto Skillport Client](https://www.skillsoft.com/contact.asp) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="777a4-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) tooget these values.</span></span>
 
4. <span data-ttu-id="777a4-168">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="777a4-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="777a4-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="777a4-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="777a4-172">tooconfigure single sign-on sul **Skillport** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="777a4-172">tooconfigure single sign-on on **Skillport** side, you need toosend hello downloaded **Metadata XML** too[Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="777a4-173">Verrà impostata hello toohave connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="777a4-173">They will set it up toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="777a4-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="777a4-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="777a4-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="777a4-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="777a4-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="777a4-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="777a4-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="777a4-178">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="777a4-180">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="777a4-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="777a4-182">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="777a4-182">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="777a4-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="777a4-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="777a4-186">a.</span><span class="sxs-lookup"><span data-stu-id="777a4-186">a.</span></span> <span data-ttu-id="777a4-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="777a4-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="777a4-188">b.</span><span class="sxs-lookup"><span data-stu-id="777a4-188">b.</span></span> <span data-ttu-id="777a4-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="777a4-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="777a4-190">c.</span><span class="sxs-lookup"><span data-stu-id="777a4-190">c.</span></span> <span data-ttu-id="777a4-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="777a4-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="777a4-192">d.</span><span class="sxs-lookup"><span data-stu-id="777a4-192">d.</span></span> <span data-ttu-id="777a4-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="777a4-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="777a4-194">Creazione di un utente di test di Skillport</span><span class="sxs-lookup"><span data-stu-id="777a4-194">Creating a Skillport test user</span></span>

<span data-ttu-id="777a4-195">Utente di prova Skillport toocreate ordine, è necessario toocontact [team di supporto Skillport](https://www.skillsoft.com/contact.asp) in cui più scenari aziendali in base a requisiti toohello dell'utente finale.</span><span class="sxs-lookup"><span data-stu-id="777a4-195">In order toocreate Skillport test user, you need toocontact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according toohello requirement of end user.</span></span> <span data-ttu-id="777a4-196">È necessario configurarlo dopo discussione con gli utenti di hello.</span><span class="sxs-lookup"><span data-stu-id="777a4-196">They will configure it after discussion with hello users.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="777a4-197">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="777a4-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="777a4-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSkillport.</span><span class="sxs-lookup"><span data-stu-id="777a4-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkillport.</span></span>

![Assegna utente][200] 

<span data-ttu-id="777a4-200">**tooassign Britta Simon tooSkillport, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="777a4-200">**tooassign Britta Simon tooSkillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="777a4-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="777a4-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="777a4-203">Nell'elenco di applicazioni hello, selezionare **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="777a4-203">In hello applications list, select **Skillport**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="777a4-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="777a4-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="777a4-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="777a4-207">Click **Add** button.</span></span> <span data-ttu-id="777a4-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="777a4-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="777a4-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="777a4-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="777a4-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="777a4-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="777a4-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="777a4-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="777a4-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="777a4-213">Testing single sign-on</span></span>

<span data-ttu-id="777a4-214">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="777a4-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="777a4-215">Quando si fa clic su riquadro Skillport hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Skillport applicazione.</span><span class="sxs-lookup"><span data-stu-id="777a4-215">When you click hello Skillport tile in hello Access Panel, you should get automatically signed-on tooyour Skillport application.</span></span>
<span data-ttu-id="777a4-216">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="777a4-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="777a4-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="777a4-217">Additional resources</span></span>

* [<span data-ttu-id="777a4-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="777a4-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="777a4-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="777a4-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png


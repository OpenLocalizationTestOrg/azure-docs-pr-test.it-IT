---
title: 'Esercitazione: Integrazione di Azure Active Directory con Concur | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="c9633-103">Esercitazione: Integrazione di Azure Active Directory con Concur</span><span class="sxs-lookup"><span data-stu-id="c9633-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="c9633-104">In questa esercitazione, è illustrato come toointegrate Concur con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9633-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9633-105">Integrazione di Concur con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c9633-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c9633-106">È possibile controllare in Azure AD che ha accesso tooConcur</span><span class="sxs-lookup"><span data-stu-id="c9633-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="c9633-107">È possibile abilitare l'utenti tooautomatically get connesso tooConcur (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9633-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9633-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c9633-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c9633-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione di app SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9633-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9633-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c9633-110">Prerequisites</span></span>

<span data-ttu-id="c9633-111">integrazione di Azure AD con Concur tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c9633-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="c9633-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9633-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9633-113">Sottoscrizione di Concur abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c9633-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9633-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c9633-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9633-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="c9633-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9633-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c9633-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9633-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9633-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9633-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c9633-118">Scenario description</span></span>
<span data-ttu-id="c9633-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c9633-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9633-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c9633-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9633-121">Aggiunta di Concur dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c9633-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="c9633-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9633-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="c9633-123">configurazione di Hello della sottoscrizione di Concur per SSO federato tramite SAML è un'attività separata, che è necessario contattare [team di supporto Client di Concur](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="c9633-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="c9633-124">Aggiunta di Concur dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c9633-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="c9633-125">integrazione hello tooconfigure di Concur in Azure AD, è necessario tooadd Concur dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c9633-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9633-126">**tooadd Concur dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c9633-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9633-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c9633-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9633-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c9633-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c9633-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c9633-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c9633-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c9633-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c9633-134">Nella casella di ricerca hello, digitare **Concur**.</span><span class="sxs-lookup"><span data-stu-id="c9633-134">In hello search box, type **Concur**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="c9633-136">Nel riquadro dei risultati hello, selezionare **Concur**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c9633-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9633-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9633-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9633-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Concur usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c9633-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c9633-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Concur è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9633-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="c9633-141">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Concur richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="c9633-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="c9633-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Concur.</span><span class="sxs-lookup"><span data-stu-id="c9633-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="c9633-143">tooconfigure e test Azure single sign-on AD con Concur, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="c9633-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c9633-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c9633-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c9633-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9633-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9633-146">**[Creazione di un utente test Concur](#creating-a-concur-test-user)**  -toohave un equivalente di Britta Simon in Concur che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c9633-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9633-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c9633-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9633-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="c9633-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9633-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9633-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9633-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Concur.</span><span class="sxs-lookup"><span data-stu-id="c9633-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="c9633-151">**Azure AD tooconfigure single sign-on con Concur, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c9633-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9633-152">Nel portale di Azure su hello hello **Concur** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c9633-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c9633-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c9633-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="c9633-156">In hello **Concur dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c9633-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="c9633-158">a.</span><span class="sxs-lookup"><span data-stu-id="c9633-158">a.</span></span> <span data-ttu-id="c9633-159">In hello **URL di accesso** casella di testo, valore di tipo hello utilizzando hello modello:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="c9633-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="c9633-160">b.</span><span class="sxs-lookup"><span data-stu-id="c9633-160">b.</span></span> <span data-ttu-id="c9633-161">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="c9633-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9633-162">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="c9633-162">These values are not hello real.</span></span> <span data-ttu-id="c9633-163">Aggiornamento di questi valori con hello effettivo accesso URL e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="c9633-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="c9633-164">Contatto [team di supporto Client di Concur](https://www.concur.co.in/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="c9633-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="c9633-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c9633-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="c9633-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c9633-167">Click **Save** button.</span></span>

    <span data-ttu-id="c9633-168">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="c9633-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="c9633-169">tooconfigure single sign-on sul **Concur** lato, è necessario hello toosend scaricato **Metadata XML** tooConcur supporto.</span><span class="sxs-lookup"><span data-stu-id="c9633-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="c9633-170">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="c9633-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c9633-171">configurazione di Hello della sottoscrizione di Concur per SSO federato tramite SAML è un'attività separata, che è necessario contattare [team di supporto Client di Concur](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="c9633-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="c9633-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="c9633-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c9633-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c9633-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c9633-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9633-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9633-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9633-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9633-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9633-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c9633-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c9633-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9633-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c9633-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9633-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c9633-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9633-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c9633-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9633-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c9633-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9633-187">a.</span><span class="sxs-lookup"><span data-stu-id="c9633-187">a.</span></span> <span data-ttu-id="c9633-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9633-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9633-189">b.</span><span class="sxs-lookup"><span data-stu-id="c9633-189">b.</span></span> <span data-ttu-id="c9633-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c9633-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9633-191">c.</span><span class="sxs-lookup"><span data-stu-id="c9633-191">c.</span></span> <span data-ttu-id="c9633-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="c9633-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c9633-193">d.</span><span class="sxs-lookup"><span data-stu-id="c9633-193">d.</span></span> <span data-ttu-id="c9633-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9633-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="c9633-195">Creazione di un utente di test di Concur</span><span class="sxs-lookup"><span data-stu-id="c9633-195">Creating a Concur test user</span></span>

<span data-ttu-id="c9633-196">L'applicazione supporta hello immediatamente in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c9633-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c9633-197">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9633-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c9633-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooConcur.</span><span class="sxs-lookup"><span data-stu-id="c9633-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c9633-200">**tooassign Britta Simon tooConcur, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c9633-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9633-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c9633-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c9633-203">Nell'elenco di applicazioni hello, selezionare **Concur**.</span><span class="sxs-lookup"><span data-stu-id="c9633-203">In hello applications list, select **Concur**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="c9633-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c9633-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c9633-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c9633-207">Click **Add** button.</span></span> <span data-ttu-id="c9633-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c9633-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c9633-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c9633-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c9633-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c9633-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9633-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c9633-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9633-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c9633-213">Testing single sign-on</span></span>

<span data-ttu-id="c9633-214">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c9633-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c9633-215">Quando si fa clic su riquadro Concur hello in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione di Concur.</span><span class="sxs-lookup"><span data-stu-id="c9633-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="c9633-216">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9633-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c9633-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c9633-217">Additional resources</span></span>

* [<span data-ttu-id="c9633-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9633-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9633-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9633-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c9633-220">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="c9633-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png


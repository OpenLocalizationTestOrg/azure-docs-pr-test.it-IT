---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="e870a-103">Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="e870a-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="e870a-104">In questa esercitazione, è illustrato come toointegrate Salesforce Sandbox con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e870a-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e870a-105">Integrazione di Salesforce Sandbox con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e870a-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e870a-106">È possibile controllare in Azure AD che ha accesso tooSalesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="e870a-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="e870a-107">È possibile abilitare l'utenti tooautomatically get connesso tooSalesforce Sandbox (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870a-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e870a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e870a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e870a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e870a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e870a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e870a-110">Prerequisites</span></span>

<span data-ttu-id="e870a-111">integrazione di Azure AD con Salesforce Sandbox tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e870a-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="e870a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e870a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e870a-113">Sottoscrizione di Salesforce Sandbox abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e870a-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e870a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e870a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e870a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e870a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e870a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e870a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e870a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e870a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e870a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e870a-118">Scenario description</span></span>
<span data-ttu-id="e870a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e870a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e870a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e870a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e870a-121">Aggiunta di Salesforce Sandbox dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e870a-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="e870a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="e870a-123">Aggiunta di Salesforce Sandbox dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e870a-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="e870a-124">integrazione hello tooconfigure di Salesforce Sandbox in Azure AD, è necessario tooadd Salesforce Sandbox dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e870a-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e870a-125">**tooadd Salesforce Sandbox dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e870a-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e870a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e870a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e870a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e870a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e870a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e870a-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e870a-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="e870a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e870a-133">Nella casella di ricerca hello, digitare **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="e870a-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="e870a-135">Nel riquadro dei risultati hello, selezionare **Salesforce Sandbox**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e870a-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e870a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e870a-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Salesforce Sandbox in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e870a-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e870a-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Salesforce Sandbox è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e870a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="e870a-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Salesforce Sandbox richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e870a-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="e870a-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e870a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="e870a-142">tooconfigure e test Azure single sign-on AD con Salesforce Sandbox, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e870a-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e870a-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e870a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e870a-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e870a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e870a-145">**[Creazione di un utente test Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave un equivalente di Britta Simon in Salesforce Sandbox con rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e870a-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e870a-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e870a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e870a-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e870a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e870a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e870a-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e870a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="e870a-150">**Azure AD tooconfigure single sign-on con Salesforce Sandbox, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e870a-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="e870a-151">Nel portale di Azure su hello hello **Salesforce Sandbox** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e870a-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e870a-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e870a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="e870a-155">In hello **URL e dominio di Salesforce Sandbox** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e870a-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="e870a-157">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e870a-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e870a-158">Questo valore non è hello reale.</span><span class="sxs-lookup"><span data-stu-id="e870a-158">This value is not hello real.</span></span> <span data-ttu-id="e870a-159">Aggiornare questo valore con URL hello effettivo Sign-on. Contatto [team di supporto Client di Sandbox Salesforce](https://help.salesforce.com/support) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="e870a-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="e870a-160">Se già stato configurato single sign-on per un'altra istanza di Salesforce Sandbox nella directory, quindi è necessario configurare anche hello **identificatore** toohave hello stesso valore di hello **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="e870a-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="e870a-161">Hello **identificatore** trovato controllando hello **Mostra impostazioni avanzate** casella di controllo hello **Configura URL App** pagina della finestra di dialogo hello</span><span class="sxs-lookup"><span data-stu-id="e870a-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="e870a-162">In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="e870a-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="e870a-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e870a-164">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e870a-166">In hello **Salesforce Sandbox configurazione** fare clic su **configurare Salesforce Sandbox** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="e870a-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e870a-167">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="e870a-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="e870a-168">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="e870a-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="e870a-169">Aprire una nuova scheda nel browser e accedere tooyour account amministratore Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e870a-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="e870a-170">Scegliere dal menu hello in primo piano hello **installazione**.</span><span class="sxs-lookup"><span data-stu-id="e870a-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="e870a-172">Nel riquadro di spostamento hello hello sinistra, fare clic su **controlli di sicurezza**, quindi fare clic su **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="e870a-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="e870a-174">Nella sezione Impostazioni di Single Sign-On hello, eseguire hello alla procedura seguente: ![configurare Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="e870a-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="e870a-175">a.</span><span class="sxs-lookup"><span data-stu-id="e870a-175">a.</span></span>  <span data-ttu-id="e870a-176">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="e870a-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="e870a-177">b.</span><span class="sxs-lookup"><span data-stu-id="e870a-177">b.</span></span>  <span data-ttu-id="e870a-178">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="e870a-178">Click **New**.</span></span>

12. <span data-ttu-id="e870a-179">Nella sezione SAML Single Sign-On Settings hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e870a-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="e870a-181">casella di testo Nome hello a.In, nome della configurazione hello hello del tipo (ad esempio: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="e870a-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="e870a-182">b.</span><span class="sxs-lookup"><span data-stu-id="e870a-182">b.</span></span> <span data-ttu-id="e870a-183">Incolla **ID entità SMAL** valore in hello **dell'autorità di certificazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e870a-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="e870a-184">c.</span><span class="sxs-lookup"><span data-stu-id="e870a-184">c.</span></span> <span data-ttu-id="e870a-185">In hello **Id entità** casella tipo **https://test.salesforce.com** se hello prima istanza di Salesforce Sandbox, che si sta aggiungendo tooyour directory.</span><span class="sxs-lookup"><span data-stu-id="e870a-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="e870a-186">Se esiste già un'istanza di Salesforce Sandbox, quindi per hello **ID entità** tipo di hello **URL di accesso**, che deve essere nel formato seguente:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e870a-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="e870a-187">d.</span><span class="sxs-lookup"><span data-stu-id="e870a-187">d.</span></span> <span data-ttu-id="e870a-188">Fare clic su **Sfoglia** hello tooupload scaricato certificato.</span><span class="sxs-lookup"><span data-stu-id="e870a-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="e870a-189">e.</span><span class="sxs-lookup"><span data-stu-id="e870a-189">e.</span></span> <span data-ttu-id="e870a-190">Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**.</span><span class="sxs-lookup"><span data-stu-id="e870a-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="e870a-191">f.</span><span class="sxs-lookup"><span data-stu-id="e870a-191">f.</span></span> <span data-ttu-id="e870a-192">Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentifier hello di hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="e870a-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="e870a-193">g.</span><span class="sxs-lookup"><span data-stu-id="e870a-193">g.</span></span> <span data-ttu-id="e870a-194">Incolla **URL servizio Single Sign-On** in hello **Identity Provider Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e870a-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="e870a-195">h.</span><span class="sxs-lookup"><span data-stu-id="e870a-195">h.</span></span> <span data-ttu-id="e870a-196">SFDC non supporta la disconnessione SAML.</span><span class="sxs-lookup"><span data-stu-id="e870a-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="e870a-197">In alternativa, incollare 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' in hello **Identity Provider Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e870a-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="e870a-198">i.</span><span class="sxs-lookup"><span data-stu-id="e870a-198">i.</span></span> <span data-ttu-id="e870a-199">In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="e870a-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="e870a-200">j.</span><span class="sxs-lookup"><span data-stu-id="e870a-200">j.</span></span> <span data-ttu-id="e870a-201">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e870a-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="e870a-202">Abilitare il dominio</span><span class="sxs-lookup"><span data-stu-id="e870a-202">Enable your domain</span></span>
<span data-ttu-id="e870a-203">In questa sezione si presuppone che sia già stato creato un dominio.</span><span class="sxs-lookup"><span data-stu-id="e870a-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="e870a-204">Per altre informazioni, vedere [Definizione del nome di dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="e870a-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="e870a-205">**tooenable il dominio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e870a-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="e870a-206">Nel riquadro di spostamento a sinistra di hello, fare clic su **Gestione dominio**, quindi fare clic su **risorse del dominio.**</span><span class="sxs-lookup"><span data-stu-id="e870a-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="e870a-208">Assicurarsi che il dominio sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="e870a-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="e870a-209">In hello **Login Page Settings** fare clic su **modifica**, quindi, come **servizio di autenticazione**, selezionare il nome di hello di hello impostazione SAML Single Sign-On da hello precedente sezione e infine fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e870a-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="e870a-211">Non appena si dispone di un dominio configurato, gli utenti devono usare Salesforce sandbox di hello dominio URL toologin toohello.</span><span class="sxs-lookup"><span data-stu-id="e870a-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="e870a-212">valore di hello tooget dell'URL di hello, selezionare il profilo SSO hello creato nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e870a-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="e870a-213">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="e870a-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e870a-214">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="e870a-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e870a-215">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e870a-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e870a-216">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870a-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="e870a-217">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e870a-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e870a-219">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e870a-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e870a-220">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e870a-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e870a-222">elenco di hello toodisplay utenti andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e870a-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e870a-224">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e870a-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e870a-226">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e870a-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e870a-228">a.</span><span class="sxs-lookup"><span data-stu-id="e870a-228">a.</span></span> <span data-ttu-id="e870a-229">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e870a-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e870a-230">b.</span><span class="sxs-lookup"><span data-stu-id="e870a-230">b.</span></span> <span data-ttu-id="e870a-231">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e870a-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e870a-232">c.</span><span class="sxs-lookup"><span data-stu-id="e870a-232">c.</span></span> <span data-ttu-id="e870a-233">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="e870a-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e870a-234">d.</span><span class="sxs-lookup"><span data-stu-id="e870a-234">d.</span></span> <span data-ttu-id="e870a-235">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e870a-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="e870a-236">Creazione di un utente test di Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="e870a-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="e870a-237">In questa sezione si crea un utente di nome Britta Simon in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e870a-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="e870a-238">Salesforce Sandbox supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e870a-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="e870a-239">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e870a-239">There is no action item for you in this section.</span></span> <span data-ttu-id="e870a-240">Se un utente non esiste già nell'ambiente Salesforce Sandbox, viene creato uno nuovo quando si tenta di tooaccess Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e870a-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e870a-241">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e870a-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e870a-242">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e870a-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e870a-244">**tooassign Britta Simon tooSalesforce Sandbox, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e870a-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="e870a-245">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e870a-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e870a-247">Nell'elenco di applicazioni hello, selezionare **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="e870a-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="e870a-249">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e870a-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e870a-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e870a-251">Click **Add** button.</span></span> <span data-ttu-id="e870a-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e870a-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e870a-254">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="e870a-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e870a-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e870a-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e870a-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e870a-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e870a-257">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e870a-257">Testing single sign-on</span></span>

<span data-ttu-id="e870a-258">Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="e870a-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="e870a-259">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e870a-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e870a-260">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e870a-260">Additional resources</span></span>

* [<span data-ttu-id="e870a-261">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e870a-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e870a-262">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e870a-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e870a-263">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="e870a-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png


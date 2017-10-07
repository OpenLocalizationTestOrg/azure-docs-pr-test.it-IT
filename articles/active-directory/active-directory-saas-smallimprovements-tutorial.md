---
title: 'Esercitazione: Integrazione di Azure Active Directory con Small Improvements | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e i miglioramenti di piccole dimensioni.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="415aa-103">Esercitazione: Integrazione di Azure Active Directory con Small Improvements</span><span class="sxs-lookup"><span data-stu-id="415aa-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="415aa-104">In questa esercitazione, è illustrato come toointegrate piccoli miglioramenti con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="415aa-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="415aa-105">Miglioramenti di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="415aa-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="415aa-106">È possibile controllare in Azure AD che ha accesso tooSmall miglioramenti</span><span class="sxs-lookup"><span data-stu-id="415aa-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="415aa-107">È possibile abilitare l'utenti tooautomatically get connesso tooSmall miglioramenti (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="415aa-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="415aa-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="415aa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="415aa-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="415aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="415aa-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="415aa-110">Prerequisites</span></span>

<span data-ttu-id="415aa-111">tooconfigure integrazione di Azure AD con miglioramenti di piccole dimensioni, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="415aa-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="415aa-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="415aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="415aa-113">Sottoscrizione di Small Improvements abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="415aa-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="415aa-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="415aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="415aa-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="415aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="415aa-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="415aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="415aa-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="415aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="415aa-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="415aa-118">Scenario description</span></span>
<span data-ttu-id="415aa-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="415aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="415aa-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="415aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="415aa-121">Aggiunta di piccoli miglioramenti dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="415aa-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="415aa-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="415aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="415aa-123">Aggiunta di piccoli miglioramenti dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="415aa-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="415aa-124">integrazione hello tooconfigure di piccoli miglioramenti in Azure AD, è necessario tooadd piccoli miglioramenti dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="415aa-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="415aa-125">**tooadd piccoli miglioramenti dalla raccolta hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="415aa-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="415aa-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="415aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="415aa-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="415aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="415aa-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="415aa-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="415aa-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="415aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="415aa-133">Nella casella di ricerca hello, digitare **piccoli miglioramenti**.</span><span class="sxs-lookup"><span data-stu-id="415aa-133">In hello search box, type **Small Improvements**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="415aa-135">Nel riquadro dei risultati hello, selezionare **piccoli miglioramenti**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="415aa-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="415aa-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="415aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="415aa-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Small Improvements con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="415aa-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="415aa-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello piccoli miglioramenti è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="415aa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="415aa-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello piccoli miglioramenti deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="415aa-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="415aa-141">Miglioramenti di piccole dimensioni, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="415aa-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="415aa-142">tooconfigure e test Azure AD single sign-on con miglioramenti di piccole dimensioni, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="415aa-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="415aa-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="415aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="415aa-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="415aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="415aa-145">**[Creazione di un utente di test di piccoli miglioramenti](#creating-a-small-improvements-test-user)**  -toohave un equivalente di Britta Simon piccoli miglioramenti che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="415aa-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="415aa-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="415aa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="415aa-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="415aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="415aa-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="415aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="415aa-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione piccoli miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="415aa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="415aa-150">**Azure AD tooconfigure single sign-on con piccoli miglioramenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="415aa-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="415aa-151">Nel portale di Azure su hello hello **piccoli miglioramenti** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="415aa-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="415aa-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="415aa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="415aa-155">In hello **piccoli miglioramenti dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="415aa-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="415aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="415aa-157">a.</span></span> <span data-ttu-id="415aa-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="415aa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="415aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="415aa-159">b.</span></span> <span data-ttu-id="415aa-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="415aa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="415aa-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="415aa-161">These values are not real.</span></span> <span data-ttu-id="415aa-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="415aa-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="415aa-163">Contatto [team di supporto Client i miglioramenti di piccole dimensioni](mailto:support@small-improvements.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="415aa-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="415aa-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="415aa-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="415aa-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="415aa-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="415aa-168">In hello **piccoli miglioramenti configurazione** fare clic su **configurare piccoli miglioramenti** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="415aa-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="415aa-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="415aa-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="415aa-171">In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour piccoli miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="415aa-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="415aa-172">Dalla pagina dashboard principale hello, fare clic su **amministrazione** pulsante a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="415aa-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="415aa-174">Fare clic su hello **SAML SSO** pulsante **integrazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="415aa-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="415aa-176">Nella pagina di installazione SSO hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="415aa-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="415aa-178">a.</span><span class="sxs-lookup"><span data-stu-id="415aa-178">a.</span></span> <span data-ttu-id="415aa-179">In hello **HTTP Endpoint** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="415aa-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="415aa-180">b.</span><span class="sxs-lookup"><span data-stu-id="415aa-180">b.</span></span> <span data-ttu-id="415aa-181">Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **x509 certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="415aa-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="415aa-182">c.</span><span class="sxs-lookup"><span data-stu-id="415aa-182">c.</span></span> <span data-ttu-id="415aa-183">Se si desidera toohave SSO e l'account di accesso autenticazione opzione modulo disponibile per gli utenti, quindi controllare hello **abilitare l'accesso tramite account di accesso e password troppo** opzione.</span><span class="sxs-lookup"><span data-stu-id="415aa-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="415aa-184">d.</span><span class="sxs-lookup"><span data-stu-id="415aa-184">d.</span></span> <span data-ttu-id="415aa-185">Immettere pulsante di accesso SSO hello di tooName di hello valore appropriato in hello **richiesta SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="415aa-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="415aa-186">e.</span><span class="sxs-lookup"><span data-stu-id="415aa-186">e.</span></span> <span data-ttu-id="415aa-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="415aa-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="415aa-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="415aa-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="415aa-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="415aa-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="415aa-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="415aa-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="415aa-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="415aa-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="415aa-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="415aa-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="415aa-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="415aa-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="415aa-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="415aa-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="415aa-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="415aa-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="415aa-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="415aa-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="415aa-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="415aa-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="415aa-203">a.</span><span class="sxs-lookup"><span data-stu-id="415aa-203">a.</span></span> <span data-ttu-id="415aa-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="415aa-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="415aa-205">b.</span><span class="sxs-lookup"><span data-stu-id="415aa-205">b.</span></span> <span data-ttu-id="415aa-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="415aa-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="415aa-207">c.</span><span class="sxs-lookup"><span data-stu-id="415aa-207">c.</span></span> <span data-ttu-id="415aa-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="415aa-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="415aa-209">d.</span><span class="sxs-lookup"><span data-stu-id="415aa-209">d.</span></span> <span data-ttu-id="415aa-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="415aa-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="415aa-211">Creazione di un utente test di Small Improvements</span><span class="sxs-lookup"><span data-stu-id="415aa-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="415aa-212">toolog agli utenti di Azure AD tooenable in tooSmall miglioramenti, è necessario eseguirne il provisioning in piccoli miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="415aa-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="415aa-213">Nel caso di hello di miglioramenti di piccole dimensioni, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="415aa-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="415aa-214">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="415aa-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="415aa-215">Sito della società di piccoli miglioramenti tooyour Sign-on come amministratore.</span><span class="sxs-lookup"><span data-stu-id="415aa-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="415aa-216">Dalla Home page di hello, andare toohello menu hello a sinistra, fare clic su **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="415aa-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="415aa-217">Fare clic su hello **Directory utente** pulsante dalla sezione Gestione utenti.</span><span class="sxs-lookup"><span data-stu-id="415aa-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="415aa-219">Fare clic su **Aggiungi utenti**.</span><span class="sxs-lookup"><span data-stu-id="415aa-219">Click **Add users**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="415aa-221">In hello **Aggiungi utenti** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="415aa-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="415aa-223">a.</span><span class="sxs-lookup"><span data-stu-id="415aa-223">a.</span></span> <span data-ttu-id="415aa-224">Immettere hello **nome** dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="415aa-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="415aa-225">b.</span><span class="sxs-lookup"><span data-stu-id="415aa-225">b.</span></span> <span data-ttu-id="415aa-226">Immettere hello **cognome** dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="415aa-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="415aa-227">c.</span><span class="sxs-lookup"><span data-stu-id="415aa-227">c.</span></span> <span data-ttu-id="415aa-228">Immettere hello **posta elettronica** dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="415aa-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="415aa-229">d.</span><span class="sxs-lookup"><span data-stu-id="415aa-229">d.</span></span> <span data-ttu-id="415aa-230">È anche possibile scegliere il messaggio personale tooenter hello in hello **invia notifica tramite posta elettronica** casella.</span><span class="sxs-lookup"><span data-stu-id="415aa-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="415aa-231">Se non si desidera che la notifica di hello toosend, quindi deselezionare questa casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="415aa-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="415aa-232">e.</span><span class="sxs-lookup"><span data-stu-id="415aa-232">e.</span></span> <span data-ttu-id="415aa-233">Fare clic su **Crea utenti**.</span><span class="sxs-lookup"><span data-stu-id="415aa-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="415aa-234">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="415aa-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="415aa-235">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSmall miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="415aa-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Assegna utente][200] 

<span data-ttu-id="415aa-237">**tooassign Britta Simon tooSmall miglioramenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="415aa-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="415aa-238">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="415aa-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="415aa-240">Nell'elenco di applicazioni hello, selezionare **piccoli miglioramenti**.</span><span class="sxs-lookup"><span data-stu-id="415aa-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="415aa-242">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="415aa-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="415aa-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="415aa-244">Click **Add** button.</span></span> <span data-ttu-id="415aa-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="415aa-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="415aa-247">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="415aa-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="415aa-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="415aa-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="415aa-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="415aa-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="415aa-250">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="415aa-250">Testing single sign-on</span></span>

<span data-ttu-id="415aa-251">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="415aa-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="415aa-252">Quando si fa clic hello piccoli miglioramenti riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione piccoli miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="415aa-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="415aa-253">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="415aa-253">Additional resources</span></span>

* [<span data-ttu-id="415aa-254">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="415aa-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="415aa-255">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="415aa-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP NetWeaver | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP NetWeaver.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 69008734864e1e258a0c2ec872e51aa331491fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="3dfaa-103">Esercitazione: Integrazione di Azure Active Directory con SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="3dfaa-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="3dfaa-104">In questa esercitazione, è illustrato come toointegrate SAP NetWeaver in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3dfaa-104">In this tutorial, you learn how toointegrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3dfaa-105">L'integrazione di SAP NetWeaver in Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3dfaa-105">Integrating SAP NetWeaver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3dfaa-106">È possibile controllare in Azure AD che ha accesso tooSAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="3dfaa-106">You can control in Azure AD who has access tooSAP NetWeaver</span></span>
- <span data-ttu-id="3dfaa-107">È possibile abilitare l'utenti tooautomatically get connesso tooSAP NetWeaver (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dfaa-107">You can enable your users tooautomatically get signed-on tooSAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3dfaa-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3dfaa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3dfaa-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3dfaa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3dfaa-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3dfaa-110">Prerequisites</span></span>

<span data-ttu-id="3dfaa-111">tooconfigure integrazione di Azure AD con SAP NetWeaver, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3dfaa-111">tooconfigure Azure AD integration with SAP NetWeaver, you need hello following items:</span></span>

- <span data-ttu-id="3dfaa-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3dfaa-113">Sottoscrizione di SAP NetWeaver abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3dfaa-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3dfaa-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3dfaa-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="3dfaa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3dfaa-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3dfaa-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3dfaa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3dfaa-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3dfaa-118">Scenario description</span></span>
<span data-ttu-id="3dfaa-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3dfaa-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="3dfaa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3dfaa-121">Aggiunta di SAP NetWeaver dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3dfaa-121">Adding SAP NetWeaver from hello gallery</span></span>
2. <span data-ttu-id="3dfaa-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dfaa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-hello-gallery"></a><span data-ttu-id="3dfaa-123">Aggiunta di SAP NetWeaver dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3dfaa-123">Adding SAP NetWeaver from hello gallery</span></span>
<span data-ttu-id="3dfaa-124">integrazione hello tooconfigure di SAP NetWeaver in Azure AD, è necessario tooadd SAP NetWeaver dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-124">tooconfigure hello integration of SAP NetWeaver into Azure AD, you need tooadd SAP NetWeaver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3dfaa-125">**tooadd SAP NetWeaver dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3dfaa-125">**tooadd SAP NetWeaver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dfaa-126">In hello  **[portale Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3dfaa-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3dfaa-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3dfaa-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3dfaa-133">Nella casella di ricerca hello, digitare **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-133">In hello search box, type **SAP NetWeaver**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="3dfaa-135">Nel riquadro dei risultati hello, selezionare **SAP NetWeaver**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-135">In hello results panel, select **SAP NetWeaver**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3dfaa-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dfaa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3dfaa-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP NetWeaver con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3dfaa-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3dfaa-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAP NetWeaver è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP NetWeaver is tooa user in Azure AD.</span></span> <span data-ttu-id="3dfaa-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SAP NetWeaver deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-140">In other words, a link relationship between an Azure AD user and hello related user in SAP NetWeaver needs toobe established.</span></span>

<span data-ttu-id="3dfaa-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="3dfaa-142">tooconfigure e prova AD Azure single sign-on con SAP NetWeaver, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="3dfaa-142">tooconfigure and test Azure AD single sign-on with SAP NetWeaver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3dfaa-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3dfaa-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3dfaa-145">**[Creazione di un utente test SAP NetWeaver](#creating-an-sap-netweaver-test-user)**  -toohave un equivalente di Britta Simon in SAP NetWeaver che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - toohave a counterpart of Britta Simon in SAP NetWeaver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3dfaa-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3dfaa-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3dfaa-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dfaa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3dfaa-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="3dfaa-150">**Azure AD tooconfigure single sign-on con SAP NetWeaver, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3dfaa-150">**tooconfigure Azure AD single sign-on with SAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dfaa-151">Nel portale di Azure su hello hello **SAP NetWeaver** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-151">In hello Azure portal, on hello **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3dfaa-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="3dfaa-155">In hello **SAP NetWeaver dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3dfaa-155">On hello **SAP NetWeaver Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="3dfaa-157">a.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-157">a.</span></span> <span data-ttu-id="3dfaa-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="3dfaa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="3dfaa-159">b.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-159">b.</span></span> <span data-ttu-id="3dfaa-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="3dfaa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="3dfaa-161">c.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-161">c.</span></span> <span data-ttu-id="3dfaa-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="3dfaa-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3dfaa-163">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-163">These values are not hello real.</span></span> <span data-ttu-id="3dfaa-164">Aggiornare questi valori con hello effettivo identificatore e l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-164">Update these values with hello actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="3dfaa-165">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="3dfaa-166">Contatto [team di supporto di SAP NetWeaver Client](https://www.sap.com/support.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) tooget these values.</span></span> 

4. <span data-ttu-id="3dfaa-167">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="3dfaa-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3dfaa-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3dfaa-171">In hello **configurazione di SAP NetWeaver** fare clic su **configurare SAP NetWeaver** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-171">On hello **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3dfaa-172">Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="3dfaa-172">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="3dfaa-174">tooconfigure single sign-on sul **SAP NetWeaver** lato, è necessario hello toosend scaricato **Metadata XML** e **ID entità SAML** troppo[supporto di SAP NetWeaver ](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="3dfaa-174">tooconfigure single sign-on on **SAP NetWeaver** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="3dfaa-175">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="3dfaa-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3dfaa-176">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3dfaa-177">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3dfaa-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3dfaa-178">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dfaa-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="3dfaa-179">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3dfaa-181">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3dfaa-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dfaa-182">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3dfaa-184">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3dfaa-186">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3dfaa-188">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3dfaa-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3dfaa-190">a.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-190">a.</span></span> <span data-ttu-id="3dfaa-191">In hello **nome** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-191">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="3dfaa-192">b.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-192">b.</span></span> <span data-ttu-id="3dfaa-193">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-193">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="3dfaa-194">c.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-194">c.</span></span> <span data-ttu-id="3dfaa-195">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3dfaa-196">d.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-196">d.</span></span> <span data-ttu-id="3dfaa-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="3dfaa-198">Creazione di un utente test di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="3dfaa-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="3dfaa-199">In questa sezione viene creato un utente chiamato Britta Simon in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="3dfaa-200">Utilizzare il [il supporto di SAP NetWeaver](https://www.sap.com/support.html) utenti hello tooadd nella piattaforma di SAP NetWeaver hello.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) tooadd hello users in hello SAP NetWeaver platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3dfaa-201">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dfaa-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3dfaa-202">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP NetWeaver.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3dfaa-204">**tooassign Britta Simon tooSAP NetWeaver, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3dfaa-204">**tooassign Britta Simon tooSAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dfaa-205">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3dfaa-207">Nell'elenco di applicazioni hello, selezionare **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-207">In hello applications list, select **SAP NetWeaver**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="3dfaa-209">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3dfaa-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-211">Click **Add** button.</span></span> <span data-ttu-id="3dfaa-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3dfaa-214">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3dfaa-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3dfaa-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3dfaa-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3dfaa-217">Testing single sign-on</span></span>

<span data-ttu-id="3dfaa-218">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3dfaa-219">Quando si fa clic su riquadro SAP NetWeaver hello in hello Pannello di accesso, è necessario ottenere l'applicazione SAP NetWeaver tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="3dfaa-219">When you click hello SAP NetWeaver tile in hello Access Panel, you should get automatically signed-on tooyour SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3dfaa-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3dfaa-220">Additional resources</span></span>

* [<span data-ttu-id="3dfaa-221">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dfaa-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3dfaa-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dfaa-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png


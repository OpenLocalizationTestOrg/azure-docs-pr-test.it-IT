---
title: 'Esercitazione: Integrazione di Azure Active Directory con StatusPage | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e StatusPage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="71d57-103">Esercitazione Integrazione di Azure Active Directory con StatusPage</span><span class="sxs-lookup"><span data-stu-id="71d57-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="71d57-104">In questa esercitazione, è illustrato come toointegrate StatusPage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71d57-104">In this tutorial, you learn how toointegrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71d57-105">Integrazione StatusPage con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="71d57-105">Integrating StatusPage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="71d57-106">È possibile controllare in Azure AD che ha accesso tooStatusPage</span><span class="sxs-lookup"><span data-stu-id="71d57-106">You can control in Azure AD who has access tooStatusPage</span></span>
- <span data-ttu-id="71d57-107">È possibile abilitare l'utenti tooautomatically get connesso tooStatusPage (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="71d57-107">You can enable your users tooautomatically get signed-on tooStatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71d57-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="71d57-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="71d57-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71d57-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71d57-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="71d57-110">Prerequisites</span></span>

<span data-ttu-id="71d57-111">integrazione di Azure AD con StatusPage tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="71d57-111">tooconfigure Azure AD integration with StatusPage, you need hello following items:</span></span>

- <span data-ttu-id="71d57-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71d57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71d57-113">Sottoscrizione di StatusPage abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="71d57-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71d57-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="71d57-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71d57-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="71d57-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71d57-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="71d57-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71d57-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71d57-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71d57-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="71d57-118">Scenario description</span></span>
<span data-ttu-id="71d57-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="71d57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71d57-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="71d57-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71d57-121">Aggiunta di StatusPage dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="71d57-121">Adding StatusPage from hello gallery</span></span>
2. <span data-ttu-id="71d57-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="71d57-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-hello-gallery"></a><span data-ttu-id="71d57-123">Aggiunta di StatusPage dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="71d57-123">Adding StatusPage from hello gallery</span></span>
<span data-ttu-id="71d57-124">integrazione hello tooconfigure di StatusPage in Azure AD, è necessario tooadd StatusPage dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="71d57-124">tooconfigure hello integration of StatusPage into Azure AD, you need tooadd StatusPage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="71d57-125">**tooadd StatusPage dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="71d57-125">**tooadd StatusPage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71d57-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="71d57-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="71d57-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="71d57-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="71d57-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="71d57-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="71d57-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="71d57-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="71d57-133">Nella casella di ricerca hello, digitare **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="71d57-133">In hello search box, type **StatusPage**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="71d57-135">Nel riquadro dei risultati hello, selezionare **StatusPage**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="71d57-135">In hello results panel, select **StatusPage**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71d57-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="71d57-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71d57-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con StatusPage in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="71d57-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71d57-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in StatusPage è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71d57-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in StatusPage is tooa user in Azure AD.</span></span> <span data-ttu-id="71d57-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in StatusPage deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="71d57-140">In other words, a link relationship between an Azure AD user and hello related user in StatusPage needs toobe established.</span></span>

<span data-ttu-id="71d57-141">In StatusPage, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="71d57-141">In StatusPage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="71d57-142">tooconfigure e prova AD Azure single sign-on con StatusPage, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="71d57-142">tooconfigure and test Azure AD single sign-on with StatusPage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71d57-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="71d57-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71d57-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71d57-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71d57-145">**[Creazione di un utente test StatusPage](#creating-a-statuspage-test-user)**  -toohave un equivalente di Britta Simon in StatusPage che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="71d57-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - toohave a counterpart of Britta Simon in StatusPage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="71d57-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71d57-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71d57-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="71d57-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71d57-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="71d57-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71d57-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione StatusPage.</span><span class="sxs-lookup"><span data-stu-id="71d57-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="71d57-150">**Azure AD tooconfigure single sign-on con StatusPage, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="71d57-150">**tooconfigure Azure AD single sign-on with StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="71d57-151">Nel portale di Azure su hello hello **StatusPage** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="71d57-151">In hello Azure portal, on hello **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="71d57-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71d57-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="71d57-155">In hello **StatusPage dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="71d57-155">On hello **StatusPage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="71d57-157">a.</span><span class="sxs-lookup"><span data-stu-id="71d57-157">a.</span></span> <span data-ttu-id="71d57-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="71d57-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="71d57-159">b.</span><span class="sxs-lookup"><span data-stu-id="71d57-159">b.</span></span> <span data-ttu-id="71d57-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="71d57-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="71d57-161">Contattare il team di supporto StatusPage hello in [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest i metadati necessari tooconfigure accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71d57-161">Contact hello StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)toorequest metadata necessary tooconfigure single sign-on.</span></span> 
    >
    ><span data-ttu-id="71d57-162">a.</span><span class="sxs-lookup"><span data-stu-id="71d57-162">a.</span></span> <span data-ttu-id="71d57-163">Dai metadati hello, copiare il valore di autorità di certificazione hello e quindi incollarlo hello **identificatore** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="71d57-163">From hello metadata, copy hello Issuer value, and then paste it into hello **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="71d57-164">b.</span><span class="sxs-lookup"><span data-stu-id="71d57-164">b.</span></span> <span data-ttu-id="71d57-165">Dai metadati hello, copiare l'URL di risposta hello e quindi incollarlo hello **URL di risposta** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="71d57-165">From hello metadata, copy hello Reply URL, and then paste it into hello **Reply URL** textbox.</span></span>

4. <span data-ttu-id="71d57-166">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="71d57-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="71d57-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="71d57-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="71d57-170">In hello **StatusPage configurazione** fare clic su **configurare StatusPage** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="71d57-170">On hello **StatusPage Configuration** section, click **Configure StatusPage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="71d57-171">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="71d57-171">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="71d57-173">In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour StatusPage.</span><span class="sxs-lookup"><span data-stu-id="71d57-173">In another browser window, sign on tooyour StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="71d57-174">Nella barra degli strumenti principale hello, fare clic su **Gestisci Account**.</span><span class="sxs-lookup"><span data-stu-id="71d57-174">In hello main toolbar, click **Manage Account**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="71d57-176">Fare clic su hello **Single Sign-on** scheda.</span><span class="sxs-lookup"><span data-stu-id="71d57-176">Click hello **Single Sign-on** tab.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="71d57-178">Nella pagina di installazione SSO hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="71d57-178">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="71d57-181">a.</span><span class="sxs-lookup"><span data-stu-id="71d57-181">a.</span></span> <span data-ttu-id="71d57-182">In hello **SSO Target URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="71d57-182">In hello **SSO Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="71d57-183">b.</span><span class="sxs-lookup"><span data-stu-id="71d57-183">b.</span></span> <span data-ttu-id="71d57-184">Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="71d57-184">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span> 

    <span data-ttu-id="71d57-185">c.</span><span class="sxs-lookup"><span data-stu-id="71d57-185">c.</span></span> <span data-ttu-id="71d57-186">Fare clic su **SALVA CONFIGURAZIONE**.</span><span class="sxs-lookup"><span data-stu-id="71d57-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="71d57-187">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="71d57-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="71d57-188">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="71d57-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="71d57-189">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71d57-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71d57-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="71d57-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="71d57-191">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="71d57-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="71d57-193">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="71d57-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71d57-194">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="71d57-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71d57-196">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="71d57-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71d57-198">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="71d57-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71d57-200">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="71d57-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71d57-202">a.</span><span class="sxs-lookup"><span data-stu-id="71d57-202">a.</span></span> <span data-ttu-id="71d57-203">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71d57-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71d57-204">b.</span><span class="sxs-lookup"><span data-stu-id="71d57-204">b.</span></span> <span data-ttu-id="71d57-205">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="71d57-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71d57-206">c.</span><span class="sxs-lookup"><span data-stu-id="71d57-206">c.</span></span> <span data-ttu-id="71d57-207">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="71d57-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="71d57-208">d.</span><span class="sxs-lookup"><span data-stu-id="71d57-208">d.</span></span> <span data-ttu-id="71d57-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="71d57-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="71d57-210">Creazione di un utente test per StatusPage</span><span class="sxs-lookup"><span data-stu-id="71d57-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="71d57-211">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in StatusPage toocreate.</span><span class="sxs-lookup"><span data-stu-id="71d57-211">hello objective of this section is toocreate a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="71d57-212">StatusPage supporta il provisioning JIT (just-in-time),</span><span class="sxs-lookup"><span data-stu-id="71d57-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="71d57-213">È già stato abilitato in [Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="71d57-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="71d57-214">**un utente denominato Britta Simon in StatusPage, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="71d57-214">**toocreate a user called Britta Simon in StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="71d57-215">Sito dell'azienda StatusPage tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="71d57-215">Sign-on tooyour StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="71d57-216">Scegliere dal menu hello in primo piano hello **Gestisci Account**.</span><span class="sxs-lookup"><span data-stu-id="71d57-216">In hello menu on hello top, click **Manage Account**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="71d57-218">Fare clic su hello **i membri del Team** scheda.</span><span class="sxs-lookup"><span data-stu-id="71d57-218">Click hello **Team Members** tab.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="71d57-220">Fare clic su **AGGIUNGI MEMBRO DEL TEAM**.</span><span class="sxs-lookup"><span data-stu-id="71d57-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="71d57-222">Hello tipo **indirizzo di posta elettronica**, **nome**, e **nome Sur** di un utente valido desiderate tooprovision hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="71d57-222">Type hello **Email Address**, **First Name**, and **Sur Name** of a valid user you want tooprovision into hello related textboxes.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="71d57-224">Per **Ruolo** scegliere **Client Administrator** (Amministratore client).</span><span class="sxs-lookup"><span data-stu-id="71d57-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="71d57-225">Fare clic su **CREA ACCOUNT**.</span><span class="sxs-lookup"><span data-stu-id="71d57-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="71d57-226">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="71d57-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="71d57-227">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooStatusPage.</span><span class="sxs-lookup"><span data-stu-id="71d57-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooStatusPage.</span></span>

![Assegna utente][200] 

<span data-ttu-id="71d57-229">**tooassign Britta Simon tooStatusPage, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="71d57-229">**tooassign Britta Simon tooStatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="71d57-230">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="71d57-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="71d57-232">Nell'elenco di applicazioni hello, selezionare **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="71d57-232">In hello applications list, select **StatusPage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="71d57-234">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="71d57-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="71d57-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="71d57-236">Click **Add** button.</span></span> <span data-ttu-id="71d57-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="71d57-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="71d57-239">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="71d57-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="71d57-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="71d57-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71d57-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="71d57-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="71d57-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="71d57-242">Testing single sign-on</span></span>

<span data-ttu-id="71d57-243">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="71d57-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="71d57-244">Quando si fa clic su riquadro StatusPage hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour StatusPage applicazione.</span><span class="sxs-lookup"><span data-stu-id="71d57-244">When you click hello StatusPage tile in hello Access Panel, you should get automatically signed-on tooyour StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71d57-245">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="71d57-245">Additional resources</span></span>

* [<span data-ttu-id="71d57-246">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71d57-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71d57-247">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71d57-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png


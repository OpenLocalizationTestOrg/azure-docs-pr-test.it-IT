---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cerner Central | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Cerner centrale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="154f2-103">Esercitazione: Integrazione di Azure Active Directory con Central Desktop</span><span class="sxs-lookup"><span data-stu-id="154f2-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="154f2-104">In questa esercitazione, è illustrato come toointegrate Cerner centrale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="154f2-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="154f2-105">Integrazione Cerner centrale con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="154f2-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="154f2-106">È possibile controllare in Azure AD che ha accesso tooCerner centrale</span><span class="sxs-lookup"><span data-stu-id="154f2-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="154f2-107">È possibile abilitare l'utenti tooautomatically get connesso tooCerner centrale (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="154f2-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="154f2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="154f2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="154f2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="154f2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="154f2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="154f2-110">Prerequisites</span></span>

<span data-ttu-id="154f2-111">integrazione di Azure AD con Cerner Central tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="154f2-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="154f2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="154f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="154f2-113">Account di sistema Cerner Central approvato</span><span class="sxs-lookup"><span data-stu-id="154f2-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="154f2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="154f2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="154f2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="154f2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="154f2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="154f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="154f2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="154f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="154f2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="154f2-118">Scenario description</span></span>
<span data-ttu-id="154f2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="154f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="154f2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="154f2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="154f2-121">Aggiunta di Cerner centrale dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="154f2-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="154f2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="154f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="154f2-123">Aggiunta di Cerner centrale dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="154f2-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="154f2-124">integrazione hello tooconfigure di Cerner centrale in Azure AD, è necessario tooadd Cerner centrale dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="154f2-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="154f2-125">**tooadd Cerner centrale dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="154f2-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="154f2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="154f2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="154f2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="154f2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="154f2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="154f2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="154f2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="154f2-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="154f2-133">Nella casella di ricerca hello, digitare **centrale Cerner**.</span><span class="sxs-lookup"><span data-stu-id="154f2-133">In hello search box, type **Cerner Central**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="154f2-135">Nel riquadro dei risultati hello, selezionare **Cerner centrale**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="154f2-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="154f2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="154f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="154f2-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Cerner Central in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="154f2-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="154f2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Cerner centrale è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="154f2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="154f2-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello in Centro Cerner deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="154f2-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="154f2-141">tooconfigure e prova AD Azure single sign-on con Cerner centrale, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="154f2-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="154f2-142">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="154f2-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="154f2-143">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="154f2-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="154f2-144">**[Creazione di un utente test centrale Cerner](#creating-a-cerner-central-test-user)**  -toohave un equivalente di Britta Simon Cerner centrale che è la rappresentazione toohello collegato Azure AD dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="154f2-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="154f2-145">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="154f2-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="154f2-146">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="154f2-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="154f2-147">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="154f2-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="154f2-148">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione centro Cerner.</span><span class="sxs-lookup"><span data-stu-id="154f2-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="154f2-149">**Azure AD tooconfigure single sign-on con Cerner centrale, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="154f2-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="154f2-150">Nel portale di Azure su hello hello **Cerner centrale** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="154f2-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="154f2-152">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="154f2-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="154f2-154">In hello **Cerner centrale dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="154f2-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="154f2-156">a.</span><span class="sxs-lookup"><span data-stu-id="154f2-156">a.</span></span> <span data-ttu-id="154f2-157">In hello **identificatore** casella di testo, valore di tipo hello hello seguito modelli utilizzando:</span><span class="sxs-lookup"><span data-stu-id="154f2-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="154f2-158">b.</span><span class="sxs-lookup"><span data-stu-id="154f2-158">b.</span></span> <span data-ttu-id="154f2-159">In hello **URL di risposta** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="154f2-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="154f2-160">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="154f2-160">These values are not hello real.</span></span> <span data-ttu-id="154f2-161">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="154f2-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="154f2-162">Contatto [team di supporto centrale Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="154f2-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="154f2-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="154f2-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="154f2-165">hello toogenerate **metadati** url, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="154f2-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="154f2-166">a.</span><span class="sxs-lookup"><span data-stu-id="154f2-166">a.</span></span> <span data-ttu-id="154f2-167">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="154f2-167">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="154f2-169">b.</span><span class="sxs-lookup"><span data-stu-id="154f2-169">b.</span></span> <span data-ttu-id="154f2-170">Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="154f2-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="154f2-172">c.</span><span class="sxs-lookup"><span data-stu-id="154f2-172">c.</span></span> <span data-ttu-id="154f2-173">Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="154f2-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="154f2-175">d.</span><span class="sxs-lookup"><span data-stu-id="154f2-175">d.</span></span> <span data-ttu-id="154f2-176">Ora passare toohello pagina delle proprietà di **Cerner centrale** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="154f2-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="154f2-178">e.</span><span class="sxs-lookup"><span data-stu-id="154f2-178">e.</span></span> <span data-ttu-id="154f2-179">Generare hello **URL dei metadati** utilizzando hello seguente motivo:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="154f2-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="154f2-180">tooconfigure single sign-on sul **Cerner centrale** lato, è necessario hello toosend **URL dei metadati** troppo[supporto centrale Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="154f2-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="154f2-181">Configurano hello SSO sull'integrazione di applicazioni lato toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="154f2-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="154f2-182">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="154f2-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="154f2-183">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="154f2-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="154f2-184">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="154f2-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="154f2-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="154f2-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="154f2-186">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="154f2-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Creare un utente di Azure AD][100]

<span data-ttu-id="154f2-188">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="154f2-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="154f2-189">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="154f2-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="154f2-191">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="154f2-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="154f2-193">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="154f2-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="154f2-195">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="154f2-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="154f2-197">a.</span><span class="sxs-lookup"><span data-stu-id="154f2-197">a.</span></span> <span data-ttu-id="154f2-198">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="154f2-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="154f2-199">b.</span><span class="sxs-lookup"><span data-stu-id="154f2-199">b.</span></span> <span data-ttu-id="154f2-200">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="154f2-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="154f2-201">c.</span><span class="sxs-lookup"><span data-stu-id="154f2-201">c.</span></span> <span data-ttu-id="154f2-202">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="154f2-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="154f2-203">d.</span><span class="sxs-lookup"><span data-stu-id="154f2-203">d.</span></span> <span data-ttu-id="154f2-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="154f2-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="154f2-205">Creazione di un utente test di Cerner Central</span><span class="sxs-lookup"><span data-stu-id="154f2-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="154f2-206">L'applicazione **Cerner Central** consente l'autenticazione da qualsiasi provider di identità federato.</span><span class="sxs-lookup"><span data-stu-id="154f2-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="154f2-207">Se un utente è in grado di toolog nella home page dell'applicazione toohello, essi sono federati e non sono necessari per qualsiasi funzionalità di provisioning manuale.</span><span class="sxs-lookup"><span data-stu-id="154f2-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="154f2-208">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="154f2-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="154f2-209">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCerner centrale.</span><span class="sxs-lookup"><span data-stu-id="154f2-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Assegna utente][200] 

<span data-ttu-id="154f2-211">**tooassign Britta Simon tooCerner centrale, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="154f2-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="154f2-212">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="154f2-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="154f2-214">Nell'elenco di applicazioni hello, selezionare **centrale Cerner**.</span><span class="sxs-lookup"><span data-stu-id="154f2-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="154f2-216">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="154f2-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="154f2-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="154f2-218">Click **Add** button.</span></span> <span data-ttu-id="154f2-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="154f2-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="154f2-221">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="154f2-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="154f2-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="154f2-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="154f2-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="154f2-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="154f2-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="154f2-224">Testing single sign-on</span></span>

<span data-ttu-id="154f2-225">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="154f2-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="154f2-226">Quando si fa clic hello centrale Cerner riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Cerner centrale.</span><span class="sxs-lookup"><span data-stu-id="154f2-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="154f2-227">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="154f2-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="154f2-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="154f2-228">Additional resources</span></span>

* [<span data-ttu-id="154f2-229">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="154f2-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="154f2-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="154f2-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png


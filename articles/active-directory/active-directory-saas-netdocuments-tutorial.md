---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetDocuments | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e NetDocuments.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="49c49-103">Esercitazione: Integrazione di Azure Active Directory con NetDocuments</span><span class="sxs-lookup"><span data-stu-id="49c49-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="49c49-104">In questa esercitazione, è illustrato come toointegrate NetDocuments con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49c49-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49c49-105">Integrazione NetDocuments con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="49c49-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49c49-106">È possibile controllare in Azure AD che ha accesso tooNetDocuments</span><span class="sxs-lookup"><span data-stu-id="49c49-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="49c49-107">È possibile abilitare l'utenti tooautomatically get connesso tooNetDocuments (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c49-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49c49-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="49c49-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49c49-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49c49-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49c49-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="49c49-110">Prerequisites</span></span>

<span data-ttu-id="49c49-111">integrazione di Azure AD con NetDocuments tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="49c49-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="49c49-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c49-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49c49-113">Sottoscrizione di NetDocuments abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="49c49-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49c49-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="49c49-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49c49-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="49c49-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49c49-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="49c49-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49c49-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49c49-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49c49-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="49c49-118">Scenario description</span></span>
<span data-ttu-id="49c49-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="49c49-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49c49-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="49c49-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49c49-121">Aggiunta di NetDocuments dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="49c49-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="49c49-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c49-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="49c49-123">Aggiunta di NetDocuments dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="49c49-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="49c49-124">integrazione hello tooconfigure di NetDocuments in Azure AD, è necessario tooadd NetDocuments dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="49c49-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49c49-125">**tooadd NetDocuments dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49c49-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c49-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="49c49-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49c49-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="49c49-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49c49-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="49c49-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="49c49-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="49c49-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="49c49-133">Nella casella di ricerca hello, digitare **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="49c49-133">In hello search box, type **NetDocuments**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="49c49-135">Nel riquadro dei risultati hello, selezionare **NetDocuments**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="49c49-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49c49-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c49-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49c49-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con NetDocuments usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="49c49-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49c49-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in NetDocuments è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c49-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="49c49-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in NetDocuments richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="49c49-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="49c49-141">In NetDocuments, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="49c49-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="49c49-142">tooconfigure e prova AD Azure single sign-on con NetDocuments, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="49c49-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49c49-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="49c49-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49c49-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49c49-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49c49-145">**[Creazione di un utente test NetDocuments](#creating-a-netdocuments-test-user)**  -toohave un equivalente di Britta Simon in NetDocuments che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="49c49-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49c49-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="49c49-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49c49-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="49c49-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49c49-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c49-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49c49-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="49c49-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="49c49-150">**Azure AD tooconfigure single sign-on con NetDocuments, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49c49-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c49-151">Nel portale di Azure su hello hello **NetDocuments** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="49c49-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="49c49-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="49c49-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="49c49-155">In hello **NetDocuments dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="49c49-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="49c49-157">a.</span><span class="sxs-lookup"><span data-stu-id="49c49-157">a.</span></span> <span data-ttu-id="49c49-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="49c49-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="49c49-159">b.</span><span class="sxs-lookup"><span data-stu-id="49c49-159">b.</span></span> <span data-ttu-id="49c49-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="49c49-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49c49-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="49c49-161">These values are not real.</span></span> <span data-ttu-id="49c49-162">Aggiornare questi valori con URL hello effettivo Sign-on e URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="49c49-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="49c49-163">Contatto [team di supporto NetDocuments](https://support.netdocuments.com/hc/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="49c49-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="49c49-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="49c49-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="49c49-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="49c49-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49c49-168">In un'altra finestra del Web browser accedere al sito aziendale di NetDocuments come amministratore.</span><span class="sxs-lookup"><span data-stu-id="49c49-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="49c49-169">Andare troppo**Admin**.</span><span class="sxs-lookup"><span data-stu-id="49c49-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="49c49-170">Fare clic su **Aggiungi e rimuovi utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="49c49-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="49c49-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="49c49-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="49c49-172">Fare clic su **Configura opzioni di autenticazione avanzata**.</span><span class="sxs-lookup"><span data-stu-id="49c49-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="49c49-173">![Configurare opzioni di autenticazione avanzata](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurare opzioni di autenticazione avanzata")</span><span class="sxs-lookup"><span data-stu-id="49c49-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="49c49-174">In hello **Federated Identity** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="49c49-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="49c49-175">![Identità federata](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identità federata")</span><span class="sxs-lookup"><span data-stu-id="49c49-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="49c49-176">a.</span><span class="sxs-lookup"><span data-stu-id="49c49-176">a.</span></span> <span data-ttu-id="49c49-177">Come **Federated identity server type** (Tipo di server identità federata) selezionare **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="49c49-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="49c49-178">b.</span><span class="sxs-lookup"><span data-stu-id="49c49-178">b.</span></span> <span data-ttu-id="49c49-179">Fare clic su **Choose file**, hello tooupload scaricato i file di metadati che è stato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="49c49-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="49c49-180">c.</span><span class="sxs-lookup"><span data-stu-id="49c49-180">c.</span></span> <span data-ttu-id="49c49-181">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="49c49-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="49c49-182">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="49c49-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49c49-183">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="49c49-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49c49-184">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49c49-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49c49-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c49-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="49c49-186">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="49c49-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="49c49-188">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49c49-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c49-189">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="49c49-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49c49-191">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="49c49-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49c49-193">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="49c49-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49c49-195">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="49c49-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49c49-197">a.</span><span class="sxs-lookup"><span data-stu-id="49c49-197">a.</span></span> <span data-ttu-id="49c49-198">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49c49-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49c49-199">b.</span><span class="sxs-lookup"><span data-stu-id="49c49-199">b.</span></span> <span data-ttu-id="49c49-200">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49c49-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49c49-201">c.</span><span class="sxs-lookup"><span data-stu-id="49c49-201">c.</span></span> <span data-ttu-id="49c49-202">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="49c49-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49c49-203">d.</span><span class="sxs-lookup"><span data-stu-id="49c49-203">d.</span></span> <span data-ttu-id="49c49-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="49c49-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="49c49-205">Creazione di un utente di test di NetDocuments</span><span class="sxs-lookup"><span data-stu-id="49c49-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="49c49-206">toolog agli utenti di Azure AD tooenable in tooNetDocuments, è necessario eseguirne il provisioning in NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="49c49-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="49c49-207">Nel caso di hello di NetDocuments, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="49c49-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="49c49-208">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49c49-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c49-209">Sing su tooyour **NetDocuments** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="49c49-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="49c49-210">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="49c49-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="49c49-211">![Amministratore](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="49c49-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="49c49-212">Fare clic su **Aggiungi e rimuovi utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="49c49-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="49c49-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="49c49-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="49c49-214">In hello **indirizzo di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica di un account Azure Active Directory valido, si desidera tooprovision e quindi fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="49c49-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="49c49-215">![Indirizzo di posta elettronica](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Indirizzo di posta elettronica")</span><span class="sxs-lookup"><span data-stu-id="49c49-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="49c49-216">titolare dell'account di Azure Active Directory di Hello riceverà un messaggio di posta elettronica che include un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="49c49-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="49c49-217">È possibile usare qualsiasi altro NetDocuments utente account strumento di creazione o le API fornite da NetDocuments tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="49c49-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="49c49-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c49-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="49c49-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNetDocuments.</span><span class="sxs-lookup"><span data-stu-id="49c49-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Assegna utente][200] 

<span data-ttu-id="49c49-221">**tooassign Britta Simon tooNetDocuments, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="49c49-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c49-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="49c49-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="49c49-224">Nell'elenco di applicazioni hello, selezionare **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="49c49-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="49c49-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="49c49-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="49c49-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="49c49-228">Click **Add** button.</span></span> <span data-ttu-id="49c49-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="49c49-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="49c49-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="49c49-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49c49-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="49c49-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49c49-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="49c49-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49c49-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="49c49-234">Testing single sign-on</span></span>

<span data-ttu-id="49c49-235">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="49c49-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="49c49-236">Quando si fa clic hello NetDocuments riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="49c49-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="49c49-237">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49c49-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49c49-238">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="49c49-238">Additional resources</span></span>

* [<span data-ttu-id="49c49-239">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49c49-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49c49-240">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49c49-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png


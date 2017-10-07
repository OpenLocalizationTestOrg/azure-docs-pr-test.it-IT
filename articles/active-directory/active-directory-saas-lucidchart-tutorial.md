---
title: 'Esercitazione: Integrazione di Azure Active Directory con Lucidchart | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Lucidchart.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="1efed-103">Esercitazione: Integrazione di Azure Active Directory con Lucidchart</span><span class="sxs-lookup"><span data-stu-id="1efed-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="1efed-104">In questa esercitazione, è illustrato come toointegrate Lucidchart con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1efed-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1efed-105">Integrazione Lucidchart con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1efed-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1efed-106">È possibile controllare in Azure AD che ha accesso tooLucidchart</span><span class="sxs-lookup"><span data-stu-id="1efed-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="1efed-107">È possibile abilitare l'utenti tooautomatically get connesso tooLucidchart (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1efed-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1efed-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1efed-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1efed-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1efed-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1efed-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1efed-110">Prerequisites</span></span>

<span data-ttu-id="1efed-111">integrazione di Azure AD con Lucidchart tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1efed-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="1efed-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1efed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1efed-113">Sottoscrizione di Lucidchart abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1efed-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1efed-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1efed-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1efed-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1efed-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1efed-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1efed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1efed-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1efed-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1efed-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1efed-118">Scenario description</span></span>
<span data-ttu-id="1efed-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1efed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1efed-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1efed-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1efed-121">Aggiunta di Lucidchart dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1efed-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="1efed-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1efed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="1efed-123">Aggiunta di Lucidchart dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1efed-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="1efed-124">integrazione hello tooconfigure di Lucidchart in Azure AD, è necessario tooadd Lucidchart dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1efed-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1efed-125">**tooadd Lucidchart dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1efed-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1efed-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1efed-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1efed-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1efed-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1efed-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1efed-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1efed-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1efed-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1efed-133">Nella casella di ricerca hello, digitare **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="1efed-133">In hello search box, type **Lucidchart**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="1efed-135">Nel riquadro dei risultati hello, selezionare **Lucidchart**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1efed-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1efed-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1efed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1efed-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Lucidchart usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1efed-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1efed-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Lucidchart è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1efed-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="1efed-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Lucidchart deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1efed-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="1efed-141">In Lucidchart, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1efed-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1efed-142">tooconfigure e prova AD Azure single sign-on con Lucidchart, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1efed-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1efed-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1efed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1efed-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1efed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1efed-145">**[Creazione di un utente test Lucidchart](#creating-a-lucidchart-test-user)**  -toohave un equivalente di Britta Simon in Lucidchart che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1efed-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1efed-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1efed-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1efed-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1efed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1efed-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1efed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1efed-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="1efed-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="1efed-150">**Azure AD tooconfigure single sign-on con Lucidchart, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1efed-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="1efed-151">Nel portale di Azure su hello hello **Lucidchart** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1efed-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1efed-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1efed-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="1efed-155">In hello **Lucidchart dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1efed-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="1efed-157">In hello **Sign-on URL** casella di testo, digitare un URL come:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="1efed-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="1efed-158">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1efed-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="1efed-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1efed-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1efed-162">In un'altra finestra del Web browser accedere al sito aziendale di Lucidchart come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1efed-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="1efed-163">Scegliere dal menu hello in primo piano hello **Team**.</span><span class="sxs-lookup"><span data-stu-id="1efed-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="1efed-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span><span class="sxs-lookup"><span data-stu-id="1efed-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="1efed-165">Fare clic su **Applications (Applicazioni) \> Manage SAML (Gestisci SAML)**.</span><span class="sxs-lookup"><span data-stu-id="1efed-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="1efed-166">![Gestire SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Gestire SAML")</span><span class="sxs-lookup"><span data-stu-id="1efed-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="1efed-167">In hello **SAML Authentication Settings** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1efed-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="1efed-168">a.</span><span class="sxs-lookup"><span data-stu-id="1efed-168">a.</span></span> <span data-ttu-id="1efed-169">Selezionare **Enable SAML Authentication** (Abilita autenticazione SAML) e quindi fare clic su **Optional** (Facoltativo).</span><span class="sxs-lookup"><span data-stu-id="1efed-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="1efed-170">![Dettagli dell'autenticazione SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "Dettagli dell'autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="1efed-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="1efed-171">b.</span><span class="sxs-lookup"><span data-stu-id="1efed-171">b.</span></span> <span data-ttu-id="1efed-172">In hello **dominio** casella di testo, digitare il dominio e quindi fare clic su **Cambia certificato**.</span><span class="sxs-lookup"><span data-stu-id="1efed-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="1efed-173">![Cambiare il certificato](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Cambiare il certificato")</span><span class="sxs-lookup"><span data-stu-id="1efed-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="1efed-174">c.</span><span class="sxs-lookup"><span data-stu-id="1efed-174">c.</span></span> <span data-ttu-id="1efed-175">Aprire il file di metadati scaricato, hello copia del contenuto e quindi incollarlo hello **Upload Metadata** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1efed-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="1efed-176">![Caricare i metadati](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Caricare i metadati")</span><span class="sxs-lookup"><span data-stu-id="1efed-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="1efed-177">d.</span><span class="sxs-lookup"><span data-stu-id="1efed-177">d.</span></span> <span data-ttu-id="1efed-178">Selezionare **automaticamente aggiungere nuovo gruppo di utenti toohello**, quindi fare clic su **salvare modifiche**.</span><span class="sxs-lookup"><span data-stu-id="1efed-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="1efed-179">![Salvare le modifiche](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Salvare le modifiche")</span><span class="sxs-lookup"><span data-stu-id="1efed-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="1efed-180">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1efed-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1efed-181">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1efed-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1efed-182">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1efed-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1efed-183">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1efed-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="1efed-184">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1efed-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1efed-186">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1efed-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1efed-187">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1efed-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1efed-189">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1efed-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1efed-191">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1efed-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1efed-193">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1efed-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1efed-195">a.</span><span class="sxs-lookup"><span data-stu-id="1efed-195">a.</span></span> <span data-ttu-id="1efed-196">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1efed-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1efed-197">b.</span><span class="sxs-lookup"><span data-stu-id="1efed-197">b.</span></span> <span data-ttu-id="1efed-198">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1efed-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1efed-199">c.</span><span class="sxs-lookup"><span data-stu-id="1efed-199">c.</span></span> <span data-ttu-id="1efed-200">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1efed-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1efed-201">d.</span><span class="sxs-lookup"><span data-stu-id="1efed-201">d.</span></span> <span data-ttu-id="1efed-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1efed-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="1efed-203">Creazione di un utente test di Lucidchart</span><span class="sxs-lookup"><span data-stu-id="1efed-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="1efed-204">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="1efed-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="1efed-205">Quando un utente assegnato tenta toolog a Lucidchart mediante il pannello di accesso di hello, Lucidchart verifica se hello utente esiste.</span><span class="sxs-lookup"><span data-stu-id="1efed-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="1efed-206">Se l’account utente non è ancora disponibile, viene creato automaticamente da Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="1efed-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1efed-207">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1efed-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1efed-208">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="1efed-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1efed-210">**tooassign Britta Simon tooLucidchart, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1efed-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="1efed-211">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1efed-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1efed-213">Nell'elenco di applicazioni hello, selezionare **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="1efed-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="1efed-215">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1efed-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1efed-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1efed-217">Click **Add** button.</span></span> <span data-ttu-id="1efed-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1efed-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1efed-220">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1efed-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1efed-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1efed-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1efed-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1efed-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1efed-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1efed-223">Testing single sign-on</span></span>

<span data-ttu-id="1efed-224">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1efed-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1efed-225">Quando si fa clic su riquadro Lucidchart hello in hello Pannello di accesso, è necessario ottenere applicazione Lucidchart tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="1efed-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="1efed-226">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1efed-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1efed-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1efed-227">Additional resources</span></span>

* [<span data-ttu-id="1efed-228">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1efed-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1efed-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1efed-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png


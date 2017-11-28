---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jive | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="88481-103">Esercitazione: Integrazione di Azure Active Directory con Jive</span><span class="sxs-lookup"><span data-stu-id="88481-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="88481-104">In questa esercitazione, è illustrato come toointegrate Jive con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88481-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88481-105">Integrazione Jive con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="88481-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88481-106">È possibile controllare in Azure AD che ha accesso tooJive</span><span class="sxs-lookup"><span data-stu-id="88481-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="88481-107">È possibile abilitare l'utenti tooautomatically get connesso tooJive (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="88481-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88481-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="88481-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="88481-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione di app SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88481-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88481-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="88481-110">Prerequisites</span></span>

<span data-ttu-id="88481-111">integrazione di Azure AD con Jive tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="88481-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="88481-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88481-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88481-113">Sottoscrizione di Jive abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="88481-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88481-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="88481-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88481-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="88481-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88481-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="88481-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88481-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88481-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88481-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="88481-118">Scenario description</span></span>
<span data-ttu-id="88481-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="88481-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88481-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="88481-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88481-121">Aggiunta di Jive dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="88481-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="88481-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88481-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="88481-123">Aggiunta di Jive dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="88481-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="88481-124">integrazione di hello tooconfigure di Jive in Azure AD, è necessario tooadd Jive dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="88481-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88481-125">**tooadd Jive dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="88481-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88481-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="88481-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88481-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="88481-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88481-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="88481-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="88481-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="88481-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="88481-133">Nella casella di ricerca hello, digitare **Jive**.</span><span class="sxs-lookup"><span data-stu-id="88481-133">In hello search box, type **Jive**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="88481-135">Nel riquadro dei risultati hello, selezionare **Jive**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="88481-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88481-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88481-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88481-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jive in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88481-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88481-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Jive è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88481-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="88481-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Jive deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="88481-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="88481-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Jive.</span><span class="sxs-lookup"><span data-stu-id="88481-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="88481-142">tooconfigure e test Azure single sign-on AD con Jive, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="88481-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88481-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="88481-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88481-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88481-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88481-145">**[Creazione di un utente test Jive](#creating-a-jive-test-user)**  -toohave un equivalente di Britta Simon in Jive che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="88481-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88481-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="88481-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88481-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="88481-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88481-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88481-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88481-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Jive.</span><span class="sxs-lookup"><span data-stu-id="88481-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="88481-150">**tooconfigure Azure single sign-on AD con Jive, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="88481-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="88481-151">Nel portale di Azure su hello hello **Jive** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="88481-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="88481-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="88481-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="88481-155">In hello **Jive dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="88481-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="88481-157">a.</span><span class="sxs-lookup"><span data-stu-id="88481-157">a.</span></span> <span data-ttu-id="88481-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="88481-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="88481-159">b.</span><span class="sxs-lookup"><span data-stu-id="88481-159">b.</span></span> <span data-ttu-id="88481-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="88481-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88481-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="88481-161">These values are not hello real.</span></span> <span data-ttu-id="88481-162">Aggiornare questi valori con URL hello effettivo Sign-on e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="88481-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="88481-163">Contatto [team di supporto Client Jive](https://www.jivesoftware.com/services-support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="88481-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="88481-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="88481-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="88481-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="88481-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88481-168">tooconfigure single sign-on sul **Jive** tenant Jive tooyour laterale, accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="88481-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="88481-169">Nel menu di hello in primo piano hello, fare clic su "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="88481-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="88481-171">a.</span><span class="sxs-lookup"><span data-stu-id="88481-171">a.</span></span> <span data-ttu-id="88481-172">Selezionare **abilitato** in hello **generale** scheda.</span><span class="sxs-lookup"><span data-stu-id="88481-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="88481-173">b.</span><span class="sxs-lookup"><span data-stu-id="88481-173">b.</span></span> <span data-ttu-id="88481-174">Fare clic su hello "**salvare tutte le impostazioni di saml**" pulsante.</span><span class="sxs-lookup"><span data-stu-id="88481-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="88481-175">Passare toohello "**Idp Metadata**" scheda.</span><span class="sxs-lookup"><span data-stu-id="88481-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="88481-177">a.</span><span class="sxs-lookup"><span data-stu-id="88481-177">a.</span></span> <span data-ttu-id="88481-178">Copiare il contenuto di hello del file XML di metadati scaricato hello e quindi incollarlo hello **i metadati del Provider di identità (IDP)** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="88481-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="88481-179">b.</span><span class="sxs-lookup"><span data-stu-id="88481-179">b.</span></span> <span data-ttu-id="88481-180">Fare clic su hello "**salvare tutte le impostazioni di saml**" pulsante.</span><span class="sxs-lookup"><span data-stu-id="88481-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="88481-181">Passare toohello "**Mapping attributo utente**" scheda.</span><span class="sxs-lookup"><span data-stu-id="88481-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="88481-183">a.</span><span class="sxs-lookup"><span data-stu-id="88481-183">a.</span></span> <span data-ttu-id="88481-184">In hello **posta elettronica** nome dell'attributo hello casella di testo, copia e Incolla di **posta** valore.</span><span class="sxs-lookup"><span data-stu-id="88481-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="88481-185">b.</span><span class="sxs-lookup"><span data-stu-id="88481-185">b.</span></span> <span data-ttu-id="88481-186">In hello **nome** nome dell'attributo hello casella di testo, copia e Incolla di **givenname** valore.</span><span class="sxs-lookup"><span data-stu-id="88481-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="88481-187">c.</span><span class="sxs-lookup"><span data-stu-id="88481-187">c.</span></span> <span data-ttu-id="88481-188">In hello **cognome** nome dell'attributo hello casella di testo, copia e Incolla di **surname** valore.</span><span class="sxs-lookup"><span data-stu-id="88481-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="88481-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="88481-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88481-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="88481-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88481-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88481-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88481-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88481-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="88481-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="88481-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="88481-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="88481-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88481-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="88481-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88481-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="88481-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88481-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="88481-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88481-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="88481-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88481-204">a.</span><span class="sxs-lookup"><span data-stu-id="88481-204">a.</span></span> <span data-ttu-id="88481-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88481-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88481-206">b.</span><span class="sxs-lookup"><span data-stu-id="88481-206">b.</span></span> <span data-ttu-id="88481-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88481-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88481-208">c.</span><span class="sxs-lookup"><span data-stu-id="88481-208">c.</span></span> <span data-ttu-id="88481-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="88481-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="88481-210">d.</span><span class="sxs-lookup"><span data-stu-id="88481-210">d.</span></span> <span data-ttu-id="88481-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="88481-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="88481-212">Creazione di un utente test di Jive</span><span class="sxs-lookup"><span data-stu-id="88481-212">Creating a Jive test user</span></span>

<span data-ttu-id="88481-213">Lavorare con [team di supporto Client Jive](https://www.jivesoftware.com/services-support/) utenti hello tooadd nella piattaforma Jive hello.</span><span class="sxs-lookup"><span data-stu-id="88481-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="88481-214">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="88481-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="88481-215">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooJive.</span><span class="sxs-lookup"><span data-stu-id="88481-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Assegna utente][200] 

<span data-ttu-id="88481-217">**tooassign Britta Simon tooJive, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="88481-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="88481-218">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="88481-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="88481-220">Nell'elenco di applicazioni hello, selezionare **Jive**.</span><span class="sxs-lookup"><span data-stu-id="88481-220">In hello applications list, select **Jive**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="88481-222">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="88481-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="88481-224">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="88481-224">Click **Add** button.</span></span> <span data-ttu-id="88481-225">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="88481-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="88481-227">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="88481-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88481-228">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="88481-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88481-229">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="88481-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88481-230">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="88481-230">Testing single sign-on</span></span>

<span data-ttu-id="88481-231">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="88481-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88481-232">Quando si fa clic su riquadro Jive hello in hello Pannello di accesso, è necessario ottenere applicazione Jive tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="88481-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88481-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="88481-233">Additional resources</span></span>

* [<span data-ttu-id="88481-234">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88481-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88481-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88481-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="88481-236">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="88481-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Evernote | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Evernote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="8c182-103">Esercitazione: Integrazione di Azure Active Directory con Evernote</span><span class="sxs-lookup"><span data-stu-id="8c182-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="8c182-104">In questa esercitazione, è illustrato come toointegrate Evernote con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c182-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c182-105">Integrazione Evernote con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8c182-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c182-106">È possibile controllare in Azure AD che ha accesso tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="8c182-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="8c182-107">È possibile abilitare l'utenti tooautomatically get connesso tooEvernote (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c182-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8c182-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c182-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8c182-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c182-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c182-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c182-110">Prerequisites</span></span>

<span data-ttu-id="8c182-111">integrazione di Azure AD con Evernote tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8c182-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="8c182-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c182-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c182-113">Sottoscrizione di Evernote abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8c182-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c182-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8c182-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c182-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8c182-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c182-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8c182-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c182-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c182-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c182-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8c182-118">Scenario description</span></span>
<span data-ttu-id="8c182-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8c182-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c182-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8c182-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c182-121">Aggiunta di Evernote dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8c182-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="8c182-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c182-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="8c182-123">Aggiunta di Evernote dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8c182-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="8c182-124">integrazione hello tooconfigure di Evernote in Azure AD, è necessario tooadd Evernote dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8c182-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c182-125">**tooadd Evernote dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c182-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c182-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8c182-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="8c182-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8c182-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8c182-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c182-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="8c182-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8c182-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="8c182-133">Nella casella di ricerca hello, digitare **Evernote**selezionare **Evernote** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8c182-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8c182-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c182-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8c182-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Evernote in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8c182-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8c182-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Evernote è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c182-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="8c182-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Evernote deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8c182-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="8c182-139">In Evernote, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8c182-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8c182-140">tooconfigure e prova AD Azure single sign-on con Evernote, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8c182-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c182-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8c182-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c182-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c182-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c182-143">**[Creare un utente test Evernote](#create-an-evernote-test-user)**  -toohave un equivalente di Britta Simon in Evernote che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8c182-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c182-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c182-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c182-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8c182-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8c182-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c182-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8c182-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Evernote.</span><span class="sxs-lookup"><span data-stu-id="8c182-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="8c182-148">**Azure AD tooconfigure single sign-on con Evernote, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c182-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c182-149">Nel portale di Azure su hello hello **Evernote** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8c182-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="8c182-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c182-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="8c182-153">In hello **Evernote dominio e gli URL** seguire passaggi se si desidera modalità iniziata da un'applicazione hello tooconfigure in IDP hello:</span><span class="sxs-lookup"><span data-stu-id="8c182-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="8c182-155">In hello **identificatore** casella di testo, digitare l'URL hello:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="8c182-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="8c182-156">Controllare **Mostra URL impostazioni avanzate** ed eseguire hello riportata dopo il passaggio se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="8c182-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="8c182-158">In hello **URL di accesso** casella di testo, digitare l'URL hello:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="8c182-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="8c182-159">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8c182-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="8c182-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8c182-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8c182-163">In hello **Evernote configurazione** fare clic su **configurare Evernote** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="8c182-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8c182-164">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8c182-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="8c182-166">In un'altra finestra del Web browser accedere al sito aziendale di Evernote come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8c182-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="8c182-167">Andare troppo**'Console di amministrazione di '**</span><span class="sxs-lookup"><span data-stu-id="8c182-167">Go too**'Admin Console'**</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="8c182-169">Da hello **'Console di amministrazione'**, andare troppo**'Security'** e selezionare **' Single Sign-On'**</span><span class="sxs-lookup"><span data-stu-id="8c182-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="8c182-171">Configurare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="8c182-171">Configure hello following values:</span></span>

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="8c182-173">a.</span><span class="sxs-lookup"><span data-stu-id="8c182-173">a.</span></span>  <span data-ttu-id="8c182-174">**Abilitare SSO:** SSO è abilitato per impostazione predefinita (fare clic su **disabilitare Single Sign-on** requisito di SSO hello tooremove)</span><span class="sxs-lookup"><span data-stu-id="8c182-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="8c182-175">b.</span><span class="sxs-lookup"><span data-stu-id="8c182-175">b.</span></span> <span data-ttu-id="8c182-176">Incolla **SAML Single sign-on Service URL** valore, che è stato copiato dal portale di Azure hello in hello **URL di richiesta HTTP SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8c182-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="8c182-177">c.</span><span class="sxs-lookup"><span data-stu-id="8c182-177">c.</span></span> <span data-ttu-id="8c182-178">Aprire certificato scaricato hello da Azure AD in un contenuto di hello in blocco note e copiare inclusi "BEGIN" e "Fine certificato" e incollarlo in hello **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8c182-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="8c182-179">Fare clic su **Save Changes** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="8c182-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="8c182-180">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8c182-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8c182-181">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8c182-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8c182-182">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c182-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8c182-183">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c182-183">Create an Azure AD test user</span></span>

<span data-ttu-id="8c182-184">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8c182-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="8c182-186">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c182-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c182-187">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8c182-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8c182-189">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8c182-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8c182-191">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8c182-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8c182-193">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8c182-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8c182-195">a.</span><span class="sxs-lookup"><span data-stu-id="8c182-195">a.</span></span> <span data-ttu-id="8c182-196">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c182-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c182-197">b.</span><span class="sxs-lookup"><span data-stu-id="8c182-197">b.</span></span> <span data-ttu-id="8c182-198">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c182-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8c182-199">c.</span><span class="sxs-lookup"><span data-stu-id="8c182-199">c.</span></span> <span data-ttu-id="8c182-200">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="8c182-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8c182-201">d.</span><span class="sxs-lookup"><span data-stu-id="8c182-201">d.</span></span> <span data-ttu-id="8c182-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8c182-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="8c182-203">Creare un utente test di Evernote</span><span class="sxs-lookup"><span data-stu-id="8c182-203">Create an Evernote test user</span></span>

<span data-ttu-id="8c182-204">In ordine tooenable Azure AD utenti toolog in Evernote, è necessario eseguirne il provisioning in Evernote.</span><span class="sxs-lookup"><span data-stu-id="8c182-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="8c182-205">Nel caso di hello di Evernote, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="8c182-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="8c182-206">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="8c182-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c182-207">Accedi tooyour sito della società Evernote come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8c182-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="8c182-208">Fare clic su hello **'Console di amministrazione'**.</span><span class="sxs-lookup"><span data-stu-id="8c182-208">Click hello **'Admin Console'**.</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="8c182-210">Da hello **'Console di amministrazione'**, andare troppo**'Aggiungi utenti'**.</span><span class="sxs-lookup"><span data-stu-id="8c182-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="8c182-212">**Aggiungere membri del team** in hello **posta elettronica** casella di testo, digitare l'indirizzo di posta elettronica hello dell'account utente e fare clic su **dell'invito.**</span><span class="sxs-lookup"><span data-stu-id="8c182-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="8c182-214">Dopo che viene inviato l'invito, titolare dell'account di Azure Active Directory hello riceveranno un invito di hello tooaccept di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="8c182-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8c182-215">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c182-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8c182-216">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="8c182-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="8c182-218">**tooassign Britta Simon tooEvernote, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8c182-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c182-219">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c182-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8c182-221">Nell'elenco di applicazioni hello, selezionare **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="8c182-221">In hello applications list, select **Evernote**.</span></span>

    ![collegamento Evernote Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="8c182-223">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8c182-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="8c182-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c182-225">Click **Add** button.</span></span> <span data-ttu-id="8c182-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8c182-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="8c182-228">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8c182-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8c182-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8c182-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c182-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8c182-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8c182-231">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8c182-231">Test single sign-on</span></span>

<span data-ttu-id="8c182-232">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8c182-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8c182-233">Quando si fa clic su riquadro Evernote hello in hello Pannello di accesso, è necessario ottenere connesso tooyour Evernote applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c182-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="8c182-234">Sarà possibile registrazione come un account aziendale ma toolog necessario con l'account personale.</span><span class="sxs-lookup"><span data-stu-id="8c182-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8c182-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8c182-235">Additional resources</span></span>

* [<span data-ttu-id="8c182-236">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c182-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c182-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c182-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Asana | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Asana.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="59851-103">Esercitazione: Integrazione di Azure Active Directory con Asana</span><span class="sxs-lookup"><span data-stu-id="59851-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="59851-104">In questa esercitazione, è illustrato come toointegrate Asana con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59851-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59851-105">Integrazione Asana con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="59851-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59851-106">È possibile controllare in Azure AD che ha accesso tooAsana</span><span class="sxs-lookup"><span data-stu-id="59851-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="59851-107">È possibile abilitare l'utenti tooautomatically get connesso tooAsana (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="59851-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59851-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="59851-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="59851-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59851-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59851-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="59851-110">Prerequisites</span></span>

<span data-ttu-id="59851-111">integrazione di Azure AD con Asana tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="59851-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="59851-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59851-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59851-113">Sottoscrizione di Asana abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="59851-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59851-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="59851-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59851-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="59851-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59851-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="59851-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59851-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59851-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59851-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="59851-118">Scenario description</span></span>
<span data-ttu-id="59851-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="59851-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59851-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="59851-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59851-121">Aggiunta di Asana dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="59851-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="59851-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59851-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="59851-123">Aggiunta di Asana dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="59851-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="59851-124">integrazione hello tooconfigure di Asana in Azure AD, è necessario tooadd Asana dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="59851-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59851-125">**tooadd Asana dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59851-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59851-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="59851-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="59851-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="59851-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59851-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="59851-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="59851-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="59851-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="59851-133">Nella casella di ricerca hello, digitare **Asana**selezionare **Asana** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="59851-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="59851-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59851-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="59851-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Asana in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="59851-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="59851-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Asana è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59851-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="59851-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Asana deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="59851-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="59851-139">In Asana, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="59851-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="59851-140">tooconfigure e prova AD Azure single sign-on con Asana, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="59851-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59851-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="59851-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59851-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59851-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59851-143">**[Creare un utente test Asana](#create-an-asana-test-user)**  -toohave un equivalente di Britta Simon in Asana che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="59851-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59851-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="59851-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59851-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="59851-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="59851-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59851-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="59851-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Asana.</span><span class="sxs-lookup"><span data-stu-id="59851-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="59851-148">**Azure AD tooconfigure single sign-on con Asana, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59851-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="59851-149">Nel portale di Azure su hello hello **Asana** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="59851-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="59851-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="59851-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="59851-153">In hello **Asana dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="59851-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="59851-155">a.</span><span class="sxs-lookup"><span data-stu-id="59851-155">a.</span></span> <span data-ttu-id="59851-156">In hello **Sign-on URL** casella di testo, digitare l'URL:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="59851-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="59851-157">b.</span><span class="sxs-lookup"><span data-stu-id="59851-157">b.</span></span> <span data-ttu-id="59851-158">In hello **identificatore** casella di testo, il valore di tipo:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="59851-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="59851-159">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="59851-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="59851-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="59851-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="59851-163">In hello **Asana configurazione** fare clic su **configurare Asana** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="59851-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="59851-164">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="59851-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="59851-166">In un'altra finestra del browser sign-on tooyour Asana applicazione.</span><span class="sxs-lookup"><span data-stu-id="59851-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="59851-167">tooconfigure SSO in Asana, le impostazioni di accesso hello dell'area di lavoro fare clic sul nome dell'area di lavoro hello in hello angolo superiore destro della schermata Ciao.</span><span class="sxs-lookup"><span data-stu-id="59851-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="59851-168">Fare quindi clic su **\<your workspace name\> Settings** (Impostazioni <nome area di lavoro>).</span><span class="sxs-lookup"><span data-stu-id="59851-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Impostazioni SSO di Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="59851-170">In hello **impostazioni organizzazione** finestra, fare clic su **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="59851-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="59851-171">Quindi, fare clic su **membri necessario effettuare l'accesso tramite SAML** tooenable configurazione di SSO hello.</span><span class="sxs-lookup"><span data-stu-id="59851-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="59851-172">Hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="59851-172">hello perform hello following steps:</span></span>
   
    ![Configurare le impostazioni dell'accesso Single Sign-On per l'organizzazione](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="59851-174">a.</span><span class="sxs-lookup"><span data-stu-id="59851-174">a.</span></span> <span data-ttu-id="59851-175">In hello **accesso URL della pagina** casella di testo, incollare hello **SAML Single Sign-On Service URL**.</span><span class="sxs-lookup"><span data-stu-id="59851-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="59851-176">b.</span><span class="sxs-lookup"><span data-stu-id="59851-176">b.</span></span> <span data-ttu-id="59851-177">Fare clic con il pulsante destro certificato hello scaricato dal portale di Azure, quindi aprire il file di certificato hello utilizzando blocco note o qualsiasi editor di testo.</span><span class="sxs-lookup"><span data-stu-id="59851-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="59851-178">Copia il contenuto di hello tra hello iniziare e hello fine certificato titolo e incollarlo in hello **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="59851-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="59851-179">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="59851-179">Click **Save**.</span></span> <span data-ttu-id="59851-180">Andare troppo[Asana Guida per la configurazione di SSO](https://asana.com/guide/help/premium/authentication#gl-saml) se è necessaria ulteriore assistenza.</span><span class="sxs-lookup"><span data-stu-id="59851-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="59851-181">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="59851-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="59851-182">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="59851-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="59851-183">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59851-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="59851-184">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59851-184">Create an Azure AD test user</span></span>

<span data-ttu-id="59851-185">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="59851-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="59851-187">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59851-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59851-188">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="59851-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59851-190">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="59851-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59851-192">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="59851-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59851-194">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="59851-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59851-196">a.</span><span class="sxs-lookup"><span data-stu-id="59851-196">a.</span></span> <span data-ttu-id="59851-197">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59851-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59851-198">b.</span><span class="sxs-lookup"><span data-stu-id="59851-198">b.</span></span> <span data-ttu-id="59851-199">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59851-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59851-200">c.</span><span class="sxs-lookup"><span data-stu-id="59851-200">c.</span></span> <span data-ttu-id="59851-201">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="59851-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="59851-202">d.</span><span class="sxs-lookup"><span data-stu-id="59851-202">d.</span></span> <span data-ttu-id="59851-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="59851-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="59851-204">Creare un utente test per Asana</span><span class="sxs-lookup"><span data-stu-id="59851-204">Create an Asana test user</span></span>

<span data-ttu-id="59851-205">In questa sezione viene creato un utente di nome Britta Simon in Asana.</span><span class="sxs-lookup"><span data-stu-id="59851-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="59851-206">In **Asana**, visitare toohello **Team** sezione nel riquadro di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="59851-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="59851-207">Fare clic su hello segno pulsante.</span><span class="sxs-lookup"><span data-stu-id="59851-207">Click hello plus sign button.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="59851-209">Tipo di messaggio di posta elettronica hello britta.simon@contoso.com nella casella di testo hello e quindi selezionare **invitare**.</span><span class="sxs-lookup"><span data-stu-id="59851-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="59851-210">Fare clic su **Send Invite** (Invia invito).</span><span class="sxs-lookup"><span data-stu-id="59851-210">Click **Send Invite**.</span></span> <span data-ttu-id="59851-211">nuovo utente Hello riceverà un messaggio di posta elettronica nel proprio account di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="59851-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="59851-212">Lei sarà anche necessario toocreate e convalidare l'account hello.</span><span class="sxs-lookup"><span data-stu-id="59851-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="59851-213">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="59851-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="59851-214">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAsana.</span><span class="sxs-lookup"><span data-stu-id="59851-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Assegnazione del ruolo utente hello][200]

<span data-ttu-id="59851-216">**tooassign Britta Simon tooAsana, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59851-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="59851-217">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="59851-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="59851-219">Nell'elenco di applicazioni hello, selezionare **Asana**.</span><span class="sxs-lookup"><span data-stu-id="59851-219">In hello applications list, select **Asana**.</span></span>

    ![collegamento Asana Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="59851-221">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="59851-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="59851-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="59851-223">Click **Add** button.</span></span> <span data-ttu-id="59851-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="59851-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="59851-226">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="59851-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59851-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="59851-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59851-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="59851-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="59851-229">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="59851-229">Test single sign-on</span></span>

<span data-ttu-id="59851-230">obiettivo di Hello di questa sezione è tootest il Azure single sign-on AD.</span><span class="sxs-lookup"><span data-stu-id="59851-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="59851-231">Visitare la pagina di accesso tooAsana.</span><span class="sxs-lookup"><span data-stu-id="59851-231">Go tooAsana login page.</span></span> <span data-ttu-id="59851-232">Nella casella Indirizzo di posta elettronica hello, inserire l'indirizzo di posta elettronica hello britta.simon@contoso.com. Lasciare una casella di testo password hello spazio vuoto e quindi fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="59851-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="59851-233">Sarà reindirizzato tooAzure AD pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="59851-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="59851-234">Completare le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59851-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="59851-235">A questo punto si è connessi ad Asana.</span><span class="sxs-lookup"><span data-stu-id="59851-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59851-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="59851-236">Additional resources</span></span>

* [<span data-ttu-id="59851-237">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59851-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59851-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59851-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png

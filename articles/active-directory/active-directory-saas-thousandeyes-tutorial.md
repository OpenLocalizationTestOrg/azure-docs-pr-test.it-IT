---
title: 'Esercitazione: Integrazione di Azure Active Directory con ThousandEyes | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ThousandEyes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="f942f-103">Esercitazione: Integrazione di Azure Active Directory con ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="f942f-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="f942f-104">In questa esercitazione, è illustrato come toointegrate ThousandEyes con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f942f-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f942f-105">Integrazione di ThousandEyes con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f942f-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f942f-106">È possibile controllare in Azure AD che ha accesso tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="f942f-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="f942f-107">È possibile abilitare l'utenti tooautomatically get connesso tooThousandEyes (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f942f-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f942f-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f942f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f942f-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f942f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f942f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f942f-110">Prerequisites</span></span>

<span data-ttu-id="f942f-111">integrazione di Azure AD con ThousandEyes tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f942f-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="f942f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f942f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f942f-113">Una sottoscrizione di ThousandEyes abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f942f-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f942f-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f942f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f942f-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f942f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f942f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f942f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f942f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f942f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f942f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f942f-118">Scenario description</span></span>
<span data-ttu-id="f942f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f942f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f942f-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f942f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f942f-121">Aggiunta di ThousandEyes dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f942f-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="f942f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f942f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="f942f-123">Aggiunta di ThousandEyes dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f942f-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="f942f-124">integrazione hello tooconfigure di ThousandEyes in Azure AD, è necessario tooadd ThousandEyes dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f942f-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f942f-125">**tooadd ThousandEyes dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f942f-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f942f-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f942f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f942f-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f942f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f942f-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f942f-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f942f-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f942f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f942f-133">Nella casella di ricerca hello, digitare **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="f942f-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="f942f-135">Nel riquadro dei risultati hello, selezionare **ThousandEyes**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f942f-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f942f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f942f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f942f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ThousandEyes usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f942f-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f942f-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ThousandEyes è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f942f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="f942f-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ThousandEyes deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f942f-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="f942f-141">In ThousandEyes, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="f942f-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f942f-142">tooconfigure e prova AD Azure single sign-on con ThousandEyes, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f942f-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f942f-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f942f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f942f-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f942f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f942f-145">**[Creazione di un utente test ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave un equivalente di Britta Simon in ThousandEyes che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f942f-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f942f-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f942f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f942f-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f942f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f942f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f942f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f942f-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="f942f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="f942f-150">**Azure AD tooconfigure single sign-on con ThousandEyes, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f942f-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="f942f-151">Nel portale di Azure su hello hello **ThousandEyes** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f942f-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f942f-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f942f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="f942f-155">In hello **ThousandEyes dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f942f-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="f942f-157">In hello **Sign-on URL** casella di testo, digitare un URL come:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="f942f-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="f942f-158">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f942f-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="f942f-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f942f-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f942f-162">In hello **ThousandEyes configurazione** fare clic su **configurare ThousandEyes** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f942f-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f942f-163">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f942f-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="f942f-165">In una finestra del web browser, accedere tooyour **ThousandEyes** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f942f-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="f942f-166">Scegliere dal menu hello in primo piano hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="f942f-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="f942f-167">![Impostazioni](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="f942f-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="f942f-168">Fare clic su **Account**</span><span class="sxs-lookup"><span data-stu-id="f942f-168">Click **Account**</span></span>
   
    <span data-ttu-id="f942f-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="f942f-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="f942f-170">Fare clic su hello **sicurezza e autenticazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="f942f-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="f942f-171">![Sicurezza e autenticazione](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security e autenticazione")</span><span class="sxs-lookup"><span data-stu-id="f942f-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="f942f-172">In hello **Setup Single Sign-On** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f942f-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f942f-173">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f942f-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="f942f-174">a.</span><span class="sxs-lookup"><span data-stu-id="f942f-174">a.</span></span> <span data-ttu-id="f942f-175">Selezionare **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f942f-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="f942f-176">b.</span><span class="sxs-lookup"><span data-stu-id="f942f-176">b.</span></span> <span data-ttu-id="f942f-177">Nella casella di testo **Login Page URL** (URL pagina di accesso) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f942f-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="f942f-178">c.</span><span class="sxs-lookup"><span data-stu-id="f942f-178">c.</span></span> <span data-ttu-id="f942f-179">Nella casella di testo **Logout Page URL** (URL pagina di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f942f-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="f942f-180">d.</span><span class="sxs-lookup"><span data-stu-id="f942f-180">d.</span></span> <span data-ttu-id="f942f-181">Nella casella di testo **Autorità di certificazione del provider di identità** incollare l'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f942f-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="f942f-182">e.</span><span class="sxs-lookup"><span data-stu-id="f942f-182">e.</span></span> <span data-ttu-id="f942f-183">In **certificato di verifica**, fare clic su **Choose file**e quindi caricare il certificato di hello scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f942f-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="f942f-184">f.</span><span class="sxs-lookup"><span data-stu-id="f942f-184">f.</span></span> <span data-ttu-id="f942f-185">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f942f-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="f942f-186">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f942f-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f942f-187">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f942f-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f942f-188">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f942f-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f942f-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f942f-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="f942f-190">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f942f-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f942f-192">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f942f-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f942f-193">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f942f-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f942f-195">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f942f-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f942f-197">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f942f-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f942f-199">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f942f-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f942f-201">a.</span><span class="sxs-lookup"><span data-stu-id="f942f-201">a.</span></span> <span data-ttu-id="f942f-202">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f942f-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f942f-203">b.</span><span class="sxs-lookup"><span data-stu-id="f942f-203">b.</span></span> <span data-ttu-id="f942f-204">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f942f-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f942f-205">c.</span><span class="sxs-lookup"><span data-stu-id="f942f-205">c.</span></span> <span data-ttu-id="f942f-206">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f942f-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f942f-207">d.</span><span class="sxs-lookup"><span data-stu-id="f942f-207">d.</span></span> <span data-ttu-id="f942f-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f942f-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="f942f-209">Creazione di un utente di test di ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="f942f-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="f942f-210">In ordine tooenable Azure AD utenti toolog a ThousandEyes, è necessario eseguirne il provisioning in ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="f942f-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="f942f-211">Nel caso di hello di ThousandEyes, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f942f-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="f942f-212">È possibile usare qualsiasi altro ThousandEyes utente account strumento di creazione o le API fornite da ThousandEyes tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="f942f-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="f942f-213">**tooprovision tooThousandEyes un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f942f-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="f942f-214">Accedere al sito aziendale di ThousandEyes come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f942f-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="f942f-215">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="f942f-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="f942f-216">![Impostazioni](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="f942f-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="f942f-217">Fare clic su **Account**.</span><span class="sxs-lookup"><span data-stu-id="f942f-217">Click **Account**.</span></span>
   
    <span data-ttu-id="f942f-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span><span class="sxs-lookup"><span data-stu-id="f942f-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="f942f-219">Fare clic su hello **account e utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="f942f-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="f942f-220">![Account e utenti](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Account e utenti")</span><span class="sxs-lookup"><span data-stu-id="f942f-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="f942f-221">In hello **aggiungere utenti e account** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f942f-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f942f-222">![Aggiungere account utente](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Aggiungere account utente")</span><span class="sxs-lookup"><span data-stu-id="f942f-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="f942f-223">a.</span><span class="sxs-lookup"><span data-stu-id="f942f-223">a.</span></span> <span data-ttu-id="f942f-224">In **nome** casella di testo Nome hello del tipo di utente come **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f942f-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="f942f-225">b.</span><span class="sxs-lookup"><span data-stu-id="f942f-225">b.</span></span> <span data-ttu-id="f942f-226">In **posta elettronica** casella Tipo hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f942f-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="f942f-227">b.</span><span class="sxs-lookup"><span data-stu-id="f942f-227">b.</span></span> <span data-ttu-id="f942f-228">Fare clic su **tooAccount Add New User**.</span><span class="sxs-lookup"><span data-stu-id="f942f-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="f942f-229">titolare dell'account di Azure Active Directory Hello otterrà un messaggio di posta elettronica inclusi tooconfirm un collegamento e attivare hello account.</span><span class="sxs-lookup"><span data-stu-id="f942f-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f942f-230">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f942f-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f942f-231">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="f942f-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f942f-233">**tooassign Britta Simon tooThousandEyes, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f942f-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="f942f-234">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f942f-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f942f-236">Nell'elenco di applicazioni hello, selezionare **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="f942f-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="f942f-238">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f942f-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f942f-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f942f-240">Click **Add** button.</span></span> <span data-ttu-id="f942f-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f942f-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f942f-243">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f942f-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f942f-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f942f-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f942f-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f942f-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f942f-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f942f-246">Testing single sign-on</span></span>

<span data-ttu-id="f942f-247">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f942f-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f942f-248">Quando si fa clic hello ThousandEyes riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="f942f-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="f942f-249">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f942f-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f942f-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f942f-250">Additional resources</span></span>

* [<span data-ttu-id="f942f-251">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f942f-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f942f-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f942f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png


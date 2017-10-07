---
title: 'Esercitazione: Integrazione di Azure Active Directory con Intacct | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Intacct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="461f0-103">Esercitazione: Integrazione di Azure Active Directory con Intacct</span><span class="sxs-lookup"><span data-stu-id="461f0-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="461f0-104">In questa esercitazione, è illustrato come toointegrate Intacct con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="461f0-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="461f0-105">Integrazione di Intacct con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="461f0-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="461f0-106">È possibile controllare in Azure AD che ha accesso tooIntacct</span><span class="sxs-lookup"><span data-stu-id="461f0-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="461f0-107">È possibile abilitare l'utenti tooautomatically get connesso tooIntacct (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="461f0-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="461f0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="461f0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="461f0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="461f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="461f0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="461f0-110">Prerequisites</span></span>

<span data-ttu-id="461f0-111">integrazione di Azure AD con Intacct tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="461f0-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="461f0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="461f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="461f0-113">Sottoscrizione di Intacct abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="461f0-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="461f0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="461f0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="461f0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="461f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="461f0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="461f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="461f0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="461f0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="461f0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="461f0-118">Scenario description</span></span>
<span data-ttu-id="461f0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="461f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="461f0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="461f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="461f0-121">Aggiunta di Intacct dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="461f0-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="461f0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="461f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="461f0-123">Aggiunta di Intacct dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="461f0-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="461f0-124">integrazione hello tooconfigure di Intacct in Azure AD, è necessario tooadd Intacct dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="461f0-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="461f0-125">**tooadd Intacct dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="461f0-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="461f0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="461f0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="461f0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="461f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="461f0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="461f0-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="461f0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="461f0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="461f0-133">Nella casella di ricerca hello, digitare **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="461f0-133">In hello search box, type **Intacct**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="461f0-135">Nel riquadro dei risultati hello, selezionare **Intacct**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="461f0-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="461f0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="461f0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="461f0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Intacct con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="461f0-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="461f0-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Intacct è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="461f0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="461f0-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Intacct deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="461f0-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="461f0-141">In Intacct, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="461f0-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="461f0-142">tooconfigure e prova AD Azure single sign-on con Intacct, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="461f0-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="461f0-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="461f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="461f0-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="461f0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="461f0-145">**[Creazione di un utente test Intacct](#creating-an-intacct-test-user)**  -toohave un equivalente di Britta Simon in Intacct che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="461f0-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="461f0-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="461f0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="461f0-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="461f0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="461f0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="461f0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="461f0-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Intacct.</span><span class="sxs-lookup"><span data-stu-id="461f0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="461f0-150">**Azure AD tooconfigure single sign-on con Intacct, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="461f0-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="461f0-151">Nel portale di Azure su hello hello **Intacct** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="461f0-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="461f0-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="461f0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="461f0-155">In hello **Intacct dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="461f0-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="461f0-157">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="461f0-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="461f0-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="461f0-158">This value is not real.</span></span> <span data-ttu-id="461f0-159">Aggiornare questo valore con l'URL di risposta effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="461f0-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="461f0-160">Contatto [team di supporto Intacct](https://us.intacct.com/support) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="461f0-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="461f0-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="461f0-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="461f0-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="461f0-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="461f0-165">In hello **Intacct configurazione** fare clic su **configurare Intacct** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="461f0-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="461f0-166">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="461f0-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="461f0-168">In una finestra del web browser, accedere come amministratore nel sito della società Intacct di tooyour.</span><span class="sxs-lookup"><span data-stu-id="461f0-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="461f0-169">Fare clic su hello **aziendale** scheda e quindi fare clic su **informazioni sulla società**.</span><span class="sxs-lookup"><span data-stu-id="461f0-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="461f0-170">![Azienda](./media/active-directory-saas-intacct-tutorial/ic790037.png "Azienda")</span><span class="sxs-lookup"><span data-stu-id="461f0-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="461f0-171">Fare clic su hello **sicurezza** scheda e quindi fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="461f0-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="461f0-172">![Sicurezza](./media/active-directory-saas-intacct-tutorial/ic790038.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="461f0-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="461f0-173">In hello **Single sign-on (SSO)** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="461f0-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="461f0-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span><span class="sxs-lookup"><span data-stu-id="461f0-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="461f0-175">a.</span><span class="sxs-lookup"><span data-stu-id="461f0-175">a.</span></span> <span data-ttu-id="461f0-176">Selezionare **Abilita Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="461f0-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="461f0-177">b.</span><span class="sxs-lookup"><span data-stu-id="461f0-177">b.</span></span> <span data-ttu-id="461f0-178">In **Identity provider type** (Tipo di provider di identità) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="461f0-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="461f0-179">c.</span><span class="sxs-lookup"><span data-stu-id="461f0-179">c.</span></span> <span data-ttu-id="461f0-180">In **URL autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="461f0-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="461f0-181">d.</span><span class="sxs-lookup"><span data-stu-id="461f0-181">d.</span></span> <span data-ttu-id="461f0-182">In **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="461f0-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="461f0-183">e.</span><span class="sxs-lookup"><span data-stu-id="461f0-183">e.</span></span> <span data-ttu-id="461f0-184">Aprire il **base 64** codificato nel blocco note, hello copia del contenuto di esso negli Appunti, certificato e quindi incollarlo toohello **certificato** casella.</span><span class="sxs-lookup"><span data-stu-id="461f0-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="461f0-185">f.</span><span class="sxs-lookup"><span data-stu-id="461f0-185">f.</span></span> <span data-ttu-id="461f0-186">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="461f0-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="461f0-187">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="461f0-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="461f0-188">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="461f0-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="461f0-189">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="461f0-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="461f0-190">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="461f0-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="461f0-191">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="461f0-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="461f0-193">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="461f0-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="461f0-194">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="461f0-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="461f0-196">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="461f0-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="461f0-198">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="461f0-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="461f0-200">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="461f0-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="461f0-202">a.</span><span class="sxs-lookup"><span data-stu-id="461f0-202">a.</span></span> <span data-ttu-id="461f0-203">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="461f0-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="461f0-204">b.</span><span class="sxs-lookup"><span data-stu-id="461f0-204">b.</span></span> <span data-ttu-id="461f0-205">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="461f0-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="461f0-206">c.</span><span class="sxs-lookup"><span data-stu-id="461f0-206">c.</span></span> <span data-ttu-id="461f0-207">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="461f0-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="461f0-208">d.</span><span class="sxs-lookup"><span data-stu-id="461f0-208">d.</span></span> <span data-ttu-id="461f0-209">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="461f0-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="461f0-210">Creazione di un utente di test di Intacct</span><span class="sxs-lookup"><span data-stu-id="461f0-210">Creating an Intacct test user</span></span>

<span data-ttu-id="461f0-211">tooset di utenti di Azure AD in modo che possano accedere tooIntacct, è necessario eseguirne il provisioning in Intacct.</span><span class="sxs-lookup"><span data-stu-id="461f0-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="461f0-212">In Intacct il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="461f0-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="461f0-213">**gli account utente tooprovision, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="461f0-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="461f0-214">Accedi tooyour **Intacct** tenant.</span><span class="sxs-lookup"><span data-stu-id="461f0-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="461f0-215">Fare clic su hello **aziendale** scheda e quindi fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="461f0-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="461f0-216">![Utenti](./media/active-directory-saas-intacct-tutorial/ic790041.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="461f0-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="461f0-217">Fare clic su hello **Aggiungi** scheda.</span><span class="sxs-lookup"><span data-stu-id="461f0-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="461f0-218">![Aggiungi](./media/active-directory-saas-intacct-tutorial/ic790042.png "Aggiungi")</span><span class="sxs-lookup"><span data-stu-id="461f0-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="461f0-219">In hello **informazioni utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="461f0-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="461f0-220">![Informazioni utente](./media/active-directory-saas-intacct-tutorial/ic790043.png "Informazioni utente")</span><span class="sxs-lookup"><span data-stu-id="461f0-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="461f0-221">a.</span><span class="sxs-lookup"><span data-stu-id="461f0-221">a.</span></span> <span data-ttu-id="461f0-222">Immettere hello **ID utente**, hello **cognome**, **nome**, hello **indirizzo di posta elettronica**, hello **titolo**, hello e **Phone** di un account di Azure AD che si desidera tooprovision in hello **informazioni utente** sezione.</span><span class="sxs-lookup"><span data-stu-id="461f0-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="461f0-223">b.</span><span class="sxs-lookup"><span data-stu-id="461f0-223">b.</span></span> <span data-ttu-id="461f0-224">Seleziona hello **privilegi di amministratore** di un account di Azure AD che si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="461f0-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="461f0-225">c.</span><span class="sxs-lookup"><span data-stu-id="461f0-225">c.</span></span> <span data-ttu-id="461f0-226">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="461f0-226">Click **Save**.</span></span> <span data-ttu-id="461f0-227">titolare dell'account di Azure AD Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="461f0-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="461f0-228">tooprovision account utente di Azure AD, è possibile utilizzare altri strumenti di creazione di account utente Intacct o le API fornite da Intacct.</span><span class="sxs-lookup"><span data-stu-id="461f0-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="461f0-229">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="461f0-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="461f0-230">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIntacct.</span><span class="sxs-lookup"><span data-stu-id="461f0-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Assegna utente][200] 

<span data-ttu-id="461f0-232">**tooassign Britta Simon tooIntacct, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="461f0-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="461f0-233">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="461f0-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="461f0-235">Nell'elenco di applicazioni hello, selezionare **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="461f0-235">In hello applications list, select **Intacct**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="461f0-237">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="461f0-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="461f0-239">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="461f0-239">Click **Add** button.</span></span> <span data-ttu-id="461f0-240">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="461f0-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="461f0-242">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="461f0-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="461f0-243">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="461f0-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="461f0-244">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="461f0-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="461f0-245">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="461f0-245">Testing single sign-on</span></span>

<span data-ttu-id="461f0-246">In questa sezione Configurazione di Azure AD single sign-on utilizzare test hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="461f0-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="461f0-247">Quando si fa clic su riquadro Intacct hello nel Pannello di accesso hello, è necessario essere connessi automaticamente tooyour applicazione Intacct.</span><span class="sxs-lookup"><span data-stu-id="461f0-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="461f0-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="461f0-248">Additional resources</span></span>

* [<span data-ttu-id="461f0-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="461f0-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="461f0-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="461f0-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png


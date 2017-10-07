---
title: 'Esercitazione: Integrazione di Azure Active Directory con Menlo Security | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e di sicurezza Menlo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="79a69-103">Esercitazione: Integrazione di Azure Active Directory con Menlo Security</span><span class="sxs-lookup"><span data-stu-id="79a69-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="79a69-104">In questa esercitazione, è illustrato come toointegrate Menlo sicurezza con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79a69-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79a69-105">Integrazione di protezione Menlo con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="79a69-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79a69-106">È possibile controllare in Azure AD che ha accesso tooMenlo, sicurezza</span><span class="sxs-lookup"><span data-stu-id="79a69-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="79a69-107">È possibile abilitare l'utenti tooautomatically get connesso tooMenlo sicurezza (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a69-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79a69-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="79a69-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79a69-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="79a69-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="79a69-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79a69-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79a69-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="79a69-111">Prerequisites</span></span>

<span data-ttu-id="79a69-112">integrazione di Azure AD con sicurezza Menlo tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="79a69-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="79a69-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a69-113">An Azure AD subscription</span></span>
- <span data-ttu-id="79a69-114">Sottoscrizione di Menlo Security abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="79a69-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79a69-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="79a69-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79a69-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="79a69-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79a69-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="79a69-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79a69-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79a69-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79a69-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="79a69-119">Scenario description</span></span>
<span data-ttu-id="79a69-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="79a69-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79a69-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="79a69-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79a69-122">Aggiunta di sicurezza Menlo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="79a69-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="79a69-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a69-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="79a69-124">Aggiunta di sicurezza Menlo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="79a69-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="79a69-125">integrazione hello tooconfigure di sicurezza Menlo in Azure AD, è necessario tooadd Menlo sicurezza dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="79a69-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79a69-126">**tooadd Menlo sicurezza dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="79a69-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a69-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="79a69-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79a69-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="79a69-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79a69-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="79a69-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="79a69-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="79a69-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="79a69-134">Nella casella di ricerca hello, digitare **Menlo sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="79a69-134">In hello search box, type **Menlo Security**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="79a69-136">Nel riquadro dei risultati hello, selezionare **Menlo sicurezza**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="79a69-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79a69-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a69-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79a69-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Menlo Security con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="79a69-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79a69-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in sicurezza Menlo è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a69-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="79a69-141">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in sicurezza Menlo deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="79a69-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="79a69-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Menlo protezione.</span><span class="sxs-lookup"><span data-stu-id="79a69-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="79a69-143">tooconfigure e prova AD Azure single sign-on con Menlo sicurezza, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="79a69-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79a69-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="79a69-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79a69-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79a69-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79a69-146">**[Creazione di un utente test sicurezza Menlo](#creating-a-menlo-security-test-user)**  -toohave un equivalente di Britta Simon nella sicurezza Menlo che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="79a69-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79a69-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="79a69-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79a69-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="79a69-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79a69-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a69-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79a69-150">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Menlo sicurezza.</span><span class="sxs-lookup"><span data-stu-id="79a69-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="79a69-151">**Azure AD tooconfigure single sign-on con sicurezza Menlo, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="79a69-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a69-152">Nel portale di Azure su hello hello **Menlo sicurezza** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="79a69-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="79a69-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="79a69-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="79a69-156">In hello **URL e il dominio di sicurezza Menlo** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="79a69-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="79a69-158">a.</span><span class="sxs-lookup"><span data-stu-id="79a69-158">a.</span></span> <span data-ttu-id="79a69-159">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="79a69-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="79a69-160">b.</span><span class="sxs-lookup"><span data-stu-id="79a69-160">b.</span></span> <span data-ttu-id="79a69-161">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="79a69-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79a69-162">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="79a69-162">These values are not hello real.</span></span> <span data-ttu-id="79a69-163">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="79a69-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="79a69-164">Contatto [team di supporto Client di protezione Menlo](https://www.menlosecurity.com/menlo-contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="79a69-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="79a69-165">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="79a69-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="79a69-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="79a69-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79a69-169">In hello **configurazione della sicurezza Menlo** fare clic su **configurare la sicurezza Menlo** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="79a69-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="79a69-170">Hello copia **ID entità SAML**, e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="79a69-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="79a69-172">tooconfigure single sign-on sul **Menlo sicurezza** lato, account di accesso toohello **Menlo sicurezza** sito Web come amministratore.</span><span class="sxs-lookup"><span data-stu-id="79a69-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="79a69-173">In **impostazioni** andare troppo**autenticazione** ed eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="79a69-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="79a69-175">a.</span><span class="sxs-lookup"><span data-stu-id="79a69-175">a.</span></span> <span data-ttu-id="79a69-176">Selezionare la casella di controllo di hello **abilitare l'autenticazione utente tramite SAML**.</span><span class="sxs-lookup"><span data-stu-id="79a69-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="79a69-177">b.</span><span class="sxs-lookup"><span data-stu-id="79a69-177">b.</span></span> <span data-ttu-id="79a69-178">Selezionare **consentire l'accesso esterno** troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="79a69-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="79a69-179">c.</span><span class="sxs-lookup"><span data-stu-id="79a69-179">c.</span></span> <span data-ttu-id="79a69-180">In **SAML Provider** (Provider SAML), selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79a69-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="79a69-181">d.</span><span class="sxs-lookup"><span data-stu-id="79a69-181">d.</span></span> <span data-ttu-id="79a69-182">**SAML 2.0 Endpoint** : hello Incolla **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="79a69-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="79a69-183">e.</span><span class="sxs-lookup"><span data-stu-id="79a69-183">e.</span></span> <span data-ttu-id="79a69-184">**Identificatore del servizio (autorità di certificazione)** : hello Incolla **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="79a69-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="79a69-185">f.</span><span class="sxs-lookup"><span data-stu-id="79a69-185">f.</span></span> <span data-ttu-id="79a69-186">**Certificato x. 509** : hello aprire **certificato (Base64)** scaricato dal portale di Azure di hello nel blocco note e incollarlo in questa casella.</span><span class="sxs-lookup"><span data-stu-id="79a69-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="79a69-187">g.</span><span class="sxs-lookup"><span data-stu-id="79a69-187">g.</span></span> <span data-ttu-id="79a69-188">Fare clic su **salvare** impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="79a69-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="79a69-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="79a69-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79a69-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="79a69-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79a69-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79a69-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79a69-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a69-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="79a69-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="79a69-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="79a69-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="79a69-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a69-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="79a69-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79a69-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="79a69-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79a69-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="79a69-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79a69-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="79a69-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79a69-204">a.</span><span class="sxs-lookup"><span data-stu-id="79a69-204">a.</span></span> <span data-ttu-id="79a69-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79a69-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79a69-206">b.</span><span class="sxs-lookup"><span data-stu-id="79a69-206">b.</span></span> <span data-ttu-id="79a69-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79a69-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79a69-208">c.</span><span class="sxs-lookup"><span data-stu-id="79a69-208">c.</span></span> <span data-ttu-id="79a69-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="79a69-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79a69-210">d.</span><span class="sxs-lookup"><span data-stu-id="79a69-210">d.</span></span> <span data-ttu-id="79a69-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="79a69-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="79a69-212">Creazione di un utente test di Menlo Security</span><span class="sxs-lookup"><span data-stu-id="79a69-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="79a69-213">In questa sezione viene creato un utente chiamato Britta Simon in Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="79a69-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="79a69-214">Lavorare con [team di supporto Client di protezione Menlo](https://www.menlosecurity.com/menlo-contact) utenti hello tooadd nella piattaforma di sicurezza Menlo hello.</span><span class="sxs-lookup"><span data-stu-id="79a69-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="79a69-215">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="79a69-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79a69-216">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a69-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79a69-217">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMenlo sicurezza.</span><span class="sxs-lookup"><span data-stu-id="79a69-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Assegna utente][200] 

<span data-ttu-id="79a69-219">**tooassign Britta Simon tooMenlo protezione, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="79a69-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a69-220">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="79a69-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="79a69-222">Nell'elenco di applicazioni hello, selezionare **Menlo sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="79a69-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="79a69-224">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="79a69-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="79a69-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="79a69-226">Click **Add** button.</span></span> <span data-ttu-id="79a69-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="79a69-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="79a69-229">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="79a69-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79a69-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="79a69-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79a69-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="79a69-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79a69-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="79a69-232">Testing single sign-on</span></span>

<span data-ttu-id="79a69-233">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a69-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="79a69-234">Aprire una finestra del browser in un tootrigger modalità "InPrivate" o "Incognito" una nuova autenticazione.</span><span class="sxs-lookup"><span data-stu-id="79a69-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="79a69-235">In Internet Explorer usare CTRL+MAIUSC+P.</span><span class="sxs-lookup"><span data-stu-id="79a69-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="79a69-236">In Chrome usare CTRL+MAIUSC+N.</span><span class="sxs-lookup"><span data-stu-id="79a69-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="79a69-237">Nella finestra di esplorazione privata di hello, tooa Sfoglia risorsa protetta ed eseguire un account di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a69-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="79a69-238">Dopo l'accesso ha esito positivo, sarà eseguito toohello richiesto sito in una sessione di isolamento.</span><span class="sxs-lookup"><span data-stu-id="79a69-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79a69-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="79a69-239">Additional resources</span></span>

* [<span data-ttu-id="79a69-240">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79a69-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79a69-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79a69-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Veritas Enterprise Vault.cloud SSO | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Veritas Enterprise Vault.cloud SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 1037e70515686091460ac41e9e5a7951639bb520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a><span data-ttu-id="b0e24-103">Esercitazione: Integrazione di Azure Active Directory con Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="b0e24-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span></span>

<span data-ttu-id="b0e24-104">In questa esercitazione, è illustrato come toointegrate Veritas Enterprise Vault.cloud SSO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0e24-104">In this tutorial, you learn how toointegrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0e24-105">Integrazione di Veritas Enterprise Vault.cloud SSO con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b0e24-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0e24-106">È possibile controllare in Azure AD che ha accesso tooVeritas Vault.cloud Enterprise SSO</span><span class="sxs-lookup"><span data-stu-id="b0e24-106">You can control in Azure AD who has access tooVeritas Enterprise Vault.cloud SSO</span></span>
- <span data-ttu-id="b0e24-107">È possibile abilitare l'utenti tooautomatically get connesso tooVeritas Enterprise Vault.cloud SSO (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0e24-107">You can enable your users tooautomatically get signed-on tooVeritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0e24-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0e24-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0e24-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0e24-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0e24-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b0e24-110">Prerequisites</span></span>

<span data-ttu-id="b0e24-111">tooconfigure integrazione di Azure AD con Veritas Enterprise Vault.cloud SSO, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b0e24-111">tooconfigure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need hello following items:</span></span>

- <span data-ttu-id="b0e24-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0e24-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0e24-113">Sottoscrizione di Veritas Enterprise Vault.cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b0e24-113">A Veritas Enterprise Vault.cloud SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0e24-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b0e24-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0e24-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b0e24-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0e24-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b0e24-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0e24-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0e24-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0e24-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b0e24-118">Scenario description</span></span>
<span data-ttu-id="b0e24-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b0e24-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0e24-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b0e24-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0e24-121">Aggiunta di Veritas Enterprise Vault.cloud SSO dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b0e24-121">Adding Veritas Enterprise Vault.cloud SSO from hello gallery</span></span>
2. <span data-ttu-id="b0e24-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0e24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-hello-gallery"></a><span data-ttu-id="b0e24-123">Aggiunta di Veritas Enterprise Vault.cloud SSO dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b0e24-123">Adding Veritas Enterprise Vault.cloud SSO from hello gallery</span></span>
<span data-ttu-id="b0e24-124">integrazione hello tooconfigure di Veritas Enterprise Vault.cloud SSO in Azure AD, è necessario tooadd Veritas Enterprise Vault.cloud SSO dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b0e24-124">tooconfigure hello integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need tooadd Veritas Enterprise Vault.cloud SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0e24-125">**tooadd Veritas Enterprise Vault.cloud SSO dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0e24-125">**tooadd Veritas Enterprise Vault.cloud SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0e24-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b0e24-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0e24-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0e24-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b0e24-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b0e24-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b0e24-133">Nella casella di ricerca hello, digitare **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-133">In hello search box, type **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_search.png)

5. <span data-ttu-id="b0e24-135">Nel riquadro dei risultati hello, selezionare **Veritas Enterprise Vault.cloud SSO**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0e24-135">In hello results panel, select **Veritas Enterprise Vault.cloud SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0e24-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0e24-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0e24-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Veritas Enterprise Vault.cloud SSO usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b0e24-138">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0e24-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Veritas Enterprise Vault.cloud SSO è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0e24-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veritas Enterprise Vault.cloud SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="b0e24-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Veritas Enterprise Vault.cloud SSO richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b0e24-140">In other words, a link relationship between an Azure AD user and hello related user in Veritas Enterprise Vault.cloud SSO needs toobe established.</span></span>

<span data-ttu-id="b0e24-141">In Veritas Enterprise Vault.cloud SSO, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="b0e24-141">In Veritas Enterprise Vault.cloud SSO, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b0e24-142">tooconfigure e prova AD Azure single sign-on con Veritas Enterprise Vault.cloud SSO, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b0e24-142">tooconfigure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0e24-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b0e24-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0e24-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0e24-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0e24-145">**[Creazione di un utente test Veritas Enterprise Vault.cloud SSO](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)**  -toohave un equivalente di Britta Simon in Veritas Enterprise SSO Vault.cloud che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b0e24-145">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - toohave a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0e24-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0e24-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0e24-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b0e24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0e24-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0e24-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0e24-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="b0e24-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span></span>

<span data-ttu-id="b0e24-150">**tooconfigure AD Azure single sign-on con Veritas Enterprise Vault.cloud SSO, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0e24-150">**tooconfigure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0e24-151">Nel portale di Azure su hello hello **Veritas Enterprise Vault.cloud SSO** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-151">In hello Azure portal, on hello **Veritas Enterprise Vault.cloud SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b0e24-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0e24-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_samlbase.png)

3. <span data-ttu-id="b0e24-155">In hello **Veritas Enterprise Vault.cloud SSO dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b0e24-155">On hello **Veritas Enterprise Vault.cloud SSO Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_url.png)

    <span data-ttu-id="b0e24-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span><span class="sxs-lookup"><span data-stu-id="b0e24-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b0e24-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="b0e24-158">This value is not real.</span></span> <span data-ttu-id="b0e24-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b0e24-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b0e24-160">Contatto [team di supporto di Veritas Enterprise Vault.cloud SSO Client](https://www.veritas.com/support/.html) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="b0e24-160">Contact [Veritas Enterprise Vault.cloud SSO Client support team](https://www.veritas.com/support/.html) tooget this value.</span></span> 

4. <span data-ttu-id="b0e24-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b0e24-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_certificate.png) 

5. <span data-ttu-id="b0e24-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b0e24-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0e24-165">In hello **configurazione di SSO Veritas Enterprise Vault.cloud** fare clic su **configurare Veritas Enterprise SSO Vault.cloud** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="b0e24-165">On hello **Veritas Enterprise Vault.cloud SSO Configuration** section, click **Configure Veritas Enterprise Vault.cloud SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b0e24-166">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b0e24-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_configure.png) 

7. <span data-ttu-id="b0e24-168">tooconfigure single sign-on sul **Veritas Enterprise Vault.cloud SSO** lato, è necessario hello toosend scaricato **Certificate(Base64)** e **SAML Single Sign-On Service URL**troppo[team di supporto di Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html).</span><span class="sxs-lookup"><span data-stu-id="b0e24-168">tooconfigure single sign-on on **Veritas Enterprise Vault.cloud SSO** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html).</span></span>

> [!TIP]
> <span data-ttu-id="b0e24-169">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b0e24-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0e24-170">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b0e24-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0e24-171">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0e24-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0e24-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0e24-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0e24-173">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b0e24-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b0e24-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0e24-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0e24-176">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b0e24-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0e24-178">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0e24-180">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b0e24-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0e24-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b0e24-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0e24-184">a.</span><span class="sxs-lookup"><span data-stu-id="b0e24-184">a.</span></span> <span data-ttu-id="b0e24-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0e24-186">b.</span><span class="sxs-lookup"><span data-stu-id="b0e24-186">b.</span></span> <span data-ttu-id="b0e24-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0e24-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0e24-188">c.</span><span class="sxs-lookup"><span data-stu-id="b0e24-188">c.</span></span> <span data-ttu-id="b0e24-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0e24-190">d.</span><span class="sxs-lookup"><span data-stu-id="b0e24-190">d.</span></span> <span data-ttu-id="b0e24-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-191">Click **Create**.</span></span>
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a><span data-ttu-id="b0e24-192">Creazione di un utente test di Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="b0e24-192">Creating a Veritas Enterprise Vault.cloud SSO test user</span></span>

<span data-ttu-id="b0e24-193">In questa sezione viene creato un utente di nome Britta Simon in Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="b0e24-193">In this section, you create a user called Britta Simon in Enterprise Vault.cloud SSO.</span></span> <span data-ttu-id="b0e24-194">Lavorare con [team di supporto di Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html) per aggiungere gli utenti di hello nella piattaforma di Enterprise SSO Vault.cloud hello.</span><span class="sxs-lookup"><span data-stu-id="b0e24-194">Work with [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html) to add hello users in hello Enterprise Vault.cloud SSO platform.</span></span> <span data-ttu-id="b0e24-195">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b0e24-195">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b0e24-196">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0e24-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b0e24-197">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooVeritas Vault.cloud Enterprise SSO.</span><span class="sxs-lookup"><span data-stu-id="b0e24-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeritas Enterprise Vault.cloud SSO.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b0e24-199">**tooassign tooVeritas Britta Simon Vault.cloud di Enterprise SSO, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0e24-199">**tooassign Britta Simon tooVeritas Enterprise Vault.cloud SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0e24-200">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b0e24-202">Nell'elenco di applicazioni hello, selezionare **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-202">In hello applications list, select **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_app.png) 

3. <span data-ttu-id="b0e24-204">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b0e24-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-206">Click **Add** button.</span></span> <span data-ttu-id="b0e24-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b0e24-209">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b0e24-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0e24-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0e24-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b0e24-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0e24-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b0e24-212">Testing single sign-on</span></span>

<span data-ttu-id="b0e24-213">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b0e24-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0e24-214">Quando si fa clic su riquadro Veritas Enterprise Vault.cloud SSO hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="b0e24-214">When you click hello Veritas Enterprise Vault.cloud SSO tile in hello Access Panel, you should get automatically signed-on tooyour Veritas Enterprise Vault.cloud SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0e24-215">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b0e24-215">Additional resources</span></span>

* [<span data-ttu-id="b0e24-216">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0e24-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0e24-217">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0e24-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con HappyFox | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e HappyFox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="8d001-103">Esercitazione: Integrazione di Azure Active Directory con HappyFox</span><span class="sxs-lookup"><span data-stu-id="8d001-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="8d001-104">In questa esercitazione, è illustrato come toointegrate HappyFox con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d001-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d001-105">Integrazione HappyFox con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8d001-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d001-106">È possibile controllare in Azure AD che ha accesso tooHappyFox</span><span class="sxs-lookup"><span data-stu-id="8d001-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="8d001-107">È possibile abilitare l'utenti tooautomatically get connesso tooHappyFox (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d001-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d001-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8d001-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d001-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d001-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d001-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8d001-110">Prerequisites</span></span>

<span data-ttu-id="8d001-111">integrazione di Azure AD con HappyFox tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8d001-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="8d001-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d001-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d001-113">Sottoscrizione di HappyFox abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8d001-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d001-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8d001-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d001-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8d001-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d001-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8d001-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d001-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d001-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d001-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8d001-118">Scenario description</span></span>
<span data-ttu-id="8d001-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8d001-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d001-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8d001-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d001-121">Aggiunta di HappyFox dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8d001-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="8d001-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d001-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="8d001-123">Aggiunta di HappyFox dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8d001-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="8d001-124">integrazione hello tooconfigure di HappyFox in Azure AD, è necessario tooadd HappyFox dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8d001-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d001-125">**tooadd HappyFox dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8d001-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d001-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8d001-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d001-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8d001-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d001-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8d001-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8d001-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8d001-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8d001-133">Nella casella di ricerca hello, digitare **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="8d001-133">In hello search box, type **HappyFox**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="8d001-135">Nel riquadro dei risultati hello, selezionare **HappyFox**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8d001-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d001-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d001-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d001-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HappyFox in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d001-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d001-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in HappyFox è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d001-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="8d001-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in HappyFox deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8d001-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="8d001-141">In HappyFox, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8d001-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d001-142">tooconfigure e prova AD Azure single sign-on con HappyFox, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8d001-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d001-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8d001-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d001-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d001-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d001-145">**[Creazione di un utente test HappyFox](#creating-a-happyfox-test-user)**  -toohave un equivalente di Britta Simon in HappyFox che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8d001-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d001-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d001-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d001-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8d001-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d001-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d001-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d001-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione HappyFox.</span><span class="sxs-lookup"><span data-stu-id="8d001-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="8d001-150">**Azure AD tooconfigure single sign-on con HappyFox, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8d001-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d001-151">Nel portale di Azure su hello hello **HappyFox** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8d001-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8d001-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d001-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="8d001-155">In hello **HappyFox dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8d001-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="8d001-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d001-157">a.</span></span> <span data-ttu-id="8d001-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="8d001-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="8d001-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d001-159">b.</span></span> <span data-ttu-id="8d001-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="8d001-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d001-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8d001-161">These values are not real.</span></span> <span data-ttu-id="8d001-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="8d001-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8d001-163">Contatto [team di supporto HappyFox Client](https://support.happyfox.com/home) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="8d001-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="8d001-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8d001-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="8d001-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8d001-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d001-168">In hello **HappyFox configurazione** fare clic su **configurare HappyFox** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="8d001-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8d001-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="8d001-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="8d001-171">Accedere al portale personale di tooyour HappyFox e passare troppo**Gestisci**, fare clic su **integrazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="8d001-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="8d001-173">Nella scheda integrazioni hello, fare clic su **configura** in **integrazione SAML** tooopen hello Single Sign On Settings.</span><span class="sxs-lookup"><span data-stu-id="8d001-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="8d001-175">Nella sezione di configurazione SAML, incollare hello **SAML Single Sign-On Service URL** che è stata copiata dal portale di Azure in **SSO Target URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8d001-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="8d001-177">Aprire hello certificato scaricato dal portale di Azure nel blocco note e incollare il contenuto in **IdP firma** sezione.</span><span class="sxs-lookup"><span data-stu-id="8d001-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="8d001-179">Fare clic sul pulsante **Save Settings** (Salva impostazioni).</span><span class="sxs-lookup"><span data-stu-id="8d001-179">Click **Save Settings** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="8d001-181">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8d001-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d001-182">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8d001-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d001-183">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d001-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d001-184">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d001-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d001-185">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8d001-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8d001-187">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8d001-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d001-188">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8d001-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d001-190">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8d001-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d001-192">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8d001-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d001-194">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8d001-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d001-196">a.</span><span class="sxs-lookup"><span data-stu-id="8d001-196">a.</span></span> <span data-ttu-id="8d001-197">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d001-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d001-198">b.</span><span class="sxs-lookup"><span data-stu-id="8d001-198">b.</span></span> <span data-ttu-id="8d001-199">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d001-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d001-200">c.</span><span class="sxs-lookup"><span data-stu-id="8d001-200">c.</span></span> <span data-ttu-id="8d001-201">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8d001-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d001-202">d.</span><span class="sxs-lookup"><span data-stu-id="8d001-202">d.</span></span> <span data-ttu-id="8d001-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8d001-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="8d001-204">Creazione di un utente di test di HappyFox</span><span class="sxs-lookup"><span data-stu-id="8d001-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="8d001-205">L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8d001-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d001-206">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d001-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d001-207">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHappyFox.</span><span class="sxs-lookup"><span data-stu-id="8d001-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8d001-209">**tooassign Britta Simon tooHappyFox, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8d001-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d001-210">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8d001-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8d001-212">Nell'elenco di applicazioni hello, selezionare **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="8d001-212">In hello applications list, select **HappyFox**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="8d001-214">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8d001-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8d001-216">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8d001-216">Click **Add** button.</span></span> <span data-ttu-id="8d001-217">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8d001-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8d001-219">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8d001-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d001-220">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8d001-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d001-221">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8d001-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d001-222">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8d001-222">Testing single sign-on</span></span>

<span data-ttu-id="8d001-223">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8d001-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="8d001-224">Quando si fa clic su riquadro HappyFox hello in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione HappyFox.</span><span class="sxs-lookup"><span data-stu-id="8d001-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="8d001-225">Dovrebbe essere hello **'SAML'** pulsante nella pagina di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="8d001-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![Plug-in](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="8d001-227">Fare clic su hello **'SAML'** toolog pulsante in tooHappyFox con l'account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d001-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="8d001-228">Per ulteriori informazioni su hello Pannello di accesso, vedere [Introduzione al pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d001-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8d001-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8d001-229">Additional resources</span></span>

* [<span data-ttu-id="8d001-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d001-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d001-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d001-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png


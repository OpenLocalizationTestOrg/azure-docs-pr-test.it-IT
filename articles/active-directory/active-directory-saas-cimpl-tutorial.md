---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cimpl | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Cimpl.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58ee5481-ae40-4e4a-a3c9-86343851fc9a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 0b993f2b58aaeac24e657060fb31651edc847f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cimpl"></a><span data-ttu-id="ebc4d-103">Esercitazione: Integrazione di Azure Active Directory con Cimpl</span><span class="sxs-lookup"><span data-stu-id="ebc4d-103">Tutorial: Azure Active Directory integration with Cimpl</span></span>

<span data-ttu-id="ebc4d-104">In questa esercitazione, è illustrato come toointegrate Cimpl con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebc4d-104">In this tutorial, you learn how toointegrate Cimpl with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebc4d-105">Integrazione Cimpl con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ebc4d-105">Integrating Cimpl with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ebc4d-106">È possibile controllare in Azure AD che ha accesso tooCimpl</span><span class="sxs-lookup"><span data-stu-id="ebc4d-106">You can control in Azure AD who has access tooCimpl</span></span>
- <span data-ttu-id="ebc4d-107">È possibile abilitare l'utenti tooautomatically get connesso tooCimpl (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc4d-107">You can enable your users tooautomatically get signed-on tooCimpl (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ebc4d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ebc4d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ebc4d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ebc4d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebc4d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ebc4d-110">Prerequisites</span></span>

<span data-ttu-id="ebc4d-111">integrazione di Azure AD con Cimpl tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ebc4d-111">tooconfigure Azure AD integration with Cimpl, you need hello following items:</span></span>

- <span data-ttu-id="ebc4d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebc4d-113">Sottoscrizione di Cimpl abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ebc4d-113">A Cimpl single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebc4d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebc4d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ebc4d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebc4d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebc4d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebc4d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebc4d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ebc4d-118">Scenario description</span></span>
<span data-ttu-id="ebc4d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebc4d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ebc4d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebc4d-121">Aggiunta di Cimpl dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ebc4d-121">Adding Cimpl from hello gallery</span></span>
2. <span data-ttu-id="ebc4d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc4d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cimpl-from-hello-gallery"></a><span data-ttu-id="ebc4d-123">Aggiunta di Cimpl dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ebc4d-123">Adding Cimpl from hello gallery</span></span>
<span data-ttu-id="ebc4d-124">integrazione hello tooconfigure di Cimpl in Azure AD, è necessario tooadd Cimpl dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-124">tooconfigure hello integration of Cimpl into Azure AD, you need tooadd Cimpl from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ebc4d-125">**tooadd Cimpl dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ebc4d-125">**tooadd Cimpl from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc4d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ebc4d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ebc4d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ebc4d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ebc4d-133">Nella casella di ricerca hello, digitare **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-133">In hello search box, type **Cimpl**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_search.png)

5. <span data-ttu-id="ebc4d-135">Nel riquadro dei risultati hello, selezionare **Cimpl**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-135">In hello results panel, select **Cimpl**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ebc4d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc4d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ebc4d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cimpl mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ebc4d-138">In this section, you configure and test Azure AD single sign-on with Cimpl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ebc4d-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Cimpl è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cimpl is tooa user in Azure AD.</span></span> <span data-ttu-id="ebc4d-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Cimpl deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-140">In other words, a link relationship between an Azure AD user and hello related user in Cimpl needs toobe established.</span></span>

<span data-ttu-id="ebc4d-141">In Cimpl, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-141">In Cimpl, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ebc4d-142">tooconfigure e prova AD Azure single sign-on con Cimpl, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ebc4d-142">tooconfigure and test Azure AD single sign-on with Cimpl, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ebc4d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ebc4d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebc4d-145">**[Creazione di un utente test Cimpl](#creating-a-cimpl-test-user)**  -toohave un equivalente di Britta Simon in Cimpl che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-145">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - toohave a counterpart of Britta Simon in Cimpl that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebc4d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebc4d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ebc4d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc4d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ebc4d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cimpl application.</span></span>

<span data-ttu-id="ebc4d-150">**Azure AD tooconfigure single sign-on con Cimpl, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ebc4d-150">**tooconfigure Azure AD single sign-on with Cimpl, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc4d-151">Nel portale di Azure su hello hello **Cimpl** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-151">In hello Azure portal, on hello **Cimpl** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ebc4d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_samlbase.png)

3. <span data-ttu-id="ebc4d-155">In hello **Cimpl dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ebc4d-155">On hello **Cimpl Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_url.png)

    <span data-ttu-id="ebc4d-157">a.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-157">a.</span></span> <span data-ttu-id="ebc4d-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="ebc4d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    <span data-ttu-id="ebc4d-159">b.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-159">b.</span></span> <span data-ttu-id="ebc4d-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="ebc4d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ebc4d-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ebc4d-161">These values are not real.</span></span> <span data-ttu-id="ebc4d-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ebc4d-163">Contattare il team di Cimpl **+1 866-982-8250** tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-163">Contact Cimpl team at **+1 866-982-8250** tooget these values.</span></span> 
 
4. <span data-ttu-id="ebc4d-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_certificate.png) 

5. <span data-ttu-id="ebc4d-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ebc4d-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cimpl-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ebc4d-168">In hello **Cimpl configurazione** fare clic su **configurare Cimpl** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-168">On hello **Cimpl Configuration** section, click **Configure Cimpl** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ebc4d-169">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ebc4d-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_configure.png) 

7. <span data-ttu-id="ebc4d-171">tooconfigure single sign-on sul **Cimpl** lato, è necessario hello toosend scaricato **certificato (Base64)**, **ID entità SAML e SAML Single Sign-On Service URL** tooCimpl supportare **+1 866-982-8250**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-171">tooconfigure single sign-on on **Cimpl** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Entity ID, and SAML Single Sign-On Service URL** tooCimpl support at **+1 866-982-8250**.</span></span>


> [!TIP]
> <span data-ttu-id="ebc4d-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ebc4d-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ebc4d-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ebc4d-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ebc4d-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ebc4d-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc4d-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="ebc4d-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ebc4d-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ebc4d-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc4d-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ebc4d-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ebc4d-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ebc4d-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ebc4d-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ebc4d-187">a.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-187">a.</span></span> <span data-ttu-id="ebc4d-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebc4d-189">b.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-189">b.</span></span> <span data-ttu-id="ebc4d-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ebc4d-191">c.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-191">c.</span></span> <span data-ttu-id="ebc4d-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ebc4d-193">d.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-193">d.</span></span> <span data-ttu-id="ebc4d-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-194">Click **Create**.</span></span>
 
### <a name="creating-a-cimpl-test-user"></a><span data-ttu-id="ebc4d-195">Creazione di un utente test Cimpl</span><span class="sxs-lookup"><span data-stu-id="ebc4d-195">Creating a Cimpl test user</span></span>

<span data-ttu-id="ebc4d-196">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Cimpl toocreate.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-196">hello objective of this section is toocreate a user called Britta Simon in Cimpl.</span></span> <span data-ttu-id="ebc4d-197">Rivolgersi al supporto Cimpl **+1 866-982-8250** tooadd utenti hello hello Cimpl account.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-197">Work with Cimpl support at **+1 866-982-8250** tooadd hello users in hello Cimpl account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ebc4d-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebc4d-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ebc4d-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCimpl.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCimpl.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ebc4d-201">**tooassign Britta Simon tooCimpl, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ebc4d-201">**tooassign Britta Simon tooCimpl, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebc4d-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ebc4d-204">Nell'elenco di applicazioni hello, selezionare **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-204">In hello applications list, select **Cimpl**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_app.png) 

3. <span data-ttu-id="ebc4d-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ebc4d-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-208">Click **Add** button.</span></span> <span data-ttu-id="ebc4d-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ebc4d-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ebc4d-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebc4d-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ebc4d-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ebc4d-214">Testing single sign-on</span></span>

<span data-ttu-id="ebc4d-215">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  <span data-ttu-id="ebc4d-216">Quando si fa clic su riquadro Cimpl hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Cimpl applicazione.</span><span class="sxs-lookup"><span data-stu-id="ebc4d-216">When you click hello Cimpl tile in hello Access Panel, you should get automatically signed-on tooyour Cimpl application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ebc4d-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ebc4d-217">Additional resources</span></span>

* [<span data-ttu-id="ebc4d-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebc4d-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebc4d-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebc4d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_203.png


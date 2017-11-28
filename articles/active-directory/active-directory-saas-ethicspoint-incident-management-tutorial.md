---
title: 'Esercitazione: Integrazione di Azure Active Directory con EthicsPoint Incident Management (EPIM) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e gestione di eventi imprevisti EthicsPoint (EPIM).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 73ef5fab815cddb3728f4b23173f99e62aec5bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="d6b11-103">Esercitazione: Integrazione di Azure Active Directory con EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="d6b11-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="d6b11-104">In questa esercitazione, è illustrato come toointegrate EthicsPoint Incident Management (EPIM) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6b11-104">In this tutorial, you learn how toointegrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6b11-105">Integrazione di gestione eventi imprevisti EthicsPoint (EPIM) con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d6b11-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d6b11-106">È possibile controllare in Azure AD che ha accesso tooEthicsPoint gestione evento imprevisto (EPIM)</span><span class="sxs-lookup"><span data-stu-id="d6b11-106">You can control in Azure AD who has access tooEthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="d6b11-107">È possibile abilitare l'utenti tooautomatically get connesso tooEthicsPoint gestione evento imprevisto (EPIM) (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b11-107">You can enable your users tooautomatically get signed-on tooEthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6b11-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d6b11-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d6b11-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6b11-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6b11-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d6b11-110">Prerequisites</span></span>

<span data-ttu-id="d6b11-111">integrazione di Azure AD con gestione eventi imprevisti EthicsPoint (EPIM) tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d6b11-111">tooconfigure Azure AD integration with EthicsPoint Incident Management (EPIM), you need hello following items:</span></span>

- <span data-ttu-id="d6b11-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6b11-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6b11-113">Sottoscrizione di EthicsPoint Incident Management (EPIM) abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d6b11-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6b11-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d6b11-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6b11-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d6b11-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6b11-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d6b11-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6b11-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6b11-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6b11-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d6b11-118">Scenario description</span></span>
<span data-ttu-id="d6b11-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d6b11-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6b11-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d6b11-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6b11-121">Aggiunta di gestione eventi imprevisti EthicsPoint (EPIM) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d6b11-121">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
2. <span data-ttu-id="d6b11-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b11-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-hello-gallery"></a><span data-ttu-id="d6b11-123">Aggiunta di gestione eventi imprevisti EthicsPoint (EPIM) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d6b11-123">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
<span data-ttu-id="d6b11-124">tooconfigure hello integrazione di gestione eventi imprevisti EthicsPoint (EPIM) AD Azure, è necessario tooadd EthicsPoint Incident Management (EPIM) dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d6b11-124">tooconfigure hello integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need tooadd EthicsPoint Incident Management (EPIM) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d6b11-125">**tooadd EthicsPoint Incident Management (EPIM) dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d6b11-125">**tooadd EthicsPoint Incident Management (EPIM) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6b11-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d6b11-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6b11-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d6b11-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d6b11-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d6b11-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d6b11-133">Nella casella di ricerca hello, digitare **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-133">In hello search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="d6b11-135">Nel riquadro dei risultati hello, selezionare **EthicsPoint Incident Management (EPIM)**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d6b11-135">In hello results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6b11-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b11-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6b11-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con EthicsPoint Incident Management (EPIM) usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d6b11-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6b11-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in gestione eventi imprevisti EthicsPoint (EPIM) è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6b11-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EthicsPoint Incident Management (EPIM) is tooa user in Azure AD.</span></span> <span data-ttu-id="d6b11-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello in gestione eventi imprevisti EthicsPoint (EPIM) richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d6b11-140">In other words, a link relationship between an Azure AD user and hello related user in EthicsPoint Incident Management (EPIM) needs toobe established.</span></span>

<span data-ttu-id="d6b11-141">In gestione eventi imprevisti EthicsPoint (EPIM), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="d6b11-141">In EthicsPoint Incident Management (EPIM), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d6b11-142">tooconfigure e test di Azure AD single sign-on con gestione eventi imprevisti EthicsPoint (EPIM), è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d6b11-142">tooconfigure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d6b11-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d6b11-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d6b11-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6b11-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6b11-145">**[Creazione di un utente test EthicsPoint Incident Management (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)**  -toohave un equivalente di Britta Simon EthicsPoint Incident Management (EPIM) che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d6b11-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - toohave a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6b11-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d6b11-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6b11-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d6b11-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6b11-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b11-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6b11-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione di gestione eventi imprevisti EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="d6b11-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="d6b11-150">**tooconfigure AD Azure single sign-on con gestione eventi imprevisti EthicsPoint (EPIM), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d6b11-150">**tooconfigure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="d6b11-151">Nel portale di Azure su hello hello **EthicsPoint Incident Management (EPIM)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-151">In hello Azure portal, on hello **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d6b11-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d6b11-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="d6b11-155">In hello **URL e il dominio di gestione eventi imprevisti EthicsPoint (EPIM)** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d6b11-155">On hello **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="d6b11-157">a.</span><span class="sxs-lookup"><span data-stu-id="d6b11-157">a.</span></span> <span data-ttu-id="d6b11-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="d6b11-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="d6b11-159">b.</span><span class="sxs-lookup"><span data-stu-id="d6b11-159">b.</span></span> <span data-ttu-id="d6b11-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="d6b11-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="d6b11-161">c.</span><span class="sxs-lookup"><span data-stu-id="d6b11-161">c.</span></span> <span data-ttu-id="d6b11-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="d6b11-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d6b11-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d6b11-163">These values are not real.</span></span> <span data-ttu-id="d6b11-164">Aggiornare questi valori con l'URL di risposta effettivo hello e identificatore URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d6b11-164">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="d6b11-165">Contatto [team di supporto Client di gestione eventi imprevisti EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="d6b11-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="d6b11-166">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d6b11-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="d6b11-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d6b11-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="d6b11-170">tooconfigure single sign-on sul **EthicsPoint Incident Management (EPIM)** lato, è necessario hello toosend scaricato **Metadata XML** troppo[supporto gestione eventi imprevisti EthicsPoint (EPIM) Team](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="d6b11-170">tooconfigure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need toosend hello downloaded **Metadata XML** too[EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="d6b11-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d6b11-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d6b11-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d6b11-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d6b11-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6b11-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6b11-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b11-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6b11-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d6b11-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d6b11-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d6b11-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6b11-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d6b11-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6b11-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6b11-182">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d6b11-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6b11-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d6b11-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6b11-186">a.</span><span class="sxs-lookup"><span data-stu-id="d6b11-186">a.</span></span> <span data-ttu-id="d6b11-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6b11-188">b.</span><span class="sxs-lookup"><span data-stu-id="d6b11-188">b.</span></span> <span data-ttu-id="d6b11-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6b11-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6b11-190">c.</span><span class="sxs-lookup"><span data-stu-id="d6b11-190">c.</span></span> <span data-ttu-id="d6b11-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d6b11-192">d.</span><span class="sxs-lookup"><span data-stu-id="d6b11-192">d.</span></span> <span data-ttu-id="d6b11-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="d6b11-194">Creazione di un utente test di EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="d6b11-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="d6b11-195">In questa sezione viene creato un utente chiamato Britta Simon in EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="d6b11-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="d6b11-196">Rivolgersi [team di supporto gestione eventi imprevisti EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) utenti hello tooadd nella piattaforma di gestione eventi imprevisti EthicsPoint (EPIM) hello.</span><span class="sxs-lookup"><span data-stu-id="d6b11-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) tooadd hello users in hello EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d6b11-197">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b11-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d6b11-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEthicsPoint gestione evento imprevisto (EPIM).</span><span class="sxs-lookup"><span data-stu-id="d6b11-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEthicsPoint Incident Management (EPIM).</span></span>

![Assegna utente][200] 

<span data-ttu-id="d6b11-200">**tooassign Britta Simon tooEthicsPoint gestione evento imprevisto (EPIM), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d6b11-200">**tooassign Britta Simon tooEthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="d6b11-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d6b11-203">Nell'elenco di applicazioni hello, selezionare **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-203">In hello applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="d6b11-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d6b11-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-207">Click **Add** button.</span></span> <span data-ttu-id="d6b11-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d6b11-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d6b11-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d6b11-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6b11-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d6b11-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6b11-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d6b11-213">Testing single sign-on</span></span>

<span data-ttu-id="d6b11-214">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d6b11-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="d6b11-215">Quando si fa clic su riquadro di gestione eventi imprevisti EthicsPoint (EPIM) hello in hello Pannello di accesso, è necessario ottenere l'applicazione di gestione eventi imprevisti EthicsPoint (EPIM) tooyour firmato in automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d6b11-215">When you click hello EthicsPoint Incident Management (EPIM) tile in hello Access Panel, you should get automatically signed-on tooyour EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6b11-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d6b11-216">Additional resources</span></span>

* [<span data-ttu-id="d6b11-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6b11-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6b11-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6b11-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png


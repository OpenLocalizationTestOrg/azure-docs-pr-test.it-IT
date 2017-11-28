---
title: 'Esercitazione: Integrazione di Azure Active Directory con People | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e gli utenti.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: d540c31867c92c4dc09db9c0833f8a8a7c02b371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="0e3d1-103">Esercitazione: Integrazione di Azure Active Directory con People</span><span class="sxs-lookup"><span data-stu-id="0e3d1-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="0e3d1-104">In questa esercitazione, è illustrato come toointegrate persone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e3d1-104">In this tutorial, you learn how toointegrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e3d1-105">Integrazione di persone con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0e3d1-105">Integrating People with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e3d1-106">È possibile controllare in Azure AD che ha accesso tooPeople</span><span class="sxs-lookup"><span data-stu-id="0e3d1-106">You can control in Azure AD who has access tooPeople</span></span>
- <span data-ttu-id="0e3d1-107">È possibile abilitare l'utenti tooautomatically get connesso tooPeople (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3d1-107">You can enable your users tooautomatically get signed-on tooPeople (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e3d1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0e3d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e3d1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e3d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e3d1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0e3d1-110">Prerequisites</span></span>

<span data-ttu-id="0e3d1-111">tooconfigure integrazione di Azure AD con altri utenti, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0e3d1-111">tooconfigure Azure AD integration with People, you need hello following items:</span></span>

- <span data-ttu-id="0e3d1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e3d1-113">Sottoscrizione di People abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0e3d1-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e3d1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e3d1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0e3d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e3d1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e3d1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e3d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e3d1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0e3d1-118">Scenario description</span></span>
<span data-ttu-id="0e3d1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e3d1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0e3d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e3d1-121">Aggiunta di utenti da raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0e3d1-121">Adding People from hello gallery</span></span>
2. <span data-ttu-id="0e3d1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-hello-gallery"></a><span data-ttu-id="0e3d1-123">Aggiunta di utenti da raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0e3d1-123">Adding People from hello gallery</span></span>
<span data-ttu-id="0e3d1-124">integrazione hello tooconfigure di utenti in Azure AD, è necessario tooadd persone dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-124">tooconfigure hello integration of People into Azure AD, you need tooadd People from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e3d1-125">**tooadd persone dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0e3d1-125">**tooadd People from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3d1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e3d1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e3d1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="0e3d1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="0e3d1-133">Nella casella di ricerca hello, digitare **persone**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-133">In hello search box, type **People**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="0e3d1-135">Nel riquadro dei risultati hello, selezionare **persone**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-135">In hello results panel, select **People**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e3d1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e3d1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con People in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e3d1-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e3d1-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in persone è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in People is tooa user in Azure AD.</span></span> <span data-ttu-id="0e3d1-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in persone deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-140">In other words, a link relationship between an Azure AD user and hello related user in People needs toobe established.</span></span>

<span data-ttu-id="0e3d1-141">In utenti, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-141">In People, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e3d1-142">tooconfigure e test Azure single sign-on AD con altri utenti, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0e3d1-142">tooconfigure and test Azure AD single sign-on with People, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e3d1-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e3d1-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e3d1-145">**[Creazione di un utente test persone](#creating-a-people-test-user)**  -toohave un equivalente di Britta Simon in persone con cui sono collegato toohello AD Azure rappresentazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-145">**[Creating a People test user](#creating-a-people-test-user)** - toohave a counterpart of Britta Simon in People that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e3d1-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e3d1-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e3d1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e3d1-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione persone.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="0e3d1-150">**Azure AD tooconfigure single sign-on con persone, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0e3d1-150">**tooconfigure Azure AD single sign-on with People, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3d1-151">Nel portale di Azure su hello hello **persone** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-151">In hello Azure portal, on hello **People** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0e3d1-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="0e3d1-155">In hello **dominio persone e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0e3d1-155">On hello **People Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="0e3d1-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-157">a.</span></span> <span data-ttu-id="0e3d1-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="0e3d1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="0e3d1-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-159">b.</span></span> <span data-ttu-id="0e3d1-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="0e3d1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="0e3d1-161">c.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-161">c.</span></span> <span data-ttu-id="0e3d1-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="0e3d1-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e3d1-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0e3d1-163">These values are not real.</span></span> <span data-ttu-id="0e3d1-164">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0e3d1-165">Contatto [team di supporto Client di persone](mailto:customerservices@peoplehr.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) tooget these values.</span></span>

5. <span data-ttu-id="0e3d1-166">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="0e3d1-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0e3d1-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0e3d1-170">tooget SSO configurato per l'applicazione, è necessario tenant persone tooyour toosign-on come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-170">tooget SSO configured for your application, you need toosign-on tooyour People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="0e3d1-171">Scegliere dal menu hello sul lato sinistro hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-171">In hello menu on hello left side, click **Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="0e3d1-173">Fare clic su **Azienda**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-173">Click **Company**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="0e3d1-175">In hello **file di metadati di caricamento 'Single Sign On' SAML**, fare clic su **Sfoglia** hello tooupload scaricato i file di metadati.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-175">On hello **Upload 'Single Sign On' SAML meta-data file**, click **Browse** tooupload hello downloaded metadata file.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="0e3d1-177">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0e3d1-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e3d1-178">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e3d1-179">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e3d1-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e3d1-180">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3d1-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e3d1-181">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="0e3d1-183">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0e3d1-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3d1-184">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e3d1-186">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e3d1-188">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e3d1-190">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0e3d1-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e3d1-192">a.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-192">a.</span></span> <span data-ttu-id="0e3d1-193">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e3d1-194">b.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-194">b.</span></span> <span data-ttu-id="0e3d1-195">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e3d1-196">c.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-196">c.</span></span> <span data-ttu-id="0e3d1-197">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e3d1-198">d.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-198">d.</span></span> <span data-ttu-id="0e3d1-199">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="0e3d1-200">Creazione di un utente test di People</span><span class="sxs-lookup"><span data-stu-id="0e3d1-200">Creating a People test user</span></span>

<span data-ttu-id="0e3d1-201">In questa sezione viene creato un utente chiamato Britta Simon in People.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="0e3d1-202">Lavorare con [team di supporto Client di persone](mailto:customerservices@peoplehr.com) per aggiungere gli utenti di hello nella piattaforma di persone hello.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add hello users in hello People platform.</span></span> <span data-ttu-id="0e3d1-203">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e3d1-204">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e3d1-204">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e3d1-205">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPeople.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-205">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeople.</span></span>

![Assegna utente][200] 

<span data-ttu-id="0e3d1-207">**tooassign Britta Simon tooPeople, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0e3d1-207">**tooassign Britta Simon tooPeople, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e3d1-208">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-208">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0e3d1-210">Nell'elenco di applicazioni hello, selezionare **persone**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-210">In hello applications list, select **People**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="0e3d1-212">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-212">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="0e3d1-214">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-214">Click **Add** button.</span></span> <span data-ttu-id="0e3d1-215">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="0e3d1-217">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-217">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e3d1-218">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e3d1-219">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e3d1-220">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0e3d1-220">Testing single sign-on</span></span>

<span data-ttu-id="0e3d1-221">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-221">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e3d1-222">Quando si fa clic hello persone riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione persone.</span><span class="sxs-lookup"><span data-stu-id="0e3d1-222">When you click hello People tile in hello Access Panel, you should get automatically signed-on tooyour People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e3d1-223">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0e3d1-223">Additional resources</span></span>

* [<span data-ttu-id="0e3d1-224">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e3d1-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e3d1-225">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e3d1-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png


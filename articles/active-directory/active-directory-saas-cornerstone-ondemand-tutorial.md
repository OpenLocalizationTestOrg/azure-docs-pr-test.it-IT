---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cornerstone OnDemand | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Cornerstone OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 85fd6eb4e93010d8f7477df236403e205e9f2d83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="4f9e6-103">Esercitazione: Integrazione di Azure Active Directory con Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="4f9e6-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="4f9e6-104">In questa esercitazione, è illustrato come toointegrate Cornerstone OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f9e6-104">In this tutorial, you learn how toointegrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f9e6-105">Integrazione di Cornerstone OnDemand con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4f9e6-105">Integrating Cornerstone OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4f9e6-106">È possibile controllare in Azure AD che ha accesso tooCornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="4f9e6-106">You can control in Azure AD who has access tooCornerstone OnDemand</span></span>
- <span data-ttu-id="4f9e6-107">È possibile abilitare l'utenti tooautomatically get connesso tooCornerstone OnDemand (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9e6-107">You can enable your users tooautomatically get signed-on tooCornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f9e6-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4f9e6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4f9e6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f9e6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f9e6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4f9e6-110">Prerequisites</span></span>

<span data-ttu-id="4f9e6-111">integrazione di Azure AD con Cornerstone OnDemand tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4f9e6-111">tooconfigure Azure AD integration with Cornerstone OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="4f9e6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f9e6-113">Sottoscrizione di Cornerstone OnDemand abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4f9e6-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f9e6-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f9e6-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4f9e6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f9e6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f9e6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f9e6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f9e6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4f9e6-118">Scenario description</span></span>
<span data-ttu-id="4f9e6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f9e6-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4f9e6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f9e6-121">Aggiunta di Cornerstone OnDemand dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4f9e6-121">Adding Cornerstone OnDemand from hello gallery</span></span>
2. <span data-ttu-id="4f9e6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9e6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-hello-gallery"></a><span data-ttu-id="4f9e6-123">Aggiunta di Cornerstone OnDemand dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4f9e6-123">Adding Cornerstone OnDemand from hello gallery</span></span>
<span data-ttu-id="4f9e6-124">integrazione hello tooconfigure di Cornerstone OnDemand in Azure AD, è necessario tooadd Cornerstone OnDemand dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-124">tooconfigure hello integration of Cornerstone OnDemand into Azure AD, you need tooadd Cornerstone OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4f9e6-125">**tooadd Cornerstone OnDemand dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f9e6-125">**tooadd Cornerstone OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9e6-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f9e6-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4f9e6-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4f9e6-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4f9e6-133">Nella casella di ricerca hello, digitare **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-133">In hello search box, type **Cornerstone OnDemand**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="4f9e6-135">Nel riquadro dei risultati hello, selezionare **Cornerstone OnDemand**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-135">In hello results panel, select **Cornerstone OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f9e6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9e6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f9e6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cornerstone OnDemand mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4f9e6-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4f9e6-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Cornerstone OnDemand è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cornerstone OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="4f9e6-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Cornerstone OnDemand deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-140">In other words, a link relationship between an Azure AD user and hello related user in Cornerstone OnDemand needs toobe established.</span></span>

<span data-ttu-id="4f9e6-141">In Cornerstone OnDemand, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-141">In Cornerstone OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4f9e6-142">tooconfigure e test Azure single sign-on AD con Cornerstone OnDemand, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4f9e6-142">tooconfigure and test Azure AD single sign-on with Cornerstone OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4f9e6-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4f9e6-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f9e6-145">**[Creazione di un utente test Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)**  -toohave un equivalente di Britta Simon in Cornerstone OnDemand che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - toohave a counterpart of Britta Simon in Cornerstone OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f9e6-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f9e6-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f9e6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9e6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f9e6-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="4f9e6-150">**Azure AD tooconfigure single sign-on con Cornerstone OnDemand, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f9e6-150">**tooconfigure Azure AD single sign-on with Cornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9e6-151">Nel portale di Azure su hello hello **Cornerstone OnDemand** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-151">In hello Azure portal, on hello **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4f9e6-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="4f9e6-155">In hello **Cornerstone OnDemand dominio e gli URL** seguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="4f9e6-155">On hello **Cornerstone OnDemand Domain and URLs** section, perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="4f9e6-157">a.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-157">a.</span></span> <span data-ttu-id="4f9e6-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="4f9e6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="4f9e6-159">b.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-159">b.</span></span> <span data-ttu-id="4f9e6-160">In **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="4f9e6-160">In **Identifier** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f9e6-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4f9e6-161">These values are not real.</span></span> <span data-ttu-id="4f9e6-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4f9e6-163">Contatto [team di supporto di Cornerstone OnDemand Client](mailTo:moreinfo@csod.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4f9e6-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="4f9e6-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4f9e6-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4f9e6-168">In hello **Cornerstone OnDemand configurazione** fare clic su **configurare Cornerstone OnDemand** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-168">On hello **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4f9e6-169">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4f9e6-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="4f9e6-171">tooconfigure single sign-on sul **Cornerstone OnDemand** lato, è necessario hello toosend scaricato **certificato**, **Sign-Out URL** e **SAML Single Sign-On Service URL** troppo[team di supporto di Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="4f9e6-171">tooconfigure single sign-on on **Cornerstone OnDemand** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  too[Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="4f9e6-172">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4f9e6-173">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4f9e6-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4f9e6-174">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4f9e6-175">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f9e6-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f9e6-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9e6-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f9e6-177">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4f9e6-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f9e6-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9e6-180">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f9e6-182">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f9e6-184">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f9e6-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4f9e6-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f9e6-188">a.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-188">a.</span></span> <span data-ttu-id="4f9e6-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f9e6-190">b.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-190">b.</span></span> <span data-ttu-id="4f9e6-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f9e6-192">c.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-192">c.</span></span> <span data-ttu-id="4f9e6-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4f9e6-194">d.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-194">d.</span></span> <span data-ttu-id="4f9e6-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="4f9e6-196">Creazione di un utente test di Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="4f9e6-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="4f9e6-197">In ordine tooenable Azure AD utenti toolog in Cornerstone OnDemand, è necessario eseguirne il provisioning in Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-197">In order tooenable Azure AD users toolog into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="4f9e6-198">Nel caso di hello di Cornerstone OnDemand, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-198">In hello case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="4f9e6-199">utente tooconfigure informazioni di provisioning, trasmissione hello (ad esempio: nome, posta elettronica) sull'utente hello Azure AD desiderato tooprovision toohello [team di supporto di Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="4f9e6-199">tooconfigure user provisioning, send hello information (e.g.: Name, Email) about hello Azure AD user you want tooprovision toohello [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="4f9e6-200">È possibile usare qualsiasi altro Cornerstone OnDemand account strumento di creazione utente o qualsiasi API fornita da Cornerstone OnDemand tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4f9e6-201">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f9e6-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4f9e6-202">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCornerstone OnDemand.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4f9e6-204">**tooassign Britta Simon tooCornerstone OnDemand, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f9e6-204">**tooassign Britta Simon tooCornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f9e6-205">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4f9e6-207">Nell'elenco di applicazioni hello, selezionare **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-207">In hello applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="4f9e6-209">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4f9e6-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-211">Click **Add** button.</span></span> <span data-ttu-id="4f9e6-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4f9e6-214">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4f9e6-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f9e6-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f9e6-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4f9e6-217">Testing single sign-on</span></span>

<span data-ttu-id="4f9e6-218">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4f9e6-219">Quando si fa clic su riquadro Cornerstone OnDemand hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Cornerstone OnDemand applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f9e6-219">When you click hello Cornerstone OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour Cornerstone OnDemand application.</span></span>
<span data-ttu-id="4f9e6-220">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f9e6-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4f9e6-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4f9e6-221">Additional resources</span></span>

* [<span data-ttu-id="4f9e6-222">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f9e6-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f9e6-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f9e6-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Nomadesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Nomadesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d261b776-b48e-45f0-9722-0297adefabb8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 9aa55ba6106ea24f556217cfe84d21d7415d9c78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadesk"></a><span data-ttu-id="60b1c-103">Esercitazione: Integrazione di Azure Active Directory con Nomadesk</span><span class="sxs-lookup"><span data-stu-id="60b1c-103">Tutorial: Azure Active Directory integration with Nomadesk</span></span>

<span data-ttu-id="60b1c-104">In questa esercitazione, è illustrato come toointegrate Nomadesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60b1c-104">In this tutorial, you learn how toointegrate Nomadesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60b1c-105">Integrazione Nomadesk con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="60b1c-105">Integrating Nomadesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="60b1c-106">È possibile controllare in Azure AD che ha accesso tooNomadesk</span><span class="sxs-lookup"><span data-stu-id="60b1c-106">You can control in Azure AD who has access tooNomadesk</span></span>
- <span data-ttu-id="60b1c-107">È possibile abilitare l'utenti tooautomatically get connesso tooNomadesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b1c-107">You can enable your users tooautomatically get signed-on tooNomadesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60b1c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="60b1c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="60b1c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60b1c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60b1c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="60b1c-110">Prerequisites</span></span>

<span data-ttu-id="60b1c-111">integrazione di Azure AD con Nomadesk tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="60b1c-111">tooconfigure Azure AD integration with Nomadesk, you need hello following items:</span></span>

- <span data-ttu-id="60b1c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60b1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60b1c-113">Sottoscrizione di Nomadesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="60b1c-113">A Nomadesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60b1c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="60b1c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60b1c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="60b1c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60b1c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="60b1c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60b1c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60b1c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60b1c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="60b1c-118">Scenario description</span></span>
<span data-ttu-id="60b1c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="60b1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60b1c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="60b1c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60b1c-121">Aggiunta di Nomadesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="60b1c-121">Adding Nomadesk from hello gallery</span></span>
2. <span data-ttu-id="60b1c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b1c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nomadesk-from-hello-gallery"></a><span data-ttu-id="60b1c-123">Aggiunta di Nomadesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="60b1c-123">Adding Nomadesk from hello gallery</span></span>
<span data-ttu-id="60b1c-124">integrazione hello tooconfigure di Nomadesk in Azure AD, è necessario tooadd Nomadesk dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="60b1c-124">tooconfigure hello integration of Nomadesk into Azure AD, you need tooadd Nomadesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="60b1c-125">**tooadd Nomadesk dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="60b1c-125">**tooadd Nomadesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="60b1c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="60b1c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60b1c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="60b1c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="60b1c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="60b1c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="60b1c-133">Nella casella di ricerca hello, digitare **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-133">In hello search box, type **Nomadesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_search.png)

5. <span data-ttu-id="60b1c-135">Nel riquadro dei risultati hello, selezionare **Nomadesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="60b1c-135">In hello results panel, select **Nomadesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60b1c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b1c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60b1c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Nomadesk in base a un utente di prova di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="60b1c-138">In this section, you configure and test Azure AD single sign-on with Nomadesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60b1c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Nomadesk è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60b1c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nomadesk is tooa user in Azure AD.</span></span> <span data-ttu-id="60b1c-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Nomadesk deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="60b1c-140">In other words, a link relationship between an Azure AD user and hello related user in Nomadesk needs toobe established.</span></span>

<span data-ttu-id="60b1c-141">In Nomadesk, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="60b1c-141">In Nomadesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="60b1c-142">tooconfigure e prova AD Azure single sign-on con Nomadesk, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="60b1c-142">tooconfigure and test Azure AD single sign-on with Nomadesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="60b1c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="60b1c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="60b1c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60b1c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60b1c-145">**[Creazione di un utente test Nomadesk](#creating-a-nomadesk-test-user)**  -toohave un equivalente di Britta Simon in Nomadesk che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="60b1c-145">**[Creating a Nomadesk test user](#creating-a-nomadesk-test-user)** - toohave a counterpart of Britta Simon in Nomadesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="60b1c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60b1c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60b1c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="60b1c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60b1c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b1c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60b1c-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Nomadesk.</span><span class="sxs-lookup"><span data-stu-id="60b1c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nomadesk application.</span></span>

<span data-ttu-id="60b1c-150">**Azure AD tooconfigure single sign-on con Nomadesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="60b1c-150">**tooconfigure Azure AD single sign-on with Nomadesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="60b1c-151">Nel portale di Azure su hello hello **Nomadesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-151">In hello Azure portal, on hello **Nomadesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="60b1c-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60b1c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_samlbase.png)

3. <span data-ttu-id="60b1c-155">In hello **Nomadesk dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="60b1c-155">On hello **Nomadesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_url.png)

    <span data-ttu-id="60b1c-157">a.</span><span class="sxs-lookup"><span data-stu-id="60b1c-157">a.</span></span> <span data-ttu-id="60b1c-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://mynomadesk.com/logon/saml/<TENANTID>`</span><span class="sxs-lookup"><span data-stu-id="60b1c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mynomadesk.com/logon/saml/<TENANTID>`</span></span>

    <span data-ttu-id="60b1c-159">b.</span><span class="sxs-lookup"><span data-stu-id="60b1c-159">b.</span></span> <span data-ttu-id="60b1c-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://secure.nomadesk.com/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="60b1c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://secure.nomadesk.com/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60b1c-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="60b1c-161">These values are not real.</span></span> <span data-ttu-id="60b1c-162">Aggiornare questi valori con URL hello effettivo Sign-on e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="60b1c-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="60b1c-163">Contatto [team di supporto Nomadesk Client](mailto:support@nomadesk.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="60b1c-163">Contact [Nomadesk Client support team](mailto:support@nomadesk.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="60b1c-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="60b1c-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_certificate.png) 

5. <span data-ttu-id="60b1c-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="60b1c-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nomadesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60b1c-168">In hello **Nomadesk configurazione** fare clic su **configurare Nomadesk** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="60b1c-168">On hello **Nomadesk Configuration** section, click **Configure Nomadesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="60b1c-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="60b1c-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_configure.png) 

7. <span data-ttu-id="60b1c-171">tooconfigure single sign-on sul **Nomadesk** lato, è necessario hello toosend scaricato **certificato**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="60b1c-171">tooconfigure single sign-on on **Nomadesk** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Nomadesk support team](mailto:support@nomadesk.com).</span></span> <span data-ttu-id="60b1c-172">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="60b1c-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="60b1c-173">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="60b1c-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="60b1c-174">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="60b1c-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="60b1c-175">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60b1c-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60b1c-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b1c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="60b1c-177">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="60b1c-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="60b1c-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="60b1c-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="60b1c-180">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="60b1c-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60b1c-182">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60b1c-184">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="60b1c-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60b1c-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="60b1c-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-nomadesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60b1c-188">a.</span><span class="sxs-lookup"><span data-stu-id="60b1c-188">a.</span></span> <span data-ttu-id="60b1c-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60b1c-190">b.</span><span class="sxs-lookup"><span data-stu-id="60b1c-190">b.</span></span> <span data-ttu-id="60b1c-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="60b1c-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60b1c-192">c.</span><span class="sxs-lookup"><span data-stu-id="60b1c-192">c.</span></span> <span data-ttu-id="60b1c-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="60b1c-194">d.</span><span class="sxs-lookup"><span data-stu-id="60b1c-194">d.</span></span> <span data-ttu-id="60b1c-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-195">Click **Create**.</span></span>
 
### <a name="creating-a-nomadesk-test-user"></a><span data-ttu-id="60b1c-196">Creazione di un utente di test Nomadesk</span><span class="sxs-lookup"><span data-stu-id="60b1c-196">Creating a Nomadesk test user</span></span>

<span data-ttu-id="60b1c-197">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Nomadesk toocreate.</span><span class="sxs-lookup"><span data-stu-id="60b1c-197">hello objective of this section is toocreate a user called Britta Simon in Nomadesk.</span></span> <span data-ttu-id="60b1c-198">Nomadesk supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="60b1c-198">Nomadesk supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="60b1c-199">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="60b1c-199">There is no action item for you in this section.</span></span> <span data-ttu-id="60b1c-200">Se non esiste ancora, durante un tooaccess tentativo Nomadesk viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="60b1c-200">A new user is created during an attempt tooaccess Nomadesk if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="60b1c-201">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Nomadesk](mailto:support@nomadesk.com).</span><span class="sxs-lookup"><span data-stu-id="60b1c-201">If you need toocreate a user manually, you need toocontact hello [Nomadesk support team](mailto:support@nomadesk.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="60b1c-202">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="60b1c-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="60b1c-203">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNomadesk.</span><span class="sxs-lookup"><span data-stu-id="60b1c-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNomadesk.</span></span>

![Assegna utente][200] 

<span data-ttu-id="60b1c-205">**tooassign Britta Simon tooNomadesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="60b1c-205">**tooassign Britta Simon tooNomadesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="60b1c-206">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="60b1c-208">Nell'elenco di applicazioni hello, selezionare **Nomadesk**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-208">In hello applications list, select **Nomadesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-nomadesk-tutorial/tutorial_nomadesk_app.png) 

3. <span data-ttu-id="60b1c-210">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="60b1c-212">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-212">Click **Add** button.</span></span> <span data-ttu-id="60b1c-213">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="60b1c-215">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="60b1c-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="60b1c-216">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60b1c-217">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="60b1c-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60b1c-218">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="60b1c-218">Testing single sign-on</span></span>

<span data-ttu-id="60b1c-219">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="60b1c-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="60b1c-220">Quando si fa clic su riquadro Nomadesk hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Nomadesk applicazione.</span><span class="sxs-lookup"><span data-stu-id="60b1c-220">When you click hello Nomadesk tile in hello Access Panel,  you should get automatically signed-on tooyour Nomadesk application.</span></span>
<span data-ttu-id="60b1c-221">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60b1c-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60b1c-222">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="60b1c-222">Additional resources</span></span>

* [<span data-ttu-id="60b1c-223">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60b1c-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60b1c-224">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60b1c-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadesk-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Rally Software | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Rally Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="f0c72-103">Esercitazione: Integrazione di Azure Active Directory con Rally Software</span><span class="sxs-lookup"><span data-stu-id="f0c72-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="f0c72-104">In questa esercitazione, è illustrato come toointegrate Rally Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0c72-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0c72-105">Integrazione di Rally Software con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f0c72-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f0c72-106">È possibile controllare in Azure AD che ha accesso tooRally Software.</span><span class="sxs-lookup"><span data-stu-id="f0c72-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="f0c72-107">È possibile abilitare l'utenti tooautomatically get connesso tooRally Software (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0c72-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f0c72-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0c72-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="f0c72-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0c72-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0c72-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f0c72-110">Prerequisites</span></span>

<span data-ttu-id="f0c72-111">integrazione di Azure AD con Rally Software tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f0c72-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="f0c72-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0c72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0c72-113">Sottoscrizione di Rally Software abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f0c72-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0c72-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f0c72-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0c72-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f0c72-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0c72-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f0c72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0c72-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0c72-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0c72-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f0c72-118">Scenario description</span></span>
<span data-ttu-id="f0c72-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f0c72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0c72-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f0c72-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0c72-121">Aggiunta di Rally Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f0c72-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="f0c72-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0c72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="f0c72-123">Aggiunta di Rally Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f0c72-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="f0c72-124">integrazione hello tooconfigure di Rally Software in Azure AD, è necessario tooadd Rally Software dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f0c72-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f0c72-125">**tooadd Rally Software dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f0c72-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0c72-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f0c72-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="f0c72-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f0c72-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="f0c72-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f0c72-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="f0c72-133">Nella casella di ricerca hello, digitare **Rally Software**selezionare **Rally Software** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f0c72-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Rally Software nell'elenco risultati hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f0c72-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0c72-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f0c72-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Rally Software mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f0c72-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0c72-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Rally Software è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0c72-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="f0c72-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Rally Software richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f0c72-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="f0c72-139">In Rally Software, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="f0c72-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f0c72-140">tooconfigure e test Azure single sign-on AD con Rally Software, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f0c72-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f0c72-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f0c72-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f0c72-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0c72-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0c72-143">**[Creare un utente test Rally Software](#create-a-rally-software-test-user)**  -toohave un equivalente di Britta Simon in Rally Software che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f0c72-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0c72-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c72-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0c72-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f0c72-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f0c72-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0c72-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f0c72-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Rally Software.</span><span class="sxs-lookup"><span data-stu-id="f0c72-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="f0c72-148">**Azure AD tooconfigure single sign-on con Rally Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f0c72-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0c72-149">Nel portale di Azure su hello hello **Rally Software** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="f0c72-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c72-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="f0c72-153">In hello **Rally Software dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f0c72-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="f0c72-155">a.</span><span class="sxs-lookup"><span data-stu-id="f0c72-155">a.</span></span> <span data-ttu-id="f0c72-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="f0c72-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="f0c72-157">b.</span><span class="sxs-lookup"><span data-stu-id="f0c72-157">b.</span></span> <span data-ttu-id="f0c72-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="f0c72-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0c72-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f0c72-159">These values are not real.</span></span> <span data-ttu-id="f0c72-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="f0c72-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f0c72-161">Contatto [team di supporto di Rally Software Client](https://help.rallydev.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="f0c72-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="f0c72-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f0c72-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="f0c72-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f0c72-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f0c72-166">In hello **Rally Software configurazione** fare clic su **configurare Rally Software** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f0c72-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f0c72-167">Hello copia **Sign-Out URL e l'ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f0c72-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="f0c72-169">Accedi tooyour **Rally Software** tenant.</span><span class="sxs-lookup"><span data-stu-id="f0c72-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="f0c72-170">Nella barra degli strumenti hello in primo piano hello, fare clic su **installazione**, quindi selezionare **sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="f0c72-171">![Sottoscrizione](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Sottoscrizione")</span><span class="sxs-lookup"><span data-stu-id="f0c72-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="f0c72-172">Fare clic su hello **azione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f0c72-172">Click hello **Action** button.</span></span> <span data-ttu-id="f0c72-173">Selezionare **Modifica sottoscrizione** in hello lato superiore destro della barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="f0c72-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="f0c72-174">In hello **sottoscrizione** pagina eseguire hello alla procedura seguente e quindi fare clic su **Salva e Chiudi**:</span><span class="sxs-lookup"><span data-stu-id="f0c72-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="f0c72-175">![Autenticazione](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Autenticazione")</span><span class="sxs-lookup"><span data-stu-id="f0c72-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="f0c72-176">a.</span><span class="sxs-lookup"><span data-stu-id="f0c72-176">a.</span></span> <span data-ttu-id="f0c72-177">Selezionare **Rally or SSO authentication** (Autenticazione Rally o SSO) dall'elenco a discesa Authentication (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="f0c72-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="f0c72-178">b.</span><span class="sxs-lookup"><span data-stu-id="f0c72-178">b.</span></span> <span data-ttu-id="f0c72-179">In hello **URL provider di identità** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0c72-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="f0c72-180">c.</span><span class="sxs-lookup"><span data-stu-id="f0c72-180">c.</span></span> <span data-ttu-id="f0c72-181">In hello **disconnessione SSO** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0c72-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="f0c72-182">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f0c72-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f0c72-183">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f0c72-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f0c72-184">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0c72-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f0c72-185">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0c72-185">Create an Azure AD test user</span></span>

<span data-ttu-id="f0c72-186">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f0c72-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="f0c72-188">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f0c72-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0c72-189">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f0c72-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f0c72-191">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f0c72-193">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f0c72-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f0c72-195">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f0c72-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f0c72-197">a.</span><span class="sxs-lookup"><span data-stu-id="f0c72-197">a.</span></span> <span data-ttu-id="f0c72-198">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0c72-199">b.</span><span class="sxs-lookup"><span data-stu-id="f0c72-199">b.</span></span> <span data-ttu-id="f0c72-200">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0c72-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="f0c72-201">c.</span><span class="sxs-lookup"><span data-stu-id="f0c72-201">c.</span></span> <span data-ttu-id="f0c72-202">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="f0c72-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="f0c72-203">d.</span><span class="sxs-lookup"><span data-stu-id="f0c72-203">d.</span></span> <span data-ttu-id="f0c72-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="f0c72-205">Creare un utente test di Rally Software</span><span class="sxs-lookup"><span data-stu-id="f0c72-205">Create a Rally Software test user</span></span>

<span data-ttu-id="f0c72-206">Per Azure AD utenti toobe in grado di toosign in devono essere sottoposte a provisioning toohello applicazione Rally Software usando i rispettivi nomi utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0c72-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="f0c72-207">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f0c72-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0c72-208">Accedi tooyour tenant di Rally Software.</span><span class="sxs-lookup"><span data-stu-id="f0c72-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="f0c72-209">Andare troppo**installazione \> utenti**, quindi fare clic su **+ Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="f0c72-210">![Utenti](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="f0c72-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="f0c72-211">Digitare il nome di hello nella casella di testo hello nuovo utente e quindi fare clic su **Aggiungi con dettagli**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="f0c72-212">In hello **Create User** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f0c72-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f0c72-213">![Crea utente](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="f0c72-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="f0c72-214">a.</span><span class="sxs-lookup"><span data-stu-id="f0c72-214">a.</span></span> <span data-ttu-id="f0c72-215">In hello **nome utente** casella di testo Nome hello del tipo di utente come **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="f0c72-216">b.</span><span class="sxs-lookup"><span data-stu-id="f0c72-216">b.</span></span> <span data-ttu-id="f0c72-217">In **indirizzo di posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f0c72-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f0c72-218">c.</span><span class="sxs-lookup"><span data-stu-id="f0c72-218">c.</span></span> <span data-ttu-id="f0c72-219">In **nome** testo hello nome dell'utente come immettere **Laura**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="f0c72-220">d.</span><span class="sxs-lookup"><span data-stu-id="f0c72-220">d.</span></span> <span data-ttu-id="f0c72-221">In **cognome** testo immettere il cognome di hello dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="f0c72-222">e.</span><span class="sxs-lookup"><span data-stu-id="f0c72-222">e.</span></span> <span data-ttu-id="f0c72-223">Fare clic su **Salva e chiudi**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f0c72-224">È possibile usare qualsiasi altro Rally Software utente account strumento di creazione o le API fornite da Rally Software tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0c72-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f0c72-225">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0c72-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f0c72-226">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRally Software.</span><span class="sxs-lookup"><span data-stu-id="f0c72-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="f0c72-228">**tooassign Britta Simon tooRally Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f0c72-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0c72-229">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f0c72-231">Nell'elenco di applicazioni hello, selezionare **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-231">In hello applications list, select **Rally Software**.</span></span>

    ![collegamento di Rally Software Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="f0c72-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="f0c72-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-235">Click **Add** button.</span></span> <span data-ttu-id="f0c72-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="f0c72-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f0c72-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f0c72-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0c72-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f0c72-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f0c72-241">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f0c72-241">Test single sign-on</span></span>

<span data-ttu-id="f0c72-242">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f0c72-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f0c72-243">Quando si fa clic su riquadro Rally Software hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Rally Software.</span><span class="sxs-lookup"><span data-stu-id="f0c72-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0c72-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f0c72-244">Additional resources</span></span>

* [<span data-ttu-id="f0c72-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0c72-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0c72-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0c72-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Halogen Software | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e alogeno Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="fa424-103">Esercitazione: Integrazione di Azure Active Directory con Halogen Software</span><span class="sxs-lookup"><span data-stu-id="fa424-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="fa424-104">In questa esercitazione, è illustrato come toointegrate alogeno Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa424-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa424-105">Integrazione Software alogeno con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="fa424-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fa424-106">È possibile controllare in Azure AD che ha accesso tooHalogen Software</span><span class="sxs-lookup"><span data-stu-id="fa424-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="fa424-107">È possibile abilitare l'utenti tooautomatically get connesso tooHalogen Software (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa424-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa424-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fa424-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fa424-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa424-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa424-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fa424-110">Prerequisites</span></span>

<span data-ttu-id="fa424-111">integrazione di Azure AD con Software alogeno tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fa424-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="fa424-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa424-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa424-113">Sottoscrizione di Halogen Software abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fa424-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa424-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="fa424-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa424-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="fa424-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa424-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fa424-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa424-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa424-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa424-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fa424-118">Scenario description</span></span>

<span data-ttu-id="fa424-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fa424-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa424-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="fa424-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa424-121">Aggiunta di alogeno Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fa424-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="fa424-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa424-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="fa424-123">Aggiunta di alogeno Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="fa424-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="fa424-124">integrazione hello tooconfigure di Software alogeno in Azure AD, è necessario tooadd alogeno Software dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fa424-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fa424-125">**tooadd alogeno Software dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa424-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa424-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fa424-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa424-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fa424-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fa424-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fa424-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="fa424-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fa424-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="fa424-133">Nella casella di ricerca hello, digitare **alogeno Software**.</span><span class="sxs-lookup"><span data-stu-id="fa424-133">In hello search box, type **Halogen Software**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="fa424-135">Nel riquadro dei risultati hello, selezionare **Software alogeno**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fa424-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa424-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa424-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa424-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Halogen Software mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fa424-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa424-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello alogeno software è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fa424-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="fa424-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello alogeno software richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="fa424-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="fa424-141">Nel Software alogeno, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="fa424-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fa424-142">tooconfigure e prova AD Azure single sign-on con alogeno Software, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="fa424-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fa424-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fa424-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fa424-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fa424-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa424-145">**[Creazione di un utente test alogeno Software](#creating-a-halogen-software-test-user)**  -toohave un equivalente di Britta Simon software alogeni che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fa424-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa424-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fa424-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa424-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="fa424-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa424-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa424-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa424-149">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione alogeno Software.</span><span class="sxs-lookup"><span data-stu-id="fa424-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="fa424-150">**Azure AD tooconfigure single sign-on con alogeno Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa424-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa424-151">Nel portale di Azure su hello hello **Software alogeno** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fa424-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fa424-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fa424-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="fa424-155">In hello **alogeno Software dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa424-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="fa424-157">a.</span><span class="sxs-lookup"><span data-stu-id="fa424-157">a.</span></span> <span data-ttu-id="fa424-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="fa424-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="fa424-159">b.</span><span class="sxs-lookup"><span data-stu-id="fa424-159">b.</span></span> <span data-ttu-id="fa424-160">In hello **identificatore** casella di testo, digitare un URL con modello di hello: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="fa424-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa424-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="fa424-161">These values are not real.</span></span> <span data-ttu-id="fa424-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="fa424-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fa424-163">Contatto [team di supporto Client Software alogeno](https://support.halogensoftware.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="fa424-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="fa424-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="fa424-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="fa424-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fa424-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fa424-168">In un'altra finestra del browser, sign-on tooyour **Software alogeno** applicazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa424-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="fa424-169">Fare clic su hello **opzioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="fa424-169">Click hello **Options** tab.</span></span> 
   
    ![Cos'è Azure AD Connect][12]

8. <span data-ttu-id="fa424-171">Nel riquadro di spostamento a sinistra di hello, fare clic su **configurazione SAML**.</span><span class="sxs-lookup"><span data-stu-id="fa424-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Cos'è Azure AD Connect][13]

9. <span data-ttu-id="fa424-173">In hello **configurazione SAML** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa424-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![Cos'è Azure AD Connect][14]

     <span data-ttu-id="fa424-175">a.</span><span class="sxs-lookup"><span data-stu-id="fa424-175">a.</span></span> <span data-ttu-id="fa424-176">Come **Identificatore univoco**, selezionare **NameID**.</span><span class="sxs-lookup"><span data-stu-id="fa424-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="fa424-177">b.</span><span class="sxs-lookup"><span data-stu-id="fa424-177">b.</span></span> <span data-ttu-id="fa424-178">Come **Unique Identifier Maps To** (L'identificatore univoco mappa verso) selezionare **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="fa424-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="fa424-179">c.</span><span class="sxs-lookup"><span data-stu-id="fa424-179">c.</span></span> <span data-ttu-id="fa424-180">tooupload file di metadati scaricato, fare clic su **Sfoglia** file hello tooselect e quindi **carica File**.</span><span class="sxs-lookup"><span data-stu-id="fa424-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="fa424-181">d.</span><span class="sxs-lookup"><span data-stu-id="fa424-181">d.</span></span> <span data-ttu-id="fa424-182">configurazione di hello tootest, fare clic su **Esegui Test**.</span><span class="sxs-lookup"><span data-stu-id="fa424-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="fa424-183">È necessario toowait per il messaggio hello "*test SAML hello è stato completato. Please close this window*".</span><span class="sxs-lookup"><span data-stu-id="fa424-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="fa424-184">Quindi, chiudere finestra del browser aperto hello.</span><span class="sxs-lookup"><span data-stu-id="fa424-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="fa424-185">Hello **Enable SAML** casella di controllo è abilitata solo se il test di hello è stato completato.</span><span class="sxs-lookup"><span data-stu-id="fa424-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="fa424-186">e.</span><span class="sxs-lookup"><span data-stu-id="fa424-186">e.</span></span> <span data-ttu-id="fa424-187">Selezionare **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="fa424-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="fa424-188">f.</span><span class="sxs-lookup"><span data-stu-id="fa424-188">f.</span></span> <span data-ttu-id="fa424-189">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="fa424-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="fa424-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="fa424-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fa424-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="fa424-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fa424-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fa424-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa424-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa424-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="fa424-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fa424-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="fa424-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa424-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa424-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="fa424-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa424-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fa424-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa424-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="fa424-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa424-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa424-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa424-205">a.</span><span class="sxs-lookup"><span data-stu-id="fa424-205">a.</span></span> <span data-ttu-id="fa424-206">In hello **nome** casella di testo, il nome di tipo come **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa424-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="fa424-207">b.</span><span class="sxs-lookup"><span data-stu-id="fa424-207">b.</span></span> <span data-ttu-id="fa424-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fa424-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa424-209">c.</span><span class="sxs-lookup"><span data-stu-id="fa424-209">c.</span></span> <span data-ttu-id="fa424-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="fa424-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fa424-211">d.</span><span class="sxs-lookup"><span data-stu-id="fa424-211">d.</span></span> <span data-ttu-id="fa424-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fa424-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="fa424-213">Creazione di un utente test di Halogen Software</span><span class="sxs-lookup"><span data-stu-id="fa424-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="fa424-214">obiettivo Hello di questa sezione è un utente denominato Britta Simon nel Software alogeno toocreate.</span><span class="sxs-lookup"><span data-stu-id="fa424-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="fa424-215">**un utente denominato Britta Simon nel Software alogeno toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa424-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa424-216">Accesso tooyour **Software alogeno** applicazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="fa424-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="fa424-217">Fare clic su hello **Center utente** scheda e quindi fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="fa424-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![Cos'è Azure AD Connect][300]  

3. <span data-ttu-id="fa424-219">In hello **nuovo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fa424-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![Cos'è Azure AD Connect][301]

    <span data-ttu-id="fa424-221">a.</span><span class="sxs-lookup"><span data-stu-id="fa424-221">a.</span></span> <span data-ttu-id="fa424-222">In hello **nome** casella di testo Nome tipo di utente hello come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="fa424-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="fa424-223">b.</span><span class="sxs-lookup"><span data-stu-id="fa424-223">b.</span></span> <span data-ttu-id="fa424-224">In hello **cognome** casella di testo, digitare cognome dell'utente hello come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fa424-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="fa424-225">c.</span><span class="sxs-lookup"><span data-stu-id="fa424-225">c.</span></span> <span data-ttu-id="fa424-226">In hello **Username** casella tipo **Britta Simon**, nome utente hello come hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa424-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="fa424-227">d.</span><span class="sxs-lookup"><span data-stu-id="fa424-227">d.</span></span> <span data-ttu-id="fa424-228">In hello **Password** casella di testo, digitare una password per Laura.</span><span class="sxs-lookup"><span data-stu-id="fa424-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="fa424-229">e.</span><span class="sxs-lookup"><span data-stu-id="fa424-229">e.</span></span> <span data-ttu-id="fa424-230">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fa424-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fa424-231">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa424-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fa424-232">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHalogen Software.</span><span class="sxs-lookup"><span data-stu-id="fa424-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Assegna utente][200] 

<span data-ttu-id="fa424-234">**tooassign Britta Simon tooHalogen Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fa424-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa424-235">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fa424-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fa424-237">Nell'elenco di applicazioni hello, selezionare **alogeno Software**.</span><span class="sxs-lookup"><span data-stu-id="fa424-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="fa424-239">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fa424-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="fa424-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fa424-241">Click **Add** button.</span></span> <span data-ttu-id="fa424-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fa424-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="fa424-244">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="fa424-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fa424-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fa424-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa424-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fa424-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa424-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fa424-247">Testing single sign-on</span></span>

<span data-ttu-id="fa424-248">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fa424-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="fa424-249">Quando si fa clic su riquadro Software alogeno hello in hello Pannello di accesso, è necessario ottenere l'applicazione Software alogeno tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="fa424-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa424-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fa424-250">Additional resources</span></span>

* [<span data-ttu-id="fa424-251">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa424-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa424-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa424-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png

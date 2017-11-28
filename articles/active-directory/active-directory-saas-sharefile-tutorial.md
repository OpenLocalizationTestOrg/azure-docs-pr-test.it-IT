---
title: 'Esercitazione: Integrazione di Azure Active Directory con Citrix ShareFile | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Citrix ShareFile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="85614-103">Esercitazione: Integrazione di Azure Active Directory con Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="85614-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="85614-104">In questa esercitazione, è illustrato come toointegrate Citrix ShareFile con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85614-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85614-105">Integrazione di Citrix ShareFile con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="85614-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="85614-106">È possibile controllare in Azure AD che ha accesso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="85614-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="85614-107">È possibile abilitare l'utenti tooautomatically get connesso tooCitrix ShareFile (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85614-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="85614-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="85614-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="85614-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85614-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85614-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="85614-110">Prerequisites</span></span>

<span data-ttu-id="85614-111">integrazione di Azure AD con Citrix ShareFile tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="85614-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="85614-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85614-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85614-113">Sottoscrizione di Citrix ShareFile abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="85614-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85614-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="85614-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85614-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="85614-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85614-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="85614-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85614-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85614-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85614-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="85614-118">Scenario description</span></span>
<span data-ttu-id="85614-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="85614-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85614-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="85614-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85614-121">Aggiungere Citrix ShareFile dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="85614-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="85614-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85614-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="85614-123">Aggiungere Citrix ShareFile dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="85614-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="85614-124">integrazione hello tooconfigure di Citrix ShareFile in Azure AD, è necessario tooadd Citrix ShareFile dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="85614-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="85614-125">**tooadd Citrix ShareFile dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="85614-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="85614-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="85614-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="85614-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="85614-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="85614-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="85614-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="85614-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="85614-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="85614-133">Nella casella di ricerca hello, digitare **Citrix ShareFile**selezionare **Citrix ShareFile** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="85614-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco dei risultati di Citrix ShareFile in hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="85614-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85614-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="85614-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Citrix ShareFile in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85614-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85614-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Citrix ShareFile è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85614-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="85614-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Citrix ShareFile deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="85614-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="85614-139">In Citrix ShareFile, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="85614-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="85614-140">tooconfigure e test Azure single sign-on AD con Citrix ShareFile, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="85614-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="85614-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="85614-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="85614-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85614-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85614-143">**[Creare un utente test Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave un equivalente di Britta Simon in Citrix ShareFile che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="85614-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="85614-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="85614-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85614-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="85614-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="85614-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85614-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="85614-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="85614-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="85614-148">**Azure AD tooconfigure single sign-on con Citrix ShareFile, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="85614-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="85614-149">Nel portale di Azure su hello hello **Citrix ShareFile** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="85614-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="85614-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="85614-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="85614-153">In hello **Citrix ShareFile dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="85614-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="85614-155">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="85614-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85614-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="85614-156">This value is not real.</span></span> <span data-ttu-id="85614-157">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="85614-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="85614-158">Contatto [team di supporto Client di Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="85614-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="85614-159">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="85614-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="85614-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="85614-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="85614-163">In hello **configurazione di Citrix ShareFile** fare clic su **configurare Citrix ShareFile** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="85614-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="85614-164">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="85614-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="85614-166">In un'altra finestra del Web browser accedere al sito aziendale di **Citrix ShareFile** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="85614-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="85614-167">Nella barra degli strumenti hello in primo piano hello, fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="85614-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="85614-168">Nel riquadro di spostamento a sinistra di hello, selezionare **configurare Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="85614-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="85614-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span><span class="sxs-lookup"><span data-stu-id="85614-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="85614-170">In hello **Single Sign-On / SAML 2.0 Configuration** nella pagina in **le impostazioni di base**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="85614-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="85614-171">![Single Sign-On](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="85614-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="85614-172">a.</span><span class="sxs-lookup"><span data-stu-id="85614-172">a.</span></span> <span data-ttu-id="85614-173">Fare clic su **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="85614-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="85614-174">b.</span><span class="sxs-lookup"><span data-stu-id="85614-174">b.</span></span> <span data-ttu-id="85614-175">In **Your IDP Issuer / Entity ID** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="85614-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="85614-176">c.</span><span class="sxs-lookup"><span data-stu-id="85614-176">c.</span></span> <span data-ttu-id="85614-177">Fare clic su **modifica** toohello Avanti **certificato x. 509** campo e quindi carica certificato di hello è stato scaricato dal portale di Azure di hello.</span><span class="sxs-lookup"><span data-stu-id="85614-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="85614-178">d.</span><span class="sxs-lookup"><span data-stu-id="85614-178">d.</span></span> <span data-ttu-id="85614-179">In **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="85614-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="85614-180">e.</span><span class="sxs-lookup"><span data-stu-id="85614-180">e.</span></span> <span data-ttu-id="85614-181">In **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="85614-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="85614-182">Fare clic su **salvare** nel portale di gestione di Citrix ShareFile hello.</span><span class="sxs-lookup"><span data-stu-id="85614-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="85614-183">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="85614-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="85614-184">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="85614-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="85614-185">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85614-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="85614-186">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85614-186">Create an Azure AD test user</span></span>

<span data-ttu-id="85614-187">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="85614-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="85614-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="85614-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="85614-190">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="85614-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="85614-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="85614-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="85614-194">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="85614-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="85614-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="85614-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="85614-198">a.</span><span class="sxs-lookup"><span data-stu-id="85614-198">a.</span></span> <span data-ttu-id="85614-199">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85614-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85614-200">b.</span><span class="sxs-lookup"><span data-stu-id="85614-200">b.</span></span> <span data-ttu-id="85614-201">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85614-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="85614-202">c.</span><span class="sxs-lookup"><span data-stu-id="85614-202">c.</span></span> <span data-ttu-id="85614-203">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="85614-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="85614-204">d.</span><span class="sxs-lookup"><span data-stu-id="85614-204">d.</span></span> <span data-ttu-id="85614-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="85614-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="85614-206">Creare un utente test di Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="85614-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="85614-207">In ordine tooenable Azure AD utenti toolog in Citrix ShareFile, è necessario eseguirne il provisioning in Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="85614-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="85614-208">Nel caso di hello di Citrix ShareFile, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="85614-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="85614-209">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="85614-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="85614-210">Accedi tooyour **Citrix ShareFile** tenant.</span><span class="sxs-lookup"><span data-stu-id="85614-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="85614-211">Fare clic su **Manage Users \> Manage Users Home \> + Create Employee** (Gestisci utenti > Gestisci home utenti > + Crea dipendente).</span><span class="sxs-lookup"><span data-stu-id="85614-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="85614-212">![Crea dipendente](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Crea dipendente")</span><span class="sxs-lookup"><span data-stu-id="85614-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="85614-213">In hello **le informazioni di base** sezione, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="85614-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="85614-214">![Informazioni di base](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Informazioni di base")</span><span class="sxs-lookup"><span data-stu-id="85614-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="85614-215">a.</span><span class="sxs-lookup"><span data-stu-id="85614-215">a.</span></span> <span data-ttu-id="85614-216">In hello **indirizzo di posta elettronica** casella Indirizzo di posta elettronica di tipo hello di Britta Simon come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="85614-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="85614-217">b.</span><span class="sxs-lookup"><span data-stu-id="85614-217">b.</span></span> <span data-ttu-id="85614-218">In hello **nome** casella tipo **nome** dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="85614-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="85614-219">c.</span><span class="sxs-lookup"><span data-stu-id="85614-219">c.</span></span> <span data-ttu-id="85614-220">In hello **cognome** casella tipo **cognome** dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="85614-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="85614-221">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="85614-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="85614-222">titolare dell'account di Azure AD Hello riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo. È possibile usare qualsiasi altro Citrix ShareFile utente account strumento di creazione o qualsiasi API fornita da Citrix ShareFile tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85614-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="85614-223">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="85614-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="85614-224">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="85614-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="85614-226">**tooassign tooCitrix Britta Simon ShareFile, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="85614-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="85614-227">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="85614-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="85614-229">Nell'elenco di applicazioni hello, selezionare **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="85614-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Hello Citrix ShareFile collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="85614-231">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="85614-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="85614-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="85614-233">Click **Add** button.</span></span> <span data-ttu-id="85614-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="85614-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="85614-236">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="85614-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="85614-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="85614-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85614-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="85614-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="85614-239">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="85614-239">Test single sign-on</span></span>

<span data-ttu-id="85614-240">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="85614-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="85614-241">Quando si fa clic hello Citrix ShareFile riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="85614-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="85614-242">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85614-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="85614-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="85614-243">Additional resources</span></span>

* [<span data-ttu-id="85614-244">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85614-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85614-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85614-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: integrazione di Azure Active Directory con EasyTerritory | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed EasyTerritory.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4f1e9fb4d615325f0d57bebaed955529d5dcd9b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="bd53e-103">Esercitazione: integrazione di Azure Active Directory con EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="bd53e-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="bd53e-104">In questa esercitazione, è illustrato come toointegrate EasyTerritory con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd53e-104">In this tutorial, you learn how toointegrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd53e-105">Integrazione EasyTerritory con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="bd53e-105">Integrating EasyTerritory with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd53e-106">È possibile controllare in Azure AD che ha accesso tooEasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="bd53e-106">You can control in Azure AD who has access tooEasyTerritory.</span></span>
- <span data-ttu-id="bd53e-107">È possibile abilitare l'utenti tooautomatically get connesso tooEasyTerritory (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd53e-107">You can enable your users tooautomatically get signed-on tooEasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bd53e-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd53e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="bd53e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd53e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd53e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd53e-110">Prerequisites</span></span>

<span data-ttu-id="bd53e-111">integrazione di Azure AD con EasyTerritory tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="bd53e-111">tooconfigure Azure AD integration with EasyTerritory, you need hello following items:</span></span>

- <span data-ttu-id="bd53e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd53e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd53e-113">Sottoscrizione di EasyTerritory abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd53e-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd53e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bd53e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd53e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="bd53e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd53e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bd53e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd53e-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd53e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd53e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bd53e-118">Scenario description</span></span>
<span data-ttu-id="bd53e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bd53e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd53e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="bd53e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd53e-121">Aggiunta di EasyTerritory dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bd53e-121">Adding EasyTerritory from hello gallery</span></span>
2. <span data-ttu-id="bd53e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd53e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-hello-gallery"></a><span data-ttu-id="bd53e-123">Aggiunta di EasyTerritory dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bd53e-123">Adding EasyTerritory from hello gallery</span></span>
<span data-ttu-id="bd53e-124">integrazione hello tooconfigure di EasyTerritory in Azure AD, è necessario tooadd EasyTerritory dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bd53e-124">tooconfigure hello integration of EasyTerritory into Azure AD, you need tooadd EasyTerritory from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd53e-125">**tooadd EasyTerritory dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd53e-125">**tooadd EasyTerritory from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53e-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bd53e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="bd53e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd53e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="bd53e-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bd53e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="bd53e-133">Nella casella di ricerca hello, digitare **EasyTerritory**selezionare **EasyTerritory** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bd53e-133">In hello search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bd53e-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd53e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bd53e-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con EasyTerritory con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bd53e-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd53e-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in EasyTerritory è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd53e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EasyTerritory is tooa user in Azure AD.</span></span> <span data-ttu-id="bd53e-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in EasyTerritory deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="bd53e-138">In other words, a link relationship between an Azure AD user and hello related user in EasyTerritory needs toobe established.</span></span>

<span data-ttu-id="bd53e-139">In EasyTerritory, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="bd53e-139">In EasyTerritory, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bd53e-140">tooconfigure e prova AD Azure single sign-on con EasyTerritory, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="bd53e-140">tooconfigure and test Azure AD single sign-on with EasyTerritory, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd53e-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bd53e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd53e-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd53e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd53e-143">**[Creare un utente test EasyTerritory](#create-a-easyterritory-test-user)**  -toohave un equivalente di Britta Simon in EasyTerritory che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bd53e-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - toohave a counterpart of Britta Simon in EasyTerritory that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd53e-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bd53e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd53e-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bd53e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bd53e-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd53e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bd53e-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="bd53e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="bd53e-148">**Azure AD tooconfigure single sign-on con EasyTerritory, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd53e-148">**tooconfigure Azure AD single sign-on with EasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53e-149">Nel portale di Azure su hello hello **EasyTerritory** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-149">In hello Azure portal, on hello **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="bd53e-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bd53e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="bd53e-153">In hello **EasyTerritory dominio e gli URL** seguire passaggi se si desidera modalità iniziata da un'applicazione hello tooconfigure in IDP hello:</span><span class="sxs-lookup"><span data-stu-id="bd53e-153">On hello **EasyTerritory Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="bd53e-155">a.</span><span class="sxs-lookup"><span data-stu-id="bd53e-155">a.</span></span> <span data-ttu-id="bd53e-156">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="bd53e-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="bd53e-157">b.</span><span class="sxs-lookup"><span data-stu-id="bd53e-157">b.</span></span> <span data-ttu-id="bd53e-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="bd53e-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="bd53e-159">Controllare **Mostra URL impostazioni avanzate** ed eseguire hello riportata dopo il passaggio se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="bd53e-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="bd53e-161">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="bd53e-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bd53e-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="bd53e-162">These values are not real.</span></span> <span data-ttu-id="bd53e-163">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="bd53e-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="bd53e-164">Contatto [team di supporto EasyTerritory Client](mailto:sales@easyterritory.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="bd53e-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) tooget these values.</span></span> 

5. <span data-ttu-id="bd53e-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bd53e-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="bd53e-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bd53e-167">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bd53e-169">tooconfigure single sign-on sul **EasyTerritory** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="bd53e-169">tooconfigure single sign-on on **EasyTerritory** side, you need toosend hello downloaded **Metadata XML** too[EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="bd53e-170">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="bd53e-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bd53e-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="bd53e-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd53e-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="bd53e-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd53e-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd53e-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bd53e-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd53e-174">Create an Azure AD test user</span></span>

<span data-ttu-id="bd53e-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bd53e-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="bd53e-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd53e-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53e-178">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="bd53e-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bd53e-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bd53e-182">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bd53e-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bd53e-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bd53e-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bd53e-186">a.</span><span class="sxs-lookup"><span data-stu-id="bd53e-186">a.</span></span> <span data-ttu-id="bd53e-187">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd53e-188">b.</span><span class="sxs-lookup"><span data-stu-id="bd53e-188">b.</span></span> <span data-ttu-id="bd53e-189">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd53e-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="bd53e-190">c.</span><span class="sxs-lookup"><span data-stu-id="bd53e-190">c.</span></span> <span data-ttu-id="bd53e-191">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="bd53e-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="bd53e-192">d.</span><span class="sxs-lookup"><span data-stu-id="bd53e-192">d.</span></span> <span data-ttu-id="bd53e-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="bd53e-194">Creare un utente di test di EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="bd53e-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="bd53e-195">In questa sezione viene creato un utente chiamato Britta Simon in EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="bd53e-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="bd53e-196">Rivolgersi [team di supporto EasyTerritory](mailto:sales@easyterritory.com) utenti hello tooadd nella piattaforma EasyTerritory hello.</span><span class="sxs-lookup"><span data-stu-id="bd53e-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) tooadd hello users in hello EasyTerritory platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bd53e-197">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd53e-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bd53e-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="bd53e-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEasyTerritory.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="bd53e-200">**tooassign Britta Simon tooEasyTerritory, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bd53e-200">**tooassign Britta Simon tooEasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd53e-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bd53e-203">Nell'elenco di applicazioni hello, selezionare **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-203">In hello applications list, select **EasyTerritory**.</span></span>

    ![collegamento EasyTerritory Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="bd53e-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="bd53e-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-207">Click **Add** button.</span></span> <span data-ttu-id="bd53e-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="bd53e-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="bd53e-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd53e-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd53e-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bd53e-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bd53e-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bd53e-213">Test single sign-on</span></span>

<span data-ttu-id="bd53e-214">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bd53e-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd53e-215">Quando si fa clic su riquadro EasyTerritory hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour EasyTerritory applicazione.</span><span class="sxs-lookup"><span data-stu-id="bd53e-215">When you click hello EasyTerritory tile in hello Access Panel, you should get automatically signed-on tooyour EasyTerritory application.</span></span>
<span data-ttu-id="bd53e-216">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bd53e-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bd53e-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bd53e-217">Additional resources</span></span>

* [<span data-ttu-id="bd53e-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd53e-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd53e-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd53e-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png


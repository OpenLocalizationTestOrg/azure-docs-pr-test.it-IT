---
title: "Esercitazione: Integrazione di Azure Active Directory con Infor Retail – Information Management | Documentazione Microsoft"
description: 'Informazioni su come tooconfigure single sign-on tra Azure Active Directory e delle informazioni di vendita al dettaglio: gestione di informazioni.'
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 9cd8ab65d41d01832e0611f7f8254aa257120508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="22c81-103">Esercitazione: Integrazione di Azure Active Directory con Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="22c81-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="22c81-104">In questa esercitazione, è illustrato come toointegrate vendita al dettaglio delle informazioni: informazioni di gestione con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22c81-104">In this tutorial, you learn how toointegrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22c81-105">L'integrazione delle informazioni di vendita al dettaglio – Information Management con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="22c81-105">Integrating Infor Retail – Information Management with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="22c81-106">È possibile controllare in Azure AD che ha accesso tooInfor delle vendite al dettaglio: gestione di informazioni.</span><span class="sxs-lookup"><span data-stu-id="22c81-106">You can control in Azure AD who has access tooInfor Retail – Information Management.</span></span>
- <span data-ttu-id="22c81-107">È possibile abilitare l'utenti tooautomatically get connesso tooInfor delle vendite al dettaglio: gestione di informazioni (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22c81-107">You can enable your users tooautomatically get signed-on tooInfor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="22c81-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22c81-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="22c81-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22c81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22c81-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="22c81-110">Prerequisites</span></span>

<span data-ttu-id="22c81-111">tooconfigure integrazione di Azure AD con delle informazioni di vendita al dettaglio: gestione di informazioni, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="22c81-111">tooconfigure Azure AD integration with Infor Retail – Information Management, you need hello following items:</span></span>

- <span data-ttu-id="22c81-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22c81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22c81-113">Sottoscrizione di Infor Retail – Information Management abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="22c81-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22c81-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="22c81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22c81-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="22c81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22c81-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="22c81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22c81-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22c81-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22c81-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="22c81-118">Scenario description</span></span>
<span data-ttu-id="22c81-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="22c81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22c81-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="22c81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22c81-121">Aggiunta delle informazioni delle vendite al dettaglio: gestione di informazioni dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="22c81-121">Adding Infor Retail – Information Management from hello gallery</span></span>
2. <span data-ttu-id="22c81-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22c81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-hello-gallery"></a><span data-ttu-id="22c81-123">Aggiunta delle informazioni delle vendite al dettaglio: gestione di informazioni dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="22c81-123">Adding Infor Retail – Information Management from hello gallery</span></span>
<span data-ttu-id="22c81-124">integrazione di hello tooconfigure delle informazioni di vendita al dettaglio: gestione di informazioni in Azure AD, è necessario tooadd delle informazioni di vendita al dettaglio: gestione di informazioni dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="22c81-124">tooconfigure hello integration of Infor Retail – Information Management into Azure AD, you need tooadd Infor Retail – Information Management from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="22c81-125">**tooadd vendita al dettaglio delle informazioni: gestione di informazioni dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22c81-125">**tooadd Infor Retail – Information Management from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="22c81-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="22c81-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="22c81-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="22c81-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="22c81-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22c81-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="22c81-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="22c81-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="22c81-133">Nella casella di ricerca hello, digitare **delle informazioni di vendita al dettaglio: gestione di informazioni**selezionare **delle informazioni di vendita al dettaglio – Information Management** dal pannello risultati quindi fare clic su **Aggiungi** hello tooadd pulsante applicazione.</span><span class="sxs-lookup"><span data-stu-id="22c81-133">In hello search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco dei risultati delle informazioni di vendita al dettaglio: gestione delle informazioni sulla hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="22c81-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22c81-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="22c81-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Infor Retail – Information Management usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="22c81-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="22c81-137">Toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello delle informazioni di dettaglio: gestione di informazioni è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22c81-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Infor Retail – Information Management is tooa user in Azure AD.</span></span> <span data-ttu-id="22c81-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello delle informazioni di dettaglio: gestione delle informazioni deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="22c81-138">In other words, a link relationship between an Azure AD user and hello related user in Infor Retail – Information Management needs toobe established.</span></span>

<span data-ttu-id="22c81-139">Dettaglio delle informazioni-Information Management, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="22c81-139">In Infor Retail – Information Management, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="22c81-140">tooconfigure e prova AD Azure single sign-on con delle informazioni di vendita al dettaglio: gestione di informazioni, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="22c81-140">tooconfigure and test Azure AD single sign-on with Infor Retail – Information Management, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="22c81-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="22c81-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="22c81-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22c81-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22c81-143">**[Creare una vendita al dettaglio delle informazioni di: utente di gestione dei test](#create-an-infor-retail--information-management-test-user)**  - toohave un equivalente di Britta Simon delle informazioni di dettaglio: gestione di informazioni che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="22c81-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - toohave a counterpart of Britta Simon in Infor Retail – Information Management that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="22c81-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="22c81-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22c81-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="22c81-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="22c81-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22c81-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="22c81-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on, il dettaglio delle informazioni: applicazione di gestione di informazioni.</span><span class="sxs-lookup"><span data-stu-id="22c81-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="22c81-148">**tooconfigure AD Azure single sign-on con delle informazioni di vendita al dettaglio: gestione di informazioni, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22c81-148">**tooconfigure Azure AD single sign-on with Infor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="22c81-149">Nel portale di Azure su hello hello **delle informazioni di vendita al dettaglio – Information Management** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="22c81-149">In hello Azure portal, on hello **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="22c81-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="22c81-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="22c81-153">In hello **delle informazioni di vendita al dettaglio – URL e il dominio di gestione di informazioni** seguire passaggi se si desidera modalità iniziata da un'applicazione hello tooconfigure in IDP hello:</span><span class="sxs-lookup"><span data-stu-id="22c81-153">On hello **Infor Retail – Information Management Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Infor Retail – Information Management per IDP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="22c81-155">a.</span><span class="sxs-lookup"><span data-stu-id="22c81-155">a.</span></span> <span data-ttu-id="22c81-156">In hello **identificatore** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="22c81-156">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="22c81-157">b.</span><span class="sxs-lookup"><span data-stu-id="22c81-157">b.</span></span> <span data-ttu-id="22c81-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="22c81-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="22c81-159">Controllare **Mostra URL impostazioni avanzate** ed eseguire hello riportata dopo il passaggio se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="22c81-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Infor Retail – Information Management per SP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="22c81-161">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="22c81-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="22c81-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="22c81-162">These values are not real.</span></span> <span data-ttu-id="22c81-163">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="22c81-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="22c81-164">Contatto [delle informazioni di vendita al dettaglio: il team di supporto Client di gestione di informazioni](mailto:innovate@infor.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="22c81-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) tooget these values.</span></span> 

5. <span data-ttu-id="22c81-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="22c81-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="22c81-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="22c81-167">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="22c81-169">tooconfigure single sign-on sul **delle informazioni di vendita al dettaglio – Information Management** lato, è necessario hello toosend scaricato **Metadata XML** troppo[delle informazioni di vendita al dettaglio: il team di supporto di gestione di informazioni ](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="22c81-169">tooconfigure single sign-on on **Infor Retail – Information Management** side, you need toosend hello downloaded **Metadata XML** too[Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="22c81-170">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="22c81-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="22c81-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="22c81-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="22c81-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="22c81-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="22c81-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="22c81-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="22c81-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22c81-174">Create an Azure AD test user</span></span>

<span data-ttu-id="22c81-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="22c81-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="22c81-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22c81-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="22c81-178">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="22c81-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="22c81-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="22c81-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="22c81-182">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="22c81-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="22c81-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="22c81-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="22c81-186">a.</span><span class="sxs-lookup"><span data-stu-id="22c81-186">a.</span></span> <span data-ttu-id="22c81-187">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22c81-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22c81-188">b.</span><span class="sxs-lookup"><span data-stu-id="22c81-188">b.</span></span> <span data-ttu-id="22c81-189">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22c81-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="22c81-190">c.</span><span class="sxs-lookup"><span data-stu-id="22c81-190">c.</span></span> <span data-ttu-id="22c81-191">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="22c81-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="22c81-192">d.</span><span class="sxs-lookup"><span data-stu-id="22c81-192">d.</span></span> <span data-ttu-id="22c81-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="22c81-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="22c81-194">Creare un utente di test di Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="22c81-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="22c81-195">In questa sezione viene creato un utente chiamato Britta Simon in Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="22c81-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="22c81-196">Rivolgersi [delle informazioni di vendita al dettaglio: il team di supporto di gestione di informazioni](mailto:innovate@infor.com) utenti hello tooadd hello delle informazioni di vendita al dettaglio: piattaforma di gestione.</span><span class="sxs-lookup"><span data-stu-id="22c81-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) tooadd hello users in hello Infor Retail – Information Management platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="22c81-197">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="22c81-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="22c81-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooInfor delle vendite al dettaglio: gestione di informazioni.</span><span class="sxs-lookup"><span data-stu-id="22c81-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInfor Retail – Information Management.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="22c81-200">**tooassign Britta Simon tooInfor delle vendite al dettaglio: gestione di informazioni, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22c81-200">**tooassign Britta Simon tooInfor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="22c81-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22c81-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="22c81-203">Nell'elenco di applicazioni hello, selezionare **delle informazioni di vendita al dettaglio – Information Management**.</span><span class="sxs-lookup"><span data-stu-id="22c81-203">In hello applications list, select **Infor Retail – Information Management**.</span></span>

    ![Hello delle informazioni di vendita al dettaglio: gestione delle informazioni sul collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="22c81-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="22c81-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="22c81-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22c81-207">Click **Add** button.</span></span> <span data-ttu-id="22c81-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22c81-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="22c81-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="22c81-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="22c81-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="22c81-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22c81-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22c81-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="22c81-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="22c81-213">Test single sign-on</span></span>

<span data-ttu-id="22c81-214">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="22c81-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="22c81-215">Quando si fa clic hello delle informazioni di vendita al dettaglio: riquadro di gestione delle informazioni nel Pannello di accesso, hello è necessario ottenere automaticamente firmato in tooyour vendita al dettaglio delle informazioni: applicazione di gestione di informazioni.</span><span class="sxs-lookup"><span data-stu-id="22c81-215">When you click hello Infor Retail – Information Management tile in hello Access Panel, you should get automatically signed-on tooyour Infor Retail – Information Management application.</span></span>
<span data-ttu-id="22c81-216">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="22c81-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="22c81-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="22c81-217">Additional resources</span></span>

* [<span data-ttu-id="22c81-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22c81-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22c81-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22c81-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Predictix Ordering | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e di ordinamento Predictix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2fe2f976-e97f-4368-9695-3e1624409e8b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 0418ef24d7942b6b751c0b4d64e7bd1fba1d6a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-ordering"></a><span data-ttu-id="209c9-103">Esercitazione: Integrazione di Azure Active Directory con Predictix Ordering</span><span class="sxs-lookup"><span data-stu-id="209c9-103">Tutorial: Azure Active Directory integration with Predictix Ordering</span></span>

<span data-ttu-id="209c9-104">In questa esercitazione, è illustrato come toointegrate Predictix ordinamento con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="209c9-104">In this tutorial, you learn how toointegrate Predictix Ordering with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="209c9-105">Integrazione Predictix ordinamento con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="209c9-105">Integrating Predictix Ordering with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="209c9-106">È possibile controllare in Azure AD che ha accesso tooPredictix ordinamento.</span><span class="sxs-lookup"><span data-stu-id="209c9-106">You can control in Azure AD who has access tooPredictix Ordering.</span></span>
- <span data-ttu-id="209c9-107">È possibile abilitare il get tooautomatically utenti connesso tooPredictix ordinamento (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="209c9-107">You can enable your users tooautomatically get signed-on tooPredictix Ordering (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="209c9-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="209c9-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="209c9-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="209c9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="209c9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="209c9-110">Prerequisites</span></span>

<span data-ttu-id="209c9-111">integrazione di Azure AD con ordinamento Predictix tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="209c9-111">tooconfigure Azure AD integration with Predictix Ordering, you need hello following items:</span></span>

- <span data-ttu-id="209c9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="209c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="209c9-113">Sottoscrizione di Predictix Ordering abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="209c9-113">A Predictix Ordering single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="209c9-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="209c9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="209c9-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="209c9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="209c9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="209c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="209c9-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="209c9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="209c9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="209c9-118">Scenario description</span></span>
<span data-ttu-id="209c9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="209c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="209c9-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="209c9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="209c9-121">Aggiunta di ordinamento Predictix dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="209c9-121">Adding Predictix Ordering from hello gallery</span></span>
2. <span data-ttu-id="209c9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="209c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-ordering-from-hello-gallery"></a><span data-ttu-id="209c9-123">Aggiunta di ordinamento Predictix dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="209c9-123">Adding Predictix Ordering from hello gallery</span></span>
<span data-ttu-id="209c9-124">integrazione hello tooconfigure di ordinamento Predictix in Azure AD, è necessario tooadd Predictix ordinamento dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="209c9-124">tooconfigure hello integration of Predictix Ordering into Azure AD, you need tooadd Predictix Ordering from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="209c9-125">**tooadd Predictix ordinamento dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="209c9-125">**tooadd Predictix Ordering from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="209c9-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="209c9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="209c9-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="209c9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="209c9-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="209c9-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="209c9-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="209c9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="209c9-133">Nella casella di ricerca hello, digitare **Predictix ordinamento**selezionare **Predictix ordinamento** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="209c9-133">In hello search box, type **Predictix Ordering**, select **Predictix Ordering** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco dei risultati di ordinamento Predictix in hello](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="209c9-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="209c9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="209c9-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Predictix Ordering usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="209c9-136">In this section, you configure and test Azure AD single sign-on with Predictix Ordering based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="209c9-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Predictix ordinamento è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="209c9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Ordering is tooa user in Azure AD.</span></span> <span data-ttu-id="209c9-138">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello Predictix ordinamento richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="209c9-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Ordering needs toobe established.</span></span>

<span data-ttu-id="209c9-139">In ordinamento Predictix, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="209c9-139">In Predictix Ordering, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="209c9-140">tooconfigure e prova AD Azure single sign-on con Predictix ordinamento, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="209c9-140">tooconfigure and test Azure AD single sign-on with Predictix Ordering, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="209c9-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="209c9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="209c9-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="209c9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="209c9-143">**[Creare un utente test ordinamento Predictix](#create-a-predictix-ordering-test-user)**  -toohave un equivalente di Britta Simon Predictix ordinamento che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="209c9-143">**[Create a Predictix Ordering test user](#create-a-predictix-ordering-test-user)** - toohave a counterpart of Britta Simon in Predictix Ordering that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="209c9-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="209c9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="209c9-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="209c9-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="209c9-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="209c9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="209c9-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Predictix ordinamento.</span><span class="sxs-lookup"><span data-stu-id="209c9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Ordering application.</span></span>

<span data-ttu-id="209c9-148">**Azure AD tooconfigure single sign-on con Predictix ordinamento, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="209c9-148">**tooconfigure Azure AD single sign-on with Predictix Ordering, perform hello following steps:**</span></span>

1. <span data-ttu-id="209c9-149">Nel portale di Azure su hello hello **Predictix ordinamento** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="209c9-149">In hello Azure portal, on hello **Predictix Ordering** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="209c9-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="209c9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_samlbase.png)

3. <span data-ttu-id="209c9-153">In hello **Predictix ordinamento dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="209c9-153">On hello **Predictix Ordering Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Predictix Ordering](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_url.png)

    <span data-ttu-id="209c9-155">a.</span><span class="sxs-lookup"><span data-stu-id="209c9-155">a.</span></span> <span data-ttu-id="209c9-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname-pricing>.ordering.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="209c9-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.ordering.predictix.com/sso/request`</span></span>

    <span data-ttu-id="209c9-157">b.</span><span class="sxs-lookup"><span data-stu-id="209c9-157">b.</span></span> <span data-ttu-id="209c9-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="209c9-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<companyname-pricing>.dev.ordering.predictix.com` |
    | `https://<companyname-pricing>.ordering.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="209c9-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="209c9-159">These values are not real.</span></span> <span data-ttu-id="209c9-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="209c9-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="209c9-161">Contatto [team di supporto Client di ordinamento Predictix](https://www.predix.io/support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="209c9-161">Contact [Predictix Ordering Client support team](https://www.predix.io/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="209c9-162">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="209c9-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_certificate.png) 

5. <span data-ttu-id="209c9-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="209c9-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-predictixordering-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="209c9-166">In hello **Predictix ordinamento configurazione** fare clic su **configurare ordinamento Predictix** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="209c9-166">On hello **Predictix Ordering Configuration** section, click **Configure Predictix Ordering** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="209c9-167">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="209c9-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Predictix Ordering](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_configure.png) 

7. <span data-ttu-id="209c9-169">tooconfigure single sign-on sul **Predictix ordinamento** lato, è necessario hello toosend scaricato **certificato (Base64)**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL**  troppo[Predictix ordinamento team di supporto](https://www.predix.io/support/).</span><span class="sxs-lookup"><span data-stu-id="209c9-169">tooconfigure single sign-on on **Predictix Ordering** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Ordering support team](https://www.predix.io/support/).</span></span> <span data-ttu-id="209c9-170">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="209c9-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="209c9-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="209c9-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="209c9-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="209c9-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="209c9-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="209c9-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="209c9-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="209c9-174">Create an Azure AD test user</span></span>
<span data-ttu-id="209c9-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="209c9-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="209c9-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="209c9-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="209c9-178">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="209c9-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="209c9-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="209c9-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="209c9-182">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="209c9-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="209c9-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="209c9-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_04.png)

   <span data-ttu-id="209c9-186">a.</span><span class="sxs-lookup"><span data-stu-id="209c9-186">a.</span></span> <span data-ttu-id="209c9-187">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="209c9-187">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="209c9-188">b.</span><span class="sxs-lookup"><span data-stu-id="209c9-188">b.</span></span> <span data-ttu-id="209c9-189">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="209c9-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="209c9-190">c.</span><span class="sxs-lookup"><span data-stu-id="209c9-190">c.</span></span> <span data-ttu-id="209c9-191">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="209c9-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="209c9-192">d.</span><span class="sxs-lookup"><span data-stu-id="209c9-192">d.</span></span> <span data-ttu-id="209c9-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="209c9-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-ordering-test-user"></a><span data-ttu-id="209c9-194">Creare un utente di test di Predictix Ordering</span><span class="sxs-lookup"><span data-stu-id="209c9-194">Create a Predictix Ordering test user</span></span>

<span data-ttu-id="209c9-195">In questa sezione viene creato un utente di nome Britta Simon in Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="209c9-195">In this section, you create a user called Britta Simon in Predictix Ordering.</span></span> <span data-ttu-id="209c9-196">Lavorare con [Predictix ordinamento team di supporto](https://www.predix.io/support/) utenti hello tooadd nella piattaforma Predictix ordinamento hello.</span><span class="sxs-lookup"><span data-stu-id="209c9-196">Work with [Predictix Ordering support team](https://www.predix.io/support/) tooadd hello users in hello Predictix Ordering platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="209c9-197">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="209c9-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="209c9-198">In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accesso tooPredictix ordinamento.</span><span class="sxs-lookup"><span data-stu-id="209c9-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Ordering.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="209c9-200">**tooassign Britta Simon tooPredictix ordinamento, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="209c9-200">**tooassign Britta Simon tooPredictix Ordering, perform hello following steps:**</span></span>

1. <span data-ttu-id="209c9-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="209c9-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="209c9-203">Nell'elenco di applicazioni hello, selezionare **Predictix ordinamento**.</span><span class="sxs-lookup"><span data-stu-id="209c9-203">In hello applications list, select **Predictix Ordering**.</span></span>

    ![collegamento Predictix ordinamento Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_app.png)  

3. <span data-ttu-id="209c9-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="209c9-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="209c9-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="209c9-207">Click **Add** button.</span></span> <span data-ttu-id="209c9-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="209c9-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="209c9-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="209c9-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="209c9-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="209c9-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="209c9-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="209c9-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="209c9-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="209c9-213">Test single sign-on</span></span>

<span data-ttu-id="209c9-214">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="209c9-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="209c9-215">Quando si fa clic su riquadro Predictix ordinamento hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Predictix ordinamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="209c9-215">When you click hello Predictix Ordering tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Ordering application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="209c9-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="209c9-216">Additional resources</span></span>

* [<span data-ttu-id="209c9-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="209c9-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="209c9-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="209c9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_203.png


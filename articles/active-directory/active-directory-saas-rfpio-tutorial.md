---
title: 'Esercitazione: Integrazione di Azure Active Directory con RFPIO | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="07edb-103">Esercitazione: Integrazione di Azure Active Directory con RFPIO</span><span class="sxs-lookup"><span data-stu-id="07edb-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="07edb-104">In questa esercitazione, è illustrato come toointegrate RFPIO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07edb-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07edb-105">Integrazione RFPIO con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="07edb-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="07edb-106">È possibile controllare che in Azure AD che ha accesso tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="07edb-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="07edb-107">È possibile abilitare l'utenti tooautomatically get connesso tooRFPIO (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07edb-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="07edb-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07edb-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="07edb-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07edb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07edb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="07edb-110">Prerequisites</span></span>

<span data-ttu-id="07edb-111">integrazione di Azure AD con RFPIO tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="07edb-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="07edb-112">Una sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07edb-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="07edb-113">Sottoscrizione RFPIO abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="07edb-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="07edb-114">Non è consigliabile utilizzare una procedura di produzione ambiente tootest hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="07edb-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="07edb-115">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="07edb-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="07edb-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="07edb-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="07edb-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07edb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07edb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="07edb-118">Scenario description</span></span>
<span data-ttu-id="07edb-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="07edb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07edb-120">scenario di Hello descritta in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="07edb-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07edb-121">Aggiunta di RFPIO dalla raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="07edb-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="07edb-122">Configurazione e test dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07edb-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="07edb-123">Aggiungere RFPIO dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="07edb-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="07edb-124">integrazione hello tooconfigure di RFPIO in Azure AD, è necessario tooadd RFPIO dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="07edb-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="07edb-125">tooadd RFPIO dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="07edb-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="07edb-126">In hello  **[portale di Azure](https://portal.azure.com)**, nel riquadro di spostamento a sinistra di hello, selezionare hello **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="07edb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07edb-128">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07edb-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="07edb-130">tooadd una nuova applicazione, seleziona hello **nuova applicazione** pulsante nella parte superiore di hello nella finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="07edb-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="07edb-132">Nella casella di ricerca hello, digitare **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="07edb-132">In hello search box, type **RFPIO**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="07edb-134">Nel riquadro dei risultati hello, selezionare **RFPIO**, quindi selezionare hello **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="07edb-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="07edb-136">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07edb-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="07edb-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RFPIO in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="07edb-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07edb-138">Per toowork di accesso singolo, Azure AD deve tooknow relazioni hello sono compreso tra l'utente corrispondente in RFPIO e un utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07edb-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="07edb-139">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in RFPIO deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="07edb-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="07edb-140">In RFPIO, assegnare il valore di hello del **nome utente** in Azure AD come valore hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="07edb-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="07edb-141">tooconfigure e prova AD Azure single sign-on con RFPIO, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="07edb-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="07edb-142">**[Configurare Azure Active Directory Single Sign-On](#configuring-azure-ad-single-sign-on)**- tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="07edb-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="07edb-143">**[Creare un utente prova AD Azure](#creating-an-azure-ad-test-user)**-tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07edb-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07edb-144">**[Creare un utente test RFPIO](#creating-a-rfpio-test-user)**  - toohave un equivalente di Britta Simon in RFPIO che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="07edb-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="07edb-145">**[Assegnare l'utente test hello Azure AD](#assigning-the-azure-ad-test-user)**- tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="07edb-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07edb-146">**[Testare Single Sign-On](#testing-single-sign-on)**  - tooverify se configurazione hello funziona.</span><span class="sxs-lookup"><span data-stu-id="07edb-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="07edb-147">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07edb-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="07edb-148">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione RFPIO.</span><span class="sxs-lookup"><span data-stu-id="07edb-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="07edb-149">**Azure AD tooconfigure single sign-on con RFPIO, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07edb-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="07edb-150">Nel portale di Azure su hello hello **RFPIO** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="07edb-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="07edb-152">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="07edb-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="07edb-154">In hello **RFPIO dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="07edb-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="07edb-156">a.</span><span class="sxs-lookup"><span data-stu-id="07edb-156">a.</span></span> <span data-ttu-id="07edb-157">In hello **identificatore** casella di testo, digitare l'URL hello:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="07edb-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="07edb-159">b.</span><span class="sxs-lookup"><span data-stu-id="07edb-159">b.</span></span> <span data-ttu-id="07edb-160">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="07edb-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="07edb-161">c.</span><span class="sxs-lookup"><span data-stu-id="07edb-161">c.</span></span> <span data-ttu-id="07edb-162">In hello **stato inoltro** casella di testo immettere un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="07edb-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="07edb-163">Contatto [team di supporto RFPIO](https://www.rfpio.com/contact/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="07edb-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="07edb-164">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="07edb-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="07edb-165">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="07edb-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="07edb-167">In hello **URL di accesso** casella di testo, digitare l'URL hello:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="07edb-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="07edb-168">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="07edb-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="07edb-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="07edb-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="07edb-172">In una finestra del web browser, account di accesso toohello **RFPIO** sito Web come amministratore.</span><span class="sxs-lookup"><span data-stu-id="07edb-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="07edb-173">Fare clic sull'elenco a discesa di hello in basso a sinistra.</span><span class="sxs-lookup"><span data-stu-id="07edb-173">Click on hello bottom left corner dropdown.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="07edb-175">Fare clic su hello **impostazioni organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="07edb-175">Click on hello **Organization Settings**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="07edb-177">Fare clic su hello **funzionalità & integrazione**.</span><span class="sxs-lookup"><span data-stu-id="07edb-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="07edb-179">In hello **SAML SSO Configuration** fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="07edb-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="07edb-181">In questa sezione eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="07edb-181">In this Section perform following actions:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="07edb-183">a.</span><span class="sxs-lookup"><span data-stu-id="07edb-183">a.</span></span> <span data-ttu-id="07edb-184">Copiare il contenuto di hello di hello **XML di metadati scaricato** e incollarlo in hello **la configurazione dell'identità** campo.</span><span class="sxs-lookup"><span data-stu-id="07edb-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="07edb-185">scaricato hello toocopy contenuto di **Metadata XML** utilizzare **blocco note + +** o corretto **Editor XML**.</span><span class="sxs-lookup"><span data-stu-id="07edb-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="07edb-186">b.</span><span class="sxs-lookup"><span data-stu-id="07edb-186">b.</span></span> <span data-ttu-id="07edb-187">Fare clic su **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="07edb-187">Click **Validate**.</span></span>

    <span data-ttu-id="07edb-188">c.</span><span class="sxs-lookup"><span data-stu-id="07edb-188">c.</span></span> <span data-ttu-id="07edb-189">Dopo la selezione **convalida**, capovolgimento **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="07edb-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="07edb-190">d.</span><span class="sxs-lookup"><span data-stu-id="07edb-190">d.</span></span> <span data-ttu-id="07edb-191">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="07edb-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="07edb-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="07edb-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="07edb-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="07edb-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="07edb-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07edb-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="07edb-195">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07edb-195">Create an Azure AD test user</span></span>
<span data-ttu-id="07edb-196">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="07edb-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="07edb-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07edb-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="07edb-199">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="07edb-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07edb-201">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="07edb-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07edb-203">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="07edb-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07edb-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="07edb-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07edb-207">a.</span><span class="sxs-lookup"><span data-stu-id="07edb-207">a.</span></span> <span data-ttu-id="07edb-208">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07edb-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07edb-209">b.</span><span class="sxs-lookup"><span data-stu-id="07edb-209">b.</span></span> <span data-ttu-id="07edb-210">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="07edb-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07edb-211">c.</span><span class="sxs-lookup"><span data-stu-id="07edb-211">c.</span></span> <span data-ttu-id="07edb-212">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="07edb-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="07edb-213">d.</span><span class="sxs-lookup"><span data-stu-id="07edb-213">d.</span></span> <span data-ttu-id="07edb-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="07edb-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="07edb-215">Creare un utente di test di RFPIO</span><span class="sxs-lookup"><span data-stu-id="07edb-215">Create a RFPIO test user</span></span>

<span data-ttu-id="07edb-216">toolog agli utenti di Azure AD tooenable in tooRFPIO, è necessario eseguirne il provisioning in RFPIO.</span><span class="sxs-lookup"><span data-stu-id="07edb-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="07edb-217">Nel caso di hello di RFPIO, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="07edb-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="07edb-218">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07edb-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="07edb-219">Accedi tooyour sito della società RFPIO come amministratore.</span><span class="sxs-lookup"><span data-stu-id="07edb-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="07edb-220">Fare clic sull'elenco a discesa di hello in basso a sinistra.</span><span class="sxs-lookup"><span data-stu-id="07edb-220">Click on hello bottom left corner dropdown.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="07edb-222">Fare clic su hello **impostazioni organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="07edb-222">Click on hello **Organization Settings**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="07edb-224">Fare clic su **MEMBRI DEL TEAM**.</span><span class="sxs-lookup"><span data-stu-id="07edb-224">Click **TEAM MEMBERS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="07edb-226">Fare clic su **AGGIUNGI MEMBRI**.</span><span class="sxs-lookup"><span data-stu-id="07edb-226">Click on **ADD MEMBERS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="07edb-228">In hello **aggiungere nuovi membri** sezione.</span><span class="sxs-lookup"><span data-stu-id="07edb-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="07edb-229">eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="07edb-229">Perform following actions:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="07edb-231">a.</span><span class="sxs-lookup"><span data-stu-id="07edb-231">a.</span></span> <span data-ttu-id="07edb-232">Invio **indirizzo di posta elettronica** in hello **immettere un messaggio di posta elettronica per ogni riga** campo.</span><span class="sxs-lookup"><span data-stu-id="07edb-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="07edb-233">b.</span><span class="sxs-lookup"><span data-stu-id="07edb-233">b.</span></span> <span data-ttu-id="07edb-234">Selezionare il **ruolo** in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="07edb-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="07edb-235">c.</span><span class="sxs-lookup"><span data-stu-id="07edb-235">c.</span></span> <span data-ttu-id="07edb-236">Fare clic su **AGGIUNGI MEMBRI**.</span><span class="sxs-lookup"><span data-stu-id="07edb-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="07edb-237">titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="07edb-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="07edb-238">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="07edb-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="07edb-239">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="07edb-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Assegna utente][200] 

<span data-ttu-id="07edb-241">**tooassign Britta Simon tooRFPIO, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="07edb-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="07edb-242">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07edb-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="07edb-244">Nell'elenco di applicazioni hello, selezionare **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="07edb-244">In hello applications list, select **RFPIO**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="07edb-246">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07edb-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="07edb-248">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="07edb-248">Click **Add** button.</span></span> <span data-ttu-id="07edb-249">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07edb-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="07edb-251">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="07edb-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="07edb-252">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07edb-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07edb-253">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="07edb-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="07edb-254">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07edb-254">Test single sign-on</span></span>

<span data-ttu-id="07edb-255">In questa sezione Configurazione di Azure AD single sign-on utilizzare test hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="07edb-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="07edb-256">Quando si fa clic hello RFPIO riquadro in hello Pannello di accesso, è necessario ottenere applicazione RFPIO tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="07edb-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="07edb-257">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07edb-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07edb-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="07edb-258">Additional resources</span></span>

* [<span data-ttu-id="07edb-259">Elenco di esercitazioni sulla toointegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07edb-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07edb-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07edb-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png


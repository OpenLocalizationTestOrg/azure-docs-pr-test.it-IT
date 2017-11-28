---
title: 'Esercitazione: Integrazione di Azure Active Directory con IBM Kenexa Survey Enterprise | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e IBM Kenexa sondaggio Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="4a26a-103">Esercitazione: Integrazione di Azure Active Directory con IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="4a26a-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="4a26a-104">In questa esercitazione, è illustrato come toointegrate IBM Kenexa sondaggio Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a26a-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a26a-105">Integrazione di IBM Kenexa sondaggio Enterprise con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4a26a-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a26a-106">È possibile controllare in Azure AD che ha accesso tooIBM Kenexa sondaggio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4a26a-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="4a26a-107">È possibile abilitare l'accesso agli utenti tooautomatically tooIBM Kenexa sondaggio Enterprise single sign-on (SSO) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a26a-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4a26a-108">È possibile gestire gli account in un'unica posizione centrale: hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a26a-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="4a26a-109">Se si desidera tooknow informazioni sul software come una servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a26a-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a26a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4a26a-110">Prerequisites</span></span>

<span data-ttu-id="4a26a-111">integrazione di Azure AD con IBM Kenexa sondaggio Enterprise tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4a26a-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="4a26a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a26a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a26a-113">Una sottoscrizione IBM Kenexa Survey Enterprise abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="4a26a-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a26a-114">Quando si testano passaggi hello in questa esercitazione, è consigliabile non utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4a26a-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="4a26a-115">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="4a26a-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="4a26a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4a26a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a26a-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a26a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a26a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4a26a-118">Scenario description</span></span>
<span data-ttu-id="4a26a-119">In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4a26a-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="4a26a-120">scenario di Hello descritto nell'esercitazione hello è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4a26a-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="4a26a-121">Aggiunta di IBM Kenexa sondaggio Enterprise dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4a26a-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="4a26a-122">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a26a-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="4a26a-123">Aggiungere IBM Kenexa sondaggio Enterprise dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="4a26a-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="4a26a-124">integrazione di hello tooconfigure di IBM Kenexa sondaggio Enterprise in Azure AD, aggiungere IBM Kenexa sondaggio Enterprise hello raccolta tooyour elenco di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4a26a-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a26a-125">tooadd IBM Kenexa sondaggio Enterprise dalla raccolta di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a26a-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="4a26a-126">In hello [portale di Azure](https://portal.azure.com)in hello riquadro sinistro, fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4a26a-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="4a26a-128">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="4a26a-130">tooadd un'applicazione, fare clic su hello **nuova applicazione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4a26a-130">tooadd an application, click hello **New application** button.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="4a26a-132">Nella casella di ricerca hello, digitare **IBM Kenexa sondaggio Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="4a26a-134">Selezionare dall'elenco risultati hello **IBM Kenexa sondaggio Enterprise**, quindi fare clic su hello **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4a26a-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa sondaggio aziendale nell'elenco risultati hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4a26a-136">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a26a-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4a26a-137">In questa sezione viene configurato e testato l'accesso SSO di Azure AD con IBM Kenexa Survey Enterprise con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4a26a-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4a26a-138">Per toowork SSO, Azure AD deve controparte di tooidentify hello IBM Kenexa sondaggio Enterprise utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a26a-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="4a26a-139">In altre parole, Azure AD deve stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4a26a-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="4a26a-140">relazione di collegamento hello tooestablish, assegnare un valore di hello hello **nome utente** in IBM Kenexa sondaggio Enterprise come valore di hello di hello **Username** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a26a-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="4a26a-141">tooconfigure e SSO AD Azure con IBM Kenexa sondaggio Enterprise, completo di test hello blocchi predefiniti di hello nelle due sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="4a26a-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="4a26a-142">Configurare l'accesso SSO di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a26a-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="4a26a-143">In questa sezione abilitare SSO AD Azure nel portale di Azure hello e configurare SSO nell'applicazione IBM Kenexa sondaggio Enterprise eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a26a-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="4a26a-144">Nel portale di Azure su hello hello **IBM Kenexa sondaggio Enterprise** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa Survey Enterprise Configurazione collegamento Single Sign-On][4]

2. <span data-ttu-id="4a26a-146">In hello **Single sign-on** della finestra di dialogo hello **modalità** , quindi selezionare **basato su SAML Sign-on** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="4a26a-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="4a26a-148">In hello **IBM Kenexa sondaggio Enterprise dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4a26a-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="4a26a-150">a.</span><span class="sxs-lookup"><span data-stu-id="4a26a-150">a.</span></span> <span data-ttu-id="4a26a-151">In hello **identificatore** casella di testo, digitare un URL con hello seguente motivo:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="4a26a-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="4a26a-152">b.</span><span class="sxs-lookup"><span data-stu-id="4a26a-152">b.</span></span> <span data-ttu-id="4a26a-153">In hello **URL di risposta** casella di testo, digitare un URL con hello seguente motivo:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="4a26a-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a26a-154">Hello valori precedenti non sono reali.</span><span class="sxs-lookup"><span data-stu-id="4a26a-154">hello preceding values are not real.</span></span> <span data-ttu-id="4a26a-155">Aggiornarli con identificatore effettivo hello e URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="4a26a-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="4a26a-156">i valori effettivi, hello contatto di hello tooobtain [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="4a26a-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="4a26a-157">In **certificato di firma SAML**, fare clic su **certificato (Base64)**e quindi salvare computer tooyour file certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="4a26a-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![collegamento al download del certificato (Base64) Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="4a26a-159">applicazione aziendale di sondaggio Kenexa IBM Hello prevede le asserzioni di sicurezza asserzioni Markup Language (SAML) hello tooreceive in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping toohello degli attributi token SAML.</span><span class="sxs-lookup"><span data-stu-id="4a26a-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="4a26a-160">Hello valore dell'attestazione utente identificatore hello in risposta hello deve corrispondere hello ID SSO configurato nel sistema Kenexa hello.</span><span class="sxs-lookup"><span data-stu-id="4a26a-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="4a26a-161">toomap hello identificatore utente appropriato all'interno dell'organizzazione come SSO Internet Datagram Protocol (IDP), il lavoro con hello [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="4a26a-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="4a26a-162">Per impostazione predefinita, Azure AD imposta l'identificatore utente hello come valore del nome principale (UPN) utente hello.</span><span class="sxs-lookup"><span data-stu-id="4a26a-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="4a26a-163">È possibile modificare questo valore su hello **attributo** scheda, come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="4a26a-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="4a26a-164">integrazione di Hello funziona solo dopo aver completato correttamente il mapping di hello.</span><span class="sxs-lookup"><span data-stu-id="4a26a-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![finestra di dialogo attributi di utente Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="4a26a-166">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-166">Click **Save**.</span></span>

    ![Hello configurare single sign-on pulsante Salva](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a26a-168">hello tooopen **Configura sign-on** finestra, in **IBM Kenexa sondaggio Enterprise configurazione**, fare clic su **configurare IBM Kenexa sondaggio Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![collegamento di Hello configurare IBM Kenexa sondaggio Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="4a26a-170">Hello copia **Sign-Out URL**, **ID entità SAML**, e **SAML single sign-on Service URL** valori hello **riferimento rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="4a26a-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="4a26a-171">In hello **Configura sign-on** finestra, in **riferimento rapido**, hello copia **Sign-Out URL**, **ID entità SAML**, e  **SAML single sign-on Service URL** valori.</span><span class="sxs-lookup"><span data-stu-id="4a26a-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="4a26a-172">tooconfigure SSO su hello **IBM Kenexa sondaggio Enterprise** sul lato, inviare hello scaricato **certificato (Base64)**, **Sign-Out URL**, **ID entità SAML**, e **SAML single sign-on Service URL** valori toohello [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="4a26a-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="4a26a-173">È possibile fare riferimento tooa versione concisa di queste istruzioni in hello [portale di Azure](https://portal.azure.com) mentre si stanno impostando app hello.</span><span class="sxs-lookup"><span data-stu-id="4a26a-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="4a26a-174">Dopo aver aggiunto l'applicazione hello da hello **Active Directory** > **applicazioni aziendali** fare semplicemente clic su hello **accesso single sign-on** scheda e quindi accedere Hello incorporato documentazione tramite hello **configurazione** sezione alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="4a26a-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="4a26a-175">toolearn più feature hello documentazione incorporati, vedere [AD Azure incorporato documentazione](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="4a26a-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4a26a-176">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a26a-176">Create an Azure AD test user</span></span>
<span data-ttu-id="4a26a-177">In questa sezione è creare utente test Britta Simon nel portale di Azure hello eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a26a-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Creare un utente test di Azure AD][100]

1. <span data-ttu-id="4a26a-179">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4a26a-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a26a-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a26a-183">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4a26a-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a26a-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4a26a-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a26a-187">a.</span><span class="sxs-lookup"><span data-stu-id="4a26a-187">a.</span></span> <span data-ttu-id="4a26a-188">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a26a-189">b.</span><span class="sxs-lookup"><span data-stu-id="4a26a-189">b.</span></span> <span data-ttu-id="4a26a-190">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a26a-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4a26a-191">c.</span><span class="sxs-lookup"><span data-stu-id="4a26a-191">c.</span></span> <span data-ttu-id="4a26a-192">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="4a26a-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4a26a-193">d.</span><span class="sxs-lookup"><span data-stu-id="4a26a-193">d.</span></span> <span data-ttu-id="4a26a-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="4a26a-195">Creare un utente test di IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="4a26a-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="4a26a-196">In questa sezione viene creato un utente chiamato Britta Simon in IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4a26a-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="4a26a-197">utenti toocreate hello sistema IBM Kenexa sondaggio Enterprise e hello mappa ID SSO per essi, è possibile utilizzare hello [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="4a26a-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="4a26a-198">Il valore dell'ID di SSO deve inoltre essere eseguito il mapping di valore dell'identificatore utente toohello da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a26a-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="4a26a-199">È possibile modificare questa impostazione predefinita su hello **attributo** scheda.</span><span class="sxs-lookup"><span data-stu-id="4a26a-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4a26a-200">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a26a-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4a26a-201">In questa sezione per abilitare utente Britta Simon toouse SSO Azure concessione dell'accesso tooIBM Kenexa sondaggio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4a26a-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="4a26a-203">utente tooassign tooIBM Britta Simon Kenexa sondaggio Enterprise, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a26a-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="4a26a-204">Nel portale di Azure hello, aprire hello **applicazioni** visualizzare, andare toohello **Directory** visualizzazione, selezionare **applicazioni aziendali**, quindi fare clic su **tutti applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Hello "applicazioni aziendali" e i collegamenti di "Tutte le applicazioni"][201] 

2. <span data-ttu-id="4a26a-206">In hello **applicazioni** elenco, selezionare **IBM Kenexa sondaggio Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![collegamento a IBM Kenexa sondaggio Enterprise Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="4a26a-208">Nel riquadro di sinistra hello, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-208">In hello left pane, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="4a26a-210">Fare clic su hello **Aggiungi** pulsante e quindi nel hello **Aggiungi** riquadro, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="4a26a-212">In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4a26a-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="4a26a-213">In hello **utenti e gruppi** finestra di dialogo fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4a26a-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="4a26a-214">In hello **Aggiungi** finestra di dialogo fare clic su hello **assegnare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4a26a-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4a26a-215">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4a26a-215">Test single sign-on</span></span>

<span data-ttu-id="4a26a-216">In questa sezione verificare la configurazione di SSO AD Azure tramite hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4a26a-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="4a26a-217">Quando si fa clic su hello **IBM Kenexa sondaggio Enterprise** hello di riquadro nel Pannello di accesso, è necessario essere connessi automaticamente tooyour applicazione aziendale di sondaggio Kenexa IBM.</span><span class="sxs-lookup"><span data-stu-id="4a26a-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a26a-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4a26a-218">Additional resources</span></span>

* [<span data-ttu-id="4a26a-219">Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a26a-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a26a-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a26a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 

---
title: 'Esercitazione: Integrazione di Azure Active Directory con Autotask Workplace | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Autotask all'area di lavoro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="7620d-103">Esercitazione: Integrazione di Azure Active Directory con Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="7620d-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="7620d-104">In questa esercitazione, è illustrato come toointegrate Autotask all'area di lavoro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7620d-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7620d-105">Integrazione Autotask all'area di lavoro con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="7620d-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7620d-106">È possibile controllare in Azure AD che ha accesso tooAutotask all'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="7620d-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="7620d-107">È possibile abilitare l'utenti tooautomatically get connesso tooAutotask all'area di lavoro (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7620d-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7620d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7620d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7620d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7620d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7620d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7620d-110">Prerequisites</span></span>

<span data-ttu-id="7620d-111">tooconfigure integrazione di Azure AD con Autotask all'area di lavoro, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7620d-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="7620d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7620d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7620d-113">Sottoscrizione di Autotask Workplace abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7620d-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="7620d-114">È necessario essere un amministratore o un amministratore con privilegi avanzati in Workplace.</span><span class="sxs-lookup"><span data-stu-id="7620d-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="7620d-115">È necessario un account amministratore hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7620d-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="7620d-116">utenti Hello che utilizzano questa funzionalità devono avere un account all'interno di hello Azure AD e luogo di lavoro e i relativi indirizzi di posta elettronica per entrambi devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="7620d-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="7620d-117">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="7620d-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7620d-118">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="7620d-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7620d-119">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7620d-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7620d-120">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7620d-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7620d-121">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7620d-121">Scenario description</span></span>
<span data-ttu-id="7620d-122">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7620d-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7620d-123">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="7620d-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7620d-124">Aggiunta all'area di lavoro Autotask dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7620d-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="7620d-125">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7620d-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="7620d-126">Aggiunta all'area di lavoro Autotask dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7620d-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="7620d-127">integrazione hello tooconfigure di Autotask all'area di lavoro in Azure AD, è necessario tooadd Autotask all'area di lavoro dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7620d-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7620d-128">**tooadd Autotask all'area di lavoro Raccolta hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7620d-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7620d-129">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7620d-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="7620d-131">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7620d-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7620d-132">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7620d-132">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="7620d-134">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7620d-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="7620d-136">Nella casella di ricerca hello, digitare **Autotask all'area di lavoro**selezionare **Autotask all'area di lavoro** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7620d-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco dei risultati Autotask all'area di lavoro in hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7620d-138">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7620d-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7620d-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Autotask Workplace usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7620d-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7620d-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nell'area di lavoro Autotask è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7620d-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="7620d-141">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nell'area di lavoro Autotask deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="7620d-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="7620d-142">Nell'area di lavoro Autotask, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="7620d-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7620d-143">tooconfigure e prova AD Azure single sign-on con Autotask all'area di lavoro, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7620d-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7620d-144">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7620d-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7620d-145">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7620d-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7620d-146">**[Creare un utente di test all'area di lavoro Autotask](#create-an-autotask-workplace-test-user)**  -toohave un equivalente di Britta Simon Autotask area di lavoro che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7620d-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7620d-147">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7620d-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7620d-148">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="7620d-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7620d-149">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7620d-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7620d-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Autotask all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7620d-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="7620d-151">**Azure AD tooconfigure single sign-on con Autotask all'area di lavoro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7620d-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7620d-152">Nel portale di Azure su hello hello **Autotask all'area di lavoro** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7620d-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="7620d-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7620d-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="7620d-156">Se si desidera un'applicazione hello tooconfigure in **IDP** , modalità iniziata da eseguire hello seguendo i passaggi hello **Autotask all'area di lavoro dominio e gli URL** sezione:</span><span class="sxs-lookup"><span data-stu-id="7620d-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Autotask Workplace per IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="7620d-158">a.</span><span class="sxs-lookup"><span data-stu-id="7620d-158">a.</span></span> <span data-ttu-id="7620d-159">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="7620d-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="7620d-160">b.</span><span class="sxs-lookup"><span data-stu-id="7620d-160">b.</span></span> <span data-ttu-id="7620d-161">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="7620d-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="7620d-162">Se si desidera in un'applicazione hello tooconfigure **SP** modalità avviata, controllo **Mostra URL impostazioni avanzate** ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7620d-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Autotask Workplace per SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="7620d-164">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="7620d-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7620d-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="7620d-165">These values are not real.</span></span> <span data-ttu-id="7620d-166">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7620d-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7620d-167">Contatto [team di supporto Client all'area di lavoro Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="7620d-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="7620d-168">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="7620d-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="7620d-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7620d-170">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7620d-172">In una finestra del web browser, l'accesso utilizzando Online tooWorkplace hello le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="7620d-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="7620d-173">Quando si configura hello IdP, un sottodominio sarà necessario toobe specificato.</span><span class="sxs-lookup"><span data-stu-id="7620d-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="7620d-174">tooconfirm hello corretto sottodominio tooWorkplace accesso Online.</span><span class="sxs-lookup"><span data-stu-id="7620d-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="7620d-175">Una volta effettuato l'accesso, è possibile apportare sottodominio toohello nota in hello URL.</span><span class="sxs-lookup"><span data-stu-id="7620d-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="7620d-176">sottodominio Hello fa parte di hello tra hello "https://" e ".awp.autotask.net/" e deve essere Stati Uniti, Europa, autorità di certificazione o Australia.</span><span class="sxs-lookup"><span data-stu-id="7620d-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="7620d-177">Andare troppo**configurazione** > **Single Sign-On** ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7620d-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Configurazione Single Sign-On per Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="7620d-179">a.</span><span class="sxs-lookup"><span data-stu-id="7620d-179">a.</span></span> <span data-ttu-id="7620d-180">Seleziona hello **File di metadati XML** opzione e quindi caricare hello **Metadata XML** scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7620d-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="7620d-181">b.</span><span class="sxs-lookup"><span data-stu-id="7620d-181">b.</span></span> <span data-ttu-id="7620d-182">Fare clic su **Enable SSO** (Abilita SSO).</span><span class="sxs-lookup"><span data-stu-id="7620d-182">Click **Enable SSO**.</span></span>
    
    ![Approvazione della configurazione Single Sign-On per Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="7620d-184">c.</span><span class="sxs-lookup"><span data-stu-id="7620d-184">c.</span></span> <span data-ttu-id="7620d-185">Seleziona hello **verificare queste informazioni siano corrette e il provider di identità attendibili** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="7620d-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="7620d-186">d.</span><span class="sxs-lookup"><span data-stu-id="7620d-186">d.</span></span> <span data-ttu-id="7620d-187">Fare clic su **Approve** (Approva).</span><span class="sxs-lookup"><span data-stu-id="7620d-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="7620d-188">Se si richiede assistenza nella configurazione Autotask all'area di lavoro, vedere [questa pagina](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistenza con l'account aziendale.</span><span class="sxs-lookup"><span data-stu-id="7620d-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="7620d-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="7620d-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7620d-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="7620d-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7620d-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7620d-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7620d-192">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7620d-192">Create an Azure AD test user</span></span>

<span data-ttu-id="7620d-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7620d-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="7620d-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7620d-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7620d-196">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7620d-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7620d-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="7620d-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7620d-200">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7620d-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7620d-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7620d-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7620d-204">a.</span><span class="sxs-lookup"><span data-stu-id="7620d-204">a.</span></span> <span data-ttu-id="7620d-205">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7620d-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7620d-206">b.</span><span class="sxs-lookup"><span data-stu-id="7620d-206">b.</span></span> <span data-ttu-id="7620d-207">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7620d-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7620d-208">c.</span><span class="sxs-lookup"><span data-stu-id="7620d-208">c.</span></span> <span data-ttu-id="7620d-209">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="7620d-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7620d-210">d.</span><span class="sxs-lookup"><span data-stu-id="7620d-210">d.</span></span> <span data-ttu-id="7620d-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7620d-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="7620d-212">Creare un utente di test di Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="7620d-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="7620d-213">In questa sezione viene creato un utente di nome Britta Simon in Autotask.</span><span class="sxs-lookup"><span data-stu-id="7620d-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="7620d-214">Rivolgersi [team di supporto all'area di lavoro Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd utenti hello hello piattaforma Autotask all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7620d-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7620d-215">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7620d-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7620d-216">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAutotask all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7620d-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="7620d-218">**tooassign Britta Simon tooAutotask all'area di lavoro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7620d-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7620d-219">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7620d-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7620d-221">Nell'elenco di applicazioni hello, selezionare **Autotask all'area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="7620d-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![collegamento all'area di lavoro Autotask nell'elenco delle applicazioni hello Hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="7620d-223">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7620d-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="7620d-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7620d-225">Click **Add** button.</span></span> <span data-ttu-id="7620d-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7620d-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="7620d-228">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="7620d-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7620d-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7620d-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7620d-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7620d-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7620d-231">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7620d-231">Test single sign-on</span></span>

<span data-ttu-id="7620d-232">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7620d-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7620d-233">Quando si fa clic hello all'area di lavoro Autotask riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Autotask all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7620d-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="7620d-234">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7620d-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7620d-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7620d-235">Additional resources</span></span>

* [<span data-ttu-id="7620d-236">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7620d-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7620d-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7620d-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png


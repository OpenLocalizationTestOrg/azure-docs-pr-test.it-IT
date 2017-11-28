---
title: 'Esercitazione: Integrazione di Azure Active Directory con TargetProcess | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TargetProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="6343c-103">Esercitazione: Integrazione di Azure Active Directory con TargetProcess</span><span class="sxs-lookup"><span data-stu-id="6343c-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="6343c-104">In questa esercitazione, è illustrato come toointegrate TargetProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6343c-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6343c-105">Integrazione TargetProcess con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6343c-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6343c-106">È possibile controllare in Azure AD che ha accesso tooTargetProcess</span><span class="sxs-lookup"><span data-stu-id="6343c-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="6343c-107">È possibile abilitare l'utenti tooautomatically get connesso tooTargetProcess (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6343c-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6343c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6343c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6343c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6343c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6343c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6343c-110">Prerequisites</span></span>

<span data-ttu-id="6343c-111">integrazione di Azure AD con TargetProcess tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6343c-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="6343c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6343c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6343c-113">Sottoscrizione di TargetProcess abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6343c-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6343c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6343c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6343c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6343c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6343c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6343c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6343c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6343c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6343c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6343c-118">Scenario description</span></span>
<span data-ttu-id="6343c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6343c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6343c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6343c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6343c-121">Aggiungere TargetProcess dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="6343c-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="6343c-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6343c-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="6343c-123">Aggiungere TargetProcess dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="6343c-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="6343c-124">integrazione hello tooconfigure di TargetProcess in Azure AD, è necessario tooadd TargetProcess dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6343c-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6343c-125">**tooadd TargetProcess dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6343c-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6343c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6343c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6343c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6343c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6343c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6343c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6343c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6343c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6343c-133">Nella casella di ricerca hello, digitare **TargetProcess**selezionare **TargetProcess** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6343c-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Aggiungere TargetProcess dalla raccolta](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6343c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6343c-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6343c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TargetProcess Online usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6343c-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6343c-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TargetProcess è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6343c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="6343c-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TargetProcess deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6343c-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="6343c-139">In TargetProcess, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6343c-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6343c-140">tooconfigure e prova AD Azure single sign-on con TargetProcess, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6343c-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6343c-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6343c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6343c-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6343c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6343c-143">**[Creare un utente test TargetProcess](#create-a-targetprocess-test-user)**  -toohave un equivalente di Britta Simon in TargetProcess che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6343c-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6343c-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6343c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6343c-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6343c-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6343c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6343c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6343c-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="6343c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="6343c-148">**Azure AD tooconfigure single sign-on con TargetProcess, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6343c-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="6343c-149">Nel portale di Azure su hello hello **TargetProcess** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6343c-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6343c-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6343c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="6343c-153">In hello **TargetProcess dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6343c-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Sezione URL e dominio TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="6343c-155">a.</span><span class="sxs-lookup"><span data-stu-id="6343c-155">a.</span></span> <span data-ttu-id="6343c-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="6343c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="6343c-157">b.</span><span class="sxs-lookup"><span data-stu-id="6343c-157">b.</span></span> <span data-ttu-id="6343c-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="6343c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6343c-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="6343c-159">These values are not real.</span></span> <span data-ttu-id="6343c-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="6343c-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6343c-161">Contatto [team di supporto TargetProcess Client](mailto:support@targetprocess.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="6343c-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="6343c-162">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6343c-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="6343c-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6343c-164">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6343c-166">In hello **TargetProcess configurazione** fare clic su **configurare TargetProcess** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="6343c-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6343c-167">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="6343c-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sezione di configurazione di TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="6343c-169">Sign-on tooyour TargetProcess applicazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6343c-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="6343c-170">Scegliere dal menu hello in primo piano hello **installazione**.</span><span class="sxs-lookup"><span data-stu-id="6343c-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Configurazione](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="6343c-172">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="6343c-172">Click **Settings**.</span></span>
   
    ![Impostazioni](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="6343c-174">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6343c-174">Click **Single Sign-on**.</span></span>
   
    ![fare clic su Single Sign-On](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="6343c-176">In hello Single Sign-on finestra di dialogo Impostazioni, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6343c-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="6343c-178">a.</span><span class="sxs-lookup"><span data-stu-id="6343c-178">a.</span></span> <span data-ttu-id="6343c-179">Fare clic su **Abilita Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6343c-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="6343c-180">b.</span><span class="sxs-lookup"><span data-stu-id="6343c-180">b.</span></span> <span data-ttu-id="6343c-181">In **Sign-on URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6343c-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6343c-182">c.</span><span class="sxs-lookup"><span data-stu-id="6343c-182">c.</span></span> <span data-ttu-id="6343c-183">Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="6343c-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="6343c-184">d.</span><span class="sxs-lookup"><span data-stu-id="6343c-184">d.</span></span> <span data-ttu-id="6343c-185">Fare clic su **Abilita Provisioning JIT**.</span><span class="sxs-lookup"><span data-stu-id="6343c-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="6343c-186">e.</span><span class="sxs-lookup"><span data-stu-id="6343c-186">e.</span></span> <span data-ttu-id="6343c-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6343c-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6343c-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6343c-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6343c-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6343c-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6343c-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6343c-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6343c-191">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6343c-191">Create an Azure AD test user</span></span>
<span data-ttu-id="6343c-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6343c-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6343c-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6343c-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6343c-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6343c-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6343c-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6343c-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![elenco di hello toodisplay degli utenti](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6343c-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6343c-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6343c-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6343c-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Sezione Utente](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6343c-203">a.</span><span class="sxs-lookup"><span data-stu-id="6343c-203">a.</span></span> <span data-ttu-id="6343c-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6343c-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6343c-205">b.</span><span class="sxs-lookup"><span data-stu-id="6343c-205">b.</span></span> <span data-ttu-id="6343c-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6343c-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6343c-207">c.</span><span class="sxs-lookup"><span data-stu-id="6343c-207">c.</span></span> <span data-ttu-id="6343c-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6343c-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6343c-209">d.</span><span class="sxs-lookup"><span data-stu-id="6343c-209">d.</span></span> <span data-ttu-id="6343c-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6343c-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="6343c-211">Creare un utente test per TargetProcess</span><span class="sxs-lookup"><span data-stu-id="6343c-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="6343c-212">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in TargetProcess toocreate.</span><span class="sxs-lookup"><span data-stu-id="6343c-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="6343c-213">TargetProcess supporta il provisioning JIT (just-in-time),</span><span class="sxs-lookup"><span data-stu-id="6343c-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="6343c-214">È già stato abilitato in [Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="6343c-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="6343c-215">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="6343c-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6343c-216">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6343c-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6343c-217">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTargetProcess.</span><span class="sxs-lookup"><span data-stu-id="6343c-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6343c-219">**tooassign Britta Simon tooTargetProcess, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6343c-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="6343c-220">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6343c-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6343c-222">Nell'elenco di applicazioni hello, selezionare **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="6343c-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess nell'elenco di app](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="6343c-224">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6343c-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6343c-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6343c-226">Click **Add** button.</span></span> <span data-ttu-id="6343c-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6343c-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6343c-229">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6343c-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6343c-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6343c-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6343c-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6343c-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6343c-232">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6343c-232">Test single sign-on</span></span>

<span data-ttu-id="6343c-233">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6343c-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6343c-234">Quando si fa clic hello TargetProcess riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour TargetProcess applicazione.</span><span class="sxs-lookup"><span data-stu-id="6343c-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="6343c-235">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6343c-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6343c-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6343c-236">Additional resources</span></span>

* [<span data-ttu-id="6343c-237">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6343c-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6343c-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6343c-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png


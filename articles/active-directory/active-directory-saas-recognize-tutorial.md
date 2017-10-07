---
title: 'Esercitazione: Integrazione di Azure Active Directory con Recognize | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e riconoscere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="68c16-103">Esercitazione: Integrazione di Azure Active Directory con Recognize</span><span class="sxs-lookup"><span data-stu-id="68c16-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="68c16-104">In questa esercitazione, è illustrato come toointegrate riconoscere con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68c16-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68c16-105">Riconoscere l'integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="68c16-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="68c16-106">È possibile controllare in Azure AD che ha accesso tooRecognize</span><span class="sxs-lookup"><span data-stu-id="68c16-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="68c16-107">È possibile abilitare l'utenti tooautomatically get connesso tooRecognize (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="68c16-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68c16-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="68c16-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="68c16-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68c16-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68c16-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="68c16-110">Prerequisites</span></span>

<span data-ttu-id="68c16-111">integrazione di Azure AD tooconfigure con riconoscere, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="68c16-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="68c16-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68c16-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68c16-113">Sottoscrizione di Recognize abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="68c16-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68c16-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="68c16-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68c16-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="68c16-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68c16-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="68c16-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68c16-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68c16-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68c16-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="68c16-118">Scenario description</span></span>
<span data-ttu-id="68c16-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="68c16-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68c16-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="68c16-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68c16-121">Aggiunta di riconoscere dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="68c16-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="68c16-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="68c16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="68c16-123">Aggiunta di riconoscere dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="68c16-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="68c16-124">integrazione hello tooconfigure di riconoscere in Azure AD, è necessario tooadd Riconosci dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="68c16-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="68c16-125">**tooadd Riconosci dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="68c16-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="68c16-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="68c16-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68c16-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="68c16-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="68c16-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="68c16-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="68c16-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="68c16-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="68c16-133">Nella casella di ricerca hello, digitare **Riconosci**.</span><span class="sxs-lookup"><span data-stu-id="68c16-133">In hello search box, type **Recognize**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="68c16-135">Nel riquadro dei risultati hello, selezionare **Riconosci**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="68c16-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68c16-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="68c16-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68c16-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Recognize in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="68c16-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="68c16-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Riconosci è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68c16-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="68c16-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello Riconosci deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="68c16-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="68c16-141">Nel riconoscere, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="68c16-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="68c16-142">tooconfigure e test di Azure AD accesso single sign-on con riconoscere, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="68c16-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="68c16-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="68c16-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="68c16-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68c16-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68c16-145">**[Creazione di un utente test Riconosci](#creating-a-recognize-test-user)**  -toohave un equivalente di Britta Simon nel riconoscere che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="68c16-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="68c16-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="68c16-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68c16-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="68c16-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68c16-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="68c16-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68c16-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Riconosci.</span><span class="sxs-lookup"><span data-stu-id="68c16-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="68c16-150">**Azure AD tooconfigure single sign-on con Riconosci, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="68c16-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="68c16-151">Nel portale di Azure su hello hello **Riconosci** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="68c16-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="68c16-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="68c16-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="68c16-155">In hello **riconoscere dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="68c16-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="68c16-157">a.</span><span class="sxs-lookup"><span data-stu-id="68c16-157">a.</span></span> <span data-ttu-id="68c16-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="68c16-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="68c16-159">b.</span><span class="sxs-lookup"><span data-stu-id="68c16-159">b.</span></span> <span data-ttu-id="68c16-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="68c16-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="68c16-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="68c16-161">These values are not real.</span></span> <span data-ttu-id="68c16-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="68c16-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="68c16-163">Contatto [team di supporto Client riconosce](mailto:support@recognizeapp.com) per ottenere l'URL Sign-On ed è possibile ottenere il valore di identificatore aprendo hello URL del servizio Provider di metadati da hello sezione Impostazioni SSO descritto più avanti nell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="68c16-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="68c16-164">.</span><span class="sxs-lookup"><span data-stu-id="68c16-164">.</span></span> 
 
4. <span data-ttu-id="68c16-165">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="68c16-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="68c16-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="68c16-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="68c16-169">In hello **configurazione riconoscere** fare clic su **configurare riconoscere** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="68c16-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="68c16-170">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="68c16-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="68c16-172">In una finestra del web browser, accesso tooyour Riconosci tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="68c16-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="68c16-173">Hello angolo superiore destro, scegliere **Menu**.</span><span class="sxs-lookup"><span data-stu-id="68c16-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="68c16-174">Andare troppo**amministratore società**.</span><span class="sxs-lookup"><span data-stu-id="68c16-174">Go too**Company Admin**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="68c16-176">Nel riquadro di spostamento a sinistra di hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="68c16-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="68c16-178">Eseguire hello seguendo i passaggi **impostazioni SSO** sezione.</span><span class="sxs-lookup"><span data-stu-id="68c16-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="68c16-180">a.</span><span class="sxs-lookup"><span data-stu-id="68c16-180">a.</span></span> <span data-ttu-id="68c16-181">In **Enable SSO** (Abilita SSO) selezionare **ON**.</span><span class="sxs-lookup"><span data-stu-id="68c16-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="68c16-182">b.</span><span class="sxs-lookup"><span data-stu-id="68c16-182">b.</span></span> <span data-ttu-id="68c16-183">In hello **IDP Entity ID** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="68c16-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="68c16-184">c.</span><span class="sxs-lookup"><span data-stu-id="68c16-184">c.</span></span> <span data-ttu-id="68c16-185">In hello **Sso target url** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="68c16-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="68c16-186">d.</span><span class="sxs-lookup"><span data-stu-id="68c16-186">d.</span></span> <span data-ttu-id="68c16-187">In hello **url di destinazione Slo** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="68c16-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="68c16-188">e.</span><span class="sxs-lookup"><span data-stu-id="68c16-188">e.</span></span> <span data-ttu-id="68c16-189">Aprire lo scaricato **certificato (Base64)** file nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="68c16-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="68c16-190">f.</span><span class="sxs-lookup"><span data-stu-id="68c16-190">f.</span></span> <span data-ttu-id="68c16-191">Fare clic su hello **salvare impostazioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="68c16-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="68c16-192">Accanto a hello **impostazioni SSO** sezione, copiare l'URL di hello in **url dei metadati del Provider del servizio**.</span><span class="sxs-lookup"><span data-stu-id="68c16-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="68c16-194">Aprire hello **collegamento URL dei metadati** in un documento di metadati hello toodownload vuota del browser.</span><span class="sxs-lookup"><span data-stu-id="68c16-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="68c16-195">Copiare quindi hello EntityDescriptor value(entityID) dal file hello e incollarlo in **identificatore** nella casella di testo **sezione riconoscere dominio e gli URL** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="68c16-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="68c16-197">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="68c16-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="68c16-198">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="68c16-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="68c16-199">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68c16-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68c16-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="68c16-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="68c16-201">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="68c16-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="68c16-203">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="68c16-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="68c16-204">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="68c16-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68c16-206">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="68c16-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68c16-208">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="68c16-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68c16-210">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="68c16-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68c16-212">a.</span><span class="sxs-lookup"><span data-stu-id="68c16-212">a.</span></span> <span data-ttu-id="68c16-213">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68c16-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68c16-214">b.</span><span class="sxs-lookup"><span data-stu-id="68c16-214">b.</span></span> <span data-ttu-id="68c16-215">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="68c16-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68c16-216">c.</span><span class="sxs-lookup"><span data-stu-id="68c16-216">c.</span></span> <span data-ttu-id="68c16-217">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="68c16-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="68c16-218">d.</span><span class="sxs-lookup"><span data-stu-id="68c16-218">d.</span></span> <span data-ttu-id="68c16-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="68c16-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="68c16-220">Creazione di un utente test di Recognize</span><span class="sxs-lookup"><span data-stu-id="68c16-220">Creating a Recognize test user</span></span>

<span data-ttu-id="68c16-221">In ordine tooenable Azure AD utenti toolog in riconoscere, è necessario essere il provisioning in Riconosci.</span><span class="sxs-lookup"><span data-stu-id="68c16-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="68c16-222">Nel caso di hello di riconoscere, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="68c16-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="68c16-223">Questa app non supporta il provisioning SCIM, ma dispone di una sincronizzazione utente alternativa che esegue il provisioning degli utenti.</span><span class="sxs-lookup"><span data-stu-id="68c16-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="68c16-224">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="68c16-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="68c16-225">Accedere al sito aziendale di Recognize come amministratore.</span><span class="sxs-lookup"><span data-stu-id="68c16-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="68c16-226">Hello angolo superiore destro, scegliere **Menu**.</span><span class="sxs-lookup"><span data-stu-id="68c16-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="68c16-227">Andare troppo**amministratore società**.</span><span class="sxs-lookup"><span data-stu-id="68c16-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="68c16-228">Nel riquadro di spostamento a sinistra di hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="68c16-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="68c16-229">Eseguire hello seguendo i passaggi **sincronizzazione utente** sezione.</span><span class="sxs-lookup"><span data-stu-id="68c16-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="68c16-230">![Nuovo utente](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="68c16-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="68c16-231">a.</span><span class="sxs-lookup"><span data-stu-id="68c16-231">a.</span></span> <span data-ttu-id="68c16-232">In **Sync Enabled** (Sincronizzazione abilitata) selezionare **ON**.</span><span class="sxs-lookup"><span data-stu-id="68c16-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="68c16-233">b.</span><span class="sxs-lookup"><span data-stu-id="68c16-233">b.</span></span> <span data-ttu-id="68c16-234">In **Choose sync provider** (Scegli provider di sincronizzazione) selezionare **Microsoft/Office 365**.</span><span class="sxs-lookup"><span data-stu-id="68c16-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="68c16-235">c.</span><span class="sxs-lookup"><span data-stu-id="68c16-235">c.</span></span> <span data-ttu-id="68c16-236">Fare clic su **Run User Sync** (Esegui sincronizzazione utente).</span><span class="sxs-lookup"><span data-stu-id="68c16-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="68c16-237">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="68c16-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="68c16-238">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRecognize.</span><span class="sxs-lookup"><span data-stu-id="68c16-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Assegna utente][200] 

<span data-ttu-id="68c16-240">**tooassign Britta Simon tooRecognize, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="68c16-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="68c16-241">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="68c16-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="68c16-243">Nell'elenco di applicazioni hello, selezionare **Riconosci**.</span><span class="sxs-lookup"><span data-stu-id="68c16-243">In hello applications list, select **Recognize**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="68c16-245">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="68c16-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="68c16-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="68c16-247">Click **Add** button.</span></span> <span data-ttu-id="68c16-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="68c16-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="68c16-250">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="68c16-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="68c16-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="68c16-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68c16-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="68c16-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68c16-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="68c16-253">Testing single sign-on</span></span>

<span data-ttu-id="68c16-254">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="68c16-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="68c16-255">Quando si fa clic su riquadro Riconosci hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Riconosci applicazione.</span><span class="sxs-lookup"><span data-stu-id="68c16-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="68c16-256">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68c16-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68c16-257">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="68c16-257">Additional resources</span></span>

* [<span data-ttu-id="68c16-258">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68c16-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68c16-259">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68c16-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png


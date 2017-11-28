---
title: 'Esercitazione: Integrazione di Azure Active Directory con M-Files | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e file di M.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="70cd1-103">Esercitazione: Integrazione di Azure Active Directory con M-Files</span><span class="sxs-lookup"><span data-stu-id="70cd1-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="70cd1-104">In questa esercitazione, è illustrato come toointegrate M-file con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70cd1-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70cd1-105">M-file di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="70cd1-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70cd1-106">È possibile controllare in Azure AD che dispone di accesso tooM-file</span><span class="sxs-lookup"><span data-stu-id="70cd1-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="70cd1-107">È possibile abilitare gli utenti tooautomatically get connesso tooM-file (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="70cd1-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70cd1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="70cd1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70cd1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70cd1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70cd1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="70cd1-110">Prerequisites</span></span>

<span data-ttu-id="70cd1-111">tooconfigure integrazione di Azure AD con i file-M, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="70cd1-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="70cd1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70cd1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70cd1-113">Sottoscrizione di M-Files abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="70cd1-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70cd1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="70cd1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70cd1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="70cd1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70cd1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="70cd1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70cd1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70cd1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70cd1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="70cd1-118">Scenario description</span></span>
<span data-ttu-id="70cd1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="70cd1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70cd1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="70cd1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70cd1-121">Aggiunta di M-file dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="70cd1-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="70cd1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70cd1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="70cd1-123">Aggiunta di M-file dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="70cd1-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="70cd1-124">integrazione hello tooconfigure di M file in Azure AD, è necessario tooadd M file dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="70cd1-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70cd1-125">**tooadd M file dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70cd1-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70cd1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="70cd1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70cd1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70cd1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="70cd1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="70cd1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="70cd1-133">Nella casella di ricerca hello, digitare **M file**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-133">In hello search box, type **M-Files**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="70cd1-135">Nel riquadro dei risultati hello, selezionare **M file**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="70cd1-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70cd1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70cd1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70cd1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con M-Files usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="70cd1-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="70cd1-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nei file di M è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70cd1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="70cd1-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e utente correlato di hello nei file-M deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="70cd1-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="70cd1-141">M-file, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="70cd1-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70cd1-142">tooconfigure e prova AD Azure single sign-on con i file-M, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="70cd1-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70cd1-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="70cd1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70cd1-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70cd1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70cd1-145">**[Creazione di un utente test M file](#creating-a-m-files-test-user)**  -toohave un equivalente di Britta Simon M-file che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="70cd1-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70cd1-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="70cd1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70cd1-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="70cd1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70cd1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70cd1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70cd1-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione i file-M.</span><span class="sxs-lookup"><span data-stu-id="70cd1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="70cd1-150">**Azure AD tooconfigure single sign-on con M-file, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70cd1-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="70cd1-151">Nel portale di Azure su hello hello **M file** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="70cd1-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="70cd1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="70cd1-155">In hello **M-file di dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70cd1-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="70cd1-157">a.</span><span class="sxs-lookup"><span data-stu-id="70cd1-157">a.</span></span> <span data-ttu-id="70cd1-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="70cd1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="70cd1-159">b.</span><span class="sxs-lookup"><span data-stu-id="70cd1-159">b.</span></span> <span data-ttu-id="70cd1-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="70cd1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70cd1-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="70cd1-161">These values are not real.</span></span> <span data-ttu-id="70cd1-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="70cd1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="70cd1-163">Contatto [team di supporto Client i file-M](mailto:support@m-files.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="70cd1-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="70cd1-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="70cd1-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="70cd1-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="70cd1-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70cd1-168">tooget SSO è configurato per l'applicazione, contattare [M-file di supporto tecnico](mailto:support@m-files.com) e fornire loro hello scaricato i metadati.</span><span class="sxs-lookup"><span data-stu-id="70cd1-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="70cd1-169">Seguire i passaggi successivi hello se si desidera tooconfigure SSO per l'utente applicazione desktop M-File.</span><span class="sxs-lookup"><span data-stu-id="70cd1-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="70cd1-170">Se si desidera solo tooconfigure SSO per la versione web M-file, è necessario alcun passaggi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="70cd1-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="70cd1-171">Seguire hello successivi passaggi tooconfigure hello M File applicazione desktop tooenable SSO con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70cd1-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="70cd1-172">toodownload M-file, andare troppo[scaricare i file-M](https://www.m-files.com/en/download-latest-version) pagina.</span><span class="sxs-lookup"><span data-stu-id="70cd1-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="70cd1-173">Aprire hello **M-file di impostazioni del Desktop** finestra.</span><span class="sxs-lookup"><span data-stu-id="70cd1-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="70cd1-174">Fare quindi clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-174">Then, click **Add**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="70cd1-176">In hello **documento insieme di credenziali delle proprietà di connessione** finestra, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70cd1-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="70cd1-178">In tipo di sezione Server hello, hello valori come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="70cd1-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="70cd1-179">a.</span><span class="sxs-lookup"><span data-stu-id="70cd1-179">a.</span></span> <span data-ttu-id="70cd1-180">Per **Nome** digitare `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="70cd1-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="70cd1-181">b.</span><span class="sxs-lookup"><span data-stu-id="70cd1-181">b.</span></span> <span data-ttu-id="70cd1-182">Per **Numero porta** digitare **4466**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="70cd1-183">c.</span><span class="sxs-lookup"><span data-stu-id="70cd1-183">c.</span></span> <span data-ttu-id="70cd1-184">Per **Protocollo** selezionare **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="70cd1-185">d.</span><span class="sxs-lookup"><span data-stu-id="70cd1-185">d.</span></span> <span data-ttu-id="70cd1-186">In hello **autenticazione** campi, selezionare **utente di Windows specifico**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="70cd1-187">Verrà visualizzata una pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="70cd1-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="70cd1-188">Inserire le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70cd1-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="70cd1-189">e.</span><span class="sxs-lookup"><span data-stu-id="70cd1-189">e.</span></span> <span data-ttu-id="70cd1-190">Per hello **insieme di credenziali nel Server**, selezionare hello insieme di credenziali corrispondente nel server.</span><span class="sxs-lookup"><span data-stu-id="70cd1-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="70cd1-191">f.</span><span class="sxs-lookup"><span data-stu-id="70cd1-191">f.</span></span> <span data-ttu-id="70cd1-192">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="70cd1-193">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="70cd1-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70cd1-194">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="70cd1-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70cd1-195">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70cd1-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70cd1-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70cd1-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="70cd1-197">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="70cd1-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="70cd1-199">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70cd1-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70cd1-200">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="70cd1-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70cd1-202">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70cd1-204">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="70cd1-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70cd1-206">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70cd1-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70cd1-208">a.</span><span class="sxs-lookup"><span data-stu-id="70cd1-208">a.</span></span> <span data-ttu-id="70cd1-209">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70cd1-210">b.</span><span class="sxs-lookup"><span data-stu-id="70cd1-210">b.</span></span> <span data-ttu-id="70cd1-211">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70cd1-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70cd1-212">c.</span><span class="sxs-lookup"><span data-stu-id="70cd1-212">c.</span></span> <span data-ttu-id="70cd1-213">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70cd1-214">d.</span><span class="sxs-lookup"><span data-stu-id="70cd1-214">d.</span></span> <span data-ttu-id="70cd1-215">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="70cd1-216">Creazione di un utente di test per M-Files</span><span class="sxs-lookup"><span data-stu-id="70cd1-216">Creating a M-Files test user</span></span>

<span data-ttu-id="70cd1-217">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon M-file.</span><span class="sxs-lookup"><span data-stu-id="70cd1-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="70cd1-218">Lavorare con [M-file di supporto tecnico](mailto:support@m-files.com) utenti hello tooadd M file hello.</span><span class="sxs-lookup"><span data-stu-id="70cd1-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70cd1-219">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70cd1-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70cd1-220">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooM-file.</span><span class="sxs-lookup"><span data-stu-id="70cd1-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Assegna utente][200] 

<span data-ttu-id="70cd1-222">**tooassign Britta Simon tooM-file, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70cd1-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="70cd1-223">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="70cd1-225">Nell'elenco di applicazioni hello, selezionare **M file**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-225">In hello applications list, select **M-Files**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="70cd1-227">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="70cd1-229">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-229">Click **Add** button.</span></span> <span data-ttu-id="70cd1-230">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="70cd1-232">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="70cd1-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70cd1-233">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70cd1-234">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="70cd1-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70cd1-235">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="70cd1-235">Testing single sign-on</span></span>

<span data-ttu-id="70cd1-236">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="70cd1-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="70cd1-237">Quando si fa clic hello M file riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour M file applicazione.</span><span class="sxs-lookup"><span data-stu-id="70cd1-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70cd1-238">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="70cd1-238">Additional resources</span></span>

* [<span data-ttu-id="70cd1-239">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70cd1-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70cd1-240">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70cd1-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png


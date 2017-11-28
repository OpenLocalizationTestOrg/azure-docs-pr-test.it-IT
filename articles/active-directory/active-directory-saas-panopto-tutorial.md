---
title: 'Esercitazione: Integrazione di Azure Active Directory con Panopto | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Panopto.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="19edd-103">Esercitazione: Integrazione di Azure Active Directory con Panopto</span><span class="sxs-lookup"><span data-stu-id="19edd-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="19edd-104">In questa esercitazione, è illustrato come toointegrate Panopto con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19edd-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19edd-105">Integrazione Panopto con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="19edd-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="19edd-106">È possibile controllare in Azure AD che ha accesso tooPanopto</span><span class="sxs-lookup"><span data-stu-id="19edd-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="19edd-107">È possibile abilitare l'utenti tooautomatically get connesso tooPanopto (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="19edd-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19edd-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="19edd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="19edd-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19edd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19edd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="19edd-110">Prerequisites</span></span>

<span data-ttu-id="19edd-111">integrazione di Azure AD con Panopto tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="19edd-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="19edd-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19edd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19edd-113">Sottoscrizione di Panopto abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="19edd-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19edd-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="19edd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19edd-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="19edd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19edd-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="19edd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19edd-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19edd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19edd-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="19edd-118">Scenario description</span></span>
<span data-ttu-id="19edd-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="19edd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19edd-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="19edd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19edd-121">Aggiunta di Panopto dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="19edd-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="19edd-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19edd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="19edd-123">Aggiunta di Panopto dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="19edd-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="19edd-124">integrazione hello tooconfigure di Panopto in Azure AD, è necessario tooadd Panopto dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="19edd-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="19edd-125">**tooadd Panopto dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19edd-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="19edd-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="19edd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19edd-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="19edd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="19edd-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="19edd-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="19edd-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="19edd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="19edd-133">Nella casella di ricerca hello, digitare **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="19edd-133">In hello search box, type **Panopto**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="19edd-135">Nel riquadro dei risultati hello, selezionare **Panopto**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="19edd-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19edd-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19edd-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="19edd-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Panopto usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19edd-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="19edd-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Panopto è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19edd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="19edd-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Panopto deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="19edd-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="19edd-141">In Panopto, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="19edd-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="19edd-142">tooconfigure e test Azure single sign-on AD con Panopto, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="19edd-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="19edd-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="19edd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="19edd-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19edd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19edd-145">**[Creazione di un utente test Panopto](#creating-a-panopto-test-user)**  -toohave un equivalente di Britta Simon in Panopto che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="19edd-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="19edd-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19edd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19edd-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="19edd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19edd-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19edd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19edd-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Panopto.</span><span class="sxs-lookup"><span data-stu-id="19edd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="19edd-150">**Azure AD tooconfigure single sign-on con Panopto, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19edd-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="19edd-151">Nel portale di Azure su hello hello **Panopto** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="19edd-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="19edd-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19edd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="19edd-155">In hello **Panopto dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="19edd-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="19edd-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="19edd-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="19edd-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="19edd-158">This value is not real.</span></span> <span data-ttu-id="19edd-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="19edd-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="19edd-160">Contatto [team di supporto Panopto Client](mailto:support@panopto.com‎) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="19edd-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="19edd-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="19edd-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="19edd-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="19edd-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19edd-165">In hello **Panopto configurazione** fare clic su **configurare Panopto** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="19edd-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="19edd-166">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="19edd-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="19edd-168">In una finestra del web browser, accedere come amministratore nel sito della società Panopto di tooyour.</span><span class="sxs-lookup"><span data-stu-id="19edd-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="19edd-169">Nella barra degli strumenti hello hello sinistra, fare clic su **sistema**, quindi fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="19edd-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="19edd-170">![Sistema](./media/active-directory-saas-panopto-tutorial/ic777670.png "Sistema")</span><span class="sxs-lookup"><span data-stu-id="19edd-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="19edd-171">Fare clic su **Aggiungi provider**.</span><span class="sxs-lookup"><span data-stu-id="19edd-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="19edd-172">![Provider di identità](./media/active-directory-saas-panopto-tutorial/ic777671.png "Provider di identità")</span><span class="sxs-lookup"><span data-stu-id="19edd-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="19edd-173">Nella sezione relativa al provider SAML hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="19edd-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="19edd-174">![Configurazione SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Configurazione SaaS")</span><span class="sxs-lookup"><span data-stu-id="19edd-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="19edd-175">a.</span><span class="sxs-lookup"><span data-stu-id="19edd-175">a.</span></span> <span data-ttu-id="19edd-176">Da hello **tipo di Provider** elenco, selezionare **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="19edd-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="19edd-177">b.</span><span class="sxs-lookup"><span data-stu-id="19edd-177">b.</span></span> <span data-ttu-id="19edd-178">In hello **nome dell'istanza** casella di testo, digitare un nome per l'istanza di hello.</span><span class="sxs-lookup"><span data-stu-id="19edd-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="19edd-179">c.</span><span class="sxs-lookup"><span data-stu-id="19edd-179">c.</span></span> <span data-ttu-id="19edd-180">In hello **descrizione** casella di testo, digitare una descrizione.</span><span class="sxs-lookup"><span data-stu-id="19edd-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="19edd-181">d.</span><span class="sxs-lookup"><span data-stu-id="19edd-181">d.</span></span> <span data-ttu-id="19edd-182">In **Bounce Page Url** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="19edd-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="19edd-183">e.</span><span class="sxs-lookup"><span data-stu-id="19edd-183">e.</span></span> <span data-ttu-id="19edd-184">In hello **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="19edd-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="19edd-185">f.</span><span class="sxs-lookup"><span data-stu-id="19edd-185">f.</span></span> <span data-ttu-id="19edd-186">Aprire il certificato con codifica base 64, che è stato scaricato da Azure hello copia portale, contenuto negli Appunti tooyour di esso, e quindi incollarlo toohello **chiave pubblica** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="19edd-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="19edd-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="19edd-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="19edd-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="19edd-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="19edd-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="19edd-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="19edd-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19edd-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19edd-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="19edd-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="19edd-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="19edd-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="19edd-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19edd-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="19edd-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="19edd-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19edd-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="19edd-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19edd-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="19edd-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19edd-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="19edd-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19edd-203">a.</span><span class="sxs-lookup"><span data-stu-id="19edd-203">a.</span></span> <span data-ttu-id="19edd-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19edd-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19edd-205">b.</span><span class="sxs-lookup"><span data-stu-id="19edd-205">b.</span></span> <span data-ttu-id="19edd-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="19edd-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19edd-207">c.</span><span class="sxs-lookup"><span data-stu-id="19edd-207">c.</span></span> <span data-ttu-id="19edd-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="19edd-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="19edd-209">d.</span><span class="sxs-lookup"><span data-stu-id="19edd-209">d.</span></span> <span data-ttu-id="19edd-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="19edd-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="19edd-211">Creazione di un utente di test di Panopto</span><span class="sxs-lookup"><span data-stu-id="19edd-211">Creating a Panopto test user</span></span>

<span data-ttu-id="19edd-212">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="19edd-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="19edd-213">Quando un utente assegnato tenta toolog in tooPanopto mediante il pannello di accesso di hello, Panopto verifica se hello utente esiste.</span><span class="sxs-lookup"><span data-stu-id="19edd-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="19edd-214">Se l’account utente non è disponibile, viene creato automaticamente da Panopto.</span><span class="sxs-lookup"><span data-stu-id="19edd-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="19edd-215">È possibile usare qualsiasi altro Panopto utente account strumento di creazione o le API fornite da Panopto tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19edd-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="19edd-216">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="19edd-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="19edd-217">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="19edd-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![Assegna utente][200] 

<span data-ttu-id="19edd-219">**tooassign Britta Simon tooPanopto, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="19edd-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="19edd-220">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="19edd-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="19edd-222">Nell'elenco di applicazioni hello, selezionare **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="19edd-222">In hello applications list, select **Panopto**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="19edd-224">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="19edd-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="19edd-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="19edd-226">Click **Add** button.</span></span> <span data-ttu-id="19edd-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="19edd-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="19edd-229">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="19edd-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="19edd-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="19edd-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19edd-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="19edd-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19edd-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="19edd-232">Testing single sign-on</span></span>

<span data-ttu-id="19edd-233">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="19edd-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="19edd-234">Quando si fa clic su riquadro Panopto hello in hello Pannello di accesso, è necessario ottenere automaticamente la pagina di accesso dell'applicazione Panopto.</span><span class="sxs-lookup"><span data-stu-id="19edd-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="19edd-235">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19edd-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19edd-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="19edd-236">Additional resources</span></span>

* [<span data-ttu-id="19edd-237">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19edd-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19edd-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19edd-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png


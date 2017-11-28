---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zoom | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Zoom.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="1e637-103">Esercitazione: Integrazione di Azure Active Directory con Zoom</span><span class="sxs-lookup"><span data-stu-id="1e637-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="1e637-104">In questa esercitazione, è illustrato come eseguire lo Zoom toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e637-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e637-105">Integrazione di Zoom con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1e637-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e637-106">È possibile controllare in Azure AD che ha accesso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="1e637-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="1e637-107">È possibile abilitare l'utenti tooautomatically get connesso tooZoom (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e637-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1e637-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e637-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1e637-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e637-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e637-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1e637-110">Prerequisites</span></span>

<span data-ttu-id="1e637-111">integrazione di tooconfigure Azure AD con Zoom, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1e637-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="1e637-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e637-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e637-113">Sottoscrizione di Zoom abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1e637-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e637-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1e637-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e637-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1e637-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e637-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1e637-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e637-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e637-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e637-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1e637-118">Scenario description</span></span>
<span data-ttu-id="1e637-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1e637-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e637-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1e637-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e637-121">Aggiunta di Zoom dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1e637-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="1e637-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e637-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="1e637-123">Aggiunta di Zoom dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1e637-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="1e637-124">integrazione di hello tooconfigure di Zoom in Azure AD, è necessario tooadd Zoom dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1e637-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e637-125">**tooadd Zoom dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e637-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e637-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1e637-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="1e637-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1e637-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e637-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e637-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="1e637-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1e637-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="1e637-133">Nella casella di ricerca hello, digitare **Zoom**selezionare **Zoom** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1e637-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Eseguire lo zoom avanti nell'elenco risultati hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1e637-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e637-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1e637-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zoom usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1e637-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e637-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zoom è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e637-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="1e637-138">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Zoom esigenze toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1e637-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="1e637-139">Nella finestra di Zoom, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1e637-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1e637-140">tooconfigure e prova AD Azure single sign-on con Zoom, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1e637-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e637-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1e637-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e637-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e637-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e637-143">**[Creare un utente test Zoom](#create-a-zoom-test-user)**  -toohave un equivalente di Britta Simon nel livello di Zoom che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1e637-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e637-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1e637-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e637-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1e637-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1e637-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e637-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1e637-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione dello Zoom.</span><span class="sxs-lookup"><span data-stu-id="1e637-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="1e637-148">**tooconfigure AD Azure single sign-on con fattore di Zoom, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e637-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e637-149">Nel portale di Azure su hello hello **Zoom** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1e637-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="1e637-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1e637-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="1e637-153">In hello **Zoom dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e637-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="1e637-155">a.</span><span class="sxs-lookup"><span data-stu-id="1e637-155">a.</span></span> <span data-ttu-id="1e637-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="1e637-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="1e637-157">b.</span><span class="sxs-lookup"><span data-stu-id="1e637-157">b.</span></span> <span data-ttu-id="1e637-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="1e637-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e637-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1e637-159">These values are not real.</span></span> <span data-ttu-id="1e637-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="1e637-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e637-161">Contatto [team di supporto Client di eseguire lo Zoom](https://support.zoom.us/hc) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1e637-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="1e637-162">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1e637-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="1e637-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1e637-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e637-166">In hello **Zoom configurazione** fare clic su **configurare Zoom** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1e637-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e637-167">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1e637-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="1e637-169">In una finestra del web browser, accedere come amministratore nel sito della società Zoom di tooyour.</span><span class="sxs-lookup"><span data-stu-id="1e637-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="1e637-170">Fare clic su hello **Single Sign-On** scheda.</span><span class="sxs-lookup"><span data-stu-id="1e637-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="1e637-171">![Scheda Single Sign-On](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1e637-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="1e637-172">Fare clic su hello **controllo di sicurezza** scheda e quindi passare toohello **Single Sign-On** impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1e637-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="1e637-173">Nella sezione Single Sign-On hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e637-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1e637-174">![Sezione Single Sign-On](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1e637-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="1e637-175">a.</span><span class="sxs-lookup"><span data-stu-id="1e637-175">a.</span></span> <span data-ttu-id="1e637-176">In hello **accesso URL della pagina** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e637-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="1e637-177">b.</span><span class="sxs-lookup"><span data-stu-id="1e637-177">b.</span></span> <span data-ttu-id="1e637-178">In hello **URL pagina di disconnessione** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e637-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="1e637-179">c.</span><span class="sxs-lookup"><span data-stu-id="1e637-179">c.</span></span> <span data-ttu-id="1e637-180">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1e637-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="1e637-181">d.</span><span class="sxs-lookup"><span data-stu-id="1e637-181">d.</span></span> <span data-ttu-id="1e637-182">In hello **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e637-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1e637-183">e.</span><span class="sxs-lookup"><span data-stu-id="1e637-183">e.</span></span> <span data-ttu-id="1e637-184">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1e637-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1e637-185">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1e637-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e637-186">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1e637-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e637-187">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e637-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1e637-188">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e637-188">Create an Azure AD test user</span></span>

<span data-ttu-id="1e637-189">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1e637-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="1e637-191">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e637-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e637-192">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="1e637-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1e637-194">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1e637-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1e637-196">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1e637-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1e637-198">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e637-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1e637-200">a.</span><span class="sxs-lookup"><span data-stu-id="1e637-200">a.</span></span> <span data-ttu-id="1e637-201">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e637-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e637-202">b.</span><span class="sxs-lookup"><span data-stu-id="1e637-202">b.</span></span> <span data-ttu-id="1e637-203">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e637-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1e637-204">c.</span><span class="sxs-lookup"><span data-stu-id="1e637-204">c.</span></span> <span data-ttu-id="1e637-205">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="1e637-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1e637-206">d.</span><span class="sxs-lookup"><span data-stu-id="1e637-206">d.</span></span> <span data-ttu-id="1e637-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1e637-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="1e637-208">Creare un utente di test di Zoom</span><span class="sxs-lookup"><span data-stu-id="1e637-208">Create a Zoom test user</span></span>

<span data-ttu-id="1e637-209">In ordine tooenable Azure AD utenti toolog in tooZoom, è necessario eseguirne il provisioning in Zoom.</span><span class="sxs-lookup"><span data-stu-id="1e637-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="1e637-210">Nel caso di hello di Zoom, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="1e637-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="1e637-211">tooprovision un account utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e637-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="1e637-212">Accedi tooyour **Zoom** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1e637-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="1e637-213">Fare clic su hello **gestione degli Account** scheda e quindi fare clic su **Gestione utenti**.</span><span class="sxs-lookup"><span data-stu-id="1e637-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="1e637-214">Nella sezione User Management hello, fare clic su **aggiungere utenti**.</span><span class="sxs-lookup"><span data-stu-id="1e637-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="1e637-215">![Gestione degli utenti](./media/active-directory-saas-zoom-tutorial/IC784703.png "Gestione degli utenti")</span><span class="sxs-lookup"><span data-stu-id="1e637-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="1e637-216">In hello **aggiungere utenti** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e637-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="1e637-217">![Aggiungere utenti](./media/active-directory-saas-zoom-tutorial/IC784704.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="1e637-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="1e637-218">a.</span><span class="sxs-lookup"><span data-stu-id="1e637-218">a.</span></span> <span data-ttu-id="1e637-219">In **Tipo utente** selezionare **Basic**.</span><span class="sxs-lookup"><span data-stu-id="1e637-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="1e637-220">b.</span><span class="sxs-lookup"><span data-stu-id="1e637-220">b.</span></span> <span data-ttu-id="1e637-221">In hello **messaggi di posta elettronica** casella Tipo hello di indirizzo di posta elettronica di un valido di Azure si desidera tooprovision di account di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e637-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="1e637-222">c.</span><span class="sxs-lookup"><span data-stu-id="1e637-222">c.</span></span> <span data-ttu-id="1e637-223">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1e637-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="1e637-224">È possibile usare qualsiasi altro Zoom utente account strumento di creazione o le API fornite da Zoom tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="1e637-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1e637-225">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e637-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1e637-226">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="1e637-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="1e637-228">**tooassign Britta Simon tooZoom, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e637-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e637-229">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e637-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1e637-231">Nell'elenco di applicazioni hello, selezionare **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="1e637-231">In hello applications list, select **Zoom**.</span></span>

    ![collegamento di Zoom Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="1e637-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1e637-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="1e637-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1e637-235">Click **Add** button.</span></span> <span data-ttu-id="1e637-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1e637-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="1e637-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1e637-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e637-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1e637-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e637-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1e637-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1e637-241">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1e637-241">Test single sign-on</span></span>

<span data-ttu-id="1e637-242">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e637-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e637-243">Quando si fa clic su Riquadro Zoom hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Zoom applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e637-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e637-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1e637-244">Additional resources</span></span>

* [<span data-ttu-id="1e637-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e637-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e637-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e637-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png


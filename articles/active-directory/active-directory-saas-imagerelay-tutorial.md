---
title: 'Esercitazione: Integrazione di Azure Active Directory con Image Relay | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e l'inoltro di immagine.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="586b1-103">Esercitazione: Integrazione di Azure Active Directory con Image Relay</span><span class="sxs-lookup"><span data-stu-id="586b1-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="586b1-104">In questa esercitazione, è illustrato come toointegrate inoltro immagine con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="586b1-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="586b1-105">Immagine di inoltro di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="586b1-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="586b1-106">È possibile controllare in Azure AD che ha accesso tooImage inoltro</span><span class="sxs-lookup"><span data-stu-id="586b1-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="586b1-107">È possibile abilitare l'utenti tooautomatically get connesso tooImage inoltro (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="586b1-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="586b1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="586b1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="586b1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="586b1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="586b1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="586b1-110">Prerequisites</span></span>

<span data-ttu-id="586b1-111">integrazione di Azure AD con inoltro immagine tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="586b1-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="586b1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="586b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="586b1-113">Sottoscrizione di Image Relay abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="586b1-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="586b1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="586b1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="586b1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="586b1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="586b1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="586b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="586b1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="586b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="586b1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="586b1-118">Scenario description</span></span>
<span data-ttu-id="586b1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="586b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="586b1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="586b1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="586b1-121">Aggiunta di inoltro immagine dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="586b1-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="586b1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="586b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="586b1-123">Aggiunta di inoltro immagine dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="586b1-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="586b1-124">integrazione hello tooconfigure di inoltro di immagine in Azure AD, è necessario tooadd inoltro immagine dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="586b1-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="586b1-125">**tooadd inoltro immagine dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="586b1-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="586b1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="586b1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="586b1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="586b1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="586b1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="586b1-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="586b1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="586b1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="586b1-133">Nella casella di ricerca hello, digitare **inoltro immagine**.</span><span class="sxs-lookup"><span data-stu-id="586b1-133">In hello search box, type **Image Relay**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="586b1-135">Nel riquadro dei risultati hello, selezionare **inoltro immagine**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="586b1-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="586b1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="586b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="586b1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Image Relay mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="586b1-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="586b1-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in inoltro immagine è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="586b1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="586b1-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in inoltro immagine richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="586b1-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="586b1-141">Nell'immagine di inoltro, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="586b1-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="586b1-142">tooconfigure e prova AD Azure single sign-on con immagine di inoltro, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="586b1-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="586b1-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="586b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="586b1-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="586b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="586b1-145">**[Creazione di un utente di test di inoltro immagine](#creating-an-image-relay-test-user)**  -toohave un equivalente di Britta Simon nell'inoltro di immagine che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="586b1-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="586b1-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="586b1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="586b1-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="586b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="586b1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="586b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="586b1-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione inoltro immagine.</span><span class="sxs-lookup"><span data-stu-id="586b1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="586b1-150">**Azure AD tooconfigure single sign-on con inoltro immagine, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="586b1-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="586b1-151">Nel portale di Azure su hello hello **inoltro immagine** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="586b1-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="586b1-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="586b1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="586b1-155">In hello **URL e il dominio di inoltro immagine** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="586b1-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="586b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="586b1-157">a.</span></span> <span data-ttu-id="586b1-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="586b1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="586b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="586b1-159">b.</span></span> <span data-ttu-id="586b1-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="586b1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="586b1-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="586b1-161">These values are not real.</span></span> <span data-ttu-id="586b1-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="586b1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="586b1-163">Contatto [team di supporto Client di inoltro immagine](http://support.imagerelay.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="586b1-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="586b1-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="586b1-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="586b1-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="586b1-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="586b1-168">In hello **immagine inoltro configurazione** fare clic su **configurare inoltro immagine** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="586b1-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="586b1-169">Hello copia **Sign-Out URL del servizio e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="586b1-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="586b1-171">In un'altra finestra del browser, accedere come amministratore nel sito della società di inoltro immagine tooyour.</span><span class="sxs-lookup"><span data-stu-id="586b1-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="586b1-172">Nella barra degli strumenti hello in primo piano hello, fare clic su hello **utenti e autorizzazioni** carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="586b1-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="586b1-174">Fare clic su **Create New Permission**(Crea nuova autorizzazione).</span><span class="sxs-lookup"><span data-stu-id="586b1-174">Click **Create New Permission**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="586b1-176">In hello **Single Sign On Settings** carico di lavoro, seleziona hello **questo gruppo possono solo Accedi tramite Single Sign-On** casella di controllo e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="586b1-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="586b1-178">Andare troppo**impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="586b1-178">Go too**Account Settings**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="586b1-180">Passare toohello **Single Sign On Settings** carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="586b1-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="586b1-182">In hello **impostazioni SAML** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="586b1-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="586b1-184">a.</span><span class="sxs-lookup"><span data-stu-id="586b1-184">a.</span></span> <span data-ttu-id="586b1-185">In **URL di accesso** casella di testo, hello Incolla valore **URL servizio Single Sign-On** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="586b1-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="586b1-186">b.</span><span class="sxs-lookup"><span data-stu-id="586b1-186">b.</span></span> <span data-ttu-id="586b1-187">In **Logout URL** casella di testo, hello Incolla valore **URL del servizio Single Sign-Out** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="586b1-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="586b1-188">c.</span><span class="sxs-lookup"><span data-stu-id="586b1-188">c.</span></span> <span data-ttu-id="586b1-189">Come **Name Id Format** (Formato ID nome) selezionare**urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="586b1-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="586b1-190">d.</span><span class="sxs-lookup"><span data-stu-id="586b1-190">d.</span></span> <span data-ttu-id="586b1-191">Come **opzioni di associazione per le richieste dal Provider di servizi (immagine inoltro) hello**selezionare **POST associazione**.</span><span class="sxs-lookup"><span data-stu-id="586b1-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="586b1-192">e.</span><span class="sxs-lookup"><span data-stu-id="586b1-192">e.</span></span> <span data-ttu-id="586b1-193">In **Certificato X.509** fare clic su **Aggiorna certificato**.</span><span class="sxs-lookup"><span data-stu-id="586b1-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="586b1-195">f.</span><span class="sxs-lookup"><span data-stu-id="586b1-195">f.</span></span> <span data-ttu-id="586b1-196">Aprire il certificato di hello scaricato nel blocco note, copiarne il contenuto di hello e quindi incollarlo nella casella di testo certificato x. 509 hello.</span><span class="sxs-lookup"><span data-stu-id="586b1-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="586b1-198">g.</span><span class="sxs-lookup"><span data-stu-id="586b1-198">g.</span></span> <span data-ttu-id="586b1-199">In **Provisioning utente JIT** sezione, seleziona hello **Abilita Provisioning utenti JIT**.</span><span class="sxs-lookup"><span data-stu-id="586b1-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="586b1-201">h.</span><span class="sxs-lookup"><span data-stu-id="586b1-201">h.</span></span> <span data-ttu-id="586b1-202">Gruppo di autorizzazioni SELECT hello (ad esempio, **SSO base**) che è consentito toosign in solo tramite accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="586b1-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="586b1-204">i.</span><span class="sxs-lookup"><span data-stu-id="586b1-204">i.</span></span> <span data-ttu-id="586b1-205">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="586b1-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="586b1-206">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="586b1-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="586b1-207">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="586b1-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="586b1-208">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="586b1-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="586b1-209">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="586b1-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="586b1-210">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="586b1-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="586b1-212">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="586b1-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="586b1-213">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="586b1-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="586b1-215">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="586b1-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="586b1-217">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="586b1-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="586b1-219">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="586b1-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="586b1-221">a.</span><span class="sxs-lookup"><span data-stu-id="586b1-221">a.</span></span> <span data-ttu-id="586b1-222">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="586b1-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="586b1-223">b.</span><span class="sxs-lookup"><span data-stu-id="586b1-223">b.</span></span> <span data-ttu-id="586b1-224">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="586b1-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="586b1-225">c.</span><span class="sxs-lookup"><span data-stu-id="586b1-225">c.</span></span> <span data-ttu-id="586b1-226">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="586b1-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="586b1-227">d.</span><span class="sxs-lookup"><span data-stu-id="586b1-227">d.</span></span> <span data-ttu-id="586b1-228">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="586b1-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="586b1-229">Creazione di un utente test di Image Relay</span><span class="sxs-lookup"><span data-stu-id="586b1-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="586b1-230">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon nell'immagine di inoltro.</span><span class="sxs-lookup"><span data-stu-id="586b1-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="586b1-231">**un utente denominato Britta Simon nell'immagine di inoltro, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="586b1-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="586b1-232">Sito aziendale di inoltro immagine tooyour Sign-on come amministratore.</span><span class="sxs-lookup"><span data-stu-id="586b1-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="586b1-233">Andare troppo**utenti e autorizzazioni** e selezionare **Crea utente SSO**.</span><span class="sxs-lookup"><span data-stu-id="586b1-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="586b1-235">Immettere hello **posta elettronica**, **nome**, **cognome**, e **aziendale** dell'utente hello desiderato tooprovision e gruppo di autorizzazioni select hello (ad esempio, SSO di base) che è il gruppo hello che può accedere solo tramite accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="586b1-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="586b1-237">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="586b1-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="586b1-238">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="586b1-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="586b1-239">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooImage inoltro.</span><span class="sxs-lookup"><span data-stu-id="586b1-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Assegna utente][200] 

<span data-ttu-id="586b1-241">**tooassign Britta Simon tooImage inoltro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="586b1-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="586b1-242">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="586b1-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="586b1-244">Nell'elenco di applicazioni hello, selezionare **inoltro immagine**.</span><span class="sxs-lookup"><span data-stu-id="586b1-244">In hello applications list, select **Image Relay**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="586b1-246">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="586b1-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="586b1-248">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="586b1-248">Click **Add** button.</span></span> <span data-ttu-id="586b1-249">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="586b1-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="586b1-251">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="586b1-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="586b1-252">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="586b1-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="586b1-253">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="586b1-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="586b1-254">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="586b1-254">Testing single sign-on</span></span>

<span data-ttu-id="586b1-255">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="586b1-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="586b1-256">Quando si fa clic su riquadro immagine inoltro hello in hello Pannello di accesso, è necessario ottenere l'applicazione di inoltro immagine tooyour automaticamente firmato in.</span><span class="sxs-lookup"><span data-stu-id="586b1-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="586b1-257">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="586b1-257">Additional resources</span></span>

* [<span data-ttu-id="586b1-258">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="586b1-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="586b1-259">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="586b1-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Adobe Creative Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Cloud creativi Adobe.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="02cc8-103">Esercitazione: Integrazione di Azure Active Directory con Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="02cc8-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="02cc8-104">In questa esercitazione, è illustrato come toointegrate Adobe Creative Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02cc8-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02cc8-105">Integrazione di Adobe Creative Cloud con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="02cc8-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="02cc8-106">È possibile controllare in Azure AD che ha accesso tooAdobe Cloud creativi</span><span class="sxs-lookup"><span data-stu-id="02cc8-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="02cc8-107">È possibile abilitare l'utenti tooautomatically get connesso tooAdobe Cloud creativi (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="02cc8-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02cc8-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="02cc8-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="02cc8-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02cc8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02cc8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02cc8-110">Prerequisites</span></span>

<span data-ttu-id="02cc8-111">integrazione di Azure AD con Cloud creativi Adobe tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="02cc8-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="02cc8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02cc8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02cc8-113">Sottoscrizione di Adobe Creative Cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="02cc8-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02cc8-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="02cc8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02cc8-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="02cc8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02cc8-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="02cc8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="02cc8-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02cc8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02cc8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="02cc8-118">Scenario description</span></span>
<span data-ttu-id="02cc8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="02cc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02cc8-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="02cc8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02cc8-121">Aggiunta di Cloud creativi Adobe dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="02cc8-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="02cc8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02cc8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="02cc8-123">Aggiunta di Cloud creativi Adobe dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="02cc8-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="02cc8-124">integrazione hello tooconfigure di Adobe Creative Cloud in Azure AD, è necessario tooadd Cloud creativi Adobe dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="02cc8-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="02cc8-125">**tooadd Adobe Cloud creativi dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="02cc8-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="02cc8-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="02cc8-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02cc8-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="02cc8-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="02cc8-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="02cc8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="02cc8-133">Nella casella di ricerca hello, digitare **Cloud creativi Adobe**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="02cc8-135">Nel riquadro dei risultati hello, selezionare **Cloud creativi Adobe**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="02cc8-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02cc8-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02cc8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02cc8-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Adobe Creative Cloud con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="02cc8-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02cc8-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Cloud creativi Adobe è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02cc8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="02cc8-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Cloud creativi Adobe deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="02cc8-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="02cc8-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nel Cloud creativi Adobe.</span><span class="sxs-lookup"><span data-stu-id="02cc8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="02cc8-142">tooconfigure e test Azure single sign-on AD Adobe Creative cloud, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="02cc8-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="02cc8-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="02cc8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="02cc8-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02cc8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02cc8-145">**[Creazione di un utente test Cloud creativi Adobe](#creating-an-adobe-creative-cloud-test-user)**  -toohave un equivalente di Britta Simon in Adobe Creative Cloud rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="02cc8-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="02cc8-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="02cc8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02cc8-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="02cc8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02cc8-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02cc8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02cc8-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione Cloud creativi Adobe.</span><span class="sxs-lookup"><span data-stu-id="02cc8-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="02cc8-150">**tooconfigure AD Azure single sign-on con Cloud creativi Adobe, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="02cc8-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="02cc8-151">Nel portale di gestione di Azure hello in hello **Cloud creativi Adobe** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="02cc8-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="02cc8-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="02cc8-155">In hello **Adobe Creative Cloud dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="02cc8-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="02cc8-157">a.</span><span class="sxs-lookup"><span data-stu-id="02cc8-157">a.</span></span> <span data-ttu-id="02cc8-158">In hello **identificatore** casella di testo, tipo di valore hello di:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="02cc8-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="02cc8-159">b.</span><span class="sxs-lookup"><span data-stu-id="02cc8-159">b.</span></span> <span data-ttu-id="02cc8-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="02cc8-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02cc8-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="02cc8-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="02cc8-162">È necessario tooupdate questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="02cc8-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="02cc8-163">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="02cc8-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="02cc8-164">Se è necessario un utente toocreate manualmente, è necessario team di supporto Cloud creativi Adobe toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="02cc8-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="02cc8-165">In hello **Adobe Creative Cloud dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="02cc8-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="02cc8-167">a.</span><span class="sxs-lookup"><span data-stu-id="02cc8-167">a.</span></span> <span data-ttu-id="02cc8-168">Fare clic su hello **Mostra URL impostazioni avanzate** opzione</span><span class="sxs-lookup"><span data-stu-id="02cc8-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="02cc8-169">b.</span><span class="sxs-lookup"><span data-stu-id="02cc8-169">b.</span></span> <span data-ttu-id="02cc8-170">In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="02cc8-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="02cc8-171">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="02cc8-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="02cc8-173">In hello **configurazione Cloud creativi Adobe** fare clic su **Cloud creativi Adobe configurare** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="02cc8-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="02cc8-174">Copiare hello **Id entità SAML** e **SAML SSO Service URL** dalla sezione di riferimento rapido.</span><span class="sxs-lookup"><span data-stu-id="02cc8-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="02cc8-176">In una finestra del web browser, tenant Cloud creativi Adobe tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="02cc8-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="02cc8-177">Andare troppo**identità** hello riquadro di spostamento a sinistra e selezionare il dominio.</span><span class="sxs-lookup"><span data-stu-id="02cc8-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="02cc8-178">Eseguire quindi seguire i passaggi di hello **Single Sign in configurazione necessario** sezione.</span><span class="sxs-lookup"><span data-stu-id="02cc8-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="02cc8-179">![Impostazioni](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="02cc8-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="02cc8-180">Fare clic su **Sfoglia** hello tooupload scaricato certificato da Azure AD troppo**IDP Certificate**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="02cc8-181">In hello **IDP issuer** casella di testo, inserire il valore di hello di **Id entità SAML** che è stato copiato da **Configura sign-on** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="02cc8-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="02cc8-182">In hello **IDP Login URL** casella di testo, inserire il valore di hello di **SAML SSO Service URL** che è stato copiato da **Configura sign-on** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="02cc8-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="02cc8-183">Selezionare **HTTP - Redirect** (HTTP - Reindirizzamento) per **IDP Binding** (Binding IDP).</span><span class="sxs-lookup"><span data-stu-id="02cc8-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="02cc8-184">Selezionare **Email Address** (Indirizzo di posta elettronica) per **User Login Setting** (Impostazione accesso utente).</span><span class="sxs-lookup"><span data-stu-id="02cc8-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="02cc8-185">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="02cc8-185">Click **Save** button.</span></span>

15. <span data-ttu-id="02cc8-186">dashboard Hello mostrerà ora hello XML **"Scaricare i metadati"** file.</span><span class="sxs-lookup"><span data-stu-id="02cc8-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="02cc8-187">che contiene l'URL EntityDescriptor e l'URL AssertionConsumerService di Adobe.</span><span class="sxs-lookup"><span data-stu-id="02cc8-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="02cc8-188">Aprire file hello e configurarli nel hello applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02cc8-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="02cc8-191">a.</span><span class="sxs-lookup"><span data-stu-id="02cc8-191">a.</span></span> <span data-ttu-id="02cc8-192">Hello utilizzare EntityDescriptor valore Adobe fornita per **identificatore** su hello **Configura impostazioni App** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="02cc8-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="02cc8-193">b.</span><span class="sxs-lookup"><span data-stu-id="02cc8-193">b.</span></span> <span data-ttu-id="02cc8-194">Hello utilizzare AssertionConsumerService valore Adobe fornita per **URL di risposta** su hello **Configura impostazioni App** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="02cc8-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02cc8-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="02cc8-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="02cc8-196">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="02cc8-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="02cc8-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="02cc8-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="02cc8-199">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="02cc8-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02cc8-201">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="02cc8-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02cc8-203">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="02cc8-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02cc8-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="02cc8-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02cc8-207">a.</span><span class="sxs-lookup"><span data-stu-id="02cc8-207">a.</span></span> <span data-ttu-id="02cc8-208">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02cc8-209">b.</span><span class="sxs-lookup"><span data-stu-id="02cc8-209">b.</span></span> <span data-ttu-id="02cc8-210">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02cc8-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02cc8-211">c.</span><span class="sxs-lookup"><span data-stu-id="02cc8-211">c.</span></span> <span data-ttu-id="02cc8-212">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="02cc8-213">d.</span><span class="sxs-lookup"><span data-stu-id="02cc8-213">d.</span></span> <span data-ttu-id="02cc8-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="02cc8-215">Creare un utente test di Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="02cc8-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="02cc8-216">In ordine tooenable Azure AD utenti toolog in Cloud creativi Adobe, è necessario eseguirne il provisioning in Cloud creativi Adobe.</span><span class="sxs-lookup"><span data-stu-id="02cc8-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="02cc8-217">Nel caso di hello di Cloud creativi Adobe, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="02cc8-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="02cc8-218">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="02cc8-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="02cc8-219">Accedi tooyour sito della società Adobe Creative Cloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="02cc8-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="02cc8-220">Fare clic su **Persone**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-220">Click **People**.</span></span>

    <span data-ttu-id="02cc8-221">![Persone](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="02cc8-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="02cc8-222">Fare clic su **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-222">Click **Invite User**.</span></span>

    <span data-ttu-id="02cc8-223">![Invitare utenti](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invitare utenti")</span><span class="sxs-lookup"><span data-stu-id="02cc8-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="02cc8-224">In hello **Invite People** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="02cc8-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="02cc8-225">![Invitare persone](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="02cc8-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="02cc8-226">a.</span><span class="sxs-lookup"><span data-stu-id="02cc8-226">a.</span></span> <span data-ttu-id="02cc8-227">In hello **posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02cc8-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="02cc8-228">b.</span><span class="sxs-lookup"><span data-stu-id="02cc8-228">b.</span></span> <span data-ttu-id="02cc8-229">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="02cc8-230">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="02cc8-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="02cc8-231">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="02cc8-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="02cc8-232">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooAdobe accesso Cloud creativi.</span><span class="sxs-lookup"><span data-stu-id="02cc8-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="02cc8-234">**tooassign Britta Simon tooAdobe Cloud creativi, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="02cc8-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="02cc8-235">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="02cc8-237">Nell'elenco di applicazioni hello, selezionare **Cloud creativi Adobe**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="02cc8-239">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="02cc8-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-241">Click **Add** button.</span></span> <span data-ttu-id="02cc8-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="02cc8-244">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="02cc8-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="02cc8-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02cc8-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="02cc8-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02cc8-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="02cc8-247">Testing single sign-on</span></span>

<span data-ttu-id="02cc8-248">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="02cc8-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="02cc8-249">Quando si fa clic su riquadro Cloud creativi Adobe hello in hello Pannello di accesso, è necessario ottenere l'applicazione Cloud creativi Adobe tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="02cc8-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="02cc8-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="02cc8-250">Additional resources</span></span>

* [<span data-ttu-id="02cc8-251">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02cc8-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02cc8-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02cc8-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png
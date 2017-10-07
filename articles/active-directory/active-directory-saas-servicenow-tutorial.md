---
title: 'Esercitazione: Integrazione di Azure Active Directory con ServiceNow | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ServiceNow e ServiceNow Express.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="96b7b-103">Esercitazione: Integrazione di Azure Active Directory con ServiceNow</span><span class="sxs-lookup"><span data-stu-id="96b7b-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="96b7b-104">In questa esercitazione, è illustrato come toointegrate ServiceNow ed Express di ServiceNow con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96b7b-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96b7b-105">Integrazione di ServiceNow e ServiceNow Express con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="96b7b-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="96b7b-106">È possibile controllare in Azure AD che ha accesso tooServiceNow e ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="96b7b-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="96b7b-107">È possibile abilitare l'utenti tooautomatically get connesso tooServiceNow e ServiceNow Express (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="96b7b-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="96b7b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="96b7b-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="96b7b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96b7b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96b7b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="96b7b-110">Prerequisites</span></span>
<span data-ttu-id="96b7b-111">integrazione di Azure AD con ServiceNow e ServiceNow Express tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="96b7b-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="96b7b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96b7b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="96b7b-113">Per ServiceNow, un'istanza o un tenant di ServiceNow, versione Calgary o successiva</span><span class="sxs-lookup"><span data-stu-id="96b7b-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="96b7b-114">Per ServiceNow Express, un'istanza di ServiceNow Express, versione Helsinki o successiva</span><span class="sxs-lookup"><span data-stu-id="96b7b-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="96b7b-115">tenant di ServiceNow Hello deve avere hello [più Provider Single Sign nel plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) abilitato.</span><span class="sxs-lookup"><span data-stu-id="96b7b-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="96b7b-116">Questa operazione può essere eseguita [inviando una richiesta di servizio](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="96b7b-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="96b7b-117">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="96b7b-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="96b7b-118">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="96b7b-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="96b7b-119">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="96b7b-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="96b7b-120">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96b7b-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96b7b-121">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="96b7b-121">Scenario description</span></span>
<span data-ttu-id="96b7b-122">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="96b7b-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96b7b-123">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="96b7b-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96b7b-124">Aggiunta di ServiceNow dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="96b7b-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="96b7b-125">Configurazione e test dell'accesso Single Sign-On di Azure AD per ServiceNow o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="96b7b-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="96b7b-126">Aggiunta di ServiceNow dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="96b7b-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="96b7b-127">integrazione hello tooconfigure di ServiceNow o ServiceNow Express in Azure AD, è necessario tooadd ServiceNow dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="96b7b-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="96b7b-128">**tooadd ServiceNow dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="96b7b-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96b7b-129">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="96b7b-131">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="96b7b-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="96b7b-132">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applicazioni][2]
4. <span data-ttu-id="96b7b-134">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="96b7b-136">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applicazioni][4]
6. <span data-ttu-id="96b7b-138">Nella casella di ricerca hello, digitare **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="96b7b-140">Nel riquadro risultati hello selezionare **ServiceNow**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96b7b-142">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="96b7b-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96b7b-143">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ServiceNow o ServiceNow Express in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="96b7b-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96b7b-144">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ServiceNow è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96b7b-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="96b7b-145">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ServiceNow richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="96b7b-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="96b7b-146">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="96b7b-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="96b7b-147">tooconfigure e test Azure single sign-on AD con ServiceNow, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="96b7b-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96b7b-148">**[Configurazione di Azure AD Single Sign-On per ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="96b7b-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96b7b-149">**[Configurazione di Azure AD Single Sign-On per ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="96b7b-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="96b7b-150">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96b7b-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="96b7b-151">**[Creazione di un utente test ServiceNow](#creating-a-servicenow-test-user)**  -toohave un equivalente di Britta Simon in ServiceNow che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="96b7b-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="96b7b-152">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="96b7b-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="96b7b-153">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="96b7b-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="96b7b-154">Se si desidera tooconfigure ServiceNow omettere il passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="96b7b-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="96b7b-155">Analogamente, se si desidera tooconfigure ServiceNow Express omettere il passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="96b7b-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="96b7b-156">Configurazione dell'accesso Single Sign-On per ServiceNow</span><span class="sxs-lookup"><span data-stu-id="96b7b-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="96b7b-157">Nel portale classico hello Azure AD su hello **ServiceNow** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo .</span><span class="sxs-lookup"><span data-stu-id="96b7b-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="96b7b-158">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="96b7b-159">In hello **come si sarebbe ad esempio utenti toosign su tooServiceNow** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="96b7b-160">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="96b7b-161">In hello **Configura impostazioni App** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="96b7b-162">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="96b7b-163">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-163">a.</span></span> <span data-ttu-id="96b7b-164">in hello **ServiceNow URL di accesso** casella di testo digitare l'URL usato dall'applicazione ServiceNow tooyour toosign-on agli utenti il modello di hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="96b7b-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="96b7b-165">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-165">b.</span></span> <span data-ttu-id="96b7b-166">In hello **identificatore** casella di testo digitare l'URL usato dall'applicazione ServiceNow tooyour toosign-on agli utenti il modello di hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="96b7b-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="96b7b-167">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-167">c.</span></span> <span data-ttu-id="96b7b-168">Fare clic su **Avanti**</span><span class="sxs-lookup"><span data-stu-id="96b7b-168">Click **Next**</span></span>

4. <span data-ttu-id="96b7b-169">Azure AD toohave automaticamente configurare ServiceNow per l'autenticazione basata su SAML, immettere il nome dell'istanza ServiceNow, nome utente amministratore e la password di amministratore in hello **configura automaticamente l'accesso single sign-on** formato e fare clic su  *Configurare*.</span><span class="sxs-lookup"><span data-stu-id="96b7b-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="96b7b-170">Si noti che nome utente amministratore hello fornito deve avere hello **security_admin** ruolo assegnato in ServiceNow per questo toowork.</span><span class="sxs-lookup"><span data-stu-id="96b7b-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="96b7b-171">In caso contrario, toomanually configurare ServiceNow toouse Azure AD come provider di identità SAML, fare clic su **configurare manualmente un'applicazione hello per single sign-on**, quindi fare clic su **Avanti** e hello completo procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="96b7b-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="96b7b-172">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="96b7b-173">In hello **Configura accesso single sign-on in ServiceNow** pagina, fare clic su **Scarica certificato**, salvare il file di certificato hello in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="96b7b-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="96b7b-174">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="96b7b-175">Sign-on tooyour ServiceNow applicazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="96b7b-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="96b7b-176">Attivare hello *- integrazione di più Provider Single Sign-On Installer* plug-in seguendo hello passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="96b7b-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="96b7b-177">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-177">a.</span></span> <span data-ttu-id="96b7b-178">Nel riquadro di spostamento hello sul lato sinistro di hello, andare troppo**definizione sistema** sezione e quindi fare clic su **plug-in**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="96b7b-179">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Attivare il plug-in")</span><span class="sxs-lookup"><span data-stu-id="96b7b-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="96b7b-180">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-180">b.</span></span> <span data-ttu-id="96b7b-181">Cercare *Integration - Multiple Provider Single Sign-On Installer*.</span><span class="sxs-lookup"><span data-stu-id="96b7b-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="96b7b-182">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Attivare il plug-in")</span><span class="sxs-lookup"><span data-stu-id="96b7b-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="96b7b-183">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-183">c.</span></span> <span data-ttu-id="96b7b-184">Selezionare i plug-in hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-184">Select hello plugin.</span></span> <span data-ttu-id="96b7b-185">Fare clic e selezionare **Activate/Upgrade** (Attiva/Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="96b7b-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="96b7b-186">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-186">d.</span></span> <span data-ttu-id="96b7b-187">Fare clic su hello **attiva** pulsante.</span><span class="sxs-lookup"><span data-stu-id="96b7b-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="96b7b-188">Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="96b7b-189">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="96b7b-190">In hello **più proprietà del Provider SSO** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="96b7b-191">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="96b7b-192">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-192">a.</span></span> <span data-ttu-id="96b7b-193">Per **Enable multiple provider SSO** selezionare **Yes**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="96b7b-194">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-194">b.</span></span> <span data-ttu-id="96b7b-195">Come **abilita la registrazione di debug ottenuta hello più provider SSO integration**selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="96b7b-196">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-196">c.</span></span> <span data-ttu-id="96b7b-197">In **tabella campo hello utente hello...**  casella tipo **nome_utente**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="96b7b-198">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-198">d.</span></span> <span data-ttu-id="96b7b-199">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-199">Click **Save**.</span></span>

10. <span data-ttu-id="96b7b-200">Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **certificati x509**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="96b7b-201">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="96b7b-202">In hello **certificati x. 509** finestra di dialogo, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="96b7b-203">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="96b7b-204">In hello **certificati x. 509** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="96b7b-205">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="96b7b-206">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-206">a.</span></span> <span data-ttu-id="96b7b-207">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-207">Click **New**.</span></span>
    
     <span data-ttu-id="96b7b-208">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-208">b.</span></span> <span data-ttu-id="96b7b-209">In hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="96b7b-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="96b7b-210">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-210">c.</span></span> <span data-ttu-id="96b7b-211">Selezionare **Active**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-211">Select **Active**.</span></span>
    
     <span data-ttu-id="96b7b-212">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-212">d.</span></span> <span data-ttu-id="96b7b-213">Per **Format** selezionare **PEM**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="96b7b-214">e.</span><span class="sxs-lookup"><span data-stu-id="96b7b-214">e.</span></span> <span data-ttu-id="96b7b-215">Per **Type** selezionare **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="96b7b-216">f.</span><span class="sxs-lookup"><span data-stu-id="96b7b-216">f.</span></span> <span data-ttu-id="96b7b-217">Aprire il certificato con codificata base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato PEM** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="96b7b-218">g.</span><span class="sxs-lookup"><span data-stu-id="96b7b-218">g.</span></span> <span data-ttu-id="96b7b-219">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-219">Click **Update**.</span></span>

13. <span data-ttu-id="96b7b-220">Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="96b7b-221">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="96b7b-222">In hello **provider di identità** finestra di dialogo, fare clic su **New**:</span><span class="sxs-lookup"><span data-stu-id="96b7b-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="96b7b-223">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="96b7b-224">In hello **provider di identità** finestra di dialogo, fare clic su **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="96b7b-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="96b7b-225">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="96b7b-226">Nella finestra di dialogo Proprietà Update1 SAML2 hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="96b7b-227">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="96b7b-228">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-228">a.</span></span> <span data-ttu-id="96b7b-229">in hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="96b7b-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="96b7b-230">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-230">b.</span></span> <span data-ttu-id="96b7b-231">In hello **campo utente** casella tipo **posta elettronica** o **nome_utente**, a seconda di quale campo viene usato toouniquely identificare gli utenti nella distribuzione di ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="96b7b-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="96b7b-232">Puoi tooemit configurazione Azure AD l'ID utente hello Azure AD (nome dell'entità utente) o hello indirizzo di posta elettronica come hello identificatore univoco nel token SAML hello da passare toohello **ServiceNow > attributi > Single Sign-On** sezione Hello portale di Azure classico e mapping hello desiderato campo toohello **nameidentifier** attributo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="96b7b-233">il valore di Hello archiviato per l'attributo selezionato hello in Azure Active Directory (ad esempio nome dell'entità utente) deve corrispondere il valore di hello archiviato in ServiceNow per il campo hello immesso (ad esempio nome_utente)</span><span class="sxs-lookup"><span data-stu-id="96b7b-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="96b7b-234">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-234">c.</span></span> <span data-ttu-id="96b7b-235">Nel portale classico di hello Azure AD copiare hello **ID Provider di identità** valore e quindi incollarlo hello **Identity Provider URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="96b7b-236">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-236">d.</span></span> <span data-ttu-id="96b7b-237">Nel portale classico di hello Azure AD copiare hello **URL richiesta di autenticazione** valore e quindi incollarlo hello **AuthnRequest del Provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="96b7b-238">e.</span><span class="sxs-lookup"><span data-stu-id="96b7b-238">e.</span></span> <span data-ttu-id="96b7b-239">Nel portale classico di hello Azure AD copiare hello **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **SingleLogoutRequest Provider identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="96b7b-240">f.</span><span class="sxs-lookup"><span data-stu-id="96b7b-240">f.</span></span> <span data-ttu-id="96b7b-241">In hello **ServiceNow Homepage** casella di testo, digitare l'URL della home page di istanza di ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96b7b-242">Home page dell'istanza ServiceNow Hello è una concatenazione del **URL tenant ServieNow** e **/navpage.do** (ad esempio:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="96b7b-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="96b7b-243">g.</span><span class="sxs-lookup"><span data-stu-id="96b7b-243">g.</span></span> <span data-ttu-id="96b7b-244">In hello **ID entità o dell'autorità di certificazione** casella di testo, digitare l'URL del tenant di ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="96b7b-245">h.</span><span class="sxs-lookup"><span data-stu-id="96b7b-245">h.</span></span> <span data-ttu-id="96b7b-246">In hello **URL pubblico** casella di testo, digitare l'URL del tenant di ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="96b7b-247">i.</span><span class="sxs-lookup"><span data-stu-id="96b7b-247">i.</span></span> <span data-ttu-id="96b7b-248">In hello **protocollo di associazione per hello dell'IDP SingleLogoutRequest** casella tipo **urn: oasis: nomi: tc: SAML:2.0:bindings:HTTP-reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="96b7b-249">j.</span><span class="sxs-lookup"><span data-stu-id="96b7b-249">j.</span></span> <span data-ttu-id="96b7b-250">Nella casella di testo criteri NameID hello, digitare **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: non specificato**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="96b7b-251">k.</span><span class="sxs-lookup"><span data-stu-id="96b7b-251">k.</span></span> <span data-ttu-id="96b7b-252">Fare clic su **Create an AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="96b7b-253">l.</span><span class="sxs-lookup"><span data-stu-id="96b7b-253">l.</span></span> <span data-ttu-id="96b7b-254">In hello **metodo AuthnContextClassRef**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="96b7b-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="96b7b-255">Questa operazione è necessaria soltanto per le organizzazioni basate solo su cloud.</span><span class="sxs-lookup"><span data-stu-id="96b7b-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="96b7b-256">Se si usa AD FS o MFA in locale per l'autenticazione, non è necessario configurare questo valore.</span><span class="sxs-lookup"><span data-stu-id="96b7b-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="96b7b-257">m.</span><span class="sxs-lookup"><span data-stu-id="96b7b-257">m.</span></span> <span data-ttu-id="96b7b-258">Nella casella di testo **Clock Skew** digitare **60**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="96b7b-259">n.</span><span class="sxs-lookup"><span data-stu-id="96b7b-259">n.</span></span> <span data-ttu-id="96b7b-260">Per **Single Sign On Script** selezionare **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="96b7b-261">o.</span><span class="sxs-lookup"><span data-stu-id="96b7b-261">o.</span></span> <span data-ttu-id="96b7b-262">Come **x509 certificato**, selezionare il certificato di hello è stato creato nel passaggio precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="96b7b-263">p.</span><span class="sxs-lookup"><span data-stu-id="96b7b-263">p.</span></span> <span data-ttu-id="96b7b-264">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="96b7b-265">Nel portale classico hello Azure AD, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="96b7b-266">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="96b7b-267">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="96b7b-268">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="96b7b-269">Configurazione dell'accesso Single Sign-On per ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="96b7b-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="96b7b-270">Nel portale classico hello Azure AD su hello **ServiceNow** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo .</span><span class="sxs-lookup"><span data-stu-id="96b7b-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="96b7b-271">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="96b7b-272">In hello **come si sarebbe ad esempio utenti toosign su tooServiceNow** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="96b7b-273">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="96b7b-274">In hello **Configura impostazioni App** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="96b7b-275">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="96b7b-276">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-276">a.</span></span> <span data-ttu-id="96b7b-277">in hello **ServiceNow URL di accesso** casella di testo digitare l'URL usato dall'applicazione ServiceNow tooyour toosign-on agli utenti il modello di hello: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="96b7b-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="96b7b-278">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-278">b.</span></span> <span data-ttu-id="96b7b-279">In hello **URL autorità di certificazione** , digitare l'URL usato dagli utenti toosign-on tooyour ServiceNow applicazione hello modello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="96b7b-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="96b7b-280">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-280">c.</span></span> <span data-ttu-id="96b7b-281">Fare clic su **Avanti**</span><span class="sxs-lookup"><span data-stu-id="96b7b-281">Click **Next**</span></span>

4. <span data-ttu-id="96b7b-282">Fare clic su **configurare manualmente un'applicazione hello per single sign-on**, quindi fare clic su **Avanti** e hello completo seguendo i passaggi.</span><span class="sxs-lookup"><span data-stu-id="96b7b-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="96b7b-283">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="96b7b-284">In hello **Configura accesso single sign-on in ServiceNow** pagina, fare clic su **Scarica certificato**, salvare il file di certificato hello in locale nel computer e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="96b7b-285">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="96b7b-286">Sign-on tooyour ServiceNow Express applicazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="96b7b-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="96b7b-287">Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="96b7b-288">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="96b7b-289">In hello **Single Sign-On** finestra di dialogo, fare clic sull'icona di configurazione hello in alto hello destro e imposta hello le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="96b7b-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="96b7b-290">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="96b7b-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="96b7b-291">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-291">a.</span></span> <span data-ttu-id="96b7b-292">Attiva/disattiva **abilitare più provider SSO** toohello destra.</span><span class="sxs-lookup"><span data-stu-id="96b7b-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="96b7b-293">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-293">b.</span></span> <span data-ttu-id="96b7b-294">Attiva/disattiva **debug abilitare la registrazione per hello più provider SSO integration** toohello destra.</span><span class="sxs-lookup"><span data-stu-id="96b7b-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="96b7b-295">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-295">c.</span></span> <span data-ttu-id="96b7b-296">In **tabella campo hello utente hello...**  casella tipo **nome_utente**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="96b7b-297">In hello **Single Sign-On** finestra di dialogo, fare clic su **Aggiungi nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="96b7b-298">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="96b7b-299">In hello **certificati x. 509** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="96b7b-300">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="96b7b-301">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-301">a.</span></span> <span data-ttu-id="96b7b-302">In hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="96b7b-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="96b7b-303">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-303">b.</span></span> <span data-ttu-id="96b7b-304">Selezionare **Active**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-304">Select **Active**.</span></span>
    
    <span data-ttu-id="96b7b-305">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-305">c.</span></span> <span data-ttu-id="96b7b-306">Per **Format** selezionare **PEM**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="96b7b-307">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-307">d.</span></span> <span data-ttu-id="96b7b-308">Per **Type** selezionare **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="96b7b-309">e.</span><span class="sxs-lookup"><span data-stu-id="96b7b-309">e.</span></span> <span data-ttu-id="96b7b-310">Creare un file con codifica Base64 dal certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="96b7b-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="96b7b-311">Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="96b7b-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="96b7b-312">f.</span><span class="sxs-lookup"><span data-stu-id="96b7b-312">f.</span></span> <span data-ttu-id="96b7b-313">Aprire il certificato con codificata base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato PEM** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="96b7b-314">g.</span><span class="sxs-lookup"><span data-stu-id="96b7b-314">g.</span></span> <span data-ttu-id="96b7b-315">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-315">Click **Update**.</span></span>
11. <span data-ttu-id="96b7b-316">In hello **Single Sign-On** finestra di dialogo, fare clic su **aggiungere nuovo IdP**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="96b7b-317">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="96b7b-318">In hello **Aggiungi nuovo Provider di identità** finestra di dialogo, in **configurare Provider di identità**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="96b7b-319">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="96b7b-320">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-320">a.</span></span> <span data-ttu-id="96b7b-321">in hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="96b7b-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="96b7b-322">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-322">b.</span></span> <span data-ttu-id="96b7b-323">Nel portale classico di hello Azure AD copiare hello **ID Provider di identità** valore e quindi incollarlo hello **Identity Provider URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="96b7b-324">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-324">c.</span></span> <span data-ttu-id="96b7b-325">Nel portale classico di hello Azure AD copiare hello **URL richiesta di autenticazione** valore e quindi incollarlo hello **AuthnRequest del Provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="96b7b-326">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-326">d.</span></span> <span data-ttu-id="96b7b-327">Nel portale classico di hello Azure AD copiare hello **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **SingleLogoutRequest Provider identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="96b7b-328">e.</span><span class="sxs-lookup"><span data-stu-id="96b7b-328">e.</span></span> <span data-ttu-id="96b7b-329">Come **Identity Provider Certificate**, selezionare il certificato di hello è stato creato nel passaggio precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="96b7b-330">Fare clic su **impostazioni avanzate**e in **proprietà Provider di identità aggiuntive**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="96b7b-331">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="96b7b-332">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-332">a.</span></span> <span data-ttu-id="96b7b-333">In hello **protocollo di associazione per hello dell'IDP SingleLogoutRequest** casella tipo **urn: oasis: nomi: tc: SAML:2.0:bindings:HTTP-reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="96b7b-334">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-334">b.</span></span> <span data-ttu-id="96b7b-335">In hello **criteri NameID** casella tipo **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: non specificato**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="96b7b-336">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-336">c.</span></span> <span data-ttu-id="96b7b-337">In hello **metodo AuthnContextClassRef**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="96b7b-338">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-338">d.</span></span> <span data-ttu-id="96b7b-339">Fare clic su **Create an AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="96b7b-340">In **ulteriori proprietà Provider del servizio**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="96b7b-341">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="96b7b-342">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-342">a.</span></span> <span data-ttu-id="96b7b-343">In hello **ServiceNow Homepage** casella di testo, digitare l'URL della home page di istanza di ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="96b7b-344">Home page dell'istanza ServiceNow Hello è una concatenazione del **URL tenant ServieNow** e **/navpage.do** (ad esempio: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="96b7b-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="96b7b-345">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-345">b.</span></span> <span data-ttu-id="96b7b-346">In hello **ID entità o dell'autorità di certificazione** casella di testo, digitare l'URL del tenant di ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="96b7b-347">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-347">c.</span></span> <span data-ttu-id="96b7b-348">In hello **URI destinatario** casella di testo, digitare l'URL del tenant di ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="96b7b-349">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-349">d.</span></span> <span data-ttu-id="96b7b-350">Nella casella di testo **Clock Skew** digitare **60**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="96b7b-351">e.</span><span class="sxs-lookup"><span data-stu-id="96b7b-351">e.</span></span> <span data-ttu-id="96b7b-352">In hello **campo utente** casella tipo **posta elettronica** o **nome_utente**, a seconda di quale campo viene usato toouniquely identificare gli utenti nella distribuzione di ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="96b7b-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="96b7b-353">Puoi tooemit configurazione Azure AD l'ID utente hello Azure AD (nome dell'entità utente) o hello indirizzo di posta elettronica come hello identificatore univoco nel token SAML hello da passare toohello **ServiceNow > attributi > Single Sign-On** sezione Hello portale di Azure classico e mapping hello desiderato campo toohello **nameidentifier** attributo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="96b7b-354">il valore di Hello archiviato per l'attributo selezionato hello in Azure Active Directory (ad esempio nome dell'entità utente) deve corrispondere il valore di hello archiviato in ServiceNow per il campo hello immesso (ad esempio nome_utente)</span><span class="sxs-lookup"><span data-stu-id="96b7b-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="96b7b-355">f.</span><span class="sxs-lookup"><span data-stu-id="96b7b-355">f.</span></span> <span data-ttu-id="96b7b-356">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-356">Click **Save**.</span></span> 

3. <span data-ttu-id="96b7b-357">Nel portale classico hello Azure AD, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="96b7b-358">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="96b7b-359">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="96b7b-360">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96b7b-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="96b7b-361">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="96b7b-361">Configuring user provisioning</span></span>
<span data-ttu-id="96b7b-362">obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooServiceNow.</span><span class="sxs-lookup"><span data-stu-id="96b7b-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="96b7b-363">tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="96b7b-364">Nel portale di gestione di Azure classico hello, su hello **ServiceNow** pagina di integrazione dell'applicazione, fare clic su **Configura provisioning utente**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="96b7b-365">![Provisioning degli utenti](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Provisioning degli utenti")</span><span class="sxs-lookup"><span data-stu-id="96b7b-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="96b7b-366">In hello **immettere i ServiceNow credenziali tooenable il provisioning utente automatico** fornire hello le impostazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="96b7b-367">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-367">a.</span></span> <span data-ttu-id="96b7b-368">In hello **nome istanza ServiceNow** casella di testo Nome istanza ServiceNow hello del tipo.</span><span class="sxs-lookup"><span data-stu-id="96b7b-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="96b7b-369">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-369">b.</span></span> <span data-ttu-id="96b7b-370">In hello **nome utente amministratore ServiceNow** casella di testo Nome hello del tipo di account amministratore ServiceNow hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="96b7b-371">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-371">c.</span></span> <span data-ttu-id="96b7b-372">In hello **Password amministratore ServiceNow** casella di testo, digitare la password hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="96b7b-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="96b7b-373">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-373">d.</span></span> <span data-ttu-id="96b7b-374">Fare clic su **convalidare** tooverify la configurazione.</span><span class="sxs-lookup"><span data-stu-id="96b7b-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="96b7b-375">e.</span><span class="sxs-lookup"><span data-stu-id="96b7b-375">e.</span></span> <span data-ttu-id="96b7b-376">Fare clic su hello **Avanti** hello tooopen pulsante **passaggi successivi** pagina.</span><span class="sxs-lookup"><span data-stu-id="96b7b-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="96b7b-377">f.</span><span class="sxs-lookup"><span data-stu-id="96b7b-377">f.</span></span> <span data-ttu-id="96b7b-378">Se si desidera tooprovision applicazione di toothis tutti gli utenti, selezionare "**esegue automaticamente il provisioning di tutti gli account utente in un'applicazione hello directory toothis**".</span><span class="sxs-lookup"><span data-stu-id="96b7b-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="96b7b-379">![Passaggi successivi](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Passaggi successivi")</span><span class="sxs-lookup"><span data-stu-id="96b7b-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="96b7b-380">g.</span><span class="sxs-lookup"><span data-stu-id="96b7b-380">g.</span></span> <span data-ttu-id="96b7b-381">In hello **passaggi successivi** pagina, fare clic su **completa** toosave la configurazione.</span><span class="sxs-lookup"><span data-stu-id="96b7b-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96b7b-382">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="96b7b-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="96b7b-383">In questa sezione creare un utente test nel portale classico di hello chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96b7b-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="96b7b-385">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="96b7b-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96b7b-386">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="96b7b-388">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="96b7b-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="96b7b-389">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96b7b-391">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="96b7b-393">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="96b7b-395">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-395">a.</span></span> <span data-ttu-id="96b7b-396">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="96b7b-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="96b7b-397">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-397">b.</span></span> <span data-ttu-id="96b7b-398">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="96b7b-399">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-399">c.</span></span> <span data-ttu-id="96b7b-400">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-400">Click **Next**.</span></span>

6. <span data-ttu-id="96b7b-401">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="96b7b-403">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-403">a.</span></span> <span data-ttu-id="96b7b-404">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="96b7b-405">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-405">b.</span></span> <span data-ttu-id="96b7b-406">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="96b7b-407">c.</span><span class="sxs-lookup"><span data-stu-id="96b7b-407">c.</span></span> <span data-ttu-id="96b7b-408">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="96b7b-409">d.</span><span class="sxs-lookup"><span data-stu-id="96b7b-409">d.</span></span> <span data-ttu-id="96b7b-410">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="96b7b-411">e.</span><span class="sxs-lookup"><span data-stu-id="96b7b-411">e.</span></span> <span data-ttu-id="96b7b-412">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-412">Click **Next**.</span></span>

7. <span data-ttu-id="96b7b-413">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="96b7b-415">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96b7b-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="96b7b-417">a.</span><span class="sxs-lookup"><span data-stu-id="96b7b-417">a.</span></span> <span data-ttu-id="96b7b-418">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="96b7b-419">b.</span><span class="sxs-lookup"><span data-stu-id="96b7b-419">b.</span></span> <span data-ttu-id="96b7b-420">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="96b7b-421">Creazione di un utente test di ServiceNow</span><span class="sxs-lookup"><span data-stu-id="96b7b-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="96b7b-422">In questa sezione viene creato un utente di nome Britta Simon in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="96b7b-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="96b7b-423">In questa sezione viene creato un utente di nome Britta Simon in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="96b7b-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="96b7b-424">Se non si conosce la modalità tooadd un utente nel ServiceNow o ServiceNow Express account, contattare il team di supporto di ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="96b7b-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96b7b-425">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="96b7b-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="96b7b-426">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooServiceNow proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="96b7b-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Assegna utente][200] 

<span data-ttu-id="96b7b-428">**tooassign Britta Simon tooServiceNow, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="96b7b-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="96b7b-429">Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="96b7b-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Assegna utente][201] 

2. <span data-ttu-id="96b7b-431">Nell'elenco di applicazioni hello, selezionare **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="96b7b-433">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Assegna utente][203] 

4. <span data-ttu-id="96b7b-435">Selezionare dall'elenco di tutti gli utenti di hello **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="96b7b-436">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="96b7b-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="96b7b-438">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="96b7b-438">Testing single sign-on</span></span>
<span data-ttu-id="96b7b-439">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="96b7b-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96b7b-440">Quando si fa clic su riquadro ServiceNow hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour ServiceNow applicazione.</span><span class="sxs-lookup"><span data-stu-id="96b7b-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96b7b-441">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="96b7b-441">Additional resources</span></span>
* [<span data-ttu-id="96b7b-442">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96b7b-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96b7b-443">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96b7b-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png

---
title: 'Esercitazione: Integrazione di Azure Active Directory con Huddle | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Huddle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="3ffd6-103">Esercitazione: Integrazione di Azure Active Directory con Huddle</span><span class="sxs-lookup"><span data-stu-id="3ffd6-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="3ffd6-104">In questa esercitazione, è illustrato come toointegrate Huddle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ffd6-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ffd6-105">Integrazione di Huddle con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3ffd6-106">È possibile controllare in Azure AD che ha accesso tooHuddle</span><span class="sxs-lookup"><span data-stu-id="3ffd6-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="3ffd6-107">È possibile abilitare l'utenti tooautomatically get connesso tooHuddle (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ffd6-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ffd6-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3ffd6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3ffd6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ffd6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ffd6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3ffd6-110">Prerequisites</span></span>

<span data-ttu-id="3ffd6-111">integrazione di Azure AD tooconfigure con Huddle, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="3ffd6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ffd6-113">Sottoscrizione di Huddle abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3ffd6-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ffd6-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ffd6-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ffd6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ffd6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ffd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ffd6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3ffd6-118">Scenario description</span></span>

<span data-ttu-id="3ffd6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ffd6-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ffd6-121">Aggiunta di Huddle dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3ffd6-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="3ffd6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ffd6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="3ffd6-123">Aggiunta di Huddle dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3ffd6-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="3ffd6-124">integrazione di hello tooconfigure di Huddle in Azure AD, è necessario tooadd Huddle dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3ffd6-125">**tooadd Huddle dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ffd6-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ffd6-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ffd6-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3ffd6-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3ffd6-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3ffd6-133">Nella casella di ricerca hello, digitare **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-133">In hello search box, type **Huddle**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="3ffd6-135">Nel riquadro dei risultati hello, selezionare **Huddle**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ffd6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ffd6-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3ffd6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Huddle usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ffd6-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3ffd6-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Huddle è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="3ffd6-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Huddle esigenze toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="3ffd6-141">In Huddle, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3ffd6-142">tooconfigure e prova AD Azure single sign-on con Huddle, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3ffd6-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="3ffd6-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="3ffd6-145">**[Creazione di un utente test Huddle](#creating-a-huddle-test-user)**  -toohave un equivalente di Britta Simon in Huddle che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="3ffd6-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="3ffd6-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ffd6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ffd6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ffd6-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Huddle.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="3ffd6-150">**tooconfigure AD Azure single sign-on con Huddle, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ffd6-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ffd6-151">Nel portale di Azure su hello hello **Huddle** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3ffd6-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="3ffd6-155">In hello **Huddle dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="3ffd6-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="3ffd6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ffd6-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="3ffd6-158">This value is not real.</span></span> <span data-ttu-id="3ffd6-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3ffd6-160">Contatto [team di supporto di Huddle Client](https://huddle.zendesk.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="3ffd6-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="3ffd6-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3ffd6-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ffd6-165">In hello **Huddle configurazione** fare clic su **configurare Huddle** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3ffd6-166">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="3ffd6-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="3ffd6-168">tooconfigure single sign-on sul lato di Huddle, è necessario hello toosend scaricato **certificato**, **SAML Single Sign-On Service URL**, e **ID entità SAML** troppo[Team di supporto di huddle Client](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="3ffd6-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="3ffd6-169">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="3ffd6-170">Accesso Single sign-on deve toobe abilitato dal team di supporto di Huddle hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="3ffd6-171">Si riceve una notifica quando hello configurazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="3ffd6-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="3ffd6-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3ffd6-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3ffd6-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ffd6-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ffd6-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ffd6-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="3ffd6-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3ffd6-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ffd6-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ffd6-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ffd6-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ffd6-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ffd6-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ffd6-187">a.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-187">a.</span></span> <span data-ttu-id="3ffd6-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ffd6-189">b.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-189">b.</span></span> <span data-ttu-id="3ffd6-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ffd6-191">c.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-191">c.</span></span> <span data-ttu-id="3ffd6-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3ffd6-193">d.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-193">d.</span></span> <span data-ttu-id="3ffd6-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="3ffd6-195">Creazione di un utente di test di Huddle</span><span class="sxs-lookup"><span data-stu-id="3ffd6-195">Creating a Huddle test user</span></span>

<span data-ttu-id="3ffd6-196">toolog agli utenti di Azure AD tooenable in tooHuddle, è necessario eseguirne il provisioning in Huddle.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="3ffd6-197">Nel caso di hello di Huddle, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="3ffd6-198">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ffd6-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ffd6-199">Accedi tooyour **Huddle** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="3ffd6-200">Fare clic su **Area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="3ffd6-201">Fare clic su **Persone \> Invite People (Invita persone)**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="3ffd6-202">![Persone](./media/active-directory-saas-huddle-tutorial/IC787838.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="3ffd6-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="3ffd6-203">In hello **creare un nuovo invito** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3ffd6-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3ffd6-204">![Nuovo invito](./media/active-directory-saas-huddle-tutorial/IC787839.png "Nuovo invito")</span><span class="sxs-lookup"><span data-stu-id="3ffd6-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="3ffd6-205">a.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-205">a.</span></span> <span data-ttu-id="3ffd6-206">In hello **scegliere un toojoin di persone tooinvite team** elenco, selezionare **team**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="3ffd6-207">b.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-207">b.</span></span> <span data-ttu-id="3ffd6-208">Hello tipo **indirizzo di posta elettronica** di un annuncio di Azure valido account desiderato tooprovision troppo**immettere indirizzo di posta elettronica per gli utenti desiderati tooinvite** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="3ffd6-209">c.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-209">c.</span></span> <span data-ttu-id="3ffd6-210">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="3ffd6-211">Hello account Azure AD titolare riceverà un messaggio di posta elettronica tra un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="3ffd6-212">È possibile usare qualsiasi altro Huddle utente account strumento di creazione o le API fornite da Huddle tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3ffd6-213">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ffd6-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3ffd6-214">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHuddle.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3ffd6-216">**tooassign Britta Simon tooHuddle, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ffd6-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ffd6-217">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3ffd6-219">Nell'elenco di applicazioni hello, selezionare **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-219">In hello applications list, select **Huddle**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="3ffd6-221">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3ffd6-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-223">Click **Add** button.</span></span> <span data-ttu-id="3ffd6-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3ffd6-226">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3ffd6-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ffd6-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ffd6-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3ffd6-229">Testing single sign-on</span></span>

<span data-ttu-id="3ffd6-230">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3ffd6-231">Quando si fa clic su riquadro Huddle hello in hello Pannello di accesso, è necessario ottenere automaticamente la pagina di accesso dell'applicazione di Huddle.</span><span class="sxs-lookup"><span data-stu-id="3ffd6-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="3ffd6-232">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ffd6-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ffd6-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3ffd6-233">Additional resources</span></span>

* [<span data-ttu-id="3ffd6-234">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ffd6-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ffd6-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ffd6-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png

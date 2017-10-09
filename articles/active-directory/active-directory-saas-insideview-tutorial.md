---
title: 'Esercitazione: Integrazione di Azure Active Directory con InsideView | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e InsideView.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="4bf0b-103">Esercitazione: Integrazione di Azure Active Directory con InsideView</span><span class="sxs-lookup"><span data-stu-id="4bf0b-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="4bf0b-104">In questa esercitazione, è illustrato come toointegrate InsideView con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4bf0b-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4bf0b-105">Integrazione di InsideView con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4bf0b-106">È possibile controllare in Azure AD che ha accesso tooInsideView</span><span class="sxs-lookup"><span data-stu-id="4bf0b-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="4bf0b-107">È possibile abilitare l'utenti tooautomatically get connesso tooInsideView (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bf0b-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4bf0b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4bf0b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4bf0b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4bf0b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bf0b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4bf0b-110">Prerequisites</span></span>

<span data-ttu-id="4bf0b-111">integrazione di Azure AD con InsideView tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="4bf0b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4bf0b-113">Sottoscrizione di InsideView abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4bf0b-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4bf0b-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4bf0b-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4bf0b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4bf0b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4bf0b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4bf0b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4bf0b-118">Scenario description</span></span>
<span data-ttu-id="4bf0b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4bf0b-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4bf0b-121">Aggiunta di InsideView dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4bf0b-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="4bf0b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bf0b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="4bf0b-123">Aggiunta di InsideView dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4bf0b-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="4bf0b-124">integrazione hello tooconfigure di InsideView nella tooAzure Active Directory, è necessario tooadd InsideView dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4bf0b-125">**tooadd InsideView dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4bf0b-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bf0b-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4bf0b-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4bf0b-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4bf0b-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4bf0b-133">Nella casella di ricerca hello, digitare **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-133">In hello search box, type **InsideView**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="4bf0b-135">Nel riquadro dei risultati hello, selezionare **InsideView**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4bf0b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bf0b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4bf0b-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con InsideView con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4bf0b-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4bf0b-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in InsideView è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="4bf0b-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in InsideView deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="4bf0b-141">In InsideView, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4bf0b-142">tooconfigure e prova AD Azure single sign-on con InsideView, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4bf0b-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4bf0b-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4bf0b-145">**[Creazione di un utente test InsideView](#creating-a-insideview-test-user)**  -toohave un equivalente di Britta Simon in InsideView che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4bf0b-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4bf0b-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4bf0b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bf0b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4bf0b-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione InsideView.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="4bf0b-150">**Azure AD tooconfigure single sign-on con InsideView, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4bf0b-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bf0b-151">Nel portale di Azure su hello hello **InsideView** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4bf0b-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="4bf0b-155">In hello **InsideView dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="4bf0b-157">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="4bf0b-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4bf0b-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="4bf0b-158">This value is not real.</span></span> <span data-ttu-id="4bf0b-159">Aggiornare questo valore con l'URL di risposta effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="4bf0b-160">Contatto [team di supporto InsideView ](mailto:support@insideview.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="4bf0b-161">In hello **certificato di firma SAML** fare clic su **certificato (Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="4bf0b-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4bf0b-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4bf0b-165">In hello **InsideView configurazione** fare clic su **configurare InsideView** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4bf0b-166">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4bf0b-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="4bf0b-168">In una finestra del web browser, accedere come amministratore nel sito della società InsideView di tooyour.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="4bf0b-169">Nella barra degli strumenti hello in primo piano hello, fare clic su **Admin**, **SingleSignOn Settings**, quindi fare clic su **Add SAML**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="4bf0b-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="4bf0b-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="4bf0b-171">In hello **aggiungere un nuovo SAML** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="4bf0b-172">![Aggiungi un nuovo SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Aggiungi un nuovo SAML")</span><span class="sxs-lookup"><span data-stu-id="4bf0b-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="4bf0b-173">a.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-173">a.</span></span> <span data-ttu-id="4bf0b-174">In hello **STS Name** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="4bf0b-175">b.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-175">b.</span></span> <span data-ttu-id="4bf0b-176">In **EndPoint indesiderati SamlP/WS-Fed** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4bf0b-177">c.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-177">c.</span></span> <span data-ttu-id="4bf0b-178">Aprire il certificato con codifica base 64, che è stato scaricato da Azure hello copia portale, del contenuto di esso negli Appunti, e quindi incollarlo toohello **STS Certificate** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="4bf0b-179">d.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-179">d.</span></span> <span data-ttu-id="4bf0b-180">In hello **Crm User Id Mapping** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="4bf0b-181">e.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-181">e.</span></span> <span data-ttu-id="4bf0b-182">In hello **Crm Email Mapping** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="4bf0b-183">f.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-183">f.</span></span> <span data-ttu-id="4bf0b-184">In hello **Crm First Name Mapping** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="4bf0b-185">g.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-185">g.</span></span> <span data-ttu-id="4bf0b-186">In hello **Crm lastName Mapping** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="4bf0b-187">h.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-187">h.</span></span> <span data-ttu-id="4bf0b-188">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4bf0b-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4bf0b-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4bf0b-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4bf0b-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4bf0b-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4bf0b-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bf0b-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="4bf0b-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4bf0b-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4bf0b-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bf0b-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4bf0b-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4bf0b-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4bf0b-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4bf0b-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4bf0b-204">a.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-204">a.</span></span> <span data-ttu-id="4bf0b-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4bf0b-206">b.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-206">b.</span></span> <span data-ttu-id="4bf0b-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4bf0b-208">c.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-208">c.</span></span> <span data-ttu-id="4bf0b-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4bf0b-210">d.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-210">d.</span></span> <span data-ttu-id="4bf0b-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="4bf0b-212">Creazione di un utente test di InsideView</span><span class="sxs-lookup"><span data-stu-id="4bf0b-212">Creating a InsideView test user</span></span>

<span data-ttu-id="4bf0b-213">toolog agli utenti di Azure AD tooenable in tooInsideView, è necessario eseguirne il provisioning in tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="4bf0b-214">Nel caso di hello di InsideView, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="4bf0b-215">creare utenti tooget o contatti in InsideView, contattare [team di supporto InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="4bf0b-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="4bf0b-216">È possibile usare qualsiasi altro InsideView utente account strumento di creazione o le API fornite da InsideView tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4bf0b-217">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bf0b-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4bf0b-218">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4bf0b-220">**tooassign Britta Simon tooInsideView, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4bf0b-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bf0b-221">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4bf0b-223">Nell'elenco di applicazioni hello, selezionare **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-223">In hello applications list, select **InsideView**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="4bf0b-225">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4bf0b-227">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-227">Click **Add** button.</span></span> <span data-ttu-id="4bf0b-228">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4bf0b-230">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4bf0b-231">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4bf0b-232">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4bf0b-233">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4bf0b-233">Testing single sign-on</span></span>

<span data-ttu-id="4bf0b-234">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4bf0b-235">Quando si fa clic su riquadro InsideView hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in InsideView applicazione.</span><span class="sxs-lookup"><span data-stu-id="4bf0b-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4bf0b-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4bf0b-236">Additional resources</span></span>

* [<span data-ttu-id="4bf0b-237">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bf0b-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4bf0b-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bf0b-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con AppDynamics | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e AppDynamics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="f8abc-103">Esercitazione: Integrazione di Azure Active Directory con AppDynamics</span><span class="sxs-lookup"><span data-stu-id="f8abc-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="f8abc-104">In questa esercitazione, è illustrato come toointegrate AppDynamics con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8abc-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8abc-105">Integrazione di AppDynamics con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f8abc-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8abc-106">È possibile controllare in Azure AD che ha accesso tooAppDynamics</span><span class="sxs-lookup"><span data-stu-id="f8abc-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="f8abc-107">È possibile abilitare l'utenti tooautomatically get connesso tooAppDynamics (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8abc-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8abc-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f8abc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8abc-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8abc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8abc-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f8abc-110">Prerequisites</span></span>

<span data-ttu-id="f8abc-111">integrazione di Azure AD con AppDynamics tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f8abc-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="f8abc-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8abc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8abc-113">Sottoscrizione AppDynamics abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f8abc-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8abc-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f8abc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8abc-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f8abc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8abc-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f8abc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8abc-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8abc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8abc-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f8abc-118">Scenario description</span></span>
<span data-ttu-id="f8abc-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f8abc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8abc-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f8abc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8abc-121">Aggiunta di AppDynamics dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f8abc-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="f8abc-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8abc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="f8abc-123">Aggiunta di AppDynamics dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f8abc-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="f8abc-124">integrazione hello tooconfigure di AppDynamics in Azure AD, è necessario tooadd AppDynamics dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f8abc-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8abc-125">**tooadd AppDynamics dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8abc-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8abc-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f8abc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f8abc-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8abc-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f8abc-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f8abc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f8abc-133">Nella casella di ricerca hello, digitare **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-133">In hello search box, type **AppDynamics**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="f8abc-135">Nel riquadro dei risultati hello, selezionare **AppDynamics**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8abc-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8abc-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8abc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8abc-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con AppDynamics usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f8abc-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f8abc-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in AppDynamics è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8abc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="f8abc-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in AppDynamics deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f8abc-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="f8abc-141">In AppDynamics, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="f8abc-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f8abc-142">tooconfigure e prova AD Azure single sign-on con AppDynamics, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f8abc-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8abc-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f8abc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8abc-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8abc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8abc-145">**[Creazione di un utente test AppDynamics](#creating-an-appdynamics-test-user)**  -toohave un equivalente di Britta Simon in AppDynamics che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f8abc-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8abc-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8abc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8abc-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f8abc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8abc-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8abc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8abc-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f8abc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="f8abc-150">**Azure AD tooconfigure single sign-on con AppDynamics, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8abc-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8abc-151">Nel portale di Azure su hello hello **AppDynamics** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f8abc-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8abc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="f8abc-155">In hello **AppDynamics dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8abc-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="f8abc-157">a.</span><span class="sxs-lookup"><span data-stu-id="f8abc-157">a.</span></span> <span data-ttu-id="f8abc-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="f8abc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="f8abc-159">b.</span><span class="sxs-lookup"><span data-stu-id="f8abc-159">b.</span></span> <span data-ttu-id="f8abc-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="f8abc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f8abc-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f8abc-161">These values are not real.</span></span> <span data-ttu-id="f8abc-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="f8abc-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f8abc-163">Contatto [team di supporto Client di AppDynamics](https://www.appdynamics.com/support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="f8abc-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="f8abc-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f8abc-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="f8abc-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f8abc-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8abc-168">In hello **AppDynamics configurazione** fare clic su **configurare AppDynamics** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f8abc-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f8abc-169">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f8abc-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="f8abc-171">In una finestra del web browser, accedere come amministratore nel sito della società AppDynamics di tooyour.</span><span class="sxs-lookup"><span data-stu-id="f8abc-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="f8abc-172">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**, quindi fare clic su **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="f8abc-173">![Amministrazione](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="f8abc-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="f8abc-174">Fare clic su hello **Provider di autenticazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="f8abc-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="f8abc-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span><span class="sxs-lookup"><span data-stu-id="f8abc-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="f8abc-176">In hello **Provider di autenticazione** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8abc-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f8abc-177">![Configurazione SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="f8abc-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="f8abc-178">a.</span><span class="sxs-lookup"><span data-stu-id="f8abc-178">a.</span></span> <span data-ttu-id="f8abc-179">Per **Authentication Provider** selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="f8abc-180">b.</span><span class="sxs-lookup"><span data-stu-id="f8abc-180">b.</span></span> <span data-ttu-id="f8abc-181">In hello **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f8abc-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f8abc-182">c.</span><span class="sxs-lookup"><span data-stu-id="f8abc-182">c.</span></span> <span data-ttu-id="f8abc-183">In hello **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f8abc-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="f8abc-184">d.</span><span class="sxs-lookup"><span data-stu-id="f8abc-184">d.</span></span> <span data-ttu-id="f8abc-185">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato** casella di testo</span><span class="sxs-lookup"><span data-stu-id="f8abc-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="f8abc-186">e.</span><span class="sxs-lookup"><span data-stu-id="f8abc-186">e.</span></span> <span data-ttu-id="f8abc-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-187">Click **Save**.</span></span>

     <span data-ttu-id="f8abc-188">![Salvare](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Salvare")</span><span class="sxs-lookup"><span data-stu-id="f8abc-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="f8abc-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f8abc-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8abc-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f8abc-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8abc-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8abc-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8abc-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8abc-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8abc-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f8abc-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f8abc-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8abc-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8abc-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f8abc-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8abc-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8abc-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f8abc-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8abc-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8abc-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8abc-204">a.</span><span class="sxs-lookup"><span data-stu-id="f8abc-204">a.</span></span> <span data-ttu-id="f8abc-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8abc-206">b.</span><span class="sxs-lookup"><span data-stu-id="f8abc-206">b.</span></span> <span data-ttu-id="f8abc-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8abc-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8abc-208">c.</span><span class="sxs-lookup"><span data-stu-id="f8abc-208">c.</span></span> <span data-ttu-id="f8abc-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8abc-210">d.</span><span class="sxs-lookup"><span data-stu-id="f8abc-210">d.</span></span> <span data-ttu-id="f8abc-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="f8abc-212">Creazione di un utente di test di AppDynamics</span><span class="sxs-lookup"><span data-stu-id="f8abc-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="f8abc-213">toolog agli utenti di Azure AD tooenable in tooAppDynamics, è necessario eseguirne il provisioning in AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f8abc-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="f8abc-214">Nel caso di hello di AppDynamics, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f8abc-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="f8abc-215">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8abc-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8abc-216">Accedi tooyour sito della società AppDynamics come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f8abc-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="f8abc-217">Andare troppo**utenti**, quindi fare clic su  **+**  tooopen hello **Create User** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f8abc-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="f8abc-218">![Utenti](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="f8abc-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="f8abc-219">In hello **Create User** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8abc-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f8abc-220">![Crea utente](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="f8abc-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="f8abc-221">a.</span><span class="sxs-lookup"><span data-stu-id="f8abc-221">a.</span></span> <span data-ttu-id="f8abc-222">Hello tipo **Username**, **nome**, **posta elettronica**, **nuova Password**, **conferma della nuova Password** di valido di Azure ad account si vuole tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="f8abc-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="f8abc-223">b.</span><span class="sxs-lookup"><span data-stu-id="f8abc-223">b.</span></span> <span data-ttu-id="f8abc-224">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f8abc-225">È possibile usare qualsiasi altro AppDynamics utente account strumento di creazione o le API fornite da AppDynamics tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8abc-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f8abc-226">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8abc-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f8abc-227">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f8abc-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f8abc-229">**tooassign Britta Simon tooAppDynamics, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8abc-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8abc-230">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f8abc-232">Nell'elenco di applicazioni hello, selezionare **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-232">In hello applications list, select **AppDynamics**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="f8abc-234">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f8abc-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-236">Click **Add** button.</span></span> <span data-ttu-id="f8abc-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f8abc-239">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f8abc-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8abc-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8abc-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f8abc-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8abc-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f8abc-242">Testing single sign-on</span></span>

<span data-ttu-id="f8abc-243">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f8abc-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f8abc-244">Quando si fa clic hello AppDynamics riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f8abc-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8abc-245">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f8abc-245">Additional resources</span></span>

* [<span data-ttu-id="f8abc-246">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8abc-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8abc-247">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8abc-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png


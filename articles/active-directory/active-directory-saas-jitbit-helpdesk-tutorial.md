---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jitbit Helpdesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="a5535-103">Esercitazione: Integrazione di Azure Active Directory con Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="a5535-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="a5535-104">In questa esercitazione, è illustrato come toointegrate Jitbit Helpdesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5535-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5535-105">Integrazione di Jitbit Helpdesk con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a5535-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a5535-106">È possibile controllare in Azure AD che ha accesso tooJitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="a5535-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="a5535-107">È possibile abilitare l'utenti tooautomatically get connesso tooJitbit Helpdesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5535-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5535-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a5535-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a5535-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5535-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5535-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5535-110">Prerequisites</span></span>

<span data-ttu-id="a5535-111">tooconfigure integrazione di Azure AD con Jitbit Helpdesk, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a5535-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="a5535-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5535-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5535-113">Sottoscrizione di Jitbit Helpdesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a5535-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5535-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a5535-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5535-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="a5535-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5535-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a5535-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5535-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5535-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5535-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a5535-118">Scenario description</span></span>
<span data-ttu-id="a5535-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a5535-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5535-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="a5535-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5535-121">Aggiunta di Jitbit Helpdesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a5535-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="a5535-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5535-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="a5535-123">Aggiunta di Jitbit Helpdesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a5535-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="a5535-124">integrazione hello tooconfigure di Jitbit Helpdesk in Azure AD, è necessario tooadd Jitbit Helpdesk dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a5535-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a5535-125">**tooadd Jitbit Helpdesk dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a5535-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5535-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a5535-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5535-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a5535-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a5535-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a5535-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a5535-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a5535-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a5535-133">Nella casella di ricerca hello, digitare **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="a5535-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="a5535-135">Nel riquadro dei risultati hello, selezionare **Jitbit Helpdesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a5535-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5535-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5535-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5535-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jitbit Helpdesk in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a5535-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a5535-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Jitbit Helpdesk è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5535-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="a5535-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Jitbit Helpdesk deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="a5535-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="a5535-141">In Jitbit Helpdesk, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="a5535-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a5535-142">tooconfigure e test Azure single sign-on AD con Jitbit Helpdesk, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="a5535-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a5535-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a5535-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a5535-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5535-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5535-145">**[Creazione di un utente test Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave un equivalente di Britta Simon in Jitbit Helpdesk che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a5535-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5535-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5535-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5535-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a5535-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5535-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5535-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5535-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="a5535-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="a5535-150">**Azure AD tooconfigure single sign-on con Jitbit Helpdesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a5535-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5535-151">Nel portale di Azure su hello hello **Jitbit Helpdesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a5535-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a5535-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5535-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="a5535-155">In hello **Jitbit Helpdesk dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a5535-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="a5535-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5535-157">a.</span></span> <span data-ttu-id="a5535-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="a5535-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="a5535-159">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="a5535-159">This value is not real.</span></span> <span data-ttu-id="a5535-160">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a5535-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a5535-161">Contatto [team di supporto Client di Jitbit Helpdesk](https://www.jitbit.com/support/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="a5535-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="a5535-162">b.</span><span class="sxs-lookup"><span data-stu-id="a5535-162">b.</span></span>  <span data-ttu-id="a5535-163">In hello **identificatore** casella di testo, digitare un URL come riportato di seguito:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="a5535-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="a5535-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="a5535-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="a5535-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a5535-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5535-168">In hello **Jitbit Helpdesk configurazione** fare clic su **configurare Jitbit Helpdesk** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="a5535-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a5535-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a5535-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="a5535-171">In un'altra finestra del Web browser accedere al sito aziendale di Jitbit Helpdesk come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a5535-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="a5535-172">Nella barra degli strumenti hello in primo piano hello, fare clic su **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="a5535-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="a5535-173">![Amministrazione](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="a5535-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="a5535-174">Fare clic su **General settings**.</span><span class="sxs-lookup"><span data-stu-id="a5535-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="a5535-175">![Users, companies and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies and permissions")</span><span class="sxs-lookup"><span data-stu-id="a5535-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="a5535-176">In hello **le impostazioni di autenticazione** configurazione seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a5535-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a5535-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span><span class="sxs-lookup"><span data-stu-id="a5535-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="a5535-178">a.</span><span class="sxs-lookup"><span data-stu-id="a5535-178">a.</span></span> <span data-ttu-id="a5535-179">Selezionare **accesso Enable SAML 2.0 single**, toosign utilizzando Single Sign-On (SSO), con **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="a5535-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="a5535-180">b.</span><span class="sxs-lookup"><span data-stu-id="a5535-180">b.</span></span> <span data-ttu-id="a5535-181">In hello **URL dell'EndPoint** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5535-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5535-182">c.</span><span class="sxs-lookup"><span data-stu-id="a5535-182">c.</span></span> <span data-ttu-id="a5535-183">Aprire il **base 64** codificato nel blocco note, hello copia del contenuto di esso negli Appunti, certificato e quindi incollarlo toohello **certificato x. 509** casella di testo</span><span class="sxs-lookup"><span data-stu-id="a5535-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="a5535-184">d.</span><span class="sxs-lookup"><span data-stu-id="a5535-184">d.</span></span> <span data-ttu-id="a5535-185">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="a5535-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a5535-186">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="a5535-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a5535-187">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="a5535-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a5535-188">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5535-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5535-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5535-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5535-190">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a5535-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a5535-192">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a5535-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5535-193">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a5535-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5535-195">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a5535-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5535-197">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="a5535-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5535-199">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a5535-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5535-201">a.</span><span class="sxs-lookup"><span data-stu-id="a5535-201">a.</span></span> <span data-ttu-id="a5535-202">In hello **nome** casella di testo, il nome di tipo come **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5535-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="a5535-203">b.</span><span class="sxs-lookup"><span data-stu-id="a5535-203">b.</span></span> <span data-ttu-id="a5535-204">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a5535-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5535-205">c.</span><span class="sxs-lookup"><span data-stu-id="a5535-205">c.</span></span> <span data-ttu-id="a5535-206">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="a5535-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a5535-207">d.</span><span class="sxs-lookup"><span data-stu-id="a5535-207">d.</span></span> <span data-ttu-id="a5535-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a5535-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="a5535-209">Creazione di un utente test di Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="a5535-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="a5535-210">In ordine tooenable Azure AD utenti toolog in Jitbit Helpdesk, è necessario eseguirne il provisioning in Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="a5535-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="a5535-211">Nel caso di hello di Jitbit Helpdesk, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="a5535-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="a5535-212">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a5535-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5535-213">Accedi tooyour **Jitbit Helpdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="a5535-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="a5535-214">Scegliere dal menu hello in primo piano hello **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="a5535-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="a5535-215">![Amministrazione](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="a5535-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="a5535-216">Fare clic su **Users, companies and permissions**.</span><span class="sxs-lookup"><span data-stu-id="a5535-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="a5535-217">![Users, companies and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies and permissions")</span><span class="sxs-lookup"><span data-stu-id="a5535-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="a5535-218">Fare clic su **Add User**.</span><span class="sxs-lookup"><span data-stu-id="a5535-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="a5535-219">![Aggiungere un utente](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="a5535-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="a5535-220">Nella sezione creare hello, digitare dati hello dell'account di Azure AD hello desiderato tooprovision come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a5535-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="a5535-221">![Creare](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="a5535-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="a5535-222">a.</span><span class="sxs-lookup"><span data-stu-id="a5535-222">a.</span></span> <span data-ttu-id="a5535-223">In hello **Username** casella tipo **BrittaSimon**, nome utente hello come hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5535-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="a5535-224">b.</span><span class="sxs-lookup"><span data-stu-id="a5535-224">b.</span></span> <span data-ttu-id="a5535-225">In hello **posta elettronica** casella di testo, come di tipo messaggio di posta elettronica dell'utente hello  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a5535-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="a5535-226">c.</span><span class="sxs-lookup"><span data-stu-id="a5535-226">c.</span></span> <span data-ttu-id="a5535-227">In hello **nome** casella di testo Nome tipo di utente hello come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="a5535-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="a5535-228">d.</span><span class="sxs-lookup"><span data-stu-id="a5535-228">d.</span></span> <span data-ttu-id="a5535-229">In hello **cognome** casella di testo, digitare cognome dell'utente hello come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a5535-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="a5535-230">e.</span><span class="sxs-lookup"><span data-stu-id="a5535-230">e.</span></span> <span data-ttu-id="a5535-231">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a5535-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="a5535-232">È possibile usare qualsiasi altro Jitbit Helpdesk utente account strumento di creazione o qualsiasi API fornita da Jitbit Helpdesk tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5535-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a5535-233">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5535-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a5535-234">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooJitbit supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="a5535-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a5535-236">**tooassign Britta Simon tooJitbit Helpdesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a5535-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="a5535-237">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a5535-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a5535-239">Nell'elenco di applicazioni hello, selezionare **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="a5535-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="a5535-241">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a5535-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a5535-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a5535-243">Click **Add** button.</span></span> <span data-ttu-id="a5535-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a5535-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a5535-246">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a5535-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a5535-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a5535-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5535-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a5535-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5535-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a5535-249">Testing single sign-on</span></span>

<span data-ttu-id="a5535-250">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a5535-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a5535-251">Quando si fa clic hello Jitbit Helpdesk riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione di Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="a5535-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="a5535-252">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5535-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5535-253">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a5535-253">Additional resources</span></span>

* [<span data-ttu-id="a5535-254">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5535-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5535-255">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5535-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png


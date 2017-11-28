---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kudos | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kudos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="c3556-103">Esercitazione: integrazione di Azure Active Directory con Kudos</span><span class="sxs-lookup"><span data-stu-id="c3556-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="c3556-104">In questa esercitazione, è illustrato come toointegrate Kudos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3556-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3556-105">Integrazione di Kudos con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c3556-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c3556-106">È possibile controllare in Azure AD che ha accesso tooKudos</span><span class="sxs-lookup"><span data-stu-id="c3556-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="c3556-107">È possibile abilitare l'utenti tooautomatically get connesso tooKudos (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3556-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3556-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c3556-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c3556-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3556-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3556-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c3556-110">Prerequisites</span></span>

<span data-ttu-id="c3556-111">integrazione di Azure AD con Kudos tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c3556-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="c3556-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3556-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3556-113">Sottoscrizione di Kudos abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3556-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3556-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c3556-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3556-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="c3556-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3556-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c3556-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3556-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3556-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3556-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c3556-118">Scenario description</span></span>
<span data-ttu-id="c3556-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c3556-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3556-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c3556-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3556-121">Aggiunta di Kudos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c3556-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="c3556-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3556-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="c3556-123">Aggiunta di Kudos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c3556-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="c3556-124">integrazione hello tooconfigure di Kudos in Azure AD, è necessario tooadd Kudos dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c3556-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c3556-125">**tooadd Kudos dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3556-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3556-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c3556-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3556-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c3556-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c3556-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3556-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c3556-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c3556-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c3556-133">Nella casella di ricerca hello, digitare **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="c3556-133">In hello search box, type **Kudos**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="c3556-135">Nel riquadro dei risultati hello, selezionare **Kudos**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c3556-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3556-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3556-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3556-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kudos usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3556-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3556-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kudos è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3556-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="c3556-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Kudos deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="c3556-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="c3556-141">In Kudos, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="c3556-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c3556-142">tooconfigure e prova AD Azure single sign-on con Kudos, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="c3556-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c3556-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c3556-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c3556-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3556-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3556-145">**[Creazione di un utente test Kudos](#creating-a-kudos-test-user)**  -toohave un equivalente di Britta Simon in Kudos che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c3556-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3556-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3556-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3556-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="c3556-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3556-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3556-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3556-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Kudos.</span><span class="sxs-lookup"><span data-stu-id="c3556-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="c3556-150">**Azure AD tooconfigure single sign-on con Kudos, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3556-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3556-151">Nel portale di Azure su hello hello **Kudos** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c3556-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c3556-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3556-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="c3556-155">In hello **Kudos dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c3556-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="c3556-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="c3556-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="c3556-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="c3556-158">This value is not real.</span></span> <span data-ttu-id="c3556-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c3556-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c3556-160">Contatto [team di supporto Client di Kudos](http://success.kudosnow.com/home) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="c3556-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="c3556-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c3556-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="c3556-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c3556-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3556-165">In hello **Kudos configurazione** fare clic su **configurare Kudos** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="c3556-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c3556-166">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c3556-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="c3556-168">In un'altra finestra del Web browser accedere al sito aziendale di Kudos come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c3556-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="c3556-169">Scegliere dal menu hello in primo piano hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3556-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="c3556-170">![Impostazioni](./media/active-directory-saas-kudos-tutorial/ic787806.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="c3556-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="c3556-171">Fare clic su **Integrations (Integrazioni) \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="c3556-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="c3556-172">In hello **SSO** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c3556-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c3556-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="c3556-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="c3556-174">a.</span><span class="sxs-lookup"><span data-stu-id="c3556-174">a.</span></span> <span data-ttu-id="c3556-175">In **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3556-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c3556-176">b.</span><span class="sxs-lookup"><span data-stu-id="c3556-176">b.</span></span> <span data-ttu-id="c3556-177">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo</span><span class="sxs-lookup"><span data-stu-id="c3556-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="c3556-178">c.</span><span class="sxs-lookup"><span data-stu-id="c3556-178">c.</span></span> <span data-ttu-id="c3556-179">In **Logout tooURL**, incollare il valore di hello di **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3556-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c3556-180">d.</span><span class="sxs-lookup"><span data-stu-id="c3556-180">d.</span></span> <span data-ttu-id="c3556-181">In hello **Your Kudos URL** casella di testo, digitare il nome della società.</span><span class="sxs-lookup"><span data-stu-id="c3556-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="c3556-182">e.</span><span class="sxs-lookup"><span data-stu-id="c3556-182">e.</span></span> <span data-ttu-id="c3556-183">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c3556-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c3556-184">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="c3556-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c3556-185">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c3556-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c3556-186">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3556-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3556-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3556-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3556-188">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c3556-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c3556-190">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3556-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3556-191">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c3556-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3556-193">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c3556-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3556-195">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c3556-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3556-197">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c3556-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3556-199">a.</span><span class="sxs-lookup"><span data-stu-id="c3556-199">a.</span></span> <span data-ttu-id="c3556-200">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3556-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3556-201">b.</span><span class="sxs-lookup"><span data-stu-id="c3556-201">b.</span></span> <span data-ttu-id="c3556-202">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c3556-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3556-203">c.</span><span class="sxs-lookup"><span data-stu-id="c3556-203">c.</span></span> <span data-ttu-id="c3556-204">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="c3556-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c3556-205">d.</span><span class="sxs-lookup"><span data-stu-id="c3556-205">d.</span></span> <span data-ttu-id="c3556-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c3556-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="c3556-207">Creazione di un utente test di Kudos</span><span class="sxs-lookup"><span data-stu-id="c3556-207">Creating a Kudos test user</span></span>

<span data-ttu-id="c3556-208">In ordine tooenable Azure AD utenti toolog a Kudos, è necessario eseguirne il provisioning in Kudos.</span><span class="sxs-lookup"><span data-stu-id="c3556-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="c3556-209">Nel caso di hello di Kudos, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="c3556-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="c3556-210">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3556-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3556-211">Accedi tooyour **Kudos** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c3556-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="c3556-212">Scegliere dal menu hello in primo piano hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3556-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="c3556-213">![Impostazioni](./media/active-directory-saas-kudos-tutorial/ic787806.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="c3556-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="c3556-214">Fare clic su **User Admin**.</span><span class="sxs-lookup"><span data-stu-id="c3556-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="c3556-215">Fare clic su hello **utenti** scheda e quindi fare clic su **aggiungere un utente**.</span><span class="sxs-lookup"><span data-stu-id="c3556-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="c3556-216">![Amministratore utenti](./media/active-directory-saas-kudos-tutorial/ic787809.png "Amministratore utenti")</span><span class="sxs-lookup"><span data-stu-id="c3556-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="c3556-217">In hello **aggiungere un utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c3556-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c3556-218">![Aggiungere un utente](./media/active-directory-saas-kudos-tutorial/ic787810.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="c3556-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="c3556-219">a.</span><span class="sxs-lookup"><span data-stu-id="c3556-219">a.</span></span> <span data-ttu-id="c3556-220">Hello tipo **nome**, **cognome**, **posta elettronica** e altri dettagli di un account di Azure Active Directory valido, si vuole tooprovision in hello correlati nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="c3556-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="c3556-221">b.</span><span class="sxs-lookup"><span data-stu-id="c3556-221">b.</span></span> <span data-ttu-id="c3556-222">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="c3556-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="c3556-223">È possibile usare qualsiasi altro Kudos utente account strumento di creazione o le API fornite da Kudos tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="c3556-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c3556-224">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3556-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c3556-225">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKudos.</span><span class="sxs-lookup"><span data-stu-id="c3556-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c3556-227">**tooassign Britta Simon tooKudos, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3556-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3556-228">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3556-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c3556-230">Nell'elenco di applicazioni hello, selezionare **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="c3556-230">In hello applications list, select **Kudos**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="c3556-232">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c3556-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c3556-234">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c3556-234">Click **Add** button.</span></span> <span data-ttu-id="c3556-235">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3556-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c3556-237">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c3556-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c3556-238">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c3556-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3556-239">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3556-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3556-240">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3556-240">Testing single sign-on</span></span>

<span data-ttu-id="c3556-241">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c3556-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c3556-242">Quando si fa clic su riquadro Kudos hello in hello Pannello di accesso, è necessario ottenere applicazione Kudos tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="c3556-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="c3556-243">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3556-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3556-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c3556-244">Additional resources</span></span>

* [<span data-ttu-id="c3556-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3556-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3556-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3556-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png


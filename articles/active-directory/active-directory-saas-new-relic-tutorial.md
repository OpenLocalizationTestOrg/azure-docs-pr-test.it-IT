---
title: 'Esercitazione: Integrazione di Azure Active Directory con New Relic | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e New Relic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="5e7d2-103">Esercitazione: Integrazione di Azure Active Directory con New Relic</span><span class="sxs-lookup"><span data-stu-id="5e7d2-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="5e7d2-104">In questa esercitazione, è illustrato come toointegrate New Relic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e7d2-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e7d2-105">Integrazione di New Relic con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5e7d2-106">È possibile controllare in Azure AD che ha accesso tooNew Relic</span><span class="sxs-lookup"><span data-stu-id="5e7d2-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="5e7d2-107">È possibile abilitare l'utenti tooautomatically get connesso tooNew Relic (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e7d2-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e7d2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5e7d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5e7d2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e7d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e7d2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5e7d2-110">Prerequisites</span></span>

<span data-ttu-id="5e7d2-111">integrazione di Azure AD con New Relic tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="5e7d2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e7d2-113">Sottoscrizione di New Relic abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5e7d2-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e7d2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e7d2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e7d2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e7d2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e7d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e7d2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5e7d2-118">Scenario description</span></span>
<span data-ttu-id="5e7d2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e7d2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e7d2-121">Aggiunta di New Relic nella raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5e7d2-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="5e7d2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e7d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="5e7d2-123">Aggiunta di New Relic nella raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5e7d2-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="5e7d2-124">integrazione hello tooconfigure di New Relic in Azure AD, è necessario tooadd New Relic dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5e7d2-125">**tooadd New Relic nella raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5e7d2-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e7d2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5e7d2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5e7d2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5e7d2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5e7d2-133">Nella casella di ricerca hello, digitare **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-133">In hello search box, type **New Relic**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="5e7d2-135">Nel riquadro dei risultati hello, selezionare **New Relic**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5e7d2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e7d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5e7d2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con New Relic usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5e7d2-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5e7d2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in New Relic è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="5e7d2-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in New Relic deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="5e7d2-141">In New Relic, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5e7d2-142">tooconfigure e prova AD Azure single sign-on con New Relic, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5e7d2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5e7d2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e7d2-145">**[Creazione di un utente test New Relic](#creating-a-new-relic-test-user)**  -toohave un equivalente di Britta Simon in New Relic che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e7d2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e7d2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5e7d2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e7d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5e7d2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione New Relic.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="5e7d2-150">**Azure AD tooconfigure single sign-on con New Relic, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5e7d2-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e7d2-151">Nel portale di Azure su hello hello **New Relic** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5e7d2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="5e7d2-155">In hello **nuovo dominio Relic e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="5e7d2-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="5e7d2-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5e7d2-158">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-158">hello value is not real.</span></span> <span data-ttu-id="5e7d2-159">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5e7d2-160">Contatto [team di supporto di nuovi Client Relic](https://support.newrelic.com/) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="5e7d2-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="5e7d2-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5e7d2-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e7d2-165">In hello **nuova configurazione Relic** fare clic su **configurare New Relic** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5e7d2-166">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5e7d2-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="5e7d2-168">In una finestra del web browser, accedere tooyour **New Relic** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="5e7d2-169">Scegliere dal menu hello in primo piano hello **impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="5e7d2-170">![Impostazioni account](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="5e7d2-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="5e7d2-171">Fare clic su hello **sicurezza e autenticazione** scheda e quindi fare clic su hello **Single sign-on** scheda.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="5e7d2-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="5e7d2-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="5e7d2-173">Nella pagina della finestra di hello SAML eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5e7d2-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="5e7d2-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="5e7d2-175">a.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-175">a.</span></span> <span data-ttu-id="5e7d2-176">Fare clic su **Scegli File** tooupload il certificato di Azure Active Directory scaricato.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="5e7d2-177">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-177">b.</span></span> <span data-ttu-id="5e7d2-178">In hello **URL di accesso remoto** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="5e7d2-179">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-179">c.</span></span> <span data-ttu-id="5e7d2-180">In hello **Logout landing URL** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="5e7d2-181">d.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-181">d.</span></span> <span data-ttu-id="5e7d2-182">Fare clic su **Save my changes**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5e7d2-183">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5e7d2-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5e7d2-184">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5e7d2-185">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5e7d2-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5e7d2-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e7d2-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="5e7d2-187">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5e7d2-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5e7d2-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e7d2-190">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e7d2-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e7d2-194">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e7d2-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e7d2-198">a.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-198">a.</span></span> <span data-ttu-id="5e7d2-199">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e7d2-200">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-200">b.</span></span> <span data-ttu-id="5e7d2-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5e7d2-202">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-202">c.</span></span> <span data-ttu-id="5e7d2-203">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5e7d2-204">d.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-204">d.</span></span> <span data-ttu-id="5e7d2-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="5e7d2-206">Creazione di un utente di test di New Relic</span><span class="sxs-lookup"><span data-stu-id="5e7d2-206">Creating a New Relic test user</span></span>

<span data-ttu-id="5e7d2-207">In ordine tooenable Azure Active Directory gli utenti toolog in tooNew Relic, è necessario eseguirne il provisioning in New Relic.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="5e7d2-208">Nel caso di hello di New Relic, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="5e7d2-209">**tooprovision un tooNew di account utente Relic, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5e7d2-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e7d2-210">Accedi tooyour **New Relic** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="5e7d2-211">Scegliere dal menu hello in primo piano hello **impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="5e7d2-212">![Impostazioni account](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="5e7d2-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="5e7d2-213">In hello **Account** riquadro hello lato sinistra, fare clic su **riepilogo**, quindi fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="5e7d2-214">![Impostazioni account](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="5e7d2-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="5e7d2-215">In hello **utenti attivi** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5e7d2-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5e7d2-216">![Utenti attivi](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Utenti attivi")</span><span class="sxs-lookup"><span data-stu-id="5e7d2-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="5e7d2-217">a.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-217">a.</span></span> <span data-ttu-id="5e7d2-218">In hello **posta elettronica** casella di testo, hello tipo indirizzo di posta elettronica di un utente di Azure Active Directory valido, si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="5e7d2-219">b.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-219">b.</span></span> <span data-ttu-id="5e7d2-220">Come **Role** (Ruolo) selezionare **User** (Utente).</span><span class="sxs-lookup"><span data-stu-id="5e7d2-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="5e7d2-221">c.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-221">c.</span></span> <span data-ttu-id="5e7d2-222">Fare clic su **Add this user**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="5e7d2-223">È possibile usare qualsiasi altro New Relic utente account strumento di creazione o le API fornite da New Relic tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5e7d2-224">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e7d2-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5e7d2-225">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNew Relic.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5e7d2-227">**tooassign tooNew Britta Simon Relic, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5e7d2-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e7d2-228">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5e7d2-230">Nell'elenco di applicazioni hello, selezionare **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-230">In hello applications list, select **New Relic**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="5e7d2-232">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5e7d2-234">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-234">Click **Add** button.</span></span> <span data-ttu-id="5e7d2-235">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5e7d2-237">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5e7d2-238">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e7d2-239">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5e7d2-240">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5e7d2-240">Testing single sign-on</span></span>

<span data-ttu-id="5e7d2-241">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5e7d2-242">Quando si fa clic su riquadro New Relic hello in hello Pannello di accesso, è necessario ottenere l'applicazione New Relic tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="5e7d2-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e7d2-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5e7d2-243">Additional resources</span></span>

* [<span data-ttu-id="5e7d2-244">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e7d2-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e7d2-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e7d2-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png


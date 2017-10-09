---
title: 'Esercitazione: Integrazione di Azure Active Directory con UserEcho | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e UserEcho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="5ca10-103">Esercitazione: Integrazione di Azure Active Directory con UserEcho</span><span class="sxs-lookup"><span data-stu-id="5ca10-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="5ca10-104">In questa esercitazione, è illustrato come toointegrate UserEcho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ca10-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ca10-105">Integrazione UserEcho con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5ca10-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ca10-106">È possibile controllare in Azure AD che ha accesso tooUserEcho</span><span class="sxs-lookup"><span data-stu-id="5ca10-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="5ca10-107">È possibile abilitare l'utenti tooautomatically get connesso tooUserEcho (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ca10-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ca10-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5ca10-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5ca10-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ca10-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ca10-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ca10-110">Prerequisites</span></span>

<span data-ttu-id="5ca10-111">integrazione di Azure AD con UserEcho tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5ca10-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="5ca10-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ca10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ca10-113">Sottoscrizione di UserEcho abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5ca10-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ca10-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5ca10-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ca10-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5ca10-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ca10-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5ca10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ca10-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ca10-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ca10-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5ca10-118">Scenario description</span></span>
<span data-ttu-id="5ca10-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5ca10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ca10-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5ca10-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ca10-121">Aggiunta di UserEcho dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5ca10-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="5ca10-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ca10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="5ca10-123">Aggiunta di UserEcho dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5ca10-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="5ca10-124">integrazione hello tooconfigure di UserEcho in Azure AD, è necessario tooadd UserEcho dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5ca10-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ca10-125">**tooadd UserEcho dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ca10-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ca10-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5ca10-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ca10-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ca10-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5ca10-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5ca10-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5ca10-133">Nella casella di ricerca hello, digitare **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-133">In hello search box, type **UserEcho**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="5ca10-135">Nel riquadro dei risultati hello, selezionare **UserEcho**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5ca10-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ca10-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ca10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ca10-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UserEcho con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5ca10-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ca10-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in UserEcho è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ca10-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="5ca10-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in UserEcho deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5ca10-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="5ca10-141">In UserEcho, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5ca10-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5ca10-142">tooconfigure e prova AD Azure single sign-on con UserEcho, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5ca10-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ca10-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5ca10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ca10-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ca10-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ca10-145">**[Creazione di un utente test UserEcho](#creating-a-userecho-test-user)**  -toohave un equivalente di Britta Simon in UserEcho che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5ca10-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ca10-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5ca10-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ca10-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5ca10-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ca10-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ca10-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ca10-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione UserEcho.</span><span class="sxs-lookup"><span data-stu-id="5ca10-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="5ca10-150">**Azure AD tooconfigure single sign-on con UserEcho, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ca10-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ca10-151">Nel portale di Azure su hello hello **UserEcho** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5ca10-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5ca10-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="5ca10-155">In hello **UserEcho dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ca10-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="5ca10-157">a.</span><span class="sxs-lookup"><span data-stu-id="5ca10-157">a.</span></span> <span data-ttu-id="5ca10-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="5ca10-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="5ca10-159">b.</span><span class="sxs-lookup"><span data-stu-id="5ca10-159">b.</span></span> <span data-ttu-id="5ca10-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="5ca10-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ca10-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="5ca10-161">These values are not real.</span></span> <span data-ttu-id="5ca10-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="5ca10-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5ca10-163">Contatto [team di supporto UserEcho Client](https://feedback.userecho.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="5ca10-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="5ca10-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5ca10-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="5ca10-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5ca10-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5ca10-168">In hello **UserEcho configurazione** fare clic su **configurare UserEcho** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5ca10-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5ca10-169">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5ca10-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="5ca10-171">In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour UserEcho.</span><span class="sxs-lookup"><span data-stu-id="5ca10-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="5ca10-172">Nella barra degli strumenti hello in primo piano hello, fare clic su nel menu di hello tooexpand nome utente e quindi fare clic su **installazione**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="5ca10-174">Fare clic su **Integrations**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-174">Click **Integrations**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="5ca10-176">Fare clic su **Sito web** e quindi su **Single sign-on (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="5ca10-178">In hello **Single sign-on (SAML)** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ca10-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="5ca10-180">a.</span><span class="sxs-lookup"><span data-stu-id="5ca10-180">a.</span></span> <span data-ttu-id="5ca10-181">Per **SAML-enabled** (Abilitato per SAML) selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="5ca10-182">b.</span><span class="sxs-lookup"><span data-stu-id="5ca10-182">b.</span></span> <span data-ttu-id="5ca10-183">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **URL SSO SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5ca10-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="5ca10-184">c.</span><span class="sxs-lookup"><span data-stu-id="5ca10-184">c.</span></span> <span data-ttu-id="5ca10-185">Incolla **Sign-Out URL**, che è stato copiato dal portale di Azure hello in hello **URL remoto logoout** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5ca10-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="5ca10-186">d.</span><span class="sxs-lookup"><span data-stu-id="5ca10-186">d.</span></span> <span data-ttu-id="5ca10-187">Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5ca10-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="5ca10-188">e.</span><span class="sxs-lookup"><span data-stu-id="5ca10-188">e.</span></span> <span data-ttu-id="5ca10-189">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5ca10-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5ca10-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5ca10-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5ca10-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5ca10-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ca10-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ca10-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ca10-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ca10-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5ca10-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5ca10-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ca10-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ca10-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5ca10-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ca10-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ca10-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5ca10-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ca10-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ca10-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ca10-205">a.</span><span class="sxs-lookup"><span data-stu-id="5ca10-205">a.</span></span> <span data-ttu-id="5ca10-206">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ca10-207">b.</span><span class="sxs-lookup"><span data-stu-id="5ca10-207">b.</span></span> <span data-ttu-id="5ca10-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ca10-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ca10-209">c.</span><span class="sxs-lookup"><span data-stu-id="5ca10-209">c.</span></span> <span data-ttu-id="5ca10-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ca10-211">d.</span><span class="sxs-lookup"><span data-stu-id="5ca10-211">d.</span></span> <span data-ttu-id="5ca10-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="5ca10-213">Creazione di un utente test per UserEcho</span><span class="sxs-lookup"><span data-stu-id="5ca10-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="5ca10-214">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in UserEcho toocreate.</span><span class="sxs-lookup"><span data-stu-id="5ca10-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="5ca10-215">**un utente denominato Britta Simon in UserEcho, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ca10-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ca10-216">Sito dell'azienda UserEcho tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5ca10-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="5ca10-217">Nella barra degli strumenti hello in primo piano hello, fare clic su nel menu di hello tooexpand nome utente e quindi fare clic su **installazione**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="5ca10-219">Fare clic su **utenti**, hello tooexpand **utenti** sezione.</span><span class="sxs-lookup"><span data-stu-id="5ca10-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="5ca10-221">Fare clic su **Users**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-221">Click **Users**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="5ca10-223">Fare clic su **Invite a new user**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-223">Click **Invite a new user**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="5ca10-225">In hello **invitare un nuovo utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ca10-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="5ca10-227">a.</span><span class="sxs-lookup"><span data-stu-id="5ca10-227">a.</span></span> <span data-ttu-id="5ca10-228">In hello **nome** casella di testo, nome del tipo di utente hello come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ca10-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="5ca10-229">b.</span><span class="sxs-lookup"><span data-stu-id="5ca10-229">b.</span></span>  <span data-ttu-id="5ca10-230">In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5ca10-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="5ca10-231">c.</span><span class="sxs-lookup"><span data-stu-id="5ca10-231">c.</span></span> <span data-ttu-id="5ca10-232">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-232">Click **Invite**.</span></span>

<span data-ttu-id="5ca10-233">TooBritta, consentendo la sua toostart utilizzando UserEcho viene inviato un invito.</span><span class="sxs-lookup"><span data-stu-id="5ca10-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5ca10-234">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ca10-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5ca10-235">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooUserEcho.</span><span class="sxs-lookup"><span data-stu-id="5ca10-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5ca10-237">**tooassign Britta Simon tooUserEcho, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ca10-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ca10-238">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5ca10-240">Nell'elenco di applicazioni hello, selezionare **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-240">In hello applications list, select **UserEcho**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="5ca10-242">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5ca10-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-244">Click **Add** button.</span></span> <span data-ttu-id="5ca10-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5ca10-247">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5ca10-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ca10-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ca10-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5ca10-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ca10-250">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5ca10-250">Testing single sign-on</span></span>

<span data-ttu-id="5ca10-251">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5ca10-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5ca10-252">Quando si fa clic su riquadro UserEcho hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour UserEcho applicazione.</span><span class="sxs-lookup"><span data-stu-id="5ca10-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ca10-253">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5ca10-253">Additional resources</span></span>

* [<span data-ttu-id="5ca10-254">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ca10-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ca10-255">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ca10-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png


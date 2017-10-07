---
title: 'Esercitazione: Integrazione di Azure Active Directory con HireVue |Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e HireVue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f890633ee4f13919c32a43d7b6cf30f2270ef6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="4cfd4-103">Esercitazione: Integrazione di Azure Active Directory con HireVue</span><span class="sxs-lookup"><span data-stu-id="4cfd4-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="4cfd4-104">In questa esercitazione, è illustrato come toointegrate HireVue con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4cfd4-104">In this tutorial, you learn how toointegrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4cfd4-105">Integrazione HireVue con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-105">Integrating HireVue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4cfd4-106">È possibile controllare in Azure AD che ha accesso tooHireVue</span><span class="sxs-lookup"><span data-stu-id="4cfd4-106">You can control in Azure AD who has access tooHireVue</span></span>
- <span data-ttu-id="4cfd4-107">È possibile abilitare l'utenti tooautomatically get connesso tooHireVue (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cfd4-107">You can enable your users tooautomatically get signed-on tooHireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4cfd4-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4cfd4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4cfd4-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4cfd4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cfd4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4cfd4-110">Prerequisites</span></span>

<span data-ttu-id="4cfd4-111">integrazione di Azure AD con HireVue tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-111">tooconfigure Azure AD integration with HireVue, you need hello following items:</span></span>

- <span data-ttu-id="4cfd4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4cfd4-113">Sottoscrizione di HireVue abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4cfd4-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4cfd4-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4cfd4-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4cfd4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4cfd4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4cfd4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4cfd4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4cfd4-118">Scenario description</span></span>
<span data-ttu-id="4cfd4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4cfd4-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4cfd4-121">Aggiunta di HireVue dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4cfd4-121">Adding HireVue from hello gallery</span></span>
2. <span data-ttu-id="4cfd4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cfd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-hello-gallery"></a><span data-ttu-id="4cfd4-123">Aggiunta di HireVue dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4cfd4-123">Adding HireVue from hello gallery</span></span>
<span data-ttu-id="4cfd4-124">integrazione hello tooconfigure di HireVue in Azure AD, è necessario tooadd HireVue dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-124">tooconfigure hello integration of HireVue into Azure AD, you need tooadd HireVue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4cfd4-125">**tooadd HireVue dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4cfd4-125">**tooadd HireVue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cfd4-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4cfd4-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4cfd4-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4cfd4-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4cfd4-133">Nella casella di ricerca hello, digitare **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-133">In hello search box, type **HireVue**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="4cfd4-135">Nel riquadro dei risultati hello, selezionare **HireVue**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-135">In hello results panel, select **HireVue**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4cfd4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cfd4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4cfd4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HireVue in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4cfd4-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4cfd4-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in HireVue è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HireVue is tooa user in Azure AD.</span></span> <span data-ttu-id="4cfd4-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in HireVue deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-140">In other words, a link relationship between an Azure AD user and hello related user in HireVue needs toobe established.</span></span>

<span data-ttu-id="4cfd4-141">In HireVue, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-141">In HireVue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4cfd4-142">tooconfigure e prova AD Azure single sign-on con HireVue, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-142">tooconfigure and test Azure AD single sign-on with HireVue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4cfd4-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4cfd4-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4cfd4-145">**[Creazione di un utente test HireVue](#creating-a-hirevue-test-user)**  -toohave un equivalente di Britta Simon in HireVue che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - toohave a counterpart of Britta Simon in HireVue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4cfd4-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4cfd4-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4cfd4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cfd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4cfd4-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione HireVue.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="4cfd4-150">**Azure AD tooconfigure single sign-on con HireVue, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4cfd4-150">**tooconfigure Azure AD single sign-on with HireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cfd4-151">Nel portale di Azure su hello hello **HireVue** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-151">In hello Azure portal, on hello **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4cfd4-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="4cfd4-155">In hello **HireVue dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-155">On hello **HireVue Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="4cfd4-157">a.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-157">a.</span></span> <span data-ttu-id="4cfd4-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>

    | <span data-ttu-id="4cfd4-159">Environment</span><span class="sxs-lookup"><span data-stu-id="4cfd4-159">Environment</span></span> | <span data-ttu-id="4cfd4-160">URL</span><span class="sxs-lookup"><span data-stu-id="4cfd4-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="4cfd4-161">Produzione</span><span class="sxs-lookup"><span data-stu-id="4cfd4-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="4cfd4-162">Staging</span><span class="sxs-lookup"><span data-stu-id="4cfd4-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="4cfd4-163">b.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-163">b.</span></span> <span data-ttu-id="4cfd4-164">In hello **identificatore** casella di testo, digitare un URL come:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-164">In hello **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="4cfd4-165">Environment</span><span class="sxs-lookup"><span data-stu-id="4cfd4-165">Environment</span></span> | <span data-ttu-id="4cfd4-166">URN</span><span class="sxs-lookup"><span data-stu-id="4cfd4-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="4cfd4-167">Produzione</span><span class="sxs-lookup"><span data-stu-id="4cfd4-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="4cfd4-168">Staging</span><span class="sxs-lookup"><span data-stu-id="4cfd4-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="4cfd4-169">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4cfd4-169">These values are not real.</span></span> <span data-ttu-id="4cfd4-170">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-170">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4cfd4-171">Contatto [team di supporto HireVue Client](mailto:samlsupport@hirevue.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4cfd4-172">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-172">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="4cfd4-174">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4cfd4-174">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4cfd4-176">In hello **HireVue configurazione** fare clic su **configurare HireVue** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-176">On hello **HireVue Configuration** section, click **Configure HireVue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4cfd4-177">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4cfd4-177">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="4cfd4-179">tooconfigure single sign-on sul **HireVue** lato, è necessario hello toosend scaricato **Certificate(Base64)** e **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="4cfd4-179">tooconfigure single sign-on on **HireVue** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="4cfd4-180">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-180">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4cfd4-181">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4cfd4-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4cfd4-182">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4cfd4-183">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4cfd4-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4cfd4-184">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cfd4-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="4cfd4-185">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4cfd4-187">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4cfd4-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cfd4-188">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4cfd4-190">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4cfd4-192">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4cfd4-194">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4cfd4-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4cfd4-196">a.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-196">a.</span></span> <span data-ttu-id="4cfd4-197">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4cfd4-198">b.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-198">b.</span></span> <span data-ttu-id="4cfd4-199">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4cfd4-200">c.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-200">c.</span></span> <span data-ttu-id="4cfd4-201">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4cfd4-202">d.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-202">d.</span></span> <span data-ttu-id="4cfd4-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="4cfd4-204">Creazione di un utente test di HireVue</span><span class="sxs-lookup"><span data-stu-id="4cfd4-204">Creating a HireVue test user</span></span>

<span data-ttu-id="4cfd4-205">In questa sezione viene creato un utente di nome Britta Simon in HireVue.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="4cfd4-206">Rivolgersi [team di supporto HireVue](mailto:samlsupport@hirevue.com) utenti hello tooadd nella piattaforma HireVue hello.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) tooadd hello users in hello HireVue platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4cfd4-207">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cfd4-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4cfd4-208">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHireVue.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHireVue.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4cfd4-210">**tooassign Britta Simon tooHireVue, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4cfd4-210">**tooassign Britta Simon tooHireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cfd4-211">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4cfd4-213">Nell'elenco di applicazioni hello, selezionare **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-213">In hello applications list, select **HireVue**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="4cfd4-215">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4cfd4-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-217">Click **Add** button.</span></span> <span data-ttu-id="4cfd4-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4cfd4-220">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4cfd4-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4cfd4-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4cfd4-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4cfd4-223">Testing single sign-on</span></span>

<span data-ttu-id="4cfd4-224">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4cfd4-225">Quando si fa clic su riquadro HireVue hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour HireVue applicazione.</span><span class="sxs-lookup"><span data-stu-id="4cfd4-225">When you click hello HireVue tile in hello Access Panel, you should get automatically signed-on tooyour HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4cfd4-226">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4cfd4-226">Additional resources</span></span>

* [<span data-ttu-id="4cfd4-227">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4cfd4-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4cfd4-228">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4cfd4-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png


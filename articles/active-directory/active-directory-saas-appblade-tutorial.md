---
title: 'Esercitazione: Integrazione di Azure Active Directory con AppBlade | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e AppBlade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="42652-103">Esercitazione: Integrazione di Azure Active Directory con AppBlade</span><span class="sxs-lookup"><span data-stu-id="42652-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="42652-104">In questa esercitazione, è illustrato come toointegrate AppBlade con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42652-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42652-105">Integrazione AppBlade con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="42652-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42652-106">È possibile controllare in Azure AD che ha accesso tooAppBlade</span><span class="sxs-lookup"><span data-stu-id="42652-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="42652-107">È possibile abilitare l'utenti tooautomatically get connesso tooAppBlade (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="42652-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42652-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="42652-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="42652-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42652-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42652-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="42652-110">Prerequisites</span></span>

<span data-ttu-id="42652-111">integrazione di Azure AD con AppBlade tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="42652-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="42652-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42652-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42652-113">Sottoscrizione di AppBlade abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="42652-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42652-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="42652-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42652-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="42652-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42652-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="42652-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42652-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42652-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42652-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="42652-118">Scenario description</span></span>
<span data-ttu-id="42652-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="42652-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42652-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="42652-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42652-121">Aggiunta di AppBlade dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="42652-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="42652-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42652-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="42652-123">Aggiunta di AppBlade dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="42652-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="42652-124">integrazione hello tooconfigure di AppBlade in Azure AD, è necessario tooadd AppBlade dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="42652-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42652-125">**tooadd AppBlade dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="42652-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42652-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="42652-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42652-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="42652-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42652-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="42652-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="42652-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="42652-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="42652-133">Nella casella di ricerca hello, digitare **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="42652-133">In hello search box, type **AppBlade**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="42652-135">Nel riquadro dei risultati hello, selezionare **AppBlade**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="42652-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42652-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42652-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42652-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con AppBlade in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42652-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42652-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in AppBlade è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42652-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="42652-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in AppBlade deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="42652-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="42652-141">In AppBlade, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="42652-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="42652-142">tooconfigure e prova AD Azure single sign-on con AppBlade, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="42652-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42652-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="42652-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42652-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42652-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42652-145">**[Creazione di un utente test AppBlade](#creating-an-appblade-test-user)**  -toohave un equivalente di Britta Simon in AppBlade che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="42652-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42652-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42652-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42652-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="42652-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42652-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42652-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42652-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione AppBlade.</span><span class="sxs-lookup"><span data-stu-id="42652-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="42652-150">**Azure AD tooconfigure single sign-on con AppBlade, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="42652-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="42652-151">Nel portale di Azure su hello hello **AppBlade** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="42652-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="42652-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42652-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="42652-155">In hello **AppBlade dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="42652-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="42652-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="42652-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42652-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="42652-158">This value is not real.</span></span> <span data-ttu-id="42652-159">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="42652-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="42652-160">Contatto [team di supporto AppBlade Client](mailto:support@appblade.com) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="42652-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="42652-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="42652-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="42652-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="42652-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42652-165">tooconfigure single sign-on sul **AppBlade** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="42652-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="42652-166">Inoltre, chiedere loro hello tooconfigure **URL autorità di certificazione SSO** come `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="42652-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="42652-167">Questa impostazione è necessaria per single sign-on toowork.</span><span class="sxs-lookup"><span data-stu-id="42652-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="42652-168">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="42652-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42652-169">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="42652-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42652-170">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42652-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42652-171">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42652-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="42652-172">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="42652-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="42652-174">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="42652-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42652-175">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="42652-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42652-177">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="42652-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42652-179">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="42652-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42652-181">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="42652-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42652-183">a.</span><span class="sxs-lookup"><span data-stu-id="42652-183">a.</span></span> <span data-ttu-id="42652-184">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42652-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42652-185">b.</span><span class="sxs-lookup"><span data-stu-id="42652-185">b.</span></span> <span data-ttu-id="42652-186">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42652-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42652-187">c.</span><span class="sxs-lookup"><span data-stu-id="42652-187">c.</span></span> <span data-ttu-id="42652-188">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="42652-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42652-189">d.</span><span class="sxs-lookup"><span data-stu-id="42652-189">d.</span></span> <span data-ttu-id="42652-190">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="42652-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="42652-191">Creazione di un utente di test AppBlade</span><span class="sxs-lookup"><span data-stu-id="42652-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="42652-192">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in AppBlade toocreate.</span><span class="sxs-lookup"><span data-stu-id="42652-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="42652-193">AppBlade supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="42652-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="42652-194">**Assicurarsi che il nome di dominio sia configurato con AppBlade per il provisioning utente. Dopo che solo hello-in-time di provisioning dell'utente funziona.**</span><span class="sxs-lookup"><span data-stu-id="42652-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="42652-195">Se l'utente di hello dispone di un indirizzo di posta elettronica che terminano con il dominio hello configurato da AppBlade per l'account, quindi utente hello verrà automaticamente aggiunti account hello come un membro con il livello di autorizzazione hello specificato, ovvero una delle "Basic" (un utente di base che può essere installato solo applicazioni), "Membro del Team", un utente in grado di caricare nuove versioni di app e gestire progetti, o "Administrator" (account toohello privilegi di amministratore completo).</span><span class="sxs-lookup"><span data-stu-id="42652-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="42652-196">In genere uno sarebbe scegliere base e quindi alzare di livello utenti manualmente tramite un account di accesso di amministratore (AppBlade deve tooconfigure a un account di accesso di amministrazione basata su posta elettronica in anticipo o alzare di livello un utente per conto cliente hello dopo l'accesso).</span><span class="sxs-lookup"><span data-stu-id="42652-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="42652-197">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="42652-197">There is no action item for you in this section.</span></span> <span data-ttu-id="42652-198">Se non esiste ancora, durante un tooaccess tentativo AppBlade viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="42652-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="42652-199">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="42652-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42652-200">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="42652-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42652-201">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAppBlade.</span><span class="sxs-lookup"><span data-stu-id="42652-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Assegna utente][200] 

<span data-ttu-id="42652-203">**tooassign Britta Simon tooAppBlade, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="42652-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="42652-204">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="42652-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="42652-206">Nell'elenco di applicazioni hello, selezionare **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="42652-206">In hello applications list, select **AppBlade**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="42652-208">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="42652-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="42652-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="42652-210">Click **Add** button.</span></span> <span data-ttu-id="42652-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="42652-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="42652-213">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="42652-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42652-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="42652-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42652-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="42652-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42652-216">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="42652-216">Testing single sign-on</span></span>

<span data-ttu-id="42652-217">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="42652-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="42652-218">Quando si fa clic su riquadro AppBlade hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour AppBlade applicazione.</span><span class="sxs-lookup"><span data-stu-id="42652-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42652-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="42652-219">Additional resources</span></span>

* [<span data-ttu-id="42652-220">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42652-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42652-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42652-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png


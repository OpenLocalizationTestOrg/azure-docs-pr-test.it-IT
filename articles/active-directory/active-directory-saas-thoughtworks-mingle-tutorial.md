---
title: 'Esercitazione: Integrazione di Azure Active Directory con Thoughtworks Mingle | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Thoughtworks Mingle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="6f584-103">Esercitazione: Integrazione di Azure Active Directory con Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="6f584-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="6f584-104">In questa esercitazione, è illustrato come toointegrate Thoughtworks Mingle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f584-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f584-105">Integrazione di Thoughtworks Mingle con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6f584-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f584-106">È possibile controllare in Azure AD che ha accesso tooThoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="6f584-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="6f584-107">È possibile abilitare l'utenti tooautomatically get connesso tooThoughtworks Mingle (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f584-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f584-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6f584-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6f584-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f584-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f584-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f584-110">Prerequisites</span></span>

<span data-ttu-id="6f584-111">integrazione di Azure AD con Thoughtworks Mingle tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6f584-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="6f584-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f584-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f584-113">Sottoscrizione di Thoughtworks Mingle abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f584-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f584-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6f584-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f584-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6f584-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f584-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6f584-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f584-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f584-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f584-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6f584-118">Scenario description</span></span>
<span data-ttu-id="6f584-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6f584-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f584-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6f584-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f584-121">Aggiunta di Thoughtworks Mingle dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6f584-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="6f584-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f584-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="6f584-123">Aggiunta di Thoughtworks Mingle dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6f584-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="6f584-124">integrazione hello tooconfigure di Thoughtworks Mingle in Azure AD, è necessario tooadd Thoughtworks Mingle dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6f584-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f584-125">**tooadd Thoughtworks Mingle dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f584-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f584-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6f584-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="6f584-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6f584-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f584-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f584-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="6f584-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6f584-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="6f584-133">Nella casella di ricerca hello, digitare **Thoughtworks Mingle**selezionare **Thoughtworks Mingle** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6f584-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Thoughtworks Mingle nell'elenco risultati hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6f584-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f584-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6f584-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Thoughtworks Mingle usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f584-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f584-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Thoughtworks Mingle è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f584-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="6f584-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Thoughtworks Mingle deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6f584-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="6f584-139">In Thoughtworks Mingle, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6f584-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6f584-140">tooconfigure e prova AD Azure single sign-on con Thoughtworks Mingle, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6f584-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f584-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6f584-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f584-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f584-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f584-143">**[Creare un utente test Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave un equivalente di Britta Simon in Thoughtworks Mingle che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6f584-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f584-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6f584-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f584-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6f584-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6f584-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f584-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6f584-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="6f584-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="6f584-148">**Azure AD tooconfigure single sign-on con Thoughtworks Mingle, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f584-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f584-149">Nel portale di Azure su hello hello **Thoughtworks Mingle** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6f584-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6f584-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6f584-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="6f584-153">In hello **Thoughtworks Mingle dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f584-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="6f584-155">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="6f584-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f584-156">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="6f584-156">hello value is not real.</span></span> <span data-ttu-id="6f584-157">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6f584-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6f584-158">Contatto [team di supporto Client di Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="6f584-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="6f584-159">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6f584-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="6f584-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6f584-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f584-163">Accedi tooyour **Thoughtworks Mingle** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f584-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="6f584-164">Fare clic su hello **Admin** scheda e quindi fare clic su **SSO Config**.</span><span class="sxs-lookup"><span data-stu-id="6f584-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="6f584-165">![Scheda Amministrazione](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Config SSO")</span><span class="sxs-lookup"><span data-stu-id="6f584-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="6f584-166">In hello **SSO Config** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f584-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6f584-167">![Configurazione dell'accesso SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configurazione dell'accesso SSO")</span><span class="sxs-lookup"><span data-stu-id="6f584-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="6f584-168">a.</span><span class="sxs-lookup"><span data-stu-id="6f584-168">a.</span></span> <span data-ttu-id="6f584-169">file di metadati hello tooupload, fare clic su **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="6f584-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="6f584-170">b.</span><span class="sxs-lookup"><span data-stu-id="6f584-170">b.</span></span> <span data-ttu-id="6f584-171">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="6f584-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6f584-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6f584-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f584-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6f584-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f584-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f584-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6f584-175">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f584-175">Create an Azure AD test user</span></span>
<span data-ttu-id="6f584-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6f584-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="6f584-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f584-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f584-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6f584-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f584-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6f584-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f584-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6f584-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f584-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f584-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f584-187">a.</span><span class="sxs-lookup"><span data-stu-id="6f584-187">a.</span></span> <span data-ttu-id="6f584-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f584-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f584-189">b.</span><span class="sxs-lookup"><span data-stu-id="6f584-189">b.</span></span> <span data-ttu-id="6f584-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f584-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f584-191">c.</span><span class="sxs-lookup"><span data-stu-id="6f584-191">c.</span></span> <span data-ttu-id="6f584-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6f584-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6f584-193">d.</span><span class="sxs-lookup"><span data-stu-id="6f584-193">d.</span></span> <span data-ttu-id="6f584-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6f584-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="6f584-195">Creare un utente di test di Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="6f584-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="6f584-196">Per Azure AD utenti toobe in grado di toosign in devono essere sottoposte a provisioning toohello applicazione Thoughtworks Mingle usando i rispettivi nomi utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6f584-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="6f584-197">Nel caso di hello di Thoughtworks Mingle, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="6f584-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="6f584-198">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f584-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f584-199">Accedi tooyour del sito della società Thoughtworks Mingle come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f584-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="6f584-200">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="6f584-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="6f584-201">![Primo progetto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Primo progetto")</span><span class="sxs-lookup"><span data-stu-id="6f584-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="6f584-202">Fare clic su hello **Admin** scheda e quindi fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="6f584-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="6f584-203">![Utenti](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="6f584-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="6f584-204">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="6f584-204">Click **New User**.</span></span>
   
    <span data-ttu-id="6f584-205">![Nuovo utente](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="6f584-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="6f584-206">In hello **nuovo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f584-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="6f584-207">![Finestra di dialogo Nuovo utente](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="6f584-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="6f584-208">a.</span><span class="sxs-lookup"><span data-stu-id="6f584-208">a.</span></span> <span data-ttu-id="6f584-209">Hello tipo **nome di accesso**, **nome visualizzato**, **scegliere password**, **Conferma password** di Azure un valido account di Active Directory, si desidera tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="6f584-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="6f584-210">b.</span><span class="sxs-lookup"><span data-stu-id="6f584-210">b.</span></span> <span data-ttu-id="6f584-211">In **Tipo di utente** selezionare **Base**.</span><span class="sxs-lookup"><span data-stu-id="6f584-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="6f584-212">c.</span><span class="sxs-lookup"><span data-stu-id="6f584-212">c.</span></span> <span data-ttu-id="6f584-213">Fare clic su **Crea questo profilo**.</span><span class="sxs-lookup"><span data-stu-id="6f584-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="6f584-214">È possibile usare qualsiasi altro Thoughtworks Mingle utente account strumento di creazione o le API fornite da Thoughtworks Mingle tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="6f584-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6f584-215">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f584-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6f584-216">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooThoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="6f584-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="6f584-218">**tooassign tooThoughtworks Britta Simon Mingle, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f584-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f584-219">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f584-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6f584-221">Nell'elenco di applicazioni hello, selezionare **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="6f584-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![collegamento di Thoughtworks Mingle Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="6f584-223">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f584-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="6f584-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6f584-225">Click **Add** button.</span></span> <span data-ttu-id="6f584-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f584-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="6f584-228">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6f584-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f584-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f584-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f584-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f584-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6f584-231">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f584-231">Test single sign-on</span></span>

<span data-ttu-id="6f584-232">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6f584-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f584-233">Quando si fa clic su riquadro Thoughtworks Mingle hello in hello Pannello di accesso, è necessario ottenere applicazione Thoughtworks Mingle tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="6f584-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f584-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6f584-234">Additional resources</span></span>

* [<span data-ttu-id="6f584-235">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f584-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f584-236">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f584-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png


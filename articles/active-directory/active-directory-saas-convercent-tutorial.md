---
title: 'Esercitazione: Integrazione di Azure Active Directory con Convercent | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Convercent.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: e6d09d7de52779dcf05e80215df9369ebc2ed06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="f1655-103">Esercitazione: Integrazione di Azure Active Directory con Convercent</span><span class="sxs-lookup"><span data-stu-id="f1655-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="f1655-104">In questa esercitazione, è illustrato come toointegrate Convercent con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1655-104">In this tutorial, you learn how toointegrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1655-105">Integrazione Convercent con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f1655-105">Integrating Convercent with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1655-106">È possibile controllare in Azure AD che ha accesso tooConvercent</span><span class="sxs-lookup"><span data-stu-id="f1655-106">You can control in Azure AD who has access tooConvercent</span></span>
- <span data-ttu-id="f1655-107">È possibile abilitare l'utenti tooautomatically get connesso tooConvercent (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1655-107">You can enable your users tooautomatically get signed-on tooConvercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1655-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f1655-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1655-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1655-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1655-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1655-110">Prerequisites</span></span>

<span data-ttu-id="f1655-111">integrazione di Azure AD con Convercent tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f1655-111">tooconfigure Azure AD integration with Convercent, you need hello following items:</span></span>

- <span data-ttu-id="f1655-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1655-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1655-113">Sottoscrizione di Convercent abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f1655-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1655-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f1655-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1655-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f1655-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1655-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f1655-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1655-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1655-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1655-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f1655-118">Scenario description</span></span>
<span data-ttu-id="f1655-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f1655-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1655-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f1655-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1655-121">Aggiunta di Convercent dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f1655-121">Adding Convercent from hello gallery</span></span>
2. <span data-ttu-id="f1655-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1655-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-hello-gallery"></a><span data-ttu-id="f1655-123">Aggiunta di Convercent dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f1655-123">Adding Convercent from hello gallery</span></span>
<span data-ttu-id="f1655-124">integrazione hello tooconfigure di Convercent in Azure AD, è necessario tooadd Convercent dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f1655-124">tooconfigure hello integration of Convercent into Azure AD, you need tooadd Convercent from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1655-125">**tooadd Convercent dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1655-125">**tooadd Convercent from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1655-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f1655-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1655-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f1655-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1655-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f1655-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f1655-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f1655-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f1655-133">Nella casella di ricerca hello, digitare **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="f1655-133">In hello search box, type **Convercent**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="f1655-135">Nel riquadro dei risultati hello, selezionare **Convercent**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f1655-135">In hello results panel, select **Convercent**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1655-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1655-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1655-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Convercent mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f1655-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1655-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Convercent è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1655-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Convercent is tooa user in Azure AD.</span></span> <span data-ttu-id="f1655-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Convercent deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f1655-140">In other words, a link relationship between an Azure AD user and hello related user in Convercent needs toobe established.</span></span>

<span data-ttu-id="f1655-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Convercent.</span><span class="sxs-lookup"><span data-stu-id="f1655-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Convercent.</span></span>

<span data-ttu-id="f1655-142">tooconfigure e prova AD Azure single sign-on con Convercent, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f1655-142">tooconfigure and test Azure AD single sign-on with Convercent, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1655-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f1655-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1655-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1655-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1655-145">**[Creazione di un utente test Convercent](#creating-a-convercent-test-user)**  -toohave un equivalente di Britta Simon in Convercent che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f1655-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - toohave a counterpart of Britta Simon in Convercent that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1655-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1655-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1655-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f1655-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1655-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1655-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1655-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Convercent.</span><span class="sxs-lookup"><span data-stu-id="f1655-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="f1655-150">**Azure AD tooconfigure single sign-on con Convercent, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1655-150">**tooconfigure Azure AD single sign-on with Convercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1655-151">Nel portale di Azure su hello hello **Convercent** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f1655-151">In hello Azure portal, on hello **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f1655-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1655-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="f1655-155">In hello **Convercent dominio e gli URL** sezione, se si desidera un'applicazione hello tooconfigure in **modalità avviata da IDP**, eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="f1655-155">On hello **Convercent Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="f1655-157">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="f1655-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="f1655-158">Se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, su hello **Convercent dominio e gli URL** sezione eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f1655-158">If you wish tooconfigure hello application in **SP initiated mode**, on hello **Convercent Domain and URLs** section perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="f1655-160">a.</span><span class="sxs-lookup"><span data-stu-id="f1655-160">a.</span></span> <span data-ttu-id="f1655-161">Fare clic su **Mostra impostazioni URL avanzate**.</span><span class="sxs-lookup"><span data-stu-id="f1655-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="f1655-162">b.</span><span class="sxs-lookup"><span data-stu-id="f1655-162">b.</span></span> <span data-ttu-id="f1655-163">In hello **URL di accesso** casella di testo, valore di tipo hello utilizzando hello modello:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="f1655-163">In hello **Sign On URL** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="f1655-164">c.</span><span class="sxs-lookup"><span data-stu-id="f1655-164">c.</span></span> <span data-ttu-id="f1655-165">In hello **stato inoltro** casella di testo, valore di tipo hello utilizzando hello modello:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="f1655-165">In hello **Relay State** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1655-166">Questi valori non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="f1655-166">These values are not hello real values.</span></span> <span data-ttu-id="f1655-167">Aggiornare questi valori con hello effettivo identificatore, URL di accesso e lo stato di inoltro.</span><span class="sxs-lookup"><span data-stu-id="f1655-167">Update these values with hello actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="f1655-168">Contatto [team di supporto Convercent Client](http://support.convercent.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="f1655-168">Contact [Convercent Client support team](http://support.convercent.com) tooget these values.</span></span>

5. <span data-ttu-id="f1655-169">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f1655-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="f1655-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f1655-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f1655-173">tooget SSO è configurato per l'applicazione, contattare [team di supporto Convercent](mailto:support@convercent.com) e fornire loro hello scaricato **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="f1655-173">tooget SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with hello downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="f1655-174">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f1655-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1655-175">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f1655-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1655-176">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1655-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1655-177">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1655-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1655-178">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1655-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f1655-180">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1655-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1655-181">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f1655-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1655-183">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f1655-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1655-185">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f1655-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1655-187">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f1655-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1655-189">a.</span><span class="sxs-lookup"><span data-stu-id="f1655-189">a.</span></span> <span data-ttu-id="f1655-190">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1655-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1655-191">b.</span><span class="sxs-lookup"><span data-stu-id="f1655-191">b.</span></span> <span data-ttu-id="f1655-192">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1655-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1655-193">c.</span><span class="sxs-lookup"><span data-stu-id="f1655-193">c.</span></span> <span data-ttu-id="f1655-194">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f1655-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1655-195">d.</span><span class="sxs-lookup"><span data-stu-id="f1655-195">d.</span></span> <span data-ttu-id="f1655-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f1655-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="f1655-197">Creazione di un utente test di Convercent</span><span class="sxs-lookup"><span data-stu-id="f1655-197">Creating a Convercent test user</span></span>

<span data-ttu-id="f1655-198">Lavorare con [team di supporto Convercent](mailto:support@convercent.com) utenti hello tooadd nella piattaforma Convercent hello.</span><span class="sxs-lookup"><span data-stu-id="f1655-198">Work with [Convercent support team](mailto:support@convercent.com) tooadd hello users in hello Convercent platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1655-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1655-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1655-200">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooConvercent.</span><span class="sxs-lookup"><span data-stu-id="f1655-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConvercent.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f1655-202">**tooassign Britta Simon tooConvercent, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1655-202">**tooassign Britta Simon tooConvercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1655-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f1655-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f1655-205">Nell'elenco di applicazioni hello, selezionare **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="f1655-205">In hello applications list, select **Convercent**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="f1655-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f1655-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f1655-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f1655-209">Click **Add** button.</span></span> <span data-ttu-id="f1655-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f1655-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f1655-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f1655-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1655-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f1655-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1655-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f1655-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1655-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f1655-215">Testing single sign-on</span></span>

<span data-ttu-id="f1655-216">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f1655-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1655-217">Quando si fa clic su riquadro Convercent hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Convercent applicazione.</span><span class="sxs-lookup"><span data-stu-id="f1655-217">When you click hello Convercent tile in hello Access Panel, you should get automatically signed-on tooyour Convercent application.</span></span>
<span data-ttu-id="f1655-218">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1655-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f1655-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f1655-219">Additional resources</span></span>

* [<span data-ttu-id="f1655-220">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1655-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1655-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1655-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png


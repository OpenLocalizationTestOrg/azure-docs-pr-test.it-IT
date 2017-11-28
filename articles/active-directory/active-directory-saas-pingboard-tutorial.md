---
title: 'Esercitazione: Integrazione di Azure Active Directory con PingBoard | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Pingboard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="c5a4c-103">Esercitazione: Integrazione di Azure Active Directory con PingBoard</span><span class="sxs-lookup"><span data-stu-id="c5a4c-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="c5a4c-104">In questa esercitazione, è illustrato come toointegrate Pingboard con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5a4c-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5a4c-105">Integrazione Pingboard con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5a4c-106">È possibile controllare in Azure AD che ha accesso tooPingboard</span><span class="sxs-lookup"><span data-stu-id="c5a4c-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="c5a4c-107">È possibile abilitare l'utenti tooautomatically get connesso tooPingboard (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5a4c-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5a4c-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="c5a4c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="c5a4c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5a4c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5a4c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c5a4c-110">Prerequisites</span></span>

<span data-ttu-id="c5a4c-111">integrazione di Azure AD con Pingboard tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="c5a4c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5a4c-113">Sottoscrizione di PingBoard abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c5a4c-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5a4c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5a4c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5a4c-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c5a4c-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5a4c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5a4c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c5a4c-118">Scenario description</span></span>
<span data-ttu-id="c5a4c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5a4c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5a4c-121">Aggiunta di Pingboard dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c5a4c-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="c5a4c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5a4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="c5a4c-123">Aggiunta di Pingboard dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c5a4c-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="c5a4c-124">integrazione hello tooconfigure di Pingboard in Azure AD, è necessario tooadd Pingboard dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5a4c-125">**tooadd Pingboard dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5a4c-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5a4c-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5a4c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5a4c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c5a4c-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c5a4c-133">Nella casella di ricerca hello, digitare **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-133">In hello search box, type **Pingboard**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="c5a4c-135">Nel riquadro dei risultati hello, selezionare **Pingboard**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5a4c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5a4c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5a4c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PingBoard con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c5a4c-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5a4c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Pingboard è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="c5a4c-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Pingboard deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="c5a4c-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="c5a4c-142">tooconfigure e prova AD Azure single sign-on con Pingboard, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5a4c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5a4c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5a4c-145">**[Creazione di un utente test Pingboard](#creating-a-pingboard-test-user)**  -toohave un equivalente di Britta Simon in Pingboard toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c5a4c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5a4c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5a4c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5a4c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5a4c-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione Pingboard.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="c5a4c-150">**Azure AD tooconfigure single sign-on con Pingboard, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5a4c-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5a4c-151">Nel portale di gestione di Azure hello in hello **Pingboard** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c5a4c-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="c5a4c-155">In hello **Pingboard dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="c5a4c-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-157">a.</span></span> <span data-ttu-id="c5a4c-158">In hello **identificatore** casella di testo, tipo di valore hello di:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="c5a4c-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="c5a4c-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-159">b.</span></span> <span data-ttu-id="c5a4c-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="c5a4c-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5a4c-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="c5a4c-162">È necessario tooupdate questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c5a4c-163">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="c5a4c-164">Contatto [team di supporto Pingboard Client](https://support.pingboard.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="c5a4c-165">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="c5a4c-167">a.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-167">a.</span></span> <span data-ttu-id="c5a4c-168">In hello **Sign-on URL** casella di testo, tipo di valore hello di:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="c5a4c-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="c5a4c-169">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="c5a4c-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c5a4c-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c5a4c-173">tooconfigure SSO sul lato Pingboard, aprire una nuova finestra del browser e accedere tooyour Pingboard Account.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="c5a4c-174">In, è necessario essere un tooset admin Pingboard backup singolo segno.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="c5a4c-175">Scegliere dal menu in alto hello **App > integrazioni**</span><span class="sxs-lookup"><span data-stu-id="c5a4c-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="c5a4c-177">In hello **integrazioni** pagina, trovare hello **"Di Azure Active Directory"** riquadro e farvi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="c5a4c-179">In hello modale che segue fare clic su **"Configura"**</span><span class="sxs-lookup"><span data-stu-id="c5a4c-179">In hello modal that follows click **"Configure"**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="c5a4c-181">Nella seguente pagina di hello, si noterà che "integrazione di Azure SSO è abilitato.".</span><span class="sxs-lookup"><span data-stu-id="c5a4c-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="c5a4c-182">Aprire hello scaricati file Metadata XML in un blocco note e incollare hello è contenuto in **IDP Metadata**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="c5a4c-184">file Hello verrà convalidato e se le informazioni sono corrette, single sign-on verrà abilitata</span><span class="sxs-lookup"><span data-stu-id="c5a4c-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5a4c-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5a4c-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5a4c-186">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c5a4c-188">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5a4c-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5a4c-189">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5a4c-191">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5a4c-193">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5a4c-195">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c5a4c-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5a4c-197">a.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-197">a.</span></span> <span data-ttu-id="c5a4c-198">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5a4c-199">b.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-199">b.</span></span> <span data-ttu-id="c5a4c-200">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5a4c-201">c.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-201">c.</span></span> <span data-ttu-id="c5a4c-202">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5a4c-203">d.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-203">d.</span></span> <span data-ttu-id="c5a4c-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="c5a4c-205">Creazione di un utente test PingBoard</span><span class="sxs-lookup"><span data-stu-id="c5a4c-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="c5a4c-206">In ordine tooenable Azure AD utenti toolog in Pingboard, è necessario eseguirne il provisioning in Pingboard.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="c5a4c-207">Nel caso di hello di Pingboard, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="c5a4c-208">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="c5a4c-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5a4c-209">Accedi tooyour sito della società Pingboard come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="c5a4c-210">Fare clic sul pulsante **"Add Employee"** ("Aggiungi dipendente") nella pagina **Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="c5a4c-212">In hello **"Add Employee"** finestra di dialogo eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Invita persone](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="c5a4c-214">a.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-214">a.</span></span> <span data-ttu-id="c5a4c-215">In hello **nome completo** casella di testo, nome completo del tipo hello di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="c5a4c-216">b.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-216">b.</span></span> <span data-ttu-id="c5a4c-217">In hello **posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="c5a4c-218">c.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-218">c.</span></span> <span data-ttu-id="c5a4c-219">In hello **titolo professionale** casella di testo, titolo professionale hello di tipo di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="c5a4c-220">d.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-220">d.</span></span> <span data-ttu-id="c5a4c-221">In hello **percorso** percorso selezionare hello di Britta Simon elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="c5a4c-222">e.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-222">e.</span></span> <span data-ttu-id="c5a4c-223">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-223">Click **Add**.</span></span>   

4. <span data-ttu-id="c5a4c-224">Schermata di conferma comparirà aggiunta hello tooconfirm dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![confermare](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="c5a4c-226">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5a4c-227">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5a4c-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5a4c-228">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooPingboard proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c5a4c-230">**tooassign Britta Simon tooPingboard, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c5a4c-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5a4c-231">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c5a4c-233">Nell'elenco di applicazioni hello, selezionare **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-233">In hello applications list, select **Pingboard**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="c5a4c-235">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c5a4c-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-237">Click **Add** button.</span></span> <span data-ttu-id="c5a4c-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c5a4c-240">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5a4c-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5a4c-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5a4c-243">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c5a4c-243">Testing single sign-on</span></span>

<span data-ttu-id="c5a4c-244">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5a4c-245">Quando si fa clic su riquadro Pingboard hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Pingboard applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5a4c-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5a4c-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c5a4c-246">Additional resources</span></span>

* [<span data-ttu-id="c5a4c-247">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5a4c-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5a4c-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5a4c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png

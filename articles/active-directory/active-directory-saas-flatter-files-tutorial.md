---
title: Esercitazione Integrazione di Azure Active Directory con Flatter Files | Documentazione Microsoft
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e i file più semplice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="b5171-103">Esercitazione: Integrazione di Azure Active Directory con Flatter Files</span><span class="sxs-lookup"><span data-stu-id="b5171-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="b5171-104">In questa esercitazione, è illustrato come toointegrate file più semplice con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5171-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5171-105">I file più semplice l'integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b5171-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5171-106">È possibile controllare in Azure AD che ha accesso file tooFlatter</span><span class="sxs-lookup"><span data-stu-id="b5171-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="b5171-107">È possibile abilitare il tooautomatically utenti ottenere i file firmati in tooFlatter (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5171-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5171-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b5171-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b5171-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5171-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5171-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b5171-110">Prerequisites</span></span>

<span data-ttu-id="b5171-111">tooconfigure integrazione di Azure AD con i file più semplice, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b5171-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="b5171-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5171-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5171-113">Sottoscrizione di Flatter Files abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b5171-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5171-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b5171-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5171-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b5171-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5171-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b5171-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5171-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5171-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5171-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b5171-118">Scenario description</span></span>
<span data-ttu-id="b5171-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b5171-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5171-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b5171-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5171-121">Aggiunta di file più semplice dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b5171-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="b5171-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5171-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="b5171-123">Aggiunta di file più semplice dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b5171-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="b5171-124">integrazione hello tooconfigure di file più semplice in Azure AD, è necessario tooadd più semplice di file dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b5171-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5171-125">**tooadd più semplice di file dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5171-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5171-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b5171-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5171-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b5171-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b5171-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b5171-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b5171-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b5171-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b5171-133">Nella casella di ricerca hello, digitare **più piana file**.</span><span class="sxs-lookup"><span data-stu-id="b5171-133">In hello search box, type **Flatter Files**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="b5171-135">Nel riquadro dei risultati hello, selezionare **file più piana**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b5171-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5171-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5171-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5171-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Flatter Files mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b5171-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5171-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in file più semplice è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5171-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="b5171-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in file più semplice richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b5171-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="b5171-141">Nei file più semplice, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="b5171-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b5171-142">tooconfigure e prova AD Azure single sign-on con i file più semplice, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b5171-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5171-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b5171-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5171-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5171-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5171-145">**[Creazione di un utente di test di file più piana](#creating-a-flatter-files-test-user)**  -toohave un equivalente di Britta Simon in file più semplice che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b5171-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5171-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b5171-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5171-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b5171-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5171-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5171-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5171-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione i file più semplice.</span><span class="sxs-lookup"><span data-stu-id="b5171-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="b5171-150">**tooconfigure AD Azure single sign-on con i file più semplice, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5171-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5171-151">Nel portale di Azure su hello hello **file più piana** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b5171-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b5171-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b5171-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="b5171-155">In hello **più semplice file di dominio e gli URL** sezione, hello utente non dispone di tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.</span><span class="sxs-lookup"><span data-stu-id="b5171-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="b5171-157">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b5171-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="b5171-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b5171-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b5171-161">In hello **più semplice file di configurazione** fare clic su **configurazione più semplice file** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="b5171-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b5171-162">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b5171-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="b5171-164">Sign-on tooyour applicazione più semplice file come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b5171-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="b5171-165">Fare clic su **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="b5171-165">Click **DASHBOARD**.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="b5171-167">Fare clic su **impostazioni**e quindi eseguire hello seguendo i passaggi hello **aziendale** scheda:</span><span class="sxs-lookup"><span data-stu-id="b5171-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="b5171-169">a.</span><span class="sxs-lookup"><span data-stu-id="b5171-169">a.</span></span> <span data-ttu-id="b5171-170">Selezionare **Use SAML 2.0 for Authentication**.</span><span class="sxs-lookup"><span data-stu-id="b5171-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="b5171-171">b.</span><span class="sxs-lookup"><span data-stu-id="b5171-171">b.</span></span> <span data-ttu-id="b5171-172">Fare clic su **Configure SAML**.</span><span class="sxs-lookup"><span data-stu-id="b5171-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="b5171-173">In hello **configurazione SAML** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5171-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="b5171-175">a.</span><span class="sxs-lookup"><span data-stu-id="b5171-175">a.</span></span> <span data-ttu-id="b5171-176">In hello **dominio** casella di testo, digitare il dominio registrato.</span><span class="sxs-lookup"><span data-stu-id="b5171-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="b5171-177">Se ancora non si ha un dominio registrato, contattare il team di supporto di Flatter Files all'indirizzo [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="b5171-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="b5171-178">b.</span><span class="sxs-lookup"><span data-stu-id="b5171-178">b.</span></span> <span data-ttu-id="b5171-179">In **Identity Provider URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato modulo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5171-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="b5171-180">c.</span><span class="sxs-lookup"><span data-stu-id="b5171-180">c.</span></span>  <span data-ttu-id="b5171-181">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **Identity Provider Certificate** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b5171-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="b5171-182">d.</span><span class="sxs-lookup"><span data-stu-id="b5171-182">d.</span></span> <span data-ttu-id="b5171-183">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="b5171-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="b5171-184">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b5171-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5171-185">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b5171-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5171-186">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5171-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5171-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5171-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5171-188">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b5171-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b5171-190">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5171-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5171-191">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b5171-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5171-193">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b5171-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5171-195">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b5171-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5171-197">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5171-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5171-199">a.</span><span class="sxs-lookup"><span data-stu-id="b5171-199">a.</span></span> <span data-ttu-id="b5171-200">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5171-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5171-201">b.</span><span class="sxs-lookup"><span data-stu-id="b5171-201">b.</span></span> <span data-ttu-id="b5171-202">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b5171-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5171-203">c.</span><span class="sxs-lookup"><span data-stu-id="b5171-203">c.</span></span> <span data-ttu-id="b5171-204">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="b5171-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b5171-205">d.</span><span class="sxs-lookup"><span data-stu-id="b5171-205">d.</span></span> <span data-ttu-id="b5171-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b5171-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="b5171-207">Creazione di un utente test per Flatter Files</span><span class="sxs-lookup"><span data-stu-id="b5171-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="b5171-208">obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon nei file più semplice.</span><span class="sxs-lookup"><span data-stu-id="b5171-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="b5171-209">**un utente denominato Britta Simon in file più semplice, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5171-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5171-210">Accesso tooyour **file più piana** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b5171-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="b5171-211">Nel riquadro di spostamento hello hello sinistra, fare clic su **impostazioni**, quindi fare clic su hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="b5171-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Creare un utente in Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="b5171-213">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="b5171-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="b5171-214">In hello **Aggiungi utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5171-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Creare un utente in Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="b5171-216">a.</span><span class="sxs-lookup"><span data-stu-id="b5171-216">a.</span></span> <span data-ttu-id="b5171-217">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="b5171-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="b5171-218">b.</span><span class="sxs-lookup"><span data-stu-id="b5171-218">b.</span></span> <span data-ttu-id="b5171-219">In hello **cognome** casella tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b5171-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="b5171-220">c.</span><span class="sxs-lookup"><span data-stu-id="b5171-220">c.</span></span> <span data-ttu-id="b5171-221">In hello **indirizzo di posta elettronica** casella di testo, digitare l'indirizzo di posta elettronica di Sandro in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5171-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="b5171-222">d.</span><span class="sxs-lookup"><span data-stu-id="b5171-222">d.</span></span> <span data-ttu-id="b5171-223">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="b5171-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b5171-224">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5171-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b5171-225">In questa sezione, si abilita Britta Simon toouse single sign-on Azure tramite la concessione di accedere ai file tooFlatter.</span><span class="sxs-lookup"><span data-stu-id="b5171-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b5171-227">**tooassign Britta Simon tooFlatter file, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5171-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5171-228">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b5171-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b5171-230">Nell'elenco di applicazioni hello, selezionare **più piana file**.</span><span class="sxs-lookup"><span data-stu-id="b5171-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="b5171-232">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b5171-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b5171-234">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b5171-234">Click **Add** button.</span></span> <span data-ttu-id="b5171-235">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b5171-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b5171-237">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b5171-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5171-238">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b5171-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5171-239">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b5171-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5171-240">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b5171-240">Testing single sign-on</span></span>

<span data-ttu-id="b5171-241">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b5171-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b5171-242">Quando si fa clic hello file più semplice riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione i file più semplice.</span><span class="sxs-lookup"><span data-stu-id="b5171-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="b5171-243">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5171-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5171-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b5171-244">Additional resources</span></span>

* [<span data-ttu-id="b5171-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5171-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5171-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5171-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png


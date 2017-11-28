---
title: 'Esercitazione: Integrazione di Azure Active Directory con Lecorpio | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Lecorpio.
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
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 963eb36678c589f942f63c7ab555161255324717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="c1476-103">Esercitazione: Integrazione di Azure Active Directory con Lecorpio</span><span class="sxs-lookup"><span data-stu-id="c1476-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="c1476-104">In questa esercitazione, è illustrato come toointegrate Lecorpio con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1476-104">In this tutorial, you learn how toointegrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1476-105">Integrazione Lecorpio con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="c1476-105">Integrating Lecorpio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c1476-106">È possibile controllare in Azure AD che ha accesso tooLecorpio</span><span class="sxs-lookup"><span data-stu-id="c1476-106">You can control in Azure AD who has access tooLecorpio</span></span>
- <span data-ttu-id="c1476-107">È possibile abilitare l'utenti tooautomatically get connesso tooLecorpio (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1476-107">You can enable your users tooautomatically get signed-on tooLecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1476-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c1476-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c1476-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1476-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1476-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c1476-110">Prerequisites</span></span>

<span data-ttu-id="c1476-111">integrazione di Azure AD con Lecorpio tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c1476-111">tooconfigure Azure AD integration with Lecorpio, you need hello following items:</span></span>

- <span data-ttu-id="c1476-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1476-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1476-113">Sottoscrizione di Lecorpio abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c1476-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1476-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c1476-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1476-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="c1476-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1476-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c1476-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1476-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1476-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1476-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c1476-118">Scenario description</span></span>
<span data-ttu-id="c1476-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c1476-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1476-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="c1476-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1476-121">Aggiunta di Lecorpio dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c1476-121">Adding Lecorpio from hello gallery</span></span>
2. <span data-ttu-id="c1476-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1476-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-hello-gallery"></a><span data-ttu-id="c1476-123">Aggiunta di Lecorpio dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="c1476-123">Adding Lecorpio from hello gallery</span></span>
<span data-ttu-id="c1476-124">integrazione hello tooconfigure di Lecorpio in Azure AD, è necessario tooadd Lecorpio dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c1476-124">tooconfigure hello integration of Lecorpio into Azure AD, you need tooadd Lecorpio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c1476-125">**tooadd Lecorpio dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c1476-125">**tooadd Lecorpio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1476-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c1476-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1476-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c1476-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c1476-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c1476-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c1476-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="c1476-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c1476-133">Nella casella di ricerca hello, digitare **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="c1476-133">In hello search box, type **Lecorpio**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="c1476-135">Nel riquadro dei risultati hello, selezionare **Lecorpio**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c1476-135">In hello results panel, select **Lecorpio**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1476-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1476-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1476-138">In questa sezione si configura e si testa l'accesso Single Sign-On di Azure AD con Lecorpio con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1476-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c1476-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Lecorpio è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1476-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lecorpio is tooa user in Azure AD.</span></span> <span data-ttu-id="c1476-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Lecorpio deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="c1476-140">In other words, a link relationship between an Azure AD user and hello related user in Lecorpio needs toobe established.</span></span>

<span data-ttu-id="c1476-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="c1476-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lecorpio.</span></span>

<span data-ttu-id="c1476-142">tooconfigure e prova AD Azure single sign-on con Lecorpio, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="c1476-142">tooconfigure and test Azure AD single sign-on with Lecorpio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c1476-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c1476-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c1476-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1476-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1476-145">**[Creazione di un utente test Lecorpio](#creating-a-lecorpio-test-user)**  -toohave un equivalente di Britta Simon in Lecorpio che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c1476-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - toohave a counterpart of Britta Simon in Lecorpio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1476-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c1476-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1476-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="c1476-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1476-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1476-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1476-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="c1476-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="c1476-150">**Azure AD tooconfigure single sign-on con Lecorpio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c1476-150">**tooconfigure Azure AD single sign-on with Lecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1476-151">Nel portale di Azure su hello hello **Lecorpio** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c1476-151">In hello Azure portal, on hello **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c1476-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c1476-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="c1476-155">In hello **Lecorpio dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c1476-155">On hello **Lecorpio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="c1476-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1476-157">a.</span></span> <span data-ttu-id="c1476-158">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="c1476-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="c1476-159">b.</span><span class="sxs-lookup"><span data-stu-id="c1476-159">b.</span></span> <span data-ttu-id="c1476-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="c1476-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1476-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="c1476-161">These values are not hello real.</span></span> <span data-ttu-id="c1476-162">Aggiornare questi valori con URL hello effettivo Sign-on e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="c1476-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="c1476-163">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="c1476-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="c1476-164">Contatto [team di supporto Lecorpio Client](mailto:info@lecorpio.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="c1476-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c1476-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c1476-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="c1476-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c1476-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c1476-169">tooconfigure single sign-on sul **Lecorpio** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="c1476-169">tooconfigure single sign-on on **Lecorpio** side, you need toosend hello downloaded **Metadata XML** too[Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="c1476-170">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="c1476-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c1476-171">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c1476-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c1476-172">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1476-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1476-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1476-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1476-174">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c1476-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c1476-176">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c1476-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1476-177">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="c1476-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1476-179">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="c1476-179">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1476-181">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c1476-181">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1476-183">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c1476-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1476-185">a.</span><span class="sxs-lookup"><span data-stu-id="c1476-185">a.</span></span> <span data-ttu-id="c1476-186">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1476-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1476-187">b.</span><span class="sxs-lookup"><span data-stu-id="c1476-187">b.</span></span> <span data-ttu-id="c1476-188">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c1476-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1476-189">c.</span><span class="sxs-lookup"><span data-stu-id="c1476-189">c.</span></span> <span data-ttu-id="c1476-190">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="c1476-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c1476-191">d.</span><span class="sxs-lookup"><span data-stu-id="c1476-191">d.</span></span> <span data-ttu-id="c1476-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c1476-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="c1476-193">Creazione di un utente test di Lecorpio</span><span class="sxs-lookup"><span data-stu-id="c1476-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="c1476-194">In questa sezione si crea un utente di nome Britta Simon in Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="c1476-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="c1476-195">Contatto [team di supporto Lecorpio Client](mailto:info@lecorpio.com) tooadd utenti hello hello Lecorpio applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1476-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooadd hello users in hello Lecorpio application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c1476-196">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1476-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c1476-197">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLecorpio.</span><span class="sxs-lookup"><span data-stu-id="c1476-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLecorpio.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c1476-199">**tooassign Britta Simon tooLecorpio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c1476-199">**tooassign Britta Simon tooLecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1476-200">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c1476-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c1476-202">Nell'elenco di applicazioni hello, selezionare **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="c1476-202">In hello applications list, select **Lecorpio**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="c1476-204">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c1476-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c1476-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c1476-206">Click **Add** button.</span></span> <span data-ttu-id="c1476-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c1476-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c1476-209">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="c1476-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c1476-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c1476-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1476-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c1476-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1476-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c1476-212">Testing single sign-on</span></span>

<span data-ttu-id="c1476-213">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c1476-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c1476-214">Quando si fa clic su riquadro Lecorpio hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Lecorpio applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1476-214">When you click hello Lecorpio tile in hello Access Panel, you should get automatically signed-on tooyour Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1476-215">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c1476-215">Additional resources</span></span>

* [<span data-ttu-id="c1476-216">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1476-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1476-217">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1476-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png


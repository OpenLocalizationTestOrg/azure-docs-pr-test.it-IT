---
title: 'Esercitazione: Integrazione di Azure Active Directory con @Task| Documenti Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e @Task.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="559aa-103">Esercitazione: Integrazione di Azure Active Directory con @Task</span><span class="sxs-lookup"><span data-stu-id="559aa-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="559aa-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate @Task con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="559aa-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="559aa-105">L'integrazione @Task con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="559aa-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="559aa-106">È possibile controllare in Azure AD che ha accessotoo@Task</span><span class="sxs-lookup"><span data-stu-id="559aa-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="559aa-107">È possibile consentire agli utenti di ottenere tooautomatically connesso too@Task (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="559aa-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="559aa-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="559aa-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="559aa-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="559aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="559aa-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="559aa-110">Prerequisites</span></span>
<span data-ttu-id="559aa-111">integrazione di Azure AD tooconfigure con @Task, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="559aa-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="559aa-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="559aa-112">An Azure AD subscription</span></span>
* <span data-ttu-id="559aa-113">Sottoscrizione di @Task abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="559aa-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="559aa-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="559aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="559aa-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="559aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="559aa-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="559aa-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="559aa-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="559aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="559aa-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="559aa-118">Scenario Description</span></span>
<span data-ttu-id="559aa-119">obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="559aa-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="559aa-120">scenario di Hello descritto in questa esercitazione è composto da tre componenti principali:</span><span class="sxs-lookup"><span data-stu-id="559aa-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="559aa-121">Aggiunta di @Task dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="559aa-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="559aa-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="559aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="559aa-123">Aggiunta di @Task dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="559aa-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="559aa-124">integrazione di hello tooconfigure di @Task in Azure AD, è necessario tooadd @Task dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="559aa-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="559aa-125">**tooadd @Task dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="559aa-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="559aa-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="559aa-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="559aa-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="559aa-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="559aa-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="559aa-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applicazioni][2] 
4. <span data-ttu-id="559aa-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="559aa-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3] 
5. <span data-ttu-id="559aa-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="559aa-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applicazioni][4] 
6. <span data-ttu-id="559aa-135">Nella casella di ricerca hello, digitare  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="559aa-135">In hello search box, type **@Task**.</span></span>
   
    ![Applicazioni][5] 
7. <span data-ttu-id="559aa-137">Nel riquadro risultati hello selezionare  **@Task** , quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="559aa-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Applicazioni][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="559aa-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="559aa-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="559aa-140">obiettivo di questa sezione Hello è tooshow è come tooconfigure e Azure AD di test singolo sign-on con @Task in base a un utente di test denominato "Laura Giussani".</span><span class="sxs-lookup"><span data-stu-id="559aa-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="559aa-141">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in @Task tooan utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="559aa-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="559aa-142">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in @Task deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="559aa-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="559aa-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in @Task.</span><span class="sxs-lookup"><span data-stu-id="559aa-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="559aa-144">tooconfigure e test di Azure AD accesso single sign-on con @Task, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="559aa-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="559aa-145">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="559aa-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="559aa-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="559aa-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="559aa-147">**[Creazione di un @Tasktest utente](#creating-a-halogen-software-test-user)**  -toohave un equivalente di Britta Simon in @Taskthat è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="559aa-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="559aa-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="559aa-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="559aa-149">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="559aa-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="559aa-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="559aa-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="559aa-151">obiettivo di Hello di questa sezione è tooenable AD Azure single sign-on nel portale di Azure classico hello e tooconfigure accesso single sign-on nel @Task dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="559aa-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="559aa-152">**tooconfigure AD Azure single sign-on con @Task, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="559aa-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="559aa-153">Nel portale di Azure classico, in hello hello  **@Task**  pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="559aa-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 
2. <span data-ttu-id="559aa-155">In hello **come farebbe come utenti toosign per too@Task**  selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][7] 
3. <span data-ttu-id="559aa-157">In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="559aa-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configurare le impostazioni dell'app][8] 
   
     <span data-ttu-id="559aa-159">a.</span><span class="sxs-lookup"><span data-stu-id="559aa-159">a.</span></span> <span data-ttu-id="559aa-160">In hello **URL di accesso** casella di testo, digitare l'URL hello usato dall'utenti toosign-on tooyour @Task applicazione (ad esempio:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="559aa-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="559aa-161">b.</span><span class="sxs-lookup"><span data-stu-id="559aa-161">b.</span></span> <span data-ttu-id="559aa-162">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-162">Click **Next**.</span></span>
4. <span data-ttu-id="559aa-163">In hello **configurare single sign-on in @Task**  pagina, fare clic su **Scarica metadati**, salvare il file di metadati hello in locale nel computer e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Cos'è Azure AD Connect][9] 
5. <span data-ttu-id="559aa-165">Sign-on tooyour @Task sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="559aa-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="559aa-166">Andare troppo**Single Sign On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="559aa-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="559aa-167">In hello **Single Sign-On** finestra di dialogo, eseguire i passaggi hello</span><span class="sxs-lookup"><span data-stu-id="559aa-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Configura accesso Single Sign-On][23]
   
    <span data-ttu-id="559aa-169">a.</span><span class="sxs-lookup"><span data-stu-id="559aa-169">a.</span></span> <span data-ttu-id="559aa-170">Per **Type** selezionare**SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="559aa-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="559aa-171">b.</span><span class="sxs-lookup"><span data-stu-id="559aa-171">b.</span></span> <span data-ttu-id="559aa-172">Selezionare **Service Provider ID**.</span><span class="sxs-lookup"><span data-stu-id="559aa-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="559aa-173">c.</span><span class="sxs-lookup"><span data-stu-id="559aa-173">c.</span></span> <span data-ttu-id="559aa-174">Nel portale di Azure classico hello, copiare hello **URL accesso remoto**e quindi incollarlo hello **URL del portale account di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="559aa-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="559aa-175">d.</span><span class="sxs-lookup"><span data-stu-id="559aa-175">d.</span></span> <span data-ttu-id="559aa-176">Nel portale di Azure classico hello, copiare hello **URL del servizio Single Sign-Out**e quindi incollarlo hello **Sign-Out URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="559aa-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="559aa-177">e.</span><span class="sxs-lookup"><span data-stu-id="559aa-177">e.</span></span> <span data-ttu-id="559aa-178">Nel portale di Azure classico hello, copiare hello **Modifica URL Password**e quindi incollarlo hello **Modifica URL Password** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="559aa-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="559aa-179">f.</span><span class="sxs-lookup"><span data-stu-id="559aa-179">f.</span></span> <span data-ttu-id="559aa-180">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="559aa-180">Click **Save**.</span></span>
8. <span data-ttu-id="559aa-181">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Cos'è Azure AD Connect][10]
9. <span data-ttu-id="559aa-183">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="559aa-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Cos'è Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="559aa-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="559aa-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="559aa-186">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="559aa-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Creare un utente di Azure AD][20]

<span data-ttu-id="559aa-188">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="559aa-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="559aa-189">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="559aa-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="559aa-191">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="559aa-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="559aa-192">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="559aa-194">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="559aa-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="559aa-196">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="559aa-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="559aa-198">a.</span><span class="sxs-lookup"><span data-stu-id="559aa-198">a.</span></span> <span data-ttu-id="559aa-199">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="559aa-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="559aa-200">b.</span><span class="sxs-lookup"><span data-stu-id="559aa-200">b.</span></span> <span data-ttu-id="559aa-201">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="559aa-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="559aa-202">c.</span><span class="sxs-lookup"><span data-stu-id="559aa-202">c.</span></span> <span data-ttu-id="559aa-203">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-203">Click **Next**.</span></span>
6. <span data-ttu-id="559aa-204">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="559aa-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="559aa-206">a.</span><span class="sxs-lookup"><span data-stu-id="559aa-206">a.</span></span> <span data-ttu-id="559aa-207">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="559aa-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="559aa-208">b.</span><span class="sxs-lookup"><span data-stu-id="559aa-208">b.</span></span> <span data-ttu-id="559aa-209">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="559aa-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="559aa-210">c.</span><span class="sxs-lookup"><span data-stu-id="559aa-210">c.</span></span> <span data-ttu-id="559aa-211">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="559aa-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="559aa-212">d.</span><span class="sxs-lookup"><span data-stu-id="559aa-212">d.</span></span> <span data-ttu-id="559aa-213">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="559aa-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="559aa-214">e.</span><span class="sxs-lookup"><span data-stu-id="559aa-214">e.</span></span> <span data-ttu-id="559aa-215">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-215">Click **Next**.</span></span>

7. <span data-ttu-id="559aa-216">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="559aa-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="559aa-218">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="559aa-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="559aa-220">a.</span><span class="sxs-lookup"><span data-stu-id="559aa-220">a.</span></span> <span data-ttu-id="559aa-221">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="559aa-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="559aa-222">b.</span><span class="sxs-lookup"><span data-stu-id="559aa-222">b.</span></span> <span data-ttu-id="559aa-223">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="559aa-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="559aa-224">Creazione di un utente di test di @Task</span><span class="sxs-lookup"><span data-stu-id="559aa-224">Creating an @Task test user</span></span>
<span data-ttu-id="559aa-225">obiettivo Hello di questa sezione è un utente denominato Britta Simon in toocreate @Task.</span><span class="sxs-lookup"><span data-stu-id="559aa-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="559aa-226">**un utente denominato Britta Simon in toocreate @Task, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="559aa-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="559aa-227">Accesso tooyour @Task sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="559aa-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="559aa-228">Scegliere dal menu hello in primo piano hello **persone**.</span><span class="sxs-lookup"><span data-stu-id="559aa-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="559aa-229">Fare clic su **New Person**.</span><span class="sxs-lookup"><span data-stu-id="559aa-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="559aa-230">Nella finestra di dialogo nuova persona hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="559aa-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Creare un utente di test di @Task][21] 
   
    <span data-ttu-id="559aa-232">a.</span><span class="sxs-lookup"><span data-stu-id="559aa-232">a.</span></span> <span data-ttu-id="559aa-233">In hello **nome** casella di testo, digitare "Sandro".</span><span class="sxs-lookup"><span data-stu-id="559aa-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="559aa-234">b.</span><span class="sxs-lookup"><span data-stu-id="559aa-234">b.</span></span> <span data-ttu-id="559aa-235">In hello **cognome** casella di testo, digitare "Simon".</span><span class="sxs-lookup"><span data-stu-id="559aa-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="559aa-236">c.</span><span class="sxs-lookup"><span data-stu-id="559aa-236">c.</span></span> <span data-ttu-id="559aa-237">In hello **indirizzo di posta elettronica** casella di testo, digitare l'indirizzo di posta elettronica Britta Simon in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="559aa-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="559aa-238">d.</span><span class="sxs-lookup"><span data-stu-id="559aa-238">d.</span></span> <span data-ttu-id="559aa-239">Fare clic su **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="559aa-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="559aa-240">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="559aa-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="559aa-241">obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure tramite la concessione di accesso too@Task.</span><span class="sxs-lookup"><span data-stu-id="559aa-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Assegna utente][200] 

<span data-ttu-id="559aa-243">**tooassign Britta Simon too@Task, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="559aa-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="559aa-244">In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="559aa-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Assegna utente][201] 
2. <span data-ttu-id="559aa-246">Nell'elenco di applicazioni hello, selezionare  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="559aa-246">In hello applications list, select **@Task**.</span></span>
   
    ![Assegna utente][202] 
3. <span data-ttu-id="559aa-248">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="559aa-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Assegna utente][203] 
4. <span data-ttu-id="559aa-250">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="559aa-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="559aa-251">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="559aa-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="559aa-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="559aa-253">Testing Single Sign-On</span></span>
<span data-ttu-id="559aa-254">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="559aa-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="559aa-255">Quando si fa clic su hello @Task hello di riquadro nel Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour @Task dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="559aa-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="559aa-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="559aa-256">Additional Resources</span></span>
* [<span data-ttu-id="559aa-257">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="559aa-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="559aa-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="559aa-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png







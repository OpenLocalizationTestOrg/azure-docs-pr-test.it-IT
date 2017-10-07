---
title: 'Esercitazione: Integrazione di Azure Active Directory con SciQuest Spend Director | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SciQuest direttore di spesa.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="8b020-103">Esercitazione: Integrazione di Azure Active Directory con SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="8b020-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="8b020-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate SciQuest spesa Director con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b020-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="8b020-105">Integrazione SciQuest spesa Director con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8b020-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="8b020-106">È possibile controllare in Azure AD che ha accesso tooSciQuest spesa Director</span><span class="sxs-lookup"><span data-stu-id="8b020-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="8b020-107">È possibile abilitare l'utenti tooautomatically get connesso tooSciQuest Director spesa (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b020-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8b020-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="8b020-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="8b020-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b020-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b020-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b020-110">Prerequisites</span></span>
<span data-ttu-id="8b020-111">integrazione di Azure AD con Director spesa SciQuest tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8b020-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="8b020-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b020-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8b020-113">Sottoscrizione di SciQuest Spend Director abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b020-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b020-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8b020-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8b020-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8b020-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8b020-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8b020-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8b020-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b020-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="8b020-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8b020-118">Scenario Description</span></span>
<span data-ttu-id="8b020-119">obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8b020-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="8b020-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8b020-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b020-121">Aggiunta di Director spesa SciQuest dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8b020-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="8b020-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b020-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="8b020-123">Aggiunta di Director spesa SciQuest dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8b020-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="8b020-124">integrazione hello tooconfigure di SciQuest spesa Director in Azure AD, è necessario tooadd SciQuest spesa Director dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8b020-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b020-125">**tooadd SciQuest spesa Director dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b020-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b020-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b020-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="8b020-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="8b020-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="8b020-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="8b020-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applicazioni][2]

4. <span data-ttu-id="8b020-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="8b020-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3]

5. <span data-ttu-id="8b020-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="8b020-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applicazioni][4]

6. <span data-ttu-id="8b020-135">Nella casella di ricerca hello, digitare **sciQuest spesa director**.</span><span class="sxs-lookup"><span data-stu-id="8b020-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Applicazioni][5]

7. <span data-ttu-id="8b020-137">Nel riquadro dei risultati di hello, selezionare **SciQuest spesa Director**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b020-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Applicazioni][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b020-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b020-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b020-140">obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con SciQuest spesa Director basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8b020-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b020-141">Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello Director spesa SciQuest tooan utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b020-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="8b020-142">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in SciQuest spesa Director deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8b020-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="8b020-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in SciQuest direttore di spesa.</span><span class="sxs-lookup"><span data-stu-id="8b020-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="8b020-144">tooconfigure e prova AD Azure single sign-on con SciQuest spesa Director, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8b020-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b020-145">**[Configurazione di Azure Active Directory singola Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8b020-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b020-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b020-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b020-147">**[Creazione di un utente test Director spesa SciQuest](#creating-a-halogen-software-test-user)**  -toohave un equivalente di Britta Simon in SciQuest spesa Director toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="8b020-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8b020-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8b020-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b020-149">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8b020-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="8b020-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b020-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="8b020-151">obiettivo di Hello di questa sezione è tooenable Azure AD single sign-on nel portale di Azure classico hello e tooconfigure single sign-on nell'applicazione SciQuest spesa Director.</span><span class="sxs-lookup"><span data-stu-id="8b020-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="8b020-152">**tooconfigure AD Azure single sign-on con SciQuest spesa Director, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b020-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b020-153">Nel portale di Azure classico, in hello hello **SciQuest spesa Director** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8b020-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][8]

2. <span data-ttu-id="8b020-155">In hello **come si sarebbe ad esempio utenti toosign su tooSciQuest spesa Director** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8b020-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][9]

3. <span data-ttu-id="8b020-157">In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b020-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Configurare le impostazioni dell'app][10]
   
     <span data-ttu-id="8b020-159">a.</span><span class="sxs-lookup"><span data-stu-id="8b020-159">a.</span></span> <span data-ttu-id="8b020-160">In hello **URL di accesso** , digitare l'URL usato dal toosign gli utenti nell'applicazione SciQuest spesa Director tooyour utilizzando hello seguente modello: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="8b020-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="8b020-161">b.</span><span class="sxs-lookup"><span data-stu-id="8b020-161">b.</span></span> <span data-ttu-id="8b020-162">In hello **URL di risposta** casella di testo, hello tipo stesso valore è stato digitato in hello **URL di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8b020-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="8b020-163">c.</span><span class="sxs-lookup"><span data-stu-id="8b020-163">c.</span></span> <span data-ttu-id="8b020-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8b020-164">Click **Next**.</span></span>

4. <span data-ttu-id="8b020-165">In hello **configurare single sign-on in Director spesa SciQuest** pagina, fare clic su **Scarica metadati**e quindi salvare il file di metadati hello in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="8b020-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Cos'è Azure AD Connect][11]

5. <span data-ttu-id="8b020-167">Contattare SciQuest supporto tooenable questo metodo di autenticazione utilizzando i metadati scaricato hello precedente.</span><span class="sxs-lookup"><span data-stu-id="8b020-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="8b020-168">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8b020-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Cos'è Azure AD Connect][15]

7. <span data-ttu-id="8b020-170">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="8b020-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b020-171">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b020-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b020-172">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8b020-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="8b020-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b020-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b020-174">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b020-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Cos'è Azure AD Connect][100] 

2. <span data-ttu-id="8b020-176">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="8b020-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="8b020-177">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="8b020-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Cos'è Azure AD Connect][101] 

4. <span data-ttu-id="8b020-179">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="8b020-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Cos'è Azure AD Connect][102] 

5. <span data-ttu-id="8b020-181">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b020-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Cos'è Azure AD Connect][103] 
   
    <span data-ttu-id="8b020-183">a.</span><span class="sxs-lookup"><span data-stu-id="8b020-183">a.</span></span> <span data-ttu-id="8b020-184">In **Tipo di utente** selezionare **Nuovo utente nell'organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="8b020-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="8b020-185">b.</span><span class="sxs-lookup"><span data-stu-id="8b020-185">b.</span></span> <span data-ttu-id="8b020-186">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b020-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8b020-187">c.</span><span class="sxs-lookup"><span data-stu-id="8b020-187">c.</span></span> <span data-ttu-id="8b020-188">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8b020-188">Click **Next**.</span></span>

6. <span data-ttu-id="8b020-189">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b020-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Cos'è Azure AD Connect][104] 
   
    <span data-ttu-id="8b020-191">a.</span><span class="sxs-lookup"><span data-stu-id="8b020-191">a.</span></span> <span data-ttu-id="8b020-192">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="8b020-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="8b020-193">b.</span><span class="sxs-lookup"><span data-stu-id="8b020-193">b.</span></span> <span data-ttu-id="8b020-194">In hello **cognome** txtbox, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8b020-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="8b020-195">c.</span><span class="sxs-lookup"><span data-stu-id="8b020-195">c.</span></span> <span data-ttu-id="8b020-196">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8b020-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="8b020-197">d.</span><span class="sxs-lookup"><span data-stu-id="8b020-197">d.</span></span> <span data-ttu-id="8b020-198">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="8b020-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="8b020-199">e.</span><span class="sxs-lookup"><span data-stu-id="8b020-199">e.</span></span> <span data-ttu-id="8b020-200">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8b020-200">Click **Next**.</span></span>

7. <span data-ttu-id="8b020-201">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="8b020-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Cos'è Azure AD Connect][105]  

8. <span data-ttu-id="8b020-203">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b020-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Cos'è Azure AD Connect][106]   
   
    <span data-ttu-id="8b020-205">a.</span><span class="sxs-lookup"><span data-stu-id="8b020-205">a.</span></span> <span data-ttu-id="8b020-206">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="8b020-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="8b020-207">b.</span><span class="sxs-lookup"><span data-stu-id="8b020-207">b.</span></span> <span data-ttu-id="8b020-208">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8b020-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="8b020-209">Creazione di un utente test di SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="8b020-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="8b020-210">obiettivo Hello di questa sezione è un utente denominato Britta Simon in Director spesa SciQuest toocreate.</span><span class="sxs-lookup"><span data-stu-id="8b020-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="8b020-211">È necessario toocontact il team di supporto SciQuest direttore di spesa e di fornire dettagli hello su tooget di account del test che è creato.</span><span class="sxs-lookup"><span data-stu-id="8b020-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="8b020-212">In alternativa, è anche possibile sfruttare il provisioning JIT, una funzionalità Single Sign-On supportata da SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="8b020-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="8b020-213">Se il provisioning JIT è abilitato, gli utenti vengono creati automaticamente da SciQuest Spend Director durante un tentativo di accesso Single Sign-ON, se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="8b020-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="8b020-214">Questa funzionalità Elimina la necessità di hello toomanually creare single sign-on controparte utenti.</span><span class="sxs-lookup"><span data-stu-id="8b020-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="8b020-215">provisioning just-in-time tooget abilitato, è necessario toocontact sei il team di supporto SciQuest direttore di spesa.</span><span class="sxs-lookup"><span data-stu-id="8b020-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8b020-216">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b020-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="8b020-217">obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo proprio tooSciQuest accesso direttore di spesa.</span><span class="sxs-lookup"><span data-stu-id="8b020-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Cos'è Azure AD Connect][200]

<span data-ttu-id="8b020-219">**tooassign Britta Simon tooSciQuest direttore di spesa, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b020-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b020-220">In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="8b020-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Cos'è Azure AD Connect][201]

2. <span data-ttu-id="8b020-222">Nell'elenco di applicazioni hello, selezionare **SciQuest spesa Director**.</span><span class="sxs-lookup"><span data-stu-id="8b020-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Cos'è Azure AD Connect][202]

3. <span data-ttu-id="8b020-224">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="8b020-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Cos'è Azure AD Connect][203]

4. <span data-ttu-id="8b020-226">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8b020-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Cos'è Azure AD Connect][204]

5. <span data-ttu-id="8b020-228">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="8b020-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Cos'è Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8b020-230">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b020-230">Testing Single Sign-On</span></span>
<span data-ttu-id="8b020-231">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8b020-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="8b020-232">Quando si fa clic su riquadro SciQuest spesa Director hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour SciQuest spesa Director applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b020-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b020-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8b020-233">Additional Resources</span></span>
* [<span data-ttu-id="8b020-234">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b020-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b020-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b020-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bynder | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Bynder.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="f7b2c-103">Esercitazione: Integrazione di Azure Active Directory con Bynder</span><span class="sxs-lookup"><span data-stu-id="f7b2c-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="f7b2c-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Bynder con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7b2c-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7b2c-105">Integrazione Bynder con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="f7b2c-106">È possibile controllare in Azure AD che ha accesso tooBynder</span><span class="sxs-lookup"><span data-stu-id="f7b2c-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="f7b2c-107">È possibile abilitare l'utenti tooautomatically get connesso tooBynder single sign-on (SSO) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7b2c-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="f7b2c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="f7b2c-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="f7b2c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7b2c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7b2c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f7b2c-110">Prerequisites</span></span>
<span data-ttu-id="f7b2c-111">integrazione di Azure AD con Bynder tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="f7b2c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="f7b2c-113">Sottoscrizione di Bynder abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="f7b2c-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="f7b2c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="f7b2c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f7b2c-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f7b2c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7b2c-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7b2c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f7b2c-118">Scenario description</span></span>
<span data-ttu-id="f7b2c-119">obiettivo di Hello di questa esercitazione è tooenable si tootest SSO di Microsoft Azure Active Directory in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="f7b2c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7b2c-121">Aggiunta di Bynder dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f7b2c-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="f7b2c-122">Configurazione e test dell'accesso Single Sign-On di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7b2c-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="f7b2c-123">Aggiungere Bynder dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="f7b2c-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="f7b2c-124">integrazione hello tooconfigure di Bynder in Azure AD, è necessario tooadd Bynder dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f7b2c-125">**tooadd Bynder dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f7b2c-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7b2c-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="f7b2c-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f7b2c-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applicazioni][2]
4. <span data-ttu-id="f7b2c-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="f7b2c-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applicazioni][4]
6. <span data-ttu-id="f7b2c-135">Nella casella di ricerca hello, digitare **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-135">In hello search box, type **Bynder**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="f7b2c-137">Nel riquadro dei risultati hello, selezionare **Bynder**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Selezionare l'applicazione hello nella raccolta hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="f7b2c-139">Configurare e testare l'accesso Single Sign-On di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7b2c-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="f7b2c-140">obiettivo di Hello di questa sezione è tooshow come tooconfigure e test di Microsoft Azure AD SSO con Bynder basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f7b2c-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7b2c-141">Per toowork SSO, Azure AD deve tooknow è quale utente controparte hello Bynder tooan utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="f7b2c-142">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Bynder deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="f7b2c-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Bynder.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="f7b2c-144">tooconfigure e test di Microsoft Azure AD SSO con Bynder, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f7b2c-145">**[Configurazione di Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f7b2c-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="f7b2c-147">**[Creazione di un utente test Bynder](#creating-a-bynder-test-user)**  -toohave un equivalente di Britta Simon in Bynder toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f7b2c-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="f7b2c-149">**[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="f7b2c-150">Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7b2c-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="f7b2c-151">In questa sezione abilitare SSO di Microsoft Azure Active Directory nel portale classico hello e configurare SSO nell'applicazione Bynder.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="f7b2c-152">**tooconfigure SSO di Microsoft Azure AD con Bynder, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f7b2c-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7b2c-153">Nel portale classico hello in hello **Bynder** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 
2. <span data-ttu-id="f7b2c-155">In hello **come si sarebbe ad esempio utenti toosign su tooBynder** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="f7b2c-157">In hello **Configura impostazioni App** nella pagina, se si desidera un'applicazione hello tooconfigure in **modalità avviata da IDP**, eseguire hello alla procedura seguente e fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="f7b2c-159">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="f7b2c-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="f7b2c-160">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-160">Click **Next**.</span></span>
4. <span data-ttu-id="f7b2c-161">Se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP** su hello **Configura impostazioni App** nella pagina, quindi fare clic su hello **"(facoltative) Impostazioni avanzate Show"**e quindi immettere hello **URL di accesso** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="f7b2c-163">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="f7b2c-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="f7b2c-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="f7b2c-165">valore Hello hello URL di accesso in questa esercitazione è semplicemente un placeholfer.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="f7b2c-166">valore effettivo di hello tooget per l'ambiente, contattare Bynder.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="f7b2c-167">In hello **configurare single sign-on a Bynder** pagina, eseguire hello alla procedura seguente e fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="f7b2c-169">Fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="f7b2c-170">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-170">Click **Next**.</span></span>
6. <span data-ttu-id="f7b2c-171">tooget SSO configurato per l'applicazione, contattare il team di supporto Bynder.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="f7b2c-172">Collegare il file di metadati scaricato hello e condividerlo con Bynder team tooset di SSO sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="f7b2c-173">Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][10]
8. <span data-ttu-id="f7b2c-175">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f7b2c-177">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7b2c-177">Create an Azure AD test user</span></span>
<span data-ttu-id="f7b2c-178">obiettivo di Hello di questa sezione è toocreate un utente di test nel portale classico di hello chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="f7b2c-180">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f7b2c-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7b2c-181">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="f7b2c-183">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f7b2c-184">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="f7b2c-186">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="f7b2c-188">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="f7b2c-190">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="f7b2c-191">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="f7b2c-192">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-192">Click **Next**.</span></span>
6. <span data-ttu-id="f7b2c-193">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="f7b2c-195">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="f7b2c-196">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="f7b2c-197">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="f7b2c-198">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="f7b2c-199">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-199">Click **Next**.</span></span>
7. <span data-ttu-id="f7b2c-200">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="f7b2c-202">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f7b2c-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="f7b2c-204">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="f7b2c-205">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="f7b2c-206">Creare un utente test per Bynder</span><span class="sxs-lookup"><span data-stu-id="f7b2c-206">Create a Bynder test user</span></span>
<span data-ttu-id="f7b2c-207">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Bynder toocreate.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="f7b2c-208">Bynder supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f7b2c-209">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-209">There is no action item for you in this section.</span></span> <span data-ttu-id="f7b2c-210">Verrà creato un nuovo utente durante una tooaccess tentativo Bynder se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f7b2c-211">Se è necessario un utente toocreate manualmente, è necessario team di supporto Bynder toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f7b2c-212">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7b2c-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="f7b2c-213">obiettivo di Hello di questa sezione è tooenabling Britta Simon toouse SSO Azure concedendo tooBynder proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Assegna utente][200]

<span data-ttu-id="f7b2c-215">**tooassign Britta Simon tooBynder, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f7b2c-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7b2c-216">Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Assegna utente][201]
2. <span data-ttu-id="f7b2c-218">Nell'elenco di applicazioni hello, selezionare **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="f7b2c-220">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Assegna utente][203]
4. <span data-ttu-id="f7b2c-222">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="f7b2c-223">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="f7b2c-225">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f7b2c-225">Test single sign-on</span></span>
<span data-ttu-id="f7b2c-226">obiettivo di Hello di questa sezione è tootest la configurazione di SSO di Microsoft Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f7b2c-227">Quando si fa clic su riquadro Bynder hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Bynder applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7b2c-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7b2c-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f7b2c-228">Additional resources</span></span>
* [<span data-ttu-id="f7b2c-229">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7b2c-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7b2c-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7b2c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png

---
title: 'Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Splunk Enterprise e Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="47ac1-103">Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="47ac1-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="47ac1-104">In questa esercitazione, è illustrato come toointegrate Splunk Enterprise e Splunk Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47ac1-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47ac1-105">Integrazione di Splunk Enterprise e Splunk Cloud con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="47ac1-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47ac1-106">È possibile controllare in Azure AD che ha accesso Enterprise tooSplunk e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="47ac1-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="47ac1-107">È possibile abilitare l'utenti tooautomatically get connesso tooSplunk Splunk Cloud e Enterprise single sign-on (SSO) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="47ac1-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="47ac1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="47ac1-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="47ac1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47ac1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47ac1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="47ac1-110">Prerequisites</span></span>

<span data-ttu-id="47ac1-111">integrazione di Azure AD con Splunk Enterprise e Splunk Cloud tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="47ac1-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="47ac1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47ac1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47ac1-113">Sottoscrizione di Splunk Enterprise o Splunk Cloud abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="47ac1-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="47ac1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="47ac1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="47ac1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="47ac1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47ac1-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="47ac1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="47ac1-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47ac1-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="47ac1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="47ac1-118">Scenario description</span></span>
<span data-ttu-id="47ac1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="47ac1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="47ac1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="47ac1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47ac1-121">Aggiunta di Splunk Enterprise e Splunk Cloud dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="47ac1-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="47ac1-122">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="47ac1-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="47ac1-123">Aggiungere Splunk Enterprise e Splunk Cloud dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="47ac1-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="47ac1-124">integrazione hello tooconfigure di Splunk Enterprise e Splunk Cloud in Azure AD, è necessario tooadd Splunk Enterprise Splunk Cloud dall'elenco di tooyour hello raccolta di App e gestite SaaS.</span><span class="sxs-lookup"><span data-stu-id="47ac1-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47ac1-125">**tooadd Splunk Enterprise e Splunk Cloud dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47ac1-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47ac1-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="47ac1-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="47ac1-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="47ac1-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="47ac1-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Applicazioni][2]

4. <span data-ttu-id="47ac1-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="47ac1-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Applicazioni][3]

5. <span data-ttu-id="47ac1-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Applicazioni][4]

6. <span data-ttu-id="47ac1-135">Nella casella di ricerca hello, digitare **Splunk Enterprise o Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="47ac1-137">Nel riquadro dei risultati di hello, selezionare **Splunk Enterprise e Splunk Cloud**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="47ac1-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="47ac1-139">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47ac1-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="47ac1-140">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Splunk Enterprise e Splunk Cloud con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47ac1-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="47ac1-141">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Splunk Enterprise e Splunk Cloud è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47ac1-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="47ac1-142">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Splunk Enterprise e Splunk Cloud deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="47ac1-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="47ac1-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="47ac1-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="47ac1-144">tooconfigure e prova AD Azure single sign-on con Splunk Enterprise e Splunk Cloud, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="47ac1-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47ac1-145">**[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="47ac1-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47ac1-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47ac1-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47ac1-147">**[Creazione di un utente test Splunk Enterprise e Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave un equivalente di Britta Simon Splunk azienda e Splunk Cloud toohello collegato AD Azure rappresentazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="47ac1-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="47ac1-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47ac1-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47ac1-149">**[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="47ac1-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="47ac1-150">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47ac1-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="47ac1-151">In questa sezione abilitare SSO AD Azure nel portale classico hello e configurare SSO nell'applicazione Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="47ac1-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="47ac1-152">**tooconfigure AD Azure single sign-on con Splunk Enterprise e Splunk Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47ac1-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="47ac1-153">Nel portale classico hello in hello **Splunk Enterprise e Splunk Cloud** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="47ac1-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configura accesso Single Sign-On][6] 

2. <span data-ttu-id="47ac1-155">In hello **come si desidera che gli utenti toosign su tooSplunk Enterprise e Splunk Cloud** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="47ac1-157">In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47ac1-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="47ac1-159">In hello **URL di accesso** casella di testo, digitare l'URL hello usato dall'applicazione Splunk Cloud hello modello di utilizzo e gli utenti toosign-on tooyour Splunk Enterprise:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="47ac1-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="47ac1-160">In hello **identificatore** casella di testo, digitare l'URL del Splunk Server hello.</span><span class="sxs-lookup"><span data-stu-id="47ac1-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="47ac1-161">In hello **URL di risposta** casella di testo, digitare l'URL hello con hello seguente motivo:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="47ac1-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="47ac1-162">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="47ac1-163">In hello **configurare single sign-on in Splunk Enterprise e Splunk Cloud** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47ac1-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="47ac1-165">Fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="47ac1-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="47ac1-166">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-166">Click **Next**.</span></span>

5. <span data-ttu-id="47ac1-167">tooget SSO configurato per l'applicazione, contattare Splunk Enterprise e il team di supporto Splunk Cloud e fornire loro seguente hello:</span><span class="sxs-lookup"><span data-stu-id="47ac1-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="47ac1-168">Hello scaricato **federaton metadati**</span><span class="sxs-lookup"><span data-stu-id="47ac1-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="47ac1-169">Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Single Sign-On di Microsoft Azure AD][10]

7. <span data-ttu-id="47ac1-171">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="47ac1-173">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="47ac1-173">Create an Azure AD test user</span></span>
<span data-ttu-id="47ac1-174">In questa sezione creare un utente test nel portale classico di hello chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47ac1-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="47ac1-176">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47ac1-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47ac1-177">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="47ac1-179">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="47ac1-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="47ac1-180">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47ac1-182">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="47ac1-184">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47ac1-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="47ac1-186">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="47ac1-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="47ac1-187">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="47ac1-188">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-188">Click **Next**.</span></span>

6.  <span data-ttu-id="47ac1-189">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47ac1-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="47ac1-191">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="47ac1-192">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="47ac1-193">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="47ac1-194">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="47ac1-195">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-195">Click **Next**.</span></span>

7. <span data-ttu-id="47ac1-196">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="47ac1-198">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="47ac1-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="47ac1-200">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="47ac1-201">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="47ac1-202">Creare un utente test di Splunk Enterprise e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="47ac1-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="47ac1-203">In questa sezione viene creato un utente chiamato Britta Simon in Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="47ac1-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="47ac1-204">Rivolgersi Splunk Enterprise e Splunk Cloud supporto team tooadd hello utenti hello Splunk Enterprise e Splunk Cloud platform.</span><span class="sxs-lookup"><span data-stu-id="47ac1-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="47ac1-205">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="47ac1-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="47ac1-206">In questa sezione è abilitare Britta Simon toouse SSOy Azure conceda proprio accesso tooSplunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="47ac1-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="47ac1-208">**tooassign Britta Simon tooSplunk Enterprise e Splunk Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="47ac1-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="47ac1-209">Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="47ac1-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="47ac1-211">Nell'elenco di applicazioni hello, selezionare **Splunk Enterprise e Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="47ac1-213">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-213">In hello menu on hello top, click **Users**.</span></span>

    ![Assegna utente][203]

4. <span data-ttu-id="47ac1-215">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="47ac1-216">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="47ac1-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="47ac1-218">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="47ac1-218">Test single sign-on</span></span>

<span data-ttu-id="47ac1-219">In questa sezione è verificare il AD SSOonfiguration Azure tramite hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="47ac1-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="47ac1-220">Quando si fa clic hello Splunk Enterprise e riquadro Splunk Cloud in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="47ac1-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="47ac1-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="47ac1-221">Additional resources</span></span>

* [<span data-ttu-id="47ac1-222">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47ac1-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47ac1-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47ac1-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png

---
title: 'Esercitazione: Integrazione di Azure Active Directory con Wizergos Productivity Software | Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e produttività Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="cfd95-103">Esercitazione: Integrazione di Azure Active Directory con Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="cfd95-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="cfd95-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Wizergos produttività con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfd95-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfd95-105">Integrazione di Software per la produttività Wizergos con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cfd95-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="cfd95-106">È possibile controllare in Azure AD che ha accesso tooWizergos Software per la produttività</span><span class="sxs-lookup"><span data-stu-id="cfd95-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="cfd95-107">È possibile abilitare l'utenti tooautomatically get connesso tooWizergos produttività single sign-on (SSO) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd95-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="cfd95-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="cfd95-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="cfd95-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfd95-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfd95-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cfd95-110">Prerequisites</span></span>
<span data-ttu-id="cfd95-111">integrazione di Azure AD con Software per la produttività Wizergos tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cfd95-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="cfd95-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfd95-112">An Azure AD subscription</span></span>
* <span data-ttu-id="cfd95-113">Sottoscrizione di Wizergos Productivity Software abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="cfd95-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="cfd95-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cfd95-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="cfd95-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cfd95-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="cfd95-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cfd95-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="cfd95-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfd95-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfd95-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cfd95-118">Scenario description</span></span>
<span data-ttu-id="cfd95-119">obiettivo di Hello di questa esercitazione è tooenable si tootest SSO AD Azure in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cfd95-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="cfd95-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cfd95-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfd95-121">Aggiunta di Software per la produttività Wizergos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cfd95-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="cfd95-122">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd95-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="cfd95-123">Aggiunta di Software per la produttività Wizergos dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cfd95-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="cfd95-124">integrazione hello tooconfigure di produttività Wizergos in Azure AD, è necessario tooadd Wizergos produttività Software dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cfd95-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfd95-125">**tooadd Wizergos produttività Software dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfd95-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfd95-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="cfd95-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="cfd95-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="cfd95-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="cfd95-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applicazioni][2]
4. <span data-ttu-id="cfd95-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="cfd95-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="cfd95-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applicazioni][4]
6. <span data-ttu-id="cfd95-135">Nella casella di ricerca hello, digitare **Wizergos produttività**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="cfd95-137">Nel riquadro dei risultati hello, selezionare **produttività Wizergos**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cfd95-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Selezionare l'applicazione hello nella raccolta hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="cfd95-139">Configurare e testare l'accesso Single Sign-On (SSO) di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd95-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="cfd95-140">obiettivo di Hello di questa sezione è tooshow come tooconfigure e test di accesso SSO AD Azure con Wizergos produttività Software basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cfd95-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfd95-141">Per toowork SSO, Azure AD deve tooknow è quale utente controparte hello utente tooan Wizergos produttività in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfd95-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="cfd95-142">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello nel Software di produttività Wizergos deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cfd95-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="cfd95-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** Wizergos produttività software.</span><span class="sxs-lookup"><span data-stu-id="cfd95-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="cfd95-144">tooconfigure e prova AD Azure single sign-on con BynWizergos produttività Softwareder, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cfd95-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfd95-145">**[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cfd95-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfd95-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfd95-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfd95-147">**[Creazione di un utente di test del Software per la produttività Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave un equivalente di Britta Simon Wizergos produttività software che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cfd95-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cfd95-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cfd95-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfd95-149">**[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cfd95-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="cfd95-150">Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd95-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="cfd95-151">In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare single sign-on Wizergos produttività dell'applicazione in uso.</span><span class="sxs-lookup"><span data-stu-id="cfd95-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="cfd95-152">**tooconfigure Azure single sign-on AD Wizergos produttività software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfd95-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfd95-153">Nel portale classico hello in hello **produttività Wizergos** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cfd95-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 
2. <span data-ttu-id="cfd95-155">In hello **come si sarebbe ad esempio utenti toosign su tooWizergos Software per la produttività** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="cfd95-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="cfd95-157">In hello **Configura impostazioni App** nella pagina, fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="cfd95-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="cfd95-159">In hello **Configura accesso single sign-on in Software di produttività Wizergos** pagina, fare clic su **Scarica certificato**e quindi salvare il file hello nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="cfd95-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="cfd95-161">In una finestra del web browser, tenant produttività Wizergos tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cfd95-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="cfd95-162">Scegliere dal menu a tre linee hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="cfd95-164">Nella pagina visualizzata selezionare **AUTHENTICATION** (AUTENTICAZIONE) nel menu a sinistra e fare clic su **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="cfd95-166">Eseguire hello seguendo i passaggi **autenticazione** sezione.</span><span class="sxs-lookup"><span data-stu-id="cfd95-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="cfd95-168">Fare clic su **caricare** hello tooupload pulsante scaricato certificato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfd95-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="cfd95-169">In hello **URL autorità di certificazione** casella di testo inserire il valore di hello di **URL autorità di certificazione** dalla configurazione guidata di Azure AD applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfd95-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="cfd95-170">In hello **URL servizio Single Sign-On** casella di testo inserire il valore di hello di **URL servizio Single Sign-on** dalla configurazione guidata di Azure AD applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfd95-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="cfd95-171">In hello **Single Sign-Out URL** casella di testo inserire il valore di hello di **URL del servizio Single Sign-Out** dalla configurazione guidata di Azure AD applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfd95-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="cfd95-172">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cfd95-172">Click **Save** button.</span></span>
9. <span data-ttu-id="cfd95-173">Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][10]
10. <span data-ttu-id="cfd95-175">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cfd95-177">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd95-177">Create an Azure AD test user</span></span>
<span data-ttu-id="cfd95-178">obiettivo di Hello di questa sezione è toocreate un utente di test nel portale classico di hello chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfd95-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="cfd95-180">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfd95-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfd95-181">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="cfd95-183">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="cfd95-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="cfd95-184">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="cfd95-186">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="cfd95-188">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfd95-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="cfd95-190">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="cfd95-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="cfd95-191">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="cfd95-192">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-192">Click **Next**.</span></span>
6. <span data-ttu-id="cfd95-193">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfd95-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="cfd95-195">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="cfd95-196">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="cfd95-197">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="cfd95-198">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="cfd95-199">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-199">Click **Next**.</span></span>
7. <span data-ttu-id="cfd95-200">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="cfd95-202">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfd95-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="cfd95-204">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="cfd95-205">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="cfd95-206">Creare un utente di test Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="cfd95-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="cfd95-207">In questa sezione viene creato un utente chiamato Britta Simon in Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="cfd95-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="cfd95-208">Rivolgersi al team di supporto di Software per la produttività Wizergos tramite [ support@wizergos.com ](emailTo:support@wizergos.com) utenti hello tooadd nella piattaforma di produttività Wizergos hello.</span><span class="sxs-lookup"><span data-stu-id="cfd95-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cfd95-209">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd95-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="cfd95-210">obiettivo Hello di questa sezione è tooenabling Britta Simon toouse SSO Azure concedendo proprio tooWizergos accesso Software per la produttività.</span><span class="sxs-lookup"><span data-stu-id="cfd95-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Assegna utente][200]

<span data-ttu-id="cfd95-212">**tooassign Britta Simon tooWizergos Software per la produttività, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cfd95-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfd95-213">Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="cfd95-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Assegna utente][201]
2. <span data-ttu-id="cfd95-215">Nell'elenco di applicazioni hello, selezionare **Wizergos produttività**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="cfd95-217">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Assegna utente][203]
4. <span data-ttu-id="cfd95-219">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="cfd95-220">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="cfd95-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="cfd95-222">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cfd95-222">Test single sign-on</span></span>
<span data-ttu-id="cfd95-223">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cfd95-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="cfd95-224">Quando si fa clic su riquadro Wizergos produttività hello in hello Pannello di accesso, è necessario ottenere l'applicazione Software per la produttività Wizergos tooyour firmato in automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cfd95-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfd95-225">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cfd95-225">Additional resources</span></span>
* [<span data-ttu-id="cfd95-226">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfd95-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfd95-227">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfd95-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png

---
title: 'Esercitazione: Integrazione di Azure Active Directory con Pacific Timesheet | Documentazione Microsoft'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e attività del Pacifico."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 5fd57ff78a3a64c135f2de9895f4643b39e33bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="475d2-103">Esercitazione: Integrazione di Azure Active Directory con Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="475d2-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="475d2-104">In questa esercitazione, è illustrato come toointegrate foglio presenze Pacifico con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="475d2-104">In this tutorial, you learn how toointegrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="475d2-105">Integrazione del foglio presenze Pacifico con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="475d2-105">Integrating Pacific Timesheet with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="475d2-106">È possibile controllare in Azure AD che ha accesso tooPacific foglio presenze</span><span class="sxs-lookup"><span data-stu-id="475d2-106">You can control in Azure AD who has access tooPacific Timesheet</span></span>
- <span data-ttu-id="475d2-107">È possibile abilitare l'utenti tooautomatically get connesso tooPacific attività (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="475d2-107">You can enable your users tooautomatically get signed-on tooPacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="475d2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="475d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="475d2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="475d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="475d2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="475d2-110">Prerequisites</span></span>

<span data-ttu-id="475d2-111">integrazione di Azure AD con attività Pacifico tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="475d2-111">tooconfigure Azure AD integration with Pacific Timesheet, you need hello following items:</span></span>

- <span data-ttu-id="475d2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="475d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="475d2-113">Sottoscrizione di Pacific Timesheet abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="475d2-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="475d2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="475d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="475d2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="475d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="475d2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="475d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="475d2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="475d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="475d2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="475d2-118">Scenario description</span></span>
<span data-ttu-id="475d2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="475d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="475d2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="475d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="475d2-121">Aggiunta di attività Pacifico dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="475d2-121">Adding Pacific Timesheet from hello gallery</span></span>
2. <span data-ttu-id="475d2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="475d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-hello-gallery"></a><span data-ttu-id="475d2-123">Aggiunta di attività Pacifico dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="475d2-123">Adding Pacific Timesheet from hello gallery</span></span>
<span data-ttu-id="475d2-124">integrazione hello tooconfigure della attività Pacifico in Azure AD, è necessario tooadd foglio presenze Pacifico dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="475d2-124">tooconfigure hello integration of Pacific Timesheet into Azure AD, you need tooadd Pacific Timesheet from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="475d2-125">**tooadd Pacifico attività dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="475d2-125">**tooadd Pacific Timesheet from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="475d2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="475d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="475d2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="475d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="475d2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="475d2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="475d2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="475d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="475d2-133">Nella casella di ricerca hello, digitare **foglio presenze Pacifico**.</span><span class="sxs-lookup"><span data-stu-id="475d2-133">In hello search box, type **Pacific Timesheet**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="475d2-135">Nel riquadro dei risultati hello, selezionare **foglio presenze Pacifico**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="475d2-135">In hello results panel, select **Pacific Timesheet**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="475d2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="475d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="475d2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Pacific Timesheet con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="475d2-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="475d2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nella scheda attività Pacific è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="475d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pacific Timesheet is tooa user in Azure AD.</span></span> <span data-ttu-id="475d2-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nella scheda attività Pacifico deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="475d2-140">In other words, a link relationship between an Azure AD user and hello related user in Pacific Timesheet needs toobe established.</span></span>

<span data-ttu-id="475d2-141">Nella scheda attività Pacifico, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="475d2-141">In Pacific Timesheet, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="475d2-142">tooconfigure e prova AD Azure single sign-on con attività Pacifico, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="475d2-142">tooconfigure and test Azure AD single sign-on with Pacific Timesheet, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="475d2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="475d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="475d2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="475d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="475d2-145">**[Creazione di un utente test foglio presenze Pacifico](#creating-a-pacific-timesheet-test-user)**  -toohave un equivalente di Britta Simon nella Pacifico attività che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="475d2-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - toohave a counterpart of Britta Simon in Pacific Timesheet that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="475d2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="475d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="475d2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="475d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="475d2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="475d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="475d2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione foglio presenze Pacifico.</span><span class="sxs-lookup"><span data-stu-id="475d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="475d2-150">**Azure AD tooconfigure single sign-on con attività Pacifico, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="475d2-150">**tooconfigure Azure AD single sign-on with Pacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="475d2-151">Nel portale di Azure su hello hello **foglio presenze Pacifico** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="475d2-151">In hello Azure portal, on hello **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="475d2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="475d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="475d2-155">In hello **Pacifico foglio presenze dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="475d2-155">On hello **Pacific Timesheet Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="475d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="475d2-157">a.</span></span> <span data-ttu-id="475d2-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="475d2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="475d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="475d2-159">b.</span></span> <span data-ttu-id="475d2-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="475d2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="475d2-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="475d2-161">These values are not real.</span></span> <span data-ttu-id="475d2-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="475d2-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="475d2-163">Contatto [team di supporto foglio presenze Pacifico](http://www.pacifictimesheet.com/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="475d2-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) tooget these values.</span></span>
 
4. <span data-ttu-id="475d2-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="475d2-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="475d2-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="475d2-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="475d2-168">In hello **Pacifico foglio presenze configurazione** fare clic su **configurare attività Pacifico** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="475d2-168">On hello **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="475d2-169">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="475d2-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="475d2-171">tooconfigure single sign-on sul **foglio presenze Pacifico** lato, è necessario hello toosend scaricato **certificato (Base64)**, **SAML Single Sign-On Service URL**e  **ID entità SAML** troppo[team di supporto foglio presenze Pacifico](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="475d2-171">tooconfigure single sign-on on **Pacific Timesheet** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="475d2-172">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="475d2-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="475d2-173">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="475d2-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="475d2-174">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="475d2-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="475d2-175">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="475d2-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="475d2-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="475d2-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="475d2-177">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="475d2-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="475d2-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="475d2-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="475d2-180">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="475d2-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="475d2-182">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="475d2-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="475d2-184">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="475d2-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="475d2-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="475d2-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="475d2-188">a.</span><span class="sxs-lookup"><span data-stu-id="475d2-188">a.</span></span> <span data-ttu-id="475d2-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="475d2-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="475d2-190">b.</span><span class="sxs-lookup"><span data-stu-id="475d2-190">b.</span></span> <span data-ttu-id="475d2-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="475d2-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="475d2-192">c.</span><span class="sxs-lookup"><span data-stu-id="475d2-192">c.</span></span> <span data-ttu-id="475d2-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="475d2-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="475d2-194">d.</span><span class="sxs-lookup"><span data-stu-id="475d2-194">d.</span></span> <span data-ttu-id="475d2-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="475d2-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="475d2-196">Creazione di un utente di test di Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="475d2-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="475d2-197">In questa sezione viene creato un utente di nome Britta Simon in Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="475d2-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="475d2-198">Lavorare con [team di supporto foglio presenze Pacifico](http://www.pacifictimesheet.com/support) toocreate un utente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="475d2-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) toocreate a user in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="475d2-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="475d2-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="475d2-200">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPacific scheda attività.</span><span class="sxs-lookup"><span data-stu-id="475d2-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPacific Timesheet.</span></span>

![Assegna utente][200] 

<span data-ttu-id="475d2-202">**tooassign Britta Simon tooPacific attività, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="475d2-202">**tooassign Britta Simon tooPacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="475d2-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="475d2-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="475d2-205">Nell'elenco di applicazioni hello, selezionare **foglio presenze Pacifico**.</span><span class="sxs-lookup"><span data-stu-id="475d2-205">In hello applications list, select **Pacific Timesheet**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="475d2-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="475d2-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="475d2-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="475d2-209">Click **Add** button.</span></span> <span data-ttu-id="475d2-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="475d2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="475d2-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="475d2-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="475d2-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="475d2-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="475d2-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="475d2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="475d2-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="475d2-215">Testing single sign-on</span></span>

<span data-ttu-id="475d2-216">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="475d2-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="475d2-217">Quando si fa clic su riquadro attività Pacifico hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato nel foglio presenze Pacifico applicazione.</span><span class="sxs-lookup"><span data-stu-id="475d2-217">When you click hello Pacific Timesheet tile in hello Access Panel, you should get automatically signed-on tooyour Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="475d2-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="475d2-218">Additional resources</span></span>

* [<span data-ttu-id="475d2-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="475d2-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="475d2-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="475d2-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png


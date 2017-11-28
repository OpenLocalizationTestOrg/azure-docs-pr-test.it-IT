---
title: 'Esercitazione: Integrazione di Azure Active Directory con Birst Agile Business Analytics | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Birst Agile Business Analitica.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f007edcec0fb8ece215ab69f7ec7ca59ca34bddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="22f34-103">Esercitazione: Integrazione di Azure Active Directory con Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="22f34-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="22f34-104">In questa esercitazione, è illustrato come toointegrate Birst Agile Business Analitica con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22f34-104">In this tutorial, you learn how toointegrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22f34-105">L'integrazione Analitica Business Agile Birst con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="22f34-105">Integrating Birst Agile Business Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="22f34-106">È possibile controllare in Azure AD che ha accesso tooBirst Agile Analitica di Business</span><span class="sxs-lookup"><span data-stu-id="22f34-106">You can control in Azure AD who has access tooBirst Agile Business Analytics</span></span>
- <span data-ttu-id="22f34-107">È possibile abilitare l'utenti tooautomatically get connesso tooBirst Agile Analitica di Business (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f34-107">You can enable your users tooautomatically get signed-on tooBirst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22f34-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22f34-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="22f34-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22f34-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22f34-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="22f34-110">Prerequisites</span></span>

<span data-ttu-id="22f34-111">integrazione di Azure AD con Birst Agile Business Analitica tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="22f34-111">tooconfigure Azure AD integration with Birst Agile Business Analytics, you need hello following items:</span></span>

- <span data-ttu-id="22f34-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22f34-113">Sottoscrizione di Birst Agile Business Analytics abilitata all'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="22f34-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22f34-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="22f34-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22f34-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="22f34-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22f34-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="22f34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22f34-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22f34-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22f34-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="22f34-118">Scenario description</span></span>
<span data-ttu-id="22f34-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="22f34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22f34-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="22f34-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22f34-121">Aggiunta di Birst Agile Business Analitica dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="22f34-121">Adding Birst Agile Business Analytics from hello gallery</span></span>
2. <span data-ttu-id="22f34-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-hello-gallery"></a><span data-ttu-id="22f34-123">Aggiunta di Birst Agile Business Analitica dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="22f34-123">Adding Birst Agile Business Analytics from hello gallery</span></span>
<span data-ttu-id="22f34-124">integrazione hello tooconfigure di Birst Agile Business Analitica in Azure AD, è necessario tooadd Birst Agile Business Analitica dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="22f34-124">tooconfigure hello integration of Birst Agile Business Analytics into Azure AD, you need tooadd Birst Agile Business Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="22f34-125">**tooadd Birst Agile Business Analitica dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22f34-125">**tooadd Birst Agile Business Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="22f34-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="22f34-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22f34-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="22f34-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="22f34-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22f34-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="22f34-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="22f34-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="22f34-133">Nella casella di ricerca hello, digitare **Birst Agile Business Analitica**.</span><span class="sxs-lookup"><span data-stu-id="22f34-133">In hello search box, type **Birst Agile Business Analytics**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="22f34-135">Nel riquadro dei risultati hello, selezionare **Birst Agile Business Analitica**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="22f34-135">In hello results panel, select **Birst Agile Business Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22f34-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f34-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22f34-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Birst Agile Business Analytics usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="22f34-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="22f34-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Birst Agile Business Analitica è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f34-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Birst Agile Business Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="22f34-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Birst Agile Business Analitica deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="22f34-140">In other words, a link relationship between an Azure AD user and hello related user in Birst Agile Business Analytics needs toobe established.</span></span>

<span data-ttu-id="22f34-141">In Birst Agile Analitica di Business, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="22f34-141">In Birst Agile Business Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="22f34-142">tooconfigure e prova AD Azure single sign-on con Birst Agile Business Analitica, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="22f34-142">tooconfigure and test Azure AD single sign-on with Birst Agile Business Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="22f34-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="22f34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="22f34-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22f34-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22f34-145">**[Creazione di un utente test Birst Agile Business Analitica](#creating-a-birst-agile-business-analytics-test-user)**  -toohave un equivalente di Britta Simon in Birst Agile Analitica di Business che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="22f34-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - toohave a counterpart of Britta Simon in Birst Agile Business Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="22f34-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="22f34-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22f34-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="22f34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22f34-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f34-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22f34-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Birst Agile Business Analitica.</span><span class="sxs-lookup"><span data-stu-id="22f34-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="22f34-150">**tooconfigure AD Azure single sign-on con Birst Agile Analitica di Business, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22f34-150">**tooconfigure Azure AD single sign-on with Birst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="22f34-151">Nel portale di Azure su hello hello **Birst Agile Business Analitica** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="22f34-151">In hello Azure portal, on hello **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="22f34-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="22f34-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="22f34-155">In hello **Birst Agile Business Analitica dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="22f34-155">On hello **Birst Agile Business Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="22f34-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="22f34-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="22f34-158">URL Hello dipende dal Data Center hello che si trova l'account Birst:</span><span class="sxs-lookup"><span data-stu-id="22f34-158">hello URL depends on hello datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="22f34-159">Per l'utilizzo di Data Center Usa il modello di hello:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="22f34-159">For US datacenter use following hello pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="22f34-160">Per l'Europa datacenter utilizzare hello seguente motivo:`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="22f34-160">For Europe datacenter use hello following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="22f34-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="22f34-161">This value is not real.</span></span> <span data-ttu-id="22f34-162">Il valore di hello aggiornamento con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="22f34-162">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="22f34-163">Contatto [team di supporto Birst Agile Business Analitica Client](mailto:info@birst.com) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="22f34-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="22f34-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="22f34-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="22f34-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="22f34-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="22f34-168">In hello **Birst Agile Business Analitica configurazione** fare clic su **Analitica Business Agile Birst configurare** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="22f34-168">On hello **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="22f34-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="22f34-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="22f34-171">tooconfigure single sign-on sul **Birst Agile Business Analitica** lato, è necessario hello toosend scaricato **certificato (Base64)**, **Sign-Out URL ID entità SAML e SAML Single Sign-On URL del servizio** troppo[Birst Agile Business Analitica team di supporto](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="22f34-171">tooconfigure single sign-on on **Birst Agile Business Analytics** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="22f34-172">Ricordare team tooBirst che questa integrazione richiede l'algoritmo SHA256 (SHA1 non saranno supportate) in modo che possano impostati hello SSO nel server appropriato hello come **app2101** e così via.</span><span class="sxs-lookup"><span data-stu-id="22f34-172">Mention tooBirst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set hello SSO on hello appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="22f34-173">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="22f34-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="22f34-174">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="22f34-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="22f34-175">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="22f34-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22f34-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f34-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="22f34-177">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="22f34-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="22f34-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22f34-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="22f34-180">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="22f34-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22f34-182">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="22f34-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22f34-184">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="22f34-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22f34-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="22f34-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22f34-188">a.</span><span class="sxs-lookup"><span data-stu-id="22f34-188">a.</span></span> <span data-ttu-id="22f34-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22f34-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22f34-190">b.</span><span class="sxs-lookup"><span data-stu-id="22f34-190">b.</span></span> <span data-ttu-id="22f34-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="22f34-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22f34-192">c.</span><span class="sxs-lookup"><span data-stu-id="22f34-192">c.</span></span> <span data-ttu-id="22f34-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="22f34-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="22f34-194">d.</span><span class="sxs-lookup"><span data-stu-id="22f34-194">d.</span></span> <span data-ttu-id="22f34-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="22f34-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="22f34-196">Creazione di un utente test di Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="22f34-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="22f34-197">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Birst Agile Business Analitica toocreate.</span><span class="sxs-lookup"><span data-stu-id="22f34-197">hello objective of this section is toocreate a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="22f34-198">Lavorare con [Birst Agile Business Analitica team di supporto](mailto:info@birst.com) utenti hello tooadd hello Birst account.</span><span class="sxs-lookup"><span data-stu-id="22f34-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) tooadd hello users in hello Birst account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="22f34-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f34-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="22f34-200">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBirst Agile Analitica di Business.</span><span class="sxs-lookup"><span data-stu-id="22f34-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBirst Agile Business Analytics.</span></span>

![Assegna utente][200] 

<span data-ttu-id="22f34-202">**tooassign Britta Simon tooBirst Agile Analitica di Business, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22f34-202">**tooassign Britta Simon tooBirst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="22f34-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22f34-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="22f34-205">Nell'elenco di applicazioni hello, selezionare **Birst Agile Business Analitica**.</span><span class="sxs-lookup"><span data-stu-id="22f34-205">In hello applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="22f34-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="22f34-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="22f34-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22f34-209">Click **Add** button.</span></span> <span data-ttu-id="22f34-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22f34-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="22f34-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="22f34-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="22f34-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="22f34-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22f34-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22f34-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="22f34-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="22f34-215">Testing single sign-on</span></span>

<span data-ttu-id="22f34-216">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="22f34-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="22f34-217">Quando si fa clic hello Birst Agile Business Analitica riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Birst Agile Business Analitica.</span><span class="sxs-lookup"><span data-stu-id="22f34-217">When you click hello Birst Agile Business Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="22f34-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="22f34-218">Additional resources</span></span>

* [<span data-ttu-id="22f34-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f34-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22f34-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f34-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png


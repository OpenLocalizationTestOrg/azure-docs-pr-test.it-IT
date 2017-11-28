---
title: 'Esercitazione: Integrazione di Azure Active Directory con Predictix Price Reporting | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Predictix prezzo Reporting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: c2ba85f613f5a71de72278a0d1916c135b835b60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="77185-103">Esercitazione: Integrazione di Azure Active Directory con Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="77185-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="77185-104">In questa esercitazione, è illustrato come toointegrate Predictix prezzo Reporting con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77185-104">In this tutorial, you learn how toointegrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77185-105">Integrazione di Reporting di prezzo Predictix con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="77185-105">Integrating Predictix Price Reporting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77185-106">È possibile controllare in Azure AD che ha accesso tooPredictix prezzo Reporting.</span><span class="sxs-lookup"><span data-stu-id="77185-106">You can control in Azure AD who has access tooPredictix Price Reporting.</span></span>
- <span data-ttu-id="77185-107">È possibile abilitare l'utenti tooautomatically get connesso tooPredictix prezzo Reporting (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77185-107">You can enable your users tooautomatically get signed-on tooPredictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="77185-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="77185-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="77185-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77185-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77185-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77185-110">Prerequisites</span></span>

<span data-ttu-id="77185-111">integrazione di Azure AD con Reporting prezzo Predictix tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="77185-111">tooconfigure Azure AD integration with Predictix Price Reporting, you need hello following items:</span></span>

- <span data-ttu-id="77185-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77185-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77185-113">Sottoscrizione di Predictix Price Reporting abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="77185-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77185-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="77185-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77185-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="77185-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77185-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="77185-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77185-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77185-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77185-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="77185-118">Scenario description</span></span>
<span data-ttu-id="77185-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="77185-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77185-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="77185-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77185-121">Aggiunta di Reporting di prezzo Predictix dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="77185-121">Adding Predictix Price Reporting from hello gallery</span></span>
2. <span data-ttu-id="77185-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77185-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-hello-gallery"></a><span data-ttu-id="77185-123">Aggiunta di Reporting di prezzo Predictix dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="77185-123">Adding Predictix Price Reporting from hello gallery</span></span>
<span data-ttu-id="77185-124">integrazione hello tooconfigure di Predictix prezzo Reporting in Azure AD, è necessario tooadd Predictix prezzo Reporting dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="77185-124">tooconfigure hello integration of Predictix Price Reporting into Azure AD, you need tooadd Predictix Price Reporting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77185-125">**tooadd Predictix prezzo Reporting dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77185-125">**tooadd Predictix Price Reporting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77185-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="77185-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="77185-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="77185-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77185-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="77185-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="77185-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="77185-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="77185-133">Nella casella di ricerca hello, digitare **Predictix prezzo Reporting**selezionare **Predictix prezzo Reporting** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="77185-133">In hello search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix prezzo Reporting nell'elenco risultati hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="77185-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77185-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="77185-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Predictix Price Reporting usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="77185-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77185-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Predictix prezzo Reporting è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77185-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Price Reporting is tooa user in Azure AD.</span></span> <span data-ttu-id="77185-138">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello Predictix prezzo Reporting richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="77185-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Price Reporting needs toobe established.</span></span>

<span data-ttu-id="77185-139">Predictix prezzo Reporting, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="77185-139">In Predictix Price Reporting, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77185-140">tooconfigure e prova AD Azure single sign-on con Predictix prezzo Reporting, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="77185-140">tooconfigure and test Azure AD single sign-on with Predictix Price Reporting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77185-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="77185-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77185-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77185-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77185-143">**[Creare un utente test Reporting prezzo Predictix](#create-a-predictix-price-reporting-test-user)**  -toohave un equivalente di Britta Simon in Predictix prezzo Reporting che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="77185-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - toohave a counterpart of Britta Simon in Predictix Price Reporting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77185-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="77185-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77185-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="77185-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="77185-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77185-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="77185-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Predictix prezzo Reporting.</span><span class="sxs-lookup"><span data-stu-id="77185-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="77185-148">**tooconfigure AD Azure single sign-on con Predictix prezzo Reporting, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77185-148">**tooconfigure Azure AD single sign-on with Predictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="77185-149">Nel portale di Azure su hello hello **Predictix prezzo Reporting** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="77185-149">In hello Azure portal, on hello **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="77185-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="77185-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="77185-153">In hello **Predictix prezzo Reporting dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77185-153">On hello **Predictix Price Reporting Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="77185-155">a.</span><span class="sxs-lookup"><span data-stu-id="77185-155">a.</span></span> <span data-ttu-id="77185-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="77185-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="77185-157">b.</span><span class="sxs-lookup"><span data-stu-id="77185-157">b.</span></span> <span data-ttu-id="77185-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="77185-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="77185-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="77185-159">These values are not real.</span></span> <span data-ttu-id="77185-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="77185-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="77185-161">Contatto [team di supporto Client di segnalazione errori prezzo Predictix](http://www.infor.com/company/customer-center/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="77185-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) tooget these values.</span></span> 
 
4. <span data-ttu-id="77185-162">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="77185-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="77185-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="77185-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77185-166">In hello **configurazione di Reporting prezzo Predictix** fare clic su **configurare Reporting prezzo Predictix** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="77185-166">On hello **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77185-167">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="77185-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="77185-169">tooconfigure single sign-on sul **Predictix prezzo Reporting** lato, è necessario hello toosend scaricato **certificato (Base64)**, **Sign-Out URL ID entità SAML e SAML Single Sign-On URL del servizio** troppo[Predictix prezzo Reporting team di supporto](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="77185-169">tooconfigure single sign-on on **Predictix Price Reporting** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="77185-170">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="77185-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="77185-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="77185-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77185-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="77185-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77185-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77185-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="77185-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77185-174">Create an Azure AD test user</span></span>

<span data-ttu-id="77185-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="77185-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="77185-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77185-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77185-178">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="77185-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="77185-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="77185-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="77185-182">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="77185-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="77185-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77185-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="77185-186">a.</span><span class="sxs-lookup"><span data-stu-id="77185-186">a.</span></span> <span data-ttu-id="77185-187">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77185-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77185-188">b.</span><span class="sxs-lookup"><span data-stu-id="77185-188">b.</span></span> <span data-ttu-id="77185-189">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77185-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="77185-190">c.</span><span class="sxs-lookup"><span data-stu-id="77185-190">c.</span></span> <span data-ttu-id="77185-191">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="77185-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="77185-192">d.</span><span class="sxs-lookup"><span data-stu-id="77185-192">d.</span></span> <span data-ttu-id="77185-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="77185-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="77185-194">Creare un utente test di Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="77185-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="77185-195">In questa sezione viene creato un utente di nome Britta Simon in Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="77185-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="77185-196">Lavorare con [Predictix prezzo Reporting team di supporto](http://www.infor.com/company/customer-center/) utenti hello tooadd nella piattaforma di Reporting di prezzo Predictix hello.</span><span class="sxs-lookup"><span data-stu-id="77185-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) tooadd hello users in hello Predictix Price Reporting platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="77185-197">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="77185-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="77185-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPredictix prezzo Reporting.</span><span class="sxs-lookup"><span data-stu-id="77185-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Price Reporting.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="77185-200">**tooassign tooPredictix Britta Simon prezzo Reporting, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77185-200">**tooassign Britta Simon tooPredictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="77185-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="77185-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="77185-203">Nell'elenco di applicazioni hello, selezionare **Predictix prezzo Reporting**.</span><span class="sxs-lookup"><span data-stu-id="77185-203">In hello applications list, select **Predictix Price Reporting**.</span></span>

    ![collegamento Predictix prezzo Reporting Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="77185-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="77185-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="77185-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="77185-207">Click **Add** button.</span></span> <span data-ttu-id="77185-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="77185-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="77185-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="77185-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77185-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="77185-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77185-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="77185-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="77185-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="77185-213">Test single sign-on</span></span>

<span data-ttu-id="77185-214">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="77185-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77185-215">Quando si fa clic su riquadro Predictix prezzo Reporting hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Predictix prezzo Reporting applicazione.</span><span class="sxs-lookup"><span data-stu-id="77185-215">When you click hello Predictix Price Reporting tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77185-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="77185-216">Additional resources</span></span>

* [<span data-ttu-id="77185-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77185-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77185-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77185-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png


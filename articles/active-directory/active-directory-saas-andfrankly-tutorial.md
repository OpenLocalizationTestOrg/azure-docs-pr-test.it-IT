---
title: 'Esercitazione: Integrazione di Azure Active Directory con &frankly | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e & Francamente.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="4582f-103">Esercitazione: Integrazione di Azure Active Directory con &frankly</span><span class="sxs-lookup"><span data-stu-id="4582f-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="4582f-104">In questa esercitazione, è illustrato come toointegrate & Francamente con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4582f-104">In this tutorial, you learn how toointegrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4582f-105">L'integrazione di & Francamente con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4582f-105">Integrating &frankly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4582f-106">È possibile controllare in Azure AD che ha accesso troppo & Francamente</span><span class="sxs-lookup"><span data-stu-id="4582f-106">You can control in Azure AD who has access too&frankly</span></span>
- <span data-ttu-id="4582f-107">È possibile abilitare gli utenti tooautomatically ottenere connesso troppo & Francamente (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4582f-107">You can enable your users tooautomatically get signed-on too&frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4582f-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4582f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4582f-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4582f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4582f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4582f-110">Prerequisites</span></span>

<span data-ttu-id="4582f-111">integrazione di Azure AD tooconfigure con & Francamente, necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4582f-111">tooconfigure Azure AD integration with &frankly, you need hello following items:</span></span>

- <span data-ttu-id="4582f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4582f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4582f-113">Sottoscrizione di &frankly abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4582f-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4582f-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4582f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4582f-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4582f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4582f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4582f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4582f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4582f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4582f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4582f-118">Scenario description</span></span>
<span data-ttu-id="4582f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4582f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4582f-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4582f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4582f-121">Aggiunta di & Francamente dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="4582f-121">Adding &frankly from hello gallery</span></span>
2. <span data-ttu-id="4582f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4582f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-hello-gallery"></a><span data-ttu-id="4582f-123">Aggiunta di & Francamente dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="4582f-123">Adding &frankly from hello gallery</span></span>
<span data-ttu-id="4582f-124">integrazione di hello tooconfigure di & Francamente in Azure AD, è necessario tooadd & Francamente dall'elenco di tooyour hello della raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4582f-124">tooconfigure hello integration of &frankly into Azure AD, you need tooadd &frankly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4582f-125">**tooadd & Francamente dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4582f-125">**tooadd &frankly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4582f-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4582f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4582f-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4582f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4582f-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4582f-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4582f-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4582f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4582f-133">Nella casella di ricerca hello, digitare **& Francamente**.</span><span class="sxs-lookup"><span data-stu-id="4582f-133">In hello search box, type **&frankly**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="4582f-135">Nel riquadro dei risultati hello, selezionare **& Francamente**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4582f-135">In hello results panel, select **&frankly**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4582f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4582f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4582f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con &frankly in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4582f-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4582f-139">Per toowork di accesso singolo, Azure AD deve tooknow cosa hello utente corrispondente in & francamente è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4582f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in &frankly is tooa user in Azure AD.</span></span> <span data-ttu-id="4582f-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e hello correlati in & utente Francamente toobe esigenze stabilita.</span><span class="sxs-lookup"><span data-stu-id="4582f-140">In other words, a link relationship between an Azure AD user and hello related user in &frankly needs toobe established.</span></span>

<span data-ttu-id="4582f-141">In & Francamente, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4582f-141">In &frankly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4582f-142">tooconfigure e prova AD Azure single sign-on con & Francamente, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4582f-142">tooconfigure and test Azure AD single sign-on with &frankly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4582f-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4582f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4582f-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4582f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4582f-145">**[Creazione di un & Francamente utente test](#creating-a-frankly-test-user)**  -toohave un equivalente di Britta Simon in & Francamente ovvero toohello collegato rappresentazione in forma di Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4582f-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - toohave a counterpart of Britta Simon in &frankly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4582f-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4582f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4582f-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4582f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4582f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4582f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4582f-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel & Francamente applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4582f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="4582f-150">**Azure AD tooconfigure singolo sign-on con & Francamente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4582f-150">**tooconfigure Azure AD single sign-on with &frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="4582f-151">Nel portale di Azure su hello hello **& Francamente** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4582f-151">In hello Azure portal, on hello **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4582f-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4582f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="4582f-155">In hello **& Francamente dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="4582f-155">On hello **&frankly Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="4582f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4582f-157">a.</span></span> <span data-ttu-id="4582f-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4582f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="4582f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4582f-159">b.</span></span> <span data-ttu-id="4582f-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4582f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="4582f-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="4582f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="4582f-162">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="4582f-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="4582f-164">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4582f-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="4582f-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4582f-165">These values are not real.</span></span> <span data-ttu-id="4582f-166">Aggiornare questi valori con hello identificatore effettivo, Sign-on e URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="4582f-166">Update these values with hello actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="4582f-167">Contatto [team di supporto andfrankly](mailto:help@andfrankly.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4582f-167">Contact [andfrankly support team](mailto:help@andfrankly.com) tooget these values.</span></span>

5. <span data-ttu-id="4582f-168">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4582f-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="4582f-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4582f-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4582f-172">tooconfigure single sign-on sul **& Francamente** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto andfrankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="4582f-172">tooconfigure single sign-on on **&frankly** side, you need toosend hello downloaded **Metadata XML** too[andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="4582f-173">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4582f-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4582f-174">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4582f-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4582f-175">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4582f-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4582f-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4582f-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="4582f-177">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4582f-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4582f-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4582f-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4582f-180">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4582f-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4582f-182">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4582f-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4582f-184">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4582f-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4582f-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4582f-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4582f-188">a.</span><span class="sxs-lookup"><span data-stu-id="4582f-188">a.</span></span> <span data-ttu-id="4582f-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4582f-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4582f-190">b.</span><span class="sxs-lookup"><span data-stu-id="4582f-190">b.</span></span> <span data-ttu-id="4582f-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4582f-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4582f-192">c.</span><span class="sxs-lookup"><span data-stu-id="4582f-192">c.</span></span> <span data-ttu-id="4582f-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4582f-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4582f-194">d.</span><span class="sxs-lookup"><span data-stu-id="4582f-194">d.</span></span> <span data-ttu-id="4582f-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4582f-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="4582f-196">Creazione di un utente test di &frankly</span><span class="sxs-lookup"><span data-stu-id="4582f-196">Creating a &frankly test user</span></span>

<span data-ttu-id="4582f-197">In questa sezione viene creato un utente chiamato Britta Simon in &frankly.</span><span class="sxs-lookup"><span data-stu-id="4582f-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="4582f-198">Lavorare con [team di supporto andfrankly](mailto:help@andfrankly.com) gli utenti di hello tooadd hello & Francamente platform.</span><span class="sxs-lookup"><span data-stu-id="4582f-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) tooadd hello users in hello &frankly platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4582f-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4582f-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4582f-200">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo l'accesso troppo & Francamente.</span><span class="sxs-lookup"><span data-stu-id="4582f-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too&frankly.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4582f-202">**tooassign Britta Simon & Francamente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4582f-202">**tooassign Britta Simon too&frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="4582f-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4582f-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4582f-205">Nell'elenco di applicazioni hello, selezionare **& Francamente**.</span><span class="sxs-lookup"><span data-stu-id="4582f-205">In hello applications list, select **&frankly**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="4582f-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4582f-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4582f-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4582f-209">Click **Add** button.</span></span> <span data-ttu-id="4582f-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4582f-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4582f-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4582f-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4582f-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4582f-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4582f-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4582f-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4582f-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4582f-215">Testing single sign-on</span></span>

<span data-ttu-id="4582f-216">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4582f-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4582f-217">Quando fa clic su hello & si Francamente riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour & Francamente applicazioni</span><span class="sxs-lookup"><span data-stu-id="4582f-217">When you click hello &frankly tile in hello Access Panel, you should get automatically signed-on tooyour &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4582f-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4582f-218">Additional resources</span></span>

* [<span data-ttu-id="4582f-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4582f-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4582f-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4582f-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png


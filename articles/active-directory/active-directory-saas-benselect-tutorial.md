---
title: 'Esercitazione: Integrazione di Azure Active Directory con BenSelect | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BenSelect.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="f783c-103">Esercitazione: Integrazione di Azure Active Directory con BenSelect</span><span class="sxs-lookup"><span data-stu-id="f783c-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="f783c-104">In questa esercitazione, è illustrato come toointegrate BenSelect con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f783c-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f783c-105">Integrazione BenSelect con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f783c-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f783c-106">È possibile controllare in Azure AD che ha accesso tooBenSelect</span><span class="sxs-lookup"><span data-stu-id="f783c-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="f783c-107">È possibile abilitare l'utenti tooautomatically get connesso tooBenSelect (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f783c-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f783c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f783c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f783c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f783c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f783c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f783c-110">Prerequisites</span></span>

<span data-ttu-id="f783c-111">integrazione di Azure AD con BenSelect tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f783c-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="f783c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f783c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f783c-113">Sottoscrizione di BenSelect abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f783c-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f783c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f783c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f783c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f783c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f783c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f783c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f783c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f783c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f783c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f783c-118">Scenario description</span></span>
<span data-ttu-id="f783c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f783c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f783c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f783c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f783c-121">Aggiunta di BenSelect dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f783c-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="f783c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f783c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="f783c-123">Aggiunta di BenSelect dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f783c-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="f783c-124">integrazione hello tooconfigure di BenSelect in Azure AD, è necessario tooadd BenSelect dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f783c-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f783c-125">**tooadd BenSelect dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f783c-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f783c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f783c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f783c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f783c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f783c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f783c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f783c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f783c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f783c-133">Nella casella di ricerca hello, digitare **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="f783c-133">In hello search box, type **BenSelect**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="f783c-135">Nel riquadro dei risultati hello, selezionare **BenSelect**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f783c-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f783c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f783c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f783c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BenSelect usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f783c-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f783c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in BenSelect è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f783c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="f783c-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in BenSelect deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f783c-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="f783c-141">In BenSelect, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="f783c-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f783c-142">tooconfigure e prova AD Azure single sign-on con BenSelect, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f783c-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f783c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f783c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f783c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f783c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f783c-145">**[Creazione di un utente test BenSelect](#creating-a-benselect-test-user)**  -toohave un equivalente di Britta Simon in BenSelect che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f783c-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f783c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f783c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f783c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f783c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f783c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f783c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f783c-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione BenSelect.</span><span class="sxs-lookup"><span data-stu-id="f783c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="f783c-150">**Azure AD tooconfigure single sign-on con BenSelect, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f783c-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="f783c-151">Nel portale di Azure su hello hello **BenSelect** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f783c-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f783c-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f783c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="f783c-155">In hello **BenSelect dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f783c-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="f783c-157">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="f783c-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f783c-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="f783c-158">This value is not real.</span></span> <span data-ttu-id="f783c-159">Aggiornare questo valore con l'URL di risposta effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="f783c-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="f783c-160">Contatto [team di supporto BenSelect](mailto:support@selerix.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="f783c-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="f783c-161">In hello **certificato di firma SAML** fare clic su **Certificate(Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f783c-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="f783c-163">Applicazione di BenSelect prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="f783c-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f783c-164">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="f783c-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="f783c-165">È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f783c-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="f783c-166">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="f783c-166">hello following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="f783c-168">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="f783c-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="f783c-169">a.</span><span class="sxs-lookup"><span data-stu-id="f783c-169">a.</span></span> <span data-ttu-id="f783c-170">In hello **identificatore utente** elenco a discesa, seleziona **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="f783c-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="f783c-171">b.</span><span class="sxs-lookup"><span data-stu-id="f783c-171">b.</span></span> <span data-ttu-id="f783c-172">In hello **posta** elenco a discesa, seleziona **User**.</span><span class="sxs-lookup"><span data-stu-id="f783c-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="f783c-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f783c-173">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f783c-175">In hello **BenSelect configurazione** fare clic su **configurare BenSelect** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f783c-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f783c-176">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f783c-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="f783c-178">tooconfigure single sign-on sul **BenSelect** lato, è necessario hello toosend scaricato **Certificate(Raw)** e **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL**troppo[team di supporto BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="f783c-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="f783c-179">È necessario toomention che questa integrazione richiede l'algoritmo SHA256 hello (SHA1 non è supportata) tooset hello SSO nel server appropriato di hello come app2101 e così via.</span><span class="sxs-lookup"><span data-stu-id="f783c-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="f783c-180">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f783c-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f783c-181">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f783c-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f783c-182">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f783c-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f783c-183">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f783c-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="f783c-184">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f783c-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f783c-186">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f783c-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f783c-187">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f783c-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f783c-189">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f783c-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f783c-191">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f783c-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f783c-193">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f783c-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f783c-195">a.</span><span class="sxs-lookup"><span data-stu-id="f783c-195">a.</span></span> <span data-ttu-id="f783c-196">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f783c-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f783c-197">b.</span><span class="sxs-lookup"><span data-stu-id="f783c-197">b.</span></span> <span data-ttu-id="f783c-198">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f783c-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f783c-199">c.</span><span class="sxs-lookup"><span data-stu-id="f783c-199">c.</span></span> <span data-ttu-id="f783c-200">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f783c-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f783c-201">d.</span><span class="sxs-lookup"><span data-stu-id="f783c-201">d.</span></span> <span data-ttu-id="f783c-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f783c-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="f783c-203">Creazione di un utente di test di BenSelect</span><span class="sxs-lookup"><span data-stu-id="f783c-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="f783c-204">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in BenSelect toocreate.</span><span class="sxs-lookup"><span data-stu-id="f783c-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="f783c-205">Lavorare con [team di supporto BenSelect](mailto:support@selerix.com) tooadd utenti hello hello BenSelect account.</span><span class="sxs-lookup"><span data-stu-id="f783c-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f783c-206">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f783c-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f783c-207">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBenSelect.</span><span class="sxs-lookup"><span data-stu-id="f783c-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f783c-209">**tooassign Britta Simon tooBenSelect, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f783c-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="f783c-210">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f783c-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f783c-212">Nell'elenco di applicazioni hello, selezionare **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="f783c-212">In hello applications list, select **BenSelect**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="f783c-214">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f783c-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f783c-216">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f783c-216">Click **Add** button.</span></span> <span data-ttu-id="f783c-217">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f783c-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f783c-219">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f783c-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f783c-220">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f783c-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f783c-221">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f783c-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f783c-222">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f783c-222">Testing single sign-on</span></span>

<span data-ttu-id="f783c-223">In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f783c-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f783c-224">Quando si fa clic su riquadro BenSelect hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour BenSelect applicazione.</span><span class="sxs-lookup"><span data-stu-id="f783c-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f783c-225">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f783c-225">Additional resources</span></span>

* [<span data-ttu-id="f783c-226">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f783c-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f783c-227">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f783c-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png


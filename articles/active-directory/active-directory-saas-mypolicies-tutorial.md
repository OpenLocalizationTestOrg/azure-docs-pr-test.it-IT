---
title: 'Esercitazione: Integrazione di Azure Active Directory con myPolicies | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e myPolicies.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="e42c3-103">Esercitazione: integrazione di Azure Active Directory con myPolicies</span><span class="sxs-lookup"><span data-stu-id="e42c3-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="e42c3-104">In questa esercitazione, è illustrato come myPolicies toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e42c3-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e42c3-105">Integrazione myPolicies con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e42c3-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e42c3-106">È possibile controllare in Azure AD che ha accesso toomyPolicies</span><span class="sxs-lookup"><span data-stu-id="e42c3-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="e42c3-107">È possibile abilitare l'utenti tooautomatically get connesso toomyPolicies (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e42c3-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e42c3-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e42c3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e42c3-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e42c3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e42c3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e42c3-110">Prerequisites</span></span>

<span data-ttu-id="e42c3-111">integrazione di Azure AD con myPolicies tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e42c3-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="e42c3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e42c3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e42c3-113">Sottoscrizione di myPolicies abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e42c3-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e42c3-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e42c3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e42c3-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e42c3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e42c3-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e42c3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e42c3-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e42c3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e42c3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e42c3-118">Scenario description</span></span>
<span data-ttu-id="e42c3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e42c3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e42c3-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e42c3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e42c3-121">Aggiunta di myPolicies dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e42c3-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="e42c3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e42c3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="e42c3-123">Aggiunta di myPolicies dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e42c3-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="e42c3-124">integrazione hello tooconfigure di myPolicies in Azure AD, è necessario myPolicies tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e42c3-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e42c3-125">**myPolicies tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e42c3-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42c3-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e42c3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e42c3-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e42c3-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e42c3-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e42c3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e42c3-133">Nella casella di ricerca hello, digitare **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-133">In hello search box, type **myPolicies**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="e42c3-135">Nel riquadro dei risultati hello, selezionare **myPolicies**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e42c3-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e42c3-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e42c3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e42c3-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con myPolicies usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e42c3-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e42c3-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in myPolicies è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e42c3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="e42c3-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in myPolicies deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e42c3-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="e42c3-141">In myPolicies, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="e42c3-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e42c3-142">tooconfigure e prova AD Azure single sign-on con myPolicies, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e42c3-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e42c3-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e42c3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e42c3-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e42c3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e42c3-145">**[Creazione di un utente test myPolicies](#creating-a-mypolicies-test-user)**  -toohave un equivalente di Britta Simon in myPolicies che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e42c3-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e42c3-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e42c3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e42c3-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e42c3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e42c3-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e42c3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e42c3-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione myPolicies.</span><span class="sxs-lookup"><span data-stu-id="e42c3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="e42c3-150">**Azure AD tooconfigure single sign-on con myPolicies, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e42c3-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42c3-151">Nel portale di Azure su hello hello **myPolicies** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e42c3-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e42c3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="e42c3-155">In hello **myPolicies dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e42c3-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="e42c3-157">a.</span><span class="sxs-lookup"><span data-stu-id="e42c3-157">a.</span></span> <span data-ttu-id="e42c3-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="e42c3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="e42c3-159">b.</span><span class="sxs-lookup"><span data-stu-id="e42c3-159">b.</span></span> <span data-ttu-id="e42c3-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="e42c3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e42c3-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="e42c3-161">These values are not real.</span></span> <span data-ttu-id="e42c3-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="e42c3-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="e42c3-163">Contatto [team di supporto myPolicies](mailto:support@mypolicies.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="e42c3-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="e42c3-164">un'applicazione Hello myPolicies prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="e42c3-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="e42c3-165">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="e42c3-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="e42c3-166">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e42c3-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="e42c3-167">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="e42c3-167">hello following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="e42c3-169">Fare clic su **visualizzare e modificare tutti gli altri attributi utente** casella di controllo in hello **gli attributi utente** sezione attributi hello tooexpand.</span><span class="sxs-lookup"><span data-stu-id="e42c3-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="e42c3-170">Eseguire operazioni in ogni hello visualizzato attributi - hello</span><span class="sxs-lookup"><span data-stu-id="e42c3-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="e42c3-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="e42c3-171">Attribute Name</span></span> | <span data-ttu-id="e42c3-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="e42c3-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="e42c3-173">givenname</span><span class="sxs-lookup"><span data-stu-id="e42c3-173">givenname</span></span> | <span data-ttu-id="e42c3-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e42c3-174">user.givenname</span></span> |
    | <span data-ttu-id="e42c3-175">surname</span><span class="sxs-lookup"><span data-stu-id="e42c3-175">surname</span></span> | <span data-ttu-id="e42c3-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="e42c3-176">user.surname</span></span> |
    | <span data-ttu-id="e42c3-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="e42c3-177">emailaddress</span></span> | <span data-ttu-id="e42c3-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="e42c3-178">user.mail</span></span> |
    | <span data-ttu-id="e42c3-179">name</span><span class="sxs-lookup"><span data-stu-id="e42c3-179">name</span></span> | <span data-ttu-id="e42c3-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="e42c3-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="e42c3-181">a.</span><span class="sxs-lookup"><span data-stu-id="e42c3-181">a.</span></span> <span data-ttu-id="e42c3-182">Fare clic su hello tooopen di attributo hello **Modifica attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e42c3-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="e42c3-184">b.</span><span class="sxs-lookup"><span data-stu-id="e42c3-184">b.</span></span> <span data-ttu-id="e42c3-185">Eliminare il valore di URL hello dalla hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="e42c3-186">c.</span><span class="sxs-lookup"><span data-stu-id="e42c3-186">c.</span></span> <span data-ttu-id="e42c3-187">Fare clic su **Ok** impostazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e42c3-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="e42c3-188">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="e42c3-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="e42c3-190">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e42c3-190">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e42c3-192">In hello **myPolicies configurazione** fare clic su **configurare myPolicies** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="e42c3-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e42c3-193">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="e42c3-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="e42c3-195">tooconfigure single sign-on sul **myPolicies** lato, è necessario hello toosend scaricato **Certificate(Base64)** e **SAML Single Sign-On Service URL** troppo[team di supporto myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="e42c3-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="e42c3-196">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="e42c3-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e42c3-197">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="e42c3-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e42c3-198">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e42c3-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e42c3-199">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e42c3-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="e42c3-200">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e42c3-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e42c3-202">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e42c3-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42c3-203">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e42c3-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e42c3-205">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e42c3-207">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="e42c3-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e42c3-209">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e42c3-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e42c3-211">a.</span><span class="sxs-lookup"><span data-stu-id="e42c3-211">a.</span></span> <span data-ttu-id="e42c3-212">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e42c3-213">b.</span><span class="sxs-lookup"><span data-stu-id="e42c3-213">b.</span></span> <span data-ttu-id="e42c3-214">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e42c3-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e42c3-215">c.</span><span class="sxs-lookup"><span data-stu-id="e42c3-215">c.</span></span> <span data-ttu-id="e42c3-216">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e42c3-217">d.</span><span class="sxs-lookup"><span data-stu-id="e42c3-217">d.</span></span> <span data-ttu-id="e42c3-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="e42c3-219">Creazione di un utente di test di myPolicies</span><span class="sxs-lookup"><span data-stu-id="e42c3-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="e42c3-220">In questa sezione viene creato un utente di nome Britta Simon in myPolicies.</span><span class="sxs-lookup"><span data-stu-id="e42c3-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="e42c3-221">Lavorare con [myPolicies team di supporto](mailto:support@mypolicies.com) per aggiungere gli utenti di hello nella piattaforma myPolicies hello.</span><span class="sxs-lookup"><span data-stu-id="e42c3-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="e42c3-222">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e42c3-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e42c3-223">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e42c3-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e42c3-224">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso toomyPolicies.</span><span class="sxs-lookup"><span data-stu-id="e42c3-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e42c3-226">**tooassign Britta Simon toomyPolicies, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e42c3-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42c3-227">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e42c3-229">Nell'elenco di applicazioni hello, selezionare **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-229">In hello applications list, select **myPolicies**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="e42c3-231">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e42c3-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-233">Click **Add** button.</span></span> <span data-ttu-id="e42c3-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e42c3-236">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="e42c3-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e42c3-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e42c3-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e42c3-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e42c3-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e42c3-239">Testing single sign-on</span></span>

<span data-ttu-id="e42c3-240">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e42c3-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e42c3-241">Quando si fa clic hello myPolicies riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour myPolicies applicazione.</span><span class="sxs-lookup"><span data-stu-id="e42c3-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="e42c3-242">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e42c3-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e42c3-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e42c3-243">Additional resources</span></span>

* [<span data-ttu-id="e42c3-244">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e42c3-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e42c3-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e42c3-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png


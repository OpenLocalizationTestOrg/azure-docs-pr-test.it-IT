---
title: 'Esercitazione: Integrazione di Azure Active Directory con Collaborative Innovation | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e dell'innovazione collaborazione.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="6bb2c-103">Esercitazione: Integrazione di Azure Active Directory con Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="6bb2c-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="6bb2c-104">In questa esercitazione, è illustrato come toointegrate innovazione collaborazione con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6bb2c-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6bb2c-105">Integrazione di innovazione collaborazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6bb2c-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6bb2c-106">È possibile controllare in Azure AD che ha accesso tooCollaborative innovazione</span><span class="sxs-lookup"><span data-stu-id="6bb2c-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="6bb2c-107">È possibile abilitare l'utenti tooautomatically get connesso tooCollaborative innovazione (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bb2c-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6bb2c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb2c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6bb2c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6bb2c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bb2c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6bb2c-110">Prerequisites</span></span>

<span data-ttu-id="6bb2c-111">integrazione di Azure AD con innovazione collaborazione tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6bb2c-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="6bb2c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6bb2c-113">Sottoscrizione di Collaborative Innovation abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6bb2c-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6bb2c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6bb2c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6bb2c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6bb2c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6bb2c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6bb2c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6bb2c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6bb2c-118">Scenario description</span></span>
<span data-ttu-id="6bb2c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6bb2c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6bb2c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6bb2c-121">Aggiunta di collaborazione innovazione dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6bb2c-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="6bb2c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bb2c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="6bb2c-123">Aggiunta di collaborazione innovazione dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6bb2c-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="6bb2c-124">integrazione hello tooconfigure di collaborazione innovazione in Azure AD, è necessario tooadd innovazione collaborazione dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6bb2c-125">**tooadd collaborazione innovazione dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bb2c-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bb2c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6bb2c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6bb2c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6bb2c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6bb2c-133">Nella casella di ricerca hello, digitare **collaborazione innovazione**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="6bb2c-135">Nel riquadro dei risultati hello, selezionare **collaborazione innovazione**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6bb2c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bb2c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6bb2c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Collaborative Innovation mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6bb2c-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6bb2c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in collaborazione innovazione è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="6bb2c-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in collaborazione innovazione deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="6bb2c-141">In collaborazione dell'innovazione, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6bb2c-142">tooconfigure e prova AD Azure single sign-on con innovazione collaborazione, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6bb2c-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6bb2c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6bb2c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6bb2c-145">**[Creazione di un utente test innovazione collaborazione](#creating-a-collaborative-innovation-test-user)**  -toohave un equivalente di Britta Simon in collaborazione innovazione che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6bb2c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6bb2c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6bb2c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bb2c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6bb2c-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione collaborativa innovazione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="6bb2c-150">**Azure AD tooconfigure single sign-on con collaborazione dell'innovazione, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bb2c-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bb2c-151">Nel portale di Azure su hello hello **collaborazione innovazione** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6bb2c-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="6bb2c-155">In hello **collaborazione innovazione dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6bb2c-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="6bb2c-157">a.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-157">a.</span></span> <span data-ttu-id="6bb2c-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="6bb2c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="6bb2c-159">b.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-159">b.</span></span> <span data-ttu-id="6bb2c-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="6bb2c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="6bb2c-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="6bb2c-161">These values are not real.</span></span> <span data-ttu-id="6bb2c-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6bb2c-163">Contatto [team di supporto Client di collaborazione innovazione](https://www.unilever.com/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="6bb2c-164">Applicazione di innovazione collaborazione prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="6bb2c-165">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="6bb2c-166">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6bb2c-167">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="6bb2c-169">Fare clic su **visualizzare e modificare tutti gli altri attributi utente** casella di controllo in hello **gli attributi utente** sezione attributi hello tooexpand.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="6bb2c-170">Eseguire operazioni in ogni hello visualizzato attributi - hello</span><span class="sxs-lookup"><span data-stu-id="6bb2c-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="6bb2c-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="6bb2c-171">Attribute Name</span></span> | <span data-ttu-id="6bb2c-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="6bb2c-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="6bb2c-173">givenname</span><span class="sxs-lookup"><span data-stu-id="6bb2c-173">givenname</span></span> | <span data-ttu-id="6bb2c-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="6bb2c-174">user.givenname</span></span> |
    | <span data-ttu-id="6bb2c-175">surname</span><span class="sxs-lookup"><span data-stu-id="6bb2c-175">surname</span></span> | <span data-ttu-id="6bb2c-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="6bb2c-176">user.surname</span></span> |
    | <span data-ttu-id="6bb2c-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="6bb2c-177">emailaddress</span></span> | <span data-ttu-id="6bb2c-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="6bb2c-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="6bb2c-179">name</span><span class="sxs-lookup"><span data-stu-id="6bb2c-179">name</span></span> | <span data-ttu-id="6bb2c-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="6bb2c-180">user.userprincipalname</span></span> |

    <span data-ttu-id="6bb2c-181">a.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-181">a.</span></span> <span data-ttu-id="6bb2c-182">Fare clic su hello tooopen di attributo hello **Modifica attributo** finestra.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="6bb2c-184">b.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-184">b.</span></span> <span data-ttu-id="6bb2c-185">Eliminare il valore di URL hello dalla hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="6bb2c-186">c.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-186">c.</span></span> <span data-ttu-id="6bb2c-187">Fare clic su **Ok** impostazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="6bb2c-188">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="6bb2c-190">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6bb2c-190">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6bb2c-192">tooconfigure single sign-on sul **collaborazione innovazione** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di collaborazione innovazione](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="6bb2c-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="6bb2c-193">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6bb2c-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6bb2c-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6bb2c-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6bb2c-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6bb2c-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6bb2c-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bb2c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="6bb2c-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6bb2c-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bb2c-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bb2c-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6bb2c-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6bb2c-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6bb2c-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6bb2c-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6bb2c-209">a.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-209">a.</span></span> <span data-ttu-id="6bb2c-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6bb2c-211">b.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-211">b.</span></span> <span data-ttu-id="6bb2c-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6bb2c-213">c.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-213">c.</span></span> <span data-ttu-id="6bb2c-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6bb2c-215">d.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-215">d.</span></span> <span data-ttu-id="6bb2c-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="6bb2c-217">Creazione di un utente test di Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="6bb2c-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="6bb2c-218">toolog agli utenti di Azure AD tooenable in tooCollaborative innovazione, è necessario eseguirne il provisioning in collaborazione innovazione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="6bb2c-219">In caso di questa applicazione di provisioning è automatico come applicazione hello supporta just-in tempo il provisioning dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="6bb2c-220">Pertanto non sia presente alcuna necessità tooperform qui eventuali passaggi.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6bb2c-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bb2c-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6bb2c-222">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCollaborative innovazione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6bb2c-224">**tooassign Britta Simon tooCollaborative dell'innovazione, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6bb2c-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bb2c-225">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6bb2c-227">Nell'elenco di applicazioni hello, selezionare **collaborazione innovazione**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="6bb2c-229">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6bb2c-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-231">Click **Add** button.</span></span> <span data-ttu-id="6bb2c-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6bb2c-234">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6bb2c-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6bb2c-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6bb2c-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6bb2c-237">Testing single sign-on</span></span>

<span data-ttu-id="6bb2c-238">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6bb2c-239">Quando si fa clic su riquadro innovazione collaborazione hello in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione di collaborazione innovazione.</span><span class="sxs-lookup"><span data-stu-id="6bb2c-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="6bb2c-240">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6bb2c-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6bb2c-241">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6bb2c-241">Additional resources</span></span>

* [<span data-ttu-id="6bb2c-242">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6bb2c-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6bb2c-243">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6bb2c-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png


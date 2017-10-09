---
title: 'Esercitazione: Integrazione di Azure Active Directory con YouEarnedIt | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e YouEarnedIt.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="05348-103">Esercitazione: Integrazione di Azure Active Directory con YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="05348-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="05348-104">In questa esercitazione, è illustrato come toointegrate YouEarnedIt con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05348-104">In this tutorial, you learn how toointegrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05348-105">Integrazione YouEarnedIt con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="05348-105">Integrating YouEarnedIt with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05348-106">È possibile controllare in Azure AD che ha accesso tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="05348-106">You can control in Azure AD who has access tooYouEarnedIt.</span></span>
- <span data-ttu-id="05348-107">È possibile abilitare l'utenti tooautomatically get connesso tooYouEarnedIt (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05348-107">You can enable your users tooautomatically get signed-on tooYouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="05348-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="05348-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="05348-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05348-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05348-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05348-110">Prerequisites</span></span>

<span data-ttu-id="05348-111">integrazione di Azure AD con YouEarnedIt tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="05348-111">tooconfigure Azure AD integration with YouEarnedIt, you need hello following items:</span></span>

- <span data-ttu-id="05348-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05348-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05348-113">Sottoscrizione di YouEarnedIt abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05348-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05348-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="05348-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05348-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="05348-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05348-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="05348-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05348-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05348-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05348-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="05348-118">Scenario description</span></span>
<span data-ttu-id="05348-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="05348-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05348-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="05348-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05348-121">Aggiunta di YouEarnedIt dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="05348-121">Adding YouEarnedIt from hello gallery</span></span>
2. <span data-ttu-id="05348-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05348-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-hello-gallery"></a><span data-ttu-id="05348-123">Aggiunta di YouEarnedIt dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="05348-123">Adding YouEarnedIt from hello gallery</span></span>
<span data-ttu-id="05348-124">integrazione hello tooconfigure di YouEarnedIt in Azure AD, è necessario tooadd YouEarnedIt dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="05348-124">tooconfigure hello integration of YouEarnedIt into Azure AD, you need tooadd YouEarnedIt from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="05348-125">**tooadd YouEarnedIt dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05348-125">**tooadd YouEarnedIt from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="05348-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="05348-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="05348-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="05348-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="05348-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="05348-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="05348-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="05348-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="05348-133">Nella casella di ricerca hello, digitare **YouEarnedt**selezionare **YouEarnedt** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="05348-133">In hello search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="05348-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05348-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="05348-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con YouEarnedIt in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="05348-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05348-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in YouEarnedIt è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05348-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in YouEarnedIt is tooa user in Azure AD.</span></span> <span data-ttu-id="05348-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in YouEarnedIt deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="05348-138">In other words, a link relationship between an Azure AD user and hello related user in YouEarnedIt needs toobe established.</span></span>

<span data-ttu-id="05348-139">In YouEarnedIt, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="05348-139">In YouEarnedIt, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="05348-140">tooconfigure e prova AD Azure single sign-on con YouEarnedIt, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="05348-140">tooconfigure and test Azure AD single sign-on with YouEarnedIt, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05348-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="05348-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05348-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05348-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05348-143">**[Creare un utente test YouEarnedIt](#create-a-youearnedit-test-user)**  -toohave un equivalente di Britta Simon in YouEarnedIt che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="05348-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - toohave a counterpart of Britta Simon in YouEarnedIt that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05348-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05348-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05348-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="05348-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="05348-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05348-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="05348-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="05348-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="05348-148">**Azure AD tooconfigure single sign-on con YouEarnedIt, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05348-148">**tooconfigure Azure AD single sign-on with YouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="05348-149">Nel portale di Azure su hello hello **YouEarnedIt** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="05348-149">In hello Azure portal, on hello **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="05348-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05348-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="05348-153">In hello **YouEarnedIt dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="05348-153">On hello **YouEarnedIt Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="05348-155">a.</span><span class="sxs-lookup"><span data-stu-id="05348-155">a.</span></span> <span data-ttu-id="05348-156">In hello **Sign-on URL** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="05348-156">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | <span data-ttu-id="05348-157">Environment</span><span class="sxs-lookup"><span data-stu-id="05348-157">Environment</span></span>  | <span data-ttu-id="05348-158">Modello</span><span class="sxs-lookup"><span data-stu-id="05348-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="05348-159">Produzione</span><span class="sxs-lookup"><span data-stu-id="05348-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="05348-160">Sandbox</span><span class="sxs-lookup"><span data-stu-id="05348-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="05348-161">b.</span><span class="sxs-lookup"><span data-stu-id="05348-161">b.</span></span> <span data-ttu-id="05348-162">In hello **identificatore** , digitare un URL utilizzando hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="05348-162">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="05348-163">Environment</span><span class="sxs-lookup"><span data-stu-id="05348-163">Environment</span></span>  | <span data-ttu-id="05348-164">Modello</span><span class="sxs-lookup"><span data-stu-id="05348-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="05348-165">Produzione</span><span class="sxs-lookup"><span data-stu-id="05348-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="05348-166">Sandbox</span><span class="sxs-lookup"><span data-stu-id="05348-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="05348-167">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="05348-167">These values are not real.</span></span> <span data-ttu-id="05348-168">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="05348-168">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="05348-169">Contatto [team di supporto YouEarnedIt Client](https://youearnedit.freshdesk.com/support/tickets/new) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="05348-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) tooget these values.</span></span> 
 
4. <span data-ttu-id="05348-170">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="05348-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="05348-172">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="05348-172">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05348-174">In hello **YouEarnedIt configurazione** fare clic su **configurare YouEarnedIt** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="05348-174">On hello **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="05348-175">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="05348-175">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="05348-177">tooconfigure single sign-on sul **YouEarnedIt** lato, è necessario hello toosend scaricato **Certificate(Base64)** e **SAML Single Sign-On Service URL** troppo[Team di supporto YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="05348-177">tooconfigure single sign-on on **YouEarnedIt** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="05348-178">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="05348-178">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="05348-179">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="05348-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05348-180">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="05348-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05348-181">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05348-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="05348-182">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05348-182">Create an Azure AD test user</span></span>

<span data-ttu-id="05348-183">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="05348-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="05348-185">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05348-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05348-186">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="05348-186">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="05348-188">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="05348-188">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="05348-190">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="05348-190">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="05348-192">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="05348-192">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="05348-194">a.</span><span class="sxs-lookup"><span data-stu-id="05348-194">a.</span></span> <span data-ttu-id="05348-195">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05348-195">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05348-196">b.</span><span class="sxs-lookup"><span data-stu-id="05348-196">b.</span></span> <span data-ttu-id="05348-197">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05348-197">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="05348-198">c.</span><span class="sxs-lookup"><span data-stu-id="05348-198">c.</span></span> <span data-ttu-id="05348-199">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="05348-199">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="05348-200">d.</span><span class="sxs-lookup"><span data-stu-id="05348-200">d.</span></span> <span data-ttu-id="05348-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="05348-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="05348-202">Creare un utente di test di YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="05348-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="05348-203">In questa sezione viene creato un utente di nome Britta Simon in YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="05348-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="05348-204">Rivolgersi gli utenti YouEarnedIt supporto team tooadd hello nella piattaforma YouEarnedIt hello.</span><span class="sxs-lookup"><span data-stu-id="05348-204">Please work with YouEarnedIt support team tooadd hello users in hello YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="05348-205">YouEarnedIt prevede che i Provider di identità di toosupply hello un EmailAddress o un nome utente nell'attributo NameID hello.</span><span class="sxs-lookup"><span data-stu-id="05348-205">YouEarnedIt expect hello Identity Provider toosupply an EmailAddress  or UserName in hello NameID attribute.</span></span> <span data-ttu-id="05348-206">L'autenticazione avrà esito negativo se un nome utente corrispondente EmailAddress non viene trovato all'interno del database hello o non corrisponde esattamente.</span><span class="sxs-lookup"><span data-stu-id="05348-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within hello database or does not match exactly.</span></span> <span data-ttu-id="05348-207">Ciò richiede che gli account di essere importati nel sistema YouEarnedIt hello prima dell'integrazione di SSO hello (in genere tramite importazione API o CSV).</span><span class="sxs-lookup"><span data-stu-id="05348-207">This will require that accounts be imported into hello YouEarnedIt system before hello SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="05348-208">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05348-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="05348-209">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="05348-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYouEarnedIt.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="05348-211">**tooassign Britta Simon tooYouEarnedIt, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05348-211">**tooassign Britta Simon tooYouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="05348-212">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="05348-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="05348-214">Nell'elenco di applicazioni hello, selezionare **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="05348-214">In hello applications list, select **YouEarnedIt**.</span></span>

    ![collegamento YouEarnedIt Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="05348-216">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="05348-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="05348-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="05348-218">Click **Add** button.</span></span> <span data-ttu-id="05348-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="05348-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="05348-221">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="05348-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05348-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="05348-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05348-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="05348-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="05348-224">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05348-224">Test single sign-on</span></span>

<span data-ttu-id="05348-225">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="05348-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="05348-226">Quando si fa clic su riquadro YouEarnedIt hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour YouEarnedIt applicazione.</span><span class="sxs-lookup"><span data-stu-id="05348-226">When you click hello YouEarnedIt tile in hello Access Panel, you should get automatically signed-on tooyour YouEarnedIt application.</span></span>
<span data-ttu-id="05348-227">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05348-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05348-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="05348-228">Additional resources</span></span>

* [<span data-ttu-id="05348-229">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05348-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05348-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05348-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png


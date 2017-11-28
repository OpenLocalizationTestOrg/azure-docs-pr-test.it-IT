---
title: 'Esercitazione: Integrazione di Azure Active Directory con Innotas | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Innotas.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 31d787a351fe9362e35afee28a292c927f43702d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="8e7d1-103">Esercitazione: Integrazione di Azure Active Directory con Innotas</span><span class="sxs-lookup"><span data-stu-id="8e7d1-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="8e7d1-104">In questa esercitazione, è illustrato come toointegrate Innotas con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e7d1-104">In this tutorial, you learn how toointegrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e7d1-105">Integrazione Innotas con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8e7d1-105">Integrating Innotas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e7d1-106">È possibile controllare in Azure AD che ha accesso tooInnotas</span><span class="sxs-lookup"><span data-stu-id="8e7d1-106">You can control in Azure AD who has access tooInnotas</span></span>
- <span data-ttu-id="8e7d1-107">È possibile abilitare l'utenti tooautomatically get connesso tooInnotas (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e7d1-107">You can enable your users tooautomatically get signed-on tooInnotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e7d1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8e7d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e7d1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e7d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e7d1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8e7d1-110">Prerequisites</span></span>

<span data-ttu-id="8e7d1-111">integrazione di Azure AD con Innotas tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8e7d1-111">tooconfigure Azure AD integration with Innotas, you need hello following items:</span></span>

- <span data-ttu-id="8e7d1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e7d1-113">Sottoscrizione Innotas abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8e7d1-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e7d1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e7d1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8e7d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e7d1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e7d1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e7d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e7d1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8e7d1-118">Scenario description</span></span>

<span data-ttu-id="8e7d1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e7d1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8e7d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e7d1-121">Aggiunta di Innotas dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8e7d1-121">Adding Innotas from hello gallery</span></span>
2. <span data-ttu-id="8e7d1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e7d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-hello-gallery"></a><span data-ttu-id="8e7d1-123">Aggiunta di Innotas dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8e7d1-123">Adding Innotas from hello gallery</span></span>
<span data-ttu-id="8e7d1-124">integrazione hello tooconfigure di Innotas in Azure AD, è necessario tooadd Innotas dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-124">tooconfigure hello integration of Innotas into Azure AD, you need tooadd Innotas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e7d1-125">**tooadd Innotas dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8e7d1-125">**tooadd Innotas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e7d1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e7d1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e7d1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8e7d1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8e7d1-133">Nella casella di ricerca hello, digitare **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-133">In hello search box, type **Innotas**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="8e7d1-135">Nel riquadro dei risultati hello, selezionare **Innotas**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-135">In hello results panel, select **Innotas**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e7d1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e7d1-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8e7d1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Innotas usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8e7d1-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8e7d1-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Innotas è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Innotas is tooa user in Azure AD.</span></span> <span data-ttu-id="8e7d1-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Innotas deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-140">In other words, a link relationship between an Azure AD user and hello related user in Innotas needs toobe established.</span></span>

<span data-ttu-id="8e7d1-141">In Innotas, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-141">In Innotas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8e7d1-142">tooconfigure e test Azure single sign-on AD con Innotas, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8e7d1-142">tooconfigure and test Azure AD single sign-on with Innotas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e7d1-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e7d1-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e7d1-145">**[Creazione di un utente test Innotas](#creating-an-innotas-test-user)**  -toohave un equivalente di Britta Simon in Innotas che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - toohave a counterpart of Britta Simon in Innotas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e7d1-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e7d1-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e7d1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e7d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e7d1-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Innotas.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="8e7d1-150">**Azure AD tooconfigure single sign-on con Innotas, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8e7d1-150">**tooconfigure Azure AD single sign-on with Innotas, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e7d1-151">Nel portale di Azure su hello hello **Innotas** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-151">In hello Azure portal, on hello **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8e7d1-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="8e7d1-155">In hello **Innotas dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8e7d1-155">On hello **Innotas Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="8e7d1-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="8e7d1-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e7d1-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="8e7d1-158">This value is not real.</span></span> <span data-ttu-id="8e7d1-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8e7d1-160">Contatto [team di supporto di Innotas Client](https://www.innotas.com/contact) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-160">Contact [Innotas Client support team](https://www.innotas.com/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="8e7d1-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="8e7d1-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8e7d1-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e7d1-165">tooconfigure single sign-on sul **Innotas** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di Innotas](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="8e7d1-165">tooconfigure single sign-on on **Innotas** side, you need toosend hello downloaded **Metadata XML** too[Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="8e7d1-166">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8e7d1-167">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8e7d1-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e7d1-168">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e7d1-169">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e7d1-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e7d1-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e7d1-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="8e7d1-171">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8e7d1-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8e7d1-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e7d1-174">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e7d1-176">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e7d1-178">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e7d1-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8e7d1-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e7d1-182">a.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-182">a.</span></span> <span data-ttu-id="8e7d1-183">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e7d1-184">b.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-184">b.</span></span> <span data-ttu-id="8e7d1-185">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e7d1-186">c.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-186">c.</span></span> <span data-ttu-id="8e7d1-187">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e7d1-188">d.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-188">d.</span></span> <span data-ttu-id="8e7d1-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="8e7d1-190">Creazione di un utente di test di Innotas</span><span class="sxs-lookup"><span data-stu-id="8e7d1-190">Creating an Innotas test user</span></span>

<span data-ttu-id="8e7d1-191">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooInnotas.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-191">There is no action item for you tooconfigure user provisioning tooInnotas.</span></span>  
<span data-ttu-id="8e7d1-192">Quando un utente assegnato tenta toolog in tooInnotas mediante il pannello di accesso di hello, Innotas verifica se hello utente esiste.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-192">When an assigned user tries toolog in tooInnotas using hello access panel, Innotas checks whether hello user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="8e7d1-193">Se l'account utente non è presente, Innotas lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8e7d1-194">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e7d1-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8e7d1-195">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooInnotas.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInnotas.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8e7d1-197">**tooassign Britta Simon tooInnotas, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8e7d1-197">**tooassign Britta Simon tooInnotas, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e7d1-198">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8e7d1-200">Nell'elenco di applicazioni hello, selezionare **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-200">In hello applications list, select **Innotas**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="8e7d1-202">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8e7d1-204">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-204">Click **Add** button.</span></span> <span data-ttu-id="8e7d1-205">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8e7d1-207">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e7d1-208">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e7d1-209">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e7d1-210">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8e7d1-210">Testing single sign-on</span></span>

<span data-ttu-id="8e7d1-211">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8e7d1-212">Quando si fa clic hello Innotas riquadro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Innotas applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e7d1-212">When you click hello Innotas tile in hello Access Panel, you should get automatically signed-on tooyour Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e7d1-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8e7d1-213">Additional resources</span></span>

* [<span data-ttu-id="8e7d1-214">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e7d1-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e7d1-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e7d1-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con ICIMS | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ICIMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="413b1-103">Esercitazione: Integrazione di Azure Active Directory con ICIMS</span><span class="sxs-lookup"><span data-stu-id="413b1-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="413b1-104">In questa esercitazione, è illustrato come toointegrate ICIMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="413b1-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="413b1-105">Integrazione ICIMS con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="413b1-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="413b1-106">È possibile controllare in Azure AD che ha accesso tooICIMS</span><span class="sxs-lookup"><span data-stu-id="413b1-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="413b1-107">È possibile abilitare l'utenti tooautomatically get connesso tooICIMS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="413b1-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="413b1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="413b1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="413b1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="413b1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="413b1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="413b1-110">Prerequisites</span></span>

<span data-ttu-id="413b1-111">integrazione di Azure AD con ICIMS tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="413b1-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="413b1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="413b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="413b1-113">Sottoscrizione di ICIMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="413b1-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="413b1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="413b1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="413b1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="413b1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="413b1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="413b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="413b1-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="413b1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="413b1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="413b1-118">Scenario description</span></span>
<span data-ttu-id="413b1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="413b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="413b1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="413b1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="413b1-121">Aggiunta di ICIMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="413b1-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="413b1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="413b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="413b1-123">Aggiunta di ICIMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="413b1-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="413b1-124">integrazione hello tooconfigure di ICIMS in Azure AD, è necessario tooadd ICIMS dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="413b1-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="413b1-125">**tooadd ICIMS dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="413b1-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="413b1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="413b1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="413b1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="413b1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="413b1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="413b1-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="413b1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="413b1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="413b1-133">Nella casella di ricerca hello, digitare **ICIMS**selezionare **ICIMS** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="413b1-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="413b1-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="413b1-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="413b1-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ICIMS in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="413b1-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="413b1-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ICIMS è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="413b1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="413b1-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ICIMS deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="413b1-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="413b1-139">In ICIMS, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="413b1-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="413b1-140">tooconfigure e prova AD Azure single sign-on con ICIMS, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="413b1-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="413b1-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="413b1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="413b1-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="413b1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="413b1-143">**[Creare un utente test ICIMS](#create-an-icims-test-user)**  -toohave un equivalente di Britta Simon in ICIMS che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="413b1-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="413b1-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="413b1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="413b1-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="413b1-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="413b1-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="413b1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="413b1-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ICIMS.</span><span class="sxs-lookup"><span data-stu-id="413b1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="413b1-148">**Azure AD tooconfigure single sign-on con ICIMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="413b1-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="413b1-149">Nel portale di Azure su hello hello **ICIMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="413b1-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="413b1-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="413b1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="413b1-153">In hello **ICIMS dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="413b1-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sul Single Sign-On di URL e dominio di ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="413b1-155">a.</span><span class="sxs-lookup"><span data-stu-id="413b1-155">a.</span></span> <span data-ttu-id="413b1-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="413b1-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="413b1-157">b.</span><span class="sxs-lookup"><span data-stu-id="413b1-157">b.</span></span> <span data-ttu-id="413b1-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="413b1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="413b1-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="413b1-159">These values are not real.</span></span> <span data-ttu-id="413b1-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="413b1-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="413b1-161">Contatto [team di supporto Client ICIMS](https://www.icims.com/contact-us) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="413b1-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="413b1-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="413b1-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="413b1-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="413b1-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="413b1-166">In hello **ICIMS configurazione** fare clic su **configurare ICIMS** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="413b1-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="413b1-167">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="413b1-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="413b1-169">tooconfigure single sign-on sul **ICIMS** lato, è necessario hello toosend scaricato **Metadata XML**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo [ICIMS team di supporto](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="413b1-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="413b1-170">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="413b1-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="413b1-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="413b1-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="413b1-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="413b1-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="413b1-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="413b1-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="413b1-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="413b1-174">Create an Azure AD test user</span></span>
<span data-ttu-id="413b1-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="413b1-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="413b1-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="413b1-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="413b1-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="413b1-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="413b1-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="413b1-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="413b1-182">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="413b1-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="413b1-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="413b1-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="413b1-186">a.</span><span class="sxs-lookup"><span data-stu-id="413b1-186">a.</span></span> <span data-ttu-id="413b1-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="413b1-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="413b1-188">b.</span><span class="sxs-lookup"><span data-stu-id="413b1-188">b.</span></span> <span data-ttu-id="413b1-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="413b1-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="413b1-190">c.</span><span class="sxs-lookup"><span data-stu-id="413b1-190">c.</span></span> <span data-ttu-id="413b1-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="413b1-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="413b1-192">d.</span><span class="sxs-lookup"><span data-stu-id="413b1-192">d.</span></span> <span data-ttu-id="413b1-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="413b1-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="413b1-194">Creare un utente test di ICIMS</span><span class="sxs-lookup"><span data-stu-id="413b1-194">Create an ICIMS test user</span></span>

<span data-ttu-id="413b1-195">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in ICIMS toocreate.</span><span class="sxs-lookup"><span data-stu-id="413b1-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="413b1-196">Lavorare con [team di supporto ICIMS](https://www.icims.com/contact-us) tooadd utenti hello hello account ICIMS.</span><span class="sxs-lookup"><span data-stu-id="413b1-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="413b1-197">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="413b1-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="413b1-198">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooICIMS.</span><span class="sxs-lookup"><span data-stu-id="413b1-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![Assegnazione del ruolo utente hello][200]

<span data-ttu-id="413b1-200">**tooassign Britta Simon tooICIMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="413b1-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="413b1-201">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="413b1-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="413b1-203">Nell'elenco di applicazioni hello, selezionare **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="413b1-203">In hello applications list, select **ICIMS**.</span></span>

    ![Hello ICIMS collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="413b1-205">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="413b1-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="413b1-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="413b1-207">Click **Add** button.</span></span> <span data-ttu-id="413b1-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="413b1-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="413b1-210">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="413b1-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="413b1-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="413b1-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="413b1-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="413b1-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="413b1-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="413b1-213">Test single sign-on</span></span>

<span data-ttu-id="413b1-214">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="413b1-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="413b1-215">Quando si fa clic hello ICIMS riquadro in hello Pannello di accesso, è necessario ottenere applicazione ICIMS tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="413b1-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="413b1-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="413b1-216">Additional resources</span></span>

* [<span data-ttu-id="413b1-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="413b1-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="413b1-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="413b1-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png


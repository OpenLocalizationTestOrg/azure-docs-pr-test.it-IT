---
title: 'Esercitazione: Integrazione di Azure Active Directory con UNIFI | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e UNIFI.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="a929e-103">Esercitazione: Integrazione di Azure Active Directory con UNIFI</span><span class="sxs-lookup"><span data-stu-id="a929e-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="a929e-104">In questa esercitazione, è illustrato come toointegrate UNIFI con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a929e-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a929e-105">Integrazione UNIFI con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a929e-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a929e-106">È possibile controllare in Azure AD che ha accesso tooUNIFI</span><span class="sxs-lookup"><span data-stu-id="a929e-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="a929e-107">È possibile abilitare l'utenti tooautomatically get connesso tooUNIFI (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a929e-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a929e-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a929e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a929e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a929e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a929e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a929e-110">Prerequisites</span></span>

<span data-ttu-id="a929e-111">integrazione di Azure AD con UNIFI tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a929e-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="a929e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a929e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a929e-113">Una sottoscrizione UNIFI abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a929e-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a929e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a929e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a929e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="a929e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a929e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a929e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a929e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a929e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a929e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a929e-118">Scenario description</span></span>
<span data-ttu-id="a929e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a929e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a929e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="a929e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a929e-121">Aggiunta di UNIFI dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a929e-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="a929e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a929e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="a929e-123">Aggiunta di UNIFI dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a929e-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="a929e-124">integrazione hello tooconfigure di UNIFI in Azure AD, è necessario tooadd UNIFI dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a929e-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a929e-125">**tooadd UNIFI dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a929e-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a929e-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a929e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a929e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a929e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a929e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a929e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a929e-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a929e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a929e-133">Nella casella di ricerca hello, digitare **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="a929e-133">In hello search box, type **UNIFI**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="a929e-135">Nel riquadro dei risultati hello, selezionare **UNIFI**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a929e-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a929e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a929e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a929e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UNIFI in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a929e-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a929e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in UNIFI è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a929e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="a929e-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in UNIFI deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="a929e-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="a929e-141">In UNIFI, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="a929e-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a929e-142">tooconfigure e prova AD Azure single sign-on con UNIFI, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="a929e-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a929e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a929e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a929e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a929e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a929e-145">**[Creazione di un UNIFI utente test](#creating-a-unifi-test-user)**  -toohave un equivalente di Britta Simon in UNIFI che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a929e-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a929e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a929e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a929e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a929e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a929e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a929e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a929e-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione UNIFI.</span><span class="sxs-lookup"><span data-stu-id="a929e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="a929e-150">**Azure AD tooconfigure single sign-on con UNIFI, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a929e-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="a929e-151">Nel portale di Azure su hello hello **UNIFI** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a929e-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a929e-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a929e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="a929e-155">In hello **UNIFI dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="a929e-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="a929e-157">In hello **identificatore** casella di testo, valore di tipo hello:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="a929e-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="a929e-158">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="a929e-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="a929e-160">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="a929e-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="a929e-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="a929e-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="a929e-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a929e-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a929e-165">In hello **UNIFI configurazione** fare clic su **configurare UNIFI** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="a929e-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a929e-166">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a929e-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="a929e-168">In una finestra del web browser, accedere tooyour **UNIFI** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a929e-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="a929e-169">Fare clic su hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="a929e-169">Click on hello **Users**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="a929e-171">Fare clic su hello **Aggiungi nuovo Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="a929e-171">Click on hello **Add New Identity Provider**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="a929e-173">In hello **Add Identity Provider** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a929e-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="a929e-175">a.</span><span class="sxs-lookup"><span data-stu-id="a929e-175">a.</span></span> <span data-ttu-id="a929e-176">In hello **nome Provider** casella di testo Nome hello del tipo di Provider di identità hello...</span><span class="sxs-lookup"><span data-stu-id="a929e-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="a929e-177">b.</span><span class="sxs-lookup"><span data-stu-id="a929e-177">b.</span></span> <span data-ttu-id="a929e-178">In hello hello **URL Provider** casella di testo incollare hello **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a929e-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a929e-179">c.</span><span class="sxs-lookup"><span data-stu-id="a929e-179">c.</span></span> <span data-ttu-id="a929e-180">Aprire hello certificato scaricato dal portale di Azure nel blocco note, hello rimuovere hello **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---** tag e quindi incollare hello rimanente contenuto in Hello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="a929e-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="a929e-181">d.</span><span class="sxs-lookup"><span data-stu-id="a929e-181">d.</span></span> <span data-ttu-id="a929e-182">Seleziona hello **provider predefinito** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="a929e-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="a929e-183">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="a929e-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a929e-184">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="a929e-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a929e-185">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a929e-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a929e-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a929e-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="a929e-187">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a929e-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a929e-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a929e-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a929e-190">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a929e-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a929e-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a929e-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a929e-194">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="a929e-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a929e-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a929e-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a929e-198">a.</span><span class="sxs-lookup"><span data-stu-id="a929e-198">a.</span></span> <span data-ttu-id="a929e-199">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a929e-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a929e-200">b.</span><span class="sxs-lookup"><span data-stu-id="a929e-200">b.</span></span> <span data-ttu-id="a929e-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a929e-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a929e-202">c.</span><span class="sxs-lookup"><span data-stu-id="a929e-202">c.</span></span> <span data-ttu-id="a929e-203">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="a929e-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a929e-204">d.</span><span class="sxs-lookup"><span data-stu-id="a929e-204">d.</span></span> <span data-ttu-id="a929e-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a929e-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="a929e-206">Creazione di un utente test di UNIFI</span><span class="sxs-lookup"><span data-stu-id="a929e-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="a929e-207">In questa sezione viene creato un utente di nome Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a929e-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="a929e-208">**UNIFI** supporta il provisioning automatico dell'utente, pertanto non è necessaria la procedura manuale.</span><span class="sxs-lookup"><span data-stu-id="a929e-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="a929e-209">Gli utenti vengono creati automaticamente al termine dell'autenticazione da hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a929e-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a929e-210">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a929e-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a929e-211">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooUNIFI.</span><span class="sxs-lookup"><span data-stu-id="a929e-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a929e-213">**tooassign Britta Simon tooUNIFI, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a929e-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="a929e-214">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a929e-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a929e-216">Nell'elenco di applicazioni hello, selezionare **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="a929e-216">In hello applications list, select **UNIFI**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="a929e-218">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a929e-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a929e-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a929e-220">Click **Add** button.</span></span> <span data-ttu-id="a929e-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a929e-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a929e-223">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a929e-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a929e-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a929e-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a929e-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a929e-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a929e-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a929e-226">Testing single sign-on</span></span>

<span data-ttu-id="a929e-227">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a929e-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a929e-228">Quando si fa clic hello UNIFI riquadro in hello Pannello di accesso, è necessario ottenere applicazione UNIFI tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="a929e-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="a929e-229">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a929e-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a929e-230">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a929e-230">Additional resources</span></span>

* [<span data-ttu-id="a929e-231">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a929e-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a929e-232">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a929e-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Voyance | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Voyance.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="a8be6-103">Esercitazione: integrazione di Azure Active Directory con Voyance</span><span class="sxs-lookup"><span data-stu-id="a8be6-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="a8be6-104">In questa esercitazione, è illustrato come toointegrate Voyance con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8be6-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8be6-105">Integrazione Voyance con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a8be6-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a8be6-106">È possibile controllare in Azure AD che ha accesso tooVoyance</span><span class="sxs-lookup"><span data-stu-id="a8be6-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="a8be6-107">È possibile abilitare l'utenti tooautomatically get connesso tooVoyance (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8be6-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8be6-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a8be6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a8be6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8be6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8be6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8be6-110">Prerequisites</span></span>

<span data-ttu-id="a8be6-111">integrazione di Azure AD con Voyance tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a8be6-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="a8be6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8be6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8be6-113">Sottoscrizione di Voyance abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a8be6-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8be6-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a8be6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8be6-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="a8be6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8be6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a8be6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8be6-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8be6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8be6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a8be6-118">Scenario description</span></span>
<span data-ttu-id="a8be6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a8be6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8be6-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="a8be6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8be6-121">Aggiunta di Voyance dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a8be6-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="a8be6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8be6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="a8be6-123">Aggiunta di Voyance dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a8be6-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="a8be6-124">integrazione hello tooconfigure di Voyance in Azure AD, è necessario tooadd Voyance dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a8be6-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a8be6-125">**tooadd Voyance dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a8be6-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8be6-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a8be6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="a8be6-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a8be6-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="a8be6-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a8be6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="a8be6-133">Nella casella di ricerca hello, digitare **Voyance**selezionare **Voyance** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a8be6-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a8be6-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8be6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a8be6-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Voyance in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a8be6-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a8be6-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Voyance è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8be6-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="a8be6-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Voyance deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="a8be6-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="a8be6-139">In Voyance, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="a8be6-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a8be6-140">tooconfigure e prova AD Azure single sign-on con Voyance, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="a8be6-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a8be6-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a8be6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a8be6-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8be6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8be6-143">**[Creare un utente test Voyance](#create-a-voyance-test-user)**  -toohave un equivalente di Britta Simon in Voyance che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a8be6-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8be6-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a8be6-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8be6-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a8be6-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a8be6-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8be6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a8be6-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Voyance.</span><span class="sxs-lookup"><span data-stu-id="a8be6-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="a8be6-148">**Azure AD tooconfigure single sign-on con Voyance, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a8be6-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8be6-149">Nel portale di Azure su hello hello **Voyance** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="a8be6-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a8be6-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="a8be6-153">In hello **Voyance dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="a8be6-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Voyance per IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="a8be6-155">a.</span><span class="sxs-lookup"><span data-stu-id="a8be6-155">a.</span></span> <span data-ttu-id="a8be6-156">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="a8be6-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="a8be6-157">b.</span><span class="sxs-lookup"><span data-stu-id="a8be6-157">b.</span></span> <span data-ttu-id="a8be6-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="a8be6-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="a8be6-159">Controllare **Mostra URL impostazioni avanzate** ed eseguire hello riportata dopo il passaggio se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="a8be6-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Voyance per SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="a8be6-161">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="a8be6-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a8be6-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="a8be6-162">These values are not real.</span></span> <span data-ttu-id="a8be6-163">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a8be6-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a8be6-164">Contatto [team di supporto Voyance Client](mailto:support@nyansa.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="a8be6-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="a8be6-165">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="a8be6-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="a8be6-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a8be6-167">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a8be6-169">In hello **Voyance configurazione** fare clic su **configurare Voyance** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="a8be6-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a8be6-170">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="a8be6-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="a8be6-172">In una finestra del web browser, accesso tooyour Voyance tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a8be6-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="a8be6-173">Passare toohello alto a destra della barra di spostamento hello e fare clic su hello elenco a discesa che indica che "**University Acme**".</span><span class="sxs-lookup"><span data-stu-id="a8be6-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Configurare l'accesso Single Sign-On sul lato app - Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="a8be6-175">Fare clic su "**Admin Settings**" (Impostazioni amministrazione).</span><span class="sxs-lookup"><span data-stu-id="a8be6-175">Click "**Admin Settings**".</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - Impostazioni di amministrazione](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="a8be6-177">Fare clic sulla scheda "**User Access**" (Accesso utente).</span><span class="sxs-lookup"><span data-stu-id="a8be6-177">Click "**User Access**" tab.</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - Accesso utente](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="a8be6-179">Fare clic su hello "**SSO è disabilitato**" pulsante tooconfigure AD Azure come un provider di identità tramite SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="a8be6-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - Pulsante che indica che l'accesso SSO è disabilitato](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="a8be6-181">Andare troppo**v2 SAML** sezione ed eseguire i passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="a8be6-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Configurare l'accesso Single Sign-On sul lato app - SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="a8be6-183">a.</span><span class="sxs-lookup"><span data-stu-id="a8be6-183">a.</span></span> <span data-ttu-id="a8be6-184">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="a8be6-185">b.</span><span class="sxs-lookup"><span data-stu-id="a8be6-185">b.</span></span> <span data-ttu-id="a8be6-186">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **IdP Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="a8be6-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="a8be6-187">c.</span><span class="sxs-lookup"><span data-stu-id="a8be6-187">c.</span></span> <span data-ttu-id="a8be6-188">Aprire il certificato con codificata Base64 scaricato nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **IdP Cert** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="a8be6-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="a8be6-189">d.</span><span class="sxs-lookup"><span data-stu-id="a8be6-189">d.</span></span> <span data-ttu-id="a8be6-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a8be6-191">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="a8be6-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a8be6-192">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="a8be6-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a8be6-193">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a8be6-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a8be6-194">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8be6-194">Create an Azure AD test user</span></span>

<span data-ttu-id="a8be6-195">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a8be6-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="a8be6-197">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a8be6-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8be6-198">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a8be6-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8be6-200">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8be6-202">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="a8be6-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8be6-204">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a8be6-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8be6-206">a.</span><span class="sxs-lookup"><span data-stu-id="a8be6-206">a.</span></span> <span data-ttu-id="a8be6-207">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8be6-208">b.</span><span class="sxs-lookup"><span data-stu-id="a8be6-208">b.</span></span> <span data-ttu-id="a8be6-209">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a8be6-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8be6-210">c.</span><span class="sxs-lookup"><span data-stu-id="a8be6-210">c.</span></span> <span data-ttu-id="a8be6-211">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a8be6-212">d.</span><span class="sxs-lookup"><span data-stu-id="a8be6-212">d.</span></span> <span data-ttu-id="a8be6-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="a8be6-214">Creare un utente test di Voyance</span><span class="sxs-lookup"><span data-stu-id="a8be6-214">Create a Voyance test user</span></span>

<span data-ttu-id="a8be6-215">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Voyance toocreate.</span><span class="sxs-lookup"><span data-stu-id="a8be6-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="a8be6-216">Voyance supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a8be6-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="a8be6-217">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="a8be6-217">There is no action item for you in this section.</span></span> <span data-ttu-id="a8be6-218">Se non esiste ancora, durante un tooaccess tentativo Voyance viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="a8be6-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a8be6-219">Se è necessario un utente toocreate manualmente, è necessario toocontact [team di supporto Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="a8be6-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a8be6-220">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8be6-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a8be6-221">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooVoyance.</span><span class="sxs-lookup"><span data-stu-id="a8be6-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Assegnazione del ruolo utente hello][200]

<span data-ttu-id="a8be6-223">**tooassign Britta Simon tooVoyance, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a8be6-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8be6-224">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a8be6-226">Nell'elenco di applicazioni hello, selezionare **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-226">In hello applications list, select **Voyance**.</span></span>

    ![collegamento Voyance Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="a8be6-228">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="a8be6-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-230">Click **Add** button.</span></span> <span data-ttu-id="a8be6-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="a8be6-233">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a8be6-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a8be6-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8be6-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a8be6-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a8be6-236">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a8be6-236">Test single sign-on</span></span>

<span data-ttu-id="a8be6-237">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a8be6-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a8be6-238">Quando si fa clic su riquadro Voyance hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Voyance applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8be6-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8be6-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a8be6-239">Additional resources</span></span>

* [<span data-ttu-id="a8be6-240">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8be6-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8be6-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8be6-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png


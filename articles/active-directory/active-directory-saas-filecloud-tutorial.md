---
title: 'Esercitazione: Integrazione di Azure Active Directory con FileCloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FileCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="8b20f-103">Esercitazione: Integrazione di Azure Active Directory con FileCloud</span><span class="sxs-lookup"><span data-stu-id="8b20f-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="8b20f-104">In questa esercitazione, è illustrato come toointegrate FileCloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b20f-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b20f-105">Integrazione FileCloud con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8b20f-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8b20f-106">È possibile controllare in Azure AD che ha accesso tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="8b20f-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="8b20f-107">È possibile abilitare l'utenti tooautomatically get connesso tooFileCloud (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b20f-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8b20f-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b20f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8b20f-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b20f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b20f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b20f-110">Prerequisites</span></span>

<span data-ttu-id="8b20f-111">integrazione di Azure AD con FileCloud tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8b20f-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="8b20f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b20f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b20f-113">Sottoscrizione di FileCloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b20f-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b20f-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8b20f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b20f-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8b20f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b20f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8b20f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b20f-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b20f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b20f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8b20f-118">Scenario description</span></span>
<span data-ttu-id="8b20f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8b20f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b20f-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8b20f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b20f-121">Aggiunta di FileCloud dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8b20f-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="8b20f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b20f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="8b20f-123">Aggiunta di FileCloud dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8b20f-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="8b20f-124">integrazione hello tooconfigure di FileCloud in Azure AD, è necessario tooadd FileCloud dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8b20f-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b20f-125">**tooadd FileCloud dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b20f-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b20f-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8b20f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="8b20f-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b20f-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="8b20f-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8b20f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="8b20f-133">Nella casella di ricerca hello, digitare **FileCloud**selezionare **FileCloud** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8b20f-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8b20f-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b20f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8b20f-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FileCloud con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8b20f-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b20f-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FileCloud è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b20f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="8b20f-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FileCloud deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8b20f-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="8b20f-139">In FileCloud, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="8b20f-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8b20f-140">tooconfigure e prova AD Azure single sign-on con FileCloud, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8b20f-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b20f-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8b20f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b20f-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b20f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b20f-143">**[Creare un utente test FileCloud](#create-a-filecloud-test-user)**  -toohave un equivalente di Britta Simon in FileCloud che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8b20f-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b20f-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8b20f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b20f-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8b20f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8b20f-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b20f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8b20f-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8b20f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="8b20f-148">**Azure AD tooconfigure single sign-on con FileCloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b20f-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b20f-149">Nel portale di Azure su hello hello **FileCloud** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="8b20f-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8b20f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="8b20f-153">In hello **FileCloud dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b20f-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="8b20f-155">a.</span><span class="sxs-lookup"><span data-stu-id="8b20f-155">a.</span></span> <span data-ttu-id="8b20f-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="8b20f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="8b20f-157">b.</span><span class="sxs-lookup"><span data-stu-id="8b20f-157">b.</span></span> <span data-ttu-id="8b20f-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="8b20f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b20f-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8b20f-159">These values are not real.</span></span> <span data-ttu-id="8b20f-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="8b20f-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8b20f-161">Contatto [team di supporto FileCloud Client](mailto:support@codelathe.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="8b20f-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="8b20f-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8b20f-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="8b20f-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8b20f-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b20f-166">In hello **FileCloud configurazione** fare clic su **configurare FileCloud** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="8b20f-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8b20f-167">Hello copia **ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8b20f-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurazione di FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="8b20f-169">In una finestra del web browser, accesso tooyour FileCloud tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8b20f-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="8b20f-170">Nel riquadro di spostamento a sinistra di hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![Sezione Settings (Impostazioni) sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="8b20f-172">Fare clic sulla scheda **SSO** nella sezione Settings (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="8b20f-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Scheda SSO sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="8b20f-174">Impostare **SAML** come **Default SSO Type** (Tipo SSO predefinito) nel riquadro **Single Sign On (SSO) Settings** (Impostazioni Single Sign-On - SSO).</span><span class="sxs-lookup"><span data-stu-id="8b20f-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Pannello Single Sign-On Settings (Impostazioni Single Sign-On - SSO) sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="8b20f-176">Incolla **ID entità SAML**, che è stato copiato dal portale di Azure in hello **IdP endpoint URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8b20f-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![Casella di testo IdP End Point URL (URL entità IdP)](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="8b20f-178">Aprire il file di metadati scaricato nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **metadati IdP** nella casella di testo **impostazioni SAML** pannello.</span><span class="sxs-lookup"><span data-stu-id="8b20f-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Sezione IdP Meta Data (Metadati IdP) sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="8b20f-180">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8b20f-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="8b20f-181">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8b20f-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8b20f-182">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8b20f-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8b20f-183">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b20f-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8b20f-184">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b20f-184">Create an Azure AD test user</span></span>

<span data-ttu-id="8b20f-185">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8b20f-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="8b20f-187">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b20f-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b20f-188">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8b20f-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8b20f-190">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8b20f-192">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8b20f-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8b20f-194">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b20f-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8b20f-196">a.</span><span class="sxs-lookup"><span data-stu-id="8b20f-196">a.</span></span> <span data-ttu-id="8b20f-197">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b20f-198">b.</span><span class="sxs-lookup"><span data-stu-id="8b20f-198">b.</span></span> <span data-ttu-id="8b20f-199">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b20f-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8b20f-200">c.</span><span class="sxs-lookup"><span data-stu-id="8b20f-200">c.</span></span> <span data-ttu-id="8b20f-201">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="8b20f-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8b20f-202">d.</span><span class="sxs-lookup"><span data-stu-id="8b20f-202">d.</span></span> <span data-ttu-id="8b20f-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="8b20f-204">Creare un utente test di FileCloud</span><span class="sxs-lookup"><span data-stu-id="8b20f-204">Create a FileCloud test user</span></span>

<span data-ttu-id="8b20f-205">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in FileCloud toocreate.</span><span class="sxs-lookup"><span data-stu-id="8b20f-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="8b20f-206">FileCloud supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8b20f-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="8b20f-207">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="8b20f-207">There is no action item for you in this section.</span></span> <span data-ttu-id="8b20f-208">Se non esiste ancora, durante un tooaccess tentativo FileCloud viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="8b20f-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="8b20f-209">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto FileCloud Client](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="8b20f-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8b20f-210">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b20f-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8b20f-211">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="8b20f-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="8b20f-213">**tooassign Britta Simon tooFileCloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b20f-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b20f-214">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8b20f-216">Nell'elenco di applicazioni hello, selezionare **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-216">In hello applications list, select **FileCloud**.</span></span>

    ![collegamento FileCloud Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="8b20f-218">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="8b20f-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-220">Click **Add** button.</span></span> <span data-ttu-id="8b20f-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="8b20f-223">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8b20f-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8b20f-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b20f-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8b20f-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8b20f-226">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b20f-226">Test single sign-on</span></span>

<span data-ttu-id="8b20f-227">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8b20f-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8b20f-228">Quando si fa clic su riquadro FileCloud hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour FileCloud applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b20f-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b20f-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8b20f-229">Additional resources</span></span>

* [<span data-ttu-id="8b20f-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b20f-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b20f-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b20f-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png


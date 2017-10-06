---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zoho | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Zoho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="6f71c-103">Esercitazione: Integrazione di Azure Active Directory con Zoho</span><span class="sxs-lookup"><span data-stu-id="6f71c-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="6f71c-104">In questa esercitazione, è illustrato come toointegrate Zoho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f71c-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f71c-105">Integrazione di Zoho con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6f71c-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f71c-106">È possibile controllare in Azure AD che ha accesso tooZoho.</span><span class="sxs-lookup"><span data-stu-id="6f71c-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="6f71c-107">È possibile abilitare l'utenti tooautomatically get connesso tooZoho (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f71c-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6f71c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f71c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6f71c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f71c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f71c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f71c-110">Prerequisites</span></span>

<span data-ttu-id="6f71c-111">integrazione di Azure AD con Zoho tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6f71c-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="6f71c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f71c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f71c-113">Sottoscrizione di Zoho abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f71c-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f71c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6f71c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f71c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6f71c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f71c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6f71c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f71c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f71c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f71c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6f71c-118">Scenario description</span></span>
<span data-ttu-id="6f71c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6f71c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f71c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6f71c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f71c-121">Aggiunta di Zoho dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6f71c-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="6f71c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f71c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="6f71c-123">Aggiunta di Zoho dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6f71c-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="6f71c-124">integrazione hello tooconfigure di Zoho in Azure AD, è necessario tooadd Zoho dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6f71c-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f71c-125">**tooadd Zoho dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f71c-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f71c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6f71c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="6f71c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f71c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="6f71c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6f71c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="6f71c-133">Nella casella di ricerca hello, digitare **Zoho**selezionare **Zoho** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6f71c-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6f71c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f71c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6f71c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zoho usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f71c-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f71c-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zoho è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f71c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="6f71c-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Zoho deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6f71c-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="6f71c-139">In Zoho, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6f71c-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6f71c-140">tooconfigure e prova AD Azure single sign-on con Zoho, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6f71c-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f71c-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6f71c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f71c-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f71c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f71c-143">**[Creare un utente test Zoho](#create-a-zoho-test-user)**  -toohave un equivalente di Britta Simon in Zoho che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6f71c-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f71c-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6f71c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f71c-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6f71c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6f71c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f71c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6f71c-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Zoho.</span><span class="sxs-lookup"><span data-stu-id="6f71c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="6f71c-148">**Azure AD tooconfigure single sign-on con Zoho, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f71c-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f71c-149">Nel portale di Azure su hello hello **Zoho** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="6f71c-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6f71c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="6f71c-153">In hello **Zoho dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f71c-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="6f71c-155">a.</span><span class="sxs-lookup"><span data-stu-id="6f71c-155">a.</span></span> <span data-ttu-id="6f71c-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="6f71c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f71c-157">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="6f71c-157">This value is not real.</span></span> <span data-ttu-id="6f71c-158">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6f71c-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6f71c-159">Contatto [team di supporto Client di Zoho](https://www.zoho.com/mail/contact.html) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="6f71c-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="6f71c-160">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6f71c-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="6f71c-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6f71c-162">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f71c-164">In hello **Zoho configurazione** fare clic su **configurare Zoho** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="6f71c-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6f71c-165">Hello copia **URL Sign-Out e Modifica URL Password SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="6f71c-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="6f71c-167">In un'altra finestra del Web browser accedere al sito aziendale di Zoho Mail come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f71c-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="6f71c-168">Passare toohello **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="6f71c-169">![Pannello di controllo](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Pannello di controllo")</span><span class="sxs-lookup"><span data-stu-id="6f71c-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="6f71c-170">Fare clic su hello **SAML Authentication** scheda.</span><span class="sxs-lookup"><span data-stu-id="6f71c-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="6f71c-171">![Autenticazione SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="6f71c-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="6f71c-172">In hello **SAML Authentication Details** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f71c-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6f71c-173">![Dettagli dell'autenticazione SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Dettagli dell'autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="6f71c-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="6f71c-174">a.</span><span class="sxs-lookup"><span data-stu-id="6f71c-174">a.</span></span> <span data-ttu-id="6f71c-175">In hello **URL di accesso** casella di testo, incollare **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f71c-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6f71c-176">b.</span><span class="sxs-lookup"><span data-stu-id="6f71c-176">b.</span></span> <span data-ttu-id="6f71c-177">In hello **Logout URL** casella di testo, incollare **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f71c-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6f71c-178">c.</span><span class="sxs-lookup"><span data-stu-id="6f71c-178">c.</span></span> <span data-ttu-id="6f71c-179">In hello **Modifica URL Password** casella di testo, incollare **Modifica URL Password** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f71c-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="6f71c-180">d.</span><span class="sxs-lookup"><span data-stu-id="6f71c-180">d.</span></span> <span data-ttu-id="6f71c-181">Aprire il certificato con codifica base 64 scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **PublicKey** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="6f71c-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="6f71c-182">e.</span><span class="sxs-lookup"><span data-stu-id="6f71c-182">e.</span></span> <span data-ttu-id="6f71c-183">In **Algorithm** (Algoritmo) selezionare **RSA**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="6f71c-184">f.</span><span class="sxs-lookup"><span data-stu-id="6f71c-184">f.</span></span> <span data-ttu-id="6f71c-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="6f71c-186">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6f71c-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f71c-187">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6f71c-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f71c-188">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f71c-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6f71c-189">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f71c-189">Create an Azure AD test user</span></span>

<span data-ttu-id="6f71c-190">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6f71c-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="6f71c-192">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f71c-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f71c-193">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="6f71c-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6f71c-195">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6f71c-197">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6f71c-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6f71c-199">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f71c-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6f71c-201">a.</span><span class="sxs-lookup"><span data-stu-id="6f71c-201">a.</span></span> <span data-ttu-id="6f71c-202">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f71c-203">b.</span><span class="sxs-lookup"><span data-stu-id="6f71c-203">b.</span></span> <span data-ttu-id="6f71c-204">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f71c-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6f71c-205">c.</span><span class="sxs-lookup"><span data-stu-id="6f71c-205">c.</span></span> <span data-ttu-id="6f71c-206">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="6f71c-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6f71c-207">d.</span><span class="sxs-lookup"><span data-stu-id="6f71c-207">d.</span></span> <span data-ttu-id="6f71c-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="6f71c-209">Creare un utente di test di Zoho</span><span class="sxs-lookup"><span data-stu-id="6f71c-209">Create a Zoho test user</span></span>

<span data-ttu-id="6f71c-210">In ordine tooenable Azure AD utenti toolog a Zoho Mail, è necessario eseguirne il provisioning in Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="6f71c-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="6f71c-211">Nel caso di hello di Zoho Mail, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="6f71c-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="6f71c-212">È possibile usare qualsiasi altro Zoho Mail utente account strumento di creazione o qualsiasi API fornita da Zoho Mail tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="6f71c-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="6f71c-213">tooprovision un account utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f71c-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="6f71c-214">Accedi tooyour **Zoho Mail** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6f71c-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="6f71c-215">Andare troppo**Pannello di controllo \> posta elettronica e documenti**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="6f71c-216">Andare troppo**dettagli utente \> Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="6f71c-217">![Aggiungere un utente](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="6f71c-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="6f71c-218">In hello **aggiungere utenti** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6f71c-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="6f71c-219">![Aggiungere un utente](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="6f71c-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="6f71c-220">a.</span><span class="sxs-lookup"><span data-stu-id="6f71c-220">a.</span></span> <span data-ttu-id="6f71c-221">In hello **nome** casella Tipo hello nome dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="6f71c-222">b.</span><span class="sxs-lookup"><span data-stu-id="6f71c-222">b.</span></span> <span data-ttu-id="6f71c-223">In hello **cognome** casella di testo, digitare hello cognome dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="6f71c-224">c.</span><span class="sxs-lookup"><span data-stu-id="6f71c-224">c.</span></span> <span data-ttu-id="6f71c-225">In hello **ID di posta elettronica** casella di testo, id di tipo hello posta elettronica dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6f71c-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="6f71c-226">d.</span><span class="sxs-lookup"><span data-stu-id="6f71c-226">d.</span></span> <span data-ttu-id="6f71c-227">In hello **Password** casella di testo, immettere la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6f71c-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="6f71c-228">e.</span><span class="sxs-lookup"><span data-stu-id="6f71c-228">e.</span></span> <span data-ttu-id="6f71c-229">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="6f71c-230">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica con un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="6f71c-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6f71c-231">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f71c-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6f71c-232">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZoho.</span><span class="sxs-lookup"><span data-stu-id="6f71c-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="6f71c-234">**tooassign Britta Simon tooZoho, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f71c-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f71c-235">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6f71c-237">Nell'elenco di applicazioni hello, selezionare **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-237">In hello applications list, select **Zoho**.</span></span>

    ![collegamento di Zoho Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="6f71c-239">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="6f71c-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-241">Click **Add** button.</span></span> <span data-ttu-id="6f71c-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="6f71c-244">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6f71c-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f71c-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f71c-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f71c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6f71c-247">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f71c-247">Test single sign-on</span></span>

<span data-ttu-id="6f71c-248">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6f71c-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f71c-249">Quando si fa clic su riquadro Zoho hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Zoho applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f71c-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="6f71c-250">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f71c-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6f71c-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6f71c-251">Additional resources</span></span>

* [<span data-ttu-id="6f71c-252">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f71c-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f71c-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f71c-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png


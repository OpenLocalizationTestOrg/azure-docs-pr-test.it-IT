---
title: 'Esercitazione: Integrazione di Azure Active Directory con Freshservice | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Freshservice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="d5142-103">Esercitazione: Integrazione di Azure Active Directory con Freshservice</span><span class="sxs-lookup"><span data-stu-id="d5142-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="d5142-104">In questa esercitazione, è illustrato come toointegrate Freshservice con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5142-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5142-105">Integrazione di Freshservice con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d5142-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5142-106">È possibile controllare in Azure AD che ha accesso tooFreshservice</span><span class="sxs-lookup"><span data-stu-id="d5142-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="d5142-107">È possibile abilitare l'utenti tooautomatically get connesso tooFreshservice (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5142-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5142-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d5142-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d5142-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5142-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5142-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5142-110">Prerequisites</span></span>

<span data-ttu-id="d5142-111">integrazione di Azure AD con Freshservice tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d5142-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="d5142-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5142-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5142-113">Sottoscrizione di Freshservice abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d5142-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5142-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d5142-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d5142-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d5142-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5142-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d5142-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d5142-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5142-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5142-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d5142-118">Scenario description</span></span>
<span data-ttu-id="d5142-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d5142-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5142-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d5142-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5142-121">Aggiunta di Freshservice dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d5142-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="d5142-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5142-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="d5142-123">Aggiunta di Freshservice dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d5142-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="d5142-124">integrazione hello tooconfigure di Freshservice in Azure AD, è necessario tooadd Freshservice dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d5142-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5142-125">**tooadd Freshservice dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5142-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5142-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d5142-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5142-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d5142-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5142-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5142-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d5142-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d5142-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d5142-133">Nella casella di ricerca hello, digitare **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="d5142-133">In hello search box, type **Freshservice**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="d5142-135">Nel riquadro dei risultati hello, selezionare **Freshservice**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d5142-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5142-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5142-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5142-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Freshservice mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d5142-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5142-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Freshservice è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5142-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="d5142-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Freshservice richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d5142-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="d5142-141">In Freshservice, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="d5142-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d5142-142">tooconfigure e prova AD Azure single sign-on con Freshservice, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d5142-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5142-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d5142-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5142-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5142-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5142-145">**[Creazione di un utente test Freshservice](#creating-a-freshservice-test-user)**  -toohave un equivalente di Britta Simon in Freshservice che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d5142-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d5142-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5142-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5142-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5142-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5142-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5142-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5142-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Freshservice.</span><span class="sxs-lookup"><span data-stu-id="d5142-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="d5142-150">**Azure AD tooconfigure single sign-on con Freshservice, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5142-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5142-151">Nel portale di Azure su hello hello **Freshservice** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d5142-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d5142-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5142-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="d5142-155">In hello **Freshservice dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5142-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="d5142-157">a.</span><span class="sxs-lookup"><span data-stu-id="d5142-157">a.</span></span> <span data-ttu-id="d5142-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="d5142-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="d5142-159">b.</span><span class="sxs-lookup"><span data-stu-id="d5142-159">b.</span></span> <span data-ttu-id="d5142-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="d5142-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5142-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d5142-161">These values are not real.</span></span> <span data-ttu-id="d5142-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="d5142-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d5142-163">Contatto [team di supporto Client di Freshservice](https://support.freshservice.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="d5142-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="d5142-164">In hello **certificato di firma SAML** sezione, copiare **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="d5142-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="d5142-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d5142-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d5142-168">In hello **Freshservice configurazione** fare clic su **configurare Freshservice** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="d5142-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d5142-169">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d5142-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="d5142-171">In una finestra del web browser, accedere come amministratore nel sito della società Freshservice di tooyour.</span><span class="sxs-lookup"><span data-stu-id="d5142-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="d5142-172">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d5142-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="d5142-173">![Amministratore](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="d5142-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="d5142-174">In hello **portale per i clienti**, fare clic su **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="d5142-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="d5142-175">![Sicurezza](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="d5142-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="d5142-176">In hello **sicurezza** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5142-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d5142-177">![Single Sign-On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d5142-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="d5142-178">a.</span><span class="sxs-lookup"><span data-stu-id="d5142-178">a.</span></span> <span data-ttu-id="d5142-179">Passare a **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d5142-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="d5142-180">b.</span><span class="sxs-lookup"><span data-stu-id="d5142-180">b.</span></span> <span data-ttu-id="d5142-181">Selezionare **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="d5142-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="d5142-182">c.</span><span class="sxs-lookup"><span data-stu-id="d5142-182">c.</span></span> <span data-ttu-id="d5142-183">In hello **SAML Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5142-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d5142-184">d.</span><span class="sxs-lookup"><span data-stu-id="d5142-184">d.</span></span> <span data-ttu-id="d5142-185">In hello **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5142-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d5142-186">e.</span><span class="sxs-lookup"><span data-stu-id="d5142-186">e.</span></span> <span data-ttu-id="d5142-187">In **Security Certificate Fingerprint** casella di testo, incollare hello **identificazione personale** valore del certificato che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5142-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d5142-188">f.</span><span class="sxs-lookup"><span data-stu-id="d5142-188">f.</span></span> <span data-ttu-id="d5142-189">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="d5142-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="d5142-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d5142-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d5142-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d5142-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d5142-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5142-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5142-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5142-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5142-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d5142-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d5142-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5142-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5142-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d5142-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5142-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d5142-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5142-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d5142-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5142-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5142-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5142-205">a.</span><span class="sxs-lookup"><span data-stu-id="d5142-205">a.</span></span> <span data-ttu-id="d5142-206">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5142-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5142-207">b.</span><span class="sxs-lookup"><span data-stu-id="d5142-207">b.</span></span> <span data-ttu-id="d5142-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5142-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5142-209">c.</span><span class="sxs-lookup"><span data-stu-id="d5142-209">c.</span></span> <span data-ttu-id="d5142-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d5142-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5142-211">d.</span><span class="sxs-lookup"><span data-stu-id="d5142-211">d.</span></span> <span data-ttu-id="d5142-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d5142-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="d5142-213">Creazione di un utente test di Freshservice</span><span class="sxs-lookup"><span data-stu-id="d5142-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="d5142-214">toolog agli utenti di Azure AD tooenable in tooFreshService, è necessario eseguirne il provisioning in FreshService.</span><span class="sxs-lookup"><span data-stu-id="d5142-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="d5142-215">Nel caso di hello di FreshService, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d5142-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="d5142-216">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5142-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5142-217">Accedi tooyour **FreshService** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d5142-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="d5142-218">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d5142-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="d5142-219">![Amministratore](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="d5142-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="d5142-220">In hello **Gestione utenti** fare clic su **richiedenti**.</span><span class="sxs-lookup"><span data-stu-id="d5142-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="d5142-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span><span class="sxs-lookup"><span data-stu-id="d5142-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="d5142-222">Fare clic su **Nuovo Requester**.</span><span class="sxs-lookup"><span data-stu-id="d5142-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="d5142-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span><span class="sxs-lookup"><span data-stu-id="d5142-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="d5142-224">In hello **nuovo richiedente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5142-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d5142-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span><span class="sxs-lookup"><span data-stu-id="d5142-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="d5142-226">a.</span><span class="sxs-lookup"><span data-stu-id="d5142-226">a.</span></span> <span data-ttu-id="d5142-227">Immettere hello **nome** e **posta elettronica** gli attributi di un account Azure Active Directory valido, si desidera tooprovision in hello correlati nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="d5142-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="d5142-228">b.</span><span class="sxs-lookup"><span data-stu-id="d5142-228">b.</span></span> <span data-ttu-id="d5142-229">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d5142-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="d5142-230">titolare dell'account di Azure Active Directory Hello Ottiene un messaggio di posta elettronica tra un account di hello tooconfirm collegamento prima che diventi attivo</span><span class="sxs-lookup"><span data-stu-id="d5142-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="d5142-231">È possibile usare qualsiasi altro FreshService utente account strumento di creazione o le API fornite da FreshService tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="d5142-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Assegna utente][200] 

<span data-ttu-id="d5142-233">**tooassign Britta Simon tooFreshservice, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5142-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5142-234">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5142-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d5142-236">Nell'elenco di applicazioni hello, selezionare **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="d5142-236">In hello applications list, select **Freshservice**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="d5142-238">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d5142-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d5142-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d5142-240">Click **Add** button.</span></span> <span data-ttu-id="d5142-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d5142-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d5142-243">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d5142-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5142-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d5142-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5142-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d5142-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d5142-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d5142-246">Testing single sign-on</span></span>

<span data-ttu-id="d5142-247">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d5142-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d5142-248">Quando si fa clic su riquadro Freshservice hello in hello Pannello di accesso, è necessario ottenere applicazione Freshservice tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="d5142-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5142-249">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d5142-249">Additional resources</span></span>

* [<span data-ttu-id="d5142-250">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5142-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5142-251">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5142-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con QuickHelp | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e QuickHelp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="5d36d-103">Esercitazione: Integrazione di Azure Active Directory con QuickHelp</span><span class="sxs-lookup"><span data-stu-id="5d36d-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="5d36d-104">In questa esercitazione, è illustrato come toointegrate QuickHelp con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d36d-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d36d-105">Integrazione QuickHelp con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5d36d-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d36d-106">È possibile controllare in Azure AD che ha accesso tooQuickHelp</span><span class="sxs-lookup"><span data-stu-id="5d36d-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="5d36d-107">È possibile abilitare l'utenti tooautomatically get connesso tooQuickHelp (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d36d-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d36d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5d36d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5d36d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d36d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d36d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5d36d-110">Prerequisites</span></span>

<span data-ttu-id="5d36d-111">integrazione di Azure AD con QuickHelp tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5d36d-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="5d36d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d36d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d36d-113">Sottoscrizione di QuickHelp abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5d36d-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d36d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5d36d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d36d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5d36d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d36d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5d36d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d36d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d36d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d36d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5d36d-118">Scenario description</span></span>
<span data-ttu-id="5d36d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5d36d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d36d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5d36d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d36d-121">Aggiunta di QuickHelp dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5d36d-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="5d36d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d36d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="5d36d-123">Aggiunta di QuickHelp dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5d36d-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="5d36d-124">integrazione hello tooconfigure di QuickHelp in Azure AD, è necessario tooadd QuickHelp dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5d36d-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d36d-125">**tooadd QuickHelp dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d36d-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d36d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5d36d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d36d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d36d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5d36d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5d36d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5d36d-133">Nella casella di ricerca hello, digitare **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-133">In hello search box, type **QuickHelp**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="5d36d-135">Nel riquadro dei risultati hello, selezionare **QuickHelp**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5d36d-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d36d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d36d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d36d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con QuickHelp in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5d36d-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d36d-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in QuickHelp è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d36d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="5d36d-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in QuickHelp deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5d36d-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="5d36d-141">In QuickHelp, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5d36d-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d36d-142">tooconfigure e prova AD Azure single sign-on con QuickHelp, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5d36d-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d36d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5d36d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d36d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d36d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d36d-145">**[Creazione di un utente test QuickHelp](#creating-a-quickhelp-test-user)**  -toohave un equivalente di Britta Simon in QuickHelp che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5d36d-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d36d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5d36d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d36d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5d36d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d36d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d36d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d36d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="5d36d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="5d36d-150">**Azure AD tooconfigure single sign-on con QuickHelp, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d36d-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d36d-151">Nel portale di Azure su hello hello **QuickHelp** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5d36d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5d36d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="5d36d-155">In hello **QuickHelp dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5d36d-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="5d36d-157">a.</span><span class="sxs-lookup"><span data-stu-id="5d36d-157">a.</span></span> <span data-ttu-id="5d36d-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="5d36d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="5d36d-159">b.</span><span class="sxs-lookup"><span data-stu-id="5d36d-159">b.</span></span> <span data-ttu-id="5d36d-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="5d36d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d36d-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="5d36d-161">These values are not real.</span></span> <span data-ttu-id="5d36d-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="5d36d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5d36d-163">Contatto [team di supporto QuickHelp Client](https://support.quickhelp.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="5d36d-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="5d36d-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5d36d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="5d36d-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5d36d-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="5d36d-168">Sito dell'azienda QuickHelp tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5d36d-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="5d36d-169">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configura accesso Single Sign-On][21]

8. <span data-ttu-id="5d36d-171">In hello **QuickHelp Admin** menu, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configura accesso Single Sign-On][22]

9. <span data-ttu-id="5d36d-173">Fare clic su **Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="5d36d-174">In hello **le impostazioni di autenticazione** hello seguendo i passaggi da eseguire</span><span class="sxs-lookup"><span data-stu-id="5d36d-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![Configura accesso Single Sign-On][23]
   
    <span data-ttu-id="5d36d-176">a.</span><span class="sxs-lookup"><span data-stu-id="5d36d-176">a.</span></span> <span data-ttu-id="5d36d-177">Come **tipo SSO**, selezionare **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="5d36d-178">b.</span><span class="sxs-lookup"><span data-stu-id="5d36d-178">b.</span></span> <span data-ttu-id="5d36d-179">tooupload file di metadati di Azure scaricato, fare clic su **Sfoglia**, passare il file toohello, quindi fare clic su Fine **Upload Metadata**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="5d36d-180">c.</span><span class="sxs-lookup"><span data-stu-id="5d36d-180">c.</span></span> <span data-ttu-id="5d36d-181">In hello **posta elettronica** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="5d36d-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="5d36d-182">d.</span><span class="sxs-lookup"><span data-stu-id="5d36d-182">d.</span></span> <span data-ttu-id="5d36d-183">In hello **nome** casella `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="5d36d-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="5d36d-184">e.</span><span class="sxs-lookup"><span data-stu-id="5d36d-184">e.</span></span> <span data-ttu-id="5d36d-185">In hello **cognome** casella `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="5d36d-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="5d36d-186">f.</span><span class="sxs-lookup"><span data-stu-id="5d36d-186">f.</span></span> <span data-ttu-id="5d36d-187">In hello **barra delle azioni**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5d36d-188">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5d36d-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d36d-189">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5d36d-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d36d-190">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d36d-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d36d-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d36d-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d36d-192">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d36d-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5d36d-194">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d36d-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d36d-195">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5d36d-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d36d-197">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d36d-199">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5d36d-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d36d-201">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5d36d-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d36d-203">a.</span><span class="sxs-lookup"><span data-stu-id="5d36d-203">a.</span></span> <span data-ttu-id="5d36d-204">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d36d-205">b.</span><span class="sxs-lookup"><span data-stu-id="5d36d-205">b.</span></span> <span data-ttu-id="5d36d-206">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d36d-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d36d-207">c.</span><span class="sxs-lookup"><span data-stu-id="5d36d-207">c.</span></span> <span data-ttu-id="5d36d-208">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5d36d-209">d.</span><span class="sxs-lookup"><span data-stu-id="5d36d-209">d.</span></span> <span data-ttu-id="5d36d-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="5d36d-211">Creazione di un utente test di QuickHelp</span><span class="sxs-lookup"><span data-stu-id="5d36d-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="5d36d-212">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in QuickHelp toocreate.</span><span class="sxs-lookup"><span data-stu-id="5d36d-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="5d36d-213">Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello QuickHelp tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d36d-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="5d36d-214">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in QuickHelp deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5d36d-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="5d36d-215">QuickHelp supporta il provisioning just-in-time.</span><span class="sxs-lookup"><span data-stu-id="5d36d-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="5d36d-216">Ciò significa che, se necessario, viene automaticamente creato un account utente in QuickHelp e account hello è collegato toohello account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d36d-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="5d36d-217">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5d36d-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5d36d-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d36d-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5d36d-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooQuickHelp.</span><span class="sxs-lookup"><span data-stu-id="5d36d-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5d36d-221">**tooassign Britta Simon tooQuickHelp, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5d36d-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d36d-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5d36d-224">Nell'elenco di applicazioni hello, selezionare **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-224">In hello applications list, select **QuickHelp**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="5d36d-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5d36d-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-228">Click **Add** button.</span></span> <span data-ttu-id="5d36d-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5d36d-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5d36d-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d36d-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d36d-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5d36d-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d36d-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5d36d-234">Testing single sign-on</span></span>

<span data-ttu-id="5d36d-235">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5d36d-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5d36d-236">Quando si fa clic su riquadro QuickHelp hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour QuickHelp applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d36d-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5d36d-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5d36d-237">Additional resources</span></span>

* [<span data-ttu-id="5d36d-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d36d-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d36d-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d36d-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png

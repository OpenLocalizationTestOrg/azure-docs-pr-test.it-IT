---
title: 'Esercitazione: Integrazione di Azure Active Directory con Citrix GoToMeeting | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="d0997-103">Esercitazione: Integrazione di Azure Active Directory con Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="d0997-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="d0997-104">In questa esercitazione, è illustrato come toointegrate Citrix GoToMeeting con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0997-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0997-105">Integrazione di Citrix GoToMeeting con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d0997-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0997-106">È possibile controllare in Azure AD che ha accesso tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="d0997-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="d0997-107">È possibile abilitare l'utenti tooautomatically get connesso tooCitrix GoToMeeting (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0997-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0997-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d0997-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d0997-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0997-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0997-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d0997-110">Prerequisites</span></span>

<span data-ttu-id="d0997-111">tooconfigure integrazione di Azure AD con Citrix GoToMeeting, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d0997-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="d0997-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0997-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0997-113">Una sottoscrizione di Citrix GoToMeeting abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d0997-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0997-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d0997-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0997-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d0997-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0997-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d0997-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0997-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0997-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0997-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d0997-118">Scenario description</span></span>
<span data-ttu-id="d0997-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d0997-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0997-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d0997-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0997-121">Aggiunta di Citrix GoToMeeting dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d0997-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="d0997-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0997-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="d0997-123">Aggiunta di Citrix GoToMeeting dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d0997-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="d0997-124">integrazione hello tooconfigure di Citrix GoToMeeting in Azure AD, è necessario tooadd Citrix GoToMeeting dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d0997-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0997-125">**tooadd Citrix GoToMeeting dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0997-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0997-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d0997-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d0997-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d0997-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0997-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d0997-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d0997-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d0997-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d0997-133">Nella casella di ricerca hello, digitare **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="d0997-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="d0997-135">Nel riquadro dei risultati hello, selezionare **Citrix GoToMeeting**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d0997-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0997-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0997-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0997-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Citrix GoToMeeting in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d0997-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0997-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Citrix GoToMeeting è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0997-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="d0997-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Citrix GoToMeeting richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d0997-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="d0997-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d0997-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="d0997-142">tooconfigure e test Azure single sign-on AD con Citrix GoToMeeting, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d0997-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0997-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d0997-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d0997-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0997-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0997-145">**[Creazione di un utente test Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave un equivalente di Britta Simon in Citrix GoToMeeting che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d0997-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0997-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0997-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0997-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d0997-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0997-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0997-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0997-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d0997-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="d0997-150">**Azure AD tooconfigure single sign-on con Citrix GoToMeeting, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0997-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0997-151">Nel portale di Azure su hello hello **Citrix GoToMeeting** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d0997-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d0997-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0997-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="d0997-155">In hello **Citrix GoToMeeting dominio e gli URL** non sezione tooperform è necessario alcun passaggio.</span><span class="sxs-lookup"><span data-stu-id="d0997-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="d0997-157">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d0997-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="d0997-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d0997-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="d0997-161">Nella sezione di configurazione di Citrix GoToMeeting SAML hello, scegliere Configura sign-on finestra tooopen di configurare Citrix GoToMeeting SAML.</span><span class="sxs-lookup"><span data-stu-id="d0997-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="d0997-162">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d0997-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="d0997-163">In un'altra finestra del browser, accedere tooyour [Citrix organizzazione Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="d0997-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="d0997-164">Fare clic su hello **Provider di identità** scheda e quindi eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d0997-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="d0997-165">![Configurazione SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="d0997-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="d0997-166">a.</span><span class="sxs-lookup"><span data-stu-id="d0997-166">a.</span></span> <span data-ttu-id="d0997-167">Selezionare **Manual**</span><span class="sxs-lookup"><span data-stu-id="d0997-167">Select **Manual**</span></span>

    <span data-ttu-id="d0997-168">b.</span><span class="sxs-lookup"><span data-stu-id="d0997-168">b.</span></span> <span data-ttu-id="d0997-169">Nel portale di Azure su hello hello **Configura accesso single sign-on in Citrix GoToMeeting** nella pagina, hello copia **SAML Single Sign-On Service URL** valore e quindi incollarlo hello **nella pagina di accesso URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d0997-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="d0997-170">c.</span><span class="sxs-lookup"><span data-stu-id="d0997-170">c.</span></span> <span data-ttu-id="d0997-171">Nel portale di Azure su hello hello **Configura accesso single sign-on in Citrix GoToMeeting** nella pagina, hello copia **Sign-Out URL** valore e quindi incollarlo hello **URL pagina di disconnessione**casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d0997-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="d0997-172">d.</span><span class="sxs-lookup"><span data-stu-id="d0997-172">d.</span></span> <span data-ttu-id="d0997-173">Nel portale di Azure su hello hello **Configura accesso single sign-on in Citrix GoToMeeting** nella pagina, hello copia **ID entità SAML** valore e quindi incollarlo hello **Identity Provider Entity ID**  casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d0997-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="d0997-174">e.</span><span class="sxs-lookup"><span data-stu-id="d0997-174">e.</span></span> <span data-ttu-id="d0997-175">tooupload il certificato scaricato, fare clic su **carica certificato**.</span><span class="sxs-lookup"><span data-stu-id="d0997-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="d0997-176">f.</span><span class="sxs-lookup"><span data-stu-id="d0997-176">f.</span></span> <span data-ttu-id="d0997-177">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d0997-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d0997-178">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d0997-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d0997-179">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d0997-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0997-180">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0997-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0997-181">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0997-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0997-182">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d0997-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d0997-184">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0997-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0997-185">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d0997-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0997-187">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d0997-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0997-189">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d0997-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0997-191">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d0997-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0997-193">a.</span><span class="sxs-lookup"><span data-stu-id="d0997-193">a.</span></span> <span data-ttu-id="d0997-194">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0997-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0997-195">b.</span><span class="sxs-lookup"><span data-stu-id="d0997-195">b.</span></span> <span data-ttu-id="d0997-196">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0997-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0997-197">c.</span><span class="sxs-lookup"><span data-stu-id="d0997-197">c.</span></span> <span data-ttu-id="d0997-198">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d0997-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d0997-199">d.</span><span class="sxs-lookup"><span data-stu-id="d0997-199">d.</span></span> <span data-ttu-id="d0997-200">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d0997-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="d0997-201">Creazione di un utente test Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="d0997-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="d0997-202">In questa sezione viene creato un utente di nome Britta Simon in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d0997-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="d0997-203">Citrix GoToMeeting supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d0997-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="d0997-204">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d0997-204">There is no action item for you in this section.</span></span> <span data-ttu-id="d0997-205">Se un utente non esiste già in Citrix GoToMeeting, quando si tenta di Citrix GoToMeeting tooaccess uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="d0997-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="d0997-206">Se è necessario toocreate manualmente, contattare l'utente [team di supporto di Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="d0997-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d0997-207">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0997-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d0997-208">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="d0997-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d0997-210">**tooassign Britta Simon tooCitrix GoToMeeting, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0997-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0997-211">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d0997-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d0997-213">Nell'elenco di applicazioni hello, selezionare **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="d0997-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="d0997-215">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d0997-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d0997-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d0997-217">Click **Add** button.</span></span> <span data-ttu-id="d0997-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d0997-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d0997-220">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d0997-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0997-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d0997-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0997-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d0997-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0997-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d0997-223">Testing single sign-on</span></span>

<span data-ttu-id="d0997-224">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d0997-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d0997-225">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="d0997-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d0997-226">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0997-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0997-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d0997-227">Additional resources</span></span>

* [<span data-ttu-id="d0997-228">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0997-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0997-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0997-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d0997-230">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="d0997-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png


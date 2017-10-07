---
title: 'Esercitazione: Integrazione di Azure Active Directory con Promapp | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Promapp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="48ae4-103">Esercitazione: Integrazione di Azure Active Directory con Promapp</span><span class="sxs-lookup"><span data-stu-id="48ae4-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="48ae4-104">In questa esercitazione, è illustrato come toointegrate Promapp con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48ae4-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48ae4-105">Integrazione Promapp con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="48ae4-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="48ae4-106">È possibile controllare in Azure AD che ha accesso tooPromapp</span><span class="sxs-lookup"><span data-stu-id="48ae4-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="48ae4-107">È possibile abilitare l'utenti tooautomatically get connesso tooPromapp (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ae4-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48ae4-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="48ae4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="48ae4-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48ae4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48ae4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="48ae4-110">Prerequisites</span></span>

<span data-ttu-id="48ae4-111">integrazione di Azure AD con Promapp tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="48ae4-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="48ae4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48ae4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48ae4-113">Sottoscrizione di Promapp abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="48ae4-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48ae4-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="48ae4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48ae4-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="48ae4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48ae4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="48ae4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48ae4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48ae4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48ae4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="48ae4-118">Scenario description</span></span>
<span data-ttu-id="48ae4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="48ae4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48ae4-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="48ae4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48ae4-121">Aggiunta di Promapp dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="48ae4-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="48ae4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ae4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="48ae4-123">Aggiunta di Promapp dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="48ae4-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="48ae4-124">integrazione hello tooconfigure di Promapp in Azure AD, è necessario tooadd Promapp dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="48ae4-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="48ae4-125">**tooadd Promapp dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48ae4-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ae4-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="48ae4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48ae4-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="48ae4-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="48ae4-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="48ae4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="48ae4-133">Nella casella di ricerca hello, digitare **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-133">In hello search box, type **Promapp**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="48ae4-135">Nel riquadro dei risultati hello, selezionare **Promapp**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="48ae4-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48ae4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ae4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48ae4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Promapp in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48ae4-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48ae4-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Promapp è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48ae4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="48ae4-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Promapp deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="48ae4-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="48ae4-141">In Promapp, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="48ae4-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="48ae4-142">tooconfigure e prova AD Azure single sign-on con Promapp, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="48ae4-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="48ae4-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="48ae4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="48ae4-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48ae4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48ae4-145">**[Creazione di un utente test Promapp](#creating-a-promapp-test-user)**  -toohave un equivalente di Britta Simon in Promapp che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="48ae4-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="48ae4-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48ae4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48ae4-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="48ae4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48ae4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ae4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48ae4-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Promapp.</span><span class="sxs-lookup"><span data-stu-id="48ae4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="48ae4-150">**Azure AD tooconfigure single sign-on con Promapp, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48ae4-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ae4-151">Nel portale di Azure su hello hello **Promapp** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="48ae4-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48ae4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="48ae4-155">In hello **Promapp dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="48ae4-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="48ae4-157">a.</span><span class="sxs-lookup"><span data-stu-id="48ae4-157">a.</span></span> <span data-ttu-id="48ae4-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="48ae4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="48ae4-159">b.</span><span class="sxs-lookup"><span data-stu-id="48ae4-159">b.</span></span> <span data-ttu-id="48ae4-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="48ae4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48ae4-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="48ae4-161">These values are not real.</span></span> <span data-ttu-id="48ae4-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="48ae4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="48ae4-163">Contatto [team di supporto Promapp Client](https://www.promapp.com/about-us/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="48ae4-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="48ae4-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="48ae4-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="48ae4-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="48ae4-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48ae4-168">In hello **Promapp configurazione** fare clic su **configurare Promapp** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="48ae4-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="48ae4-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="48ae4-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="48ae4-171">Sito dell'azienda Promapp tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="48ae4-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="48ae4-172">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][12]

9. <span data-ttu-id="48ae4-174">Fare clic su **Configure**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-174">Click **Configure**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][13]

10. <span data-ttu-id="48ae4-176">In hello **sicurezza** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="48ae4-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][14]
    
    <span data-ttu-id="48ae4-178">a.</span><span class="sxs-lookup"><span data-stu-id="48ae4-178">a.</span></span> <span data-ttu-id="48ae4-179">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **SSO Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="48ae4-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="48ae4-180">b.</span><span class="sxs-lookup"><span data-stu-id="48ae4-180">b.</span></span> <span data-ttu-id="48ae4-181">Per **SSO - Single Sign-on Mode** selezionare **Optional** e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="48ae4-182">c.</span><span class="sxs-lookup"><span data-stu-id="48ae4-182">c.</span></span> <span data-ttu-id="48ae4-183">Aprire hello scaricato certificato nel blocco note, copiare hello certificato contenuto senza hello prima riga (---BEGIN CERTIFICATE---) e ultima riga di hello (---fine certificato---), incollarlo hello **certificato x. 509 di SSO** casella di testo, quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="48ae4-184">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="48ae4-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="48ae4-185">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="48ae4-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="48ae4-186">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48ae4-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48ae4-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ae4-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="48ae4-188">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="48ae4-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="48ae4-190">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48ae4-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ae4-191">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="48ae4-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48ae4-193">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48ae4-195">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="48ae4-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48ae4-197">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="48ae4-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48ae4-199">a.</span><span class="sxs-lookup"><span data-stu-id="48ae4-199">a.</span></span> <span data-ttu-id="48ae4-200">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48ae4-201">b.</span><span class="sxs-lookup"><span data-stu-id="48ae4-201">b.</span></span> <span data-ttu-id="48ae4-202">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48ae4-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48ae4-203">c.</span><span class="sxs-lookup"><span data-stu-id="48ae4-203">c.</span></span> <span data-ttu-id="48ae4-204">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="48ae4-205">d.</span><span class="sxs-lookup"><span data-stu-id="48ae4-205">d.</span></span> <span data-ttu-id="48ae4-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="48ae4-207">Creazione di un utente test per Promapp</span><span class="sxs-lookup"><span data-stu-id="48ae4-207">Creating a Promapp test user</span></span>

<span data-ttu-id="48ae4-208">Hello Promapp applicazione supporta Just-in-Time di provisioning.</span><span class="sxs-lookup"><span data-stu-id="48ae4-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="48ae4-209">In questo campo, un account utente viene creato automaticamente se necessario durante un'applicazione di hello tooaccess tentativo utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="48ae4-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="48ae4-210">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ae4-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="48ae4-211">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPromapp.</span><span class="sxs-lookup"><span data-stu-id="48ae4-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![Assegna utente][200] 

<span data-ttu-id="48ae4-213">**tooassign Britta Simon tooPromapp, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48ae4-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ae4-214">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="48ae4-216">Nell'elenco di applicazioni hello, selezionare **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-216">In hello applications list, select **Promapp**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="48ae4-218">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="48ae4-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-220">Click **Add** button.</span></span> <span data-ttu-id="48ae4-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="48ae4-223">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="48ae4-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="48ae4-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48ae4-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="48ae4-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48ae4-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="48ae4-226">Testing single sign-on</span></span>

<span data-ttu-id="48ae4-227">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="48ae4-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="48ae4-228">Quando si fa clic su riquadro Promapp hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Promapp applicazione.</span><span class="sxs-lookup"><span data-stu-id="48ae4-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48ae4-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="48ae4-229">Additional resources</span></span>

* [<span data-ttu-id="48ae4-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48ae4-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48ae4-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48ae4-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png


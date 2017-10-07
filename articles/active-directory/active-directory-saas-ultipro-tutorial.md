---
title: 'Esercitazione: Integrazione di Azure Active Directory con UltiPro | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e UltiPro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 8cb613228893e8cbf997957452d55d0ab7939171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="5ad4b-103">Esercitazione: Integrazione di Azure Active Directory con UltiPro</span><span class="sxs-lookup"><span data-stu-id="5ad4b-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="5ad4b-104">In questa esercitazione, è illustrato come toointegrate UltiPro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ad4b-104">In this tutorial, you learn how toointegrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ad4b-105">Integrazione UltiPro con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-105">Integrating UltiPro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ad4b-106">È possibile controllare in Azure AD che ha accesso tooUltiPro</span><span class="sxs-lookup"><span data-stu-id="5ad4b-106">You can control in Azure AD who has access tooUltiPro</span></span>
- <span data-ttu-id="5ad4b-107">È possibile abilitare l'utenti tooautomatically get connesso tooUltiPro (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ad4b-107">You can enable your users tooautomatically get signed-on tooUltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ad4b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5ad4b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5ad4b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ad4b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ad4b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ad4b-110">Prerequisites</span></span>

<span data-ttu-id="5ad4b-111">integrazione di Azure AD con UltiPro tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-111">tooconfigure Azure AD integration with UltiPro, you need hello following items:</span></span>

- <span data-ttu-id="5ad4b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ad4b-113">Sottoscrizione di UltiPro abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5ad4b-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ad4b-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ad4b-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ad4b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ad4b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ad4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ad4b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5ad4b-118">Scenario description</span></span>
<span data-ttu-id="5ad4b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ad4b-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ad4b-121">Aggiunta di UltiPro dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5ad4b-121">Adding UltiPro from hello gallery</span></span>
2. <span data-ttu-id="5ad4b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ad4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-hello-gallery"></a><span data-ttu-id="5ad4b-123">Aggiunta di UltiPro dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5ad4b-123">Adding UltiPro from hello gallery</span></span>
<span data-ttu-id="5ad4b-124">integrazione hello tooconfigure di UltiPro in Azure AD, è necessario tooadd UltiPro dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-124">tooconfigure hello integration of UltiPro into Azure AD, you need tooadd UltiPro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ad4b-125">**tooadd UltiPro dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ad4b-125">**tooadd UltiPro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ad4b-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ad4b-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ad4b-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5ad4b-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5ad4b-133">Nella casella di ricerca hello, digitare **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-133">In hello search box, type **UltiPro**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="5ad4b-135">Nel riquadro dei risultati hello, selezionare **UltiPro**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-135">In hello results panel, select **UltiPro**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ad4b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ad4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ad4b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UltiPro con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5ad4b-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ad4b-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in UltiPro è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UltiPro is tooa user in Azure AD.</span></span> <span data-ttu-id="5ad4b-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in UltiPro deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-140">In other words, a link relationship between an Azure AD user and hello related user in UltiPro needs toobe established.</span></span>

<span data-ttu-id="5ad4b-141">In UltiPro, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-141">In UltiPro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5ad4b-142">tooconfigure e prova AD Azure single sign-on con UltiPro, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-142">tooconfigure and test Azure AD single sign-on with UltiPro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ad4b-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ad4b-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ad4b-145">**[Creazione di un utente test UltiPro](#creating-a-ultipro-test-user)**  -toohave un equivalente di Britta Simon in UltiPro che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - toohave a counterpart of Britta Simon in UltiPro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ad4b-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ad4b-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ad4b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ad4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ad4b-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione UltiPro.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="5ad4b-150">**Azure AD tooconfigure single sign-on con UltiPro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ad4b-150">**tooconfigure Azure AD single sign-on with UltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ad4b-151">Nel portale di Azure su hello hello **UltiPro** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-151">In hello Azure portal, on hello **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5ad4b-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="5ad4b-155">In hello **UltiPro dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-155">On hello **UltiPro Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="5ad4b-157">a.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-157">a.</span></span> <span data-ttu-id="5ad4b-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="5ad4b-159">b.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-159">b.</span></span> <span data-ttu-id="5ad4b-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="5ad4b-161">c.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-161">c.</span></span> <span data-ttu-id="5ad4b-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="5ad4b-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="5ad4b-163">These values are not real.</span></span> <span data-ttu-id="5ad4b-164">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5ad4b-165">Contatto [team di supporto UltiPro Client](https://www.ultimatesoftware.com/ContactUs) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) tooget these values.</span></span> 

5. <span data-ttu-id="5ad4b-166">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="5ad4b-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5ad4b-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="5ad4b-170">In hello **UltiPro configurazione** fare clic su **configurare UltiPro** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-170">On hello **UltiPro Configuration** section, click **Configure UltiPro** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5ad4b-171">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5ad4b-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="5ad4b-173">tooconfigure single sign-on sul **UltiPro** lato, è necessario hello toosend scaricato **Certificate(Base64), Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** troppo[UltiPro team di supporto](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="5ad4b-173">tooconfigure single sign-on on **UltiPro** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="5ad4b-174">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5ad4b-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5ad4b-175">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5ad4b-176">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ad4b-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ad4b-177">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ad4b-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ad4b-178">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5ad4b-180">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ad4b-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ad4b-181">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ad4b-183">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ad4b-185">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ad4b-187">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ad4b-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ad4b-189">a.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-189">a.</span></span> <span data-ttu-id="5ad4b-190">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ad4b-191">b.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-191">b.</span></span> <span data-ttu-id="5ad4b-192">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ad4b-193">c.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-193">c.</span></span> <span data-ttu-id="5ad4b-194">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ad4b-195">d.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-195">d.</span></span> <span data-ttu-id="5ad4b-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="5ad4b-197">Creazione di un utente test di UltiPro</span><span class="sxs-lookup"><span data-stu-id="5ad4b-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="5ad4b-198">In questa sezione viene creato un utente di nome Britta Simon in UltiPro.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="5ad4b-199">Lavorare con [team di supporto UltiPro](https://www.ultimatesoftware.com/ContactUs) per aggiungere gli utenti di hello nella piattaforma UltiPro hello.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add hello users in hello UltiPro platform.</span></span> <span data-ttu-id="5ad4b-200">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5ad4b-201">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ad4b-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5ad4b-202">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooUltiPro.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUltiPro.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5ad4b-204">**tooassign Britta Simon tooUltiPro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5ad4b-204">**tooassign Britta Simon tooUltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ad4b-205">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5ad4b-207">Nell'elenco di applicazioni hello, selezionare **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-207">In hello applications list, select **UltiPro**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="5ad4b-209">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5ad4b-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-211">Click **Add** button.</span></span> <span data-ttu-id="5ad4b-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5ad4b-214">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ad4b-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ad4b-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ad4b-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5ad4b-217">Testing single sign-on</span></span>

<span data-ttu-id="5ad4b-218">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="5ad4b-219">Quando si fa clic su riquadro UltiPro hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour UltiPro applicazione.</span><span class="sxs-lookup"><span data-stu-id="5ad4b-219">When you click hello UltiPro tile in hello Access Panel, you should get automatically signed-on tooyour UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ad4b-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5ad4b-220">Additional resources</span></span>

* [<span data-ttu-id="5ad4b-221">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ad4b-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ad4b-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ad4b-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png


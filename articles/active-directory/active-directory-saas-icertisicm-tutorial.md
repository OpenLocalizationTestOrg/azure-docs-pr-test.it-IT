---
title: 'Esercitazione: Integrazione di Azure Active Directory con Icertis Contract Management Platform | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e piattaforma di gestione di Icertis contratto.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 6eb99553ef9df732512a38fb0489e66b41ba94a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="73ae3-103">Esercitazione: Integrazione di Azure Active Directory con Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="73ae3-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="73ae3-104">In questa esercitazione, è illustrato come toointegrate Icertis contratto di piattaforma di gestione con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73ae3-104">In this tutorial, you learn how toointegrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73ae3-105">Integrazione di piattaforma di gestione di contratto Icertis con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="73ae3-105">Integrating Icertis Contract Management Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73ae3-106">È possibile controllare in Azure AD che ha accesso tooIcertis contratto piattaforma di gestione</span><span class="sxs-lookup"><span data-stu-id="73ae3-106">You can control in Azure AD who has access tooIcertis Contract Management Platform</span></span>
- <span data-ttu-id="73ae3-107">È possibile abilitare l'utenti tooautomatically get connesso tooIcertis piattaforma di gestione dei contratti (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="73ae3-107">You can enable your users tooautomatically get signed-on tooIcertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73ae3-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="73ae3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73ae3-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73ae3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73ae3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73ae3-110">Prerequisites</span></span>

<span data-ttu-id="73ae3-111">integrazione di Azure AD con la piattaforma di gestione di contratto Icertis tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="73ae3-111">tooconfigure Azure AD integration with Icertis Contract Management Platform, you need hello following items:</span></span>

- <span data-ttu-id="73ae3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73ae3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73ae3-113">Sottoscrizione di Icertis Contract Management Platform abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="73ae3-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73ae3-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="73ae3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73ae3-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="73ae3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73ae3-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="73ae3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73ae3-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73ae3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73ae3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="73ae3-118">Scenario description</span></span>
<span data-ttu-id="73ae3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="73ae3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73ae3-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="73ae3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73ae3-121">Aggiunta di piattaforma di gestione di contratto Icertis dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="73ae3-121">Adding Icertis Contract Management Platform from hello gallery</span></span>
2. <span data-ttu-id="73ae3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="73ae3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-hello-gallery"></a><span data-ttu-id="73ae3-123">Aggiunta di piattaforma di gestione di contratto Icertis dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="73ae3-123">Adding Icertis Contract Management Platform from hello gallery</span></span>
<span data-ttu-id="73ae3-124">integrazione hello tooconfigure di piattaforma di gestione di contratto Icertis in Azure AD, è necessario tooadd Icertis contratto piattaforma di gestione dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="73ae3-124">tooconfigure hello integration of Icertis Contract Management Platform into Azure AD, you need tooadd Icertis Contract Management Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73ae3-125">**tooadd Icertis contratto di piattaforma di gestione dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="73ae3-125">**tooadd Icertis Contract Management Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73ae3-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="73ae3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73ae3-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73ae3-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="73ae3-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="73ae3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="73ae3-133">Nella casella di ricerca hello, digitare **piattaforma di gestione di contratto Icertis**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-133">In hello search box, type **Icertis Contract Management Platform**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="73ae3-135">Nel riquadro dei risultati hello, selezionare **piattaforma di gestione di contratto Icertis**e quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="73ae3-135">In hello results panel, select **Icertis Contract Management Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73ae3-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="73ae3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73ae3-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Icertis Contract Management Platform mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="73ae3-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73ae3-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nella piattaforma di gestione di contratto Icertis è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73ae3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Icertis Contract Management Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="73ae3-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nella piattaforma di gestione Icertis contratto richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="73ae3-140">In other words, a link relationship between an Azure AD user and hello related user in Icertis Contract Management Platform needs toobe established.</span></span>

<span data-ttu-id="73ae3-141">Nella piattaforma di gestione di contratto Icertis, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="73ae3-141">In Icertis Contract Management Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73ae3-142">tooconfigure e prova AD Azure single sign-on con Icertis contratto piattaforma di gestione, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="73ae3-142">tooconfigure and test Azure AD single sign-on with Icertis Contract Management Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73ae3-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="73ae3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73ae3-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73ae3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73ae3-145">**[Creazione di un utente di test della piattaforma di gestione di contratto Icertis](#creating-an-icertis-contract-management-platform-test-user)**  -toohave un equivalente di Britta Simon nella piattaforma di gestione di contratto Icertis che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="73ae3-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - toohave a counterpart of Britta Simon in Icertis Contract Management Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73ae3-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73ae3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73ae3-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="73ae3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73ae3-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="73ae3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73ae3-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Icertis contratto piattaforma di gestione.</span><span class="sxs-lookup"><span data-stu-id="73ae3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="73ae3-150">**tooconfigure AD Azure single sign-on con la piattaforma di gestione di contratto Icertis, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="73ae3-150">**tooconfigure Azure AD single sign-on with Icertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="73ae3-151">Nel portale di Azure su hello hello **piattaforma di gestione di contratto Icertis** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-151">In hello Azure portal, on hello **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="73ae3-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="73ae3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="73ae3-155">In hello **Icertis contratto gestione della piattaforma dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="73ae3-155">On hello **Icertis Contract Management Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="73ae3-157">a.</span><span class="sxs-lookup"><span data-stu-id="73ae3-157">a.</span></span> <span data-ttu-id="73ae3-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="73ae3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="73ae3-159">b.</span><span class="sxs-lookup"><span data-stu-id="73ae3-159">b.</span></span> <span data-ttu-id="73ae3-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="73ae3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73ae3-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="73ae3-161">These values are not real.</span></span> <span data-ttu-id="73ae3-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="73ae3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="73ae3-163">Contatto [team di supporto Client per la piattaforma gestione Icertis contratto](https://www.icertis.com/company/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="73ae3-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="73ae3-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="73ae3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="73ae3-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="73ae3-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73ae3-168">In hello **configurazione della piattaforma di gestione contratto Icertis** fare clic su **configurare piattaforma di gestione dei contratti Icertis** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="73ae3-168">On hello **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73ae3-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="73ae3-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="73ae3-171">tooconfigure single sign-on sul **piattaforma di gestione di contratto Icertis** lato, è necessario hello toosend scaricato **Metadata XML** e **Sign-Out URL ID entità SAML e SAML Single Sign-On URL del servizio** troppo[team di supporto della piattaforma di gestione contratto Icertis](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="73ae3-171">tooconfigure single sign-on on **Icertis Contract Management Platform** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="73ae3-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="73ae3-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73ae3-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="73ae3-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73ae3-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73ae3-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73ae3-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="73ae3-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="73ae3-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="73ae3-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="73ae3-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="73ae3-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73ae3-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="73ae3-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73ae3-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73ae3-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="73ae3-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73ae3-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="73ae3-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73ae3-187">a.</span><span class="sxs-lookup"><span data-stu-id="73ae3-187">a.</span></span> <span data-ttu-id="73ae3-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73ae3-189">b.</span><span class="sxs-lookup"><span data-stu-id="73ae3-189">b.</span></span> <span data-ttu-id="73ae3-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="73ae3-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73ae3-191">c.</span><span class="sxs-lookup"><span data-stu-id="73ae3-191">c.</span></span> <span data-ttu-id="73ae3-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73ae3-193">d.</span><span class="sxs-lookup"><span data-stu-id="73ae3-193">d.</span></span> <span data-ttu-id="73ae3-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="73ae3-195">Creazione di un utente test di Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="73ae3-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="73ae3-196">In questa sezione viene creato un utente chiamato Britta Simon in Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="73ae3-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="73ae3-197">Rivolgersi [team di supporto della piattaforma di gestione contratto Icertis](https://www.icertis.com/company/contact/) tooadd utenti hello hello Icertis piattaforma di gestione di contratto.</span><span class="sxs-lookup"><span data-stu-id="73ae3-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) tooadd hello users in hello Icertis Contract Management Platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73ae3-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="73ae3-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73ae3-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIcertis piattaforma di gestione di contratto.</span><span class="sxs-lookup"><span data-stu-id="73ae3-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIcertis Contract Management Platform.</span></span>

![Assegna utente][200] 

<span data-ttu-id="73ae3-201">**tooassign Britta Simon tooIcertis contratto piattaforma di gestione, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="73ae3-201">**tooassign Britta Simon tooIcertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="73ae3-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="73ae3-204">Nell'elenco di applicazioni hello, selezionare **piattaforma di gestione di contratto Icertis**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-204">In hello applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="73ae3-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="73ae3-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-208">Click **Add** button.</span></span> <span data-ttu-id="73ae3-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="73ae3-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="73ae3-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73ae3-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73ae3-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="73ae3-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73ae3-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="73ae3-214">Testing single sign-on</span></span>

<span data-ttu-id="73ae3-215">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="73ae3-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="73ae3-216">Quando si fa clic su riquadro di piattaforma di gestione di contratto Icertis hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Icertis piattaforma di gestione di contratto.</span><span class="sxs-lookup"><span data-stu-id="73ae3-216">When you click hello Icertis Contract Management Platform tile in hello Access Panel, you should get automatically signed-on tooyour Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73ae3-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="73ae3-217">Additional resources</span></span>

* [<span data-ttu-id="73ae3-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73ae3-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73ae3-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73ae3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png


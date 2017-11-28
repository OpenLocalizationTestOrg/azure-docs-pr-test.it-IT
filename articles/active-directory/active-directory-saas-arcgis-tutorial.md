---
title: 'Esercitazione: Integrazione di Azure Active Directory con ArcGIS Online | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ArcGIS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="5c4bf-103">Esercitazione: Integrazione di Azure Active Directory con ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="5c4bf-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="5c4bf-104">In questa esercitazione, è illustrato come toointegrate ArcGIS Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c4bf-105">Integrazione ArcGIS Online con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c4bf-106">È possibile controllare in Azure AD che ha accesso tooArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="5c4bf-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="5c4bf-107">È possibile abilitare l'utenti tooautomatically get connesso tooArcGIS Online (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c4bf-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c4bf-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5c4bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c4bf-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="5c4bf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5c4bf-110">Prerequisites</span></span>

<span data-ttu-id="5c4bf-111">tooconfigure integrazione di Azure AD con ArcGIS Online, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="5c4bf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c4bf-113">Sottoscrizione di ArcGIS Online abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5c4bf-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c4bf-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c4bf-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c4bf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c4bf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c4bf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5c4bf-118">Scenario description</span></span>
<span data-ttu-id="5c4bf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c4bf-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c4bf-121">Aggiunta di ArcGIS Online dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5c4bf-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="5c4bf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c4bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="5c4bf-123">Aggiunta di ArcGIS Online dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5c4bf-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="5c4bf-124">integrazione hello tooconfigure di ArcGIS Online in Azure AD, è necessario tooadd ArcGIS Online dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c4bf-125">**tooadd ArcGIS Online dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5c4bf-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c4bf-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c4bf-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c4bf-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5c4bf-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello di hello finestra di dialogo tooadd nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5c4bf-133">Nella casella di ricerca hello, digitare **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="5c4bf-135">Nel riquadro dei risultati hello, selezionare **ArcGIS Online**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c4bf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c4bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c4bf-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ArcGIS Online usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5c4bf-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c4bf-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ArcGIS Online è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="5c4bf-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ArcGIS Online richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="5c4bf-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="5c4bf-142">tooconfigure e prova AD Azure single sign-on con ArcGIS Online, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c4bf-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c4bf-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c4bf-145">**[Creazione di un utente test Online ArcGIS](#creating-an-arcgis-online-test-user)**  -toohave un equivalente di Britta Simon in ArcGIS Online è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c4bf-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c4bf-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c4bf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c4bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c4bf-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="5c4bf-150">**Azure AD tooconfigure single sign-on con ArcGIS Online, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5c4bf-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c4bf-151">Nel portale di Azure su hello hello **ArcGIS Online** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5c4bf-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="5c4bf-155">In hello **ArcGIS Online dominio e gli URL** seguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="5c4bf-157">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="5c4bf-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c4bf-158">Questo valore non è hello reale.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-158">This value is not hello real.</span></span> <span data-ttu-id="5c4bf-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5c4bf-160">Contatto [team di supporto di Client Online ArcGIS](http://support.esri.com/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="5c4bf-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="5c4bf-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5c4bf-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c4bf-165">In un'altra finestra del Web browser accedere al sito aziendale di ArcGIS come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="5c4bf-166">Fare clic su **EDIT SETTINGS** (Modifica impostazioni).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="5c4bf-167">![Modificare le impostazioni](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Modificare le impostazioni")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="5c4bf-168">Fare clic su **Security**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-168">Click **Security**.</span></span>

    <span data-ttu-id="5c4bf-169">![Sicurezza](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="5c4bf-170">In **Enterprise Logins** (Accessi aziendali) fare clic su **SET IDENTITY PROVIDER** (Imposta provider di identità).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="5c4bf-171">![Accessi aziendali](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Accessi aziendali")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="5c4bf-172">In hello **Set Identity Provider** configurazione eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5c4bf-173">![Impostare il provider di identità](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Impostare il provider di identità")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="5c4bf-174">a.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-174">a.</span></span> <span data-ttu-id="5c4bf-175">In hello **nome** casella di testo, digitare il nome dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="5c4bf-176">b.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-176">b.</span></span> <span data-ttu-id="5c4bf-177">Per **verranno specificati i metadati per il Provider di identità Enterprise hello utilizzando**selezionare **A File**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="5c4bf-178">c.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-178">c.</span></span> <span data-ttu-id="5c4bf-179">tooupload file di metadati scaricato, fare clic su **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="5c4bf-180">d.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-180">d.</span></span> <span data-ttu-id="5c4bf-181">Fare clic su **SET IDENTITY PROVIDER** (Imposta provider di identità).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="5c4bf-182">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5c4bf-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c4bf-183">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c4bf-184">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c4bf-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c4bf-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c4bf-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c4bf-186">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5c4bf-188">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5c4bf-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c4bf-189">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c4bf-191">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c4bf-193">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c4bf-195">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c4bf-197">a.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-197">a.</span></span> <span data-ttu-id="5c4bf-198">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c4bf-199">b.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-199">b.</span></span> <span data-ttu-id="5c4bf-200">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="5c4bf-201">c.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-201">c.</span></span> <span data-ttu-id="5c4bf-202">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c4bf-203">d.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-203">d.</span></span> <span data-ttu-id="5c4bf-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="5c4bf-205">Creazione di un utente di test di ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="5c4bf-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="5c4bf-206">In ordine tooenable Azure AD utenti toolog in ArcGIS Online, è necessario eseguirne il provisioning in ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="5c4bf-207">Nel caso di hello di ArcGIS Online, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="5c4bf-208">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5c4bf-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c4bf-209">Accedi tooyour **ArcGIS** tenant.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="5c4bf-210">Fare clic su **INVITE MEMBERS** (Invita membri).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="5c4bf-211">![Invitare i membri](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invitare i membri")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="5c4bf-212">Selezionare **Add members automatically without sending an email** (Aggiungi membri automaticamente senza inviare un'e-mail) e quindi fare clic su **NEXT** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="5c4bf-213">![Aggiungere i membri automaticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Aggiungere i membri automaticamente")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="5c4bf-214">In hello **membri** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5c4bf-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="5c4bf-215">![Aggiungere ed esaminare](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Aggiungere ed esaminare")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="5c4bf-216">a.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-216">a.</span></span> <span data-ttu-id="5c4bf-217">Immettere hello **posta elettronica**, **nome**, e **cognome** di un account aAd di cui si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="5c4bf-218">b.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-218">b.</span></span> <span data-ttu-id="5c4bf-219">Fare clic su **ADD AND REVIEW** (Aggiungi e verifica).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="5c4bf-220">Esaminare i dati di hello immesse e quindi fare clic su **Aggiungi membri**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="5c4bf-221">![Aggiungere un membro](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Aggiungere un membro")</span><span class="sxs-lookup"><span data-stu-id="5c4bf-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="5c4bf-222">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c4bf-223">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c4bf-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c4bf-224">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5c4bf-226">**tooassign Britta Simon tooArcGIS Online, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5c4bf-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c4bf-227">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5c4bf-229">Nell'elenco di applicazioni hello, selezionare **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="5c4bf-231">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5c4bf-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-233">Click **Add** button.</span></span> <span data-ttu-id="5c4bf-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5c4bf-236">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c4bf-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c4bf-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c4bf-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5c4bf-239">Testing single sign-on</span></span>

<span data-ttu-id="5c4bf-240">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c4bf-241">Quando si fa clic su riquadro di ArcGIS Online hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in ArcGIS Online delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5c4bf-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="5c4bf-242">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c4bf-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c4bf-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5c4bf-243">Additional resources</span></span>

* [<span data-ttu-id="5c4bf-244">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c4bf-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c4bf-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c4bf-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Splunk Enterprise e Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 848e0485131321479f2375501b330c798627e7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="55330-103">Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="55330-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="55330-104">In questa esercitazione, è illustrato come toointegrate Splunk Enterprise e Splunk Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55330-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55330-105">Integrazione di Splunk Enterprise e Splunk Cloud con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="55330-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="55330-106">È possibile controllare in Azure AD che ha accesso Enterprise tooSplunk e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="55330-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="55330-107">È possibile abilitare l'utenti tooautomatically get connesso tooSplunk Enterprise e Splunk Cloud (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="55330-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55330-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="55330-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="55330-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55330-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55330-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="55330-110">Prerequisites</span></span>

<span data-ttu-id="55330-111">integrazione di Azure AD con Splunk Enterprise e Splunk Cloud tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="55330-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="55330-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55330-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55330-113">Sottoscrizione di Splunk Enterprise e Splunk Cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="55330-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55330-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="55330-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55330-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="55330-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55330-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="55330-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55330-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55330-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55330-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="55330-118">Scenario description</span></span>
<span data-ttu-id="55330-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="55330-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55330-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="55330-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55330-121">Aggiunta di Splunk Enterprise e Splunk Cloud dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="55330-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="55330-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="55330-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="55330-123">Aggiunta di Splunk Enterprise e Splunk Cloud dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="55330-123">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="55330-124">integrazione hello tooconfigure di Splunk Enterprise e Splunk Cloud in Azure AD, è necessario tooadd Splunk Enterprise Splunk Cloud dall'elenco di tooyour hello raccolta di App e gestite SaaS.</span><span class="sxs-lookup"><span data-stu-id="55330-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55330-125">**tooadd Splunk Enterprise e Splunk Cloud dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="55330-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55330-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="55330-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55330-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="55330-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55330-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="55330-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="55330-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="55330-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="55330-133">Nella casella di ricerca hello, digitare **Splunk Enterprise e Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="55330-133">In hello search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="55330-135">Nel riquadro dei risultati hello, selezionare **Splunk Enterprise e Splunk Cloud**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="55330-135">In hello results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55330-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="55330-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55330-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Splunk Enterprise e Splunk Cloud con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="55330-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="55330-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Splunk Enterprise e Splunk Cloud è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55330-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="55330-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Splunk Enterprise e Splunk Cloud deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="55330-140">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="55330-141">In Splunk Enterprise e Splunk Cloud, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="55330-141">In Splunk Enterprise and Splunk Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="55330-142">tooconfigure e prova AD Azure single sign-on con Splunk Enterprise e Splunk Cloud, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="55330-142">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55330-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="55330-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55330-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55330-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55330-145">**[Creazione di un utente test Splunk Enterprise e Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave un equivalente di Britta Simon Splunk azienda e Splunk Cloud toohello collegato AD Azure rappresentazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="55330-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="55330-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="55330-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55330-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="55330-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55330-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="55330-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55330-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="55330-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="55330-150">**tooconfigure AD Azure single sign-on con Splunk Enterprise e Splunk Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="55330-150">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="55330-151">Nel portale di Azure su hello hello **Splunk Enterprise e Splunk Cloud** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="55330-151">In hello Azure portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="55330-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="55330-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="55330-155">In hello **Splunk Enterprise e Splunk Cloud dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="55330-155">On hello **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="55330-157">a.</span><span class="sxs-lookup"><span data-stu-id="55330-157">a.</span></span> <span data-ttu-id="55330-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="55330-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="55330-159">b.</span><span class="sxs-lookup"><span data-stu-id="55330-159">b.</span></span> <span data-ttu-id="55330-160">In hello **identificatore** casella di testo, digitare l'URL del Splunk Server hello.</span><span class="sxs-lookup"><span data-stu-id="55330-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>

    <span data-ttu-id="55330-161">c.</span><span class="sxs-lookup"><span data-stu-id="55330-161">c.</span></span> <span data-ttu-id="55330-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="55330-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55330-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="55330-163">These values are not real.</span></span> <span data-ttu-id="55330-164">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="55330-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="55330-165">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="55330-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="55330-166">Contatto [team di supporto di Splunk Enterprise e Splunk Cloud Client](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="55330-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget these values.</span></span> 

4. <span data-ttu-id="55330-167">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="55330-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="55330-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="55330-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55330-171">tooconfigure single sign-on sul **Splunk Enterprise e Splunk Cloud** lato, è necessario hello toosend scaricato **Metadata XML** troppo[teamdisupportodiSplunkEnterpriseeSplunkCloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="55330-171">tooconfigure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need toosend hello downloaded **Metadata XML** too[Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="55330-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="55330-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="55330-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="55330-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="55330-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55330-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55330-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="55330-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="55330-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="55330-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="55330-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="55330-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55330-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="55330-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55330-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="55330-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55330-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="55330-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55330-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="55330-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55330-187">a.</span><span class="sxs-lookup"><span data-stu-id="55330-187">a.</span></span> <span data-ttu-id="55330-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55330-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55330-189">b.</span><span class="sxs-lookup"><span data-stu-id="55330-189">b.</span></span> <span data-ttu-id="55330-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="55330-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55330-191">c.</span><span class="sxs-lookup"><span data-stu-id="55330-191">c.</span></span> <span data-ttu-id="55330-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="55330-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="55330-193">d.</span><span class="sxs-lookup"><span data-stu-id="55330-193">d.</span></span> <span data-ttu-id="55330-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="55330-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="55330-195">Creazione di un utente test di Splunk Enterprise e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="55330-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="55330-196">In questa sezione viene creato un utente chiamato Britta Simon in Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="55330-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="55330-197">Lavorare con [team di supporto di Splunk Enterprise e Splunk Cloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) gli utenti di hello tooadd hello Splunk Enterprise Splunk piattaforma e Cloud.</span><span class="sxs-lookup"><span data-stu-id="55330-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="55330-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="55330-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="55330-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSplunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="55330-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="55330-201">**tooassign Britta Simon tooSplunk Enterprise e Splunk Cloud, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="55330-201">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="55330-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="55330-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="55330-204">Nell'elenco di applicazioni hello, selezionare **Splunk Enterprise e Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="55330-204">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="55330-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="55330-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="55330-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="55330-208">Click **Add** button.</span></span> <span data-ttu-id="55330-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="55330-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="55330-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="55330-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="55330-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="55330-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55330-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="55330-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="55330-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="55330-214">Testing single sign-on</span></span>

<span data-ttu-id="55330-215">In questa sezione è verificare il AD SSOonfiguration Azure tramite hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="55330-215">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="55330-216">Quando si fa clic hello Splunk Enterprise e riquadro Splunk Cloud in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="55330-216">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55330-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="55330-217">Additional resources</span></span>

* [<span data-ttu-id="55330-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55330-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55330-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55330-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png


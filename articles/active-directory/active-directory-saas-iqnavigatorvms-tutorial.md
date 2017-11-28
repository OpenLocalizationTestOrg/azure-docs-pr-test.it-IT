---
title: 'Esercitazione: Integrazione di Azure Active Directory con IQNavigator VMS | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e IQNavigator VMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="af2c9-103">Esercitazione: Integrazione di Azure Active Directory con IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="af2c9-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="af2c9-104">In questa esercitazione, è illustrato come toointegrate IQNavigator VMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af2c9-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af2c9-105">Integrazione IQNavigator VMS con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="af2c9-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="af2c9-106">È possibile controllare in Azure AD che ha accesso tooIQNavigator macchine Virtuali</span><span class="sxs-lookup"><span data-stu-id="af2c9-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="af2c9-107">È possibile abilitare l'utenti tooautomatically get connesso tooIQNavigator macchine Virtuali (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2c9-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="af2c9-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="af2c9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="af2c9-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af2c9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af2c9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="af2c9-110">Prerequisites</span></span>

<span data-ttu-id="af2c9-111">integrazione di Azure AD con VMS IQNavigator tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="af2c9-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="af2c9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af2c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="af2c9-113">Sottoscrizione di IQNavigator VMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="af2c9-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af2c9-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="af2c9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af2c9-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="af2c9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af2c9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="af2c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="af2c9-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af2c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af2c9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="af2c9-118">Scenario description</span></span>
<span data-ttu-id="af2c9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="af2c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af2c9-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="af2c9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af2c9-121">Aggiunta di IQNavigator VMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="af2c9-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="af2c9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="af2c9-123">Aggiunta di IQNavigator VMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="af2c9-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="af2c9-124">integrazione hello tooconfigure di IQNavigator VMS in Azure AD, è necessario tooadd IQNavigator VMS dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="af2c9-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="af2c9-125">**tooadd IQNavigator VMS dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af2c9-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="af2c9-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="af2c9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="af2c9-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="af2c9-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="af2c9-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="af2c9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="af2c9-133">Nella casella di ricerca hello, digitare **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="af2c9-135">Nel riquadro dei risultati hello, selezionare **IQNavigator VMS**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="af2c9-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="af2c9-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="af2c9-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con IQNavigator VMS con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="af2c9-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="af2c9-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello VMS IQNavigator è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af2c9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="af2c9-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello IQNavigator VMS deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="af2c9-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="af2c9-141">VMS IQNavigator, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="af2c9-142">tooconfigure e prova AD Azure single sign-on con IQNavigator VMS, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="af2c9-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="af2c9-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="af2c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="af2c9-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af2c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af2c9-145">**[Creazione di un utente test VMS IQNavigator](#creating-a-iqnavigator-vms-test-user)**  -toohave un equivalente di Britta Simon VMS IQNavigator che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="af2c9-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="af2c9-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af2c9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af2c9-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="af2c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="af2c9-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="af2c9-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="af2c9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="af2c9-150">**Azure AD tooconfigure single sign-on con IQNavigator VMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af2c9-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="af2c9-151">Nel portale di Azure su hello hello **IQNavigator VMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="af2c9-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af2c9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="af2c9-155">In hello **IQNavigator macchine Virtuali di dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af2c9-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="af2c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="af2c9-157">a.</span></span> <span data-ttu-id="af2c9-158">In hello **identificatore** casella di testo, digitare l'URL hello:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="af2c9-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="af2c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="af2c9-159">b.</span></span> <span data-ttu-id="af2c9-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="af2c9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="af2c9-161">Controllare **Mostra URL impostazioni avanzate**, eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="af2c9-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="af2c9-163">In hello **inoltro stato** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="af2c9-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="af2c9-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="af2c9-164">These values are not real.</span></span> <span data-ttu-id="af2c9-165">Aggiornare questi valori con stato di URL di risposta e inoltro effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="af2c9-166">Contatto [team di supporto Client di macchine Virtuali IQNavigator](https://www.beeline.com/iqn-product-support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="af2c9-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="af2c9-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="af2c9-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="af2c9-169">hello toogenerate **metadati** url, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af2c9-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="af2c9-170">a.</span><span class="sxs-lookup"><span data-stu-id="af2c9-170">a.</span></span> <span data-ttu-id="af2c9-171">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-171">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="af2c9-173">b.</span><span class="sxs-lookup"><span data-stu-id="af2c9-173">b.</span></span> <span data-ttu-id="af2c9-174">Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="af2c9-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="af2c9-176">c.</span><span class="sxs-lookup"><span data-stu-id="af2c9-176">c.</span></span> <span data-ttu-id="af2c9-177">Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="af2c9-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="af2c9-179">d.</span><span class="sxs-lookup"><span data-stu-id="af2c9-179">d.</span></span> <span data-ttu-id="af2c9-180">Ora passare toohello pagina delle proprietà di **IQNavigator VMS** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="af2c9-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="af2c9-182">e.</span><span class="sxs-lookup"><span data-stu-id="af2c9-182">e.</span></span> <span data-ttu-id="af2c9-183">Generare hello **URL dei metadati** utilizzando hello seguente motivo:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="af2c9-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="af2c9-184">Applicazione IQNavigator previsto valore dell'identificatore utente univoco hello in attestazioni nome identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="af2c9-185">Cliente può eseguire il mapping hello di valore corretto per l'attestazione dell'identificatore di nome hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="af2c9-186">In questo caso è stato eseguito il mapping utente hello. UserPrincipalName a scopo dimostrativo hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="af2c9-187">Ma in base a tooyour impostazioni dell'organizzazione è necessario mappare valore corretto hello relativo.</span><span class="sxs-lookup"><span data-stu-id="af2c9-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="af2c9-189">In hello **configurazione di macchine Virtuali IQNavigator** fare clic su **configurare macchine Virtuali IQNavigator** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="af2c9-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="af2c9-190">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="af2c9-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="af2c9-192">tooconfigure single sign-on sul **IQNavigator VMS** lato, è necessario hello toosend **URL dei metadati**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo [Team di supporto IQNavigator VMS](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="af2c9-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="af2c9-193">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="af2c9-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="af2c9-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="af2c9-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="af2c9-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="af2c9-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="af2c9-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="af2c9-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2c9-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="af2c9-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="af2c9-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="af2c9-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af2c9-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="af2c9-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="af2c9-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="af2c9-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="af2c9-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="af2c9-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af2c9-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="af2c9-209">a.</span><span class="sxs-lookup"><span data-stu-id="af2c9-209">a.</span></span> <span data-ttu-id="af2c9-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af2c9-211">b.</span><span class="sxs-lookup"><span data-stu-id="af2c9-211">b.</span></span> <span data-ttu-id="af2c9-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="af2c9-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af2c9-213">c.</span><span class="sxs-lookup"><span data-stu-id="af2c9-213">c.</span></span> <span data-ttu-id="af2c9-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="af2c9-215">d.</span><span class="sxs-lookup"><span data-stu-id="af2c9-215">d.</span></span> <span data-ttu-id="af2c9-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="af2c9-217">Creazione di un utente test di IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="af2c9-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="af2c9-218">obiettivo di Hello di questa sezione è un utente denominato Britta Simon IQNavigator VMS toocreate.</span><span class="sxs-lookup"><span data-stu-id="af2c9-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="af2c9-219">Lavorare con [team di supporto IQNavigator VMS](https://www.beeline.com/iqn-product-support/) utenti hello tooadd hello account IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="af2c9-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="af2c9-220">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2c9-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="af2c9-221">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIQNavigator macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="af2c9-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="af2c9-223">**tooassign Britta Simon tooIQNavigator le macchine Virtuali, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af2c9-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="af2c9-224">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="af2c9-226">Nell'elenco di applicazioni hello, selezionare **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="af2c9-228">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="af2c9-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-230">Click **Add** button.</span></span> <span data-ttu-id="af2c9-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="af2c9-233">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="af2c9-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="af2c9-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af2c9-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af2c9-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="af2c9-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="af2c9-236">Testing single sign-on</span></span>

<span data-ttu-id="af2c9-237">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="af2c9-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="af2c9-238">Quando si fa clic hello riquadro IQNavigator VMS in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="af2c9-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="af2c9-239">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="af2c9-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af2c9-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="af2c9-240">Additional resources</span></span>

* [<span data-ttu-id="af2c9-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af2c9-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af2c9-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af2c9-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png


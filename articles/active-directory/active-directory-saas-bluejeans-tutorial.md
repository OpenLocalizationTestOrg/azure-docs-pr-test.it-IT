---
title: 'Esercitazione: Integrazione di Azure Active Directory con BlueJeans | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BlueJeans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="cb5b5-103">Esercitazione: Integrazione di Azure Active Directory con BlueJeans</span><span class="sxs-lookup"><span data-stu-id="cb5b5-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="cb5b5-104">In questa esercitazione, è illustrato come toointegrate BlueJeans con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb5b5-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb5b5-105">Integrazione di BlueJeans con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb5b5-106">È possibile controllare in Azure AD che ha accesso tooBlueJeans</span><span class="sxs-lookup"><span data-stu-id="cb5b5-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="cb5b5-107">È possibile abilitare l'utenti tooautomatically get connesso tooBlueJeans (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5b5-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb5b5-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cb5b5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb5b5-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb5b5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb5b5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cb5b5-110">Prerequisites</span></span>

<span data-ttu-id="cb5b5-111">integrazione di Azure AD con BlueJeans tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="cb5b5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb5b5-113">Sottoscrizione di BlueJeans abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cb5b5-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb5b5-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb5b5-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb5b5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb5b5-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb5b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb5b5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cb5b5-118">Scenario description</span></span>
<span data-ttu-id="cb5b5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb5b5-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb5b5-121">Aggiunta di BlueJeans dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cb5b5-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="cb5b5-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="cb5b5-123">Aggiunta di BlueJeans dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cb5b5-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="cb5b5-124">integrazione hello tooconfigure di BlueJeans in Azure AD, è necessario tooadd BlueJeans dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb5b5-125">**tooadd BlueJeans dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cb5b5-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb5b5-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb5b5-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb5b5-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="cb5b5-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="cb5b5-133">Nella casella di ricerca hello, digitare **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-133">In hello search box, type **BlueJeans**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="cb5b5-135">Nel riquadro dei risultati hello, selezionare **BlueJeans**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb5b5-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb5b5-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BlueJeans usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cb5b5-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb5b5-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in BlueJeans è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="cb5b5-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in BlueJeans deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="cb5b5-141">In BlueJeans, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cb5b5-142">tooconfigure e test Azure single sign-on AD con BlueJeans, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb5b5-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb5b5-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb5b5-145">**[Creazione di un utente test BlueJeans](#creating-a-bluejeans-test-user)**  -toohave un equivalente di Britta Simon in BlueJeans che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb5b5-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb5b5-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb5b5-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb5b5-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="cb5b5-150">**Azure AD tooconfigure single sign-on con BlueJeans, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cb5b5-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb5b5-151">Nel portale di Azure su hello hello **BlueJeans** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="cb5b5-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="cb5b5-155">In hello **BlueJeans dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="cb5b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-157">a.</span></span> <span data-ttu-id="cb5b5-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="cb5b5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="cb5b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-159">b.</span></span> <span data-ttu-id="cb5b5-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="cb5b5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb5b5-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="cb5b5-161">These values are not real.</span></span> <span data-ttu-id="cb5b5-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cb5b5-163">Contatto [team di supporto Client di BlueJeans](https://support.bluejeans.com/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="cb5b5-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="cb5b5-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cb5b5-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb5b5-168">In hello **BlueJeans configurazione** fare clic su **configurare BlueJeans** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cb5b5-169">Hello copia **Sign-Out URL, Modifica URL Password e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="cb5b5-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="cb5b5-171">In una finestra del web browser, accedere tooyour **BlueJeans** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="cb5b5-172">Andare troppo**ADMIN \> impostazioni gruppo \> sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="cb5b5-173">![Amministratore](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="cb5b5-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="cb5b5-174">In hello **sicurezza** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="cb5b5-175">![Single Sign-On SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Single Sign-On SAML")</span><span class="sxs-lookup"><span data-stu-id="cb5b5-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="cb5b5-176">a.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-176">a.</span></span> <span data-ttu-id="cb5b5-177">Selezionare **SAML Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="cb5b5-178">b.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-178">b.</span></span> <span data-ttu-id="cb5b5-179">Selezionare **Enable automatic provisioning**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="cb5b5-180">Passare con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="cb5b5-181">![Percorso certificato](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Percorso certificato")</span><span class="sxs-lookup"><span data-stu-id="cb5b5-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="cb5b5-182">a.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-182">a.</span></span> <span data-ttu-id="cb5b5-183">Fare clic su **Scegli File**e quindi caricare il certificato scaricato hello.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="cb5b5-184">b.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-184">b.</span></span> <span data-ttu-id="cb5b5-185">Incolla **SAML Single Sign-On Service URL** in hello **URL di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="cb5b5-186">c.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-186">c.</span></span> <span data-ttu-id="cb5b5-187">Incolla **Modifica URL Password** in hello **Change Password URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="cb5b5-188">d.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-188">d.</span></span> <span data-ttu-id="cb5b5-189">Incolla **Sign-Out URL** in hello **Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="cb5b5-190">Passare con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="cb5b5-191">![Salvare le modifiche](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Salvare le modifiche")</span><span class="sxs-lookup"><span data-stu-id="cb5b5-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="cb5b5-192">a.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-192">a.</span></span> <span data-ttu-id="cb5b5-193">In hello **id utente** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="cb5b5-194">b.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-194">b.</span></span> <span data-ttu-id="cb5b5-195">In hello **posta elettronica** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="cb5b5-196">c.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-196">c.</span></span> <span data-ttu-id="cb5b5-197">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cb5b5-198">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="cb5b5-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb5b5-199">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb5b5-200">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb5b5-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb5b5-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5b5-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb5b5-202">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="cb5b5-204">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cb5b5-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb5b5-205">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb5b5-207">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb5b5-209">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb5b5-211">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb5b5-213">a.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-213">a.</span></span> <span data-ttu-id="cb5b5-214">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb5b5-215">b.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-215">b.</span></span> <span data-ttu-id="cb5b5-216">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb5b5-217">c.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-217">c.</span></span> <span data-ttu-id="cb5b5-218">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb5b5-219">d.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-219">d.</span></span> <span data-ttu-id="cb5b5-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="cb5b5-221">Creazione di un utente di test di BlueJeans</span><span class="sxs-lookup"><span data-stu-id="cb5b5-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="cb5b5-222">toolog agli utenti di Azure AD tooenable in tooBlueJeans, è necessario eseguirne il provisioning in BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="cb5b5-223">Nel caso di BlueJeans, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="cb5b5-224">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="cb5b5-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb5b5-225">Accedi tooyour **BlueJeans** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="cb5b5-226">Andare troppo**ADMIN \> Gestisci utenti \> Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="cb5b5-227">![Amministratore](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="cb5b5-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="cb5b5-228">Hello **Aggiungi utente** scheda è disponibile solo se nell'hello **scheda sicurezza**, **abilitare il provisioning automatico** è deselezionata.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="cb5b5-229">In hello **Aggiungi utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cb5b5-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="cb5b5-230">![Aggiungere un utente](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="cb5b5-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="cb5b5-231">a.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-231">a.</span></span> <span data-ttu-id="cb5b5-232">Digitare un **nome utente BlueJeans**, un **indirizzo di posta elettronica**, **ID riunione BlueJeans**, **Passcode di moderatore**, un **nome completo** , hello **aziendale** di un account aAd di cui si desidera tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="cb5b5-233">b.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-233">b.</span></span> <span data-ttu-id="cb5b5-234">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="cb5b5-235">È possibile usare qualsiasi altro BlueJeans utente account strumento di creazione o le API fornite da BlueJeans tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb5b5-236">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5b5-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb5b5-237">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Assegna utente][200] 

<span data-ttu-id="cb5b5-239">**tooassign Britta Simon tooBlueJeans, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cb5b5-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb5b5-240">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cb5b5-242">Nell'elenco di applicazioni hello, selezionare **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="cb5b5-244">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="cb5b5-246">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-246">Click **Add** button.</span></span> <span data-ttu-id="cb5b5-247">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="cb5b5-249">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb5b5-250">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb5b5-251">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb5b5-252">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cb5b5-252">Testing single sign-on</span></span>

<span data-ttu-id="cb5b5-253">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb5b5-254">Quando si fa clic hello BlueJeans riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5b5-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="cb5b5-255">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb5b5-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cb5b5-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cb5b5-256">Additional resources</span></span>

* [<span data-ttu-id="cb5b5-257">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb5b5-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb5b5-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb5b5-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png


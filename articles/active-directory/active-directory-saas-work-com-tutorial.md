---
title: 'Esercitazione: Integrazione di Azure Active Directory con Work.com | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Work.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="5f504-103">Esercitazione: Integrazione di Azure Active Directory con Work.com</span><span class="sxs-lookup"><span data-stu-id="5f504-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="5f504-104">In questa esercitazione, è illustrato come toointegrate Work.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f504-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f504-105">Integrazione di Work.com con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5f504-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5f504-106">È possibile controllare in Azure AD che ha accesso tooWork.com</span><span class="sxs-lookup"><span data-stu-id="5f504-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="5f504-107">È possibile abilitare l'utenti tooautomatically get connesso tooWork.com (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f504-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f504-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5f504-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5f504-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f504-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f504-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5f504-110">Prerequisites</span></span>

<span data-ttu-id="5f504-111">integrazione di Azure AD con Work.com tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5f504-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="5f504-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f504-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f504-113">Sottoscrizione di Work.com abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5f504-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f504-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5f504-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f504-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5f504-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f504-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5f504-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f504-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f504-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f504-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5f504-118">Scenario description</span></span>
<span data-ttu-id="5f504-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5f504-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f504-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5f504-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f504-121">Aggiungere Work.com dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="5f504-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="5f504-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f504-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="5f504-123">Aggiungere Work.com dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="5f504-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="5f504-124">integrazione hello tooconfigure di Work.com in Azure AD, è necessario tooadd Work.com dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5f504-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5f504-125">**tooadd Work.com dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5f504-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f504-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5f504-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5f504-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5f504-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5f504-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5f504-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5f504-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5f504-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5f504-133">Nella casella di ricerca hello, digitare **Work.com**selezionare **Work.com** dal riquadro dei risultati, quindi scegliere **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5f504-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Aggiungere dalla raccolta](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5f504-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f504-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5f504-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Work.com usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5f504-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f504-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Work.com è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f504-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="5f504-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Work.com deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5f504-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="5f504-139">In Work.com, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5f504-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5f504-140">tooconfigure e prova AD Azure single sign-on con Work.com, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5f504-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5f504-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5f504-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5f504-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f504-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f504-143">**[Creare un utente test Work.com](#create-a-workcom-test-user)**  -toohave un equivalente di Britta Simon in Work.com che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5f504-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f504-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5f504-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f504-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5f504-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5f504-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f504-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5f504-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Work.com.</span><span class="sxs-lookup"><span data-stu-id="5f504-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="5f504-148">tooconfigure accesso single sign-on, è necessario un nome di dominio personalizzato Work.com toosetup ancora.</span><span class="sxs-lookup"><span data-stu-id="5f504-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="5f504-149">È necessario almeno un dominio toodefine nome, verificare il nome di dominio e distribuirlo tooyour intera organizzazione.</span><span class="sxs-lookup"><span data-stu-id="5f504-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="5f504-150">**Azure AD tooconfigure single sign-on con Work.com, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5f504-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f504-151">Nel portale di Azure su hello hello **Work.com** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5f504-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5f504-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5f504-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="5f504-155">In hello **Work.com dominio e gli URL** sezione, eseguire l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="5f504-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Sezione URL e dominio Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="5f504-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="5f504-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f504-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="5f504-158">This value is not real.</span></span> <span data-ttu-id="5f504-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5f504-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5f504-160">Contatto [team di supporto Client di Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="5f504-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="5f504-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5f504-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="5f504-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5f504-163">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f504-165">In hello **Work.com configurazione** fare clic su **configurare Work.com** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5f504-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5f504-166">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5f504-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sezione Configurazione di Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="5f504-168">Accedi tooyour tenant di Work.com come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5f504-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="5f504-169">Andare troppo**installazione**.</span><span class="sxs-lookup"><span data-stu-id="5f504-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="5f504-170">![Installazione](./media/active-directory-saas-work-com-tutorial/ic794108.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="5f504-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="5f504-171">Nel riquadro di spostamento a sinistra, hello hello **Amministra** fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** hello tooopen  **Il mio dominio** pagina.</span><span class="sxs-lookup"><span data-stu-id="5f504-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="5f504-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="5f504-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="5f504-173">tooverify che il dominio è stato configurato correttamente, assicurarsi che sia in "**passaggio 4 distribuito tooUsers**" ed esaminare il "**impostazioni dominio personali**".</span><span class="sxs-lookup"><span data-stu-id="5f504-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="5f504-174">![Dominio distribuito tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser distribuite del dominio")</span><span class="sxs-lookup"><span data-stu-id="5f504-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="5f504-175">Accedi tooyour tenant di Work.com.</span><span class="sxs-lookup"><span data-stu-id="5f504-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="5f504-176">Andare troppo**installazione**.</span><span class="sxs-lookup"><span data-stu-id="5f504-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="5f504-177">![Installazione](./media/active-directory-saas-work-com-tutorial/ic794108.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="5f504-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="5f504-178">Espandere hello **controlli di sicurezza** menu e quindi fare clic su **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="5f504-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="5f504-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="5f504-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="5f504-180">In hello **Single Sign-On Settings** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f504-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="5f504-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span><span class="sxs-lookup"><span data-stu-id="5f504-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="5f504-182">a.</span><span class="sxs-lookup"><span data-stu-id="5f504-182">a.</span></span> <span data-ttu-id="5f504-183">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="5f504-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="5f504-184">b.</span><span class="sxs-lookup"><span data-stu-id="5f504-184">b.</span></span> <span data-ttu-id="5f504-185">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="5f504-185">Click **New**.</span></span>

15. <span data-ttu-id="5f504-186">In hello **SAML Single Sign-On Settings** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f504-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="5f504-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="5f504-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="5f504-188">a.</span><span class="sxs-lookup"><span data-stu-id="5f504-188">a.</span></span> <span data-ttu-id="5f504-189">In hello **nome** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="5f504-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="5f504-190">Fornisce un valore per **nome** popolare automaticamente hello **nome API** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5f504-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="5f504-191">b.</span><span class="sxs-lookup"><span data-stu-id="5f504-191">b.</span></span> <span data-ttu-id="5f504-192">In **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f504-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="5f504-193">c.</span><span class="sxs-lookup"><span data-stu-id="5f504-193">c.</span></span> <span data-ttu-id="5f504-194">certificato di tooupload hello scaricato dal portale di Azure, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="5f504-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="5f504-195">d.</span><span class="sxs-lookup"><span data-stu-id="5f504-195">d.</span></span> <span data-ttu-id="5f504-196">In hello **Id entità** casella tipo `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="5f504-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="5f504-197">e.</span><span class="sxs-lookup"><span data-stu-id="5f504-197">e.</span></span> <span data-ttu-id="5f504-198">Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**.</span><span class="sxs-lookup"><span data-stu-id="5f504-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="5f504-199">f.</span><span class="sxs-lookup"><span data-stu-id="5f504-199">f.</span></span> <span data-ttu-id="5f504-200">Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentfier hello di hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="5f504-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="5f504-201">g.</span><span class="sxs-lookup"><span data-stu-id="5f504-201">g.</span></span> <span data-ttu-id="5f504-202">In **Identity Provider Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f504-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5f504-203">h.</span><span class="sxs-lookup"><span data-stu-id="5f504-203">h.</span></span> <span data-ttu-id="5f504-204">In **Identity Provider Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f504-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="5f504-205">i.</span><span class="sxs-lookup"><span data-stu-id="5f504-205">i.</span></span> <span data-ttu-id="5f504-206">In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="5f504-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="5f504-207">j.</span><span class="sxs-lookup"><span data-stu-id="5f504-207">j.</span></span> <span data-ttu-id="5f504-208">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5f504-208">Click **Save**.</span></span>

16. <span data-ttu-id="5f504-209">Nel portale classico a Work.com, nel riquadro di spostamento a sinistra di hello, fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** tooopen hello **My Domain**pagina.</span><span class="sxs-lookup"><span data-stu-id="5f504-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="5f504-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="5f504-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="5f504-211">In hello **My Domain** pagina hello **personalizzazione pagina di accesso** fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="5f504-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="5f504-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="5f504-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="5f504-213">In hello **personalizzazione pagina di accesso** pagina hello **servizio di autenticazione** sezione, il nome di hello del **SAML SSO Settings** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="5f504-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="5f504-214">Selezionarlo e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="5f504-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="5f504-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="5f504-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="5f504-216">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5f504-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5f504-217">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5f504-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5f504-218">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f504-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5f504-219">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f504-219">Create an Azure AD test user</span></span>
<span data-ttu-id="5f504-220">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5f504-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5f504-222">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5f504-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f504-223">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5f504-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f504-225">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5f504-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi -> Tutti gli utenti](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f504-227">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5f504-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Add](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f504-229">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f504-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f504-231">a.</span><span class="sxs-lookup"><span data-stu-id="5f504-231">a.</span></span> <span data-ttu-id="5f504-232">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f504-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f504-233">b.</span><span class="sxs-lookup"><span data-stu-id="5f504-233">b.</span></span> <span data-ttu-id="5f504-234">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5f504-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f504-235">c.</span><span class="sxs-lookup"><span data-stu-id="5f504-235">c.</span></span> <span data-ttu-id="5f504-236">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5f504-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5f504-237">d.</span><span class="sxs-lookup"><span data-stu-id="5f504-237">d.</span></span> <span data-ttu-id="5f504-238">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5f504-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="5f504-239">Creare un utente di test di Work.com</span><span class="sxs-lookup"><span data-stu-id="5f504-239">Create a Work.com test user</span></span>
<span data-ttu-id="5f504-240">Per Azure Active Directory gli utenti toobe in grado di toosign in devono essere tooWork.com provisioning. Nel caso di hello di Work.com, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5f504-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="5f504-241">tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5f504-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="5f504-242">Accesso tooyour sito della società Work.com come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5f504-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="5f504-243">Andare troppo**installazione**.</span><span class="sxs-lookup"><span data-stu-id="5f504-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="5f504-244">![Installazione](./media/active-directory-saas-work-com-tutorial/IC794108.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="5f504-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="5f504-245">Andare troppo**Gestisci utenti \> utenti**.</span><span class="sxs-lookup"><span data-stu-id="5f504-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="5f504-246">![Gestione utenti](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="5f504-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="5f504-247">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="5f504-247">Click **New User**.</span></span>
   
    <span data-ttu-id="5f504-248">![Tutti gli utenti](./media/active-directory-saas-work-com-tutorial/IC794117.png "Tutti gli utenti")</span><span class="sxs-lookup"><span data-stu-id="5f504-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="5f504-249">Nella sezione User Edit hello, eseguire hello alla procedura seguente, negli attributi di un valido di Azure nelle caselle di testo relative all'account di Active Directory desiderata tooprovision in hello:</span><span class="sxs-lookup"><span data-stu-id="5f504-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="5f504-250">![Modifica dell'utente](./media/active-directory-saas-work-com-tutorial/ic794118.png "Modifica dell'utente")</span><span class="sxs-lookup"><span data-stu-id="5f504-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="5f504-251">a.</span><span class="sxs-lookup"><span data-stu-id="5f504-251">a.</span></span> <span data-ttu-id="5f504-252">In hello **nome** casella di testo, hello tipo **nome** dell'utente hello **Laura**.</span><span class="sxs-lookup"><span data-stu-id="5f504-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="5f504-253">b.</span><span class="sxs-lookup"><span data-stu-id="5f504-253">b.</span></span> <span data-ttu-id="5f504-254">In hello **cognome** casella di testo, hello tipo **cognome** dell'utente hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5f504-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="5f504-255">c.</span><span class="sxs-lookup"><span data-stu-id="5f504-255">c.</span></span> <span data-ttu-id="5f504-256">In hello **Alias** casella di testo, hello tipo **nome** dell'utente hello **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="5f504-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="5f504-257">d.</span><span class="sxs-lookup"><span data-stu-id="5f504-257">d.</span></span> <span data-ttu-id="5f504-258">In hello **posta elettronica** casella di testo, hello tipo **indirizzo di posta elettronica** dell'utente  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="5f504-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="5f504-259">e.</span><span class="sxs-lookup"><span data-stu-id="5f504-259">e.</span></span> <span data-ttu-id="5f504-260">In hello **nome utente** , digitare un nome utente dell'utente come  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="5f504-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="5f504-261">f.</span><span class="sxs-lookup"><span data-stu-id="5f504-261">f.</span></span> <span data-ttu-id="5f504-262">In hello **nome alternativo** casella di testo, digitare un **nome alternativo** dell'utente **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5f504-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="5f504-263">g.</span><span class="sxs-lookup"><span data-stu-id="5f504-263">g.</span></span> <span data-ttu-id="5f504-264">Selezionare **Role** (Ruolo), **User License**(Licenza utente) e **Profile** (Profilo).</span><span class="sxs-lookup"><span data-stu-id="5f504-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="5f504-265">h.</span><span class="sxs-lookup"><span data-stu-id="5f504-265">h.</span></span> <span data-ttu-id="5f504-266">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5f504-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="5f504-267">titolare dell'account di Azure AD di Hello riceverà un messaggio di posta elettronica tra un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="5f504-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5f504-268">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f504-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5f504-269">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWork.com.</span><span class="sxs-lookup"><span data-stu-id="5f504-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5f504-271">**tooassign Britta Simon tooWork.com, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5f504-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f504-272">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5f504-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5f504-274">Nell'elenco di applicazioni hello, selezionare **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="5f504-274">In hello applications list, select **Work.com**.</span></span>

    ![Work.com nell'elenco delle app](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="5f504-276">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5f504-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5f504-278">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5f504-278">Click **Add** button.</span></span> <span data-ttu-id="5f504-279">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5f504-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5f504-281">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5f504-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5f504-282">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5f504-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f504-283">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5f504-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5f504-284">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5f504-284">Test single sign-on</span></span>

<span data-ttu-id="5f504-285">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5f504-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5f504-286">Quando si fa clic su riquadro Work.com hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Work.com applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f504-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="5f504-287">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5f504-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f504-288">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5f504-288">Additional resources</span></span>

* [<span data-ttu-id="5f504-289">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f504-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f504-290">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f504-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png


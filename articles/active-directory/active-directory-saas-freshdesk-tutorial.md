---
title: 'Esercitazione: Integrazione di Azure Active Directory con FreshDesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="961c8-103">Esercitazione: Integrazione di Azure Active Directory con FreshDesk</span><span class="sxs-lookup"><span data-stu-id="961c8-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="961c8-104">In questa esercitazione, è illustrato come toointegrate FreshDesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="961c8-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="961c8-105">Integrazione di FreshDesk con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="961c8-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="961c8-106">È possibile controllare in Azure AD che ha accesso tooFreshDesk</span><span class="sxs-lookup"><span data-stu-id="961c8-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="961c8-107">È possibile abilitare l'utenti tooautomatically get connesso tooFreshDesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="961c8-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="961c8-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="961c8-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="961c8-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="961c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="961c8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="961c8-110">Prerequisites</span></span>

<span data-ttu-id="961c8-111">integrazione di Azure AD con FreshDesk tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="961c8-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="961c8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="961c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="961c8-113">Sottoscrizione di FreshDesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="961c8-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="961c8-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="961c8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="961c8-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="961c8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="961c8-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="961c8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="961c8-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="961c8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="961c8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="961c8-118">Scenario description</span></span>
<span data-ttu-id="961c8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="961c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="961c8-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="961c8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="961c8-121">Aggiunta di FreshDesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="961c8-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="961c8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="961c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="961c8-123">Aggiunta di FreshDesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="961c8-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="961c8-124">integrazione hello tooconfigure di FreshDesk in Azure AD, è necessario tooadd FreshDesk dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="961c8-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="961c8-125">**tooadd FreshDesk dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="961c8-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="961c8-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="961c8-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="961c8-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="961c8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="961c8-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="961c8-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="961c8-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="961c8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="961c8-133">Nella casella di ricerca hello, digitare **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="961c8-133">In hello search box, type **FreshDesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="961c8-135">Nel riquadro dei risultati hello, selezionare **FreshDesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="961c8-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="961c8-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="961c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="961c8-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FreshDesk in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="961c8-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="961c8-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FreshDesk è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="961c8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="961c8-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FreshDesk richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="961c8-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="961c8-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="961c8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="961c8-142">tooconfigure e test Azure single sign-on AD con FreshDesk, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="961c8-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="961c8-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="961c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="961c8-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="961c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="961c8-145">**[Creazione di un utente test FreshDesk](#creating-a-freshdesk-test-user)**  -toohave un equivalente di Britta Simon in FreshDesk toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="961c8-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="961c8-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="961c8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="961c8-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="961c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="961c8-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="961c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="961c8-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on in freshservice.</span><span class="sxs-lookup"><span data-stu-id="961c8-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="961c8-150">**Azure AD tooconfigure single sign-on con FreshDesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="961c8-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="961c8-151">Nel portale di gestione di Azure hello in hello **FreshDesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="961c8-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="961c8-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="961c8-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="961c8-155">In hello **FreshDesk dominio e gli URL** sezione, immettere hello **Sign-on URL** come: `https://<tenant-name>.freshdesk.com` o qualsiasi altro valore Freshdesk ha suggerito.</span><span class="sxs-lookup"><span data-stu-id="961c8-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="961c8-157">Si noti che questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="961c8-157">Please note that this is not the real value.</span></span> <span data-ttu-id="961c8-158">È necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="961c8-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="961c8-159">Per ottenere tale valore, contattare il [team di supporto di FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).</span><span class="sxs-lookup"><span data-stu-id="961c8-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="961c8-160">In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il certificato di hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="961c8-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="961c8-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="961c8-162">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="961c8-164">In hello **FreshDesk configurazione** fare clic su **FreshDesk configurare** finestra tooopen Configura sign-on.</span><span class="sxs-lookup"><span data-stu-id="961c8-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="961c8-165">Copiare hello SAML Single Sign-On Service URL e Sign-Out URL da hello **riferimento rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="961c8-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="961c8-167">In un'altra finestra del Web browser accedere al sito aziendale di Freshdesk come amministratore.</span><span class="sxs-lookup"><span data-stu-id="961c8-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="961c8-168">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="961c8-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="961c8-169">![Amministratore](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="961c8-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="961c8-170">In hello **impostazioni generali** scheda, fare clic su **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="961c8-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="961c8-171">![Sicurezza](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="961c8-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="961c8-172">In hello **sicurezza** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="961c8-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="961c8-173">![Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="961c8-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="961c8-174">a.</span><span class="sxs-lookup"><span data-stu-id="961c8-174">a.</span></span> <span data-ttu-id="961c8-175">Per **Single Sign On (SSO)** selezionare **On**.</span><span class="sxs-lookup"><span data-stu-id="961c8-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="961c8-176">b.</span><span class="sxs-lookup"><span data-stu-id="961c8-176">b.</span></span> <span data-ttu-id="961c8-177">Selezionare **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="961c8-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="961c8-178">c.</span><span class="sxs-lookup"><span data-stu-id="961c8-178">c.</span></span> <span data-ttu-id="961c8-179">Hello tipo **SAML Single Sign-On Service URL** copiati dal portale Azure nel hello **SAML Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="961c8-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="961c8-180">d.</span><span class="sxs-lookup"><span data-stu-id="961c8-180">d.</span></span> <span data-ttu-id="961c8-181">Hello tipo **Sign-Out URL** copiati dal portale Azure nel hello **Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="961c8-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="961c8-182">e.</span><span class="sxs-lookup"><span data-stu-id="961c8-182">e.</span></span> <span data-ttu-id="961c8-183">Hello copia **identificazione personale** valore dal certificato hello scaricato dal portale di Azure e incollarlo in hello **Security Certificate Fingerprint** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="961c8-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="961c8-184">Per ulteriori informazioni, vedere [come tooretrieve il valore di identificazione personale del certificato](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="961c8-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="961c8-185">f.</span><span class="sxs-lookup"><span data-stu-id="961c8-185">f.</span></span> <span data-ttu-id="961c8-186">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="961c8-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="961c8-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="961c8-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="961c8-188">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="961c8-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="961c8-190">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="961c8-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="961c8-191">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="961c8-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="961c8-193">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="961c8-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="961c8-195">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="961c8-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="961c8-197">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="961c8-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="961c8-199">a.</span><span class="sxs-lookup"><span data-stu-id="961c8-199">a.</span></span> <span data-ttu-id="961c8-200">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="961c8-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="961c8-201">b.</span><span class="sxs-lookup"><span data-stu-id="961c8-201">b.</span></span> <span data-ttu-id="961c8-202">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="961c8-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="961c8-203">c.</span><span class="sxs-lookup"><span data-stu-id="961c8-203">c.</span></span> <span data-ttu-id="961c8-204">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="961c8-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="961c8-205">d.</span><span class="sxs-lookup"><span data-stu-id="961c8-205">d.</span></span> <span data-ttu-id="961c8-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="961c8-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="961c8-207">Creazione di un utente test di FreshDesk</span><span class="sxs-lookup"><span data-stu-id="961c8-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="961c8-208">In ordine tooenable Azure AD utenti toolog a FreshDesk, è necessario eseguirne il provisioning in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="961c8-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="961c8-209">Nel caso di hello di FreshDesk, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="961c8-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="961c8-210">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="961c8-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="961c8-211">Accedi tooyour **Freshdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="961c8-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="961c8-212">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="961c8-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="961c8-213">![Amministratore](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="961c8-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="961c8-214">In hello **impostazioni generali** scheda, fare clic su **agenti**.</span><span class="sxs-lookup"><span data-stu-id="961c8-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="961c8-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span><span class="sxs-lookup"><span data-stu-id="961c8-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="961c8-216">Fare clic su **New Agent**.</span><span class="sxs-lookup"><span data-stu-id="961c8-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="961c8-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span><span class="sxs-lookup"><span data-stu-id="961c8-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="961c8-218">Nella finestra di dialogo informazioni sull'agente hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="961c8-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="961c8-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span><span class="sxs-lookup"><span data-stu-id="961c8-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="961c8-220">a.</span><span class="sxs-lookup"><span data-stu-id="961c8-220">a.</span></span> <span data-ttu-id="961c8-221">In hello **nome completo** casella di testo Nome hello del tipo di account di Azure AD hello si vuole tooprovision.</span><span class="sxs-lookup"><span data-stu-id="961c8-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="961c8-222">b.</span><span class="sxs-lookup"><span data-stu-id="961c8-222">b.</span></span> <span data-ttu-id="961c8-223">In hello **posta elettronica** casella di testo, hello tipo AD Azure indirizzo di posta elettronica dell'account di Azure AD hello si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="961c8-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="961c8-224">c.</span><span class="sxs-lookup"><span data-stu-id="961c8-224">c.</span></span> <span data-ttu-id="961c8-225">In hello **titolo** casella di testo, titolo hello tipo di account di Azure AD hello si vuole tooprovision.</span><span class="sxs-lookup"><span data-stu-id="961c8-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="961c8-226">d.</span><span class="sxs-lookup"><span data-stu-id="961c8-226">d.</span></span> <span data-ttu-id="961c8-227">Selezionare **Agents role** e quindi fare clic su **Assign**.</span><span class="sxs-lookup"><span data-stu-id="961c8-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="961c8-228">e.</span><span class="sxs-lookup"><span data-stu-id="961c8-228">e.</span></span> <span data-ttu-id="961c8-229">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="961c8-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="961c8-230">titolare dell'account di Azure AD di Hello riceverà un messaggio di posta elettronica che include un account di hello tooconfirm collegamento prima dell'effettiva attivazione.</span><span class="sxs-lookup"><span data-stu-id="961c8-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="961c8-231">È possibile usare qualsiasi altro Freshdesk utente account strumento di creazione o le API fornite da Freshdesk tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="961c8-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="961c8-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="961c8-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="961c8-233">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="961c8-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="961c8-234">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooBox proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="961c8-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Assegna utente][200] 

<span data-ttu-id="961c8-236">**tooassign Britta Simon tooFreshDesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="961c8-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="961c8-237">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="961c8-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="961c8-239">Nell'elenco di applicazioni hello, selezionare **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="961c8-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="961c8-241">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="961c8-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="961c8-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="961c8-243">Click **Add** button.</span></span> <span data-ttu-id="961c8-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="961c8-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="961c8-246">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="961c8-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="961c8-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="961c8-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="961c8-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="961c8-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="961c8-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="961c8-249">Testing single sign-on</span></span>

<span data-ttu-id="961c8-250">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="961c8-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="961c8-251">Quando si fa clic su riquadro FreshDesk hello in hello Pannello di accesso, è necessario ottenere l'account di accesso pagina tooget connesso tooyour freshservice.</span><span class="sxs-lookup"><span data-stu-id="961c8-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="961c8-252">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="961c8-252">Additional resources</span></span>

* [<span data-ttu-id="961c8-253">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="961c8-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="961c8-254">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="961c8-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png


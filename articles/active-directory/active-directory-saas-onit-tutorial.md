---
title: 'Esercitazione: Integrazione di Azure Active Directory con Onit | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Onit.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="e2916-103">Esercitazione: Integrazione di Azure Active Directory con Onit</span><span class="sxs-lookup"><span data-stu-id="e2916-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="e2916-104">In questa esercitazione, è illustrato come toointegrate Onit con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2916-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2916-105">Integrazione di Onit con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e2916-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e2916-106">È possibile controllare in Azure AD che ha accesso tooOnit.</span><span class="sxs-lookup"><span data-stu-id="e2916-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="e2916-107">È possibile abilitare l'utenti tooautomatically get connesso tooOnit (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2916-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e2916-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2916-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e2916-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2916-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2916-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e2916-110">Prerequisites</span></span>

<span data-ttu-id="e2916-111">integrazione di Azure AD con Onit tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e2916-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="e2916-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2916-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2916-113">Sottoscrizione di Onit abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e2916-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2916-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e2916-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2916-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e2916-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2916-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e2916-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2916-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2916-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2916-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e2916-118">Scenario description</span></span>

<span data-ttu-id="e2916-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e2916-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2916-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e2916-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2916-121">Aggiunta di Onit dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e2916-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="e2916-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2916-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="e2916-123">Aggiunta di Onit dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e2916-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="e2916-124">integrazione hello tooconfigure di Onit in Azure AD, è necessario tooadd Onit dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e2916-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e2916-125">**tooadd Onit dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e2916-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2916-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e2916-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="e2916-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e2916-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e2916-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e2916-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="e2916-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e2916-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="e2916-133">Nella casella di ricerca hello, digitare **Onit**selezionare **Onit** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e2916-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e2916-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2916-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e2916-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Onit usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e2916-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e2916-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Onit è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2916-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="e2916-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Onit richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e2916-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="e2916-139">In Onit, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="e2916-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e2916-140">tooconfigure e prova AD Azure single sign-on con Onit, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e2916-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e2916-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e2916-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e2916-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2916-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2916-143">**[Creare un utente test Onit](#create-an-onit-test-user)**  -toohave un equivalente di Britta Simon in Onit che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e2916-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2916-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e2916-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2916-145">**[Testare single sign-on](#test-single-sign-on)**  tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e2916-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e2916-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2916-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e2916-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Onit.</span><span class="sxs-lookup"><span data-stu-id="e2916-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="e2916-148">**Azure AD tooconfigure single sign-on con Onit, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e2916-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2916-149">Nel portale di Azure su hello hello **Onit** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e2916-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="e2916-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e2916-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="e2916-153">In hello **Onit dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e2916-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="e2916-155">a.</span><span class="sxs-lookup"><span data-stu-id="e2916-155">a.</span></span> <span data-ttu-id="e2916-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="e2916-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="e2916-157">b.</span><span class="sxs-lookup"><span data-stu-id="e2916-157">b.</span></span> <span data-ttu-id="e2916-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="e2916-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e2916-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="e2916-159">These values are not real.</span></span> <span data-ttu-id="e2916-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="e2916-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e2916-161">Contatto [team di supporto Client di Onit](https://www.onit.com/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="e2916-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="e2916-162">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="e2916-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="e2916-164">Applicazione Onit prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="e2916-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e2916-165">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="e2916-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="e2916-166">È possibile gestire i valori hello di questi attributi da hello **"Atrribute"** scheda dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e2916-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="e2916-167">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="e2916-167">hello following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="e2916-169">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e2916-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="e2916-170">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="e2916-170">Attribute Name</span></span> | <span data-ttu-id="e2916-171">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="e2916-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e2916-172">email</span><span class="sxs-lookup"><span data-stu-id="e2916-172">email</span></span> | <span data-ttu-id="e2916-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="e2916-173">user.mail</span></span> |
    
    <span data-ttu-id="e2916-174">a.</span><span class="sxs-lookup"><span data-stu-id="e2916-174">a.</span></span> <span data-ttu-id="e2916-175">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e2916-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e2916-178">b.</span><span class="sxs-lookup"><span data-stu-id="e2916-178">b.</span></span> <span data-ttu-id="e2916-179">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="e2916-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="e2916-180">c.</span><span class="sxs-lookup"><span data-stu-id="e2916-180">c.</span></span> <span data-ttu-id="e2916-181">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="e2916-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="e2916-182">d.</span><span class="sxs-lookup"><span data-stu-id="e2916-182">d.</span></span> <span data-ttu-id="e2916-183">Lasciare hello **Namespace** vuoto.</span><span class="sxs-lookup"><span data-stu-id="e2916-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="e2916-184">e.</span><span class="sxs-lookup"><span data-stu-id="e2916-184">e.</span></span> <span data-ttu-id="e2916-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2916-185">Click **Ok**.</span></span>

7. <span data-ttu-id="e2916-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e2916-186">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e2916-188">In hello **Onit configurazione** fare clic su **configurare Onit** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="e2916-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e2916-189">Hello copia **Sign-Out URL, SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="e2916-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="e2916-191">In un'altra finestra del Web browser accedere al sito aziendale di Onit come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e2916-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="e2916-192">Scegliere dal menu hello in primo piano hello **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="e2916-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="e2916-193">![Amministrazione](./media/active-directory-saas-onit-tutorial/IC791174.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="e2916-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="e2916-194">Fare clic su **Edit Corporation**.</span><span class="sxs-lookup"><span data-stu-id="e2916-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="e2916-195">![Modificare l'azienda](./media/active-directory-saas-onit-tutorial/IC791175.png "Modificare l'azienda")</span><span class="sxs-lookup"><span data-stu-id="e2916-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="e2916-196">Fare clic su hello **sicurezza** scheda.</span><span class="sxs-lookup"><span data-stu-id="e2916-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="e2916-197">![Modificare le informazioni sulla società](./media/active-directory-saas-onit-tutorial/IC791176.png "Modificare le informazioni sulla società")</span><span class="sxs-lookup"><span data-stu-id="e2916-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="e2916-198">In hello **sicurezza** effettuare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e2916-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="e2916-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e2916-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="e2916-200">a.</span><span class="sxs-lookup"><span data-stu-id="e2916-200">a.</span></span> <span data-ttu-id="e2916-201">Come **strategia di autenticazione** selezionare **Single Sign-On e password**.</span><span class="sxs-lookup"><span data-stu-id="e2916-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="e2916-202">b.</span><span class="sxs-lookup"><span data-stu-id="e2916-202">b.</span></span> <span data-ttu-id="e2916-203">In **Idp Target URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2916-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e2916-204">c.</span><span class="sxs-lookup"><span data-stu-id="e2916-204">c.</span></span> <span data-ttu-id="e2916-205">In **Idp logout URL** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2916-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e2916-206">d.</span><span class="sxs-lookup"><span data-stu-id="e2916-206">d.</span></span> <span data-ttu-id="e2916-207">In **Idp Cert Fingerprint (SHA1)** casella di testo, incollare hello **identificazione personale** valore del certificato, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2916-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="e2916-208">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="e2916-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e2916-209">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="e2916-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e2916-210">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2916-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e2916-211">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2916-211">Create an Azure AD test user</span></span>

<span data-ttu-id="e2916-212">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e2916-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="e2916-214">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e2916-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2916-215">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e2916-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e2916-217">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e2916-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e2916-219">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e2916-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e2916-221">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e2916-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e2916-223">a.</span><span class="sxs-lookup"><span data-stu-id="e2916-223">a.</span></span> <span data-ttu-id="e2916-224">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2916-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2916-225">b.</span><span class="sxs-lookup"><span data-stu-id="e2916-225">b.</span></span> <span data-ttu-id="e2916-226">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2916-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e2916-227">c.</span><span class="sxs-lookup"><span data-stu-id="e2916-227">c.</span></span> <span data-ttu-id="e2916-228">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="e2916-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e2916-229">d.</span><span class="sxs-lookup"><span data-stu-id="e2916-229">d.</span></span> <span data-ttu-id="e2916-230">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e2916-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="e2916-231">Creare un utente di test di Onit</span><span class="sxs-lookup"><span data-stu-id="e2916-231">Create an Onit test user</span></span>

<span data-ttu-id="e2916-232">In ordine tooenable Azure AD utenti toolog a Onit, è necessario eseguirne il provisioning in Onit.</span><span class="sxs-lookup"><span data-stu-id="e2916-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="e2916-233">Nel caso di hello di Onit, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="e2916-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="e2916-234">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e2916-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2916-235">Accesso tooyour **Onit** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e2916-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="e2916-236">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="e2916-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="e2916-237">![Amministrazione](./media/active-directory-saas-onit-tutorial/IC791180.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="e2916-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="e2916-238">In hello **Aggiungi utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e2916-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="e2916-239">![Aggiungere un utente](./media/active-directory-saas-onit-tutorial/IC791181.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="e2916-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="e2916-240">Hello tipo **nome** hello e **indirizzo di posta elettronica** di Azure un valido relative all'account di Active Directory desiderata tooprovision in hello nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="e2916-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="e2916-241">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e2916-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="e2916-242">titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="e2916-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e2916-243">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2916-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e2916-244">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooOnit.</span><span class="sxs-lookup"><span data-stu-id="e2916-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="e2916-246">**tooassign Britta Simon tooOnit, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e2916-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2916-247">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e2916-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e2916-249">Nell'elenco di applicazioni hello, selezionare **Onit**.</span><span class="sxs-lookup"><span data-stu-id="e2916-249">In hello applications list, select **Onit**.</span></span>

    ![collegamento di Onit Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="e2916-251">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e2916-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="e2916-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e2916-253">Click **Add** button.</span></span> <span data-ttu-id="e2916-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e2916-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="e2916-256">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="e2916-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e2916-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e2916-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2916-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e2916-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e2916-259">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e2916-259">Test single sign-on</span></span>

<span data-ttu-id="e2916-260">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e2916-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e2916-261">Quando si fa clic su riquadro Onit hello in hello Pannello di accesso, è necessario ottenere l'applicazione Onit tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="e2916-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="e2916-262">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e2916-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e2916-263">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e2916-263">Additional resources</span></span>

* [<span data-ttu-id="e2916-264">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2916-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2916-265">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2916-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png


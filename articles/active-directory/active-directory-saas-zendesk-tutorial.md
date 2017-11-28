---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zendesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Zendesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="59a2d-103">Esercitazione: Integrazione di Azure Active Directory con Zendesk</span><span class="sxs-lookup"><span data-stu-id="59a2d-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="59a2d-104">In questa esercitazione, è illustrato come toointegrate Zendesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59a2d-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59a2d-105">Integrazione di Zendesk con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="59a2d-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59a2d-106">È possibile controllare in Azure AD che ha accesso tooZendesk</span><span class="sxs-lookup"><span data-stu-id="59a2d-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="59a2d-107">È possibile abilitare l'utenti tooautomatically get connesso tooZendesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="59a2d-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59a2d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="59a2d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="59a2d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59a2d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59a2d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="59a2d-110">Prerequisites</span></span>

<span data-ttu-id="59a2d-111">integrazione di Azure AD con Zendesk tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="59a2d-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="59a2d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59a2d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59a2d-113">Zendesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="59a2d-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="59a2d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="59a2d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="59a2d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="59a2d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59a2d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="59a2d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59a2d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59a2d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="59a2d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="59a2d-118">Scenario description</span></span>
<span data-ttu-id="59a2d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="59a2d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59a2d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="59a2d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59a2d-121">Aggiunta di Zendesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="59a2d-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="59a2d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59a2d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="59a2d-123">Aggiunta di Zendesk dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="59a2d-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="59a2d-124">integrazione hello tooconfigure di Zendesk in Azure AD, è necessario tooadd Zendesk dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="59a2d-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59a2d-125">**tooadd Zendesk dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59a2d-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59a2d-126">In hello  **[portale Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="59a2d-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="59a2d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59a2d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="59a2d-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="59a2d-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="59a2d-133">Nella casella di ricerca hello, digitare **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-133">In hello search box, type **Zendesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="59a2d-135">Nel riquadro dei risultati hello, selezionare **Zendesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="59a2d-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59a2d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59a2d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59a2d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zendesk in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="59a2d-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59a2d-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zendesk è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59a2d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="59a2d-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Zendesk richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="59a2d-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="59a2d-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Zendesk.</span><span class="sxs-lookup"><span data-stu-id="59a2d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="59a2d-142">tooconfigure e test Azure single sign-on AD con Zendesk, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="59a2d-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59a2d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="59a2d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59a2d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59a2d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59a2d-145">**[Creazione di un utente test Zendesk](#creating-a-zendesk-test-user)**  -toohave un equivalente di Britta Simon in Zendesk che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="59a2d-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59a2d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="59a2d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59a2d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="59a2d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59a2d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59a2d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59a2d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Zendesk.</span><span class="sxs-lookup"><span data-stu-id="59a2d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="59a2d-150">**Azure AD tooconfigure single sign-on con Zendesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59a2d-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="59a2d-151">Nel portale di Azure su hello hello **Zendesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="59a2d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="59a2d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="59a2d-155">In hello **Zendesk dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="59a2d-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="59a2d-157">a.</span><span class="sxs-lookup"><span data-stu-id="59a2d-157">a.</span></span> <span data-ttu-id="59a2d-158">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="59a2d-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="59a2d-159">b.</span><span class="sxs-lookup"><span data-stu-id="59a2d-159">b.</span></span> <span data-ttu-id="59a2d-160">In hello **identificatore** casella di testo, valore di tipo hello utilizzando hello modello:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="59a2d-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59a2d-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="59a2d-161">These values are not real.</span></span> <span data-ttu-id="59a2d-162">Aggiornare questi valori con URL hello effettivo Sign-on e URL dell'identificatore.</span><span class="sxs-lookup"><span data-stu-id="59a2d-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="59a2d-163">Contatto [team di supporto di Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="59a2d-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="59a2d-164">Zendesk prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="59a2d-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="59a2d-165">Non sono presenti attributi SAML obbligatori ma facoltativamente è possibile aggiungere un attributo da **gli attributi utente** sezione hello seguente passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="59a2d-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="59a2d-167">a.</span><span class="sxs-lookup"><span data-stu-id="59a2d-167">a.</span></span> <span data-ttu-id="59a2d-168">Fare clic su hello **visualizzare e modificare tutti gli altri attributi di hello** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="59a2d-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="59a2d-170">b.</span><span class="sxs-lookup"><span data-stu-id="59a2d-170">b.</span></span> <span data-ttu-id="59a2d-171">Fare clic su hello **Aggiungi attributo** tooopen **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="59a2d-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="59a2d-173">c.</span><span class="sxs-lookup"><span data-stu-id="59a2d-173">c.</span></span> <span data-ttu-id="59a2d-174">In hello **nome** casella di testo, nome dell'attributo di tipo hello (ad esempio **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="59a2d-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="59a2d-175">d.</span><span class="sxs-lookup"><span data-stu-id="59a2d-175">d.</span></span> <span data-ttu-id="59a2d-176">Da hello **valore** elenco, il valore di attributo selezionare hello (come **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="59a2d-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="59a2d-177">e.</span><span class="sxs-lookup"><span data-stu-id="59a2d-177">e.</span></span> <span data-ttu-id="59a2d-178">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="59a2d-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="59a2d-179">Utilizzare gli attributi tooadd gli attributi dell'estensione che non sono in Azure AD per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="59a2d-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="59a2d-180">Fare clic su [gli attributi utente che possono essere impostati in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget elenco completo di hello di SAML attributi che **Zendesk** accetta.</span><span class="sxs-lookup"><span data-stu-id="59a2d-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="59a2d-181">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="59a2d-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="59a2d-183">In hello **Zendesk configurazione** fare clic su **configurare Zendesk** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="59a2d-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="59a2d-184">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="59a2d-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="59a2d-186">In un'altra finestra del Web browser accedere al sito aziendale di Zendesk come amministratore.</span><span class="sxs-lookup"><span data-stu-id="59a2d-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="59a2d-187">Fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-187">Click **Admin**.</span></span>

9. <span data-ttu-id="59a2d-188">Nel riquadro di spostamento a sinistra di hello, fare clic su **impostazioni**, quindi fare clic su **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="59a2d-189">In hello **sicurezza** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="59a2d-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="59a2d-190">![Sicurezza](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="59a2d-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="59a2d-191">![Single Sign-On](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="59a2d-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="59a2d-192">a.</span><span class="sxs-lookup"><span data-stu-id="59a2d-192">a.</span></span> <span data-ttu-id="59a2d-193">Fare clic su hello **Admin & agenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="59a2d-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="59a2d-194">b.</span><span class="sxs-lookup"><span data-stu-id="59a2d-194">b.</span></span> <span data-ttu-id="59a2d-195">Selezionare **Single sign-on (SSO) e SAML** e quindi **SAML**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="59a2d-196">c.</span><span class="sxs-lookup"><span data-stu-id="59a2d-196">c.</span></span> <span data-ttu-id="59a2d-197">In **URL SSO SAML** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="59a2d-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="59a2d-198">d.</span><span class="sxs-lookup"><span data-stu-id="59a2d-198">d.</span></span> <span data-ttu-id="59a2d-199">In **URL disconnessione remota** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="59a2d-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="59a2d-200">e.</span><span class="sxs-lookup"><span data-stu-id="59a2d-200">e.</span></span> <span data-ttu-id="59a2d-201">In **Certificate Fingerprint** casella di testo, incollare hello **identificazione personale** valore del certificato che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="59a2d-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="59a2d-202">f.</span><span class="sxs-lookup"><span data-stu-id="59a2d-202">f.</span></span> <span data-ttu-id="59a2d-203">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59a2d-204">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="59a2d-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="59a2d-205">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="59a2d-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="59a2d-207">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59a2d-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59a2d-208">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="59a2d-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59a2d-210">elenco di hello toodisplay utenti andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59a2d-212">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="59a2d-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59a2d-214">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="59a2d-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59a2d-216">a.</span><span class="sxs-lookup"><span data-stu-id="59a2d-216">a.</span></span> <span data-ttu-id="59a2d-217">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59a2d-218">b.</span><span class="sxs-lookup"><span data-stu-id="59a2d-218">b.</span></span> <span data-ttu-id="59a2d-219">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59a2d-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59a2d-220">c.</span><span class="sxs-lookup"><span data-stu-id="59a2d-220">c.</span></span> <span data-ttu-id="59a2d-221">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="59a2d-222">d.</span><span class="sxs-lookup"><span data-stu-id="59a2d-222">d.</span></span> <span data-ttu-id="59a2d-223">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="59a2d-224">Creazione di un utente test Zendesk</span><span class="sxs-lookup"><span data-stu-id="59a2d-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="59a2d-225">Azure AD tooenable utenti toolog in **Zendesk**, è necessario eseguirne il provisioning in **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="59a2d-226">A seconda del ruolo di hello nelle App hello, hello è previsto il comportamento:</span><span class="sxs-lookup"><span data-stu-id="59a2d-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="59a2d-227">All'accesso viene eseguito automaticamente il provisioning degli account dell'**utente finale**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="59a2d-228">**Agente** e **Admin** account necessitano toobe manualmente il provisioning **Zendesk** prima dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="59a2d-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="59a2d-229">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59a2d-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="59a2d-230">Accedi tooyour **Zendesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="59a2d-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="59a2d-231">Seleziona hello **un elenco di clienti** scheda.</span><span class="sxs-lookup"><span data-stu-id="59a2d-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="59a2d-232">Seleziona hello **utente** scheda e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="59a2d-233">![Aggiungere un utente](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="59a2d-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="59a2d-234">Digitare l'indirizzo di posta elettronica hello di un account di Azure AD esistente si desidera tooprovision e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="59a2d-235">![Nuovo utente](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="59a2d-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="59a2d-236">È possibile usare qualsiasi altro Zendesk utente account strumento di creazione o qualsiasi API fornita da Zendesk tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="59a2d-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="59a2d-237">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="59a2d-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="59a2d-238">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZendesk.</span><span class="sxs-lookup"><span data-stu-id="59a2d-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Assegna utente][200] 

<span data-ttu-id="59a2d-240">**tooassign Britta Simon tooZendesk, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="59a2d-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="59a2d-241">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="59a2d-243">Nell'elenco di applicazioni hello, selezionare **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-243">In hello applications list, select **Zendesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="59a2d-245">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="59a2d-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-247">Click **Add** button.</span></span> <span data-ttu-id="59a2d-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="59a2d-250">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="59a2d-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59a2d-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59a2d-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="59a2d-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59a2d-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="59a2d-253">Testing single sign-on</span></span>

<span data-ttu-id="59a2d-254">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="59a2d-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="59a2d-255">Quando si fa clic su riquadro Zendesk hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Zendesk applicazione.</span><span class="sxs-lookup"><span data-stu-id="59a2d-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="59a2d-256">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59a2d-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59a2d-257">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="59a2d-257">Additional resources</span></span>

* [<span data-ttu-id="59a2d-258">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59a2d-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59a2d-259">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59a2d-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png

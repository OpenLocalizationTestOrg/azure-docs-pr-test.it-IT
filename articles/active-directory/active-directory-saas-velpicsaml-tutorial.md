---
title: 'Esercitazione: Integrazione di Azure Active Directory con Velpic SAML| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Velpic SAML.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="16047-103">Esercitazione: Integrazione di Azure Active Directory con Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="16047-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="16047-104">In questa esercitazione, è illustrato come toointegrate Velpic SAML con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16047-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16047-105">Integrazione Velpic SAML con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="16047-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="16047-106">È possibile controllare in Azure AD che ha accesso tooVelpic SAML</span><span class="sxs-lookup"><span data-stu-id="16047-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="16047-107">È possibile abilitare l'utenti tooautomatically get connesso tooVelpic SAML (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="16047-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16047-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="16047-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="16047-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16047-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16047-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="16047-110">Prerequisites</span></span>

<span data-ttu-id="16047-111">integrazione di Azure AD con SAML Velpic tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="16047-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="16047-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16047-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16047-113">Sottoscrizione di Velpic SAML abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="16047-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16047-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="16047-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16047-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="16047-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16047-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="16047-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="16047-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16047-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16047-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="16047-118">Scenario description</span></span>
<span data-ttu-id="16047-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="16047-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16047-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="16047-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16047-121">Aggiunta di SAML Velpic dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="16047-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="16047-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="16047-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="16047-123">Aggiunta di SAML Velpic dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="16047-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="16047-124">integrazione hello tooconfigure di Velpic SAML in Azure AD, è necessario tooadd Velpic SAML dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="16047-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="16047-125">**tooadd Velpic SAML dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="16047-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="16047-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="16047-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16047-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="16047-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="16047-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="16047-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="16047-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="16047-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="16047-133">Nella casella di ricerca hello, digitare **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="16047-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="16047-135">Nel riquadro dei risultati hello, selezionare **Velpic SAML**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="16047-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16047-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="16047-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16047-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Velpic SAML in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="16047-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16047-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Velpic SAML è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16047-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="16047-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Velpic SAML deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="16047-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="16047-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="16047-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="16047-142">tooconfigure e prova AD Azure single sign-on con Velpic SAML, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="16047-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="16047-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="16047-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="16047-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16047-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16047-145">**[Creazione di un utente test SAML Velpic](#creating-a-velpic-saml-test-user)**  -toohave un equivalente di Britta Simon in SAML Velpic toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="16047-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="16047-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="16047-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16047-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="16047-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16047-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="16047-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16047-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on SAML Velpic nell'applicazione in uso.</span><span class="sxs-lookup"><span data-stu-id="16047-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="16047-150">**Azure AD tooconfigure single sign-on con Velpic SAML, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="16047-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="16047-151">Nel portale di gestione di Azure hello in hello **Velpic SAML** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="16047-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="16047-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="16047-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="16047-155">Immettere i dettagli di hello in hello **Velpic SAML dominio e gli URL** sezione -</span><span class="sxs-lookup"><span data-stu-id="16047-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="16047-157">a.</span><span class="sxs-lookup"><span data-stu-id="16047-157">a.</span></span> <span data-ttu-id="16047-158">In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="16047-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="16047-159">b.</span><span class="sxs-lookup"><span data-stu-id="16047-159">b.</span></span> <span data-ttu-id="16047-160">In hello **identificatore** casella di testo, incollare hello **'Single sign-on URL'** valore`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="16047-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="16047-161">Si noti che hello URL di accesso verrà fornita dai team Velpic SAML hello e valore dell'identificatore sarà disponibile quando si configura hello SSO di plug-in sul lato Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="16047-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="16047-162">È necessario toocopy che il valore dalla pagina dell'applicazione Velpic SAML e incollarlo qui.</span><span class="sxs-lookup"><span data-stu-id="16047-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="16047-163">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="16047-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="16047-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="16047-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="16047-167">Nella sezione di configurazione di SAML Velpic hello, scegliere Configura SAML Velpic tooopen Configura sign-on finestra.</span><span class="sxs-lookup"><span data-stu-id="16047-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="16047-168">Copiare hello ID entità SAML dalla sezione di riferimento rapido hello.</span><span class="sxs-lookup"><span data-stu-id="16047-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="16047-169">In un'altra finestra del Web browser accedere al sito aziendale di Velpic SAML come amministratore.</span><span class="sxs-lookup"><span data-stu-id="16047-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="16047-170">Fare clic su **Gestisci** scheda e andare troppo**integrazione** sezione in cui è necessario tooclick in **plug-in** pulsante toocreate nuovo plug-in per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="16047-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="16047-172">Fare clic su hello **'Aggiungi plug-in'** pulsante.</span><span class="sxs-lookup"><span data-stu-id="16047-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="16047-174">Fare clic su hello **SAML** riquadro nella pagina Aggiungi plug-in di hello.</span><span class="sxs-lookup"><span data-stu-id="16047-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="16047-176">Immettere il nome di hello di hello nuovo SAML plug-in e fare clic su hello **'Add'** pulsante.</span><span class="sxs-lookup"><span data-stu-id="16047-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="16047-178">Immettere i dettagli di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="16047-178">Enter hello details as follows:</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="16047-180">a.</span><span class="sxs-lookup"><span data-stu-id="16047-180">a.</span></span> <span data-ttu-id="16047-181">In hello **nome** casella di testo Nome hello del tipo di plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="16047-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="16047-182">b.</span><span class="sxs-lookup"><span data-stu-id="16047-182">b.</span></span> <span data-ttu-id="16047-183">In hello **URL autorità di certificazione** casella di testo, incollare hello **ID entità SAML** copiato dalla hello **Configura sign-on** finestra di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="16047-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="16047-184">c.</span><span class="sxs-lookup"><span data-stu-id="16047-184">c.</span></span> <span data-ttu-id="16047-185">In hello **configurazione di Provider di metadati** caricare hello file Metadata XML che è stato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="16047-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="16047-186">d.</span><span class="sxs-lookup"><span data-stu-id="16047-186">d.</span></span> <span data-ttu-id="16047-187">È anche possibile scegliere tooenable SAML appena provisioning in-time abilitando hello **'Automatica consente di creare nuovi utenti'** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="16047-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="16047-188">Se un utente non esiste in Velpic e questo flag non è abilitato, l'account di accesso hello Azure avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="16047-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="16047-189">Se il flag di hello è abilitato hello utente verrà automaticamente essere eseguito il provisioning in Velpic in fase di hello dell'account di accesso.</span><span class="sxs-lookup"><span data-stu-id="16047-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="16047-190">e.</span><span class="sxs-lookup"><span data-stu-id="16047-190">e.</span></span> <span data-ttu-id="16047-191">Hello copia **Single sign-on URL** dalla casella di testo hello e Incolla in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="16047-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="16047-192">f.</span><span class="sxs-lookup"><span data-stu-id="16047-192">f.</span></span> <span data-ttu-id="16047-193">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="16047-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16047-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="16047-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="16047-195">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="16047-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="16047-197">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="16047-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="16047-198">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="16047-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16047-200">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="16047-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16047-202">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="16047-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16047-204">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="16047-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16047-206">a.</span><span class="sxs-lookup"><span data-stu-id="16047-206">a.</span></span> <span data-ttu-id="16047-207">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16047-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16047-208">b.</span><span class="sxs-lookup"><span data-stu-id="16047-208">b.</span></span> <span data-ttu-id="16047-209">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="16047-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16047-210">c.</span><span class="sxs-lookup"><span data-stu-id="16047-210">c.</span></span> <span data-ttu-id="16047-211">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="16047-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="16047-212">d.</span><span class="sxs-lookup"><span data-stu-id="16047-212">d.</span></span> <span data-ttu-id="16047-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="16047-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="16047-214">Creare un utente test di Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="16047-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="16047-215">Questo passaggio non è in genere necessari come un'applicazione hello supporta just-in tempo il provisioning dell'utente.</span><span class="sxs-lookup"><span data-stu-id="16047-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="16047-216">Se non è abilitato il provisioning utente automatico hello quindi la creazione manuale dell'utente può essere eseguita come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="16047-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="16047-217">Accedere al sito aziendale di Velpic SAML come amministratore e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16047-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="16047-218">Fare clic sulla scheda Gestisci passare tooUsers sezione, quindi fare clic su nuovi utenti di tooadd pulsante.</span><span class="sxs-lookup"><span data-stu-id="16047-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![Aggiungi utente](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="16047-220">In hello **"Create New User"** finestra di dialogo eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="16047-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="16047-222">a.</span><span class="sxs-lookup"><span data-stu-id="16047-222">a.</span></span> <span data-ttu-id="16047-223">In hello **nome** casella di testo, hello prima del tipo Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16047-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="16047-224">b.</span><span class="sxs-lookup"><span data-stu-id="16047-224">b.</span></span> <span data-ttu-id="16047-225">In hello **cognome** casella di testo, digitare hello cognome di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16047-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="16047-226">c.</span><span class="sxs-lookup"><span data-stu-id="16047-226">c.</span></span> <span data-ttu-id="16047-227">In hello **nome utente** casella di testo, digitare il nome utente hello di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16047-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="16047-228">d.</span><span class="sxs-lookup"><span data-stu-id="16047-228">d.</span></span> <span data-ttu-id="16047-229">In hello **posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16047-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="16047-230">e.</span><span class="sxs-lookup"><span data-stu-id="16047-230">e.</span></span> <span data-ttu-id="16047-231">Resto delle informazioni di hello è facoltativo, che è possibile inserire se necessario.</span><span class="sxs-lookup"><span data-stu-id="16047-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="16047-232">f.</span><span class="sxs-lookup"><span data-stu-id="16047-232">f.</span></span> <span data-ttu-id="16047-233">Fare clic su **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="16047-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="16047-234">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="16047-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="16047-235">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooVelpic accesso SAML.</span><span class="sxs-lookup"><span data-stu-id="16047-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Assegna utente][200] 

<span data-ttu-id="16047-237">**tooassign Britta Simon tooVelpic SAML, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="16047-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="16047-238">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="16047-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="16047-240">Nell'elenco di applicazioni hello, selezionare **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="16047-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="16047-242">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="16047-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="16047-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="16047-244">Click **Add** button.</span></span> <span data-ttu-id="16047-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="16047-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="16047-247">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="16047-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="16047-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="16047-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16047-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="16047-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16047-250">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="16047-250">Testing single sign-on</span></span>

<span data-ttu-id="16047-251">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="16047-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="16047-252">Quando si fa clic hello Velpic SAML riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="16047-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="16047-253">Dovrebbe essere hello **'Accedi con Azure AD'** pulsante nella pagina di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="16047-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="16047-255">Fare clic su hello **'Accedi con Azure AD'** toolog pulsante in tooVelpic con l'account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16047-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="16047-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="16047-256">Additional resources</span></span>

* [<span data-ttu-id="16047-257">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16047-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16047-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16047-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png


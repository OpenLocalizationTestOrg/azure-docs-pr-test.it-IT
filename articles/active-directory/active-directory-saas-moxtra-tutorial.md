---
title: 'Esercitazione: integrazione di Azure Active Directory con Moxtra | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Moxtra.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="7ecff-103">Esercitazione: integrazione di Azure Active Directory con Moxtra</span><span class="sxs-lookup"><span data-stu-id="7ecff-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="7ecff-104">In questa esercitazione, è illustrato come toointegrate Moxtra con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ecff-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ecff-105">Integrazione Moxtra con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="7ecff-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ecff-106">È possibile controllare in Azure AD che ha accesso tooMoxtra</span><span class="sxs-lookup"><span data-stu-id="7ecff-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="7ecff-107">È possibile abilitare l'utenti tooautomatically get connesso tooMoxtra (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ecff-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ecff-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7ecff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7ecff-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ecff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ecff-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7ecff-110">Prerequisites</span></span>

<span data-ttu-id="7ecff-111">integrazione di Azure AD con Moxtra tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7ecff-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="7ecff-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ecff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ecff-113">Sottoscrizione di Moxtra abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7ecff-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ecff-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="7ecff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ecff-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="7ecff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ecff-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7ecff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ecff-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ecff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ecff-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7ecff-118">Scenario description</span></span>
<span data-ttu-id="7ecff-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7ecff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ecff-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="7ecff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ecff-121">Aggiunta di Moxtra dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7ecff-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="7ecff-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ecff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="7ecff-123">Aggiunta di Moxtra dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7ecff-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="7ecff-124">integrazione hello tooconfigure di Moxtra in Azure AD, è necessario tooadd Moxtra dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7ecff-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ecff-125">**tooadd Moxtra dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ecff-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ecff-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7ecff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ecff-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ecff-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7ecff-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7ecff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7ecff-133">Nella casella di ricerca hello, digitare **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-133">In hello search box, type **Moxtra**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="7ecff-135">Nel riquadro dei risultati hello, selezionare **Moxtra**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7ecff-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ecff-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ecff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ecff-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Moxtra usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7ecff-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ecff-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Moxtra è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ecff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="7ecff-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Moxtra deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="7ecff-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="7ecff-141">In Moxtra, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="7ecff-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7ecff-142">tooconfigure e prova AD Azure single sign-on con Moxtra, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7ecff-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ecff-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7ecff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ecff-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ecff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ecff-145">**[Creazione di un utente test Moxtra](#creating-a-moxtra-test-user)**  -toohave un equivalente di Britta Simon in Moxtra che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7ecff-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ecff-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ecff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ecff-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="7ecff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ecff-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ecff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ecff-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Moxtra.</span><span class="sxs-lookup"><span data-stu-id="7ecff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="7ecff-150">**Azure AD tooconfigure single sign-on con Moxtra, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ecff-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ecff-151">Nel portale di Azure su hello hello **Moxtra** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7ecff-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ecff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="7ecff-155">In hello **Moxtra dominio e gli URL** seguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="7ecff-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="7ecff-157">In hello **Sign-on URL** casella di testo, digitare un URL come:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="7ecff-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="7ecff-158">Applicazione di Moxtra prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="7ecff-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7ecff-159">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ecff-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="7ecff-160">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ecff-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="7ecff-161">Hello seguente schermata illustra un esempio di questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="7ecff-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="7ecff-163">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7ecff-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7ecff-164">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="7ecff-164">Attribute Name</span></span> | <span data-ttu-id="7ecff-165">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="7ecff-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7ecff-166">firstname</span><span class="sxs-lookup"><span data-stu-id="7ecff-166">firstname</span></span> | <span data-ttu-id="7ecff-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7ecff-167">user.givenname</span></span> |
    | <span data-ttu-id="7ecff-168">lastname</span><span class="sxs-lookup"><span data-stu-id="7ecff-168">lastname</span></span> | <span data-ttu-id="7ecff-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="7ecff-169">user.surname</span></span> |
    | <span data-ttu-id="7ecff-170">idpid</span><span class="sxs-lookup"><span data-stu-id="7ecff-170">idpid</span></span>    | <span data-ttu-id="7ecff-171">< ID entità SAML ></span><span class="sxs-lookup"><span data-stu-id="7ecff-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="7ecff-172">valore di Hello **idpid** attributo non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="7ecff-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="7ecff-173">È possibile ottenere il valore effettivo di hello da **riferimento rapido** sezione nel **Moxtra configurazione**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="7ecff-174">a.</span><span class="sxs-lookup"><span data-stu-id="7ecff-174">a.</span></span> <span data-ttu-id="7ecff-175">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7ecff-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="7ecff-177">b.</span><span class="sxs-lookup"><span data-stu-id="7ecff-177">b.</span></span> <span data-ttu-id="7ecff-178">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7ecff-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7ecff-180">c.</span><span class="sxs-lookup"><span data-stu-id="7ecff-180">c.</span></span> <span data-ttu-id="7ecff-181">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7ecff-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="7ecff-182">d.</span><span class="sxs-lookup"><span data-stu-id="7ecff-182">d.</span></span> <span data-ttu-id="7ecff-183">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="7ecff-184">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="7ecff-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="7ecff-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7ecff-186">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7ecff-188">In hello **Moxtra configurazione** fare clic su **configurare Moxtra** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="7ecff-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7ecff-189">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="7ecff-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="7ecff-191">In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour Moxtra.</span><span class="sxs-lookup"><span data-stu-id="7ecff-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="7ecff-192">Nella barra degli strumenti hello hello sinistra, fare clic su **Console di amministrazione > SAML Single Sign-on**, quindi fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="7ecff-194">In hello **SAML** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7ecff-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="7ecff-196">a.</span><span class="sxs-lookup"><span data-stu-id="7ecff-196">a.</span></span> <span data-ttu-id="7ecff-197">In hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="7ecff-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="7ecff-198">b.</span><span class="sxs-lookup"><span data-stu-id="7ecff-198">b.</span></span> <span data-ttu-id="7ecff-199">In hello **IdP Entity ID** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecff-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="7ecff-200">c.</span><span class="sxs-lookup"><span data-stu-id="7ecff-200">c.</span></span> <span data-ttu-id="7ecff-201">In **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecff-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="7ecff-202">d.</span><span class="sxs-lookup"><span data-stu-id="7ecff-202">d.</span></span> <span data-ttu-id="7ecff-203">In hello **AuthnContextClassRef** casella tipo **urn: oasis: nomi: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="7ecff-204">e.</span><span class="sxs-lookup"><span data-stu-id="7ecff-204">e.</span></span> <span data-ttu-id="7ecff-205">In hello **NameID Format** casella tipo **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="7ecff-206">f.</span><span class="sxs-lookup"><span data-stu-id="7ecff-206">f.</span></span> <span data-ttu-id="7ecff-207">Aprire il certificato scaricato dal portale di Azure nel blocco note, copiarne il contenuto di hello e quindi incollarlo hello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="7ecff-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="7ecff-208">g.</span><span class="sxs-lookup"><span data-stu-id="7ecff-208">g.</span></span> <span data-ttu-id="7ecff-209">Nella casella dominio di posta elettronica SAML di hello, digitare il dominio di posta elettronica SAML.</span><span class="sxs-lookup"><span data-stu-id="7ecff-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="7ecff-210">dominio toosee hello passaggi tooverify hello fare clic su hello "**si**" di seguito.</span><span class="sxs-lookup"><span data-stu-id="7ecff-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="7ecff-211">h.</span><span class="sxs-lookup"><span data-stu-id="7ecff-211">h.</span></span> <span data-ttu-id="7ecff-212">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="7ecff-213">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="7ecff-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7ecff-214">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="7ecff-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7ecff-215">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ecff-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ecff-216">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ecff-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ecff-217">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ecff-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7ecff-219">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ecff-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ecff-220">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7ecff-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ecff-222">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ecff-224">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="7ecff-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ecff-226">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7ecff-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ecff-228">a.</span><span class="sxs-lookup"><span data-stu-id="7ecff-228">a.</span></span> <span data-ttu-id="7ecff-229">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ecff-230">b.</span><span class="sxs-lookup"><span data-stu-id="7ecff-230">b.</span></span> <span data-ttu-id="7ecff-231">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ecff-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ecff-232">c.</span><span class="sxs-lookup"><span data-stu-id="7ecff-232">c.</span></span> <span data-ttu-id="7ecff-233">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7ecff-234">d.</span><span class="sxs-lookup"><span data-stu-id="7ecff-234">d.</span></span> <span data-ttu-id="7ecff-235">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="7ecff-236">Creare un utente test Moxtra</span><span class="sxs-lookup"><span data-stu-id="7ecff-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="7ecff-237">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Moxtra toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ecff-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="7ecff-238">**un utente denominato Britta Simon in Moxtra, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ecff-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ecff-239">Accesso tooyour sito della società Moxtra come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7ecff-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="7ecff-240">Nella barra degli strumenti hello hello sinistra, fare clic su **Console di amministrazione > Gestione utente**e quindi **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="7ecff-242">In hello **Aggiungi utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7ecff-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="7ecff-243">a.</span><span class="sxs-lookup"><span data-stu-id="7ecff-243">a.</span></span> <span data-ttu-id="7ecff-244">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="7ecff-245">b.</span><span class="sxs-lookup"><span data-stu-id="7ecff-245">b.</span></span> <span data-ttu-id="7ecff-246">In hello **cognome** casella tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="7ecff-247">c.</span><span class="sxs-lookup"><span data-stu-id="7ecff-247">c.</span></span> <span data-ttu-id="7ecff-248">In hello **posta elettronica** casella Tipo di Laura indirizzo e-mail come portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecff-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="7ecff-249">d.</span><span class="sxs-lookup"><span data-stu-id="7ecff-249">d.</span></span> <span data-ttu-id="7ecff-250">In hello **divisione** casella tipo **Dev**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="7ecff-251">e.</span><span class="sxs-lookup"><span data-stu-id="7ecff-251">e.</span></span> <span data-ttu-id="7ecff-252">In hello **reparto** casella tipo **IT**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="7ecff-253">f.</span><span class="sxs-lookup"><span data-stu-id="7ecff-253">f.</span></span> <span data-ttu-id="7ecff-254">Selezionare **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="7ecff-255">g.</span><span class="sxs-lookup"><span data-stu-id="7ecff-255">g.</span></span> <span data-ttu-id="7ecff-256">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7ecff-257">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ecff-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7ecff-258">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMoxtra.</span><span class="sxs-lookup"><span data-stu-id="7ecff-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7ecff-260">**tooassign Britta Simon tooMoxtra, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ecff-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ecff-261">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7ecff-263">Nell'elenco di applicazioni hello, selezionare **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-263">In hello applications list, select **Moxtra**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="7ecff-265">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7ecff-267">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-267">Click **Add** button.</span></span> <span data-ttu-id="7ecff-268">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7ecff-270">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="7ecff-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ecff-271">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ecff-272">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ecff-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ecff-273">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7ecff-273">Testing single sign-on</span></span>

<span data-ttu-id="7ecff-274">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7ecff-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7ecff-275">Quando si fa clic su riquadro Moxtra hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Moxtra applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ecff-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="7ecff-276">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7ecff-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ecff-277">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7ecff-277">Additional resources</span></span>

* [<span data-ttu-id="7ecff-278">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ecff-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ecff-279">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ecff-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png


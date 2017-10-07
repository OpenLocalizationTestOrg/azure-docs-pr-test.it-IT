---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Elevate| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed elevare il livello di LinkedIn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="d2e42-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="d2e42-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="d2e42-104">In questa esercitazione, è illustrato come toointegrate LinkedIn elevare con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2e42-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2e42-105">Integrazione di elevare il livello di LinkedIn con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d2e42-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d2e42-106">È possibile controllare in Azure AD che ha accesso tooLinkedIn Esegui con privilegi elevati</span><span class="sxs-lookup"><span data-stu-id="d2e42-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="d2e42-107">È possibile abilitare l'utenti tooautomatically get connesso tooLinkedIn Esegui con privilegi elevati (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2e42-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2e42-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d2e42-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d2e42-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2e42-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2e42-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d2e42-110">Prerequisites</span></span>

<span data-ttu-id="d2e42-111">integrazione di Azure AD con LinkedIn elevare tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d2e42-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="d2e42-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2e42-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2e42-113">Sottoscrizione di LinkedIn Elevate abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d2e42-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d2e42-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d2e42-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d2e42-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d2e42-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2e42-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d2e42-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d2e42-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2e42-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2e42-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d2e42-118">Scenario description</span></span>
<span data-ttu-id="d2e42-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d2e42-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2e42-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d2e42-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2e42-121">Aggiunta di LinkedIn elevare dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d2e42-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="d2e42-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2e42-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="d2e42-123">Aggiunta di LinkedIn elevare dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d2e42-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="d2e42-124">integrazione hello tooconfigure di LinkedIn elevare in Azure AD, è necessario tooadd LinkedIn elevare dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d2e42-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d2e42-125">**tooadd LinkedIn elevare dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d2e42-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2e42-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d2e42-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d2e42-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d2e42-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d2e42-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d2e42-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d2e42-133">Nella casella di ricerca hello, digitare **LinkedIn elevare**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="d2e42-134">Dal riquadro dei risultati, fare clic su **LinkedIn elevare** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d2e42-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d2e42-136">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2e42-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d2e42-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Elevate in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d2e42-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d2e42-138">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LinkedIn elevare è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2e42-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="d2e42-139">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello LinkedIn elevare deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d2e42-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="d2e42-140">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in elevare il livello di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="d2e42-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="d2e42-141">tooconfigure e prova AD Azure single sign-on con LinkedIn elevare, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d2e42-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d2e42-142">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d2e42-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d2e42-143">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2e42-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2e42-144">**[Creazione di un utente test LinkedIn elevare](#creating-a-linkedin-elevate-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2e42-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="d2e42-145">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d2e42-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2e42-146">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d2e42-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d2e42-147">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2e42-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d2e42-148">In questa sezione si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione elevare LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="d2e42-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="d2e42-149">**Azure AD tooconfigure single sign-on con LinkedIn elevare, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d2e42-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2e42-150">Nel portale di gestione di Azure hello in hello **LinkedIn elevare** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d2e42-152">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d2e42-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="d2e42-154">In una finestra del web browser, accesso tooyour LinkedIn elevare tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d2e42-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="d2e42-155">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="d2e42-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="d2e42-156">Selezionare inoltre **Elevate - elevare Test AAD** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="d2e42-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="d2e42-158">Fare clic su **o fare clic qui tooload e copia dei singoli campi modulo hello** e copia **Id entità** e **Url asserzione Consumer accesso (ACS)**</span><span class="sxs-lookup"><span data-stu-id="d2e42-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="d2e42-160">Nel portale di Azure, in **LinkedIn elevare il livello di dominio e gli URL**, eseguire i passaggi se si desidera tooconfigure SSO hello in **avviata da IdP** modalità</span><span class="sxs-lookup"><span data-stu-id="d2e42-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="d2e42-162">a.</span><span class="sxs-lookup"><span data-stu-id="d2e42-162">a.</span></span> <span data-ttu-id="d2e42-163">In hello **identificatore** casella di testo immettere hello **ID entità** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="d2e42-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="d2e42-164">b.</span><span class="sxs-lookup"><span data-stu-id="d2e42-164">b.</span></span> <span data-ttu-id="d2e42-165">In hello **URL di risposta** casella di testo immettere hello **Url asserzione Consumer accesso (ACS)** copiata dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="d2e42-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="d2e42-166">Se si desidera tooconfigure SSO in **SP Initiated**, quindi fare clic su Mostra avanzate URL opzione di impostazione nella sezione di configurazione hello e configurare hello accesso URL con modello di hello:</span><span class="sxs-lookup"><span data-stu-id="d2e42-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="d2e42-168">L'applicazione di LinkedIn elevare prevede asserzioni SAML hello in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping tooyour SAML degli attributi del token.</span><span class="sxs-lookup"><span data-stu-id="d2e42-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="d2e42-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="d2e42-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="d2e42-170">il valore predefinito di Hello **identificatore utente** è **User** ma LinkedIn elevare prevede che questo toobe mappato con indirizzo di posta elettronica dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="d2e42-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="d2e42-171">A tale scopo è possibile utilizzare **user.mail** attributo dall'elenco hello o utilizzare il valore di attributo appropriato hello in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d2e42-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="d2e42-173">In **gli attributi utente** fare clic su **visualizzare e modificare tutti gli altri attributi utente** e impostare gli attributi di hello.</span><span class="sxs-lookup"><span data-stu-id="d2e42-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="d2e42-174">È necessario tooadd un'altra attestazione denominata **reparto** e il valore di hello deve toobe mappato troppo**Department**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="d2e42-175">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="d2e42-175">Attribute Name</span></span> | <span data-ttu-id="d2e42-176">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="d2e42-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="d2e42-177">department</span><span class="sxs-lookup"><span data-stu-id="d2e42-177">department</span></span>| <span data-ttu-id="d2e42-178">user.department</span><span class="sxs-lookup"><span data-stu-id="d2e42-178">user.department</span></span> |

      ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="d2e42-180">a.</span><span class="sxs-lookup"><span data-stu-id="d2e42-180">a.</span></span> <span data-ttu-id="d2e42-181">Fare clic su nella pagina dettagli di Aggiungi attributo tooopen hello attributo Aggiungi attributo department hello, come illustrato di seguito</span><span class="sxs-lookup"><span data-stu-id="d2e42-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="d2e42-183">b.</span><span class="sxs-lookup"><span data-stu-id="d2e42-183">b.</span></span> <span data-ttu-id="d2e42-184">Fare clic su **Ok** attributo hello toosave.</span><span class="sxs-lookup"><span data-stu-id="d2e42-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="d2e42-185">c.</span><span class="sxs-lookup"><span data-stu-id="d2e42-185">c.</span></span> <span data-ttu-id="d2e42-186">Modifica nome hello dell'attributo hello **emailaddress** troppo**posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="d2e42-187">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d2e42-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="d2e42-189">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-189">Click **Save**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="d2e42-191">Andare troppo**le impostazioni di amministrazione di LinkedIn** sezione.</span><span class="sxs-lookup"><span data-stu-id="d2e42-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="d2e42-192">Caricare file XML di hello che appena scaricato dal portale di Azure hello facendo clic su hello opzione file caricare XML.</span><span class="sxs-lookup"><span data-stu-id="d2e42-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="d2e42-194">Fare clic su **su** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="d2e42-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="d2e42-195">Stato SSO viene modificato da **non connesso** troppo**connesso**</span><span class="sxs-lookup"><span data-stu-id="d2e42-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d2e42-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2e42-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d2e42-198">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d2e42-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d2e42-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d2e42-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2e42-201">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d2e42-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2e42-203">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d2e42-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2e42-205">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d2e42-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2e42-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d2e42-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2e42-209">a.</span><span class="sxs-lookup"><span data-stu-id="d2e42-209">a.</span></span> <span data-ttu-id="d2e42-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2e42-211">b.</span><span class="sxs-lookup"><span data-stu-id="d2e42-211">b.</span></span> <span data-ttu-id="d2e42-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d2e42-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2e42-213">c.</span><span class="sxs-lookup"><span data-stu-id="d2e42-213">c.</span></span> <span data-ttu-id="d2e42-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d2e42-215">d.</span><span class="sxs-lookup"><span data-stu-id="d2e42-215">d.</span></span> <span data-ttu-id="d2e42-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="d2e42-217">Creare un utente test di LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="d2e42-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="d2e42-218">Applicazione di elevare collegato supporta immediatamente in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti verrà creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d2e42-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="d2e42-219">Nella pagina di impostazioni di amministrazione di hello interruttore hello LinkedIn elevare portale hello capovolto **automaticamente assegnare licenze** tooactive tooenable JIT in fase di provisioning e questo verrà assegnato un utente toohello di licenza.</span><span class="sxs-lookup"><span data-stu-id="d2e42-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d2e42-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2e42-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d2e42-222">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooLinkedIn accesso Esegui con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="d2e42-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d2e42-224">**tooassign Britta Simon tooLinkedIn Esegui con privilegi elevati, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d2e42-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2e42-225">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d2e42-227">Nell'elenco di applicazioni hello, selezionare **LinkedIn elevare**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="d2e42-229">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d2e42-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-231">Click **Add** button.</span></span> <span data-ttu-id="d2e42-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d2e42-234">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d2e42-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d2e42-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2e42-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d2e42-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d2e42-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d2e42-237">Testing single sign-on</span></span>

<span data-ttu-id="d2e42-238">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d2e42-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d2e42-239">Quando si fa clic su riquadro LinkedIn elevare hello in hello Pannello di accesso, è necessario ottenere hello Azure pagina accesso e in a dopo l'esito positivo sign-on, è necessario ottenere LinkedIn elevare nell'applicazione in uso.</span><span class="sxs-lookup"><span data-stu-id="d2e42-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2e42-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d2e42-240">Additional resources</span></span>

* [<span data-ttu-id="d2e42-241">Esercitazione: Configurazione di LinkedIn Elevate per il provisioning utenti automatico con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2e42-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="d2e42-242">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2e42-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2e42-243">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2e42-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png

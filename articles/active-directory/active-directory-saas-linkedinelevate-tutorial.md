---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Elevate| Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e LinkedIn Elevate.
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
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="3a416-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="3a416-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="3a416-104">Questa esercitazione descrive come integrare LinkedIn Elevate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a416-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a416-105">L'integrazione di LinkedIn Elevate con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a416-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a416-106">È possibile controllare in Azure AD chi può accedere a LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="3a416-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="3a416-107">È possibile abilitare gli utenti per l'accesso automatico a LinkedIn Elevate (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a416-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a416-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="3a416-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="3a416-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a416-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a416-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3a416-110">Prerequisites</span></span>

<span data-ttu-id="3a416-111">Per configurare l'integrazione di Azure AD con LinkedIn Elevate sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a416-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="3a416-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a416-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a416-113">Sottoscrizione di LinkedIn Elevate abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3a416-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a416-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3a416-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a416-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a416-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a416-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3a416-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3a416-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a416-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a416-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3a416-118">Scenario description</span></span>
<span data-ttu-id="3a416-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3a416-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a416-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a416-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a416-121">Aggiunta di LinkedIn Elevate dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3a416-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="3a416-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a416-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="3a416-123">Aggiungere LinkedIn Elevate dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3a416-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="3a416-124">Per configurare l'integrazione di LinkedIn Elevate in Azure AD è necessario aggiungere LinkedIn Elevate dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3a416-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a416-125">**Per aggiungere LinkedIn Elevate dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3a416-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a416-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3a416-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a416-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3a416-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a416-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3a416-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3a416-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3a416-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3a416-133">Nella casella di ricerca online digitare **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="3a416-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="3a416-134">Nel riquadro dei risultati fare clic su **LinkedIn Elevate** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3a416-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a416-136">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a416-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a416-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Elevate in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3a416-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a416-138">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di LinkedIn Elevate che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a416-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="3a416-139">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="3a416-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="3a416-140">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (nome utente) in LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="3a416-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="3a416-141">Per configurare e testare l'accesso Single Sign-On di Azure AD con LinkedIn Elevate è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a416-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a416-142">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3a416-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a416-143">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a416-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a416-144">**[Creazione di un utente test di LinkedIn Elevate](#creating-a-linkedin-elevate-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a416-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="3a416-145">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a416-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a416-146">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="3a416-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a416-147">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a416-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a416-148">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="3a416-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="3a416-149">**Per configurare l'accesso Single Sign-On di Azure AD con LinkedIn Elevate seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3a416-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="3a416-150">Nella pagina di integrazione dell'applicazione **LinkedIn Elevate** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3a416-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3a416-152">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3a416-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="3a416-154">In un'altra finestra del Web browser accedere al tenant LinkedIn Elevate come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3a416-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="3a416-155">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="3a416-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="3a416-156">Selezionare anche **Elevate - Elevate AAD Test** (Elevate - Test AAD Elevate) dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="3a416-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="3a416-158">Fare clic su **OR Click Here to load and copy individual fields from the form** (O fare clic qui per caricare e copiare i singoli file dal modulo) e copiare l'**ID entità** e l'**URL ACS (Assertion Consumer Access)**</span><span class="sxs-lookup"><span data-stu-id="3a416-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="3a416-160">Nel portale di Azure, in **URL e dominio LinkedIn Elevate**, attenersi alla procedura seguente per configurare SSO in modalità **avviata da IdP**</span><span class="sxs-lookup"><span data-stu-id="3a416-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="3a416-162">a.</span><span class="sxs-lookup"><span data-stu-id="3a416-162">a.</span></span> <span data-ttu-id="3a416-163">Nella casella di testo **Identificatore** immettere l'**ID entità** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="3a416-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="3a416-164">b.</span><span class="sxs-lookup"><span data-stu-id="3a416-164">b.</span></span> <span data-ttu-id="3a416-165">Nella casella di testo **URL di risposta** immettere l'**URL ACS (Assertion Consumer Access)** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="3a416-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="3a416-166">Se si vuole configurare SSO in modalità **avviata da SP**, scegliere l'opzione Mostra impostazioni URL avanzate nella sezione di configurazione e configurare l'URL di accesso con il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="3a416-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="3a416-168">L'applicazione LinkedIn Elevate richiede le asserzioni SAML in un formato specifico. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="3a416-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="3a416-169">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="3a416-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="3a416-170">Il valore predefinito dell'**ID utente** è **user.userprincipalname** ma LinkedIn Elevate prevede che venga mappato all'indirizzo di posta elettronica dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3a416-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="3a416-171">A tale scopo è possibile usare l'attributo **user.mail** dall'elenco oppure usare il valore di attributo appropriato in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3a416-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="3a416-173">Nella sezione **Attributi utente** fare clic su **Visualizza e modifica tutti gli altri attributi utente** e impostare gli attributi.</span><span class="sxs-lookup"><span data-stu-id="3a416-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="3a416-174">È necessario aggiungere un'altra attestazione denominata **department** e il valore deve essere mappato a **user.department**.</span><span class="sxs-lookup"><span data-stu-id="3a416-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="3a416-175">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="3a416-175">Attribute Name</span></span> | <span data-ttu-id="3a416-176">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="3a416-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="3a416-177">department</span><span class="sxs-lookup"><span data-stu-id="3a416-177">department</span></span>| <span data-ttu-id="3a416-178">user.department</span><span class="sxs-lookup"><span data-stu-id="3a416-178">user.department</span></span> |

      ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="3a416-180">a.</span><span class="sxs-lookup"><span data-stu-id="3a416-180">a.</span></span> <span data-ttu-id="3a416-181">Fare clic su Aggiungi attributo per aprire la pagina dei dettagli dell'attributo e aggiungere l'attributo department come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3a416-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="3a416-183">b.</span><span class="sxs-lookup"><span data-stu-id="3a416-183">b.</span></span> <span data-ttu-id="3a416-184">Fare clic su **Ok** per salvare l'attributo.</span><span class="sxs-lookup"><span data-stu-id="3a416-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="3a416-185">c.</span><span class="sxs-lookup"><span data-stu-id="3a416-185">c.</span></span> <span data-ttu-id="3a416-186">Modificare il nome dell'attributo **emailaddress** in **email**.</span><span class="sxs-lookup"><span data-stu-id="3a416-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="3a416-187">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="3a416-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="3a416-189">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3a416-189">Click **Save**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="3a416-191">Accedere alla sezione **LinkedIn Admin Settings** (Impostazioni di amministrazione LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="3a416-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="3a416-192">Caricare il file XML appena scaricato dal portale di Azure facendo clic sull'opzione Upload XML file (Carica file XML).</span><span class="sxs-lookup"><span data-stu-id="3a416-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="3a416-194">Fare clic su **On** per abilitare SSO.</span><span class="sxs-lookup"><span data-stu-id="3a416-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="3a416-195">Lo stato SSO passa da **Not Connected** (Non connesso) a **Connected** (Connesso)</span><span class="sxs-lookup"><span data-stu-id="3a416-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a416-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a416-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a416-198">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a416-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3a416-200">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3a416-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a416-201">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3a416-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a416-203">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="3a416-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a416-205">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="3a416-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a416-207">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3a416-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a416-209">a.</span><span class="sxs-lookup"><span data-stu-id="3a416-209">a.</span></span> <span data-ttu-id="3a416-210">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a416-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a416-211">b.</span><span class="sxs-lookup"><span data-stu-id="3a416-211">b.</span></span> <span data-ttu-id="3a416-212">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a416-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a416-213">c.</span><span class="sxs-lookup"><span data-stu-id="3a416-213">c.</span></span> <span data-ttu-id="3a416-214">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="3a416-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3a416-215">d.</span><span class="sxs-lookup"><span data-stu-id="3a416-215">d.</span></span> <span data-ttu-id="3a416-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3a416-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="3a416-217">Creare un utente test di LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="3a416-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="3a416-218">L'applicazione LinkedIn Elevate supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti verranno automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3a416-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="3a416-219">Nella pagina delle impostazioni di amministrazione del portale di LinkedIn Elevate spostare il selettore dell'opzione **Automatically Assign licenses** (Assegna automaticamente le licenze) per attivarla. In questo modo si abilita il provisioning just-in-time e si assegna una licenza all'utente.</span><span class="sxs-lookup"><span data-stu-id="3a416-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3a416-221">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a416-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3a416-222">In questa sezione viene concesso a Britta Simon l'accesso a LinkedIn Elevate per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a416-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3a416-224">**Per assegnare Britta Simon a LinkedIn Elevate seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3a416-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="3a416-225">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3a416-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3a416-227">Nell'elenco delle applicazioni selezionare **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="3a416-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="3a416-229">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3a416-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3a416-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3a416-231">Click **Add** button.</span></span> <span data-ttu-id="3a416-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3a416-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3a416-234">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="3a416-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a416-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3a416-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a416-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3a416-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a416-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3a416-237">Testing single sign-on</span></span>

<span data-ttu-id="3a416-238">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3a416-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a416-239">Quando si fa clic sul riquadro LinkedIn Elevate nel Pannello di accesso, viene visualizzata la pagina di accesso di Azure e, se l'accesso ha esito positivo, si accede all'applicazione LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="3a416-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a416-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3a416-240">Additional resources</span></span>

* [<span data-ttu-id="3a416-241">Esercitazione: Configurazione di LinkedIn Elevate per il provisioning utenti automatico con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a416-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="3a416-242">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a416-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a416-243">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a416-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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

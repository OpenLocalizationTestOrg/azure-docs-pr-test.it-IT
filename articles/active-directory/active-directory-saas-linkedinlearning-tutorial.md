---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Learning| Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e LinkedIn Learning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="4f435-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="4f435-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="4f435-104">Questa esercitazione descrive come integrare LinkedIn Learning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f435-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f435-105">L'integrazione di LinkedIn Learning con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f435-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4f435-106">È possibile controllare in Azure AD chi può accedere a LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="4f435-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="4f435-107">È possibile abilitare gli utenti per l'accesso automatico a LinkedIn Learning (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f435-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f435-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f435-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4f435-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f435-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f435-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4f435-110">Prerequisites</span></span>

<span data-ttu-id="4f435-111">Per configurare l'integrazione di Azure AD con LinkedIn Learning sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f435-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="4f435-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f435-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f435-113">Sottoscrizione di LinkedIn Learning abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4f435-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f435-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4f435-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f435-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f435-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f435-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4f435-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f435-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f435-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f435-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4f435-118">Scenario description</span></span>
<span data-ttu-id="4f435-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4f435-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f435-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f435-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f435-121">Aggiunta di LinkedIn Learning dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4f435-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="4f435-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f435-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="4f435-123">Aggiungere LinkedIn Learning dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4f435-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="4f435-124">Per configurare l'integrazione di LinkedIn Learning in Azure AD è necessario aggiungere LinkedIn Learning dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4f435-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4f435-125">**Per aggiungere LinkedIn Learning dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4f435-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4f435-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4f435-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f435-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4f435-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4f435-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4f435-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4f435-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4f435-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4f435-133">Nella casella di ricerca online digitare **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="4f435-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="4f435-134">Nel riquadro dei risultati fare clic su **LinkedIn Learning** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f435-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f435-136">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f435-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f435-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Learning in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4f435-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4f435-138">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di LinkedIn Learning che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f435-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="4f435-139">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4f435-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="4f435-140">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (nome utente) in LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4f435-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="4f435-141">Per configurare e testare l'accesso Single Sign-On di Azure AD con LinkedIn Learning è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f435-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4f435-142">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4f435-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4f435-143">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f435-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f435-144">**[Creazione di un utente test di LinkedIn Learning](#creating-a-linkedin-learning-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f435-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="4f435-145">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f435-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f435-146">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="4f435-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f435-147">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f435-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f435-148">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4f435-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="4f435-149">**Per configurare l'accesso Single Sign-On di Azure AD con LinkedIn Learning seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4f435-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="4f435-150">Nella pagina di integrazione dell'applicazione **LinkedIn Learning** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4f435-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4f435-152">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4f435-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="4f435-154">In un'altra finestra del Web browser accedere al tenant LinkedIn Learning come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4f435-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="4f435-155">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="4f435-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="4f435-156">Selezionare anche **Learning - Default** (Learning - Predefinito) nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="4f435-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="4f435-158">Fare clic su **OR Click Here to load and copy individual fields from the form** (O fare clic qui per caricare e copiare i singoli file dal modulo) e copiare l'**ID entità** e l'**URL ACS (Assertion Consumer Access)**</span><span class="sxs-lookup"><span data-stu-id="4f435-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="4f435-160">Nella sezione **URL e dominio LinkedIn Learning** del portale di Azure seguire questa procedura se si desidera configurare SSO in modalità **avviata da IdP**</span><span class="sxs-lookup"><span data-stu-id="4f435-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="4f435-162">a.</span><span class="sxs-lookup"><span data-stu-id="4f435-162">a.</span></span> <span data-ttu-id="4f435-163">Nella casella di testo **Identificatore** immettere l'**ID entità** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="4f435-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="4f435-164">b.</span><span class="sxs-lookup"><span data-stu-id="4f435-164">b.</span></span> <span data-ttu-id="4f435-165">Nella casella di testo **URL di risposta** immettere l'**URL ACS (Assertion Consumer Access)** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="4f435-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="4f435-166">Se si vuole configurare SSO in modalità **avviata da SP**, scegliere l'opzione Mostra impostazioni URL avanzate nella sezione di configurazione e configurare l'URL di accesso nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="4f435-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="4f435-168">L'applicazione LinkedIn Learning richiede le asserzioni SAML in un formato specifico. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="4f435-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="4f435-169">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="4f435-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="4f435-170">Il valore predefinito dell'**ID utente** è **user.userprincipalname** ma LinkedIn Learning prevede che venga mappato all'indirizzo di posta elettronica dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4f435-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="4f435-171">A tale scopo è possibile usare l'attributo **user.mail** dall'elenco oppure usare il valore di attributo appropriato in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4f435-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="4f435-173">Nella sezione **Attributi utente** fare clic su **Visualizza e modifica tutti gli altri attributi utente** e impostare gli attributi.</span><span class="sxs-lookup"><span data-stu-id="4f435-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="4f435-174">L'utente deve aggiungere quattro attestazioni denominate **email**, **department**, **firstname** e **lastname** e il valore deve essere mappato rispettivamente a **user.mail**, **user.department**, **user.givenname** e **user.surname**</span><span class="sxs-lookup"><span data-stu-id="4f435-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="4f435-175">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="4f435-175">Attribute Name</span></span> | <span data-ttu-id="4f435-176">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="4f435-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="4f435-177">email</span><span class="sxs-lookup"><span data-stu-id="4f435-177">email</span></span>| <span data-ttu-id="4f435-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="4f435-178">user.mail</span></span> |    
    | <span data-ttu-id="4f435-179">department</span><span class="sxs-lookup"><span data-stu-id="4f435-179">department</span></span>| <span data-ttu-id="4f435-180">user.department</span><span class="sxs-lookup"><span data-stu-id="4f435-180">user.department</span></span> |
    | <span data-ttu-id="4f435-181">firstname</span><span class="sxs-lookup"><span data-stu-id="4f435-181">firstname</span></span>| <span data-ttu-id="4f435-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4f435-182">user.givenname</span></span> |
    | <span data-ttu-id="4f435-183">lastname</span><span class="sxs-lookup"><span data-stu-id="4f435-183">lastname</span></span>| <span data-ttu-id="4f435-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="4f435-184">user.surname</span></span> |
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="4f435-186">a.</span><span class="sxs-lookup"><span data-stu-id="4f435-186">a.</span></span> <span data-ttu-id="4f435-187">Fare clic su **Aggiungi attributo** per aprire la relativa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4f435-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="4f435-190">b.</span><span class="sxs-lookup"><span data-stu-id="4f435-190">b.</span></span> <span data-ttu-id="4f435-191">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4f435-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4f435-192">c.</span><span class="sxs-lookup"><span data-stu-id="4f435-192">c.</span></span> <span data-ttu-id="4f435-193">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4f435-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4f435-194">d.</span><span class="sxs-lookup"><span data-stu-id="4f435-194">d.</span></span> <span data-ttu-id="4f435-195">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="4f435-195">Click **Ok**</span></span>

10. <span data-ttu-id="4f435-196">Seguire questa procedura sull'attributo **name**.</span><span class="sxs-lookup"><span data-stu-id="4f435-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="4f435-197">a.</span><span class="sxs-lookup"><span data-stu-id="4f435-197">a.</span></span> <span data-ttu-id="4f435-198">Fare clic sull'attributo per aprire la finestra **Modifica attributo**.</span><span class="sxs-lookup"><span data-stu-id="4f435-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="4f435-200">b.</span><span class="sxs-lookup"><span data-stu-id="4f435-200">b.</span></span> <span data-ttu-id="4f435-201">Eliminare il valore dell'URL dallo **spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="4f435-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="4f435-202">c.</span><span class="sxs-lookup"><span data-stu-id="4f435-202">c.</span></span> <span data-ttu-id="4f435-203">Fare clic su **Ok** per salvare l'impostazione.</span><span class="sxs-lookup"><span data-stu-id="4f435-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="4f435-204">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="4f435-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="4f435-206">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4f435-206">Click **Save**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="4f435-208">Accedere alla sezione **LinkedIn Admin Settings** (Impostazioni di amministrazione LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="4f435-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="4f435-209">Caricare il file XML scaricato dal portale di Azure facendo clic sull'opzione Upload XML file (Carica file XML).</span><span class="sxs-lookup"><span data-stu-id="4f435-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="4f435-211">Fare clic su **On** per abilitare SSO.</span><span class="sxs-lookup"><span data-stu-id="4f435-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="4f435-212">Lo stato SSO passa da **Not Connected** (Non connesso) a **Connected** (Connesso)</span><span class="sxs-lookup"><span data-stu-id="4f435-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f435-214">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f435-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f435-215">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f435-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4f435-217">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4f435-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4f435-218">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4f435-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f435-220">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="4f435-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f435-222">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="4f435-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f435-224">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4f435-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f435-226">a.</span><span class="sxs-lookup"><span data-stu-id="4f435-226">a.</span></span> <span data-ttu-id="4f435-227">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f435-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f435-228">b.</span><span class="sxs-lookup"><span data-stu-id="4f435-228">b.</span></span> <span data-ttu-id="4f435-229">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4f435-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f435-230">c.</span><span class="sxs-lookup"><span data-stu-id="4f435-230">c.</span></span> <span data-ttu-id="4f435-231">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="4f435-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4f435-232">d.</span><span class="sxs-lookup"><span data-stu-id="4f435-232">d.</span></span> <span data-ttu-id="4f435-233">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4f435-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="4f435-234">Creare un utente test di LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="4f435-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="4f435-235">L'applicazione LinkedIn Learning supporta</span><span class="sxs-lookup"><span data-stu-id="4f435-235">Linked Learning Application supports.</span></span> <span data-ttu-id="4f435-236">il provisioning dell'utente Just-In-Time e dopo l'autenticazione gli utenti vengono creati automaticamente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f435-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="4f435-237">Nella pagina delle impostazioni di amministrazione del portale di LinkedIn Learning spostare il selettore dell'opzione **Automatically Assign licenses** (Assegna automaticamente le licenze) per attivarla. In questo modo si abilita il provisioning just-in-time e si assegna una licenza all'utente.</span><span class="sxs-lookup"><span data-stu-id="4f435-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4f435-239">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f435-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4f435-240">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4f435-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4f435-242">**Per assegnare Britta Simon a LinkedIn Learning seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4f435-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="4f435-243">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4f435-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4f435-245">Nell'elenco delle applicazioni selezionare **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="4f435-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="4f435-247">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4f435-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4f435-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4f435-249">Click **Add** button.</span></span> <span data-ttu-id="4f435-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4f435-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4f435-252">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="4f435-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4f435-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4f435-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f435-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4f435-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f435-255">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4f435-255">Testing single sign-on</span></span>

<span data-ttu-id="4f435-256">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4f435-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4f435-257">Quando si fa clic sul riquadro LinkedIn Learning nel Pannello di accesso, viene visualizzata la pagina di accesso di Azure e, se l'accesso ha esito positivo, si accede all'applicazione LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4f435-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f435-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4f435-258">Additional resources</span></span>

* [<span data-ttu-id="4f435-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f435-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f435-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f435-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png
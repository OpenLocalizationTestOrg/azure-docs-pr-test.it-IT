---
title: 'Esercitazione: Integrazione di Azure Active Directory con LinkedIn Sales Navigator | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e LinkedIn Sales Navigator.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="99ccd-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="99ccd-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="99ccd-104">Questa esercitazione descrive come integrare LinkedIn Sales Navigator con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99ccd-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99ccd-105">L'integrazione di LinkedIn Sales Navigator con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="99ccd-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="99ccd-106">È possibile controllare in Azure AD chi può accedere a LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="99ccd-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="99ccd-107">È possibile abilitare gli utenti per l'accesso automatico a LinkedIn Sales Navigator (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ccd-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="99ccd-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="99ccd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="99ccd-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99ccd-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99ccd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="99ccd-110">Prerequisites</span></span>

<span data-ttu-id="99ccd-111">Per configurare l'integrazione di Azure AD con LinkedIn Sales Navigator sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="99ccd-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="99ccd-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ccd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99ccd-113">Sottoscrizione di LinkedIn Sales Navigator abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="99ccd-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="99ccd-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="99ccd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="99ccd-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="99ccd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99ccd-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="99ccd-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="99ccd-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99ccd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99ccd-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="99ccd-118">Scenario description</span></span>
<span data-ttu-id="99ccd-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="99ccd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="99ccd-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="99ccd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99ccd-121">Aggiunta di LinkedIn Sales Navigator dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="99ccd-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="99ccd-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ccd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="99ccd-123">Aggiunta di LinkedIn Sales Navigator dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="99ccd-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="99ccd-124">Per configurare l'integrazione di LinkedIn Sales Navigator in Azure AD è necessario aggiungere LinkedIn Sales Navigator dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="99ccd-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99ccd-125">**Per aggiungere LinkedIn Sales Navigator dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="99ccd-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99ccd-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="99ccd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="99ccd-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="99ccd-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="99ccd-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="99ccd-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="99ccd-133">Nella casella di ricerca digitare **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="99ccd-135">Nel pannello dei risultati selezionare **LinkedIn Sales Navigator** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="99ccd-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99ccd-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ccd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99ccd-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Sales Navigator in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99ccd-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99ccd-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di LinkedIn Sales Navigator che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ccd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="99ccd-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="99ccd-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="99ccd-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** in Azure AD come valore dell'attributo **Username** in LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="99ccd-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="99ccd-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con LinkedIn Sales Navigator è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="99ccd-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99ccd-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="99ccd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99ccd-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99ccd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99ccd-145">**[Creazione di un utente di test LinkedIn Sales Navigator](#creating-a-linkedin-sales-navigator-test-user)**: per avere una controparte di Britta Simon in LinkedIn Sales Navigator collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ccd-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="99ccd-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ccd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99ccd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="99ccd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99ccd-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ccd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="99ccd-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="99ccd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="99ccd-150">**Per configurare l'accesso Single Sign-On di Azure AD con LinkedIn Sales Navigator seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="99ccd-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="99ccd-151">Nella pagina di integrazione dell'applicazione **LinkedIn Sales Navigator** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="99ccd-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="99ccd-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="99ccd-155">In un'altra finestra del Web browser accedere al sito Web di **LinkedIn Sales Navigator** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="99ccd-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="99ccd-156">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="99ccd-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="99ccd-157">Selezionare **Sales Navigator** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="99ccd-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="99ccd-159">Fare clic su **OR Click Here to load and copy individual fields from the form** (O fare clic qui per caricare e copiare i singoli file dal modulo) e copiare l'**ID entità** e l'**URL ACS (Assertion Consumer Access)**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="99ccd-161">Nella sezione **URL e dominio LinkedIn Sales Navigator** del portale di Azure seguire questa procedura se si desidera configurare l'applicazione in modalità avviata da **IDP**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="99ccd-163">a.</span><span class="sxs-lookup"><span data-stu-id="99ccd-163">a.</span></span> <span data-ttu-id="99ccd-164">Nella casella di testo **Identificatore** immettere l'**ID entità** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="99ccd-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="99ccd-165">b.</span><span class="sxs-lookup"><span data-stu-id="99ccd-165">b.</span></span> <span data-ttu-id="99ccd-166">Nella casella di testo **URL di risposta** immettere l'**URL ACS (Assertion Consumer Access)** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="99ccd-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="99ccd-167">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="99ccd-169">Nella casella di testo **URL di accesso** digitare il valore usando il modello seguente: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="99ccd-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="99ccd-170">L'applicazione **LinkedIn Sales Navigator** richiede le asserzioni SAML in un formato specifico. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="99ccd-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="99ccd-171">La schermata seguente mostra un esempio.</span><span class="sxs-lookup"><span data-stu-id="99ccd-171">The following screenshot shows an example.</span></span> <span data-ttu-id="99ccd-172">Il valore predefinito dell'**ID utente** è **user.userprincipalname** ma LinkedIn Sales Navigator prevede che venga mappato all'indirizzo di posta elettronica dell'utente.</span><span class="sxs-lookup"><span data-stu-id="99ccd-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="99ccd-173">È possibile usare l'attributo **user.mail** dall'elenco oppure usare il valore di attributo appropriato in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="99ccd-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="99ccd-175">Nella sezione **Attributi utente** fare clic su **Visualizza e modifica tutti gli altri attributi utente** e impostare gli attributi.</span><span class="sxs-lookup"><span data-stu-id="99ccd-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="99ccd-176">L'utente deve aggiungere quattro attestazioni denominate **email**, **department**, **firstname** e **lastname** e il valore deve essere mappato rispettivamente a **user.mail**, **user.department**, **user.givenname** e **user.surname**</span><span class="sxs-lookup"><span data-stu-id="99ccd-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="99ccd-177">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="99ccd-177">Attribute Name</span></span> | <span data-ttu-id="99ccd-178">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="99ccd-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="99ccd-179">email</span><span class="sxs-lookup"><span data-stu-id="99ccd-179">email</span></span>| <span data-ttu-id="99ccd-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="99ccd-180">user.mail</span></span> |
    | <span data-ttu-id="99ccd-181">department</span><span class="sxs-lookup"><span data-stu-id="99ccd-181">department</span></span>| <span data-ttu-id="99ccd-182">user.department</span><span class="sxs-lookup"><span data-stu-id="99ccd-182">user.department</span></span> |
    | <span data-ttu-id="99ccd-183">firstname</span><span class="sxs-lookup"><span data-stu-id="99ccd-183">firstname</span></span>| <span data-ttu-id="99ccd-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="99ccd-184">user.givenname</span></span> |
    | <span data-ttu-id="99ccd-185">lastname</span><span class="sxs-lookup"><span data-stu-id="99ccd-185">lastname</span></span>| <span data-ttu-id="99ccd-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="99ccd-186">user.surname</span></span> |
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="99ccd-188">a.</span><span class="sxs-lookup"><span data-stu-id="99ccd-188">a.</span></span> <span data-ttu-id="99ccd-189">Fare clic su **Aggiungi attributo** per aprire la relativa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="99ccd-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="99ccd-192">b.</span><span class="sxs-lookup"><span data-stu-id="99ccd-192">b.</span></span> <span data-ttu-id="99ccd-193">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="99ccd-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="99ccd-194">c.</span><span class="sxs-lookup"><span data-stu-id="99ccd-194">c.</span></span> <span data-ttu-id="99ccd-195">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="99ccd-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="99ccd-196">d.</span><span class="sxs-lookup"><span data-stu-id="99ccd-196">d.</span></span> <span data-ttu-id="99ccd-197">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="99ccd-197">Click **Ok**</span></span>

10. <span data-ttu-id="99ccd-198">Seguire questa procedura sull'attributo **name**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="99ccd-199">a.</span><span class="sxs-lookup"><span data-stu-id="99ccd-199">a.</span></span> <span data-ttu-id="99ccd-200">Fare clic sull'attributo per aprire la finestra **Modifica attributo**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="99ccd-202">b.</span><span class="sxs-lookup"><span data-stu-id="99ccd-202">b.</span></span> <span data-ttu-id="99ccd-203">Eliminare il valore dell'URL dallo **spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="99ccd-204">c.</span><span class="sxs-lookup"><span data-stu-id="99ccd-204">c.</span></span> <span data-ttu-id="99ccd-205">Fare clic su **Ok** per salvare l'impostazione.</span><span class="sxs-lookup"><span data-stu-id="99ccd-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="99ccd-206">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="99ccd-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="99ccd-208">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="99ccd-208">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="99ccd-210">Accedere alla sezione **LinkedIn Admin Settings** (Impostazioni di amministrazione LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="99ccd-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="99ccd-211">Fare clic su **Upload XML file** (Carica file XML) per caricare il file di metadati XML scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="99ccd-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="99ccd-213">Fare clic su **On** per abilitare SSO.</span><span class="sxs-lookup"><span data-stu-id="99ccd-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="99ccd-214">Lo stato SSO passa da **Not Connected** (Non connesso) a **Connected** (Connesso)</span><span class="sxs-lookup"><span data-stu-id="99ccd-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="99ccd-216">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="99ccd-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="99ccd-217">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="99ccd-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="99ccd-218">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99ccd-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99ccd-219">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ccd-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="99ccd-220">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="99ccd-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="99ccd-222">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="99ccd-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99ccd-223">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="99ccd-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="99ccd-225">Fare clic **Utenti e gruppi** e su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="99ccd-227">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="99ccd-229">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="99ccd-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="99ccd-231">a.</span><span class="sxs-lookup"><span data-stu-id="99ccd-231">a.</span></span> <span data-ttu-id="99ccd-232">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99ccd-233">b.</span><span class="sxs-lookup"><span data-stu-id="99ccd-233">b.</span></span> <span data-ttu-id="99ccd-234">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="99ccd-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="99ccd-235">c.</span><span class="sxs-lookup"><span data-stu-id="99ccd-235">c.</span></span> <span data-ttu-id="99ccd-236">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="99ccd-237">d.</span><span class="sxs-lookup"><span data-stu-id="99ccd-237">d.</span></span> <span data-ttu-id="99ccd-238">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="99ccd-239">Creazione di un utente test di LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="99ccd-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="99ccd-240">L'applicazione Linked Sales Navigator supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti verranno automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="99ccd-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="99ccd-241">Attivare l'**assegnazione automatica delle licenze** per assegnare una licenza all'utente.</span><span class="sxs-lookup"><span data-stu-id="99ccd-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="99ccd-243">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ccd-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="99ccd-244">In questa sezione viene concesso a Britta Simon l'accesso a LinkedIn Sales Navigator per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="99ccd-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Assegna utente][200] 

<span data-ttu-id="99ccd-246">**Per assegnare Britta Simon a LinkedIn Sales Navigator seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="99ccd-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="99ccd-247">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="99ccd-249">Nell'elenco delle applicazioni selezionare **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="99ccd-251">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="99ccd-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="99ccd-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-253">Click **Add** button.</span></span> <span data-ttu-id="99ccd-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="99ccd-256">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="99ccd-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="99ccd-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="99ccd-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="99ccd-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="99ccd-259">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="99ccd-259">Testing single sign-on</span></span>

<span data-ttu-id="99ccd-260">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="99ccd-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="99ccd-261">Quando si fa clic sul riquadro LinkedIn Sales Navigator nel pannello di accesso, si viene reindirizzati alla pagina dell'organizzazione, nella quale è necessario fornire i dettagli dell'account LinkedIn personale.</span><span class="sxs-lookup"><span data-stu-id="99ccd-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="99ccd-262">In questo modo l'account personale viene collegato all'account aziendale di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="99ccd-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="99ccd-263">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="99ccd-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="99ccd-264">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="99ccd-264">Additional resources</span></span>

* [<span data-ttu-id="99ccd-265">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99ccd-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99ccd-266">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99ccd-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png


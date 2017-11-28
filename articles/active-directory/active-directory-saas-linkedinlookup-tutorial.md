---
title: 'Esercitazione: integrazione di Azure Active Directory con LinkedIn Lookup| Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e LinkedIn Lookup.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="7dd23-103">Esercitazione: Integrazione di Azure Active Directory con LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="7dd23-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="7dd23-104">Questa esercitazione descrive come integrare LinkedIn Lookup con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7dd23-104">In this tutorial, you learn how to integrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7dd23-105">L'integrazione di LinkedIn Lookup con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7dd23-105">Integrating LinkedIn Lookup with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7dd23-106">È possibile controllare in Azure AD chi può accedere a LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="7dd23-106">You can control in Azure AD who has access to LinkedIn Lookup</span></span>
- <span data-ttu-id="7dd23-107">È possibile abilitare gli utenti per l'accesso automatico a LinkedIn Lookup (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd23-107">You can enable your users to automatically get signed-on to LinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7dd23-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7dd23-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7dd23-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7dd23-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dd23-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7dd23-110">Prerequisites</span></span>

<span data-ttu-id="7dd23-111">Per configurare l'integrazione di Azure AD con LinkedIn Lookup sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7dd23-111">To configure Azure AD integration with LinkedIn Lookup, you need the following items:</span></span>

- <span data-ttu-id="7dd23-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dd23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7dd23-113">Sottoscrizione di LinkedIn Lookup abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7dd23-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7dd23-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7dd23-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7dd23-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7dd23-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7dd23-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7dd23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7dd23-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7dd23-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7dd23-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7dd23-118">Scenario description</span></span>
<span data-ttu-id="7dd23-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7dd23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7dd23-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7dd23-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7dd23-121">Aggiungere LinkedIn Lookup dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7dd23-121">Adding LinkedIn Lookup from the gallery</span></span>
2. <span data-ttu-id="7dd23-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-the-gallery"></a><span data-ttu-id="7dd23-123">Aggiungere LinkedIn Lookup dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7dd23-123">Adding LinkedIn Lookup from the gallery</span></span>
<span data-ttu-id="7dd23-124">Per configurare l'integrazione di LinkedIn Lookup in Azure AD è necessario aggiungere LinkedIn Lookup dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7dd23-124">To configure the integration of LinkedIn Lookup into Azure AD, you need to add LinkedIn Lookup from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7dd23-125">**Per aggiungere LinkedIn Lookup dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7dd23-125">**To add LinkedIn Lookup from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd23-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7dd23-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7dd23-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7dd23-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7dd23-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="7dd23-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7dd23-133">Nella casella di ricerca online digitare **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-133">In the search box, type **LinkedIn Lookup**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="7dd23-135">Nel pannello dei risultati selezionare **LinkedIn Lookup** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7dd23-135">In the results panel, select **LinkedIn Lookup**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7dd23-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7dd23-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LinkedIn Lookup in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7dd23-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7dd23-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di LinkedIn Lookup che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dd23-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Lookup is to a user in Azure AD.</span></span> <span data-ttu-id="7dd23-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="7dd23-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Lookup needs to be established.</span></span>

<span data-ttu-id="7dd23-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (nome utente) in LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="7dd23-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="7dd23-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con LinkedIn Lookup è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7dd23-142">To configure and test Azure AD single sign-on with LinkedIn Lookup, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7dd23-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7dd23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7dd23-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7dd23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7dd23-145">**[Creazione di un utente test di LinkedIn Lookup](#creating-an-linkedin-lookup-test-user)**: per avere una controparte di Britta Simon in LinkedIn Lookup collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dd23-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - to have a counterpart of Britta Simon in LinkedIn Lookup that is linked to the Azure AD representation.</span></span>
4. <span data-ttu-id="7dd23-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dd23-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7dd23-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7dd23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7dd23-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7dd23-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="7dd23-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="7dd23-150">**Per configurare l'accesso Single Sign-On di Azure AD con LinkedIn Lookup seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7dd23-150">**To configure Azure AD single sign-on with LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd23-151">Nella pagina di integrazione dell'applicazione **LinkedIn Lookup** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-151">In the Azure portal, on the **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7dd23-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7dd23-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="7dd23-155">In un'altra finestra del Web browser accedere al sito Web di **LinkedIn Lookup** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7dd23-155">In a different web browser window, sign-on to your **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="7dd23-156">In **Account Center** (Centro account) fare clic su **Global Settings** (Impostazioni globali) in **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="7dd23-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="7dd23-157">Selezionare anche **Lookup** (Cerca) nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="7dd23-157">Also, select **Lookup** from the dropdown list.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="7dd23-159">Fare clic su **OR Click Here to load and copy individual fields from the form** (O fare clic qui per caricare e copiare i singoli file dal modulo) e copiare l'**ID entità** e l'**URL ACS (Assertion Consumer Access)**</span><span class="sxs-lookup"><span data-stu-id="7dd23-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="7dd23-161">Nella sezione **URL e dominio LinkedIn Lookup** del portale di Azure seguire questa procedura se si desidera configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="7dd23-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="7dd23-163">a.</span><span class="sxs-lookup"><span data-stu-id="7dd23-163">a.</span></span> <span data-ttu-id="7dd23-164">Nella casella di testo **Identificatore** immettere l'**ID entità** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="7dd23-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="7dd23-165">b.</span><span class="sxs-lookup"><span data-stu-id="7dd23-165">b.</span></span> <span data-ttu-id="7dd23-166">Nella casella di testo **URL di risposta** immettere l'**URL ACS (Assertion Consumer Access)** copiato dal portale di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="7dd23-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="7dd23-167">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="7dd23-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="7dd23-169">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="7dd23-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7dd23-170">Questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="7dd23-170">This is not real value.</span></span> <span data-ttu-id="7dd23-171">L'utente deve aggiornare questi valori con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="7dd23-171">The user has to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="7dd23-172">Per ottenere tale valore, contattare il [team di supporto di LinkedIn Lookup](https://business.LinkedIn.com/lookup).</span><span class="sxs-lookup"><span data-stu-id="7dd23-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) to get this value.</span></span>

8. <span data-ttu-id="7dd23-173">L'applicazione **LinkedIn Lookup** si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="7dd23-173">Your **LinkedIn Lookup** application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7dd23-174">L'utente deve aggiungere dei mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="7dd23-174">The user has to add custom attribute mappings to the SAML token attributes configuration.</span></span> <span data-ttu-id="7dd23-175">La schermata seguente mostra un esempio.</span><span class="sxs-lookup"><span data-stu-id="7dd23-175">The following screenshot shows an example.</span></span> <span data-ttu-id="7dd23-176">Il valore predefinito dell'**ID utente** è **user.userprincipalname** ma LinkedIn Lookup prevede che venga mappato all'indirizzo di posta elettronica dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7dd23-176">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="7dd23-177">È possibile usare l'attributo **user.mail** dall'elenco oppure usare il valore di attributo appropriato in base alla configurazione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7dd23-177">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="7dd23-179">Nella sezione **Attributi utente** fare clic su **Visualizza e modifica tutti gli altri attributi utente** e impostare gli attributi.</span><span class="sxs-lookup"><span data-stu-id="7dd23-179">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="7dd23-180">L'utente deve aggiungere quattro attestazioni denominate **email**,  **department**, **firstname** e **lastname** e il valore deve essere mappato rispettivamente a **user.mail**, **user.department**, **user.givenname** e **user.surname**</span><span class="sxs-lookup"><span data-stu-id="7dd23-180">The user needs to add four claims named **email**,  **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="7dd23-181">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="7dd23-181">Attribute Name</span></span> | <span data-ttu-id="7dd23-182">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="7dd23-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7dd23-183">email</span><span class="sxs-lookup"><span data-stu-id="7dd23-183">email</span></span>| <span data-ttu-id="7dd23-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="7dd23-184">user.mail</span></span> |    
    | <span data-ttu-id="7dd23-185">department</span><span class="sxs-lookup"><span data-stu-id="7dd23-185">department</span></span>| <span data-ttu-id="7dd23-186">user.department</span><span class="sxs-lookup"><span data-stu-id="7dd23-186">user.department</span></span> |
    | <span data-ttu-id="7dd23-187">firstname</span><span class="sxs-lookup"><span data-stu-id="7dd23-187">firstname</span></span>| <span data-ttu-id="7dd23-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7dd23-188">user.givenname</span></span> |
    | <span data-ttu-id="7dd23-189">lastname</span><span class="sxs-lookup"><span data-stu-id="7dd23-189">lastname</span></span>| <span data-ttu-id="7dd23-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="7dd23-190">user.surname</span></span> |

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="7dd23-192">a.</span><span class="sxs-lookup"><span data-stu-id="7dd23-192">a.</span></span> <span data-ttu-id="7dd23-193">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-193">Click **Add Attribute** to open the **Add Attribute** dialog.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="7dd23-196">b.</span><span class="sxs-lookup"><span data-stu-id="7dd23-196">b.</span></span> <span data-ttu-id="7dd23-197">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7dd23-197">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7dd23-198">c.</span><span class="sxs-lookup"><span data-stu-id="7dd23-198">c.</span></span> <span data-ttu-id="7dd23-199">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7dd23-199">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7dd23-200">d.</span><span class="sxs-lookup"><span data-stu-id="7dd23-200">d.</span></span> <span data-ttu-id="7dd23-201">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="7dd23-201">Click **Ok**</span></span>

10. <span data-ttu-id="7dd23-202">Seguire questa procedura sull'attributo **name**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-202">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="7dd23-203">a.</span><span class="sxs-lookup"><span data-stu-id="7dd23-203">a.</span></span> <span data-ttu-id="7dd23-204">Fare clic sull'attributo per aprire la finestra **Modifica attributo**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-204">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="7dd23-206">b.</span><span class="sxs-lookup"><span data-stu-id="7dd23-206">b.</span></span> <span data-ttu-id="7dd23-207">Eliminare il valore dell'URL dallo **spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-207">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="7dd23-208">c.</span><span class="sxs-lookup"><span data-stu-id="7dd23-208">c.</span></span> <span data-ttu-id="7dd23-209">Fare clic su **Ok** per salvare l'impostazione.</span><span class="sxs-lookup"><span data-stu-id="7dd23-209">Click **Ok** to save the setting.</span></span>

10. <span data-ttu-id="7dd23-210">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="7dd23-210">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="7dd23-212">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7dd23-212">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="7dd23-214">Accedere alla sezione **LinkedIn Admin Settings** (Impostazioni di amministrazione LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="7dd23-214">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="7dd23-215">Caricare il file XML scaricato dal portale di Azure facendo clic sull'opzione **Upload XML file** (Carica file XML).</span><span class="sxs-lookup"><span data-stu-id="7dd23-215">Upload the XML file you downloaded from the Azure portal by clicking the **Upload XML file** option.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="7dd23-217">Fare clic su **On** per abilitare SSO.</span><span class="sxs-lookup"><span data-stu-id="7dd23-217">Click **On** to enable SSO.</span></span> <span data-ttu-id="7dd23-218">Lo stato SSO passa da **Not Connected** (Non connesso) a **Connected** (Connesso)</span><span class="sxs-lookup"><span data-stu-id="7dd23-218">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="7dd23-220">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7dd23-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7dd23-221">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="7dd23-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7dd23-222">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7dd23-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7dd23-223">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd23-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="7dd23-224">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd23-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7dd23-226">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7dd23-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd23-227">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7dd23-227">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7dd23-229">Fare clic **Utenti e gruppi** e su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-229">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7dd23-231">Fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-231">Click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7dd23-233">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7dd23-233">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7dd23-235">a.</span><span class="sxs-lookup"><span data-stu-id="7dd23-235">a.</span></span> <span data-ttu-id="7dd23-236">Nella casella di testo **Name** (Nome) digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-236">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="7dd23-237">b.</span><span class="sxs-lookup"><span data-stu-id="7dd23-237">b.</span></span> <span data-ttu-id="7dd23-238">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7dd23-238">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="7dd23-239">c.</span><span class="sxs-lookup"><span data-stu-id="7dd23-239">c.</span></span> <span data-ttu-id="7dd23-240">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-240">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7dd23-241">d.</span><span class="sxs-lookup"><span data-stu-id="7dd23-241">d.</span></span> <span data-ttu-id="7dd23-242">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="7dd23-243">Creazione di un utente test di LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="7dd23-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="7dd23-244">L'applicazione Linked Lookup supporta il provisioning dell'utente just-in-time (JIT) e dopo l'autenticazione gli utenti verranno automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7dd23-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="7dd23-245">Attivare l'**assegnazione automatica delle licenze** per assegnare una licenza all'utente.</span><span class="sxs-lookup"><span data-stu-id="7dd23-245">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7dd23-247">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7dd23-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7dd23-248">In questa sezione viene concesso a Britta Simon l'accesso a LinkedIn Lookup per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd23-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Lookup.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7dd23-250">**Per assegnare Britta Simon a LinkedIn Lookup seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7dd23-250">**To assign Britta Simon to LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="7dd23-251">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7dd23-253">Nell'elenco delle applicazioni selezionare **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-253">In the applications list, select **LinkedIn Lookup**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="7dd23-255">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7dd23-255">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7dd23-257">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-257">Click **Add** button.</span></span> <span data-ttu-id="7dd23-258">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7dd23-260">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7dd23-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7dd23-261">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7dd23-262">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7dd23-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7dd23-263">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7dd23-263">Testing single sign-on</span></span>

<span data-ttu-id="7dd23-264">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7dd23-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7dd23-265">Quando si fa clic sul riquadro LinkedIn Lookup nel pannello di accesso, si viene reindirizzati alla pagina dell'organizzazione, nella quale è necessario fornire i dettagli dell'account LinkedIn personale.</span><span class="sxs-lookup"><span data-stu-id="7dd23-265">When you click the LinkedIn Lookup tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="7dd23-266">In questo modo l'account personale viene collegato all'account aziendale di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="7dd23-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="7dd23-267">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7dd23-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7dd23-268">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7dd23-268">Additional resources</span></span>

* [<span data-ttu-id="7dd23-269">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7dd23-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7dd23-270">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7dd23-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png


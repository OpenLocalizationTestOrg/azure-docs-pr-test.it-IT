---
title: 'Esercitazione: Integrazione di Azure Active Directory con ScaleX Enterprise | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ScaleX Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="85713-103">Esercitazione: Integrazione di Azure Active Directory con ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="85713-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="85713-104">Questa esercitazione descrive come integrare ScaleX Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85713-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85713-105">L'integrazione di ScaleX Enterprise con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="85713-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="85713-106">È possibile controllare in Azure AD chi può accedere a ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="85713-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="85713-107">È possibile abilitare gli utenti per l'accesso automatico a ScaleX Enterprise (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="85713-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85713-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="85713-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="85713-109">Per altre informazioni sull'integrazione di app SaaS con Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="85713-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="85713-110">Informazioni sull'accesso alle applicazioni e Single Sign-On con [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85713-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85713-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="85713-111">Prerequisites</span></span>

<span data-ttu-id="85713-112">Per configurare l'integrazione di Azure AD con ScaleX Enterprise, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="85713-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="85713-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85713-113">An Azure AD subscription</span></span>
- <span data-ttu-id="85713-114">Sottoscrizione di ScaleX Enterprise abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="85713-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85713-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="85713-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85713-116">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="85713-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85713-117">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="85713-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="85713-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85713-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85713-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="85713-119">Scenario description</span></span>
<span data-ttu-id="85713-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="85713-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85713-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="85713-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85713-122">Aggiunta di ScaleX Enterprise dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="85713-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="85713-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85713-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="85713-124">Aggiunta di ScaleX Enterprise dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="85713-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="85713-125">Per configurare l'integrazione di ScaleX Enterprise in Azure AD, è necessario aggiungere ScaleX Enterprise dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="85713-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="85713-126">**Per aggiungere ScaleX Enterprise dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="85713-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="85713-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="85713-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85713-129">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="85713-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="85713-130">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="85713-130">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="85713-132">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="85713-132">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="85713-134">Nella casella di ricerca digitare **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="85713-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="85713-136">Nel pannello dei risultati selezionare **ScaleX Enterprise** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85713-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85713-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85713-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85713-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ScaleX Enterprise con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85713-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="85713-140">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di ScaleX Enterprise che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85713-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="85713-141">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="85713-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="85713-142">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **nome utente** in ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="85713-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="85713-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con ScaleX Enterprise, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="85713-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="85713-144">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="85713-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="85713-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85713-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85713-146">**[Creazione di un utente test di ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**: per avere una controparte di Britta Simon in ScaleX Enterprise collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85713-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="85713-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85713-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85713-148">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="85713-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85713-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85713-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85713-150">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="85713-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="85713-151">**Per configurare l'accesso Single Sign-On di Azure AD con ScaleX Enterprise, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="85713-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="85713-152">Nella pagina di integrazione dell'applicazione **ScaleX Enterprise** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="85713-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="85713-154">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="85713-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="85713-156">Nella sezione **URL e dominio ScaleX Enterprise**, se si vuole configurare l'applicazione in modalità avviata da **IDP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="85713-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="85713-158">a.</span><span class="sxs-lookup"><span data-stu-id="85713-158">a.</span></span> <span data-ttu-id="85713-159">Nella casella di testo **Identificatore** digitare il valore adottando il modello seguente: `https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="85713-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="85713-160">b.</span><span class="sxs-lookup"><span data-stu-id="85713-160">b.</span></span> <span data-ttu-id="85713-161">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="85713-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="85713-162">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="85713-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="85713-164">Nella casella di testo **URL di accesso** digitare il valore usando il modello seguente: `https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="85713-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="85713-165">Questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="85713-165">These are not the real values.</span></span> <span data-ttu-id="85713-166">Aggiornare questi valori con l'identificatore, l'URL di risposta o l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="85713-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="85713-167">Per ottenere questi valori, contattare il [team di supporto clienti di ScaleX Enterprise](http://info.rescale.com/contact_sales).</span><span class="sxs-lookup"><span data-stu-id="85713-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="85713-168">L'applicazione ScaleX prevede un formato specifico per le asserzioni SAML. È quindi necessario modificare mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="85713-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="85713-169">Fare clic sulla casella di controllo **Visualizza e modifica tutti gli altri attributi utente** per aprire le impostazioni degli attributi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="85713-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="85713-171">a.</span><span class="sxs-lookup"><span data-stu-id="85713-171">a.</span></span> <span data-ttu-id="85713-172">Fare clic con il pulsante destro del mouse sul **nome** attributo, quindi fare clic su Elimina.</span><span class="sxs-lookup"><span data-stu-id="85713-172">Right click the attribute **name** and click delete.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="85713-174">b.</span><span class="sxs-lookup"><span data-stu-id="85713-174">b.</span></span> <span data-ttu-id="85713-175">Fare clic sull'attributo **emailaddress** per aprire la finestra Modifica attributo.</span><span class="sxs-lookup"><span data-stu-id="85713-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="85713-176">Modificare il relativo valore da **user.mail** a **user.userprincipalname** e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="85713-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="85713-178">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="85713-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="85713-180">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="85713-180">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="85713-182">Nella sezione **Configurazione di ScaleX Enterprise** fare clic su **Configura ScaleX Enterprise** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="85713-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="85713-183">Copiare l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="85713-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="85713-185">Per configurare l'accesso Single Sign-On sul lato **ScaleX Enterprise**, accedere al sito Web aziendale di ScaleX Enterprise come amministratore.</span><span class="sxs-lookup"><span data-stu-id="85713-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="85713-186">Fare clic sul menu in alto a destra e seleziona **Contoso Administration** (Amministrazione Contoso).</span><span class="sxs-lookup"><span data-stu-id="85713-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85713-187">Contoso è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="85713-187">Contoso is just an example.</span></span> <span data-ttu-id="85713-188">Deve essere il nome effettivo della società.</span><span class="sxs-lookup"><span data-stu-id="85713-188">This should be your actual Company Name.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="85713-190">Selezionare **Integrations** (Integrazioni) nel menu superiore e selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="85713-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="85713-192">Compilare il modulo come segue:</span><span class="sxs-lookup"><span data-stu-id="85713-192">Complete the form as follows:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="85713-194">a.</span><span class="sxs-lookup"><span data-stu-id="85713-194">a.</span></span> <span data-ttu-id="85713-195">Selezionare **Create any user who can authenticate with SSO** (Crea un utente qualsiasi che può eseguire l'autenticazione con SSO).</span><span class="sxs-lookup"><span data-stu-id="85713-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="85713-196">b.</span><span class="sxs-lookup"><span data-stu-id="85713-196">b.</span></span> <span data-ttu-id="85713-197">**Service Provider saml** (Provider del servizio SAML): incollare il valore ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span><span class="sxs-lookup"><span data-stu-id="85713-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="85713-198">c.</span><span class="sxs-lookup"><span data-stu-id="85713-198">c.</span></span> <span data-ttu-id="85713-199">**Name of Identity Provider email field in ACS response** (Nome del campo e-mail del provider d'identità nella risposta ACS): incollare il valore `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="85713-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="85713-200">d.</span><span class="sxs-lookup"><span data-stu-id="85713-200">d.</span></span> <span data-ttu-id="85713-201">**Identity Provider EntityDescriptor Entity ID** (ID entità EntityDescriptor del provider d'identità): incollare il valore **ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="85713-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="85713-202">e.</span><span class="sxs-lookup"><span data-stu-id="85713-202">e.</span></span> <span data-ttu-id="85713-203">**Identity Provider SingleSignOnService URL** (URL servizio Single Sign-On del provider d'identità): incollare l'**URL servizio Single Sign-On SAML** dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="85713-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="85713-204">f.</span><span class="sxs-lookup"><span data-stu-id="85713-204">f.</span></span> <span data-ttu-id="85713-205">**Identity Provider public X509 certificate** (Certificato X509 pubblico provider d'identità): aprire il certificato X509 scaricato da Azure nel blocco note e incollare i contenuti in questa casella.</span><span class="sxs-lookup"><span data-stu-id="85713-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="85713-206">Verificare che non vi siano interruzioni di riga nella parte centrale dei contenuti del certificato.</span><span class="sxs-lookup"><span data-stu-id="85713-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="85713-207">g.</span><span class="sxs-lookup"><span data-stu-id="85713-207">g.</span></span> <span data-ttu-id="85713-208">Selezionare le caselle di controllo seguenti: **Enabled, Encrypt NameID e Sign AuthnRequests** (Abilitato, Esegui crittografia dell'ID nome e Firma richieste di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="85713-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="85713-209">h.</span><span class="sxs-lookup"><span data-stu-id="85713-209">h.</span></span> <span data-ttu-id="85713-210">Fare clic su **Update SSO Settings** (Aggiorna impostazioni SSO) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="85713-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="85713-211">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="85713-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="85713-212">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="85713-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="85713-213">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85713-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85713-214">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85713-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="85713-215">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="85713-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="85713-217">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="85713-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="85713-218">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="85713-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85713-220">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="85713-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85713-222">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="85713-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85713-224">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="85713-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85713-226">a.</span><span class="sxs-lookup"><span data-stu-id="85713-226">a.</span></span> <span data-ttu-id="85713-227">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85713-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85713-228">b.</span><span class="sxs-lookup"><span data-stu-id="85713-228">b.</span></span> <span data-ttu-id="85713-229">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="85713-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85713-230">c.</span><span class="sxs-lookup"><span data-stu-id="85713-230">c.</span></span> <span data-ttu-id="85713-231">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="85713-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="85713-232">d.</span><span class="sxs-lookup"><span data-stu-id="85713-232">d.</span></span> <span data-ttu-id="85713-233">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="85713-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="85713-234">Creazione di un utente test ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="85713-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="85713-235">Per consentire agli utenti di Azure AD di accedere a ScaleX Enterprise, è necessario eseguirne il provisioning in ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="85713-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="85713-236">Nel caso di ScaleX Enterprise, il provisioning è un'attività automatica e non sono necessarie procedure manuali.</span><span class="sxs-lookup"><span data-stu-id="85713-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="85713-237">Per tutti gli utenti che eseguono l'autenticazione con le credenziali SSO verrà automaticamente eseguito il provisioning sul lato ScaleX.</span><span class="sxs-lookup"><span data-stu-id="85713-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="85713-238">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="85713-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="85713-239">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="85713-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Assegna utente][200] 

<span data-ttu-id="85713-241">**Per assegnare Britta Simon a ScaleX Enterprise, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="85713-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="85713-242">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="85713-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="85713-244">Nell'elenco delle applicazioni selezionare **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="85713-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="85713-246">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="85713-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="85713-248">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="85713-248">Click **Add** button.</span></span> <span data-ttu-id="85713-249">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="85713-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="85713-251">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="85713-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="85713-252">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="85713-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85713-253">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="85713-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="85713-254">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="85713-254">Testing single sign-on</span></span>

<span data-ttu-id="85713-255">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="85713-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="85713-256">Quando si fa clic sul riquadro ScaleX Enterprise nel pannello di accesso, si accede automaticamente all'applicazione ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="85713-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="85713-257">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="85713-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="85713-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="85713-258">Additional resources</span></span>

* [<span data-ttu-id="85713-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85713-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85713-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85713-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png


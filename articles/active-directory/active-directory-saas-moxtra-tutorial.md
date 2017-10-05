---
title: 'Esercitazione: integrazione di Azure Active Directory con Moxtra | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Moxtra.
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
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="57170-103">Esercitazione: integrazione di Azure Active Directory con Moxtra</span><span class="sxs-lookup"><span data-stu-id="57170-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="57170-104">Questa esercitazione descrive come integrare Moxtra con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57170-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57170-105">L'integrazione di Moxtra con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="57170-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57170-106">È possibile controllare in Azure AD chi può accedere a Moxtra</span><span class="sxs-lookup"><span data-stu-id="57170-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="57170-107">È possibile abilitare gli utenti per l'accesso automatico a Moxtra (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="57170-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57170-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57170-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57170-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57170-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57170-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57170-110">Prerequisites</span></span>

<span data-ttu-id="57170-111">Per configurare l'integrazione di Azure AD con Moxtra, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="57170-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="57170-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57170-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57170-113">Sottoscrizione di Moxtra abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="57170-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57170-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="57170-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57170-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="57170-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57170-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="57170-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57170-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57170-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57170-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="57170-118">Scenario description</span></span>
<span data-ttu-id="57170-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="57170-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57170-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="57170-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57170-121">Aggiunta di Moxtra dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="57170-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="57170-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57170-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="57170-123">Aggiunta di Moxtra dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="57170-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="57170-124">Per configurare l'integrazione di Moxtra in Azure AD, è necessario aggiungere Moxtra dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="57170-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57170-125">**Per aggiungere Moxtra dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="57170-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57170-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="57170-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57170-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="57170-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57170-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="57170-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="57170-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="57170-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="57170-133">Nella casella di ricerca, digitare **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="57170-133">In the search box, type **Moxtra**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="57170-135">Nel pannello dei risultati selezionare **Moxtra** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57170-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57170-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57170-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57170-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Moxtra usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="57170-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57170-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Moxtra corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57170-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="57170-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Moxtra.</span><span class="sxs-lookup"><span data-stu-id="57170-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="57170-141">Per stabilire la relazione di collegamento, in Moxtra assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="57170-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="57170-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Moxtra, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="57170-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57170-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="57170-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57170-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57170-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57170-145">**[Creazione di un utente di test di Moxtra](#creating-a-moxtra-test-user)**: per avere una controparte di Britta Simon in Moxtra collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57170-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57170-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57170-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57170-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="57170-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57170-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57170-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57170-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Moxtra.</span><span class="sxs-lookup"><span data-stu-id="57170-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="57170-150">**Per configurare l'accesso Single Sign-On di Azure AD con Moxtra, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="57170-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="57170-151">Nella pagina di integrazione dell'applicazione **Moxtra** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="57170-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="57170-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="57170-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="57170-155">Nella sezione **URL e dominio Moxtra** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="57170-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="57170-157">Nella casella di testo **URL di accesso** digitare l'URL come: `https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="57170-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="57170-158">L'applicazione Moxtra prevede che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="57170-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="57170-159">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="57170-159">Configure the following claims for this application.</span></span> <span data-ttu-id="57170-160">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57170-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="57170-161">Lo screenshot seguente illustra un esempio di questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="57170-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="57170-163">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come illustrato nell'immagine e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="57170-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="57170-164">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="57170-164">Attribute Name</span></span> | <span data-ttu-id="57170-165">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="57170-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="57170-166">firstname</span><span class="sxs-lookup"><span data-stu-id="57170-166">firstname</span></span> | <span data-ttu-id="57170-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="57170-167">user.givenname</span></span> |
    | <span data-ttu-id="57170-168">lastname</span><span class="sxs-lookup"><span data-stu-id="57170-168">lastname</span></span> | <span data-ttu-id="57170-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="57170-169">user.surname</span></span> |
    | <span data-ttu-id="57170-170">idpid</span><span class="sxs-lookup"><span data-stu-id="57170-170">idpid</span></span>    | <span data-ttu-id="57170-171">< ID entità SAML ></span><span class="sxs-lookup"><span data-stu-id="57170-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="57170-172">Il valore dell'attributo **idpid** non è reale.</span><span class="sxs-lookup"><span data-stu-id="57170-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="57170-173">È possibile ottenere il valore effettivo dalla **sezione di riferimento rapido** in **Configurazione di Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="57170-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="57170-174">a.</span><span class="sxs-lookup"><span data-stu-id="57170-174">a.</span></span> <span data-ttu-id="57170-175">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="57170-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="57170-177">b.</span><span class="sxs-lookup"><span data-stu-id="57170-177">b.</span></span> <span data-ttu-id="57170-178">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="57170-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="57170-180">c.</span><span class="sxs-lookup"><span data-stu-id="57170-180">c.</span></span> <span data-ttu-id="57170-181">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="57170-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="57170-182">d.</span><span class="sxs-lookup"><span data-stu-id="57170-182">d.</span></span> <span data-ttu-id="57170-183">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="57170-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="57170-184">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="57170-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="57170-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="57170-186">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="57170-188">Nella sezione **Configurazione di Moxtra** fare clic su **Configura Moxtra** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="57170-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="57170-189">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="57170-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="57170-191">In un'altra finestra del browser, accedere al sito aziendale di Moxtra come amministratore.</span><span class="sxs-lookup"><span data-stu-id="57170-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="57170-192">Nella barra degli strumenti a sinistra, fare clic su**Admin Console > SAML Single Sign-On** (Console di amministrazione > Single Sign-On SAML), quindi su **New** (Nuovo).</span><span class="sxs-lookup"><span data-stu-id="57170-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="57170-194">Nella pagina **SAML** , eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="57170-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="57170-196">a.</span><span class="sxs-lookup"><span data-stu-id="57170-196">a.</span></span> <span data-ttu-id="57170-197">Nella casella di testo **Nome** , digitare un nome per la configurazione (ad esempio *SAML*).</span><span class="sxs-lookup"><span data-stu-id="57170-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="57170-198">b.</span><span class="sxs-lookup"><span data-stu-id="57170-198">b.</span></span> <span data-ttu-id="57170-199">Nella casella di testo **IdP Entity ID** (ID entità IdP) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57170-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="57170-200">c.</span><span class="sxs-lookup"><span data-stu-id="57170-200">c.</span></span> <span data-ttu-id="57170-201">Nella casella di testo **Login URL** (URL di accesso) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57170-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="57170-202">d.</span><span class="sxs-lookup"><span data-stu-id="57170-202">d.</span></span> <span data-ttu-id="57170-203">Nella casella di testo **AuthnContextClassRef** digitare **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="57170-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="57170-204">e.</span><span class="sxs-lookup"><span data-stu-id="57170-204">e.</span></span> <span data-ttu-id="57170-205">Nella casella di testo **NameID Format** (Formato NameID) digitare **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="57170-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="57170-206">f.</span><span class="sxs-lookup"><span data-stu-id="57170-206">f.</span></span> <span data-ttu-id="57170-207">Aprire il certificato scaricato dal portale di Azure nel Blocco note, copiarne il contenuto e incollarlo nella casella di testo **Certificate** (Certificato).</span><span class="sxs-lookup"><span data-stu-id="57170-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="57170-208">g.</span><span class="sxs-lookup"><span data-stu-id="57170-208">g.</span></span> <span data-ttu-id="57170-209">Nella casella di testo dominio email SAML, digitare il dominio email SAML.</span><span class="sxs-lookup"><span data-stu-id="57170-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="57170-210">Per verificare il dominio, fare clic su “**i**” di seguito.</span><span class="sxs-lookup"><span data-stu-id="57170-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="57170-211">h.</span><span class="sxs-lookup"><span data-stu-id="57170-211">h.</span></span> <span data-ttu-id="57170-212">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="57170-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="57170-213">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="57170-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57170-214">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="57170-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57170-215">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57170-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57170-216">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57170-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="57170-217">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57170-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="57170-219">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="57170-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57170-220">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="57170-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57170-222">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="57170-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57170-224">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="57170-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57170-226">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="57170-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57170-228">a.</span><span class="sxs-lookup"><span data-stu-id="57170-228">a.</span></span> <span data-ttu-id="57170-229">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57170-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57170-230">b.</span><span class="sxs-lookup"><span data-stu-id="57170-230">b.</span></span> <span data-ttu-id="57170-231">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57170-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57170-232">c.</span><span class="sxs-lookup"><span data-stu-id="57170-232">c.</span></span> <span data-ttu-id="57170-233">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="57170-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57170-234">d.</span><span class="sxs-lookup"><span data-stu-id="57170-234">d.</span></span> <span data-ttu-id="57170-235">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="57170-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="57170-236">Creare un utente test Moxtra</span><span class="sxs-lookup"><span data-stu-id="57170-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="57170-237">Questa sezione descrive come creare un utente chiamato Britta Simon in Moxtra.</span><span class="sxs-lookup"><span data-stu-id="57170-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="57170-238">**Per creare un utente denominato Britta Simon in Moxtra, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="57170-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="57170-239">Accedere al sito aziendale di Moxtra come amministratore.</span><span class="sxs-lookup"><span data-stu-id="57170-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="57170-240">Nella barra degli strumenti a sinistra, fare clic su**Admin Console > Gestione utente** e quindi su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="57170-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="57170-242">Nella finestra di dialogo **Aggiungi utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="57170-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="57170-243">a.</span><span class="sxs-lookup"><span data-stu-id="57170-243">a.</span></span> <span data-ttu-id="57170-244">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="57170-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="57170-245">b.</span><span class="sxs-lookup"><span data-stu-id="57170-245">b.</span></span> <span data-ttu-id="57170-246">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="57170-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="57170-247">c.</span><span class="sxs-lookup"><span data-stu-id="57170-247">c.</span></span> <span data-ttu-id="57170-248">Nella casella di testo **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica di Britta come nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57170-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="57170-249">d.</span><span class="sxs-lookup"><span data-stu-id="57170-249">d.</span></span> <span data-ttu-id="57170-250">Nella casella di testo **Divisione**, digitare **Dev**.</span><span class="sxs-lookup"><span data-stu-id="57170-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="57170-251">e.</span><span class="sxs-lookup"><span data-stu-id="57170-251">e.</span></span> <span data-ttu-id="57170-252">Nella casella di testo **Reparto**, digitare **IT**.</span><span class="sxs-lookup"><span data-stu-id="57170-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="57170-253">f.</span><span class="sxs-lookup"><span data-stu-id="57170-253">f.</span></span> <span data-ttu-id="57170-254">Selezionare **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="57170-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="57170-255">g.</span><span class="sxs-lookup"><span data-stu-id="57170-255">g.</span></span> <span data-ttu-id="57170-256">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="57170-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57170-257">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="57170-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57170-258">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Moxtra.</span><span class="sxs-lookup"><span data-stu-id="57170-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Assegna utente][200] 

<span data-ttu-id="57170-260">**Per assegnare Britta Simon a Moxtra, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="57170-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="57170-261">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="57170-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="57170-263">Nell'elenco di applicazioni, selezionare **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="57170-263">In the applications list, select **Moxtra**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="57170-265">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="57170-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="57170-267">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="57170-267">Click **Add** button.</span></span> <span data-ttu-id="57170-268">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="57170-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="57170-270">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="57170-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57170-271">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="57170-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57170-272">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="57170-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57170-273">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="57170-273">Testing single sign-on</span></span>

<span data-ttu-id="57170-274">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="57170-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="57170-275">Quando si fa clic sul riquadro Moxtra nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Moxtra.</span><span class="sxs-lookup"><span data-stu-id="57170-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="57170-276">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57170-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57170-277">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="57170-277">Additional resources</span></span>

* [<span data-ttu-id="57170-278">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57170-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57170-279">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57170-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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


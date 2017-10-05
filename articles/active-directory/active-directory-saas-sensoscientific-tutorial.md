---
title: 'Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SensoScientific Wireless Temperature Monitoring System.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: fa6242cf7f9559ca394ffde2e5e734cb935b03dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="94c06-103">Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="94c06-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="94c06-104">Questa esercitazione descrive come integrare SensoScientific Wireless Temperature Monitoring System con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94c06-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94c06-105">L'integrazione di SensoScientific Wireless Temperature Monitoring System con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="94c06-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94c06-106">È possibile controllare in Azure AD chi può accedere a SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="94c06-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="94c06-107">È possibile abilitare gli utenti per l'accesso automatico a SensoScientific Wireless Temperature Monitoring System (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c06-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94c06-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="94c06-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="94c06-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94c06-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94c06-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94c06-110">Prerequisites</span></span>

<span data-ttu-id="94c06-111">Per configurare l'integrazione di Azure AD con SensoScientific Wireless Temperature Monitoring System, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="94c06-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span></span>

- <span data-ttu-id="94c06-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94c06-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94c06-113">Una sottoscrizione abilitata per l'accesso Single Sign-On per SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="94c06-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94c06-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94c06-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94c06-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="94c06-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94c06-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="94c06-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94c06-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94c06-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94c06-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="94c06-118">Scenario description</span></span>
<span data-ttu-id="94c06-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="94c06-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94c06-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94c06-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94c06-121">Aggiunta di SensoScientific Wireless Temperature Monitoring System dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="94c06-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
2. <span data-ttu-id="94c06-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c06-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a><span data-ttu-id="94c06-123">Aggiunta di SensoScientific Wireless Temperature Monitoring System dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="94c06-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
<span data-ttu-id="94c06-124">Per configurare l'integrazione di SensoScientific Wireless Temperature Monitoring System in Azure AD, è necessario aggiungerlo all'elenco di app SaaS gestite dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="94c06-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94c06-125">**Per aggiungere SensoScientific Wireless Temperature Monitoring System dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94c06-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94c06-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94c06-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94c06-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="94c06-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94c06-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94c06-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="94c06-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="94c06-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="94c06-133">Nella casella di ricerca digitare **SensoScientific Wireless Temperature Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="94c06-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="94c06-135">Nel riquadro dei risultati selezionare **SensoScientific Wireless Temperature Monitoring System**, quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94c06-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94c06-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c06-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94c06-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94c06-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="94c06-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SensoScientific Wireless Temperature Monitoring System che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94c06-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span></span> <span data-ttu-id="94c06-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="94c06-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span></span>

<span data-ttu-id="94c06-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="94c06-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="94c06-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94c06-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94c06-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="94c06-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="94c06-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94c06-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94c06-145">**[Creazione di un utente test di SensoScientific Wireless Temperature Monitoring System](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**: per avere una controparte di Britta Simon in SensoScientific Wireless Temperature Monitoring System collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94c06-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="94c06-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94c06-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94c06-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="94c06-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94c06-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c06-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94c06-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="94c06-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="94c06-150">**Per configurare l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94c06-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="94c06-151">Nel portale di Azure, nella pagina di integrazione dell'applicazione **SensoScientific Wireless Temperature Monitoring System** fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="94c06-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="94c06-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94c06-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="94c06-155">Nella sezione **URL e dominio SensoScientific Wireless Temperature Monitoring System** non è necessario eseguire alcun passaggio dal momento che l'app è già preintegrata in Azure:</span><span class="sxs-lookup"><span data-stu-id="94c06-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="94c06-157">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="94c06-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="94c06-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="94c06-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94c06-161">Nella sezione **Configurazione di SensoScientific Wireless Temperature Monitoring System** fare clic su **Configura SensoScientific Wireless Temperature Monitoring System** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="94c06-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94c06-162">Copiare l'**URL di disconnessione, l'ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="94c06-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="94c06-164">Accedere all'applicazione SensoScientific Wireless Temperature Monitoring System come amministratore.</span><span class="sxs-lookup"><span data-stu-id="94c06-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="94c06-165">Nel menu di navigazione nella parte superiore, fare clic su **Configuration** (Configurazione) e passare a **Configure** (Configura) in **Single Sign-On** per aprire Single Sign-On Settings (Impostazioni Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="94c06-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="94c06-167">Nella pagina **Single Sign-On Settings** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94c06-167">In **Single Sign On Settings** form perform the following steps:</span></span>
 
    <span data-ttu-id="94c06-168">a.</span><span class="sxs-lookup"><span data-stu-id="94c06-168">a.</span></span> <span data-ttu-id="94c06-169">Selezionare il **Nome autorità emittente** come Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94c06-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="94c06-170">b.</span><span class="sxs-lookup"><span data-stu-id="94c06-170">b.</span></span> <span data-ttu-id="94c06-171">Incollare l'**ID entità SAML** copiato dal portale di Azure nella casella di testo URL dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="94c06-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="94c06-172">c.</span><span class="sxs-lookup"><span data-stu-id="94c06-172">c.</span></span> <span data-ttu-id="94c06-173">Incollare l'**URL servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo URL servizio Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94c06-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="94c06-174">d.</span><span class="sxs-lookup"><span data-stu-id="94c06-174">d.</span></span> <span data-ttu-id="94c06-175">Incollare l'**URL di disconnessione** copiato dal portale di Azure nella casella di testo URL servizio Single Sign-Out.</span><span class="sxs-lookup"><span data-stu-id="94c06-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="94c06-176">e.</span><span class="sxs-lookup"><span data-stu-id="94c06-176">e.</span></span> <span data-ttu-id="94c06-177">Cercare il certificato scaricato dal portale di Azure e caricarlo qui.</span><span class="sxs-lookup"><span data-stu-id="94c06-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="94c06-178">f.</span><span class="sxs-lookup"><span data-stu-id="94c06-178">f.</span></span> <span data-ttu-id="94c06-179">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="94c06-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="94c06-180">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="94c06-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94c06-181">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="94c06-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94c06-182">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94c06-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94c06-183">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c06-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="94c06-184">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94c06-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="94c06-186">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="94c06-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94c06-187">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94c06-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94c06-189">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="94c06-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94c06-191">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="94c06-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94c06-193">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94c06-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94c06-195">a.</span><span class="sxs-lookup"><span data-stu-id="94c06-195">a.</span></span> <span data-ttu-id="94c06-196">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94c06-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94c06-197">b.</span><span class="sxs-lookup"><span data-stu-id="94c06-197">b.</span></span> <span data-ttu-id="94c06-198">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94c06-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94c06-199">c.</span><span class="sxs-lookup"><span data-stu-id="94c06-199">c.</span></span> <span data-ttu-id="94c06-200">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="94c06-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="94c06-201">d.</span><span class="sxs-lookup"><span data-stu-id="94c06-201">d.</span></span> <span data-ttu-id="94c06-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="94c06-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="94c06-203">Creazione di un utente test di SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="94c06-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="94c06-204">Per consentire agli utenti di Azure AD di accedere a SensoScientific Wireless Temperature Monitoring System, è necessario eseguirne il provisioning in SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="94c06-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="94c06-205">Collaborare con il [team di supporto di SensoScientific Wireless Temperature Monitoring System](https://www.sensoscientific.com/contact-us/) per aggiungere gli utenti alla piattaforma di SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="94c06-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="94c06-206">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94c06-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="94c06-207">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c06-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="94c06-208">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="94c06-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span></span>

![Assegna utente][200] 

<span data-ttu-id="94c06-210">**Per assegnare Britta Simon a SensoScientific Wireless Temperature Monitoring System, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94c06-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="94c06-211">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94c06-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="94c06-213">Nell'elenco delle applicazioni selezionare **SensoScientific Wireless Temperature Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="94c06-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="94c06-215">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="94c06-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="94c06-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="94c06-217">Click **Add** button.</span></span> <span data-ttu-id="94c06-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94c06-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="94c06-220">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="94c06-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="94c06-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="94c06-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94c06-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94c06-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94c06-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="94c06-223">Testing single sign-on</span></span>

<span data-ttu-id="94c06-224">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="94c06-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="94c06-225">Fare clic sul riquadro SensoScientific Wireless Temperature Monitoring System nel pannello di accesso; si accederà automaticamente all'applicazione SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="94c06-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="94c06-226">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="94c06-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94c06-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="94c06-227">Additional resources</span></span>

* [<span data-ttu-id="94c06-228">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94c06-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94c06-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94c06-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png


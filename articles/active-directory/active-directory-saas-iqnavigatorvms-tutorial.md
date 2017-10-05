---
title: 'Esercitazione: Integrazione di Azure Active Directory con IQNavigator VMS | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e IQNavigator VMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 1164723a171843541098f6adbda0e65f7e82a0cb
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="b1e5d-103">Esercitazione: Integrazione di Azure Active Directory con IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="b1e5d-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="b1e5d-104">Questa esercitazione descrive come integrare IQNavigator VMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-104">In this tutorial, you learn how to integrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1e5d-105">L'integrazione di IQNavigator VMS con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-105">Integrating IQNavigator VMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b1e5d-106">È possibile controllare in Azure AD chi può accedere a IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="b1e5d-106">You can control in Azure AD who has access to IQNavigator VMS</span></span>
- <span data-ttu-id="b1e5d-107">È possibile abilitare gli utenti per l'accesso automatico a IQNavigator VMS (Single Sign-On) con gli account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e5d-107">You can enable your users to automatically get signed-on to IQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1e5d-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b1e5d-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1e5d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b1e5d-110">Prerequisites</span></span>

<span data-ttu-id="b1e5d-111">Per configurare l'integrazione di Azure AD con IQNavigator VMS sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-111">To configure Azure AD integration with IQNavigator VMS, you need the following items:</span></span>

- <span data-ttu-id="b1e5d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1e5d-113">Sottoscrizione di IQNavigator VMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b1e5d-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1e5d-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1e5d-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1e5d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1e5d-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1e5d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b1e5d-118">Scenario description</span></span>
<span data-ttu-id="b1e5d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1e5d-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1e5d-121">Aggiunta di IQNavigator VMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b1e5d-121">Adding IQNavigator VMS from the gallery</span></span>
2. <span data-ttu-id="b1e5d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e5d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-the-gallery"></a><span data-ttu-id="b1e5d-123">Aggiunta di IQNavigator VMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b1e5d-123">Adding IQNavigator VMS from the gallery</span></span>
<span data-ttu-id="b1e5d-124">Per configurare l'integrazione di IQNavigator VMS in Azure AD, è necessario aggiungere IQNavigator VMS dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-124">To configure the integration of IQNavigator VMS into Azure AD, you need to add IQNavigator VMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b1e5d-125">**Per aggiungere IQNavigator VMS dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b1e5d-125">**To add IQNavigator VMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b1e5d-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1e5d-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b1e5d-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b1e5d-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b1e5d-133">Nella casella di ricerca digitare **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-133">In the search box, type **IQNavigator VMS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="b1e5d-135">Nel pannello dei risultati selezionare **IQNavigator VMS** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-135">In the results panel, select **IQNavigator VMS**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1e5d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e5d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1e5d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con IQNavigator VMS con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b1e5d-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1e5d-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di IQNavigator VMS corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IQNavigator VMS is to a user in Azure AD.</span></span> <span data-ttu-id="b1e5d-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-140">In other words, a link relationship between an Azure AD user and the related user in IQNavigator VMS needs to be established.</span></span>

<span data-ttu-id="b1e5d-141">Per stabilire la relazione di collegamento, in IQNavigator VMS assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-141">In IQNavigator VMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b1e5d-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con IQNavigator VMS, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-142">To configure and test Azure AD single sign-on with IQNavigator VMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b1e5d-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b1e5d-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1e5d-145">**[Creazione di un utente test di IQNavigator VMS](#creating-a-iqnavigator-vms-test-user)**: per avere una controparte di Britta Simon in IQNavigator VMS collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - to have a counterpart of Britta Simon in IQNavigator VMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1e5d-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1e5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1e5d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e5d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1e5d-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="b1e5d-150">**Per configurare l'accesso Single Sign-On di Azure AD con IQNavigator VMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b1e5d-150">**To configure Azure AD single sign-on with IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="b1e5d-151">Nella pagina di integrazione dell'applicazione **IQNavigator VMS** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-151">In the Azure portal, on the **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b1e5d-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="b1e5d-155">Nella sezione **URL e dominio IQNavigator VMS** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-155">On the **IQNavigator VMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="b1e5d-157">a.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-157">a.</span></span> <span data-ttu-id="b1e5d-158">Nella casella di testo **Identificatore** digitare l'URL: `iqn.com`</span><span class="sxs-lookup"><span data-stu-id="b1e5d-158">In the **Identifier** textbox, type the URL:`iqn.com`</span></span>

    <span data-ttu-id="b1e5d-159">b.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-159">b.</span></span> <span data-ttu-id="b1e5d-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="b1e5d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="b1e5d-161">Selezionare **Mostra URL impostazioni avanzate** ed eseguire l'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-161">Check **Show advanced URL settings**, perform the following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="b1e5d-163">Nella casella di testo **Stato dell'inoltro** digitare un URL usando il modello seguente: `https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="b1e5d-163">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1e5d-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b1e5d-164">These values are not real.</span></span> <span data-ttu-id="b1e5d-165">è necessario aggiornarli con l'URL di risposta e lo stato dell'inoltro effettivi.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-165">Update these values with the actual Reply URL and Relay state.</span></span> <span data-ttu-id="b1e5d-166">Per ottenere questi valori, contattare il [team di supporto clienti di IQNavigator VMS](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) to get these values.</span></span> 

5. <span data-ttu-id="b1e5d-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b1e5d-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1e5d-169">Per generare l'URL dei **metadati**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-169">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="b1e5d-170">a.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-170">a.</span></span> <span data-ttu-id="b1e5d-171">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-171">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="b1e5d-173">b.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-173">b.</span></span> <span data-ttu-id="b1e5d-174">Fare clic su **Endpoint** per aprire la finestra di dialogo **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-174">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="b1e5d-176">c.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-176">c.</span></span> <span data-ttu-id="b1e5d-177">Fare clic sul pulsante Copia per copiare l'URL del **DOCUMENTO METADATI FEDERAZIONE** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-177">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="b1e5d-179">d.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-179">d.</span></span> <span data-ttu-id="b1e5d-180">Passare ora alla pagina delle proprietà di **IQNavigator VMS** e copiare l'**ID applicazione** usando il pulsante **Copia** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-180">Now go to the property page of **IQNavigator VMS** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="b1e5d-182">e.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-182">e.</span></span> <span data-ttu-id="b1e5d-183">Generare l'**URL dei metadati** usando il modello seguente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="b1e5d-183">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="b1e5d-184">L'applicazione IQNavigator prevede il valore di ID utente univoco nell'attestazione dell'identificatore del nome.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-184">IQNavigator application expect the unique user identifier value in the Name Identifier claim.</span></span> <span data-ttu-id="b1e5d-185">Il cliente può eseguire il mapping del valore corretto per l'attestazione dell'identificatore del nome.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-185">Customer can map the correct value for the Name Identifier claim.</span></span> <span data-ttu-id="b1e5d-186">In questo caso è stato eseguito il mapping di user.UserPrincipalName a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-186">In this case we have mapped the user.UserPrincipalName for the demo purpose.</span></span> <span data-ttu-id="b1e5d-187">Tuttavia, in base alle impostazioni dell'organizzazione è necessario eseguire il mapping del valore corretto.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-187">But according to your organization settings you should map the correct value for it.</span></span>   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="b1e5d-189">Nella sezione **Configurazione di IQNavigator VMS** fare clic su **Configura IQNavigator VMS** per visualizzare la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-189">On the **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b1e5d-190">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b1e5d-190">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="b1e5d-192">Per configurare l'accesso Single Sign-On sul lato **IQNavigator VMS**, è necessario inviare l'**URL dei metadati**, l'**URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di IQNavigator VMS](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-192">To configure single sign-on on **IQNavigator VMS** side, you need to send the **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="b1e5d-193">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b1e5d-194">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b1e5d-195">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b1e5d-196">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1e5d-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e5d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1e5d-198">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b1e5d-200">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b1e5d-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b1e5d-201">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1e5d-203">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1e5d-205">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1e5d-207">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b1e5d-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1e5d-209">a.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-209">a.</span></span> <span data-ttu-id="b1e5d-210">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1e5d-211">b.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-211">b.</span></span> <span data-ttu-id="b1e5d-212">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1e5d-213">c.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-213">c.</span></span> <span data-ttu-id="b1e5d-214">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b1e5d-215">d.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-215">d.</span></span> <span data-ttu-id="b1e5d-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="b1e5d-217">Creazione di un utente test di IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="b1e5d-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="b1e5d-218">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-218">The objective of this section is to create a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="b1e5d-219">Collaborare con il [team di supporto di IQNavigator VMS](https://www.beeline.com/iqn-product-support/) per aggiungere gli utenti nell'account IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) to add the users in the IQNavigator VMS account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b1e5d-220">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1e5d-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b1e5d-221">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IQNavigator VMS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b1e5d-223">**Per assegnare Britta Simon a IQNavigator VMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b1e5d-223">**To assign Britta Simon to IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="b1e5d-224">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b1e5d-226">Nell'elenco di applicazioni selezionare **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-226">In the applications list, select **IQNavigator VMS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="b1e5d-228">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b1e5d-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-230">Click **Add** button.</span></span> <span data-ttu-id="b1e5d-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b1e5d-233">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b1e5d-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1e5d-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1e5d-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b1e5d-236">Testing single sign-on</span></span>

<span data-ttu-id="b1e5d-237">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b1e5d-238">Quando si fa clic sul riquadro IQNavigator VMS nel pannello di accesso, si accederà automaticamente all'applicazione IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="b1e5d-238">When you click the IQNavigator VMS tile in the Access Panel, you should get automatically signed-on to your IQNavigator VMS application.</span></span>
<span data-ttu-id="b1e5d-239">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1e5d-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1e5d-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b1e5d-240">Additional resources</span></span>

* [<span data-ttu-id="b1e5d-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1e5d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1e5d-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1e5d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png


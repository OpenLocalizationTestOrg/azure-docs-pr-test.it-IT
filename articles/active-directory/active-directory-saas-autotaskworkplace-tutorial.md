---
title: 'Esercitazione: Integrazione di Azure Active Directory con Autotask Workplace | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Autotask Workplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 45130162271b20860607497ff93c6a668c415233
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="89e7e-103">Esercitazione: Integrazione di Azure Active Directory con Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="89e7e-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="89e7e-104">Questa esercitazione descrive come integrare Autotask Workplace con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89e7e-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89e7e-105">L'integrazione di Autotask Workplace con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="89e7e-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="89e7e-106">È possibile controllare in Azure AD chi può accedere ad Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="89e7e-106">You can control in Azure AD who has access to Autotask Workplace</span></span>
- <span data-ttu-id="89e7e-107">È possibile abilitare gli utenti per l'accesso automatico ad Autotask Workplace (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="89e7e-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89e7e-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="89e7e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="89e7e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89e7e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89e7e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="89e7e-110">Prerequisites</span></span>

<span data-ttu-id="89e7e-111">Per configurare l'integrazione di Azure AD con Autotask Workplace, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="89e7e-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span></span>

- <span data-ttu-id="89e7e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e7e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89e7e-113">Sottoscrizione di Autotask Workplace abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="89e7e-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="89e7e-114">È necessario essere un amministratore o un amministratore con privilegi avanzati in Workplace.</span><span class="sxs-lookup"><span data-stu-id="89e7e-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="89e7e-115">È necessario avere un account Administrator in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e7e-115">You must have an administrator account in the Azure AD.</span></span>
- <span data-ttu-id="89e7e-116">Gli utenti che utilizzeranno questa funzionalità devono avere account in Workplace e Azure AD, con indirizzi e-mail corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="89e7e-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="89e7e-117">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="89e7e-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89e7e-118">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="89e7e-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89e7e-119">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="89e7e-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89e7e-120">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89e7e-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89e7e-121">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="89e7e-121">Scenario description</span></span>
<span data-ttu-id="89e7e-122">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="89e7e-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89e7e-123">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="89e7e-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89e7e-124">Aggiunta di Autotask Workplace dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="89e7e-124">Adding Autotask Workplace from the gallery</span></span>
2. <span data-ttu-id="89e7e-125">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e7e-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-the-gallery"></a><span data-ttu-id="89e7e-126">Aggiunta di Autotask Workplace dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="89e7e-126">Adding Autotask Workplace from the gallery</span></span>
<span data-ttu-id="89e7e-127">Per configurare l'integrazione di Autotask Workplace in Azure AD, è necessario aggiungere Autotask Workplace dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="89e7e-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="89e7e-128">**Per aggiungere Autotask Workplace dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="89e7e-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="89e7e-129">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="89e7e-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="89e7e-131">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="89e7e-132">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-132">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="89e7e-134">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="89e7e-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="89e7e-136">Nella casella di ricerca digitare **Autotask Workplace**, selezionare **Autotask Workplace** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="89e7e-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span></span>

    ![Autotask Workplace nell'elenco risultati](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89e7e-138">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e7e-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="89e7e-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Autotask Workplace usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="89e7e-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="89e7e-140">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Autotask Workplace corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e7e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span></span> <span data-ttu-id="89e7e-141">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="89e7e-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span></span>

<span data-ttu-id="89e7e-142">Per stabilire la relazione di collegamento, in Autotask Workplace assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="89e7e-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="89e7e-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con Autotask Workplace, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="89e7e-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="89e7e-144">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="89e7e-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="89e7e-145">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89e7e-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89e7e-146">**[Creare un utente di test di Autotask Workplace](#create-an-autotask-workplace-test-user)**: per avere una controparte di Britta Simon in Autotask Workplace collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e7e-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="89e7e-147">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e7e-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89e7e-148">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="89e7e-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89e7e-149">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e7e-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="89e7e-150">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="89e7e-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="89e7e-151">**Per configurare l'accesso Single Sign-On di Azure AD con Autotask Workplace, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="89e7e-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="89e7e-152">Nella pagina di integrazione dell'applicazione **Autotask Workplace** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="89e7e-154">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="89e7e-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="89e7e-156">Se si vuole configurare l'applicazione in modalità avviata da **IDP**, nella sezione **URL e dominio Autotask Workplace** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="89e7e-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Autotask Workplace per IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="89e7e-158">a.</span><span class="sxs-lookup"><span data-stu-id="89e7e-158">a.</span></span> <span data-ttu-id="89e7e-159">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="89e7e-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="89e7e-160">b.</span><span class="sxs-lookup"><span data-stu-id="89e7e-160">b.</span></span> <span data-ttu-id="89e7e-161">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="89e7e-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="89e7e-162">Se si desidera configurare l'applicazione in modalità avviata da **SP**, selezionare **Mostra impostazioni URL avanzate** e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="89e7e-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Autotask Workplace per SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="89e7e-164">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.awp.autotask.net/loginsso`.</span><span class="sxs-lookup"><span data-stu-id="89e7e-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="89e7e-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="89e7e-165">These values are not real.</span></span> <span data-ttu-id="89e7e-166">è necessario aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="89e7e-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="89e7e-167">Per ottenere questi valori, contattare il [team di supporto clienti di Autotask Workplace](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm).</span><span class="sxs-lookup"><span data-stu-id="89e7e-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span></span> 

5. <span data-ttu-id="89e7e-168">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="89e7e-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="89e7e-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="89e7e-170">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="89e7e-172">In un'altra finestra del Web browser accedere a Workplace Online usando le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="89e7e-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="89e7e-173">Quando si configura l'IdP, è necessario specificare un sottodominio.</span><span class="sxs-lookup"><span data-stu-id="89e7e-173">When configuring the IdP, a subdomain will need to be specified.</span></span> <span data-ttu-id="89e7e-174">Per verificare che il sottodominio sia corretto, accedere a Workplace Online.</span><span class="sxs-lookup"><span data-stu-id="89e7e-174">To confirm the correct subdomain, login to Workplace Online.</span></span> <span data-ttu-id="89e7e-175">Una volta effettuato l'accesso, prendere nota del sottodominio nell'URL.</span><span class="sxs-lookup"><span data-stu-id="89e7e-175">Once logged in, make note to the subdomain in the URL.</span></span>
    ><span data-ttu-id="89e7e-176">Il sottodominio è la parte tra "https://" e ".awp.autotask.net/" e deve essere us, eu, ca o au.</span><span class="sxs-lookup"><span data-stu-id="89e7e-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="89e7e-177">Passare a **Configuration** (Configurazione)  > **Single Sign-On** e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="89e7e-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span></span>

    ![Configurazione Single Sign-On per Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="89e7e-179">a.</span><span class="sxs-lookup"><span data-stu-id="89e7e-179">a.</span></span> <span data-ttu-id="89e7e-180">Selezionare l'opzione **XML Metadata File** (File di metadati XML) e quindi caricare il file **XML metadati** scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="89e7e-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="89e7e-181">b.</span><span class="sxs-lookup"><span data-stu-id="89e7e-181">b.</span></span> <span data-ttu-id="89e7e-182">Fare clic su **Enable SSO** (Abilita SSO).</span><span class="sxs-lookup"><span data-stu-id="89e7e-182">Click **Enable SSO**.</span></span>
    
    ![Approvazione della configurazione Single Sign-On per Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="89e7e-184">c.</span><span class="sxs-lookup"><span data-stu-id="89e7e-184">c.</span></span> <span data-ttu-id="89e7e-185">Selezionare la casella di controllo **I confirm this information is correct and I trust this IdP** (Confermo che le informazioni sono corrette e che l'IdP è attendibile).</span><span class="sxs-lookup"><span data-stu-id="89e7e-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="89e7e-186">d.</span><span class="sxs-lookup"><span data-stu-id="89e7e-186">d.</span></span> <span data-ttu-id="89e7e-187">Fare clic su **Approve** (Approva).</span><span class="sxs-lookup"><span data-stu-id="89e7e-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="89e7e-188">Se è necessario supporto per la configurazione di Autotask Workplace, vedere [questa pagina](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) per ottenere assistenza per l'account Workplace.</span><span class="sxs-lookup"><span data-stu-id="89e7e-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="89e7e-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="89e7e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="89e7e-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="89e7e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="89e7e-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89e7e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89e7e-192">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e7e-192">Create an Azure AD test user</span></span>

<span data-ttu-id="89e7e-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="89e7e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="89e7e-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="89e7e-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="89e7e-196">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="89e7e-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="89e7e-198">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="89e7e-200">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="89e7e-202">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="89e7e-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="89e7e-204">a.</span><span class="sxs-lookup"><span data-stu-id="89e7e-204">a.</span></span> <span data-ttu-id="89e7e-205">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89e7e-206">b.</span><span class="sxs-lookup"><span data-stu-id="89e7e-206">b.</span></span> <span data-ttu-id="89e7e-207">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89e7e-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="89e7e-208">c.</span><span class="sxs-lookup"><span data-stu-id="89e7e-208">c.</span></span> <span data-ttu-id="89e7e-209">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="89e7e-210">d.</span><span class="sxs-lookup"><span data-stu-id="89e7e-210">d.</span></span> <span data-ttu-id="89e7e-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="89e7e-212">Creare un utente di test di Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="89e7e-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="89e7e-213">In questa sezione viene creato un utente di nome Britta Simon in Autotask.</span><span class="sxs-lookup"><span data-stu-id="89e7e-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="89e7e-214">Collaborare con il [team di supporto di Autotask Workplace](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) per aggiungere gli utenti alla piattaforma Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="89e7e-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="89e7e-215">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e7e-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="89e7e-216">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="89e7e-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="89e7e-218">**Per assegnare Britta Simon a Autotask Workplace, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="89e7e-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="89e7e-219">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="89e7e-221">Nell'elenco di applicazioni selezionare **Autotask Workplace**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-221">In the applications list, select **Autotask Workplace**.</span></span>

    ![Collegamento di Autotask Workplace nell'elenco delle applicazioni](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="89e7e-223">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="89e7e-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="89e7e-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-225">Click **Add** button.</span></span> <span data-ttu-id="89e7e-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="89e7e-228">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="89e7e-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="89e7e-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89e7e-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="89e7e-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="89e7e-231">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="89e7e-231">Test single sign-on</span></span>

<span data-ttu-id="89e7e-232">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="89e7e-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="89e7e-233">Quando si fa clic sul riquadro Autotask Workplace nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="89e7e-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span></span>
<span data-ttu-id="89e7e-234">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89e7e-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89e7e-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="89e7e-235">Additional resources</span></span>

* [<span data-ttu-id="89e7e-236">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89e7e-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89e7e-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89e7e-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png


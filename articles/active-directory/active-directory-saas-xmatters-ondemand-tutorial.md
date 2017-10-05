---
title: 'Esercitazione: Integrazione di Azure Active Directory con xMatters OnDemand | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="96d21-103">Esercitazione: Integrazione di Azure Active Directory con xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="96d21-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="96d21-104">Questa esercitazione descrive come integrare xMatters OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96d21-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96d21-105">L'integrazione di xMatters OnDemand con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="96d21-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="96d21-106">È possibile controllare in Azure AD chi può accedere a xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="96d21-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="96d21-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a xMatters OnDemand con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="96d21-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96d21-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="96d21-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="96d21-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96d21-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96d21-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="96d21-110">Prerequisites</span></span>

<span data-ttu-id="96d21-111">Per configurare l'integrazione di Azure AD con xMatters OnDemand sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="96d21-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="96d21-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96d21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96d21-113">Sottoscrizione di xMatters OnDemand abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="96d21-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96d21-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96d21-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96d21-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="96d21-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96d21-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="96d21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96d21-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96d21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96d21-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="96d21-118">Scenario description</span></span>
<span data-ttu-id="96d21-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="96d21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96d21-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="96d21-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96d21-121">Aggiunta di xMatters OnDemand dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="96d21-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="96d21-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="96d21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="96d21-123">Aggiunta di xMatters OnDemand dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="96d21-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="96d21-124">Per configurare l'integrazione di xMatters OnDemand in Azure AD è necessario aggiungere xMatters OnDemand dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="96d21-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="96d21-125">**Per aggiungere xMatters OnDemand dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="96d21-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="96d21-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="96d21-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96d21-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="96d21-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="96d21-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="96d21-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="96d21-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="96d21-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="96d21-133">Nella casella di ricerca digitare **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="96d21-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="96d21-135">Nel pannello dei risultati selezionare **xMatters OnDemand** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="96d21-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96d21-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="96d21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96d21-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con xMatters OnDemand usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="96d21-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96d21-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di xMatters OnDemand corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96d21-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="96d21-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="96d21-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="96d21-141">Per stabilire la relazione di collegamento, in xMatters OnDemand assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="96d21-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="96d21-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con xMatters OnDemand è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="96d21-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="96d21-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="96d21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="96d21-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96d21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96d21-145">**[Creazione di un utente test di xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**: per avere una controparte di Britta Simon in xMatters OnDemand collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96d21-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="96d21-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96d21-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96d21-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="96d21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96d21-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="96d21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96d21-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="96d21-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="96d21-150">**Per configurare l'accesso Single Sign-On di Azure AD con xMatters OnDemand, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="96d21-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="96d21-151">Nella pagina di integrazione dell'applicazione **xMatters OnDemand** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="96d21-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="96d21-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="96d21-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="96d21-155">Nella sezione **URL e dominio xMatters OnDemand** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="96d21-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="96d21-157">a.</span><span class="sxs-lookup"><span data-stu-id="96d21-157">a.</span></span> <span data-ttu-id="96d21-158">Nella casella di testo **Identificatore** digitare l'URL adottando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="96d21-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="96d21-159">b.</span><span class="sxs-lookup"><span data-stu-id="96d21-159">b.</span></span> <span data-ttu-id="96d21-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="96d21-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="96d21-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="96d21-161">These values are not real.</span></span> <span data-ttu-id="96d21-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="96d21-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="96d21-163">Per ottenere questi valori, contattare il [team di supporto di xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="96d21-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="96d21-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato in locale come **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="96d21-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="96d21-166">Inoltrare il certificato al [team di supporto di xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="96d21-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="96d21-167">Per poter completare la configurazione di Single Sign-On, è necessario che il certificato venga caricato dal team di supporto xMatters.</span><span class="sxs-lookup"><span data-stu-id="96d21-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="96d21-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="96d21-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96d21-170">Nella sezione **Configurazione di xMatters OnDemand** fare clic su **Configura xMatters OnDemand** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="96d21-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="96d21-171">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="96d21-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="96d21-173">In un'altra finestra del Web browser accedere al sito aziendale di XMatters OnDemand come amministratore.</span><span class="sxs-lookup"><span data-stu-id="96d21-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="96d21-174">Sulla barra degli strumenti in alto fare clic su **Admin** e quindi su **Company Details** (Dettagli società) sulla barra di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="96d21-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="96d21-175">![Amministratore](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="96d21-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="96d21-176">Nella pagina **Configurazione SAML** seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96d21-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="96d21-177">![Configurazione SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="96d21-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="96d21-178">a.</span><span class="sxs-lookup"><span data-stu-id="96d21-178">a.</span></span> <span data-ttu-id="96d21-179">Selezionare **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="96d21-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="96d21-180">b.</span><span class="sxs-lookup"><span data-stu-id="96d21-180">b.</span></span> <span data-ttu-id="96d21-181">Incollare il valore **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure nella casella di testo **Identity provider ID** (ID provider di identità).</span><span class="sxs-lookup"><span data-stu-id="96d21-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="96d21-182">c.</span><span class="sxs-lookup"><span data-stu-id="96d21-182">c.</span></span> <span data-ttu-id="96d21-183">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **Single Sign On URL** (URL accesso Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="96d21-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="96d21-184">d.</span><span class="sxs-lookup"><span data-stu-id="96d21-184">d.</span></span> <span data-ttu-id="96d21-185">Incollare l'**URL di disconnessione** copiato dal portale di Azure nella casella di testo **Single Logout URL** (URL disconnessione singola).</span><span class="sxs-lookup"><span data-stu-id="96d21-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="96d21-186">e.</span><span class="sxs-lookup"><span data-stu-id="96d21-186">e.</span></span> <span data-ttu-id="96d21-187">Nella parte superiore della pagina Informazioni sull’azienda fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="96d21-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="96d21-188">![Dettagli dell'azienda](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Dettagli dell'azienda")</span><span class="sxs-lookup"><span data-stu-id="96d21-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="96d21-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="96d21-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="96d21-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="96d21-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="96d21-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96d21-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96d21-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="96d21-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="96d21-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="96d21-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="96d21-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="96d21-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="96d21-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="96d21-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96d21-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="96d21-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96d21-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="96d21-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96d21-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="96d21-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96d21-204">a.</span><span class="sxs-lookup"><span data-stu-id="96d21-204">a.</span></span> <span data-ttu-id="96d21-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96d21-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96d21-206">b.</span><span class="sxs-lookup"><span data-stu-id="96d21-206">b.</span></span> <span data-ttu-id="96d21-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96d21-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96d21-208">c.</span><span class="sxs-lookup"><span data-stu-id="96d21-208">c.</span></span> <span data-ttu-id="96d21-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="96d21-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="96d21-210">d.</span><span class="sxs-lookup"><span data-stu-id="96d21-210">d.</span></span> <span data-ttu-id="96d21-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="96d21-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="96d21-212">Creazione di un utente test di xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="96d21-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="96d21-213">Per consentire agli utenti di Azure AD di accedere a XMatters OnDemand, è necessario eseguirne il provisioning in XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="96d21-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="96d21-214">Nel caso di XMatters OnDemand, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="96d21-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="96d21-215">Per eseguire il provisioning di un account utente, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96d21-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="96d21-216">Accedere al tenant di **XMatters OnDemand** .</span><span class="sxs-lookup"><span data-stu-id="96d21-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="96d21-217">Fare clic sulla scheda **Utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="96d21-217">Click **Users** tab.</span></span> <span data-ttu-id="96d21-218">Fare clic su **Add User** (Aggiungi utente).</span><span class="sxs-lookup"><span data-stu-id="96d21-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="96d21-219">![Utenti](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="96d21-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="96d21-220">Nella sezione **Aggiungi un utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="96d21-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="96d21-221">![Aggiungere un utente](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="96d21-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="96d21-222">a.</span><span class="sxs-lookup"><span data-stu-id="96d21-222">a.</span></span> <span data-ttu-id="96d21-223">Selezionare **Active**.</span><span class="sxs-lookup"><span data-stu-id="96d21-223">Select **Active**.</span></span>

    <span data-ttu-id="96d21-224">b.</span><span class="sxs-lookup"><span data-stu-id="96d21-224">b.</span></span> <span data-ttu-id="96d21-225">Nella casella di testo **User ID** (ID utente) digitare l'ID dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="96d21-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="96d21-226">c.</span><span class="sxs-lookup"><span data-stu-id="96d21-226">c.</span></span> <span data-ttu-id="96d21-227">Digitare il nome dell'utente, ad esempio Britta, nella casella di testo **First Name** (Nome).</span><span class="sxs-lookup"><span data-stu-id="96d21-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="96d21-228">d.</span><span class="sxs-lookup"><span data-stu-id="96d21-228">d.</span></span> <span data-ttu-id="96d21-229">Digitare il cognome dell'utente, ad esempio Simon, nella casella di testo **Last Name** (Cognome).</span><span class="sxs-lookup"><span data-stu-id="96d21-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="96d21-230">e.</span><span class="sxs-lookup"><span data-stu-id="96d21-230">e.</span></span> <span data-ttu-id="96d21-231">Nella casella di testo **Site** (Sito) immettere il sito valido di un account di Azure AD valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="96d21-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="96d21-232">f.</span><span class="sxs-lookup"><span data-stu-id="96d21-232">f.</span></span> <span data-ttu-id="96d21-233">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="96d21-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="96d21-234">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="96d21-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="96d21-235">In questa sezione si abilita Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="96d21-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![Assegna utente][200] 

<span data-ttu-id="96d21-237">**Per assegnare Britta Simon a xMatters OnDemand, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="96d21-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="96d21-238">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="96d21-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="96d21-240">Nell'elenco delle applicazioni selezionare **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="96d21-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="96d21-242">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="96d21-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="96d21-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="96d21-244">Click **Add** button.</span></span> <span data-ttu-id="96d21-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="96d21-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="96d21-247">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="96d21-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="96d21-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="96d21-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96d21-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="96d21-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96d21-250">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="96d21-250">Testing single sign-on</span></span>

<span data-ttu-id="96d21-251">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="96d21-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="96d21-252">Quando si fa clic sul riquadro xMatters OnDemand nel pannello di accesso si accede automaticamente all'applicazione xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="96d21-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="96d21-253">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="96d21-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96d21-254">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="96d21-254">Additional resources</span></span>

* [<span data-ttu-id="96d21-255">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96d21-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96d21-256">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96d21-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png


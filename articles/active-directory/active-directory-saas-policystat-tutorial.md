---
title: 'Esercitazione: Integrazione di Azure Active Directory con PolicyStat | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e PolicyStat.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="8a9d0-103">Esercitazione: Integrazione di Azure Active Directory con PolicyStat</span><span class="sxs-lookup"><span data-stu-id="8a9d0-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="8a9d0-104">Questa esercitazione descrive come integrare PolicyStat con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a9d0-105">L'integrazione di PolicyStat con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a9d0-106">È possibile controllare in Azure AD chi può accedere a PolicyStat</span><span class="sxs-lookup"><span data-stu-id="8a9d0-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="8a9d0-107">È possibile abilitare gli utenti per l'accesso automatico a PolicyStat (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9d0-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a9d0-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a9d0-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a9d0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8a9d0-110">Prerequisites</span></span>

<span data-ttu-id="8a9d0-111">Per configurare l'integrazione di Azure AD con PolicyStat, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="8a9d0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a9d0-113">Sottoscrizione di PolicyStat abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8a9d0-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a9d0-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a9d0-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a9d0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a9d0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a9d0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8a9d0-118">Scenario description</span></span>
<span data-ttu-id="8a9d0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a9d0-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a9d0-121">Aggiunta di PolicyStat dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8a9d0-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="8a9d0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="8a9d0-123">Aggiunta di PolicyStat dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8a9d0-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="8a9d0-124">Per configurare l'integrazione di PolicyStat in Azure AD, è necessario aggiungere PolicyStat dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a9d0-125">**Per aggiungere PolicyStat dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8a9d0-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9d0-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a9d0-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a9d0-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8a9d0-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8a9d0-133">Nella casella di ricerca digitare **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-133">In the search box, type **PolicyStat**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="8a9d0-135">Nel pannello dei risultati selezionare **PolicyStat** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a9d0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a9d0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PolicyStat con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8a9d0-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a9d0-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di PolicyStat che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="8a9d0-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="8a9d0-141">Per stabilire la relazione di collegamento, in PolicyStat assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8a9d0-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con PolicyStat, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a9d0-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a9d0-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a9d0-145">**[Creazione di un utente di test di PolicyStat](#creating-a-policystat-test-user)**: per avere una controparte di Britta Simon in PolicyStat collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a9d0-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a9d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a9d0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a9d0-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel nuovo portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="8a9d0-150">**Per configurare Single Sign-On di Azure AD con PolicyStat, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8a9d0-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9d0-151">Nella pagina di integrazione dell'applicazione **PolicyStat** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8a9d0-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="8a9d0-155">Nella sezione **URL e dominio PolicyStat** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="8a9d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-157">a.</span></span> <span data-ttu-id="8a9d0-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.policystat.com`.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="8a9d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-159">b.</span></span> <span data-ttu-id="8a9d0-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="8a9d0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a9d0-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8a9d0-161">These values are not real.</span></span> <span data-ttu-id="8a9d0-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8a9d0-163">Per ottenere tali valori, contattare il [team di supporto clienti di PolicyStat](http://www.policystat.com/support/).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="8a9d0-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="8a9d0-166">In questa sezione viene descritto come consentire agli utenti di eseguire l'autenticazione a PolicyStat tramite il proprio account di Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="8a9d0-167">L'applicazione PolicyStat prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli **attributi del token SAML**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="8a9d0-168">Lo screenshot seguente ne illustra un esempio.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="8a9d0-169">![Attributi](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="8a9d0-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="8a9d0-170">Per aggiungere i mapping di attributi obbligatori, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="8a9d0-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8a9d0-171">Attribute Name</span></span>    |   <span data-ttu-id="8a9d0-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8a9d0-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="8a9d0-173">uid</span><span class="sxs-lookup"><span data-stu-id="8a9d0-173">uid</span></span> | <span data-ttu-id="8a9d0-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="8a9d0-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="8a9d0-175">a.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-175">a.</span></span> <span data-ttu-id="8a9d0-176">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="8a9d0-179">b.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-179">b.</span></span> <span data-ttu-id="8a9d0-180">Nella casella di testo **Nome attributo** digitare **uid**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="8a9d0-181">c.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-181">c.</span></span> <span data-ttu-id="8a9d0-182">Nella casella di testo **Valore attributo** selezionare **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="8a9d0-183">d.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-183">d.</span></span> <span data-ttu-id="8a9d0-184">Nell'elenco **Posta** selezionare **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="8a9d0-185">e.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-185">e.</span></span> <span data-ttu-id="8a9d0-186">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="8a9d0-186">Click **Ok**</span></span>

7. <span data-ttu-id="8a9d0-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8a9d0-187">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8a9d0-189">In un'altra finestra del Web browser accedere al sito aziendale di PolicyStat come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="8a9d0-190">Scegliere la scheda **Admin**, quindi fare clic su **Configurazione di Single Sign-On** nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="8a9d0-191">![Menu amministratore](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu amministratore")</span><span class="sxs-lookup"><span data-stu-id="8a9d0-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="8a9d0-192">Nella sezione **Configurazione** selezionare **Abilitare integrazione di Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="8a9d0-193">![Configurazione Single Sign-on](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configurazione Single Sign-on")</span><span class="sxs-lookup"><span data-stu-id="8a9d0-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="8a9d0-194">Fare clic su **Configura attributi** e nella sezione **Configura attributi** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="8a9d0-195">![Configurazione Single Sign-on](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configurazione Single Sign-on")</span><span class="sxs-lookup"><span data-stu-id="8a9d0-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="8a9d0-196">a.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-196">a.</span></span> <span data-ttu-id="8a9d0-197">Nella casella di testo **Attributo nome utente** digitare **uid**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="8a9d0-198">b.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-198">b.</span></span> <span data-ttu-id="8a9d0-199">Nella casella di testo **First Name Attribute** (Attributo nome) digitare **firstname** dell'utente **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="8a9d0-200">c.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-200">c.</span></span> <span data-ttu-id="8a9d0-201">Nella casella di testo **Last Name Attribute** (Attributo cognome) digitare **lastname** dell'utente **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="8a9d0-202">d.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-202">d.</span></span> <span data-ttu-id="8a9d0-203">Nella casella di testo **Email Attribute** (Attributo posta elettronica) digitare **emailaddress** dell'utente **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="8a9d0-204">e.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-204">e.</span></span> <span data-ttu-id="8a9d0-205">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="8a9d0-206">Fare clic su **Metadati del provider di identità** quindi, nella sezione **Metadati del provider di identità**, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="8a9d0-207">![Configurazione Single Sign-on](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configurazione Single Sign-on")</span><span class="sxs-lookup"><span data-stu-id="8a9d0-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="8a9d0-208">a.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-208">a.</span></span> <span data-ttu-id="8a9d0-209">Aprire il file di metadati scaricato, copiare il contenuto e incollarlo nella casella di testo **Your Identity Provider Metadata** (Metadati provider di identità).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="8a9d0-210">b.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-210">b.</span></span> <span data-ttu-id="8a9d0-211">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="8a9d0-212">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a9d0-213">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a9d0-214">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a9d0-215">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9d0-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a9d0-216">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8a9d0-218">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8a9d0-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9d0-219">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a9d0-221">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a9d0-223">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a9d0-225">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8a9d0-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a9d0-227">a.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-227">a.</span></span> <span data-ttu-id="8a9d0-228">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a9d0-229">b.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-229">b.</span></span> <span data-ttu-id="8a9d0-230">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a9d0-231">c.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-231">c.</span></span> <span data-ttu-id="8a9d0-232">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a9d0-233">d.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-233">d.</span></span> <span data-ttu-id="8a9d0-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="8a9d0-235">Creazione di un utente di test di PolicyStat</span><span class="sxs-lookup"><span data-stu-id="8a9d0-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="8a9d0-236">Per consentire agli utenti di Azure AD di accedere a PolicyStat, è necessario eseguirne il provisioning in PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="8a9d0-237">PolicyStat supporta solo il provisioning JIT dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="8a9d0-238">Non è pertanto è necessario aggiungere gli utenti manualmente a PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="8a9d0-239">Gli utenti verranno aggiunti automaticamente al primo accesso tramite SSO.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="8a9d0-240">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da PolicyStat per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a9d0-241">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9d0-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a9d0-242">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8a9d0-244">**Per assegnare Britta Simon a PolicyStat, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8a9d0-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9d0-245">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8a9d0-247">Nell'elenco di applicazioni selezionare **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-247">In the applications list, select **PolicyStat**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="8a9d0-249">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8a9d0-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-251">Click **Add** button.</span></span> <span data-ttu-id="8a9d0-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8a9d0-254">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8a9d0-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a9d0-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a9d0-257">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8a9d0-257">Testing single sign-on</span></span>

<span data-ttu-id="8a9d0-258">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a9d0-259">Quando si fa clic sul riquadro PolicyStat nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="8a9d0-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="8a9d0-260">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8a9d0-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a9d0-261">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8a9d0-261">Additional resources</span></span>

* [<span data-ttu-id="8a9d0-262">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a9d0-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a9d0-263">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a9d0-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con HireVue |Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e HireVue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 682d88d3010f5781948a9adde0e1351471608a5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="c0796-103">Esercitazione: Integrazione di Azure Active Directory con HireVue</span><span class="sxs-lookup"><span data-stu-id="c0796-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="c0796-104">Questa esercitazione descrive come integrare HireVue con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0796-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0796-105">L'integrazione di HireVue con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0796-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0796-106">È possibile controllare in Azure AD chi può accedere a HireVue</span><span class="sxs-lookup"><span data-stu-id="c0796-106">You can control in Azure AD who has access to HireVue</span></span>
- <span data-ttu-id="c0796-107">È possibile abilitare gli utenti per l'accesso automatico a HireVue (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0796-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0796-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0796-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0796-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0796-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0796-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c0796-110">Prerequisites</span></span>

<span data-ttu-id="c0796-111">Per configurare l'integrazione di Azure AD con HireVue, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0796-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

- <span data-ttu-id="c0796-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0796-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0796-113">Sottoscrizione di HireVue abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c0796-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0796-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c0796-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0796-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0796-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0796-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c0796-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0796-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0796-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0796-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c0796-118">Scenario description</span></span>
<span data-ttu-id="c0796-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c0796-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0796-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0796-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0796-121">Aggiunta di HireVue dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c0796-121">Adding HireVue from the gallery</span></span>
2. <span data-ttu-id="c0796-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0796-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-the-gallery"></a><span data-ttu-id="c0796-123">Aggiunta di HireVue dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c0796-123">Adding HireVue from the gallery</span></span>
<span data-ttu-id="c0796-124">Per configurare l'integrazione di HireVue in Azure AD, è necessario aggiungere HireVue dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c0796-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0796-125">**Per aggiungere HireVue dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c0796-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0796-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c0796-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0796-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c0796-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0796-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c0796-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c0796-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0796-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c0796-133">Nella casella di ricerca digitare **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="c0796-133">In the search box, type **HireVue**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="c0796-135">Nel pannello dei risultati selezionare **HireVue** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0796-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0796-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0796-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0796-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HireVue in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c0796-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0796-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di HireVue che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0796-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="c0796-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in HireVue.</span><span class="sxs-lookup"><span data-stu-id="c0796-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="c0796-141">Per stabilire la relazione di collegamento, in HireVue assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c0796-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0796-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con HireVue, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0796-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0796-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c0796-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0796-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0796-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0796-145">**[Creazione di un utente test di HireVue](#creating-a-hirevue-test-user)**: per avere una controparte di Britta Simon in HireVue collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0796-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0796-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0796-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0796-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c0796-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0796-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0796-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0796-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione HireVue.</span><span class="sxs-lookup"><span data-stu-id="c0796-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="c0796-150">**Per configurare l'accesso Single Sign-On di Azure AD con HireVue, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c0796-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="c0796-151">Nella pagina di integrazione dell'applicazione **HireVue** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c0796-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c0796-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c0796-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="c0796-155">Nella sezione **URL e dominio HireVue** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c0796-155">On the **HireVue Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="c0796-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0796-157">a.</span></span> <span data-ttu-id="c0796-158">Nella casella di testo **URL di accesso** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="c0796-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="c0796-159">Environment</span><span class="sxs-lookup"><span data-stu-id="c0796-159">Environment</span></span> | <span data-ttu-id="c0796-160">URL</span><span class="sxs-lookup"><span data-stu-id="c0796-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="c0796-161">Produzione</span><span class="sxs-lookup"><span data-stu-id="c0796-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="c0796-162">Staging</span><span class="sxs-lookup"><span data-stu-id="c0796-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="c0796-163">b.</span><span class="sxs-lookup"><span data-stu-id="c0796-163">b.</span></span> <span data-ttu-id="c0796-164">Nella casella di testo **Identificatore** digitare un URL come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c0796-164">In the **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="c0796-165">Environment</span><span class="sxs-lookup"><span data-stu-id="c0796-165">Environment</span></span> | <span data-ttu-id="c0796-166">URN</span><span class="sxs-lookup"><span data-stu-id="c0796-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="c0796-167">Produzione</span><span class="sxs-lookup"><span data-stu-id="c0796-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="c0796-168">Staging</span><span class="sxs-lookup"><span data-stu-id="c0796-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="c0796-169">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c0796-169">These values are not real.</span></span> <span data-ttu-id="c0796-170">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c0796-170">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c0796-171">Per ottenere questi valori contattare il [team di supporto clienti di HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="c0796-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span></span> 
 
4. <span data-ttu-id="c0796-172">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="c0796-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="c0796-174">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c0796-174">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0796-176">Nella sezione **Configurazione di HireVue** fare clic su **Configura HireVue** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="c0796-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c0796-177">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c0796-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="c0796-179">Per configurare l'accesso Single Sign-On sul lato **HireVue** è necessario inviare il file **Certificato (Base64)** scaricato e i valori **Sign-Out URL (URL di disconnessione), SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** al [team di supporto di HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="c0796-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="c0796-180">L'applicazione viene configurata in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="c0796-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c0796-181">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c0796-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0796-182">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c0796-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0796-183">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0796-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0796-184">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0796-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0796-185">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0796-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c0796-187">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c0796-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0796-188">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c0796-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0796-190">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c0796-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0796-192">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c0796-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0796-194">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c0796-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0796-196">a.</span><span class="sxs-lookup"><span data-stu-id="c0796-196">a.</span></span> <span data-ttu-id="c0796-197">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0796-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0796-198">b.</span><span class="sxs-lookup"><span data-stu-id="c0796-198">b.</span></span> <span data-ttu-id="c0796-199">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0796-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0796-200">c.</span><span class="sxs-lookup"><span data-stu-id="c0796-200">c.</span></span> <span data-ttu-id="c0796-201">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c0796-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0796-202">d.</span><span class="sxs-lookup"><span data-stu-id="c0796-202">d.</span></span> <span data-ttu-id="c0796-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0796-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="c0796-204">Creazione di un utente test di HireVue</span><span class="sxs-lookup"><span data-stu-id="c0796-204">Creating a HireVue test user</span></span>

<span data-ttu-id="c0796-205">In questa sezione viene creato un utente di nome Britta Simon in HireVue.</span><span class="sxs-lookup"><span data-stu-id="c0796-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="c0796-206">Collaborare con il [team di supporto di HireVue](mailto:samlsupport@hirevue.com) per aggiungere gli utenti nella piattaforma HireVue.</span><span class="sxs-lookup"><span data-stu-id="c0796-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0796-207">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0796-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0796-208">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a HireVue.</span><span class="sxs-lookup"><span data-stu-id="c0796-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c0796-210">**Per assegnare Britta Simon a HireVue, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c0796-210">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="c0796-211">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c0796-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c0796-213">Nell'elenco delle applicazioni selezionare **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="c0796-213">In the applications list, select **HireVue**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="c0796-215">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c0796-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c0796-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c0796-217">Click **Add** button.</span></span> <span data-ttu-id="c0796-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c0796-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c0796-220">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c0796-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0796-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c0796-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0796-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c0796-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0796-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c0796-223">Testing single sign-on</span></span>

<span data-ttu-id="c0796-224">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c0796-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0796-225">Quando si fa clic sul riquadro HireVue nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione HireVue.</span><span class="sxs-lookup"><span data-stu-id="c0796-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0796-226">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c0796-226">Additional resources</span></span>

* [<span data-ttu-id="c0796-227">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0796-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0796-228">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0796-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png


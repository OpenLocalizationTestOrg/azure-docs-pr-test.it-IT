---
title: 'Esercitazione: Integrazione di Azure Active Directory con SpringCM | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SpringCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: edfd06a06c730597fee4569ca1ce29092b45244a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="bcc31-103">Esercitazione: Integrazione di Azure Active Directory con SpringCM</span><span class="sxs-lookup"><span data-stu-id="bcc31-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="bcc31-104">Questa esercitazione descrive come integrare SpringCM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bcc31-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bcc31-105">L'integrazione di SpringCM con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bcc31-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bcc31-106">È possibile controllare in Azure AD chi può accedere a SpringCM</span><span class="sxs-lookup"><span data-stu-id="bcc31-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="bcc31-107">È possibile abilitare gli utenti per l'accesso automatico a SpringCM (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc31-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bcc31-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc31-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bcc31-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bcc31-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcc31-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bcc31-110">Prerequisites</span></span>

<span data-ttu-id="bcc31-111">Per configurare l'integrazione di Azure AD con SpringCM, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bcc31-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="bcc31-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcc31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bcc31-113">Sottoscrizione di Spring CM abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bcc31-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bcc31-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bcc31-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bcc31-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bcc31-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bcc31-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bcc31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bcc31-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bcc31-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bcc31-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bcc31-118">Scenario description</span></span>
<span data-ttu-id="bcc31-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bcc31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bcc31-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bcc31-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bcc31-121">Aggiunta di SpringCM dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="bcc31-121">Adding SpringCM from the gallery</span></span>
2. <span data-ttu-id="bcc31-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc31-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="bcc31-123">Aggiunta di SpringCM dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="bcc31-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="bcc31-124">Per configurare l'integrazione di SpringCM in Azure AD, è necessario aggiungere SpringCM dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bcc31-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bcc31-125">**Per aggiungere SpringCM dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bcc31-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bcc31-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="bcc31-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bcc31-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bcc31-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="bcc31-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="bcc31-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="bcc31-133">Nella casella di ricerca digitare **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-133">In the search box, type **SpringCM**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="bcc31-135">Nel pannello dei risultati selezionare **SpringCM** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bcc31-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bcc31-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc31-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bcc31-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SpringCM con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bcc31-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bcc31-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SpringCM che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcc31-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="bcc31-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SpringCM.</span><span class="sxs-lookup"><span data-stu-id="bcc31-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="bcc31-141">Per stabilire la relazione di collegamento, in SpringCM assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="bcc31-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bcc31-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SpringCM, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bcc31-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bcc31-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bcc31-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bcc31-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bcc31-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bcc31-145">**[Creazione di un utente di test di SpringCM](#creating-a-springcm-test-user)**: per avere una controparte di Britta Simon in SpringCM collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcc31-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bcc31-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcc31-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bcc31-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="bcc31-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bcc31-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc31-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bcc31-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SpringCM.</span><span class="sxs-lookup"><span data-stu-id="bcc31-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="bcc31-150">**Per configurare Single Sign-On di Azure AD con SpringCM, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bcc31-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="bcc31-151">Nella pagina di integrazione dell'applicazione **SpringCM** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="bcc31-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="bcc31-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="bcc31-155">Nella sezione **URL e dominio SpringCM** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bcc31-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="bcc31-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="bcc31-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bcc31-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="bcc31-158">This value is not real.</span></span> <span data-ttu-id="bcc31-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="bcc31-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="bcc31-160">Per ottenere questo valore, contattare il [team di supporto clienti di SpringCM](https://knowledge.springcm.com/support).</span><span class="sxs-lookup"><span data-stu-id="bcc31-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
4. <span data-ttu-id="bcc31-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (base)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="bcc31-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="bcc31-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bcc31-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bcc31-165">Nella sezione **Configurazione di SpringCM** fare clic su **Configura SpringCM** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bcc31-166">Copiare i valori **SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="bcc31-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="bcc31-168">In un'altra finestra del browser Web accedere al sito aziendale di **SpringCM** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bcc31-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="bcc31-169">Nel menu nella parte superiore fare clic su **Vai a**, scegliere **Preferenze**, quindi nella scheda **Preferenze account** fare clic su **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="bcc31-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="bcc31-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="bcc31-171">Nella sezione Configurazione provider di identità, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bcc31-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="bcc31-172">![Configurazione del provider di identità](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Configurazione del provider di identità")</span><span class="sxs-lookup"><span data-stu-id="bcc31-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="bcc31-173">a.</span><span class="sxs-lookup"><span data-stu-id="bcc31-173">a.</span></span> <span data-ttu-id="bcc31-174">Per caricare il certificato di Azure Active Directory scaricato, fare clic su **Seleziona certificato autorità di certificazione** o su **Cambia certificato autorità di certificazione**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="bcc31-175">b.</span><span class="sxs-lookup"><span data-stu-id="bcc31-175">b.</span></span> <span data-ttu-id="bcc31-176">Incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure nella casella di testo **Autorità di certificazione**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="bcc31-177">c.</span><span class="sxs-lookup"><span data-stu-id="bcc31-177">c.</span></span> <span data-ttu-id="bcc31-178">Incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **Service Provider (SP) Initiated Endpoint** (Endpoint avviato da provider di servizi).</span><span class="sxs-lookup"><span data-stu-id="bcc31-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="bcc31-179">d.</span><span class="sxs-lookup"><span data-stu-id="bcc31-179">d.</span></span> <span data-ttu-id="bcc31-180">Selezionare **Abilitato SAML** in modo che sia **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="bcc31-181">e.</span><span class="sxs-lookup"><span data-stu-id="bcc31-181">e.</span></span> <span data-ttu-id="bcc31-182">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="bcc31-183">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="bcc31-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bcc31-184">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="bcc31-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bcc31-185">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bcc31-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bcc31-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc31-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="bcc31-187">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc31-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="bcc31-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bcc31-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bcc31-190">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="bcc31-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bcc31-192">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="bcc31-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bcc31-194">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bcc31-196">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bcc31-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bcc31-198">a.</span><span class="sxs-lookup"><span data-stu-id="bcc31-198">a.</span></span> <span data-ttu-id="bcc31-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bcc31-200">b.</span><span class="sxs-lookup"><span data-stu-id="bcc31-200">b.</span></span> <span data-ttu-id="bcc31-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bcc31-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bcc31-202">c.</span><span class="sxs-lookup"><span data-stu-id="bcc31-202">c.</span></span> <span data-ttu-id="bcc31-203">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bcc31-204">d.</span><span class="sxs-lookup"><span data-stu-id="bcc31-204">d.</span></span> <span data-ttu-id="bcc31-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="bcc31-206">Creazione di un utente di test di SpringCM</span><span class="sxs-lookup"><span data-stu-id="bcc31-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="bcc31-207">Per consentire agli utenti di Azure Active Directory di accedere a SpringCM, è necessario eseguirne il provisioning in SpringCM.</span><span class="sxs-lookup"><span data-stu-id="bcc31-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="bcc31-208">Nel caso di SpringCM, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="bcc31-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="bcc31-209">Per altre informazioni, vedere [Creare e modificare un utente SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="bcc31-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="bcc31-210">**Per eseguire il provisioning di un account utente in SpringCM, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bcc31-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="bcc31-211">Accedere al sito aziendale di **SpringCM** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bcc31-211">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="bcc31-212">Fare clic su **GOTO** e scegliere **RUBRICA**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="bcc31-213">![Crea utente](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="bcc31-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="bcc31-214">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-214">Click **Create User**.</span></span>

4. <span data-ttu-id="bcc31-215">Selezionare un **Ruolo utente**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="bcc31-216">Selezionare **Invia messaggio di attivazione**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="bcc31-217">Digitare il nome, il cognome, il titolo e l'indirizzo di posta elettronica di un account utente di Azure Active Directory valido di cui si desidera effettuare il provisioning nelle caselle di testo correlate.</span><span class="sxs-lookup"><span data-stu-id="bcc31-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="bcc31-218">Aggiungere l'utente a un **Gruppo di protezione**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-218">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="bcc31-219">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="bcc31-220">È possibile usare qualsiasi altro strumento di creazione di account utente SpringCM o API fornita da SpringCM per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcc31-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bcc31-221">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc31-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bcc31-222">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a SpringCM.</span><span class="sxs-lookup"><span data-stu-id="bcc31-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![Assegna utente][200] 

<span data-ttu-id="bcc31-224">**Per assegnare Britta Simon a SpringCM seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bcc31-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="bcc31-225">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bcc31-227">Nell'elenco delle applicazioni selezionare **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-227">In the applications list, select **SpringCM**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="bcc31-229">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="bcc31-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="bcc31-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-231">Click **Add** button.</span></span> <span data-ttu-id="bcc31-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="bcc31-234">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="bcc31-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bcc31-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bcc31-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bcc31-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bcc31-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bcc31-237">Testing single sign-on</span></span>

<span data-ttu-id="bcc31-238">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bcc31-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="bcc31-239">Quando si fa clic sul riquadro SpringCM nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione SpringCM.</span><span class="sxs-lookup"><span data-stu-id="bcc31-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="bcc31-240">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bcc31-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bcc31-241">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bcc31-241">Additional resources</span></span>

* [<span data-ttu-id="bcc31-242">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bcc31-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bcc31-243">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bcc31-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png


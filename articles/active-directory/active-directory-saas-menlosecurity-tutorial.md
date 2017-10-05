---
title: 'Esercitazione: Integrazione di Azure Active Directory con Menlo Security | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Menlo Security.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="3ecc5-103">Esercitazione: Integrazione di Azure Active Directory con Menlo Security</span><span class="sxs-lookup"><span data-stu-id="3ecc5-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="3ecc5-104">Questa esercitazione descrive come integrare Menlo Security con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ecc5-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ecc5-105">L'integrazione di Menlo Security con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ecc5-106">È possibile controllare in Azure AD chi può accedere a Menlo Security</span><span class="sxs-lookup"><span data-stu-id="3ecc5-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="3ecc5-107">È possibile abilitare gli utenti per l'accesso automatico a Menlo Security (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ecc5-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ecc5-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3ecc5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ecc5-109">Per altre informazioni sull'integrazione di app SaaS con Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="3ecc5-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ecc5-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ecc5-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3ecc5-111">Prerequisites</span></span>

<span data-ttu-id="3ecc5-112">Per configurare l'integrazione di Azure AD con Menlo Security, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="3ecc5-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-113">An Azure AD subscription</span></span>
- <span data-ttu-id="3ecc5-114">Sottoscrizione di Menlo Security abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ecc5-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ecc5-116">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ecc5-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ecc5-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ecc5-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ecc5-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3ecc5-119">Scenario description</span></span>
<span data-ttu-id="3ecc5-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ecc5-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ecc5-122">Aggiunta di Menlo Security dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3ecc5-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="3ecc5-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ecc5-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="3ecc5-124">Aggiunta di Menlo Security dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3ecc5-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="3ecc5-125">Per configurare l'integrazione di Menlo Security in Azure AD, è necessario aggiungere Menlo Security dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ecc5-126">**Per aggiungere Menlo Security dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ecc5-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ecc5-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ecc5-129">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ecc5-130">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-130">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3ecc5-132">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3ecc5-134">Nella casella di ricerca digitare **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-134">In the search box, type **Menlo Security**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="3ecc5-136">Nel pannello dei risultati selezionare **Menlo Security** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ecc5-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ecc5-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ecc5-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Menlo Security con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ecc5-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3ecc5-140">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Menlo Security che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="3ecc5-141">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="3ecc5-142">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** in Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="3ecc5-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con Menlo Security, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ecc5-144">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ecc5-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ecc5-146">**[Creazione di un utente test di Menlo Security](#creating-a-menlo-security-test-user)**: per avere una controparte di Britta Simon in Menlo Security collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ecc5-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ecc5-148">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ecc5-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ecc5-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ecc5-150">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="3ecc5-151">**Per configurare Single Sign-On di Azure AD con Menlo Security, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ecc5-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="3ecc5-152">Nella pagina di integrazione dell'applicazione **Menlo Security** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3ecc5-154">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="3ecc5-156">Nella sezione **URL e dominio Menlo Security** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="3ecc5-158">a.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-158">a.</span></span> <span data-ttu-id="3ecc5-159">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.menlosecurity.com/account/login`.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="3ecc5-160">b.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-160">b.</span></span> <span data-ttu-id="3ecc5-161">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="3ecc5-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ecc5-162">Questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-162">These values are not the real.</span></span> <span data-ttu-id="3ecc5-163">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3ecc5-164">Per ottenere questi valori, contattare il [team di supporto clienti di Menlo Security](https://www.menlosecurity.com/menlo-contact).</span><span class="sxs-lookup"><span data-stu-id="3ecc5-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="3ecc5-165">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="3ecc5-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3ecc5-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ecc5-169">Nella sezione **Configurazione di Menlo Security** fare clic su **Configura Menlo Security** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3ecc5-170">Copiare l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="3ecc5-172">Per configurare l'accesso Single Sign-On sul lato **Menlo Security**, accedere al sito Web aziendale di **Menlo Security** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="3ecc5-173">In **Impostazioni** passare a **Autenticazione** ed eseguire le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="3ecc5-175">a.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-175">a.</span></span> <span data-ttu-id="3ecc5-176">Selezionare la casella di controllo **Enable user authentication using SAML** (Abilita autenticazione utente tramite SAML).</span><span class="sxs-lookup"><span data-stu-id="3ecc5-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="3ecc5-177">b.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-177">b.</span></span> <span data-ttu-id="3ecc5-178">Impostare **Allow External Access** (Consenti accesso esterno) su **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="3ecc5-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="3ecc5-179">c.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-179">c.</span></span> <span data-ttu-id="3ecc5-180">In **SAML Provider** (Provider SAML), selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="3ecc5-181">d.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-181">d.</span></span> <span data-ttu-id="3ecc5-182">**SAML 2.0 Endpoint** (Endpoint SAML 2.): copiare l'**URL servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3ecc5-183">e.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-183">e.</span></span> <span data-ttu-id="3ecc5-184">**Service Identifier (Issuer)** (Identificatore servizio (Autorità emittente)): incollare l'**ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3ecc5-185">f.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-185">f.</span></span> <span data-ttu-id="3ecc5-186">**X.509 Certificate** (Certificato X.509): aprire il certificato **Certificate (Base64)** scaricato dal portale di Azure nel blocco note e copiarlo in questa casella.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="3ecc5-187">g.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-187">g.</span></span> <span data-ttu-id="3ecc5-188">Fare clic su **Salva** per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="3ecc5-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ecc5-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ecc5-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ecc5-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ecc5-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ecc5-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ecc5-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3ecc5-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ecc5-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ecc5-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ecc5-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ecc5-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ecc5-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ecc5-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ecc5-204">a.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-204">a.</span></span> <span data-ttu-id="3ecc5-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ecc5-206">b.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-206">b.</span></span> <span data-ttu-id="3ecc5-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ecc5-208">c.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-208">c.</span></span> <span data-ttu-id="3ecc5-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ecc5-210">d.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-210">d.</span></span> <span data-ttu-id="3ecc5-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="3ecc5-212">Creazione di un utente test di Menlo Security</span><span class="sxs-lookup"><span data-stu-id="3ecc5-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="3ecc5-213">In questa sezione viene creato un utente chiamato Britta Simon in Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="3ecc5-214">Collaborare con il [team di supporto clienti di Menlo Security](https://www.menlosecurity.com/menlo-contact) per aggiungere gli utenti alla piattaforma Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="3ecc5-215">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ecc5-216">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ecc5-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ecc5-217">In questa sezione, Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3ecc5-219">**Per assegnare Britta Simon a Menlo Security, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ecc5-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="3ecc5-220">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3ecc5-222">Nell'elenco di applicazioni selezionare **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-222">In the applications list, select **Menlo Security**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="3ecc5-224">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3ecc5-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-226">Click **Add** button.</span></span> <span data-ttu-id="3ecc5-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3ecc5-229">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ecc5-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ecc5-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ecc5-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3ecc5-232">Testing single sign-on</span></span>

<span data-ttu-id="3ecc5-233">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="3ecc5-234">Aprire una finestra del browser in modalità "InPrivate" o "In incognito" per attivare una nuova autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="3ecc5-235">In Internet Explorer usare CTRL+MAIUSC+P.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="3ecc5-236">In Chrome usare CTRL+MAIUSC+N.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="3ecc5-237">Nella finestra di esplorazione privata passare a una risorsa protetta ed eseguire un accesso ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="3ecc5-238">Dopo aver eseguito l'accesso, il sito richiesto verrà aperto in una sessione di isolamento.</span><span class="sxs-lookup"><span data-stu-id="3ecc5-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ecc5-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3ecc5-239">Additional resources</span></span>

* [<span data-ttu-id="3ecc5-240">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ecc5-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ecc5-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ecc5-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png


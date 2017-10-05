---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mozy Enterprise | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Mozy Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="e7e8d-103">Esercitazione: Integrazione di Azure Active Directory con Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="e7e8d-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="e7e8d-104">Questa esercitazione descrive come integrare Mozy Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7e8d-105">L'integrazione di Mozy Enterprise con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7e8d-106">È possibile controllare in Azure AD chi può accedere a Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="e7e8d-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="e7e8d-107">È possibile abilitare gli utenti per l'accesso automatico a Mozy Enterprise (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="e7e8d-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7e8d-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7e8d-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7e8d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e7e8d-110">Prerequisites</span></span>

<span data-ttu-id="e7e8d-111">Per configurare l'integrazione di Azure AD con Mozy Enterprise, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="e7e8d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7e8d-113">Sottoscrizione di Mozy Enterprise abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7e8d-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7e8d-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7e8d-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7e8d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7e8d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7e8d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e7e8d-118">Scenario description</span></span>
<span data-ttu-id="e7e8d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7e8d-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7e8d-121">Aggiunta di Mozy Enterprise dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e7e8d-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="e7e8d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7e8d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="e7e8d-123">Aggiunta di Mozy Enterprise dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e7e8d-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="e7e8d-124">Per configurare l'integrazione di Mozy Enterprise in Azure AD, è necessario aggiungere Mozy Enterprise dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7e8d-125">**Per aggiungere Mozy Enterprise dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e7e8d-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7e8d-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7e8d-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7e8d-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e7e8d-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e7e8d-133">Nella casella di ricerca digitare **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="e7e8d-135">Nel pannello dei risultati selezionare **Mozy Enterprise** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7e8d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7e8d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7e8d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mozy Enterprise usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7e8d-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7e8d-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Mozy Enterprise corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="e7e8d-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="e7e8d-141">Per stabilire la relazione di collegamento, in Mozy Enterprise assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7e8d-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Mozy Enterprise, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7e8d-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7e8d-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7e8d-145">**[Creazione di un utente di test di Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**: per avere una controparte di Britta Simon in Mozy Enterprise collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7e8d-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7e8d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7e8d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7e8d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7e8d-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="e7e8d-150">**Per configurare l'accesso Single Sign-On di Azure AD con Mozy Enterprise, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e7e8d-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="e7e8d-151">Nella pagina di integrazione dell'applicazione **Mozy Enterprise** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e7e8d-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="e7e8d-155">Nella sezione **URL e dominio Mozy Enterprise** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="e7e8d-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="e7e8d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7e8d-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="e7e8d-158">This value is not real.</span></span> <span data-ttu-id="e7e8d-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e7e8d-160">Per ottenere questo valore, contattare il [team di supporto di Mozy Enterprise](http://support.mozy.com/).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="e7e8d-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="e7e8d-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e7e8d-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7e8d-165">Nella sezione **Configurazione di Mozy Enterprise** fare clic su **Configura Mozy Enterprise** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e7e8d-166">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="e7e8d-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="e7e8d-168">In un'altra finestra del Web browser accedere al sito aziendale di Mozy Enterprise come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="e7e8d-169">Nella sezione **Configuration** fare clic su **Authentication Policy**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="e7e8d-170">![Criteri di autenticazione](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Criteri di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="e7e8d-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="e7e8d-171">Nella sezione **Authentication Policy** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="e7e8d-172">![Criteri di autenticazione](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Criteri di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="e7e8d-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="e7e8d-173">a.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-173">a.</span></span> <span data-ttu-id="e7e8d-174">Selezionare **Directory Service** come **Provider**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="e7e8d-175">b.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-175">b.</span></span> <span data-ttu-id="e7e8d-176">Selezionare **Use LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="e7e8d-177">c.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-177">c.</span></span> <span data-ttu-id="e7e8d-178">Fare clic sulla scheda **SAML Authentication** .</span><span class="sxs-lookup"><span data-stu-id="e7e8d-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="e7e8d-179">d.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-179">d.</span></span> <span data-ttu-id="e7e8d-180">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **Authentication URL** (URL di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="e7e8d-181">e.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-181">e.</span></span> <span data-ttu-id="e7e8d-182">Incollare l'**ID di entità SAML** copiato dal portale di Azure nella casella di testo **SAML Endpoint** (Endpoint SAML).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="e7e8d-183">f.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-183">f.</span></span> <span data-ttu-id="e7e8d-184">Aprire il certificato con codifica Base 64 scaricato nel Blocco note, copiarne il contenuto negli Appunti e incollare l'intero certificato nella casella di testo **SAML Certificate** (Certificato SAML).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="e7e8d-185">g.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-185">g.</span></span> <span data-ttu-id="e7e8d-186">Selezionare **Abilita SSO per consentire agli amministratori di accedere con le proprie credenziali di rete**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="e7e8d-187">h.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-187">h.</span></span> <span data-ttu-id="e7e8d-188">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e7e8d-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7e8d-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7e8d-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7e8d-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7e8d-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7e8d-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e7e8d-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7e8d-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7e8d-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7e8d-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7e8d-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7e8d-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7e8d-204">a.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-204">a.</span></span> <span data-ttu-id="e7e8d-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7e8d-206">b.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-206">b.</span></span> <span data-ttu-id="e7e8d-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7e8d-208">c.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-208">c.</span></span> <span data-ttu-id="e7e8d-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7e8d-210">d.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-210">d.</span></span> <span data-ttu-id="e7e8d-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="e7e8d-212">Creazione di un utente di test di Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="e7e8d-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="e7e8d-213">Per consentire agli utenti di Azure AD di accedere a Mozy Enterprise, è necessario eseguirne il provisioning in Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="e7e8d-214">Nel caso di Mozy Enterprise, il provisioning è un’attività manuale.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e7e8d-215">È possibile utilizzare qualsiasi altro strumento di creazione di account utente di Mozy Enterprise o le API fornite da Mozy Enterprise per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="e7e8d-216">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e7e8d-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="e7e8d-217">Accedere al tenant **Mozy Enterprise** .</span><span class="sxs-lookup"><span data-stu-id="e7e8d-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="e7e8d-218">Fare clic su **Users** (Utenti) e quindi fare clic su **Add New User** (Aggiungi nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="e7e8d-219">![Utenti](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="e7e8d-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e7e8d-220">L'opzione **Add New User** (Aggiungi nuovo utente) viene visualizzata solo se **Mozy** è selezionato come provider in **Authentication policy** (Criteri di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="e7e8d-221">Se è configurata l'autenticazione SAML gli utenti vengono aggiunti automaticamente al primo accesso tramite Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="e7e8d-222">Nella finestra di dialogo Nuovo utente eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7e8d-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="e7e8d-223">![Aggiungere utenti](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="e7e8d-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="e7e8d-224">a.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-224">a.</span></span> <span data-ttu-id="e7e8d-225">Dall’elenco **Choose a group** selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="e7e8d-226">b.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-226">b.</span></span> <span data-ttu-id="e7e8d-227">Dall’elenco **What tupe of user** selezionare un tipo.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="e7e8d-228">c.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-228">c.</span></span> <span data-ttu-id="e7e8d-229">Nella casella di testo **Nome utente** digitare il nome dell'utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="e7e8d-230">d.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-230">d.</span></span> <span data-ttu-id="e7e8d-231">Nella casella di testo **Email** digitare l'indirizzo di posta elettronica dell'utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="e7e8d-232">e.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-232">e.</span></span> <span data-ttu-id="e7e8d-233">Selezionare **Send user instruction email**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="e7e8d-234">f.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-234">f.</span></span> <span data-ttu-id="e7e8d-235">Fare clic su **Add User(s)**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="e7e8d-236">Dopo aver creato l'utente, verrà inviato un messaggio di posta elettronica all'utente di Azure AD con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7e8d-237">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7e8d-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7e8d-238">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e7e8d-240">**Per assegnare Britta Simon a Mozy Enterprise, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e7e8d-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="e7e8d-241">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e7e8d-243">Nell'elenco delle applicazioni selezionare **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="e7e8d-245">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e7e8d-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-247">Click **Add** button.</span></span> <span data-ttu-id="e7e8d-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e7e8d-250">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7e8d-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7e8d-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7e8d-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7e8d-253">Testing single sign-on</span></span>

<span data-ttu-id="e7e8d-254">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e7e8d-255">Quando si fa clic sul riquadro Mozy Enterprise nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7e8d-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="e7e8d-256">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7e8d-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7e8d-257">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e7e8d-257">Additional resources</span></span>

* [<span data-ttu-id="e7e8d-258">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7e8d-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7e8d-259">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7e8d-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Keeper Password Manager & Digital Vault | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Keeper Password Manager & Digital Vault.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 36504a281756b980e3348e7f892ba08821873b52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="22f15-103">Esercitazione: Integrazione di Azure Active Directory con Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="22f15-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="22f15-104">Questa esercitazione descrive come integrare Keeper Password Manager & Digital Vault con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22f15-104">In this tutorial, you learn how to integrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22f15-105">L'integrazione di Keeper Password Manager & Digital Vault con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f15-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="22f15-106">È possibile controllare in Azure AD chi può accedere a Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="22f15-106">You can control in Azure AD who has access to Keeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="22f15-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Keeper Password Manager & Digital Vault con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f15-107">You can enable your users to automatically get signed-on to Keeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22f15-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f15-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="22f15-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22f15-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22f15-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="22f15-110">Prerequisites</span></span>

<span data-ttu-id="22f15-111">Per configurare l'integrazione di Azure AD con Keeper Password Manager & Digital Vault sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f15-111">To configure Azure AD integration with Keeper Password Manager & Digital Vault, you need the following items:</span></span>

- <span data-ttu-id="22f15-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22f15-113">Sottoscrizione di Keeper Password Manager & Digital Vault abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="22f15-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22f15-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="22f15-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22f15-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f15-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22f15-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="22f15-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22f15-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22f15-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22f15-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="22f15-118">Scenario description</span></span>
<span data-ttu-id="22f15-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="22f15-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22f15-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f15-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22f15-121">Aggiunta di Keeper Password Manager & Digital Vault dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="22f15-121">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
2. <span data-ttu-id="22f15-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f15-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a><span data-ttu-id="22f15-123">Aggiunta di Keeper Password Manager & Digital Vault dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="22f15-123">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
<span data-ttu-id="22f15-124">Per configurare l'integrazione di Keeper Password Manager & Digital Vault in Azure AD è necessario aggiungere Keeper Password Manager & Digital Vault dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="22f15-124">To configure the integration of Keeper Password Manager & Digital Vault into Azure AD, you need to add Keeper Password Manager & Digital Vault from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="22f15-125">**Per aggiungere Keeper Password Manager & Digital Vault dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="22f15-125">**To add Keeper Password Manager & Digital Vault from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="22f15-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="22f15-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22f15-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="22f15-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="22f15-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22f15-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="22f15-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="22f15-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="22f15-133">Nella casella di ricerca digitare **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="22f15-133">In the search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="22f15-135">Nel pannello dei risultati selezionare **Keeper Password Manager & Digital Vault** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22f15-135">In the results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22f15-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f15-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22f15-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Keeper Password Manager & Digital Vault mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="22f15-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="22f15-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Keeper Password Manager & Digital Vault corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f15-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Keeper Password Manager & Digital Vault is to a user in Azure AD.</span></span> <span data-ttu-id="22f15-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="22f15-140">In other words, a link relationship between an Azure AD user and the related user in Keeper Password Manager & Digital Vault needs to be established.</span></span>

<span data-ttu-id="22f15-141">Per stabilire la relazione di collegamento, in Keeper Password Manager & Digital Vault assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="22f15-141">In Keeper Password Manager & Digital Vault, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="22f15-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Keeper Password Manager & Digital Vault è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f15-142">To configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="22f15-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="22f15-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="22f15-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22f15-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22f15-145">**[Creazione di un utente test di Keeper Password Manager & Digital Vault](#creating-a-keeperpasswordmanager-test-user)**: per avere una controparte di Britta Simon in Keeper Password Manager & Digital Vault collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f15-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - to have a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="22f15-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f15-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22f15-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="22f15-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22f15-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f15-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22f15-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="22f15-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="22f15-150">**Per configurare l'accesso Single Sign-On di Azure AD con Keeper Password Manager & Digital Vault, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="22f15-150">**To configure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="22f15-151">Nella pagina di integrazione dell'applicazione **Keeper Password Manager & Digital Vault** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="22f15-151">In the Azure portal, on the **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="22f15-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="22f15-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="22f15-155">Nella sezione **URL e dominio Keeper Password Manager & Digital Vault** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="22f15-155">On the **Keeper Password Manager & Digital Vault Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="22f15-157">a.</span><span class="sxs-lookup"><span data-stu-id="22f15-157">a.</span></span> <span data-ttu-id="22f15-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`.</span><span class="sxs-lookup"><span data-stu-id="22f15-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="22f15-159">b.</span><span class="sxs-lookup"><span data-stu-id="22f15-159">b.</span></span> <span data-ttu-id="22f15-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="22f15-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="22f15-161">c.</span><span class="sxs-lookup"><span data-stu-id="22f15-161">c.</span></span> <span data-ttu-id="22f15-162">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="22f15-162">In the **Identifier** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="22f15-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="22f15-163">These values are not real.</span></span> <span data-ttu-id="22f15-164">è necessario aggiornarli con l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="22f15-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="22f15-165">Per ottenere questi valori contattare il [team di supporto clienti di Keeper Password Manager & Digital Vault](https://keepersecurity.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="22f15-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="22f15-166">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="22f15-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="22f15-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="22f15-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="22f15-170">Nella sezione **Configurazione di Keeper Password Manager & Digital Vault** fare clic su **Configura Keeper Password Manager & Digital Vault** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="22f15-170">On the **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** to open **Configure sign-on** window.</span></span> <span data-ttu-id="22f15-171">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="22f15-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="22f15-173">Per configurare l'accesso Single Sign-On sul lato **Keeper Password Manager & Digital Vault**, seguire le istruzioni specificate nella [Guida per il supporto di Keeper](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf).</span><span class="sxs-lookup"><span data-stu-id="22f15-173">To configure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow the guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="22f15-174">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="22f15-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="22f15-175">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="22f15-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="22f15-176">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22f15-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22f15-177">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f15-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="22f15-178">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f15-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="22f15-180">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22f15-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="22f15-181">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="22f15-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22f15-183">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="22f15-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22f15-185">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="22f15-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22f15-187">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="22f15-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22f15-189">a.</span><span class="sxs-lookup"><span data-stu-id="22f15-189">a.</span></span> <span data-ttu-id="22f15-190">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22f15-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22f15-191">b.</span><span class="sxs-lookup"><span data-stu-id="22f15-191">b.</span></span> <span data-ttu-id="22f15-192">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="22f15-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22f15-193">c.</span><span class="sxs-lookup"><span data-stu-id="22f15-193">c.</span></span> <span data-ttu-id="22f15-194">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="22f15-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="22f15-195">d.</span><span class="sxs-lookup"><span data-stu-id="22f15-195">d.</span></span> <span data-ttu-id="22f15-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="22f15-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="22f15-197">Creazione di un utente test di Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="22f15-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="22f15-198">Per consentire agli utenti di Azure AD di accedere a Keeper Password Manager & Digital Vault, è necessario eseguire il provisioning degli utenti in Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="22f15-198">To enable Azure AD users to log in to Keeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="22f15-199">L'applicazione supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti verranno automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22f15-199">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="22f15-200">Per configurare manualmente gli utenti, contattare il [supporto di Keeper](https://keepersecurity.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="22f15-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want to setup users manually.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="22f15-201">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f15-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="22f15-202">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="22f15-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Keeper Password Manager & Digital Vault.</span></span>

![Assegna utente][200] 

<span data-ttu-id="22f15-204">**Per assegnare Britta Simon a Keeper Password Manager & Digital Vault, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="22f15-204">**To assign Britta Simon to Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="22f15-205">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22f15-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="22f15-207">Nell'elenco delle applicazioni selezionare **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="22f15-207">In the applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="22f15-209">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="22f15-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="22f15-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22f15-211">Click **Add** button.</span></span> <span data-ttu-id="22f15-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22f15-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="22f15-214">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="22f15-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="22f15-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="22f15-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22f15-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22f15-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="22f15-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="22f15-217">Testing single sign-on</span></span>

<span data-ttu-id="22f15-218">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="22f15-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="22f15-219">Quando si fa clic sul riquadro Keeper Password Manager & Digital Vault nel pannello di accesso viene visualizzata la pagina di accesso all'applicazione Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="22f15-219">When you click the Keeper Password Manager & Digital Vault tile in the Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="22f15-220">Dopo aver completato l'autenticazione si accede all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22f15-220">Upon successful authentication, you should get into the application.</span></span> <span data-ttu-id="22f15-221">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="22f15-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="22f15-222">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="22f15-222">Additional resources</span></span>

* [<span data-ttu-id="22f15-223">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f15-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22f15-224">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f15-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Veritas Enterprise Vault.cloud SSO | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Veritas Enterprise Vault.cloud SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 1f8c7fd97021f320a23bc78466a7b61f2d7e513e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a><span data-ttu-id="94ca4-103">Esercitazione: Integrazione di Azure Active Directory con Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="94ca4-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span></span>

<span data-ttu-id="94ca4-104">Questa esercitazione descrive come integrare Veritas Enterprise Vault.cloud SSO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94ca4-104">In this tutorial, you learn how to integrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94ca4-105">L'integrazione di Veritas Enterprise Vault.cloud SSO con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="94ca4-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94ca4-106">È possibile controllare in Azure AD chi può accedere a Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="94ca4-106">You can control in Azure AD who has access to Veritas Enterprise Vault.cloud SSO</span></span>
- <span data-ttu-id="94ca4-107">È possibile abilitare gli utenti per l'accesso automatico a Veritas Enterprise Vault.cloud SSO (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ca4-107">You can enable your users to automatically get signed-on to Veritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94ca4-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94ca4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="94ca4-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94ca4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94ca4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94ca4-110">Prerequisites</span></span>

<span data-ttu-id="94ca4-111">Per configurare l'integrazione di Azure AD con Veritas Enterprise Vault.cloud SSO, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="94ca4-111">To configure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need the following items:</span></span>

- <span data-ttu-id="94ca4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ca4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94ca4-113">Sottoscrizione di Veritas Enterprise Vault.cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="94ca4-113">A Veritas Enterprise Vault.cloud SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94ca4-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94ca4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94ca4-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="94ca4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94ca4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="94ca4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94ca4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94ca4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94ca4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="94ca4-118">Scenario description</span></span>
<span data-ttu-id="94ca4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="94ca4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94ca4-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94ca4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94ca4-121">Aggiunta di Veritas Enterprise Vault.cloud SSO dalla galleria</span><span class="sxs-lookup"><span data-stu-id="94ca4-121">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
2. <span data-ttu-id="94ca4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ca4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-the-gallery"></a><span data-ttu-id="94ca4-123">Aggiunta di Veritas Enterprise Vault.cloud SSO dalla galleria</span><span class="sxs-lookup"><span data-stu-id="94ca4-123">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
<span data-ttu-id="94ca4-124">Per configurare l'integrazione di Veritas Enterprise Vault.cloud SSO in Azure AD, è necessario aggiungere Veritas Enterprise Vault.cloud SSO dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="94ca4-124">To configure the integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need to add Veritas Enterprise Vault.cloud SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94ca4-125">**Per aggiungere Veritas Enterprise Vault.cloud SSO, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94ca4-125">**To add Veritas Enterprise Vault.cloud SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94ca4-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94ca4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94ca4-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94ca4-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="94ca4-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="94ca4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="94ca4-133">Nella casella di ricerca digitare **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-133">In the search box, type **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_search.png)

5. <span data-ttu-id="94ca4-135">Nel pannello dei risultati selezionare **Veritas Enterprise Vault.cloud SSO** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94ca4-135">In the results panel, select **Veritas Enterprise Vault.cloud SSO**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94ca4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ca4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94ca4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Veritas Enterprise Vault.cloud SSO usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94ca4-138">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94ca4-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Veritas Enterprise Vault.cloud SSO che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ca4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Veritas Enterprise Vault.cloud SSO is to a user in Azure AD.</span></span> <span data-ttu-id="94ca4-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="94ca4-140">In other words, a link relationship between an Azure AD user and the related user in Veritas Enterprise Vault.cloud SSO needs to be established.</span></span>

<span data-ttu-id="94ca4-141">Per stabilire la relazione di collegamento, in Veritas Enterprise Vault.cloud SSO assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="94ca4-141">In Veritas Enterprise Vault.cloud SSO, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="94ca4-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Veritas Enterprise Vault.cloud SSO, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94ca4-142">To configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94ca4-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="94ca4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="94ca4-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94ca4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94ca4-145">**[Creazione di un utente di test di Veritas Enterprise Vault.cloud SSO](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)**: per avere una controparte di Britta Simon in Veritas Enterprise Vault.cloud SSO collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ca4-145">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - to have a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="94ca4-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ca4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94ca4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="94ca4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94ca4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ca4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94ca4-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="94ca4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span></span>

<span data-ttu-id="94ca4-150">**Per configurare l'accesso Single Sign-On di Azure AD con Veritas Enterprise Vault.cloud SSO, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94ca4-150">**To configure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="94ca4-151">Nella pagina di integrazione dell'applicazione **Veritas Enterprise Vault.cloud SSO** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-151">In the Azure portal, on the **Veritas Enterprise Vault.cloud SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="94ca4-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94ca4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_samlbase.png)

3. <span data-ttu-id="94ca4-155">Nella sezione **URL e dominio Veritas Enterprise Vault.cloud SSO** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94ca4-155">On the **Veritas Enterprise Vault.cloud SSO Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_url.png)

    <span data-ttu-id="94ca4-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span><span class="sxs-lookup"><span data-stu-id="94ca4-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="94ca4-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="94ca4-158">This value is not real.</span></span> <span data-ttu-id="94ca4-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="94ca4-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="94ca4-160">Per ottenere questo valore, contattare il [team di supporto clienti di Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html).</span><span class="sxs-lookup"><span data-stu-id="94ca4-160">Contact [Veritas Enterprise Vault.cloud SSO Client support team](https://www.veritas.com/support/.html) to get this value.</span></span> 

4. <span data-ttu-id="94ca4-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="94ca4-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_certificate.png) 

5. <span data-ttu-id="94ca4-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="94ca4-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="94ca4-165">Nella sezione **Configurazione di Veritas Enterprise Vault.cloud SSO** fare clic su **Configura Veritas Enterprise Vault.cloud SSO** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-165">On the **Veritas Enterprise Vault.cloud SSO Configuration** section, click **Configure Veritas Enterprise Vault.cloud SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94ca4-166">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="94ca4-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_configure.png) 

7. <span data-ttu-id="94ca4-168">Per configurare l'accesso Single Sign-On sul lato **Veritas Enterprise Vault.cloud SSO**, è necessario inviare il **certificato (Base64)** e l'**URL del servizio Single Sign-On SAML** scaricati al [team di supporto di Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html).</span><span class="sxs-lookup"><span data-stu-id="94ca4-168">To configure single sign-on on **Veritas Enterprise Vault.cloud SSO** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html).</span></span>

> [!TIP]
> <span data-ttu-id="94ca4-169">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="94ca4-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94ca4-170">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="94ca4-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94ca4-171">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94ca4-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94ca4-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ca4-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="94ca4-173">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94ca4-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="94ca4-175">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="94ca4-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94ca4-176">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94ca4-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94ca4-178">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="94ca4-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94ca4-180">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94ca4-182">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94ca4-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94ca4-184">a.</span><span class="sxs-lookup"><span data-stu-id="94ca4-184">a.</span></span> <span data-ttu-id="94ca4-185">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94ca4-186">b.</span><span class="sxs-lookup"><span data-stu-id="94ca4-186">b.</span></span> <span data-ttu-id="94ca4-187">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94ca4-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94ca4-188">c.</span><span class="sxs-lookup"><span data-stu-id="94ca4-188">c.</span></span> <span data-ttu-id="94ca4-189">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="94ca4-190">d.</span><span class="sxs-lookup"><span data-stu-id="94ca4-190">d.</span></span> <span data-ttu-id="94ca4-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-191">Click **Create**.</span></span>
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a><span data-ttu-id="94ca4-192">Creazione di un utente test di Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="94ca4-192">Creating a Veritas Enterprise Vault.cloud SSO test user</span></span>

<span data-ttu-id="94ca4-193">In questa sezione viene creato un utente di nome Britta Simon in Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="94ca4-193">In this section, you create a user called Britta Simon in Enterprise Vault.cloud SSO.</span></span> <span data-ttu-id="94ca4-194">Collaborare con il [team di supporto di Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html) per aggiungere gli utenti nella piattaforma Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="94ca4-194">Work with [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html) to add the users in the Enterprise Vault.cloud SSO platform.</span></span> <span data-ttu-id="94ca4-195">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94ca4-195">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="94ca4-196">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94ca4-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="94ca4-197">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="94ca4-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veritas Enterprise Vault.cloud SSO.</span></span>

![Assegna utente][200] 

<span data-ttu-id="94ca4-199">**Per assegnare Britta Simon a Veritas Enterprise Vault.cloud SSO, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94ca4-199">**To assign Britta Simon to Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="94ca4-200">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="94ca4-202">Nell'elenco delle applicazioni selezionare **Veritas Enterprise Vault.cloud SSO**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-202">In the applications list, select **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_app.png) 

3. <span data-ttu-id="94ca4-204">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="94ca4-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="94ca4-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-206">Click **Add** button.</span></span> <span data-ttu-id="94ca4-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="94ca4-209">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="94ca4-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="94ca4-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94ca4-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94ca4-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94ca4-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="94ca4-212">Testing single sign-on</span></span>

<span data-ttu-id="94ca4-213">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="94ca4-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="94ca4-214">Quando si fa clic sul riquadro Veritas Enterprise Vault.cloud SSO nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Veritas Enterprise Vault.cloud SSO.</span><span class="sxs-lookup"><span data-stu-id="94ca4-214">When you click the Veritas Enterprise Vault.cloud SSO tile in the Access Panel, you should get automatically signed-on to your Veritas Enterprise Vault.cloud SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94ca4-215">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="94ca4-215">Additional resources</span></span>

* [<span data-ttu-id="94ca4-216">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94ca4-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94ca4-217">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94ca4-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_203.png


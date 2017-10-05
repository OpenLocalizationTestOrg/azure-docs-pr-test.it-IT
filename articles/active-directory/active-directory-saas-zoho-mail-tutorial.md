---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zoho | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Zoho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="e66b4-103">Esercitazione: Integrazione di Azure Active Directory con Zoho</span><span class="sxs-lookup"><span data-stu-id="e66b4-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="e66b4-104">Questa esercitazione descrive come integrare Zoho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e66b4-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e66b4-105">L'integrazione di Zoho con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e66b4-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e66b4-106">È possibile controllare in Azure AD chi può accedere a Zoho.</span><span class="sxs-lookup"><span data-stu-id="e66b4-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="e66b4-107">È possibile abilitare gli utenti per l'accesso automatico a Zoho (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="e66b4-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e66b4-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e66b4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e66b4-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e66b4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e66b4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e66b4-110">Prerequisites</span></span>

<span data-ttu-id="e66b4-111">Per configurare l'integrazione di Azure AD con Zoho, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e66b4-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="e66b4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e66b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e66b4-113">Sottoscrizione di Zoho abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e66b4-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e66b4-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e66b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e66b4-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e66b4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e66b4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e66b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e66b4-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e66b4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e66b4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e66b4-118">Scenario description</span></span>
<span data-ttu-id="e66b4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e66b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e66b4-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e66b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e66b4-121">Aggiunta di Zoho dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e66b4-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="e66b4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e66b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="e66b4-123">Aggiunta di Zoho dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e66b4-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="e66b4-124">Per configurare l'integrazione di Zoho in Azure AD, è necessario aggiungere Zoho dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e66b4-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e66b4-125">**Per aggiungere Zoho dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e66b4-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e66b4-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e66b4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="e66b4-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e66b4-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="e66b4-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="e66b4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="e66b4-133">Nella casella di ricerca digitare **Zoho**, selezionare **Zoho** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e66b4-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho nell'elenco risultati](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e66b4-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e66b4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e66b4-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zoho usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e66b4-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e66b4-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Zoho corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e66b4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="e66b4-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Zoho.</span><span class="sxs-lookup"><span data-stu-id="e66b4-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="e66b4-139">Per stabilire la relazione di collegamento, in Zoho assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="e66b4-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e66b4-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Zoho, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="e66b4-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e66b4-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e66b4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e66b4-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e66b4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e66b4-143">**[Creare un utente di test di Zoho](#create-a-zoho-test-user)**: per avere una controparte di Britta Simon in Zoho collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e66b4-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e66b4-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e66b4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e66b4-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="e66b4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e66b4-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e66b4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e66b4-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Zoho.</span><span class="sxs-lookup"><span data-stu-id="e66b4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="e66b4-148">**Per configurare l'accesso Single Sign-On di Azure AD con Zoho, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e66b4-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="e66b4-149">Nella pagina di integrazione dell'applicazione **Zoho** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e66b4-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e66b4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="e66b4-153">Nella sezione **URL e dominio Zoho** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e66b4-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="e66b4-155">a.</span><span class="sxs-lookup"><span data-stu-id="e66b4-155">a.</span></span> <span data-ttu-id="e66b4-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="e66b4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e66b4-157">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="e66b4-157">This value is not real.</span></span> <span data-ttu-id="e66b4-158">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="e66b4-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e66b4-159">Per ottenere questo valore, contattare il [team di supporto clienti di Zoho](https://www.zoho.com/mail/contact.html).</span><span class="sxs-lookup"><span data-stu-id="e66b4-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="e66b4-160">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="e66b4-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="e66b4-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e66b4-162">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e66b4-164">Nella sezione **Configurazione di Zoho** fare clic su **Configura Zoho** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e66b4-165">Copiare **URL di disconnessione, URL di modifica password e URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="e66b4-167">In un'altra finestra del Web browser accedere al sito aziendale di Zoho Mail come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e66b4-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="e66b4-168">Passare a **Control panel**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="e66b4-169">![Pannello di controllo](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Pannello di controllo")</span><span class="sxs-lookup"><span data-stu-id="e66b4-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="e66b4-170">Fare clic sulla scheda **SAML Authentication** .</span><span class="sxs-lookup"><span data-stu-id="e66b4-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="e66b4-171">![Autenticazione SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="e66b4-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="e66b4-172">Nella sezione **SAML Authentication Details** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e66b4-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e66b4-173">![Dettagli dell'autenticazione SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Dettagli dell'autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="e66b4-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="e66b4-174">a.</span><span class="sxs-lookup"><span data-stu-id="e66b4-174">a.</span></span> <span data-ttu-id="e66b4-175">Nella casella di testo **Login URL** (URL di accesso) incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e66b4-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e66b4-176">b.</span><span class="sxs-lookup"><span data-stu-id="e66b4-176">b.</span></span> <span data-ttu-id="e66b4-177">Nella casella di testo **Logout URL** (URL di disconnessione) incollare l'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e66b4-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e66b4-178">c.</span><span class="sxs-lookup"><span data-stu-id="e66b4-178">c.</span></span> <span data-ttu-id="e66b4-179">Nella casella di testo **Change Password URL** (URL di modifica password) incollare l'**URL di modifica password** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e66b4-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="e66b4-180">d.</span><span class="sxs-lookup"><span data-stu-id="e66b4-180">d.</span></span> <span data-ttu-id="e66b4-181">Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **PublicKey** (Chiave pubblica).</span><span class="sxs-lookup"><span data-stu-id="e66b4-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="e66b4-182">e.</span><span class="sxs-lookup"><span data-stu-id="e66b4-182">e.</span></span> <span data-ttu-id="e66b4-183">In **Algorithm** (Algoritmo) selezionare **RSA**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="e66b4-184">f.</span><span class="sxs-lookup"><span data-stu-id="e66b4-184">f.</span></span> <span data-ttu-id="e66b4-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="e66b4-186">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="e66b4-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e66b4-187">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="e66b4-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e66b4-188">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e66b4-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e66b4-189">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e66b4-189">Create an Azure AD test user</span></span>

<span data-ttu-id="e66b4-190">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e66b4-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="e66b4-192">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e66b4-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e66b4-193">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="e66b4-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e66b4-195">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e66b4-197">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e66b4-199">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e66b4-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e66b4-201">a.</span><span class="sxs-lookup"><span data-stu-id="e66b4-201">a.</span></span> <span data-ttu-id="e66b4-202">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e66b4-203">b.</span><span class="sxs-lookup"><span data-stu-id="e66b4-203">b.</span></span> <span data-ttu-id="e66b4-204">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e66b4-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e66b4-205">c.</span><span class="sxs-lookup"><span data-stu-id="e66b4-205">c.</span></span> <span data-ttu-id="e66b4-206">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e66b4-207">d.</span><span class="sxs-lookup"><span data-stu-id="e66b4-207">d.</span></span> <span data-ttu-id="e66b4-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="e66b4-209">Creare un utente di test di Zoho</span><span class="sxs-lookup"><span data-stu-id="e66b4-209">Create a Zoho test user</span></span>

<span data-ttu-id="e66b4-210">Per consentire agli utenti di Azure AD di accedere a Zoho Mail, è necessario eseguirne il provisioning in Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="e66b4-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="e66b4-211">Nel caso di Zoho Mail, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="e66b4-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="e66b4-212">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Zoho Mail per eseguire il provisioning degli account utente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e66b4-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="e66b4-213">Per eseguire il provisioning di un account utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e66b4-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="e66b4-214">Accedere al sito aziendale di **Zoho Mail** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e66b4-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="e66b4-215">Passare a **Control Panel \> Mail & Docs**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="e66b4-216">Passare a **User Details \> Add User** (Dettagli utente > Aggiungi utente).</span><span class="sxs-lookup"><span data-stu-id="e66b4-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="e66b4-217">![Aggiungere un utente](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="e66b4-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="e66b4-218">Nella finestra di dialogo **Add users** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e66b4-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="e66b4-219">![Aggiungere un utente](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="e66b4-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="e66b4-220">a.</span><span class="sxs-lookup"><span data-stu-id="e66b4-220">a.</span></span> <span data-ttu-id="e66b4-221">Nella casella di testo **First Name** (Nome) digitare il nome dell'utente, ad esempio **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="e66b4-222">b.</span><span class="sxs-lookup"><span data-stu-id="e66b4-222">b.</span></span> <span data-ttu-id="e66b4-223">Nella casella di testo **Last name** (Cognome) digitare il cognome dell'utente, ad esempio **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="e66b4-224">c.</span><span class="sxs-lookup"><span data-stu-id="e66b4-224">c.</span></span> <span data-ttu-id="e66b4-225">Nella casella di testo **Email ID** (ID posta elettronica) digitare l'ID di posta elettronica dell'utente, ad esempio **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e66b4-226">d.</span><span class="sxs-lookup"><span data-stu-id="e66b4-226">d.</span></span> <span data-ttu-id="e66b4-227">Nella casella di testo **Password** digitare la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e66b4-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="e66b4-228">e.</span><span class="sxs-lookup"><span data-stu-id="e66b4-228">e.</span></span> <span data-ttu-id="e66b4-229">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="e66b4-230">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="e66b4-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e66b4-231">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e66b4-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="e66b4-232">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Zoho.</span><span class="sxs-lookup"><span data-stu-id="e66b4-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="e66b4-234">**Per assegnare Britta Simon a Zoho, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e66b4-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="e66b4-235">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e66b4-237">Nell'elenco delle applicazioni selezionare **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-237">In the applications list, select **Zoho**.</span></span>

    ![Collegamento di Zoho nell'elenco delle applicazioni](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="e66b4-239">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e66b4-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="e66b4-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-241">Click **Add** button.</span></span> <span data-ttu-id="e66b4-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="e66b4-244">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="e66b4-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e66b4-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e66b4-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e66b4-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e66b4-247">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e66b4-247">Test single sign-on</span></span>

<span data-ttu-id="e66b4-248">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e66b4-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e66b4-249">Quando si fa clic sul riquadro Zoho nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Zoho.</span><span class="sxs-lookup"><span data-stu-id="e66b4-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="e66b4-250">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e66b4-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e66b4-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e66b4-251">Additional resources</span></span>

* [<span data-ttu-id="e66b4-252">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e66b4-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e66b4-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e66b4-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png


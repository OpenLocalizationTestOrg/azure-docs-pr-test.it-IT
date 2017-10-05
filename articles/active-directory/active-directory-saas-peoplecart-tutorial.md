---
title: 'Esercitazione: Integrazione di Azure Active Directory con Peoplecart | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Peoplecart.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b83a1621263cac0b23bbd35a49fda213d2e4271a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="be562-103">Esercitazione: integrazione di Azure Active Directory con Peoplecart</span><span class="sxs-lookup"><span data-stu-id="be562-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="be562-104">Questa esercitazione descrive come integrare Peoplecart con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be562-104">In this tutorial, you learn how to integrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be562-105">L'integrazione di Peoplecart con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="be562-105">Integrating Peoplecart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="be562-106">È possibile controllare in Azure AD chi può accedere a Peoplecart</span><span class="sxs-lookup"><span data-stu-id="be562-106">You can control in Azure AD who has access to Peoplecart</span></span>
- <span data-ttu-id="be562-107">È possibile abilitare gli utenti per l'accesso automatico a Peoplecart (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="be562-107">You can enable your users to automatically get signed-on to Peoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be562-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be562-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="be562-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be562-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be562-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="be562-110">Prerequisites</span></span>

<span data-ttu-id="be562-111">Per configurare l'integrazione di Azure AD con Peoplecart, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="be562-111">To configure Azure AD integration with Peoplecart, you need the following items:</span></span>

- <span data-ttu-id="be562-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be562-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be562-113">Sottoscrizione di Peoplecart abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="be562-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be562-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="be562-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be562-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="be562-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be562-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="be562-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be562-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be562-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be562-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="be562-118">Scenario description</span></span>
<span data-ttu-id="be562-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="be562-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be562-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="be562-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be562-121">Aggiunta di Peoplecart dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="be562-121">Adding Peoplecart from the gallery</span></span>
2. <span data-ttu-id="be562-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be562-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-the-gallery"></a><span data-ttu-id="be562-123">Aggiunta di Peoplecart dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="be562-123">Adding Peoplecart from the gallery</span></span>
<span data-ttu-id="be562-124">Per configurare l'integrazione di Peoplecart in Azure AD, è necessario aggiungere Peoplecart dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="be562-124">To configure the integration of Peoplecart into Azure AD, you need to add Peoplecart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="be562-125">**Per aggiungere Peoplecart dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="be562-125">**To add Peoplecart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="be562-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="be562-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="be562-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="be562-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="be562-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="be562-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="be562-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="be562-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="be562-133">Nella casella di ricerca digitare **Peoplecart**, selezionare **Peoplecart** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="be562-133">In the search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button to add the application.</span></span>

    ![Peoplecart nell'elenco risultati](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="be562-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be562-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="be562-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Peoplecart in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="be562-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="be562-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Peoplecart che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be562-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Peoplecart is to a user in Azure AD.</span></span> <span data-ttu-id="be562-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="be562-138">In other words, a link relationship between an Azure AD user and the related user in Peoplecart needs to be established.</span></span>

<span data-ttu-id="be562-139">Per stabilire la relazione di collegamento, in Peoplecart assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="be562-139">In Peoplecart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="be562-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Peoplecart, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="be562-140">To configure and test Azure AD single sign-on with Peoplecart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="be562-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="be562-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="be562-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be562-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be562-143">**[Creare un utente test di Peoplecart](#create-a-peoplecart-test-user)**: per avere una controparte di Britta Simon in Peoplecart collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be562-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - to have a counterpart of Britta Simon in Peoplecart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="be562-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be562-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be562-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="be562-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="be562-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be562-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="be562-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="be562-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="be562-148">**Per configurare Single Sign-On di Azure AD con Peoplecart, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="be562-148">**To configure Azure AD single sign-on with Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="be562-149">Nella pagina di integrazione dell'applicazione **Peoplecart** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="be562-149">In the Azure portal, on the **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="be562-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="be562-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="be562-153">Nella sezione **URL e dominio Peoplecart** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="be562-153">On the **Peoplecart Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="be562-155">a.</span><span class="sxs-lookup"><span data-stu-id="be562-155">a.</span></span> <span data-ttu-id="be562-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenantname>.peoplecart.com/SignIn.aspx`.</span><span class="sxs-lookup"><span data-stu-id="be562-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="be562-157">b.</span><span class="sxs-lookup"><span data-stu-id="be562-157">b.</span></span> <span data-ttu-id="be562-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="be562-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="be562-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="be562-159">These values are not real.</span></span> <span data-ttu-id="be562-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="be562-160">Update these values with the actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="be562-161">Per ottenere questi valori, contattare il [team di supporto clienti di Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="be562-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) to get these values.</span></span> 
 
4. <span data-ttu-id="be562-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="be562-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="be562-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="be562-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="be562-166">Nella sezione **Configurazione di Peoplecart** fare clic su **Configura Peoplecart** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="be562-166">On the **Peoplecart Configuration** section, click **Configure Peoplecart** to open **Configure sign-on** window.</span></span> <span data-ttu-id="be562-167">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="be562-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="be562-169">Per configurare l'accesso Single Sign-On sul lato **Peoplecart**, è necessario inviare il file **XML metadati** scaricato e il valore dell'**URL del servizio Single Sign-On SAML** al [team di supporto di Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="be562-169">To configure single sign-on on **Peoplecart** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="be562-170">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="be562-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="be562-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="be562-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="be562-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="be562-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="be562-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be562-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="be562-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be562-174">Create an Azure AD test user</span></span>
<span data-ttu-id="be562-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be562-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="be562-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="be562-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="be562-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="be562-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be562-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="be562-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be562-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="be562-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be562-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="be562-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be562-186">a.</span><span class="sxs-lookup"><span data-stu-id="be562-186">a.</span></span> <span data-ttu-id="be562-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be562-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be562-188">b.</span><span class="sxs-lookup"><span data-stu-id="be562-188">b.</span></span> <span data-ttu-id="be562-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="be562-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be562-190">c.</span><span class="sxs-lookup"><span data-stu-id="be562-190">c.</span></span> <span data-ttu-id="be562-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="be562-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="be562-192">d.</span><span class="sxs-lookup"><span data-stu-id="be562-192">d.</span></span> <span data-ttu-id="be562-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="be562-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="be562-194">Creare un utente test di Peoplecart</span><span class="sxs-lookup"><span data-stu-id="be562-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="be562-195">In questa sezione viene creato un utente chiamato Britta Simon in Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="be562-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="be562-196">Collaborare con il [team di supporto di Peoplecart](https://peoplecart.com/ContactUs.aspx) per aggiungere gli utenti alla piattaforma Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="be562-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) to add the users in the Peoplecart platform.</span></span> <span data-ttu-id="be562-197">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="be562-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="be562-198">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be562-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="be562-199">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="be562-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Peoplecart.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="be562-201">**Per assegnare Britta Simon a Peoplecart, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="be562-201">**To assign Britta Simon to Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="be562-202">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="be562-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="be562-204">Nell'elenco delle applicazioni, selezionare **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="be562-204">In the applications list, select **Peoplecart**.</span></span>

    ![Collegamento Peoplecart nell'elenco Applicazioni](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="be562-206">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="be562-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202] 

4. <span data-ttu-id="be562-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="be562-208">Click **Add** button.</span></span> <span data-ttu-id="be562-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="be562-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="be562-211">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="be562-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="be562-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="be562-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be562-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="be562-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="be562-214">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="be562-214">Test single sign-on</span></span>

<span data-ttu-id="be562-215">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="be562-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="be562-216">Quando si fa clic sul riquadro Peoplecart nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="be562-216">When you click the Peoplecart tile in the Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="be562-217">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be562-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be562-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="be562-218">Additional resources</span></span>

* [<span data-ttu-id="be562-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be562-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be562-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be562-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png


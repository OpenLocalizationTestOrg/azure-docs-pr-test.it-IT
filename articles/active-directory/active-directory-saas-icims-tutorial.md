---
title: 'Esercitazione: Integrazione di Azure Active Directory con ICIMS | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ICIMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 26a6b41a0e59924d007855ca548f22ed00bd7e23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="fcc6c-103">Esercitazione: Integrazione di Azure Active Directory con ICIMS</span><span class="sxs-lookup"><span data-stu-id="fcc6c-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="fcc6c-104">Questa esercitazione descrive come integrare ICIMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fcc6c-104">In this tutorial, you learn how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fcc6c-105">L'integrazione di ICIMS con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fcc6c-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fcc6c-106">È possibile controllare in Azure AD chi può accedere a ICIMS</span><span class="sxs-lookup"><span data-stu-id="fcc6c-106">You can control in Azure AD who has access to ICIMS</span></span>
- <span data-ttu-id="fcc6c-107">È possibile abilitare gli utenti per l'accesso automatico a ICIMS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcc6c-107">You can enable your users to automatically get signed-on to ICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fcc6c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fcc6c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fcc6c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcc6c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fcc6c-110">Prerequisites</span></span>

<span data-ttu-id="fcc6c-111">Per configurare l'integrazione di Azure AD con ICIMS, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fcc6c-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

- <span data-ttu-id="fcc6c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fcc6c-113">Sottoscrizione di ICIMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fcc6c-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fcc6c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fcc6c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fcc6c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fcc6c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fcc6c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fcc6c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fcc6c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fcc6c-118">Scenario description</span></span>
<span data-ttu-id="fcc6c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fcc6c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fcc6c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fcc6c-121">Aggiunta di ICIMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fcc6c-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="fcc6c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcc6c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-the-gallery"></a><span data-ttu-id="fcc6c-123">Aggiunta di ICIMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fcc6c-123">Adding ICIMS from the gallery</span></span>
<span data-ttu-id="fcc6c-124">Per configurare l'integrazione di ICIMS in Azure AD, è necessario aggiungere ICIMS dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fcc6c-125">**Per aggiungere ICIMS dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fcc6c-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc6c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="fcc6c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fcc6c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="fcc6c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="fcc6c-133">Nella casella di ricerca digitare **ICIMS**, selezionare **ICIMS** dal pannello dei risultati quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-133">In the search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button to add the application.</span></span>

    ![ICIMS nell'elenco risultati](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fcc6c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcc6c-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="fcc6c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ICIMS in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fcc6c-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fcc6c-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di ICIMS che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ICIMS is to a user in Azure AD.</span></span> <span data-ttu-id="fcc6c-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ICIMS.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-138">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>

<span data-ttu-id="fcc6c-139">Per stabilire la relazione di collegamento, in ICIMS assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="fcc6c-139">In ICIMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fcc6c-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con ICIMS, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fcc6c-140">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fcc6c-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fcc6c-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fcc6c-143">**[Creare un utente test di ICIMS](#create-an-icims-test-user)**: per avere una controparte di Britta Simon in ICIMS collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fcc6c-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fcc6c-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fcc6c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcc6c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fcc6c-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ICIMS.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="fcc6c-148">**Per configurare Single Sign-On di Azure AD con ICIMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fcc6c-148">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc6c-149">Nella pagina di integrazione dell'applicazione **ICIMS** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-149">In the Azure portal, on the **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fcc6c-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="fcc6c-153">Nella sezione **URL e dominio ICIMS** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fcc6c-153">On the **ICIMS Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni sul Single Sign-On di URL e dominio di ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="fcc6c-155">a.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-155">a.</span></span> <span data-ttu-id="fcc6c-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant name>.icims.com`.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="fcc6c-157">b.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-157">b.</span></span> <span data-ttu-id="fcc6c-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="fcc6c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fcc6c-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="fcc6c-159">These values are not real.</span></span> <span data-ttu-id="fcc6c-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fcc6c-161">Per ottenere questi valori, contattare il [team di supporto clienti di ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="fcc6c-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="fcc6c-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="fcc6c-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fcc6c-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fcc6c-166">Nella sezione **Configurazione di ICIMS** fare clic su **Configura ICIMS** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-166">On the **ICIMS Configuration** section, click **Configure ICIMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fcc6c-167">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="fcc6c-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="fcc6c-169">Per configurare l'accesso Single Sign-On sul lato **ICIMS**, è necessario inviare il file di **XML metadati** scaricato, **l'URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="fcc6c-169">To configure single sign-on on **ICIMS** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="fcc6c-170">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fcc6c-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fcc6c-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fcc6c-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fcc6c-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fcc6c-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcc6c-174">Create an Azure AD test user</span></span>
<span data-ttu-id="fcc6c-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="fcc6c-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fcc6c-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc6c-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fcc6c-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fcc6c-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fcc6c-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fcc6c-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fcc6c-186">a.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-186">a.</span></span> <span data-ttu-id="fcc6c-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fcc6c-188">b.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-188">b.</span></span> <span data-ttu-id="fcc6c-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fcc6c-190">c.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-190">c.</span></span> <span data-ttu-id="fcc6c-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fcc6c-192">d.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-192">d.</span></span> <span data-ttu-id="fcc6c-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="fcc6c-194">Creare un utente test di ICIMS</span><span class="sxs-lookup"><span data-stu-id="fcc6c-194">Create an ICIMS test user</span></span>

<span data-ttu-id="fcc6c-195">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in ICIMS.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-195">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="fcc6c-196">Collaborare con il [team di supporto di ICIMS](https://www.icims.com/contact-us) per aggiungere gli utenti nell'account ICIMS.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-196">Work with [ICIMS support team](https://www.icims.com/contact-us) to add the users in the ICIMS account.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fcc6c-197">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcc6c-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="fcc6c-198">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a ICIMS.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ICIMS.</span></span>

![Assegnare il ruolo utente][200]

<span data-ttu-id="fcc6c-200">**Per assegnare Britta Simon a ICIMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fcc6c-200">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="fcc6c-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fcc6c-203">Nell'elenco delle applicazioni selezionare **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-203">In the applications list, select **ICIMS**.</span></span>

    ![Collegamento ICIMS nell'elenco Applicazioni](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="fcc6c-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202] 

4. <span data-ttu-id="fcc6c-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-207">Click **Add** button.</span></span> <span data-ttu-id="fcc6c-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="fcc6c-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fcc6c-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fcc6c-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fcc6c-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fcc6c-213">Test single sign-on</span></span>

<span data-ttu-id="fcc6c-214">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="fcc6c-215">Quando si fa clic sul riquadro ICIMS nel pannello di accesso, si accederà automaticamente all'applicazione ICIMS.</span><span class="sxs-lookup"><span data-stu-id="fcc6c-215">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcc6c-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fcc6c-216">Additional resources</span></span>

* [<span data-ttu-id="fcc6c-217">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcc6c-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fcc6c-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcc6c-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con RFPIO | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="a4c39-103">Esercitazione: Integrazione di Azure Active Directory con RFPIO</span><span class="sxs-lookup"><span data-stu-id="a4c39-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="a4c39-104">Questa esercitazione descrive come integrare RFPIO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4c39-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4c39-105">L'integrazione di RFPIO con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4c39-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a4c39-106">In Azure AD è possibile controllare chi può accedere a RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a4c39-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="a4c39-107">È possibile abilitare gli utenti per l'accesso automatico a RFPIO (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c39-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a4c39-108">Gli account possono essere gestiti da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c39-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="a4c39-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4c39-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4c39-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a4c39-110">Prerequisites</span></span>

<span data-ttu-id="a4c39-111">Per configurare l'integrazione di Azure AD con RFPIO, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4c39-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="a4c39-112">Una sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c39-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="a4c39-113">Sottoscrizione RFPIO abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a4c39-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c39-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4c39-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="a4c39-115">A questo scopo, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="a4c39-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a4c39-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a4c39-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="a4c39-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4c39-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4c39-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a4c39-118">Scenario description</span></span>
<span data-ttu-id="a4c39-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a4c39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4c39-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4c39-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4c39-121">Aggiunta di RFPIO dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="a4c39-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="a4c39-122">Configurazione e test dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c39-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="a4c39-123">Aggiungere RFPIO dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a4c39-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="a4c39-124">Per configurare l'integrazione di RFPIO in Azure AD, è necessario aggiungere RFPIO dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a4c39-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="a4c39-125">Per aggiungere RFPIO dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a4c39-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="a4c39-126">Nel **[portale di Azure](https://portal.azure.com)** selezionare l'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a4c39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4c39-128">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a4c39-130">Per aggiungere una nuova applicazione selezionare il pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a4c39-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a4c39-132">Nella casella di ricerca digitare **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-132">In the search box, type **RFPIO**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="a4c39-134">Nel pannello dei risultati selezionare **RFPIO** e quindi selezionare il pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4c39-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a4c39-136">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4c39-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a4c39-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RFPIO in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a4c39-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4c39-138">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è la relazione esistente fra un utente di Azure AD e l'utente corrispondente in RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a4c39-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="a4c39-139">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a4c39-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="a4c39-140">Per stabilire la relazione di collegamento, in RFPIO assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a4c39-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a4c39-141">Per configurare e testare l'accesso Single Sign-On di Azure AD con RFPIO, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4c39-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a4c39-142">**[Configurare l'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a4c39-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a4c39-143">**[Creare un utente di test di Azure AD](#creating-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4c39-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4c39-144">**[Creare un utente di test di RFPIO](#creating-a-rfpio-test-user)**: per avere una controparte di Britta Simon in RFPIO collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c39-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4c39-145">**[Assegnare l'utente test di Azure AD](#assigning-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c39-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4c39-146">**[Testare l'accesso Single Sign-On](#testing-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a4c39-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a4c39-147">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4c39-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a4c39-148">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a4c39-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="a4c39-149">**Per configurare l'accesso Single Sign-On di Azure AD con RFPIO, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4c39-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="a4c39-150">Nella pagina di integrazione dell'applicazione **RFPIO** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a4c39-152">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a4c39-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="a4c39-154">Nella sezione **URL e dominio RFPIO**, se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="a4c39-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="a4c39-156">a.</span><span class="sxs-lookup"><span data-stu-id="a4c39-156">a.</span></span> <span data-ttu-id="a4c39-157">Nella casella di testo **Identificatore** digitare l'URL: `https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="a4c39-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="a4c39-159">b.</span><span class="sxs-lookup"><span data-stu-id="a4c39-159">b.</span></span> <span data-ttu-id="a4c39-160">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="a4c39-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a4c39-161">c.</span><span class="sxs-lookup"><span data-stu-id="a4c39-161">c.</span></span> <span data-ttu-id="a4c39-162">Nella casella di testo **Stato dell'inoltro** immettere un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="a4c39-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="a4c39-163">Per ottenere tale valore, contattare il [team di supporto di RFPIO](https://www.rfpio.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="a4c39-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="a4c39-164">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="a4c39-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a4c39-165">se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="a4c39-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="a4c39-167">Nella casella di testo **URL di accesso** digitare l'URL: `https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="a4c39-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="a4c39-168">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="a4c39-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="a4c39-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a4c39-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a4c39-172">In un'altra finestra del Web browser accedere al sito Web **RFPIO** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a4c39-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="a4c39-173">Fare clic sull'elenco a discesa a sinistra nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a4c39-173">Click on the bottom left corner dropdown.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="a4c39-175">Fare clic su di **Impostazioni organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-175">Click on the **Organization Settings**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="a4c39-177">Fare clic sulla sezione relativa a **FUNZIONALITÀ E INTEGRAZIONE**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="a4c39-179">In **SAML Configurazione SSO** fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="a4c39-181">In questa sezione eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="a4c39-181">In this Section perform following actions:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="a4c39-183">a.</span><span class="sxs-lookup"><span data-stu-id="a4c39-183">a.</span></span> <span data-ttu-id="a4c39-184">Copiare il contenuto del **file XML di metadati scaricato** e incollarlo nella casella della **configurazione identità**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="a4c39-185">Per copiare il contenuto del file di **metadata XML** scaricato usare **Notepad++** o un **editor XML** appropriato.</span><span class="sxs-lookup"><span data-stu-id="a4c39-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="a4c39-186">b.</span><span class="sxs-lookup"><span data-stu-id="a4c39-186">b.</span></span> <span data-ttu-id="a4c39-187">Fare clic su **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-187">Click **Validate**.</span></span>

    <span data-ttu-id="a4c39-188">c.</span><span class="sxs-lookup"><span data-stu-id="a4c39-188">c.</span></span> <span data-ttu-id="a4c39-189">Dopo aver fatto clic su **Convalida**, impostare **SAML (Abilitato)** su attivato.</span><span class="sxs-lookup"><span data-stu-id="a4c39-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="a4c39-190">d.</span><span class="sxs-lookup"><span data-stu-id="a4c39-190">d.</span></span> <span data-ttu-id="a4c39-191">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="a4c39-192">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a4c39-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a4c39-193">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a4c39-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a4c39-194">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4c39-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a4c39-195">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4c39-195">Create an Azure AD test user</span></span>
<span data-ttu-id="a4c39-196">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c39-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a4c39-198">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a4c39-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a4c39-199">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a4c39-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4c39-201">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a4c39-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4c39-203">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4c39-205">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4c39-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4c39-207">a.</span><span class="sxs-lookup"><span data-stu-id="a4c39-207">a.</span></span> <span data-ttu-id="a4c39-208">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4c39-209">b.</span><span class="sxs-lookup"><span data-stu-id="a4c39-209">b.</span></span> <span data-ttu-id="a4c39-210">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4c39-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4c39-211">c.</span><span class="sxs-lookup"><span data-stu-id="a4c39-211">c.</span></span> <span data-ttu-id="a4c39-212">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a4c39-213">d.</span><span class="sxs-lookup"><span data-stu-id="a4c39-213">d.</span></span> <span data-ttu-id="a4c39-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="a4c39-215">Creare un utente di test di RFPIO</span><span class="sxs-lookup"><span data-stu-id="a4c39-215">Create a RFPIO test user</span></span>

<span data-ttu-id="a4c39-216">Per consentire agli utenti di Azure AD di accedere a RFPIO, è necessario eseguirne il provisioning in RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a4c39-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="a4c39-217">Nel caso di RFPIO, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="a4c39-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="a4c39-218">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4c39-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a4c39-219">Accedere al sito aziendale di RFPIO come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a4c39-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="a4c39-220">Fare clic sull'elenco a discesa a sinistra nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a4c39-220">Click on the bottom left corner dropdown.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="a4c39-222">Fare clic su di **Impostazioni organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-222">Click on the **Organization Settings**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="a4c39-224">Fare clic su **MEMBRI DEL TEAM**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-224">Click **TEAM MEMBERS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="a4c39-226">Fare clic su **AGGIUNGI MEMBRI**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-226">Click on **ADD MEMBERS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="a4c39-228">Nella sezione **Aggiungere nuovi membri**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-228">In the **Add New Members** section.</span></span> <span data-ttu-id="a4c39-229">eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="a4c39-229">Perform following actions:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="a4c39-231">a.</span><span class="sxs-lookup"><span data-stu-id="a4c39-231">a.</span></span> <span data-ttu-id="a4c39-232">Immettere l'**indirizzo di posta elettronica** nella casella che richiede **un indirizzo di posta elettronica per riga**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="a4c39-233">b.</span><span class="sxs-lookup"><span data-stu-id="a4c39-233">b.</span></span> <span data-ttu-id="a4c39-234">Selezionare il **ruolo** in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="a4c39-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="a4c39-235">c.</span><span class="sxs-lookup"><span data-stu-id="a4c39-235">c.</span></span> <span data-ttu-id="a4c39-236">Fare clic su **AGGIUNGI MEMBRI**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="a4c39-237">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="a4c39-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a4c39-238">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4c39-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="a4c39-239">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a4c39-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a4c39-241">**Per assegnare Britta Simon a RFPIO seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4c39-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="a4c39-242">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a4c39-244">Nell'elenco delle applicazioni selezionare **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-244">In the applications list, select **RFPIO**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="a4c39-246">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a4c39-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a4c39-248">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-248">Click **Add** button.</span></span> <span data-ttu-id="a4c39-249">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a4c39-251">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a4c39-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a4c39-252">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4c39-253">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a4c39-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a4c39-254">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a4c39-254">Test single sign-on</span></span>

<span data-ttu-id="a4c39-255">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a4c39-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="a4c39-256">Quando si fa clic sul riquadro RFPIO nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione RFPIO.</span><span class="sxs-lookup"><span data-stu-id="a4c39-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="a4c39-257">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4c39-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4c39-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a4c39-258">Additional resources</span></span>

* [<span data-ttu-id="a4c39-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4c39-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4c39-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4c39-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png


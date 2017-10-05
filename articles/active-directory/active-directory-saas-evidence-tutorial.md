---
title: 'Esercitazione: Integrazione di Azure Active Directory con Evidence.com | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Evidence.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="86e6c-103">Esercitazione: Integrazione di Azure Active Directory con Evidence.com</span><span class="sxs-lookup"><span data-stu-id="86e6c-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="86e6c-104">Questa esercitazione descrive come integrare Evidence.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86e6c-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86e6c-105">L'integrazione di Evidence.com con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="86e6c-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86e6c-106">È possibile controllare in Azure AD chi può accedere a Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="86e6c-107">È possibile abilitare gli utenti per l'accesso automatico a Evidence.com (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86e6c-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="86e6c-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="86e6c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="86e6c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86e6c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86e6c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="86e6c-110">Prerequisites</span></span>

<span data-ttu-id="86e6c-111">Per configurare l'integrazione di Azure AD con Evidence.com, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="86e6c-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="86e6c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86e6c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86e6c-113">Sottoscrizione di Evidence.com abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="86e6c-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86e6c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="86e6c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86e6c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="86e6c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86e6c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="86e6c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86e6c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86e6c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86e6c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="86e6c-118">Scenario description</span></span>
<span data-ttu-id="86e6c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="86e6c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86e6c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="86e6c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86e6c-121">Aggiunta di Evidence.com dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="86e6c-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="86e6c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="86e6c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="86e6c-123">Aggiunta di Evidence.com dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="86e6c-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="86e6c-124">Per configurare l'integrazione di Evidence.com in Azure AD, è necessario aggiungere Evidence.com dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="86e6c-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86e6c-125">**Per aggiungere Evidence.com dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="86e6c-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86e6c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="86e6c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="86e6c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86e6c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="86e6c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="86e6c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="86e6c-133">Nella casella di ricerca digitare **Evidence.com**, selezionare **Evidence.com** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="86e6c-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![Evidence.com nell'elenco risultati](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="86e6c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="86e6c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="86e6c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Evidence.com con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="86e6c-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86e6c-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Evidence.com che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86e6c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="86e6c-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="86e6c-139">Per stabilire la relazione di collegamento, in Evidence.com assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="86e6c-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="86e6c-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Evidence.com, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="86e6c-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86e6c-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="86e6c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86e6c-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86e6c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86e6c-143">**[Creare un utente di test di Evidence.com](#create-a-evidencecom-test-user)**: per avere una controparte di Britta Simon in Evidence.com collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86e6c-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86e6c-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86e6c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86e6c-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="86e6c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="86e6c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="86e6c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="86e6c-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="86e6c-148">**Per configurare l'accesso Single Sign-On di Azure AD con Evidence.com, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="86e6c-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="86e6c-149">Nella pagina di integrazione dell'applicazione **Evidence.com** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="86e6c-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="86e6c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="86e6c-153">Nella sezione **URL e dominio Evidence.com** eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="86e6c-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="86e6c-155">a.</span><span class="sxs-lookup"><span data-stu-id="86e6c-155">a.</span></span> <span data-ttu-id="86e6c-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<yourtenant>.evidence.com`.</span><span class="sxs-lookup"><span data-stu-id="86e6c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="86e6c-157">b.</span><span class="sxs-lookup"><span data-stu-id="86e6c-157">b.</span></span> <span data-ttu-id="86e6c-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="86e6c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86e6c-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="86e6c-159">These values are not real.</span></span> <span data-ttu-id="86e6c-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="86e6c-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="86e6c-161">Per ottenere questi valori, contattare il [team di supporto clienti di Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE).</span><span class="sxs-lookup"><span data-stu-id="86e6c-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="86e6c-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="86e6c-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="86e6c-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="86e6c-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86e6c-166">Nella sezione **Configurazione di Evidence.com** fare clic su **Configura Evidence.com** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="86e6c-167">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="86e6c-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="86e6c-169">In una finestra del separata del Web browser accedere al tenant Evidence.com come amministratore e passare alla scheda **Admin** .</span><span class="sxs-lookup"><span data-stu-id="86e6c-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="86e6c-170">Fare clic su **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="86e6c-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="86e6c-171">Selezionare **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="86e6c-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="86e6c-172">Copiare i valori di **ID entità SAML**, di **URL servizio Single Sign-On** e di **URL di disconnessione** visualizzati nel portale di Azure e nei campi corrispondenti in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="86e6c-173">Aprire il file Certificate (Base64) scaricato nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella **Certificato di protezione**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="86e6c-174">Salvare la configurazione in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="86e6c-175">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="86e6c-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86e6c-176">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="86e6c-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86e6c-177">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86e6c-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="86e6c-178">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="86e6c-178">Create an Azure AD test user</span></span>

<span data-ttu-id="86e6c-179">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="86e6c-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="86e6c-181">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="86e6c-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86e6c-182">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="86e6c-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="86e6c-184">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="86e6c-186">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="86e6c-188">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="86e6c-188">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="86e6c-190">a.</span><span class="sxs-lookup"><span data-stu-id="86e6c-190">a.</span></span> <span data-ttu-id="86e6c-191">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86e6c-192">b.</span><span class="sxs-lookup"><span data-stu-id="86e6c-192">b.</span></span> <span data-ttu-id="86e6c-193">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86e6c-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="86e6c-194">c.</span><span class="sxs-lookup"><span data-stu-id="86e6c-194">c.</span></span> <span data-ttu-id="86e6c-195">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="86e6c-196">d.</span><span class="sxs-lookup"><span data-stu-id="86e6c-196">d.</span></span> <span data-ttu-id="86e6c-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="86e6c-198">Creare un utente test per Evidence.com</span><span class="sxs-lookup"><span data-stu-id="86e6c-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="86e6c-199">Per consentire agli utenti di Azure AD di accedere, è necessario effettuarne il provisioning per l'accesso nell'applicazione Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="86e6c-200">Questa sezione descrive come creare account utente di Azure AD in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="86e6c-201">**Per effettuare il provisioning di un account utente in Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="86e6c-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="86e6c-202">In una finestra del Web browser accedere al sito aziendale Evidence.com come amministratore.</span><span class="sxs-lookup"><span data-stu-id="86e6c-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="86e6c-203">Passare alla scheda **Admin** .</span><span class="sxs-lookup"><span data-stu-id="86e6c-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="86e6c-204">Fare clic su **Add User**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="86e6c-205">Fare clic su **Add** .</span><span class="sxs-lookup"><span data-stu-id="86e6c-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="86e6c-206">Il valore per **Email Address** dell'utente aggiunto deve corrispondere al nome utente degli utenti in Azure AD a cui si vuole concedere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="86e6c-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="86e6c-207">Se il nome utente e l'indirizzo di posta elettronica dell'organizzazione sono diversi, è possibile usare la sezione **Evidence.com > Attributi > Single Sign-On** del portale di Azure per cambiare il valore nameidentifer inviato a Evidence.com in modo che venga usato l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="86e6c-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="86e6c-208">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="86e6c-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="86e6c-209">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="86e6c-211">**Per assegnare Britta Simon a Evidence.com, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="86e6c-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="86e6c-212">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="86e6c-214">Nell'elenco delle applicazioni selezionare **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-214">In the applications list, select **Evidence.com**.</span></span>

    ![Collegamento Evidence.com nell'elenco Applicazioni](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="86e6c-216">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="86e6c-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="86e6c-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-218">Click **Add** button.</span></span> <span data-ttu-id="86e6c-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="86e6c-221">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="86e6c-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86e6c-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86e6c-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="86e6c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="86e6c-224">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="86e6c-224">Test single sign-on</span></span>

<span data-ttu-id="86e6c-225">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="86e6c-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="86e6c-226">Quando si fa clic sul riquadro Evidence.com nel pannello di accesso, si accederà automaticamente all'applicazione Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="86e6c-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="86e6c-227">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86e6c-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="86e6c-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="86e6c-228">Additional resources</span></span>

* [<span data-ttu-id="86e6c-229">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86e6c-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86e6c-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86e6c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con Asana | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Asana.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: a2f0cecb93cc382bcfd710c44eb70f80ae67f9b6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="ebe9b-103">Esercitazione: Integrazione di Azure Active Directory con Asana</span><span class="sxs-lookup"><span data-stu-id="ebe9b-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="ebe9b-104">Questa esercitazione descrive come integrare Asana con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebe9b-105">L'integrazione di Asana con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-105">Integrating Asana with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ebe9b-106">È possibile controllare in Azure AD chi può accedere ad Asana</span><span class="sxs-lookup"><span data-stu-id="ebe9b-106">You can control in Azure AD who has access to Asana</span></span>
- <span data-ttu-id="ebe9b-107">È possibile abilitare gli utenti per l'accesso automatico ad Asana (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebe9b-107">You can enable your users to automatically get signed-on to Asana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ebe9b-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ebe9b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebe9b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ebe9b-110">Prerequisites</span></span>

<span data-ttu-id="ebe9b-111">Per configurare l'integrazione di Azure AD con Asana, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-111">To configure Azure AD integration with Asana, you need the following items:</span></span>

- <span data-ttu-id="ebe9b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebe9b-113">Sottoscrizione di Asana abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ebe9b-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebe9b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebe9b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebe9b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebe9b-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebe9b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ebe9b-118">Scenario description</span></span>
<span data-ttu-id="ebe9b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebe9b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebe9b-121">Aggiunta di Asana dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ebe9b-121">Adding Asana from the gallery</span></span>
2. <span data-ttu-id="ebe9b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebe9b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-the-gallery"></a><span data-ttu-id="ebe9b-123">Aggiunta di Asana dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ebe9b-123">Adding Asana from the gallery</span></span>
<span data-ttu-id="ebe9b-124">Per configurare l'integrazione di Asana in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ebe9b-125">**Per aggiungere Asana dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ebe9b-125">**To add Asana from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ebe9b-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="ebe9b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ebe9b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="ebe9b-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="ebe9b-133">Nella casella di ricerca digitare **Asana** selezionare **Asana** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-133">In the search box, type **Asana**, select **Asana** from result panel then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ebe9b-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebe9b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ebe9b-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Asana in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ebe9b-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ebe9b-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Asana che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span></span> <span data-ttu-id="ebe9b-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Asana.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-138">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span></span>

<span data-ttu-id="ebe9b-139">Per stabilire la relazione di collegamento, in Asana assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-139">In Asana, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ebe9b-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Asana, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-140">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ebe9b-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ebe9b-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebe9b-143">**[Creare un utente di test di Asana](#create-an-asana-test-user)**: per avere una controparte di Britta Simon in Asana collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-143">**[Create an Asana test user](#create-an-asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebe9b-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebe9b-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ebe9b-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebe9b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ebe9b-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On all'applicazione Asana.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="ebe9b-148">**Per configurare Single Sign-On di Azure AD con Asana, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ebe9b-148">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="ebe9b-149">Nella pagina di integrazione dell'applicazione **Asana** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-149">In the Azure portal, on the **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ebe9b-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="ebe9b-153">Nella sezione **URL e dominio Asana** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-153">On the **Asana Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="ebe9b-155">a.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-155">a.</span></span> <span data-ttu-id="ebe9b-156">Nella casella di testo **URL di accesso** digitare l'URL: `https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="ebe9b-156">In the **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="ebe9b-157">b.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-157">b.</span></span> <span data-ttu-id="ebe9b-158">Nella casella di testo **Identificatore** digitare il valore: `https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="ebe9b-158">In the **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="ebe9b-159">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="ebe9b-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ebe9b-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ebe9b-163">Nella sezione **Configurazione di Asana** fare clic su **Configura Asana** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-163">On the **Asana Configuration** section, click **Configure Asana** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ebe9b-164">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ebe9b-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="ebe9b-166">In una finestra del browser diversa accedere all'applicazione Asana.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-166">In a different browser window, sign-on to your Asana application.</span></span> <span data-ttu-id="ebe9b-167">Per configurare SSO in Asana, accedere alle impostazioni dell'area di lavoro facendo clic sul nome dell'area di lavoro in alto a destra della schermata.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-167">To configure SSO in Asana, access the workspace settings by clicking the workspace name on the top right corner of the screen.</span></span> <span data-ttu-id="ebe9b-168">Fare quindi clic su **\<your workspace name\> Settings** (Impostazioni <nome area di lavoro>).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Impostazioni SSO di Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="ebe9b-170">Nella finestra **Organization settings** (Impostazioni organizzazione) fare clic su **Administation** (Amministrazione).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-170">On the **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="ebe9b-171">Fare clic su **Members must log in via SAML** (I membri devono accedere tramite SAML) per abilitare la configurazione di SSO.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-171">Then, click **Members must log in via SAML** to enable the SSO configuration.</span></span> <span data-ttu-id="ebe9b-172">Eseguire quindi questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-172">The perform the following steps:</span></span>
   
    ![Configurare le impostazioni dell'accesso Single Sign-On per l'organizzazione](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="ebe9b-174">a.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-174">a.</span></span> <span data-ttu-id="ebe9b-175">Nella casella di testo **URL della pagina di accesso**, incollare il **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-175">In the **Sign-in page URL** textbox, paste the **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="ebe9b-176">b.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-176">b.</span></span> <span data-ttu-id="ebe9b-177">Fare clic con il pulsante destro del mouse sul certificato scaricato dal portale Azure, quindi aprire il file di certificato nel Blocco note o nell'editor di testo preferito.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-177">Right click the certificate downloaded from Azure portal, then open the certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="ebe9b-178">Copiare il contenuto tra l'inizio e la fine del titolo del certificato e incollarlo nella casella di testo **Certificato X.509**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-178">Copy the content between the begin and the end certificate title and paste it in the **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="ebe9b-179">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-179">Click **Save**.</span></span> <span data-ttu-id="ebe9b-180">Per altre informazioni e assistenza, vedere la [guida di Asana per la configurazione di SSO](https://asana.com/guide/help/premium/authentication#gl-saml) .</span><span class="sxs-lookup"><span data-stu-id="ebe9b-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="ebe9b-181">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ebe9b-182">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ebe9b-183">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ebe9b-184">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebe9b-184">Create an Azure AD test user</span></span>

<span data-ttu-id="ebe9b-185">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="ebe9b-187">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ebe9b-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ebe9b-188">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ebe9b-190">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ebe9b-192">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ebe9b-194">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ebe9b-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ebe9b-196">a.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-196">a.</span></span> <span data-ttu-id="ebe9b-197">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebe9b-198">b.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-198">b.</span></span> <span data-ttu-id="ebe9b-199">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ebe9b-200">c.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-200">c.</span></span> <span data-ttu-id="ebe9b-201">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ebe9b-202">d.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-202">d.</span></span> <span data-ttu-id="ebe9b-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="ebe9b-204">Creare un utente test per Asana</span><span class="sxs-lookup"><span data-stu-id="ebe9b-204">Create an Asana test user</span></span>

<span data-ttu-id="ebe9b-205">In questa sezione viene creato un utente di nome Britta Simon in Asana.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="ebe9b-206">In **Asana**, passare alla sezione **Teams** (Team) nel pannello sinistro.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-206">On **Asana**, go to the **Teams** section on the left panel.</span></span> <span data-ttu-id="ebe9b-207">Fare clic sul pulsante con il segno più.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-207">Click the plus sign button.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="ebe9b-209">Digitare l'indirizzo di posta elettronica britta.simon@contoso.com nella casella di testo e quindi selezionare **Invite**(Invita).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-209">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span></span>

3. <span data-ttu-id="ebe9b-210">Fare clic su **Send Invite** (Invia invito).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-210">Click **Send Invite**.</span></span> <span data-ttu-id="ebe9b-211">Il nuovo utente riceverà un messaggio di posta elettronica nel proprio account di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ebe9b-211">The new user will receive an email into her email account.</span></span> <span data-ttu-id="ebe9b-212">e dovrà creare e convalidare l'account.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-212">She will need to create and validate the account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ebe9b-213">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebe9b-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="ebe9b-214">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Asana.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asana.</span></span>

![Assegnare il ruolo utente][200]

<span data-ttu-id="ebe9b-216">**Per assegnare Britta Simon ad Asana, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ebe9b-216">**To assign Britta Simon to Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="ebe9b-217">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ebe9b-219">Nell'elenco delle applicazioni selezionare **Asana**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-219">In the applications list, select **Asana**.</span></span>

    ![Collegamento di Asana nell'elenco delle applicazioni](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="ebe9b-221">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="ebe9b-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-223">Click **Add** button.</span></span> <span data-ttu-id="ebe9b-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="ebe9b-226">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ebe9b-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebe9b-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ebe9b-229">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ebe9b-229">Test single sign-on</span></span>

<span data-ttu-id="ebe9b-230">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-230">The objective of this section is to test your Azure AD single sign-on.</span></span>

<span data-ttu-id="ebe9b-231">Passare alla pagina di accesso di Asana.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-231">Go to Asana login page.</span></span> <span data-ttu-id="ebe9b-232">Nella casella di testo Email address (Indirizzo e-mail) inserire l'indirizzo e-mail britta.simon@contoso.com. Lasciare vuota la casella di testo della password e quindi fare clic su **Log In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="ebe9b-232">In the Email address textbox, insert the email address britta.simon@contoso.com. Leave the password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="ebe9b-233">Si verrà reindirizzati alla pagina di accesso di Azure AA.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-233">You will be redirected to Azure AD login page.</span></span> <span data-ttu-id="ebe9b-234">Completare le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="ebe9b-235">A questo punto si è connessi ad Asana.</span><span class="sxs-lookup"><span data-stu-id="ebe9b-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ebe9b-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ebe9b-236">Additional resources</span></span>

* [<span data-ttu-id="ebe9b-237">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebe9b-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebe9b-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebe9b-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png

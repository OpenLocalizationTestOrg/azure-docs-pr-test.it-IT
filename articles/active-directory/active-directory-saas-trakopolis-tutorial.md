---
title: 'Esercitazione: Integrazione di Azure Active Directory con Trakopolis | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Trakopolis.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3887cf8c085c30eb01ac769944da2fcfe3df81f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="f5255-103">Esercitazione: Integrazione di Azure Active Directory con Trakopolis</span><span class="sxs-lookup"><span data-stu-id="f5255-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="f5255-104">Questa esercitazione descrive come integrare Trakopolis con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5255-104">In this tutorial, you learn how to integrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5255-105">L'integrazione di Trakopolis con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5255-105">Integrating Trakopolis with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5255-106">È possibile controllare in Azure AD chi può accedere a Trakopolis</span><span class="sxs-lookup"><span data-stu-id="f5255-106">You can control in Azure AD who has access to Trakopolis</span></span>
- <span data-ttu-id="f5255-107">È possibile abilitare gli utenti per l'accesso automatico a Trakopolis (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5255-107">You can enable your users to automatically get signed-on to Trakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5255-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5255-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5255-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5255-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5255-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f5255-110">Prerequisites</span></span>

<span data-ttu-id="f5255-111">Per configurare l'integrazione di Azure AD con Trakopolis, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5255-111">To configure Azure AD integration with Trakopolis, you need the following items:</span></span>

- <span data-ttu-id="f5255-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5255-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5255-113">Sottoscrizione di Trakopolis abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f5255-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5255-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f5255-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5255-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5255-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5255-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f5255-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5255-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5255-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5255-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f5255-118">Scenario description</span></span>
<span data-ttu-id="f5255-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f5255-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5255-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5255-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5255-121">Aggiunta di Trakopolis dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f5255-121">Adding Trakopolis from the gallery</span></span>
2. <span data-ttu-id="f5255-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5255-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-the-gallery"></a><span data-ttu-id="f5255-123">Aggiunta di Trakopolis dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f5255-123">Adding Trakopolis from the gallery</span></span>
<span data-ttu-id="f5255-124">Per configurare l'integrazione di Trakopolis in Azure AD, è necessario aggiungere Trakopolis dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f5255-124">To configure the integration of Trakopolis into Azure AD, you need to add Trakopolis from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5255-125">**Per aggiungere Trakopolis dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5255-125">**To add Trakopolis from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5255-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f5255-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5255-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f5255-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5255-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5255-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f5255-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5255-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f5255-133">Nella casella di ricerca digitare **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="f5255-133">In the search box, type **Trakopolis**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="f5255-135">Nel pannello dei risultati selezionare **Trakopolis** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5255-135">In the results panel, select **Trakopolis**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5255-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5255-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5255-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Trakopolis in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5255-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5255-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Trakopolis che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5255-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakopolis is to a user in Azure AD.</span></span> <span data-ttu-id="f5255-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="f5255-140">In other words, a link relationship between an Azure AD user and the related user in Trakopolis needs to be established.</span></span>

<span data-ttu-id="f5255-141">Per stabilire la relazione di collegamento, in Trakopolis assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="f5255-141">In Trakopolis, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5255-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Trakopolis, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5255-142">To configure and test Azure AD single sign-on with Trakopolis, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5255-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f5255-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5255-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5255-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5255-145">**[Creazione di un utente di test di Trakopolis](#creating-a-trakopolis-test-user)**: per avere una controparte di Britta Simon in Trakopolis collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5255-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - to have a counterpart of Britta Simon in Trakopolis that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5255-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5255-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5255-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f5255-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5255-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5255-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5255-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="f5255-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="f5255-150">**Per configurare Single Sign-On di Azure AD con Trakopolis, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5255-150">**To configure Azure AD single sign-on with Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="f5255-151">Nella pagina di integrazione dell'applicazione **Trakopolis** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f5255-151">In the Azure portal, on the **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f5255-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f5255-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="f5255-155">Nella sezione **URL e dominio Trakopolis** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5255-155">On the **Trakopolis Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="f5255-157">a.</span><span class="sxs-lookup"><span data-stu-id="f5255-157">a.</span></span> <span data-ttu-id="f5255-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.trakopolis.com/`.</span><span class="sxs-lookup"><span data-stu-id="f5255-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="f5255-159">b.</span><span class="sxs-lookup"><span data-stu-id="f5255-159">b.</span></span> <span data-ttu-id="f5255-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="f5255-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5255-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f5255-161">These values are not real.</span></span> <span data-ttu-id="f5255-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="f5255-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5255-163">Per ottenere questi valori, contattare il [team di supporto client di Trakopolis](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="f5255-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) to get these values.</span></span> 

4. <span data-ttu-id="f5255-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="f5255-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="f5255-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f5255-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5255-168">Nella sezione **Configurazione di Trakopolis** fare clic su **Configura Trakopolis** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="f5255-168">On the **Trakopolis Configuration** section, click **Configure Trakopolis** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f5255-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f5255-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="f5255-171">Per configurare l'accesso Single Sign-On sul lato **Trakopolis**, è necessario inviare il file **XML di metadati scaricato, l'URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di Trakopolis](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="f5255-171">To configure single sign-on on **Trakopolis** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="f5255-172">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="f5255-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f5255-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f5255-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5255-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f5255-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5255-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5255-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5255-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5255-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5255-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5255-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f5255-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f5255-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5255-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f5255-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5255-182">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f5255-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5255-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f5255-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5255-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f5255-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5255-188">a.</span><span class="sxs-lookup"><span data-stu-id="f5255-188">a.</span></span> <span data-ttu-id="f5255-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5255-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5255-190">b.</span><span class="sxs-lookup"><span data-stu-id="f5255-190">b.</span></span> <span data-ttu-id="f5255-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5255-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5255-192">c.</span><span class="sxs-lookup"><span data-stu-id="f5255-192">c.</span></span> <span data-ttu-id="f5255-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f5255-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5255-194">d.</span><span class="sxs-lookup"><span data-stu-id="f5255-194">d.</span></span> <span data-ttu-id="f5255-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f5255-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="f5255-196">Creazione di un utente di test di Trakopolis</span><span class="sxs-lookup"><span data-stu-id="f5255-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="f5255-197">In questa sezione viene creato un utente di nome Britta Simon in Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="f5255-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="f5255-198">Collaborare con il [team di supporto di Trakopolis](mailto:support@cantelematics.com) per aggiungere gli utenti nella piattaforma Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="f5255-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add the users in the Trakopolis platform.</span></span> <span data-ttu-id="f5255-199">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f5255-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5255-200">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5255-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5255-201">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="f5255-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakopolis.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f5255-203">**Per assegnare Britta Simon a Trakopolis, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f5255-203">**To assign Britta Simon to Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="f5255-204">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f5255-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f5255-206">Nell’elenco delle applicazioni selezionare **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="f5255-206">In the applications list, select **Trakopolis**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="f5255-208">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f5255-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f5255-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5255-210">Click **Add** button.</span></span> <span data-ttu-id="f5255-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5255-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f5255-213">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f5255-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5255-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f5255-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5255-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f5255-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5255-216">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f5255-216">Testing single sign-on</span></span>

<span data-ttu-id="f5255-217">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f5255-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f5255-218">Quando si fa clic sul riquadro Trakopolis nel pannello di accesso, si dovrebbe automaticamente accedere all'applicazione Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="f5255-218">When you click the Trakopolis tile in the Access Panel, you should get automatically signed-on to your Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5255-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f5255-219">Additional resources</span></span>

* [<span data-ttu-id="f5255-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5255-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5255-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5255-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png


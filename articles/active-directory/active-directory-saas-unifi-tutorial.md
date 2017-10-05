---
title: 'Esercitazione: Integrazione di Azure Active Directory con UNIFI | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e UNIFI.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 09074d4628825909f0bb961c8001e53fb06cf7c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="885a7-103">Esercitazione: Integrazione di Azure Active Directory con UNIFI</span><span class="sxs-lookup"><span data-stu-id="885a7-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="885a7-104">Questa esercitazione descrive come integrare UNIFI con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="885a7-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="885a7-105">L'integrazione di UNIFI con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="885a7-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="885a7-106">È possibile controllare in Azure AD chi può accedere a UNIFI</span><span class="sxs-lookup"><span data-stu-id="885a7-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="885a7-107">È possibile abilitare gli utenti per l'accesso automatico a UNIFI (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="885a7-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="885a7-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="885a7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="885a7-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="885a7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="885a7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="885a7-110">Prerequisites</span></span>

<span data-ttu-id="885a7-111">Per configurare l'integrazione di Azure AD con UNIFI, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="885a7-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="885a7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="885a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="885a7-113">Una sottoscrizione UNIFI abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="885a7-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="885a7-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="885a7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="885a7-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="885a7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="885a7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="885a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="885a7-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="885a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="885a7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="885a7-118">Scenario description</span></span>
<span data-ttu-id="885a7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="885a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="885a7-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="885a7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="885a7-121">Aggiunta di UNIFI dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="885a7-121">Adding UNIFI from the gallery</span></span>
2. <span data-ttu-id="885a7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="885a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="885a7-123">Aggiunta di UNIFI dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="885a7-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="885a7-124">Per configurare l'integrazione di UNIFI in Azure AD, è necessario aggiungere UNIFI dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="885a7-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="885a7-125">**Per aggiungere UNIFI dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="885a7-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="885a7-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="885a7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="885a7-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="885a7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="885a7-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="885a7-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="885a7-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="885a7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="885a7-133">Nella casella di ricerca digitare **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="885a7-133">In the search box, type **UNIFI**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="885a7-135">Nel pannello dei risultati selezionare **UNIFI** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="885a7-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="885a7-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="885a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="885a7-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UNIFI in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="885a7-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="885a7-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di UNIFI che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="885a7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="885a7-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in UNIFI.</span><span class="sxs-lookup"><span data-stu-id="885a7-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="885a7-141">Per stabilire la relazione di collegamento, in UNIFI assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="885a7-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="885a7-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con UNIFI, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="885a7-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="885a7-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="885a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="885a7-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="885a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="885a7-145">**[Creazione di un utente test di UNIFI](#creating-a-unifi-test-user)**: per avere una controparte di Britta Simon in UNIFI collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="885a7-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="885a7-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="885a7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="885a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="885a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="885a7-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="885a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="885a7-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione UNIFI.</span><span class="sxs-lookup"><span data-stu-id="885a7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="885a7-150">**Per configurare l'accesso Single Sign-On di Azure AD con UNIFI, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="885a7-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="885a7-151">Nella pagina di integrazione dell'applicazione **UNIFI** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="885a7-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="885a7-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="885a7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="885a7-155">Nella sezione **URL e dominio UNIFI** se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="885a7-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="885a7-157">Nella casella di testo **Identificatore** digitare il valore: `INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="885a7-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="885a7-158">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="885a7-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="885a7-160">Nella casella di testo **URL accesso** digitare l'URL: `https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="885a7-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="885a7-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="885a7-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="885a7-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="885a7-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="885a7-165">Nella sezione **Configurazione di UNIFI** fare clic su **Configura UNIFI** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="885a7-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="885a7-166">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="885a7-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="885a7-168">In un'altra finestra del browser Web accedere al sito aziendale di **UNIFI** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="885a7-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="885a7-169">Fare clic su **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="885a7-169">Click on the **Users**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="885a7-171">Fare clic su **Add New Identity Provider** (Aggiungi nuovo provider di identità).</span><span class="sxs-lookup"><span data-stu-id="885a7-171">Click on the **Add New Identity Provider**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="885a7-173">Nella sezione **Add New Identity Provider** (Aggiungi nuovo provider di identità) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="885a7-173">In the **Add Identity Provider** section, perform the following steps:</span></span>   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="885a7-175">a.</span><span class="sxs-lookup"><span data-stu-id="885a7-175">a.</span></span> <span data-ttu-id="885a7-176">Nella casella di testo **Provider Name** (Nome provider) digitare il nome del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="885a7-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="885a7-177">b.</span><span class="sxs-lookup"><span data-stu-id="885a7-177">b.</span></span> <span data-ttu-id="885a7-178">Nella casella di testo **Provider URL** (URL provider) incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="885a7-178">In the the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="885a7-179">c.</span><span class="sxs-lookup"><span data-stu-id="885a7-179">c.</span></span> <span data-ttu-id="885a7-180">Aprire il certificato scaricato dal portale di Azure nel blocco note, rimuovere i tag **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---** e quindi incollare il contenuto rimanente nella casella di testo **Certificate** (Certificato).</span><span class="sxs-lookup"><span data-stu-id="885a7-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="885a7-181">d.</span><span class="sxs-lookup"><span data-stu-id="885a7-181">d.</span></span> <span data-ttu-id="885a7-182">Selezionare la casella di controllo **is Default Provider** (Provider predefinito).</span><span class="sxs-lookup"><span data-stu-id="885a7-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="885a7-183">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="885a7-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="885a7-184">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="885a7-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="885a7-185">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="885a7-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="885a7-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="885a7-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="885a7-187">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="885a7-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="885a7-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="885a7-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="885a7-190">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="885a7-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="885a7-192">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="885a7-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="885a7-194">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="885a7-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="885a7-196">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="885a7-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="885a7-198">a.</span><span class="sxs-lookup"><span data-stu-id="885a7-198">a.</span></span> <span data-ttu-id="885a7-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="885a7-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="885a7-200">b.</span><span class="sxs-lookup"><span data-stu-id="885a7-200">b.</span></span> <span data-ttu-id="885a7-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="885a7-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="885a7-202">c.</span><span class="sxs-lookup"><span data-stu-id="885a7-202">c.</span></span> <span data-ttu-id="885a7-203">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="885a7-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="885a7-204">d.</span><span class="sxs-lookup"><span data-stu-id="885a7-204">d.</span></span> <span data-ttu-id="885a7-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="885a7-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="885a7-206">Creazione di un utente test di UNIFI</span><span class="sxs-lookup"><span data-stu-id="885a7-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="885a7-207">In questa sezione viene creato un utente di nome Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="885a7-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="885a7-208">**UNIFI** supporta il provisioning automatico dell'utente, pertanto non è necessaria la procedura manuale.</span><span class="sxs-lookup"><span data-stu-id="885a7-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="885a7-209">Gli utenti vengono creati automaticamente al termine dell'autenticazione da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="885a7-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="885a7-210">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="885a7-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="885a7-211">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a UNIFI.</span><span class="sxs-lookup"><span data-stu-id="885a7-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![Assegna utente][200] 

<span data-ttu-id="885a7-213">**Per assegnare Britta Simon a UNIFI seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="885a7-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="885a7-214">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="885a7-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="885a7-216">Nell'elenco delle applicazioni selezionare **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="885a7-216">In the applications list, select **UNIFI**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="885a7-218">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="885a7-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="885a7-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="885a7-220">Click **Add** button.</span></span> <span data-ttu-id="885a7-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="885a7-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="885a7-223">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="885a7-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="885a7-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="885a7-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="885a7-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="885a7-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="885a7-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="885a7-226">Testing single sign-on</span></span>

<span data-ttu-id="885a7-227">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="885a7-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="885a7-228">Quando si fa clic sul riquadro UNIFI nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione UNIFI.</span><span class="sxs-lookup"><span data-stu-id="885a7-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="885a7-229">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="885a7-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="885a7-230">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="885a7-230">Additional resources</span></span>

* [<span data-ttu-id="885a7-231">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="885a7-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="885a7-232">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="885a7-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png


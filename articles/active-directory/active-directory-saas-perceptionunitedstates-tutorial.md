---
title: 'Esercitazione: Integrazione di Azure Active Directory con Perception United States (Non-UltiPro) | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Perception United States (Non-UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 8e2f9f979f8b94e0c043d4db6e93bd7a53c3dd27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="52e53-103">Esercitazione: Integrazione di Azure Active Directory con Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="52e53-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="52e53-104">Questa esercitazione descrive come integrare Perception United States (Non-UltiPro) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52e53-104">In this tutorial, you learn how to integrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52e53-105">L'integrazione di Perception United States (Non-UltiPro) con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="52e53-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52e53-106">È possibile controllare in Azure AD chi può accedere a Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="52e53-106">You can control in Azure AD who has access to Perception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="52e53-107">È possibile abilitare gli utenti per l'accesso automatico a Perception United States (Non-UltiPro) (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="52e53-107">You can enable your users to automatically get signed-on to Perception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="52e53-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="52e53-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="52e53-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52e53-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52e53-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="52e53-110">Prerequisites</span></span>

<span data-ttu-id="52e53-111">Per configurare l'integrazione di Azure AD con Perception United States (Non-UltiPro), sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="52e53-111">To configure Azure AD integration with Perception United States (Non-UltiPro), you need the following items:</span></span>

- <span data-ttu-id="52e53-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52e53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52e53-113">Sottoscrizione di Perception United States (Non-UltiPro) abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="52e53-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52e53-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="52e53-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52e53-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="52e53-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52e53-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="52e53-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52e53-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52e53-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52e53-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="52e53-118">Scenario description</span></span>
<span data-ttu-id="52e53-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="52e53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52e53-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="52e53-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52e53-121">Aggiunta di Perception United States (Non-UltiPro) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="52e53-121">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
2. <span data-ttu-id="52e53-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="52e53-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a><span data-ttu-id="52e53-123">Aggiunta di Perception United States (Non-UltiPro) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="52e53-123">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
<span data-ttu-id="52e53-124">Per configurare l'integrazione di Perception United States (Non-UltiPro) in Azure AD, è necessario aggiungere Perception United States (Non-UltiPro) dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="52e53-124">To configure the integration of Perception United States (Non-UltiPro) into Azure AD, you need to add Perception United States (Non-UltiPro) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52e53-125">**Per aggiungere Perception United States (Non-UltiPro) dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="52e53-125">**To add Perception United States (Non-UltiPro) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52e53-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="52e53-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="52e53-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="52e53-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52e53-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="52e53-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="52e53-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="52e53-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="52e53-133">Nella casella di ricerca digitare **Perception United States (Non-UltiPro)**, selezionare **Perception United States (Non-UltiPro)** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="52e53-133">In the search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button to add the application.</span></span>

    ![Perception United States (Non-UltiPro) nell'elenco risultati](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="52e53-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="52e53-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="52e53-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Perception United States (Non-UltiPro) usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52e53-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52e53-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Perception United States (Non-UltiPro) corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52e53-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Perception United States (Non-UltiPro) is to a user in Azure AD.</span></span> <span data-ttu-id="52e53-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="52e53-138">In other words, a link relationship between an Azure AD user and the related user in Perception United States (Non-UltiPro) needs to be established.</span></span>

<span data-ttu-id="52e53-139">Per stabilire la relazione di collegamento, in Perception United States (Non-UltiPro) assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="52e53-139">In Perception United States (Non-UltiPro), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52e53-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Perception United States (Non-UltiPro), è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="52e53-140">To configure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52e53-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="52e53-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52e53-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52e53-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52e53-143">**[Creare un utente di test di Perception United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**: per avere una controparte di Britta Simon in Perception United States (Non-UltiPro) collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52e53-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - to have a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="52e53-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52e53-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52e53-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="52e53-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="52e53-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="52e53-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="52e53-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="52e53-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="52e53-148">**Per configurare l'accesso Single Sign-On di Azure AD con Perception United States (Non-UltiPro), seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="52e53-148">**To configure Azure AD single sign-on with Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="52e53-149">Nella pagina di integrazione dell'applicazione **Perception United States (Non-UltiPro)** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="52e53-149">In the Azure portal, on the **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="52e53-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="52e53-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="52e53-153">Nella sezione **URL e dominio Perception United States (Non-UltiPro)** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="52e53-153">On the **Perception United States (Non-UltiPro) Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="52e53-155">a.</span><span class="sxs-lookup"><span data-stu-id="52e53-155">a.</span></span> <span data-ttu-id="52e53-156">Nella casella di testo **Identificatore** digitare l'URL: `https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="52e53-156">In the **Identifier** textbox, type the URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="52e53-157">b.</span><span class="sxs-lookup"><span data-stu-id="52e53-157">b.</span></span> <span data-ttu-id="52e53-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="52e53-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52e53-159">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="52e53-159">The value is not real.</span></span> <span data-ttu-id="52e53-160">È necessario aggiornarlo con l'URL di risposta reale, descritto più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="52e53-160">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="52e53-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="52e53-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="52e53-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="52e53-163">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52e53-165">Nella sezione **Configurazione di Perception United States (Non-UltiPro)** fare clic su **Configura Perception United States (Non-UltiPro)** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="52e53-165">On the **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="52e53-166">Copiare l'**ID di entità SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="52e53-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="52e53-167">a.</span><span class="sxs-lookup"><span data-stu-id="52e53-167">a.</span></span> <span data-ttu-id="52e53-168">Per l'applicazione **Perception United States (Non-UltiPro)** è necessario il valore dell'**ID di entità SAML** copiato, che deve essere con codifica URI.</span><span class="sxs-lookup"><span data-stu-id="52e53-168">The **Perception United States (Non-UltiPro)** application requires the **SAML Entity ID** value, which you have copied, to be uri encoded.</span></span> <span data-ttu-id="52e53-169">Per ottenere il valore con codifica URI, usare il collegamento seguente: **http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="52e53-169">To get the uri encoded value, use the following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="52e53-170">b.</span><span class="sxs-lookup"><span data-stu-id="52e53-170">b.</span></span> <span data-ttu-id="52e53-171">Dopo aver ottenuto il valore con codifica URI, combinarlo con l'**URL di risposta** come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="52e53-171">After getting the uri encoded value combine it with the **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="52e53-172">c.</span><span class="sxs-lookup"><span data-stu-id="52e53-172">c.</span></span> <span data-ttu-id="52e53-173">Incollare il valore indicato sopra nella casella di testo **URL di risposta** nella sezione **URL e dominio Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="52e53-173">Paste the above value in the **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Configurazione di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="52e53-175">In un'altra finestra del browser accedere al sito aziendale di Perception United States (Non-UltiPro) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="52e53-175">In another browser window, sign on to your Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="52e53-176">Sulla barra degli strumenti principale fare clic su **Account Settings** (Impostazioni account).</span><span class="sxs-lookup"><span data-stu-id="52e53-176">In the main toolbar, click **Account Settings**.</span></span>

    ![Utente di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="52e53-178">Nella pagina **Account Settings** (Impostazioni account) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="52e53-178">On the **Account Settings** page, perform the following steps:</span></span>

    ![Utente di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="52e53-180">a.</span><span class="sxs-lookup"><span data-stu-id="52e53-180">a.</span></span> <span data-ttu-id="52e53-181">Nella casella di testo **Company Name** (Nome società) digitare il nome della **società**.</span><span class="sxs-lookup"><span data-stu-id="52e53-181">In the **Company Name** textbox, type the name of the **Company**.</span></span>
    
    <span data-ttu-id="52e53-182">b.</span><span class="sxs-lookup"><span data-stu-id="52e53-182">b.</span></span> <span data-ttu-id="52e53-183">Nella casella di testo **Account Name** (Nome account) digitare il nome dell'**account**.</span><span class="sxs-lookup"><span data-stu-id="52e53-183">In the **Account Name** textbox, type the name of the **Account**.</span></span>

    <span data-ttu-id="52e53-184">c.</span><span class="sxs-lookup"><span data-stu-id="52e53-184">c.</span></span> <span data-ttu-id="52e53-185">Nella casella di testo **Default Reply-To Email** (Indirizzo di posta elettronica predefinito per le risposte) digitare un **indirizzo**valido.</span><span class="sxs-lookup"><span data-stu-id="52e53-185">In **Default Reply-To Email** text box, type the valid **Email**.</span></span>

    <span data-ttu-id="52e53-186">d.</span><span class="sxs-lookup"><span data-stu-id="52e53-186">d.</span></span> <span data-ttu-id="52e53-187">Per **SSO Identity Provider** (Provider di identità SSO) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="52e53-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="52e53-188">Nella pagina **SSO Configuration** (Configurazione SSO) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="52e53-188">On the **SSO Configuration** page, perform the following steps:</span></span>

    ![Configurazione SSO di Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="52e53-190">a.</span><span class="sxs-lookup"><span data-stu-id="52e53-190">a.</span></span> <span data-ttu-id="52e53-191">Per **SAML NameID Type** (Tipo ID nome SAML) selezionare **EMAIL** (POSTA ELETTRONICA).</span><span class="sxs-lookup"><span data-stu-id="52e53-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="52e53-192">b.</span><span class="sxs-lookup"><span data-stu-id="52e53-192">b.</span></span> <span data-ttu-id="52e53-193">Nella casella di testo **SSO Configuration Name** (Nome configurazione SSO) digitare il nome della **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="52e53-193">In the **SSO Configuration Name** textbox, type the name of your **Configuration**.</span></span>
    
    <span data-ttu-id="52e53-194">c.</span><span class="sxs-lookup"><span data-stu-id="52e53-194">c.</span></span> <span data-ttu-id="52e53-195">Nella casella di testo **Identity Provider Name** (Nome provider di identità) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="52e53-195">In **Identity Provider Name** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="52e53-196">d.</span><span class="sxs-lookup"><span data-stu-id="52e53-196">d.</span></span> <span data-ttu-id="52e53-197">Nella casella di testo **SAML Domain** (Dominio SAML) immettere il dominio, come **@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="52e53-197">In **SAML Domain textbox**, enter the domain like **@contoso.com**.</span></span>

    <span data-ttu-id="52e53-198">e.</span><span class="sxs-lookup"><span data-stu-id="52e53-198">e.</span></span> <span data-ttu-id="52e53-199">Fare clic su **Upload Again** (Carica di nuovo) per caricare il file **XML metadati**.</span><span class="sxs-lookup"><span data-stu-id="52e53-199">Click on **Upload Again** to upload the **Metadata XML** file.</span></span>

    <span data-ttu-id="52e53-200">f.</span><span class="sxs-lookup"><span data-stu-id="52e53-200">f.</span></span> <span data-ttu-id="52e53-201">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="52e53-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="52e53-202">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="52e53-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52e53-203">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="52e53-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52e53-204">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52e53-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="52e53-205">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="52e53-205">Create an Azure AD test user</span></span>

<span data-ttu-id="52e53-206">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="52e53-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="52e53-208">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="52e53-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52e53-209">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="52e53-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="52e53-211">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="52e53-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="52e53-213">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="52e53-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="52e53-215">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="52e53-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="52e53-217">a.</span><span class="sxs-lookup"><span data-stu-id="52e53-217">a.</span></span> <span data-ttu-id="52e53-218">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52e53-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52e53-219">b.</span><span class="sxs-lookup"><span data-stu-id="52e53-219">b.</span></span> <span data-ttu-id="52e53-220">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52e53-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="52e53-221">c.</span><span class="sxs-lookup"><span data-stu-id="52e53-221">c.</span></span> <span data-ttu-id="52e53-222">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="52e53-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="52e53-223">d.</span><span class="sxs-lookup"><span data-stu-id="52e53-223">d.</span></span> <span data-ttu-id="52e53-224">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="52e53-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="52e53-225">Creare un utente di test di Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="52e53-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="52e53-226">In questa sezione viene creato un utente di nome Britta Simon in Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="52e53-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="52e53-227">Collaborare con il [team di supporto clienti di Perception United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) per aggiungere gli utenti nella piattaforma Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="52e53-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="52e53-228">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="52e53-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="52e53-229">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="52e53-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Perception United States (Non-UltiPro).</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="52e53-231">**Per assegnare Britta Simon a Perception United States (Non-UltiPro)y, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="52e53-231">**To assign Britta Simon to Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="52e53-232">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="52e53-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="52e53-234">Nell'elenco delle applicazioni selezionare **Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="52e53-234">In the applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![Collegamento di Perception United States (Non-UltiPro) nell'elenco delle applicazioni](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="52e53-236">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="52e53-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="52e53-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="52e53-238">Click **Add** button.</span></span> <span data-ttu-id="52e53-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="52e53-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="52e53-241">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="52e53-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="52e53-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="52e53-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52e53-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="52e53-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="52e53-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="52e53-244">Test single sign-on</span></span>

<span data-ttu-id="52e53-245">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="52e53-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52e53-246">Quando si fa clic sul riquadro Perception United States (Non-UltiPro) nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="52e53-246">When you click the Perception United States (Non-UltiPro) tile in the Access Panel, you should get automatically signed-on to your Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="52e53-247">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52e53-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="52e53-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="52e53-248">Additional resources</span></span>

* [<span data-ttu-id="52e53-249">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52e53-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52e53-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52e53-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png


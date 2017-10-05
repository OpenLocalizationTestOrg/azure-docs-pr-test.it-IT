---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mimecast Admin Console | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Mimecast Admin Console.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="231a5-103">Esercitazione: Integrazione di Azure Active Directory con Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="231a5-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="231a5-104">Questa esercitazione descrive come integrare Mimecast Admin Console con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="231a5-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="231a5-105">L'integrazione di Mimecast Admin Console con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="231a5-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="231a5-106">È possibile controllare in Azure AD chi può accedere a Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="231a5-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="231a5-107">È possibile abilitare gli utenti per l'accesso automatico a Mimecast Admin Console (Single Sign-On) con gli account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231a5-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="231a5-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="231a5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="231a5-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="231a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="231a5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="231a5-110">Prerequisites</span></span>

<span data-ttu-id="231a5-111">Per configurare l'integrazione di Azure AD con Mimecast Admin Console, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="231a5-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="231a5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="231a5-113">Sottoscrizione di Mimecast Admin Console abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="231a5-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="231a5-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="231a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="231a5-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="231a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="231a5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="231a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="231a5-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="231a5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="231a5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="231a5-118">Scenario description</span></span>
<span data-ttu-id="231a5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="231a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="231a5-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="231a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="231a5-121">Aggiunta di Mimecast Admin Console dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="231a5-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="231a5-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="231a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="231a5-123">Aggiunta di Mimecast Admin Console dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="231a5-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="231a5-124">Per configurare l'integrazione di Mimecast Admin Console in Azure AD, è necessario aggiungere Mimecast Admin Console dalla raccolta all'elenco delle app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="231a5-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="231a5-125">**Per aggiungere Mimecast Admin Console dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="231a5-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="231a5-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="231a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="231a5-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="231a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="231a5-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="231a5-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="231a5-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="231a5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="231a5-133">Nella casella di ricerca digitare **Mimecast Admin Console**, selezionare **Mimecast Admin Console** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="231a5-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Mimecast Admin Console nell'elenco risultati](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="231a5-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="231a5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="231a5-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mimecast Admin Console con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="231a5-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="231a5-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di Mimecast Admin Console corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231a5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="231a5-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="231a5-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="231a5-139">Per stabilire la relazione di collegamento, in Mimecast Admin Console assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="231a5-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="231a5-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Mimecast Admin Console, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="231a5-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="231a5-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="231a5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="231a5-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="231a5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="231a5-143">**[Creare un utente test di Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)**: per avere una controparte di Britta Simon in Mimecast Admin Console collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231a5-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="231a5-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231a5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="231a5-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="231a5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="231a5-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="231a5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="231a5-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="231a5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="231a5-148">**Per configurare l'accesso Single Sign-On di Azure AD con Mimecast Admin Console, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="231a5-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="231a5-149">Nella pagina di integrazione dell'applicazione **Mimecast Admin Console** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="231a5-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="231a5-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="231a5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="231a5-153">Nella sezione **URL e dominio Mimecast Admin Console** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="231a5-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="231a5-155">Nella casella di testo **URL accesso** digitare l'URL:</span><span class="sxs-lookup"><span data-stu-id="231a5-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="231a5-156">L’URL di accesso è specifico dell’area geografica.</span><span class="sxs-lookup"><span data-stu-id="231a5-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="231a5-157">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="231a5-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="231a5-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="231a5-159">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="231a5-161">Nella sezione **Configurazione di Mimecast Admin Console** fare clic su **Configura Mimecast Admin Console** per visualizzare la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="231a5-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="231a5-162">Copiare i valori **SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="231a5-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="231a5-164">In un'altra finestra del Web browser accedere a Mimecast Admin Console come amministratore.</span><span class="sxs-lookup"><span data-stu-id="231a5-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="231a5-165">Passare a **Services \> Application**.</span><span class="sxs-lookup"><span data-stu-id="231a5-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="231a5-166">![Servizi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Servizi")</span><span class="sxs-lookup"><span data-stu-id="231a5-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="231a5-167">Fare clic su **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="231a5-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="231a5-168">![Profili di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Profili di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="231a5-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="231a5-169">Fare clic su **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="231a5-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="231a5-170">![Nuovi profili di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Nuovi profili di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="231a5-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="231a5-171">Nella sezione **Authentication Profile** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="231a5-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="231a5-172">![Profilo di autenticazione](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Profilo di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="231a5-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="231a5-173">a.</span><span class="sxs-lookup"><span data-stu-id="231a5-173">a.</span></span> <span data-ttu-id="231a5-174">Nella casella di testo **Description** digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="231a5-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="231a5-175">b.</span><span class="sxs-lookup"><span data-stu-id="231a5-175">b.</span></span> <span data-ttu-id="231a5-176">Selezionare **Enforce SAML Authentication for Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="231a5-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="231a5-177">c.</span><span class="sxs-lookup"><span data-stu-id="231a5-177">c.</span></span> <span data-ttu-id="231a5-178">Come **Provider** selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="231a5-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="231a5-179">d.</span><span class="sxs-lookup"><span data-stu-id="231a5-179">d.</span></span> <span data-ttu-id="231a5-180">Incollare il valore di **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure nella casella di testo **Issuer URL** (URL autorità di certificazione).</span><span class="sxs-lookup"><span data-stu-id="231a5-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="231a5-181">e.</span><span class="sxs-lookup"><span data-stu-id="231a5-181">e.</span></span> <span data-ttu-id="231a5-182">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **Login URL** (URL di accesso).</span><span class="sxs-lookup"><span data-stu-id="231a5-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="231a5-183">f.</span><span class="sxs-lookup"><span data-stu-id="231a5-183">f.</span></span> <span data-ttu-id="231a5-184">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **Login URL** (URL di disconnessione).</span><span class="sxs-lookup"><span data-stu-id="231a5-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="231a5-185">Il valore di Login URL e il valore Logout URL per Mimecast Admin Console sono identici.</span><span class="sxs-lookup"><span data-stu-id="231a5-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="231a5-186">g.</span><span class="sxs-lookup"><span data-stu-id="231a5-186">g.</span></span> <span data-ttu-id="231a5-187">Aprire il certificato con codifica Base 64 scaricato dal portale di Azure nel Blocco note, rimuovere la prima riga ("*--*") e l'ultima riga ("*--*"), copiare il contenuto rimanente negli Appunti e quindi incollarlo nella casella di testo **Identity Provider Certificate (Metadata)** (Certificato provider di identità - Metadati).</span><span class="sxs-lookup"><span data-stu-id="231a5-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="231a5-188">h.</span><span class="sxs-lookup"><span data-stu-id="231a5-188">h.</span></span> <span data-ttu-id="231a5-189">Selezionare **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="231a5-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="231a5-190">i.</span><span class="sxs-lookup"><span data-stu-id="231a5-190">i.</span></span> <span data-ttu-id="231a5-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="231a5-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="231a5-192">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="231a5-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="231a5-193">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="231a5-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="231a5-194">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="231a5-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="231a5-195">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="231a5-195">Create an Azure AD test user</span></span>

<span data-ttu-id="231a5-196">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="231a5-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="231a5-198">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="231a5-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="231a5-199">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="231a5-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="231a5-201">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="231a5-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="231a5-203">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="231a5-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="231a5-205">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="231a5-205">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="231a5-207">a.</span><span class="sxs-lookup"><span data-stu-id="231a5-207">a.</span></span> <span data-ttu-id="231a5-208">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="231a5-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="231a5-209">b.</span><span class="sxs-lookup"><span data-stu-id="231a5-209">b.</span></span> <span data-ttu-id="231a5-210">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="231a5-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="231a5-211">c.</span><span class="sxs-lookup"><span data-stu-id="231a5-211">c.</span></span> <span data-ttu-id="231a5-212">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="231a5-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="231a5-213">d.</span><span class="sxs-lookup"><span data-stu-id="231a5-213">d.</span></span> <span data-ttu-id="231a5-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="231a5-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="231a5-215">Creare un utente test di Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="231a5-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="231a5-216">Per consentire agli utenti di Azure AD di accedere a Mimecast Admin Console, è necessario eseguirne il provisioning in Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="231a5-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="231a5-217">Nel caso di Mimecast Admin Console, il provisioning è un’attività manuale.</span><span class="sxs-lookup"><span data-stu-id="231a5-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="231a5-218">Per poter creare gli utenti è necessario registrare un dominio.</span><span class="sxs-lookup"><span data-stu-id="231a5-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="231a5-219">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="231a5-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="231a5-220">Accedere a **Mimecast Admin Console** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="231a5-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="231a5-221">Accedere a **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="231a5-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="231a5-222">![Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directory")</span><span class="sxs-lookup"><span data-stu-id="231a5-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="231a5-223">Fare clic su **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="231a5-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="231a5-224">![Registra nuovo dominio](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Registra nuovo dominio")</span><span class="sxs-lookup"><span data-stu-id="231a5-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="231a5-225">Dopo aver creato il nuovo dominio, fare clic su **New Address**.</span><span class="sxs-lookup"><span data-stu-id="231a5-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="231a5-226">![Nuovo indirizzo](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Nuovo indirizzo")</span><span class="sxs-lookup"><span data-stu-id="231a5-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="231a5-227">Nella finestra di dialogo del nuovo indirizzo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="231a5-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="231a5-228">![Salvare](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Salvare")</span><span class="sxs-lookup"><span data-stu-id="231a5-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="231a5-229">a.</span><span class="sxs-lookup"><span data-stu-id="231a5-229">a.</span></span> <span data-ttu-id="231a5-230">Nelle caselle di testo corrispondenti digitare gli attributi **indirizzo di posta elettronica**, **nome globale**, **password** e **conferma password** di un account Azure AD valido di cui si intende effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="231a5-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="231a5-231">b.</span><span class="sxs-lookup"><span data-stu-id="231a5-231">b.</span></span> <span data-ttu-id="231a5-232">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="231a5-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="231a5-233">È possibile usare qualsiasi altro strumento di creazione di account utente di Mimecast Admin Console o le API fornite da Mimecast Admin Console per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="231a5-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="231a5-234">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="231a5-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="231a5-235">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure tramite la concessione dell'accesso a Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="231a5-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="231a5-237">**Per assegnare Britta Simon a Mimecast Admin Console, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="231a5-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="231a5-238">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="231a5-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="231a5-240">Nell'elenco delle applicazioni selezionare **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="231a5-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![Collegamento Mimecast Admin Console nell'elenco Applicazioni](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="231a5-242">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="231a5-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="231a5-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="231a5-244">Click **Add** button.</span></span> <span data-ttu-id="231a5-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="231a5-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="231a5-247">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="231a5-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="231a5-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="231a5-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="231a5-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="231a5-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="231a5-250">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="231a5-250">Test single sign-on</span></span>

<span data-ttu-id="231a5-251">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="231a5-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="231a5-252">Quando si fa clic sul riquadro Mimecast Admin Console nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="231a5-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="231a5-253">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="231a5-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="231a5-254">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="231a5-254">Additional resources</span></span>

* [<span data-ttu-id="231a5-255">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="231a5-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="231a5-256">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="231a5-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png


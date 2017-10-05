---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mimecast Personal Portal | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Mimecast Personal Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="3ac7d-103">Esercitazione: Integrazione di Azure Active Directory con Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="3ac7d-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="3ac7d-104">Questa esercitazione descrive come integrare Mimecast Personal Portal con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ac7d-105">L'integrazione di Mimecast Personal Portal con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ac7d-106">È possibile controllare in Azure AD chi può accedere a Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="3ac7d-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="3ac7d-107">È possibile abilitare gli utenti per l'accesso automatico a Mimecast Personal Portal (Single Sign-On) con gli account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ac7d-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ac7d-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ac7d-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ac7d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3ac7d-110">Prerequisites</span></span>

<span data-ttu-id="3ac7d-111">Per configurare l'integrazione di Azure AD con Mimecast Personal Portal, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="3ac7d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ac7d-113">Sottoscrizione di Mimecast Personal Portal abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3ac7d-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ac7d-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ac7d-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ac7d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ac7d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ac7d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3ac7d-118">Scenario description</span></span>
<span data-ttu-id="3ac7d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ac7d-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ac7d-121">Aggiunta di Mimecast Personal Portal dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3ac7d-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="3ac7d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ac7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="3ac7d-123">Aggiunta di Mimecast Personal Portal dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3ac7d-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="3ac7d-124">Per configurare l'integrazione di Mimecast Personal Portal in Azure AD, è necessario aggiungere Mimecast Personal Portal dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ac7d-125">**Per aggiungere Mimecast Personal Portal dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ac7d-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ac7d-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ac7d-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ac7d-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="3ac7d-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="3ac7d-133">Nella casella di ricerca digitare **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="3ac7d-135">Nel pannello dei risultati selezionare **Mimecast Personal Portal** e quindi fare clic su **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ac7d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ac7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ac7d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mimecast Personal Portal con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ac7d-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ac7d-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di Mimecast Personal Portal corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="3ac7d-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="3ac7d-141">Per stabilire la relazione di collegamento, in Mimecast Personal Portal assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ac7d-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Mimecast Personal Portal, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ac7d-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ac7d-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ac7d-145">**[Creazione di un utente test di Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)** : per avere una controparte di Britta Simon in Mimecast Personal Portal collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ac7d-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ac7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ac7d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ac7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ac7d-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="3ac7d-150">**Per configurare l'accesso Single Sign-On di Azure AD con Mimecast Personal Portal, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ac7d-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="3ac7d-151">Nella pagina di integrazione dell'applicazione **Mimecast Personal Portal** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3ac7d-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="3ac7d-155">Nella sezione **URL e dominio Mimecast Personal Portal** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="3ac7d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-157">a.</span></span> <span data-ttu-id="3ac7d-158">Nella casella di testo **URL di accesso** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="3ac7d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-159">b.</span></span> <span data-ttu-id="3ac7d-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="3ac7d-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="3ac7d-161">These values are not real.</span></span> <span data-ttu-id="3ac7d-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3ac7d-163">Per ottenere questi valori, contattare il [team di supporto clienti di Mimecast Personal Portal](https://www.mimecast.com/customer-success/technical-support/).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="3ac7d-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="3ac7d-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3ac7d-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ac7d-168">Nella sezione **Configurazione di Mimecast Personal Portal** fare clic su **Configura Mimecast Personal Portal** per visualizzare la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3ac7d-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="3ac7d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="3ac7d-171">In un'altra finestra del Web browser accedere a Mimecast Personal Portal come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="3ac7d-172">Passare a **Services (Servizi) \> Applications (Applicazioni)**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="3ac7d-173">![Applicazioni](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="3ac7d-174">Fare clic su **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="3ac7d-175">![Profili di autenticazione](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Profili di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="3ac7d-176">Fare clic su **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="3ac7d-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="3ac7d-178">Nella sezione **Authentication Profile** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3ac7d-179">![Profilo di autenticazione](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Profilo di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="3ac7d-180">a.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-180">a.</span></span> <span data-ttu-id="3ac7d-181">Nella casella di testo **Description** digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="3ac7d-182">b.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-182">b.</span></span> <span data-ttu-id="3ac7d-183">Selezionare **Enforce SAML Authentication for Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="3ac7d-184">c.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-184">c.</span></span> <span data-ttu-id="3ac7d-185">Come **Provider** selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="3ac7d-186">d.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-186">d.</span></span> <span data-ttu-id="3ac7d-187">Nella casella di testo **Issuer URL** (URL autorità emittente) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="3ac7d-188">e.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-188">e.</span></span> <span data-ttu-id="3ac7d-189">Nella casella di testo **URL di accesso** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="3ac7d-190">f.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-190">f.</span></span> <span data-ttu-id="3ac7d-191">Nella casella di testo **Logout URL** (URL di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3ac7d-192">g.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-192">g.</span></span> <span data-ttu-id="3ac7d-193">Aprire nel Blocco note il certificato con codifica **Base 64** scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Identity Provider Certificate (Metadata)** (Certificato provider di identità (metadati)).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="3ac7d-194">h.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-194">h.</span></span> <span data-ttu-id="3ac7d-195">Selezionare **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="3ac7d-196">i.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-196">i.</span></span> <span data-ttu-id="3ac7d-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3ac7d-198">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ac7d-199">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ac7d-200">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ac7d-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ac7d-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ac7d-202">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="3ac7d-204">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ac7d-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ac7d-205">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ac7d-207">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ac7d-209">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ac7d-211">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ac7d-213">a.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-213">a.</span></span> <span data-ttu-id="3ac7d-214">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ac7d-215">b.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-215">b.</span></span> <span data-ttu-id="3ac7d-216">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ac7d-217">c.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-217">c.</span></span> <span data-ttu-id="3ac7d-218">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ac7d-219">d.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-219">d.</span></span> <span data-ttu-id="3ac7d-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="3ac7d-221">Creazione di un utente test di Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="3ac7d-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="3ac7d-222">Per consentire agli utenti di Azure AD di accedere a Mimecast Personal Portal, è necessario eseguirne il provisioning in Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="3ac7d-223">Nel caso di Mimecast Personal Portal, il provisioning è un’attività manuale.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="3ac7d-224">Per poter creare gli utenti è necessario registrare un dominio.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="3ac7d-225">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ac7d-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="3ac7d-226">Accedere a **Mimecast Personal Portal** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="3ac7d-227">Accedere a **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="3ac7d-228">![Directory](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directory")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="3ac7d-229">Fare clic su **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="3ac7d-230">![Registra nuovo dominio](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Registra nuovo dominio")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="3ac7d-231">Dopo aver creato il nuovo dominio, fare clic su **New Address**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="3ac7d-232">![Nuovo indirizzo](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Nuovo indirizzo")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="3ac7d-233">Nella finestra di dialogo del nuovo indirizzo eseguire i passaggi seguenti per un account Azure AD valido di cui si vuole eseguire il provisioning:</span><span class="sxs-lookup"><span data-stu-id="3ac7d-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="3ac7d-234">![Salvare](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Salvare")</span><span class="sxs-lookup"><span data-stu-id="3ac7d-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="3ac7d-235">a.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-235">a.</span></span> <span data-ttu-id="3ac7d-236">Nella casella di testo **Indirizzo di posta elettronica** digitare l'**indirizzo di posta elettronica** dell'utente **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="3ac7d-237">b.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-237">b.</span></span> <span data-ttu-id="3ac7d-238">Nella casella di testo **Global Name** (Nome globale) digitare il **nome utente** **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="3ac7d-239">c.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-239">c.</span></span> <span data-ttu-id="3ac7d-240">Nelle caselle di testo **Password** e **Conferma password** digitare la **password** dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="3ac7d-241">b.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-241">b.</span></span> <span data-ttu-id="3ac7d-242">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="3ac7d-243">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerta da Mimecast Personal Portal per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ac7d-244">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ac7d-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ac7d-245">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3ac7d-247">**Per assegnare Britta Simon a Mimecast Personal Portal, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ac7d-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="3ac7d-248">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3ac7d-250">Nell'elenco di applicazioni selezionare **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="3ac7d-252">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="3ac7d-254">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-254">Click **Add** button.</span></span> <span data-ttu-id="3ac7d-255">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="3ac7d-257">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ac7d-258">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ac7d-259">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ac7d-260">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3ac7d-260">Testing single sign-on</span></span>
<span data-ttu-id="3ac7d-261">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ac7d-262">Quando si fa clic sul riquadro Mimecast Personal Portal nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="3ac7d-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="3ac7d-263">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ac7d-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ac7d-264">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3ac7d-264">Additional resources</span></span>

* [<span data-ttu-id="3ac7d-265">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ac7d-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ac7d-266">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ac7d-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con SkyDesk Email | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SkyDesk Email.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 0ffcca4161fc836192fc9c9871a905f36ea76b32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="4c025-103">Esercitazione: Integrazione di Azure Active Directory con SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="4c025-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="4c025-104">Questa esercitazione descrive come integrare SkyDesk Email con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c025-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c025-105">L'integrazione di SkyDesk Email con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c025-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c025-106">È possibile controllare in Azure AD chi può accedere a SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="4c025-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="4c025-107">È possibile abilitare gli utenti per l'accesso automatico a SkyDesk Email (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c025-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c025-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c025-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c025-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c025-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c025-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4c025-110">Prerequisites</span></span>

<span data-ttu-id="4c025-111">Per configurare l'integrazione di Azure AD con SkyDesk Email, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c025-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="4c025-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c025-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c025-113">Sottoscrizione di SkyDesk Email abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c025-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c025-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4c025-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c025-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c025-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c025-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4c025-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c025-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c025-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c025-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4c025-118">Scenario description</span></span>
<span data-ttu-id="4c025-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4c025-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c025-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c025-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c025-121">Aggiunta di SkyDesk Email dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4c025-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="4c025-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c025-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="4c025-123">Aggiunta di SkyDesk Email dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4c025-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="4c025-124">Per configurare l'integrazione di SkyDesk Email in Azure AD, è necessario aggiungere SkyDesk Email dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4c025-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c025-125">**Per aggiungere SkyDesk Email dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c025-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c025-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4c025-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c025-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4c025-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c025-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c025-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4c025-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c025-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4c025-133">Nella casella di ricerca digitare **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="4c025-133">In the search box, type **SkyDesk Email**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="4c025-135">Nel pannello dei risultati selezionare **SkyDesk Email** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c025-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c025-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c025-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c025-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SkyDesk Email con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c025-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c025-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SkyDesk Email che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c025-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="4c025-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="4c025-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="4c025-141">Per stabilire la relazione di collegamento, in SkyDesk Email assegnare il valore di **nome utente** di Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="4c025-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c025-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SkyDesk Email, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c025-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c025-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4c025-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c025-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c025-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c025-145">**[Creazione di un utente di test di SkyDesk Email](#creating-a-skydesk-email-test-user)**: per avere una controparte di Britta Simon in SkyDesk Email che sia collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c025-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c025-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c025-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c025-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="4c025-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c025-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c025-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c025-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="4c025-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="4c025-150">**Per configurare l'accesso Single Sign-On di Azure AD con SkyDesk Email, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c025-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="4c025-151">Nella pagina di integrazione dell'applicazione **SkyDesk Email** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4c025-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4c025-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4c025-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="4c025-155">Nella sezione **URL e dominio SkyDesk Email** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c025-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="4c025-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4c025-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c025-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="4c025-158">The value is not real.</span></span> <span data-ttu-id="4c025-159">aggiornarlo con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="4c025-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="4c025-160">Per ottenere il valore, contattare il [team di supporto client di SkyDesk Email](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="4c025-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
4. <span data-ttu-id="4c025-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="4c025-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="4c025-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4c025-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c025-165">Nella sezione **Configurazione di SkyDesk Email** scegliere **Configura SkyDesk Email** per aprire la finestra di dialogo **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="4c025-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4c025-166">Copiare **l'URL di disconnessione e l'URL servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="4c025-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="4c025-168">Per abilitare SSO in **SkyDesk Email**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c025-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="4c025-169">a.</span><span class="sxs-lookup"><span data-stu-id="4c025-169">a.</span></span> <span data-ttu-id="4c025-170">Accedere al proprio account SkyDesk Email come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4c025-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="4c025-171">b.</span><span class="sxs-lookup"><span data-stu-id="4c025-171">b.</span></span> <span data-ttu-id="4c025-172">Nel menu in alto fare clic su **Configura** e quindi fare clic selezionare **Org**.</span><span class="sxs-lookup"><span data-stu-id="4c025-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="4c025-174">c.</span><span class="sxs-lookup"><span data-stu-id="4c025-174">c.</span></span> <span data-ttu-id="4c025-175">Nel pannello sinistro selezionare **Domini**.</span><span class="sxs-lookup"><span data-stu-id="4c025-175">Click on **Domains** from the left panel.</span></span>
    
      ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="4c025-177">d.</span><span class="sxs-lookup"><span data-stu-id="4c025-177">d.</span></span> <span data-ttu-id="4c025-178">Fare clic su **Aggiungi dominio**.</span><span class="sxs-lookup"><span data-stu-id="4c025-178">Click on **Add Domain**.</span></span>
    
      ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="4c025-180">e.</span><span class="sxs-lookup"><span data-stu-id="4c025-180">e.</span></span> <span data-ttu-id="4c025-181">Immettere il nome di dominio e quindi verificarlo.</span><span class="sxs-lookup"><span data-stu-id="4c025-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="4c025-183">f.</span><span class="sxs-lookup"><span data-stu-id="4c025-183">f.</span></span> <span data-ttu-id="4c025-184">Nel pannello di sinistra fare clic su **SAML Authentication** (Autenticazione SAML).</span><span class="sxs-lookup"><span data-stu-id="4c025-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="4c025-186">Nella pagina della finestra di dialogo **SAML Authentication** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c025-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="4c025-188">Per usare l'autenticazione basata su SAML, è necessario che il **dominio sia verificato** e l'**URL del portale** sia impostato.</span><span class="sxs-lookup"><span data-stu-id="4c025-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="4c025-189">È possibile impostare l'URL del portale usando un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="4c025-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="4c025-191">a.</span><span class="sxs-lookup"><span data-stu-id="4c025-191">a.</span></span> <span data-ttu-id="4c025-192">Nella casella di testo **Login URL** (URL di accesso) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c025-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="4c025-193">b.</span><span class="sxs-lookup"><span data-stu-id="4c025-193">b.</span></span> <span data-ttu-id="4c025-194">Nella casella di testo **URL di disconnessione** incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c025-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4c025-195">c.</span><span class="sxs-lookup"><span data-stu-id="4c025-195">c.</span></span> <span data-ttu-id="4c025-196">**Modifica URL password** è facoltativo e può essere lasciato vuoto.</span><span class="sxs-lookup"><span data-stu-id="4c025-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="4c025-197">d.</span><span class="sxs-lookup"><span data-stu-id="4c025-197">d.</span></span> <span data-ttu-id="4c025-198">Fare clic su **Get Key From File** (Ottieni chiave da file) per selezionare il certificato scaricato dal portale di Azure e quindi fare clic su **Apri** per caricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="4c025-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="4c025-199">e.</span><span class="sxs-lookup"><span data-stu-id="4c025-199">e.</span></span> <span data-ttu-id="4c025-200">In **Algorithm** (Algoritmo) selezionare **RSA**.</span><span class="sxs-lookup"><span data-stu-id="4c025-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="4c025-201">f.</span><span class="sxs-lookup"><span data-stu-id="4c025-201">f.</span></span> <span data-ttu-id="4c025-202">Fare clic su **Ok** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="4c025-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="4c025-203">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="4c025-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c025-204">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="4c025-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c025-205">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c025-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c025-206">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c025-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c025-207">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c025-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4c025-209">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4c025-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c025-210">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4c025-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c025-212">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="4c025-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c025-214">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="4c025-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c025-216">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c025-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c025-218">a.</span><span class="sxs-lookup"><span data-stu-id="4c025-218">a.</span></span> <span data-ttu-id="4c025-219">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c025-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c025-220">b.</span><span class="sxs-lookup"><span data-stu-id="4c025-220">b.</span></span> <span data-ttu-id="4c025-221">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c025-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c025-222">c.</span><span class="sxs-lookup"><span data-stu-id="4c025-222">c.</span></span> <span data-ttu-id="4c025-223">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="4c025-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c025-224">d.</span><span class="sxs-lookup"><span data-stu-id="4c025-224">d.</span></span> <span data-ttu-id="4c025-225">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4c025-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="4c025-226">Creazione di un utente di test di SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="4c025-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="4c025-227">In questa sezione si crea un utente di nome Britta Simon in SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="4c025-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="4c025-228">Fare clic su **User Access** (Accesso utente) nel pannello di sinistra di SkyDesk Email e quindi immettere il proprio nome utente.</span><span class="sxs-lookup"><span data-stu-id="4c025-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="4c025-230">Per creare utenti in blocco, è necessario contattare il [team di supporto client di SkyDesk Email](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="4c025-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c025-231">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c025-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c025-232">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="4c025-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4c025-234">**Per assegnare Britta Simon a SkyDesk Email, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c025-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="4c025-235">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c025-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4c025-237">Nell'elenco delle applicazioni selezionare **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="4c025-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="4c025-239">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4c025-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4c025-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4c025-241">Click **Add** button.</span></span> <span data-ttu-id="4c025-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4c025-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4c025-244">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="4c025-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c025-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4c025-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c025-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4c025-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c025-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c025-247">Testing single sign-on</span></span>

<span data-ttu-id="4c025-248">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4c025-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4c025-249">Quando si fa clic sul riquadro SkyDesk Email nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="4c025-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c025-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4c025-250">Additional resources</span></span>

* [<span data-ttu-id="4c025-251">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c025-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c025-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c025-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png


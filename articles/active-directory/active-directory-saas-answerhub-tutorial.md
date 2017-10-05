---
title: 'Esercitazione: Integrazione di Azure Active Directory con AnswerHub | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e AnswerHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="f33e0-103">Esercitazione: Integrazione di Azure Active Directory con AnswerHub</span><span class="sxs-lookup"><span data-stu-id="f33e0-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="f33e0-104">Questa esercitazione descrive come integrare AnswerHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f33e0-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f33e0-105">L'integrazione di AnswerHub con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f33e0-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f33e0-106">È possibile controllare in Azure AD chi può accedere ad AnswerHub</span><span class="sxs-lookup"><span data-stu-id="f33e0-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="f33e0-107">È possibile abilitare gli utenti per l'accesso automatico ad AnswerHub (Single Sign-On) con gli Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="f33e0-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f33e0-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33e0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f33e0-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f33e0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f33e0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f33e0-110">Prerequisites</span></span>

<span data-ttu-id="f33e0-111">Per configurare l'integrazione di Azure AD con AnswerHub, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f33e0-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="f33e0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f33e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f33e0-113">Sottoscrizione di AnswerHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f33e0-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f33e0-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f33e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f33e0-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f33e0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f33e0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f33e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f33e0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f33e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f33e0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f33e0-118">Scenario description</span></span>
<span data-ttu-id="f33e0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f33e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f33e0-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f33e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f33e0-121">Aggiunta di AnswerHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f33e0-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="f33e0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="f33e0-123">Aggiunta di AnswerHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f33e0-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="f33e0-124">Per configurare l'integrazione di AnswerHub in Azure AD, è necessario aggiungere AnswerHub dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f33e0-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f33e0-125">**Per aggiungere AnswerHub dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f33e0-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f33e0-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f33e0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f33e0-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f33e0-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f33e0-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f33e0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f33e0-133">Nella casella di ricerca digitare **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-133">In the search box, type **AnswerHub**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="f33e0-135">Nel pannello dei risultati selezionare **AnswerHub** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f33e0-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f33e0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33e0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f33e0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con AnswerHub usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f33e0-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f33e0-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di AnswerHub corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f33e0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="f33e0-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="f33e0-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="f33e0-141">Per stabilire la relazione di collegamento, in AnswerHub assegnare il valore del **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="f33e0-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f33e0-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con AnswerHub, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="f33e0-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f33e0-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f33e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f33e0-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f33e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f33e0-145">**[Creazione di un utente di test di AnswerHub](#creating-an-answerhub-test-user)**: per avere una controparte di Britta Simon in AnswerHub collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f33e0-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f33e0-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f33e0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f33e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f33e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f33e0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f33e0-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="f33e0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="f33e0-150">**Per configurare l'accesso Single Sign-On di Azure AD con AnswerHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f33e0-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="f33e0-151">Nella pagina di integrazione dell'applicazione **AnswerHub** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f33e0-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f33e0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="f33e0-155">Nella sezione **URL e dominio AnswerHub** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f33e0-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="f33e0-157">a.</span><span class="sxs-lookup"><span data-stu-id="f33e0-157">a.</span></span> <span data-ttu-id="f33e0-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company>.answerhub.com`.</span><span class="sxs-lookup"><span data-stu-id="f33e0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="f33e0-159">b.</span><span class="sxs-lookup"><span data-stu-id="f33e0-159">b.</span></span> <span data-ttu-id="f33e0-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="f33e0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f33e0-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f33e0-161">These values are not real.</span></span> <span data-ttu-id="f33e0-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="f33e0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f33e0-163">Per ottenere questi valori, contattare il [team di supporto clienti di AnswerHub](mailto:success@answerhub.com).</span><span class="sxs-lookup"><span data-stu-id="f33e0-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="f33e0-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="f33e0-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="f33e0-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f33e0-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f33e0-168">Nella sezione **Configurazione di AnswerHub** fare clic su **Configura AnswerHub** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f33e0-169">Copiare l'**URL di disconnessione e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="f33e0-171">In un'altra finestra del Web browser accedere al sito aziendale di AnswerHub come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f33e0-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="f33e0-172">Per ottenere assistenza nella configurazione di AnswerHub, contattare il [team di supporto di AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="f33e0-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="f33e0-173">Passare a **Administration**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="f33e0-174">Fare clic sulla scheda **User and Group** .</span><span class="sxs-lookup"><span data-stu-id="f33e0-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="f33e0-175">Nel riquadro di spostamento a sinistra passare alla sezione **Social Settings** e fare clic su **SAML Setup**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="f33e0-176">Fare clic sulla scheda **IDP Config** .</span><span class="sxs-lookup"><span data-stu-id="f33e0-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="f33e0-177">Nella scheda **IDP Config** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f33e0-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="f33e0-178">![Configurazione SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="f33e0-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="f33e0-179">a.</span><span class="sxs-lookup"><span data-stu-id="f33e0-179">a.</span></span> <span data-ttu-id="f33e0-180">Nella casella di testo **IDP Login URL** (URL di accesso IdP) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33e0-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="f33e0-181">b.</span><span class="sxs-lookup"><span data-stu-id="f33e0-181">b.</span></span> <span data-ttu-id="f33e0-182">Nella casella di testo **IDP Logout URL** (URL di disconnessione IdP) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33e0-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="f33e0-183">c.</span><span class="sxs-lookup"><span data-stu-id="f33e0-183">c.</span></span> <span data-ttu-id="f33e0-184">Nella casella di testo **IDP Name Identifier Format** (Formato identificatore nome IdP) immettere lo stesso valore di ID utente selezionato nella sezione **Attributi utente** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33e0-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="f33e0-185">d.</span><span class="sxs-lookup"><span data-stu-id="f33e0-185">d.</span></span> <span data-ttu-id="f33e0-186">Fare clic su **Keys and Certificates**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="f33e0-187">Nella scheda Keys and Certificates seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f33e0-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="f33e0-188">![Chiavi e certificati](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Chiavi e certificati")</span><span class="sxs-lookup"><span data-stu-id="f33e0-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="f33e0-189">a.</span><span class="sxs-lookup"><span data-stu-id="f33e0-189">a.</span></span> <span data-ttu-id="f33e0-190">Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **IDP Public Key (x509 Format)** (Chiave pubblica IdP (formato x509)).</span><span class="sxs-lookup"><span data-stu-id="f33e0-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="f33e0-191">b.</span><span class="sxs-lookup"><span data-stu-id="f33e0-191">b.</span></span> <span data-ttu-id="f33e0-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-192">Click **Save**.</span></span>

14. <span data-ttu-id="f33e0-193">Nella scheda **IDP Config** fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f33e0-194">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f33e0-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f33e0-195">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f33e0-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f33e0-196">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f33e0-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f33e0-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33e0-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f33e0-198">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f33e0-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f33e0-200">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f33e0-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f33e0-201">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f33e0-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f33e0-203">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f33e0-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f33e0-205">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f33e0-207">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f33e0-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f33e0-209">a.</span><span class="sxs-lookup"><span data-stu-id="f33e0-209">a.</span></span> <span data-ttu-id="f33e0-210">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f33e0-211">b.</span><span class="sxs-lookup"><span data-stu-id="f33e0-211">b.</span></span> <span data-ttu-id="f33e0-212">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f33e0-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f33e0-213">c.</span><span class="sxs-lookup"><span data-stu-id="f33e0-213">c.</span></span> <span data-ttu-id="f33e0-214">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f33e0-215">d.</span><span class="sxs-lookup"><span data-stu-id="f33e0-215">d.</span></span> <span data-ttu-id="f33e0-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="f33e0-217">Creazione di un utente di test di AnswerHub</span><span class="sxs-lookup"><span data-stu-id="f33e0-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="f33e0-218">Per consentire agli utenti di Azure AD di accedere ad AnswerHub, è necessario effettuarne il provisioning in AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="f33e0-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="f33e0-219">Nel caso di AnswerHub, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f33e0-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="f33e0-220">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f33e0-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f33e0-221">Accedere al sito aziendale di **AnswerHub** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f33e0-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="f33e0-222">Passare a **Administration**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="f33e0-223">Fare clic sulla scheda **Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="f33e0-224">Nel riquadro di spostamento a sinistra fare clic su **Create or import users** nella sezione **Manage users**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="f33e0-225">![Utenti e gruppi](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Utenti e gruppi")</span><span class="sxs-lookup"><span data-stu-id="f33e0-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="f33e0-226">Nelle caselle di testo **Email address**, **Username** e **Password** digitare l'indirizzo di posta elettronica, il nome utente e la password di un account utente Azure Active Directory valido di cui si vuole eseguire il provisioning e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="f33e0-227">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da AnswerHub per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f33e0-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f33e0-228">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f33e0-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f33e0-229">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="f33e0-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f33e0-231">**Per assegnare Britta Simon ad AnswerHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f33e0-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="f33e0-232">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f33e0-234">Nell'elenco delle applicazioni selezionare **Autotask**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-234">In the applications list, select **AnswerHub**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="f33e0-236">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f33e0-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f33e0-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-238">Click **Add** button.</span></span> <span data-ttu-id="f33e0-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f33e0-241">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f33e0-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f33e0-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f33e0-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f33e0-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f33e0-244">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f33e0-244">Testing single sign-on</span></span>

<span data-ttu-id="f33e0-245">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f33e0-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f33e0-246">Quando si fa clic sul riquadro AnswerHub nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="f33e0-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="f33e0-247">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f33e0-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f33e0-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f33e0-248">Additional resources</span></span>

* [<span data-ttu-id="f33e0-249">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f33e0-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f33e0-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f33e0-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png


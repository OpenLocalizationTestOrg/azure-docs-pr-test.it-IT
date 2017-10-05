---
title: 'Esercitazione: Integrazione di Azure Active Directory con Promapp | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Promapp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="95d34-103">Esercitazione: Integrazione di Azure Active Directory con Promapp</span><span class="sxs-lookup"><span data-stu-id="95d34-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="95d34-104">Questa esercitazione descrive come integrare Promapp con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95d34-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95d34-105">L'integrazione di Promapp con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="95d34-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="95d34-106">È possibile controllare in Azure AD chi può accedere a Promapp</span><span class="sxs-lookup"><span data-stu-id="95d34-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="95d34-107">È possibile abilitare gli utenti per l'accesso automatico a Promapp (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d34-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="95d34-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="95d34-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="95d34-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95d34-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95d34-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="95d34-110">Prerequisites</span></span>

<span data-ttu-id="95d34-111">Per configurare l'integrazione di Azure AD con Promapp, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="95d34-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="95d34-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95d34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95d34-113">Sottoscrizione di Promapp abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="95d34-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95d34-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="95d34-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95d34-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="95d34-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95d34-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="95d34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95d34-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95d34-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95d34-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="95d34-118">Scenario description</span></span>
<span data-ttu-id="95d34-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="95d34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95d34-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="95d34-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95d34-121">Aggiunta di Promapp dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="95d34-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="95d34-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="95d34-123">Aggiunta di Promapp dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="95d34-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="95d34-124">Per configurare l'integrazione di Promapp in Azure AD, è necessario aggiungere Promapp dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="95d34-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="95d34-125">**Per aggiungere Promapp dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="95d34-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="95d34-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="95d34-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="95d34-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="95d34-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="95d34-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="95d34-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="95d34-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="95d34-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="95d34-133">Nella casella di ricerca digitare **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="95d34-133">In the search box, type **Promapp**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="95d34-135">Nel pannello dei risultati selezionare **Promapp** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="95d34-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95d34-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d34-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95d34-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Promapp in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="95d34-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95d34-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Promapp che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95d34-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="95d34-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Promapp.</span><span class="sxs-lookup"><span data-stu-id="95d34-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="95d34-141">Per stabilire la relazione di collegamento, in Promapp assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="95d34-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="95d34-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Promapp, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="95d34-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="95d34-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="95d34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="95d34-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95d34-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95d34-145">**[Creazione di un utente test per Promapp](#creating-a-promapp-test-user)** : per avere una controparte di Britta Simon in Promapp collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95d34-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="95d34-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95d34-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95d34-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="95d34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="95d34-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d34-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="95d34-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso all'applicazione Promapp.</span><span class="sxs-lookup"><span data-stu-id="95d34-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="95d34-150">**Per configurare l'accesso Single Sign-On di Azure AD con Promapp, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="95d34-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="95d34-151">Nella pagina di integrazione dell'applicazione **Promapp** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="95d34-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="95d34-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="95d34-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="95d34-155">Nella sezione **Promapp Domain and URLs** (URL e dominio Promapp) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="95d34-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="95d34-157">a.</span><span class="sxs-lookup"><span data-stu-id="95d34-157">a.</span></span> <span data-ttu-id="95d34-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`.</span><span class="sxs-lookup"><span data-stu-id="95d34-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="95d34-159">b.</span><span class="sxs-lookup"><span data-stu-id="95d34-159">b.</span></span> <span data-ttu-id="95d34-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="95d34-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="95d34-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="95d34-161">These values are not real.</span></span> <span data-ttu-id="95d34-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="95d34-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="95d34-163">Per ottenere questi valori, contattare il [team di supporto clienti di Promapp](https://www.promapp.com/about-us/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="95d34-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="95d34-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="95d34-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="95d34-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="95d34-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="95d34-168">Nella sezione **Promapp Configuration** (Configurazione di Promapp) fare clic su **Configure Promapp** (Configura Promapp) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="95d34-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="95d34-169">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="95d34-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="95d34-171">Accedere al sito aziendale di Promapp come amministratore.</span><span class="sxs-lookup"><span data-stu-id="95d34-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="95d34-172">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="95d34-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Accesso Single Sign-On di Azure AD][12]

9. <span data-ttu-id="95d34-174">Fare clic su **Configure**.</span><span class="sxs-lookup"><span data-stu-id="95d34-174">Click **Configure**.</span></span> 
   
    ![Accesso Single Sign-On di Azure AD][13]

10. <span data-ttu-id="95d34-176">Nella finestra di dialogo **Security** (Sicurezza) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="95d34-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Accesso Single Sign-On di Azure AD][14]
    
    <span data-ttu-id="95d34-178">a.</span><span class="sxs-lookup"><span data-stu-id="95d34-178">a.</span></span> <span data-ttu-id="95d34-179">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **SSO-Login URL** (URL di accesso SSO).</span><span class="sxs-lookup"><span data-stu-id="95d34-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="95d34-180">b.</span><span class="sxs-lookup"><span data-stu-id="95d34-180">b.</span></span> <span data-ttu-id="95d34-181">Per **SSO - Single Sign-on Mode** selezionare **Optional** e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="95d34-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="95d34-182">c.</span><span class="sxs-lookup"><span data-stu-id="95d34-182">c.</span></span> <span data-ttu-id="95d34-183">Aprire il certificato scaricato nel Blocco note, copiare il contenuto del certificato senza la prima riga (-----BEGIN CERTIFICATE-----) e l'ultima riga (-----END CERTIFICATE-----), incollarlo nella casella di testo **SSO-x.509 Certificate** (Certificato SSO-x.509) e quindi fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="95d34-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="95d34-184">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="95d34-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="95d34-185">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="95d34-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="95d34-186">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95d34-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95d34-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d34-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="95d34-188">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="95d34-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="95d34-190">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="95d34-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="95d34-191">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="95d34-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="95d34-193">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="95d34-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="95d34-195">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="95d34-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95d34-197">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="95d34-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="95d34-199">a.</span><span class="sxs-lookup"><span data-stu-id="95d34-199">a.</span></span> <span data-ttu-id="95d34-200">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95d34-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95d34-201">b.</span><span class="sxs-lookup"><span data-stu-id="95d34-201">b.</span></span> <span data-ttu-id="95d34-202">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="95d34-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="95d34-203">c.</span><span class="sxs-lookup"><span data-stu-id="95d34-203">c.</span></span> <span data-ttu-id="95d34-204">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="95d34-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="95d34-205">d.</span><span class="sxs-lookup"><span data-stu-id="95d34-205">d.</span></span> <span data-ttu-id="95d34-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="95d34-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="95d34-207">Creazione di un utente test per Promapp</span><span class="sxs-lookup"><span data-stu-id="95d34-207">Creating a Promapp test user</span></span>

<span data-ttu-id="95d34-208">L'applicazione Promapp supporta il provisioning JIT (just-in-time).</span><span class="sxs-lookup"><span data-stu-id="95d34-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="95d34-209">Questo significa che, se necessario, un account utente viene creato automaticamente durante il tentativo di accedere all'applicazione tramite il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="95d34-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="95d34-210">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="95d34-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="95d34-211">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Promapp.</span><span class="sxs-lookup"><span data-stu-id="95d34-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Assegna utente][200] 

<span data-ttu-id="95d34-213">**Per assegnare Britta Simon a Promapp, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="95d34-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="95d34-214">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="95d34-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="95d34-216">Nell'elenco di applicazioni selezionare **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="95d34-216">In the applications list, select **Promapp**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="95d34-218">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="95d34-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="95d34-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="95d34-220">Click **Add** button.</span></span> <span data-ttu-id="95d34-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="95d34-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="95d34-223">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="95d34-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="95d34-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="95d34-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95d34-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="95d34-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="95d34-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="95d34-226">Testing single sign-on</span></span>

<span data-ttu-id="95d34-227">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="95d34-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="95d34-228">Quando si fa clic sul riquadro Promapp nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Promapp.</span><span class="sxs-lookup"><span data-stu-id="95d34-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95d34-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="95d34-229">Additional resources</span></span>

* [<span data-ttu-id="95d34-230">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95d34-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95d34-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95d34-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png


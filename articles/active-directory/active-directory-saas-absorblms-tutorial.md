---
title: 'Esercitazione: Integrazione di Azure Active Directory con Absorb LMS | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Absorb LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="9ce74-103">Esercitazione: Integrazione di Azure Active Directory con Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="9ce74-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="9ce74-104">Questa esercitazione descrive come integrare Absorb LMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ce74-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ce74-105">L'integrazione di Absorb LMS con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ce74-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9ce74-106">È possibile controllare in Azure AD chi può accedere ad Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9ce74-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="9ce74-107">È possibile abilitare gli utenti per l'accesso automatico a Absorb LMS (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ce74-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ce74-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce74-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9ce74-109">Per altre informazioni sull'integrazione di app SaaS con Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="9ce74-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9ce74-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ce74-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ce74-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9ce74-111">Prerequisites</span></span>

<span data-ttu-id="9ce74-112">Per configurare l'integrazione di Azure AD con Absorb LMS, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ce74-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="9ce74-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ce74-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9ce74-114">Sottoscrizione di Absorb LMS abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9ce74-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ce74-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9ce74-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ce74-116">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ce74-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ce74-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9ce74-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ce74-118">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ce74-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ce74-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9ce74-119">Scenario description</span></span>
<span data-ttu-id="9ce74-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9ce74-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ce74-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ce74-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ce74-122">Aggiunta di Absorb LMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9ce74-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="9ce74-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ce74-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="9ce74-124">Aggiunta di Absorb LMS dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9ce74-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="9ce74-125">Per configurare l'integrazione di Absorb LMS in Azure AD, è necessario aggiungere Absorb LMS dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9ce74-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9ce74-126">**Per aggiungere Absorb LMS dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9ce74-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9ce74-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9ce74-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="9ce74-129">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9ce74-130">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-130">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="9ce74-132">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ce74-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="9ce74-134">Nella casella di ricerca digitare **Absorb LMS**, selezionare **Absorb LMS** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9ce74-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![Absorb LMS nell'elenco risultati](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9ce74-136">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ce74-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9ce74-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Absorb LMS usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9ce74-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9ce74-138">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Absorb LMS che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ce74-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="9ce74-139">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9ce74-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="9ce74-140">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore dell'attributo **Username** in Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9ce74-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="9ce74-141">Per configurare e testare l'accesso Single Sign-On di Azure AD con Absorb LMS, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ce74-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9ce74-142">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9ce74-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9ce74-143">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ce74-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ce74-144">**[Creare un utente di test di Absorb LMS](#create-an-absorb-lms-test-user)**: per avere una controparte di Britta Simon in Absorb LMS collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ce74-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ce74-145">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ce74-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ce74-146">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="9ce74-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9ce74-147">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ce74-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9ce74-148">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9ce74-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="9ce74-149">**Per configurare Single Sign-On di Azure AD con Absorb LMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9ce74-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="9ce74-150">Nella pagina di integrazione dell'applicazione **Absorb LMS** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="9ce74-152">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9ce74-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="9ce74-154">Nella sezione **URL e dominio Absorb LMS** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9ce74-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="9ce74-156">a.</span><span class="sxs-lookup"><span data-stu-id="9ce74-156">a.</span></span> <span data-ttu-id="9ce74-157">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="9ce74-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="9ce74-158">b.</span><span class="sxs-lookup"><span data-stu-id="9ce74-158">b.</span></span> <span data-ttu-id="9ce74-159">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="9ce74-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9ce74-160">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="9ce74-160">These values are not the real.</span></span> <span data-ttu-id="9ce74-161">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="9ce74-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9ce74-162">Per ottenere questi valori, contattare il [team di supporto clienti di Absorb LMS](https://www.absorblms.com/support).</span><span class="sxs-lookup"><span data-stu-id="9ce74-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="9ce74-163">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="9ce74-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="9ce74-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9ce74-165">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9ce74-167">Nella sezione **Absorb LMS Configuration** (Configurazione Absorb LMS) fare clic su **Configure Absorb LMS** (Configura Absorb LMS) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9ce74-168">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="9ce74-170">In un'altra finestra del Web browser accedere al sito aziendale di Absorb LMS come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9ce74-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="9ce74-171">Fare clic sull'**icona dell'account** nell'interfaccia di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="9ce74-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="9ce74-173">Fare clic su **Impostazioni portale**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-173">Click **Portal Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="9ce74-175">Fare clic sulla scheda **Utenti** .</span><span class="sxs-lookup"><span data-stu-id="9ce74-175">Click the **Users** tab.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="9ce74-177">Per accedere ai campi di configurazione dell'accesso Single Sign-On, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9ce74-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="9ce74-179">a.</span><span class="sxs-lookup"><span data-stu-id="9ce74-179">a.</span></span> <span data-ttu-id="9ce74-180">Selezionare la **modalità** appropriata.</span><span class="sxs-lookup"><span data-stu-id="9ce74-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="9ce74-181">b.</span><span class="sxs-lookup"><span data-stu-id="9ce74-181">b.</span></span> <span data-ttu-id="9ce74-182">Aprire il certificato scaricato dal portale di Azure nel blocco note, rimuovere i tag **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---** e quindi incollare il contenuto rimanente nella casella di testo **Key** (Chiave).</span><span class="sxs-lookup"><span data-stu-id="9ce74-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="9ce74-183">c.</span><span class="sxs-lookup"><span data-stu-id="9ce74-183">c.</span></span> <span data-ttu-id="9ce74-184">Nel campo **Id Property** (Proprietà ID), selezionare l'attributo appropriato configurato come identificatore utente in Azure AD. Se, ad esempio, in Azure AD è stato selezionato userprinciplename, qui è necessario selezionare Username.</span><span class="sxs-lookup"><span data-stu-id="9ce74-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="9ce74-185">d.</span><span class="sxs-lookup"><span data-stu-id="9ce74-185">d.</span></span> <span data-ttu-id="9ce74-186">Nel campo **Login URL** (URL di accesso), incollare il valore dell'**URL servizio Single Sign-On SAML** copiato in precedenza dalla finestra **Configura accesso** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce74-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="9ce74-187">e.</span><span class="sxs-lookup"><span data-stu-id="9ce74-187">e.</span></span> <span data-ttu-id="9ce74-188">Nel campo **Logout URL** (URL di disconnessione) incollare l'**URL di disconnessione** copiato in precedenza dalla finestra **Configura accesso** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce74-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="9ce74-189">Abilitare **Only Allow SSO Login** (Consenti solo accesso SSO).</span><span class="sxs-lookup"><span data-stu-id="9ce74-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="9ce74-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="9ce74-192">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="9ce74-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9ce74-193">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="9ce74-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9ce74-194">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ce74-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9ce74-195">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ce74-195">Create an Azure AD test user</span></span>

<span data-ttu-id="9ce74-196">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ce74-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="9ce74-198">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9ce74-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9ce74-199">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9ce74-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ce74-201">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="9ce74-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ce74-203">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ce74-205">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9ce74-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ce74-207">a.</span><span class="sxs-lookup"><span data-stu-id="9ce74-207">a.</span></span> <span data-ttu-id="9ce74-208">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ce74-209">b.</span><span class="sxs-lookup"><span data-stu-id="9ce74-209">b.</span></span> <span data-ttu-id="9ce74-210">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9ce74-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ce74-211">c.</span><span class="sxs-lookup"><span data-stu-id="9ce74-211">c.</span></span> <span data-ttu-id="9ce74-212">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9ce74-213">d.</span><span class="sxs-lookup"><span data-stu-id="9ce74-213">d.</span></span> <span data-ttu-id="9ce74-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="9ce74-215">Creare un utente di test di Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="9ce74-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="9ce74-216">Per consentire agli utenti di Azure AD accedere ad Absorb LMS, è necessario eseguire il provisioning dell'account utente in Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9ce74-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="9ce74-217">In Absorb LMS il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="9ce74-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="9ce74-218">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9ce74-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9ce74-219">Accedere al sito aziendale di Absorb LMS come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9ce74-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="9ce74-220">Fare clic sulla scheda **Utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="9ce74-220">Click **Users** tab.</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="9ce74-222">Fare clic su **Utenti** nella scheda **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-222">Click **Users** under the **Users** tab.</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="9ce74-224">Dal menu a discesa **Aggiungi nuovo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-224">Select **User** from **Add New** drop-down.</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="9ce74-226">Nella pagina **Aggiungi utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9ce74-226">On the **Add User** page, perform the following steps:</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="9ce74-228">a.</span><span class="sxs-lookup"><span data-stu-id="9ce74-228">a.</span></span> <span data-ttu-id="9ce74-229">Nella casella di testo **Nome** digitare Britta.</span><span class="sxs-lookup"><span data-stu-id="9ce74-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="9ce74-230">b.</span><span class="sxs-lookup"><span data-stu-id="9ce74-230">b.</span></span> <span data-ttu-id="9ce74-231">Nella casella di testo **Cognome** digitare Simon.</span><span class="sxs-lookup"><span data-stu-id="9ce74-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="9ce74-232">c.</span><span class="sxs-lookup"><span data-stu-id="9ce74-232">c.</span></span> <span data-ttu-id="9ce74-233">Nella casella di testo **Nome utente** digitare Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ce74-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="9ce74-234">d.</span><span class="sxs-lookup"><span data-stu-id="9ce74-234">d.</span></span> <span data-ttu-id="9ce74-235">Nella casella di testo **Password** digitare la password dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ce74-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="9ce74-236">e.</span><span class="sxs-lookup"><span data-stu-id="9ce74-236">e.</span></span> <span data-ttu-id="9ce74-237">Nella casella di testo **Conferma password** digitare di nuovo la stessa password.</span><span class="sxs-lookup"><span data-stu-id="9ce74-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="9ce74-238">f.</span><span class="sxs-lookup"><span data-stu-id="9ce74-238">f.</span></span> <span data-ttu-id="9ce74-239">Rendere la password **attiva**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="9ce74-240">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9ce74-241">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ce74-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="9ce74-242">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9ce74-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![Assegnare il ruolo utente][200]

<span data-ttu-id="9ce74-244">**Per assegnare Britta Simon a Absorb LMS, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9ce74-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="9ce74-245">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9ce74-247">Nell'elenco delle applicazioni, selezionare **Absorb LMS**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-247">In the applications list, select **Absorb LMS**.</span></span>

    ![Collegamento di Absorb LMS nell'elenco delle applicazioni](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="9ce74-249">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9ce74-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202] 

4. <span data-ttu-id="9ce74-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-251">Click **Add** button.</span></span> <span data-ttu-id="9ce74-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="9ce74-254">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="9ce74-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9ce74-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ce74-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9ce74-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9ce74-257">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9ce74-257">Test single sign-on</span></span>

<span data-ttu-id="9ce74-258">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9ce74-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9ce74-259">Quando si fa clic sul riquadro Absorb LMS nel pannello di accesso, si accederà automaticamente all'applicazione Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9ce74-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="9ce74-260">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9ce74-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ce74-261">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9ce74-261">Additional resources</span></span>

* [<span data-ttu-id="9ce74-262">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ce74-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ce74-263">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ce74-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png


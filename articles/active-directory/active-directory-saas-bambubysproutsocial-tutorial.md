---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bambu by Sprout Social | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Bambu by Sprout Social .
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="80395-103">Esercitazione: Integrazione di Azure Active Directory con Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="80395-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="80395-104">Questa esercitazione descrive come integrare Bambu by Sprout Social con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80395-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80395-105">L'integrazione di Bambu by Sprout Social con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="80395-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="80395-106">È possibile controllare in Azure AD chi può accedere a Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="80395-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="80395-107">È possibile abilitare gli utenti per l'accesso automatico a Bambu by Sprout Social (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="80395-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80395-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="80395-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="80395-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80395-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="80395-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="80395-110">Prerequisites</span></span>

<span data-ttu-id="80395-111">Per configurare l'integrazione di Azure AD con Bambu by Sprout Social, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="80395-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="80395-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80395-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80395-113">Sottoscrizione di Bambu by Sprout Social abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="80395-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80395-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="80395-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80395-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="80395-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80395-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="80395-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="80395-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80395-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80395-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="80395-118">Scenario description</span></span>
<span data-ttu-id="80395-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="80395-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80395-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="80395-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80395-121">Aggiungere Bambu by Sprout Social dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="80395-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="80395-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="80395-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="80395-123">Aggiungere Bambu by Sprout Social dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="80395-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="80395-124">Per configurare l'integrazione di Bambu by Sprout Social in Azure AD, è necessario aggiungere Bambu by Sprout Social dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="80395-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="80395-125">**Per aggiungere Bambu by Sprout Social dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="80395-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="80395-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="80395-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80395-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="80395-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="80395-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="80395-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="80395-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="80395-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="80395-133">Digitare **Bambu by Sprout Social** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="80395-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="80395-135">Nel pannello dei risultati selezionare **Bambu by Sprout Social**  e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80395-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80395-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="80395-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80395-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Bambu by Sprout Social usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="80395-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="80395-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Bambu by Sprout Social che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80395-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="80395-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="80395-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="80395-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="80395-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="80395-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Bambu by Sprout Social, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="80395-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="80395-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="80395-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="80395-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80395-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80395-145">**[Creazione di un utente test di Bambu by Sprout Social](#creating-a-bambu-by-sprout-social-test-user)** : per avere una controparte di Britta Simon in Bambu by Sprout Social collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80395-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="80395-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80395-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80395-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="80395-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80395-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="80395-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80395-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="80395-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="80395-150">**Per configurare l'accesso Single Sign-On di Azure AD con Bambu by Sprout Social, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="80395-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="80395-151">Nella pagina di integrazione dell'applicazione **Bambu by Sprout Social** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="80395-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="80395-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="80395-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="80395-155">Nella sezione **URL e dominio Bambu by Sprout Social** l'utente non deve eseguire alcuna operazione perché l'applicazione è già preintegrata in Azure.</span><span class="sxs-lookup"><span data-stu-id="80395-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="80395-157">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="80395-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="80395-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="80395-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="80395-161">Nella sezione **Configurazione Bambu by Sprout Social** fare clic su **Configura Bambu by Sprout Social** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="80395-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="80395-162">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="80395-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="80395-164">Per configurare l'accesso Single Sign-On sul lato **Bambu by Sprout Social**, è necessario inviare il **file XML dei metadati** e l'**URL del servizio Single Sign-On SAML** al [supporto di Bambu by Sprout Social](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="80395-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="80395-165">L'accesso verrà configurato in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="80395-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="80395-166">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="80395-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="80395-167">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="80395-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="80395-168">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD)</span><span class="sxs-lookup"><span data-stu-id="80395-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80395-169">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="80395-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="80395-170">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="80395-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="80395-172">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="80395-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="80395-173">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="80395-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80395-175">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="80395-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80395-177">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="80395-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80395-179">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="80395-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80395-181">a.</span><span class="sxs-lookup"><span data-stu-id="80395-181">a.</span></span> <span data-ttu-id="80395-182">Nella casella di testo **Name** (Nome) digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="80395-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="80395-183">b.</span><span class="sxs-lookup"><span data-stu-id="80395-183">b.</span></span> <span data-ttu-id="80395-184">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80395-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="80395-185">c.</span><span class="sxs-lookup"><span data-stu-id="80395-185">c.</span></span> <span data-ttu-id="80395-186">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="80395-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="80395-187">d.</span><span class="sxs-lookup"><span data-stu-id="80395-187">d.</span></span> <span data-ttu-id="80395-188">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="80395-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="80395-189">Creare un utente test di Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="80395-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="80395-190">L'applicazione supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti verranno automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80395-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="80395-191">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="80395-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="80395-192">In questa sezione viene concesso a Britta Simon l'accesso a Bambu by Sprout Social per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="80395-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Assegna utente][200] 

<span data-ttu-id="80395-194">**Per assegnare Britta Simon a Bambu by Sprout Social, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="80395-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="80395-195">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="80395-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="80395-197">Nell'elenco delle applicazioni selezionare **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="80395-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="80395-199">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="80395-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="80395-201">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="80395-201">Click **Add** button.</span></span> <span data-ttu-id="80395-202">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="80395-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="80395-204">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="80395-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="80395-205">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="80395-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80395-206">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="80395-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80395-207">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="80395-207">Testing single sign-on</span></span>

<span data-ttu-id="80395-208">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="80395-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="80395-209">Quando si fa clic sul riquadro Bambu by Sprout Social nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="80395-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="80395-210">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="80395-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="80395-211">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="80395-211">Additional resources</span></span>

* [<span data-ttu-id="80395-212">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80395-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80395-213">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80395-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png


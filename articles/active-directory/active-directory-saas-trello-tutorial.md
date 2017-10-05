---
title: 'Esercitazione: Integrazione di Azure Active Directory con Trello | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Trello.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="26406-103">Esercitazione: Integrazione di Azure Active Directory con Trello</span><span class="sxs-lookup"><span data-stu-id="26406-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="26406-104">Questa esercitazione descrive come integrare Trello con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26406-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26406-105">L'integrazione di Trello con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26406-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26406-106">È possibile controllare in Azure AD chi può accedere a Trello</span><span class="sxs-lookup"><span data-stu-id="26406-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="26406-107">È possibile abilitare gli utenti per l'accesso automatico a Trello (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="26406-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26406-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26406-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="26406-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26406-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26406-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="26406-110">Prerequisites</span></span>

<span data-ttu-id="26406-111">Per configurare l'integrazione di Azure AD con Trello, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26406-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="26406-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26406-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26406-113">Sottoscrizione di Trello abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="26406-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26406-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="26406-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26406-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="26406-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26406-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="26406-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26406-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26406-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26406-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="26406-118">Scenario description</span></span>
<span data-ttu-id="26406-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="26406-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26406-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="26406-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26406-121">Aggiunta di Trello dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="26406-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="26406-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26406-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="26406-123">Aggiunta di Trello dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="26406-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="26406-124">Per configurare l'integrazione di Trello in Azure AD, è necessario aggiungere Trello dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="26406-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26406-125">**Per aggiungere Trello dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26406-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26406-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="26406-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26406-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="26406-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26406-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26406-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="26406-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="26406-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="26406-133">Nella casella di ricerca digitare **Trello**.</span><span class="sxs-lookup"><span data-stu-id="26406-133">In the search box, type **Trello**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="26406-135">Nel pannello dei risultati selezionare **Trello** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="26406-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26406-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26406-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26406-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Trello in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26406-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26406-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Trello che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26406-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="26406-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Trello.</span><span class="sxs-lookup"><span data-stu-id="26406-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="26406-141">Per stabilire la relazione di collegamento, in Trello assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="26406-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="26406-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Trello, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="26406-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26406-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="26406-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26406-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26406-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26406-145">**[Creazione di un utente di test di Trello](#creating-a-trello-test-user)**: per avere una controparte di Britta Simon in Trello collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26406-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="26406-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26406-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26406-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="26406-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26406-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26406-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26406-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Trello.</span><span class="sxs-lookup"><span data-stu-id="26406-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="26406-150">**Per configurare Single Sign-On di Azure AD con Trello, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26406-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="26406-151">Nella pagina di integrazione dell'applicazione **Trello** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="26406-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="26406-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="26406-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="26406-155">Per configurare l'applicazione in modalità avviata da **IDP**, nella sezione **URL e dominio Trello** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26406-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="26406-157">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="26406-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="26406-158">Per configurare l'applicazione in modalità avviata da **SP**, nella sezione **URL e dominio Trello** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26406-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="26406-160">a.</span><span class="sxs-lookup"><span data-stu-id="26406-160">a.</span></span> <span data-ttu-id="26406-161">Fare clic su **Mostra impostazioni URL avanzate**.</span><span class="sxs-lookup"><span data-stu-id="26406-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="26406-162">b.</span><span class="sxs-lookup"><span data-stu-id="26406-162">b.</span></span> <span data-ttu-id="26406-163">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="26406-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="26406-164">È necessario ottenere il campo dati dinamico **\<enterprise\>** da Trello.</span><span class="sxs-lookup"><span data-stu-id="26406-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="26406-165">Se non si dispone del valore per il campo dati dinamico, contattare il [team di supporto di Trello](mailto:support@trello.com) per ottenere il campo relativo all'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="26406-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="26406-166">L'applicazione Trello prevede che le asserzioni SAML contengano attributi specifici.</span><span class="sxs-lookup"><span data-stu-id="26406-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="26406-167">Configurare gli attributi seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="26406-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="26406-168">È possibile gestire i valori di questi attributi dalla scheda **"Attributi utente"** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="26406-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="26406-169">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="26406-169">The following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="26406-171">Nella finestra di dialogo **Attributi token SAML** seguire questa procedura per ciascuna riga della tabella:</span><span class="sxs-lookup"><span data-stu-id="26406-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="26406-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="26406-172">Attribute Name</span></span> | <span data-ttu-id="26406-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="26406-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="26406-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="26406-174">User.Email</span></span> | <span data-ttu-id="26406-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="26406-175">user.mail</span></span> |
    | <span data-ttu-id="26406-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="26406-176">User.FirstName</span></span> | <span data-ttu-id="26406-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="26406-177">user.givenname</span></span> |
    | <span data-ttu-id="26406-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="26406-178">User.LastName</span></span> | <span data-ttu-id="26406-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="26406-179">user.surname</span></span> |

    <span data-ttu-id="26406-180">a.</span><span class="sxs-lookup"><span data-stu-id="26406-180">a.</span></span> <span data-ttu-id="26406-181">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="26406-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="26406-184">b.</span><span class="sxs-lookup"><span data-stu-id="26406-184">b.</span></span> <span data-ttu-id="26406-185">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="26406-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="26406-186">c.</span><span class="sxs-lookup"><span data-stu-id="26406-186">c.</span></span> <span data-ttu-id="26406-187">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="26406-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="26406-188">d.</span><span class="sxs-lookup"><span data-stu-id="26406-188">d.</span></span> <span data-ttu-id="26406-189">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="26406-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="26406-190">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="26406-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="26406-192">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="26406-192">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26406-194">Nella sezione **Configurazione di Trello** fare clic su **Configura Trello** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="26406-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="26406-195">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="26406-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="26406-197">Per configurare l'SSO per l'applicazione, passare alla pagina [Configurazione di Trello enterprise SSO](https://trello.com/sso-configuration) per inviare al [team di supporto di Trello](mailto:support@trello.com) l'**URL del servizio Single Sign-On SAML** e allegare il **Certificato (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="26406-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="26406-198">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="26406-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26406-199">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="26406-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26406-200">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26406-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26406-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26406-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="26406-202">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26406-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="26406-204">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="26406-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26406-205">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="26406-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26406-207">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="26406-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26406-209">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="26406-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26406-211">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26406-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26406-213">a.</span><span class="sxs-lookup"><span data-stu-id="26406-213">a.</span></span> <span data-ttu-id="26406-214">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26406-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26406-215">b.</span><span class="sxs-lookup"><span data-stu-id="26406-215">b.</span></span> <span data-ttu-id="26406-216">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="26406-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26406-217">c.</span><span class="sxs-lookup"><span data-stu-id="26406-217">c.</span></span> <span data-ttu-id="26406-218">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="26406-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="26406-219">d.</span><span class="sxs-lookup"><span data-stu-id="26406-219">d.</span></span> <span data-ttu-id="26406-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="26406-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="26406-221">Creazione di un utente test di Trello</span><span class="sxs-lookup"><span data-stu-id="26406-221">Creating a Trello test user</span></span>

<span data-ttu-id="26406-222">In questa sezione viene creato un utente di nome Britta Simon in Trello.</span><span class="sxs-lookup"><span data-stu-id="26406-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="26406-223">In questa sezione viene creato un utente di nome Britta Simon in Trello.</span><span class="sxs-lookup"><span data-stu-id="26406-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="26406-224">Trello supporta il provisioning JIT. Al primo accesso ad Azure AD viene creato un nuovo account.</span><span class="sxs-lookup"><span data-stu-id="26406-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="26406-225">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26406-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="26406-226">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Trello.</span><span class="sxs-lookup"><span data-stu-id="26406-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Assegna utente][200] 

<span data-ttu-id="26406-228">**Per assegnare Britta Simon a Trello, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26406-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="26406-229">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26406-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="26406-231">Nell'elenco delle applicazioni selezionare **Trello**.</span><span class="sxs-lookup"><span data-stu-id="26406-231">In the applications list, select **Trello**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="26406-233">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="26406-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="26406-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="26406-235">Click **Add** button.</span></span> <span data-ttu-id="26406-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="26406-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="26406-238">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="26406-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26406-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26406-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26406-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="26406-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26406-241">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="26406-241">Testing single sign-on</span></span>

<span data-ttu-id="26406-242">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="26406-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="26406-243">Quando si fa clic sul riquadro Trello nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Trello.</span><span class="sxs-lookup"><span data-stu-id="26406-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26406-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="26406-244">Additional resources</span></span>

* [<span data-ttu-id="26406-245">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26406-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26406-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26406-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png


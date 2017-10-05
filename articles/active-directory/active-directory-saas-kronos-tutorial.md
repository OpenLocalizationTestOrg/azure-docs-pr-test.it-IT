---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kronos | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Kronos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="38cf8-103">Esercitazione: Integrazione di Azure Active Directory con Kronos</span><span class="sxs-lookup"><span data-stu-id="38cf8-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="38cf8-104">Questa esercitazione descrive come integrare Kronos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38cf8-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38cf8-105">L'integrazione di Kronos con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="38cf8-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38cf8-106">È possibile controllare in Azure AD chi può accedere a Kronos</span><span class="sxs-lookup"><span data-stu-id="38cf8-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="38cf8-107">È possibile abilitare gli utenti per l'accesso automatico a Kronos (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cf8-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38cf8-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="38cf8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="38cf8-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38cf8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38cf8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="38cf8-110">Prerequisites</span></span>

<span data-ttu-id="38cf8-111">Per configurare l'integrazione di Azure AD con Kronos, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="38cf8-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="38cf8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38cf8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38cf8-113">Sottoscrizione di **Kronos Workforce Central** abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="38cf8-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38cf8-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="38cf8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38cf8-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="38cf8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38cf8-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="38cf8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38cf8-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38cf8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38cf8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="38cf8-118">Scenario description</span></span>
<span data-ttu-id="38cf8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="38cf8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38cf8-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="38cf8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38cf8-121">Aggiunta di Kronos dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="38cf8-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="38cf8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cf8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="38cf8-123">Aggiunta di Kronos dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="38cf8-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="38cf8-124">Per configurare l'integrazione di Kronos in Azure AD, è necessario aggiungere Kronos dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="38cf8-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38cf8-125">**Per aggiungere Kronos dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="38cf8-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38cf8-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="38cf8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38cf8-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38cf8-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="38cf8-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="38cf8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="38cf8-133">Nella casella di ricerca digitare **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-133">In the search box, type **Kronos**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="38cf8-135">Nel pannello dei risultati selezionare **Kronos** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38cf8-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38cf8-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cf8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38cf8-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kronos usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="38cf8-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="38cf8-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Kronos che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38cf8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="38cf8-140">In altre parole deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Kronos.</span><span class="sxs-lookup"><span data-stu-id="38cf8-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="38cf8-141">Per stabilire la relazione di collegamento, in Kronos assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="38cf8-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="38cf8-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Kronos, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="38cf8-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38cf8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="38cf8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38cf8-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38cf8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38cf8-145">**[Creazione di un utente test di Kronos](#creating-a-kronos-test-user)**: per avere una controparte di Britta Simon in Kronos collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38cf8-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38cf8-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38cf8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38cf8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="38cf8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38cf8-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cf8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38cf8-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Kronos.</span><span class="sxs-lookup"><span data-stu-id="38cf8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="38cf8-150">**Per configurare l'accesso Single Sign-On di Azure AD con Kronos, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="38cf8-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="38cf8-151">Nella pagina di integrazione dell'applicazione **Kronos** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="38cf8-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="38cf8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="38cf8-155">Nella sezione **URL e dominio Kronos** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="38cf8-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="38cf8-157">a.</span><span class="sxs-lookup"><span data-stu-id="38cf8-157">a.</span></span> <span data-ttu-id="38cf8-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="38cf8-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="38cf8-159">b.</span><span class="sxs-lookup"><span data-stu-id="38cf8-159">b.</span></span> <span data-ttu-id="38cf8-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="38cf8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38cf8-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="38cf8-161">These values are not real.</span></span> <span data-ttu-id="38cf8-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="38cf8-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="38cf8-163">Per ottenere questi valori, contattare il [team di supporto di Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="38cf8-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="38cf8-164">L'applicazione Kronos si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="38cf8-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="38cf8-165">Contattare prima di tutto il [team di supporto di Kronos](https://www.kronos.in/contact/en-in/form) per individuare l'identificatore utente corretto che è mappato all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38cf8-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="38cf8-166">Seguire anche le indicazioni relative all'attributo da usare per il mapping.</span><span class="sxs-lookup"><span data-stu-id="38cf8-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="38cf8-167">Microsoft consiglia di usare l'attributo **"NameIdentifier"** come identificatore utente.</span><span class="sxs-lookup"><span data-stu-id="38cf8-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="38cf8-168">È possibile gestire i valori di questi attributi nella sezione **"Attributi utente"** della pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38cf8-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="38cf8-169">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="38cf8-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="38cf8-170">Qui è stato eseguito il mapping di **Identificatore utente (nameid)** con la funzione **ExtractMailPrefix()** di **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="38cf8-171">In questo modo si ottiene il valore di prefisso della posta elettronica dell'utente che rappresenta l'ID univoco dell'utente.</span><span class="sxs-lookup"><span data-stu-id="38cf8-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="38cf8-172">Questo viene inviato all'applicazione Kronos in ogni risposta con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="38cf8-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="38cf8-174">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On**:</span><span class="sxs-lookup"><span data-stu-id="38cf8-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="38cf8-175">a.</span><span class="sxs-lookup"><span data-stu-id="38cf8-175">a.</span></span> <span data-ttu-id="38cf8-176">Nell'elenco a discesa Identificatore utente selezionare **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="38cf8-177">b.</span><span class="sxs-lookup"><span data-stu-id="38cf8-177">b.</span></span> <span data-ttu-id="38cf8-178">Nell'elenco a discesa **Posta** selezionare **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="38cf8-179">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="38cf8-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="38cf8-181">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="38cf8-181">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="38cf8-183">Per configurare l'accesso Single Sign-On sul lato **Kronos**, è necessario inviare il file **XML dei metadati** scaricato al [team di supporto di Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="38cf8-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="38cf8-184">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="38cf8-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38cf8-185">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="38cf8-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38cf8-186">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38cf8-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38cf8-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cf8-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="38cf8-188">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="38cf8-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="38cf8-190">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="38cf8-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38cf8-191">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="38cf8-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38cf8-193">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="38cf8-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38cf8-195">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38cf8-197">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="38cf8-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38cf8-199">a.</span><span class="sxs-lookup"><span data-stu-id="38cf8-199">a.</span></span> <span data-ttu-id="38cf8-200">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38cf8-201">b.</span><span class="sxs-lookup"><span data-stu-id="38cf8-201">b.</span></span> <span data-ttu-id="38cf8-202">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38cf8-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38cf8-203">c.</span><span class="sxs-lookup"><span data-stu-id="38cf8-203">c.</span></span> <span data-ttu-id="38cf8-204">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38cf8-205">d.</span><span class="sxs-lookup"><span data-stu-id="38cf8-205">d.</span></span> <span data-ttu-id="38cf8-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="38cf8-207">Creazione di un utente test di Kronos</span><span class="sxs-lookup"><span data-stu-id="38cf8-207">Creating a Kronos test user</span></span>

<span data-ttu-id="38cf8-208">In questa sezione viene creato un utente chiamato Britta Simon in Kronos.</span><span class="sxs-lookup"><span data-stu-id="38cf8-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="38cf8-209">L'applicazione Kronos richiede che venga eseguito il provisioning di tutti gli utenti all'interno dell'applicazione prima di eseguire l'accesso SSO.</span><span class="sxs-lookup"><span data-stu-id="38cf8-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="38cf8-210">Contattare il [team di supporto di Kronos](https://www.kronos.in/contact/en-in/form) per eseguire il provisioning di tutti gli utenti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38cf8-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38cf8-211">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38cf8-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38cf8-212">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Kronos.</span><span class="sxs-lookup"><span data-stu-id="38cf8-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Assegna utente][200] 

<span data-ttu-id="38cf8-214">**Per assegnare Britta Simon a Kronos, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="38cf8-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="38cf8-215">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="38cf8-217">Nell'elenco delle applicazioni selezionare **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-217">In the applications list, select **Kronos**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="38cf8-219">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="38cf8-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="38cf8-221">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-221">Click **Add** button.</span></span> <span data-ttu-id="38cf8-222">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="38cf8-224">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="38cf8-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38cf8-225">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38cf8-226">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="38cf8-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38cf8-227">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="38cf8-227">Testing single sign-on</span></span>

<span data-ttu-id="38cf8-228">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="38cf8-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="38cf8-229">Quando si fa clic sul riquadro Kronos nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Kronos.</span><span class="sxs-lookup"><span data-stu-id="38cf8-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38cf8-230">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="38cf8-230">Additional resources</span></span>

* [<span data-ttu-id="38cf8-231">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38cf8-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38cf8-232">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38cf8-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con 123ContactForm | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e 123ContactForm.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="c3248-103">Esercitazione: Integrazione di Azure Active Directory con 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="c3248-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="c3248-104">Questa esercitazione descrive come integrare 123ContactForm con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3248-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3248-105">L'integrazione di 123ContactForm con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3248-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3248-106">È possibile controllare in Azure AD chi può accedere a 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="c3248-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="c3248-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a 123ContactForm con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3248-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3248-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3248-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c3248-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3248-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3248-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c3248-110">Prerequisites</span></span>

<span data-ttu-id="c3248-111">Per configurare l'integrazione di Azure AD con 123ContactForm sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3248-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="c3248-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3248-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3248-113">Sottoscrizione di 123ContactForm abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3248-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3248-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c3248-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3248-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3248-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3248-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c3248-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3248-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3248-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3248-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c3248-118">Scenario description</span></span>
<span data-ttu-id="c3248-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c3248-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3248-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3248-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3248-121">Aggiunta di 123ContactForm dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c3248-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="c3248-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3248-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="c3248-123">Aggiunta di 123ContactForm dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c3248-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="c3248-124">Per configurare l'integrazione di 123ContactForm in Azure AD è necessario aggiungere 123ContactForm dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c3248-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3248-125">**Per aggiungere 123ContactForm dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3248-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3248-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c3248-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3248-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c3248-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c3248-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3248-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c3248-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3248-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c3248-133">Nella casella di ricerca digitare **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="c3248-133">In the search box, type **123ContactForm**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="c3248-135">Nel pannello dei risultati selezionare **123ContactForm** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3248-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3248-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3248-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3248-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 123ContactForm mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3248-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c3248-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di 123ContactForm corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3248-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="c3248-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="c3248-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="c3248-141">Per stabilire la relazione di collegamento, in 123ContactForm assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c3248-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c3248-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con 123ContactForm è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3248-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3248-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c3248-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3248-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3248-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3248-145">**[Creazione di un utente test di 123ContactForm](#creating-a-123contactform-test-user)**: per avere una controparte di Britta Simon in 123ContactForm collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3248-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3248-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3248-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3248-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c3248-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3248-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3248-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3248-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="c3248-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="c3248-150">**Per configurare l'accesso Single Sign-On di Azure AD con 123ContactForm, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3248-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="c3248-151">Nella pagina di integrazione dell'applicazione **123ContactForm** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c3248-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c3248-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c3248-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="c3248-155">Nella sezione **URL e dominio 123ContactForm** seguire questa procedura per configurare l'applicazione in **modalità avviata da IDP**:</span><span class="sxs-lookup"><span data-stu-id="c3248-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="c3248-157">a.</span><span class="sxs-lookup"><span data-stu-id="c3248-157">a.</span></span> <span data-ttu-id="c3248-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="c3248-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="c3248-159">b.</span><span class="sxs-lookup"><span data-stu-id="c3248-159">b.</span></span> <span data-ttu-id="c3248-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="c3248-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="c3248-161">Per configurare l'applicazione in **modalità avviata da SP** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3248-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="c3248-163">a.</span><span class="sxs-lookup"><span data-stu-id="c3248-163">a.</span></span> <span data-ttu-id="c3248-164">Fare clic sull'opzione **Mostra impostazioni URL avanzate**.</span><span class="sxs-lookup"><span data-stu-id="c3248-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="c3248-165">b.</span><span class="sxs-lookup"><span data-stu-id="c3248-165">b.</span></span> <span data-ttu-id="c3248-166">Nella casella di testo **URL di accesso** digitare un URL come indicato di seguito: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="c3248-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3248-167">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c3248-167">These values are not real.</span></span> <span data-ttu-id="c3248-168">è necessario aggiornarli in seguito con un URL e un identificatore reali. La procedura è descritta più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c3248-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="c3248-169">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="c3248-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="c3248-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c3248-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c3248-173">Per configurare l'accesso Single Sign-On sul lato **123ContactForm** accedere a [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3248-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="c3248-175">a.</span><span class="sxs-lookup"><span data-stu-id="c3248-175">a.</span></span> <span data-ttu-id="c3248-176">Nella casella di testo **Email** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'utente, ovvero</span><span class="sxs-lookup"><span data-stu-id="c3248-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="c3248-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c3248-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="c3248-178">b.</span><span class="sxs-lookup"><span data-stu-id="c3248-178">b.</span></span> <span data-ttu-id="c3248-179">Fare clic su **Carica** e selezionare il file XML metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3248-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="c3248-180">c.</span><span class="sxs-lookup"><span data-stu-id="c3248-180">c.</span></span> <span data-ttu-id="c3248-181">Fare clic su **SUBMIT FORM** (Invia modulo).</span><span class="sxs-lookup"><span data-stu-id="c3248-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="c3248-182">In **Microsoft Azure AD - Single sign-on - Configure App Settings** (Microsoft Azure AD - Single Sign-On - Configura impostazioni app) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3248-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="c3248-184">a.</span><span class="sxs-lookup"><span data-stu-id="c3248-184">a.</span></span> <span data-ttu-id="c3248-185">Per configurare l'applicazione in **modalità avviata da IDP**, copiare il valore di **IDENTIFIER** (Identificatore) per l'istanza e incollarlo nella casella di testo **Identificatore** nella sezione **URL e dominio 123ContactForm** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3248-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="c3248-186">b.</span><span class="sxs-lookup"><span data-stu-id="c3248-186">b.</span></span> <span data-ttu-id="c3248-187">Per configurare l'applicazione in **modalità avviata da IDP**, copiare il valore di **REPLY URL** (URL di risposta) per l'istanza e incollarlo nella casella di testo **URL di risposta** nella sezione **URL e dominio 123ContactForm** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3248-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="c3248-188">c.</span><span class="sxs-lookup"><span data-stu-id="c3248-188">c.</span></span> <span data-ttu-id="c3248-189">Per configurare l'applicazione in **modalità avviata da SP**, copiare il valore di **SIGN ON URL** (URL di accesso) per l'istanza e incollarlo nella casella di testo **URL di accesso** nella sezione **URL e dominio 123ContactForm** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3248-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="c3248-190">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c3248-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c3248-191">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c3248-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c3248-192">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3248-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3248-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3248-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3248-194">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3248-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c3248-196">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c3248-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3248-197">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c3248-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3248-199">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c3248-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3248-201">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c3248-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3248-203">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c3248-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3248-205">a.</span><span class="sxs-lookup"><span data-stu-id="c3248-205">a.</span></span> <span data-ttu-id="c3248-206">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3248-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3248-207">b.</span><span class="sxs-lookup"><span data-stu-id="c3248-207">b.</span></span> <span data-ttu-id="c3248-208">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c3248-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3248-209">c.</span><span class="sxs-lookup"><span data-stu-id="c3248-209">c.</span></span> <span data-ttu-id="c3248-210">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c3248-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c3248-211">d.</span><span class="sxs-lookup"><span data-stu-id="c3248-211">d.</span></span> <span data-ttu-id="c3248-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c3248-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="c3248-213">Creazione di un utente test di 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="c3248-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="c3248-214">L'applicazione supporta il provisioning dell'utente just-in-time e dopo l'autenticazione gli utenti verranno automaticamente creati nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3248-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c3248-215">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3248-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c3248-216">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="c3248-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c3248-218">**Per assegnare Britta Simon a 123ContactForm, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c3248-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="c3248-219">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c3248-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c3248-221">Nell'elenco delle applicazioni selezionare **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="c3248-221">In the applications list, select **123ContactForm**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="c3248-223">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c3248-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c3248-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c3248-225">Click **Add** button.</span></span> <span data-ttu-id="c3248-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3248-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c3248-228">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c3248-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c3248-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c3248-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3248-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c3248-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3248-231">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c3248-231">Testing single sign-on</span></span>

<span data-ttu-id="c3248-232">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c3248-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c3248-233">Quando si fa clic sul riquadro 123ContactForm nel pannello di accesso si accede automaticamente all'applicazione 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="c3248-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="c3248-234">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3248-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3248-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c3248-235">Additional resources</span></span>

* [<span data-ttu-id="c3248-236">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3248-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3248-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3248-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png


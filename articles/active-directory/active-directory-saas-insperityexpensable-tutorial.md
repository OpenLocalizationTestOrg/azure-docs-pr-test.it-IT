---
title: 'Esercitazione: Integrazione di Azure Active Directory con Insperity ExpensAble | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Insperity ExpensAble.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: b50e10be54b1fc413be10bee5b58631790629335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="35274-103">Esercitazione: Integrazione di Azure Active Directory con Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="35274-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="35274-104">Questa esercitazione descrive come integrare Insperity ExpensAble con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35274-104">In this tutorial, you learn how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35274-105">L'integrazione di Insperity ExpensAble con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="35274-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="35274-106">È possibile controllare in Azure AD chi può accedere a Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="35274-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
- <span data-ttu-id="35274-107">È possibile abilitare gli utenti per l'accesso automatico a Insperity ExpensAble (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="35274-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35274-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="35274-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="35274-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35274-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35274-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35274-110">Prerequisites</span></span>

<span data-ttu-id="35274-111">Per configurare l'integrazione di Azure AD con Insperity ExpensAble, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="35274-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

- <span data-ttu-id="35274-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35274-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35274-113">Sottoscrizione di Insperity ExpensAble abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="35274-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35274-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="35274-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35274-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="35274-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35274-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="35274-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35274-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35274-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35274-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="35274-118">Scenario description</span></span>
<span data-ttu-id="35274-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="35274-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35274-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="35274-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35274-121">Aggiunta di Insperity ExpensAble dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="35274-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="35274-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35274-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="35274-123">Aggiunta di Insperity ExpensAble dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="35274-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="35274-124">Per configurare l'integrazione di Insperity ExpensAble in Azure AD, è necessario aggiungere Insperity ExpensAble dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="35274-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="35274-125">**Per aggiungere Insperity ExpensAble dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="35274-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="35274-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="35274-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35274-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="35274-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="35274-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="35274-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="35274-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="35274-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="35274-133">Nella casella di ricerca digitare **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="35274-133">In the search box, type **Insperity ExpensAble**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="35274-135">Nel pannello dei risultati selezionare **Insperity ExpensAble** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35274-135">In the results panel, select **Insperity ExpensAble**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35274-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35274-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35274-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Insperity ExpensAble mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="35274-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35274-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Insperity ExpensAble corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35274-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble is to a user in Azure AD.</span></span> <span data-ttu-id="35274-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="35274-140">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>

<span data-ttu-id="35274-141">Per stabilire la relazione di collegamento, in Insperity ExpensAble assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="35274-141">In Insperity ExpensAble, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="35274-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Insperity ExpensAble, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="35274-142">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="35274-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="35274-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="35274-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35274-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35274-145">**[Creazione di un utente test di Insperity ExpensAble](#creating-an-insperity-expensable-test-user)**: per avere una controparte di Britta Simon in Insperity ExpensAble collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35274-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="35274-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35274-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35274-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="35274-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35274-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35274-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35274-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="35274-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="35274-150">**Per configurare Single Sign-On di Azure AD con Insperity ExpensAble, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="35274-150">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="35274-151">Nella pagina di integrazione dell'applicazione **Insperity ExpensAble** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="35274-151">In the Azure portal, on the **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="35274-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="35274-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="35274-155">Nella sezione **URL e dominio Insperity ExpensAble** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="35274-155">On the **Insperity ExpensAble Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="35274-157">a.</span><span class="sxs-lookup"><span data-stu-id="35274-157">a.</span></span> <span data-ttu-id="35274-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="35274-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35274-159">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="35274-159">This value is not real.</span></span> <span data-ttu-id="35274-160">Aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="35274-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="35274-161">Per ottenere il valore contattare il [team di supporto clienti di Insperity ExpensAble ](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="35274-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) to get this value.</span></span> 
 
4. <span data-ttu-id="35274-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="35274-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="35274-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="35274-164">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35274-166">Nella sezione **Configurazione di Insperity ExpensAble** fare clic su **Configura Insperity ExpensAble** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="35274-166">On the **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** to open **Configure sign-on** window.</span></span> <span data-ttu-id="35274-167">Copiare i valori **SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="35274-167">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="35274-169">Per configurare l'accesso Single Sign-On sul lato **Insperity ExpensAble** è necessario inviare il file **XML metadati** scaricato e i valori **SAML Entity ID** (ID entità SAML) e **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) al [team di supporto Insperity ExpensAble](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="35274-169">To configure single sign-on on **Insperity ExpensAble** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="35274-170">L'applicazione viene configurata in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="35274-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="35274-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="35274-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="35274-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="35274-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="35274-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35274-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35274-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35274-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="35274-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="35274-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="35274-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="35274-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="35274-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="35274-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35274-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="35274-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35274-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="35274-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35274-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="35274-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35274-186">a.</span><span class="sxs-lookup"><span data-stu-id="35274-186">a.</span></span> <span data-ttu-id="35274-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35274-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35274-188">b.</span><span class="sxs-lookup"><span data-stu-id="35274-188">b.</span></span> <span data-ttu-id="35274-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35274-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35274-190">c.</span><span class="sxs-lookup"><span data-stu-id="35274-190">c.</span></span> <span data-ttu-id="35274-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="35274-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="35274-192">d.</span><span class="sxs-lookup"><span data-stu-id="35274-192">d.</span></span> <span data-ttu-id="35274-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="35274-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="35274-194">Creazione di un utente test di Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="35274-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="35274-195">Questa sezione descrive come creare un utente chiamato Britta Simon in Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="35274-195">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="35274-196">Collaborare con il [team di supporto di Insperity ExpensAble](http://expensable.com/support/support-overview) per aggiungere gli utenti nell'account Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="35274-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) to add the users in the Insperity ExpensAble account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="35274-197">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35274-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="35274-198">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="35274-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insperity ExpensAble.</span></span>

![Assegna utente][200] 

<span data-ttu-id="35274-200">**Per assegnare Britta Simon a Insperity ExpensAble, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="35274-200">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="35274-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="35274-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="35274-203">Nell’elenco di applicazioni selezionare **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="35274-203">In the applications list, select **Insperity ExpensAble**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="35274-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="35274-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="35274-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="35274-207">Click **Add** button.</span></span> <span data-ttu-id="35274-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="35274-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="35274-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="35274-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="35274-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="35274-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35274-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="35274-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35274-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="35274-213">Testing single sign-on</span></span>

<span data-ttu-id="35274-214">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="35274-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="35274-215">Quando si fa clic sul riquadro Insperity ExpensAble nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="35274-215">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>
<span data-ttu-id="35274-216">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35274-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35274-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="35274-217">Additional resources</span></span>

* [<span data-ttu-id="35274-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35274-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35274-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35274-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png


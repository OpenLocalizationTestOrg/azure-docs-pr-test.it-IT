---
title: 'Esercitazione: Integrazione di Azure Active Directory con PerformanceCentre | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e PerformanceCentre.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e86adaf4bd9b4752f2aece8207a8a423ec5590a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="d8c79-103">Esercitazione Integrazione di Azure Active Directory con PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="d8c79-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="d8c79-104">Questa esercitazione descrive come integrare PerformanceCentre con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8c79-104">In this tutorial, you learn how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8c79-105">L'integrazione di PerformanceCentre con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8c79-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d8c79-106">È possibile controllare in Azure AD chi può accedere a PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="d8c79-106">You can control in Azure AD who has access to PerformanceCentre</span></span>
- <span data-ttu-id="d8c79-107">È possibile abilitare gli utenti per l'accesso automatico a PerformanceCentre (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8c79-107">You can enable your users to automatically get signed-on to PerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8c79-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8c79-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d8c79-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8c79-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8c79-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d8c79-110">Prerequisites</span></span>

<span data-ttu-id="d8c79-111">Per configurare l'integrazione di Azure AD con PerformanceCentre, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8c79-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span></span>

- <span data-ttu-id="d8c79-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8c79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8c79-113">Sottoscrizione di PerformanceCentre abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d8c79-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8c79-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d8c79-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8c79-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8c79-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8c79-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d8c79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d8c79-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8c79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8c79-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d8c79-118">Scenario description</span></span>
<span data-ttu-id="d8c79-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d8c79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8c79-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8c79-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8c79-121">Aggiunta di PerformanceCentre dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d8c79-121">Adding PerformanceCentre from the gallery</span></span>
2. <span data-ttu-id="d8c79-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8c79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-the-gallery"></a><span data-ttu-id="d8c79-123">Aggiunta di PerformanceCentre dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d8c79-123">Adding PerformanceCentre from the gallery</span></span>
<span data-ttu-id="d8c79-124">Per configurare l'integrazione di PerformanceCentre in Azure AD, è necessario aggiungere PerformanceCentre dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d8c79-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d8c79-125">**Per aggiungere PerformanceCentre dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d8c79-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d8c79-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d8c79-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8c79-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d8c79-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d8c79-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8c79-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d8c79-133">Nella casella di ricerca digitare **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-133">In the search box, type **PerformanceCentre**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="d8c79-135">Nel pannello dei risultati selezionare **PerformanceCentre** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8c79-135">In the results panel, select **PerformanceCentre**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8c79-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8c79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8c79-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PerformanceCentre in base a un utente di prova di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d8c79-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8c79-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di PerformanceCentre che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8c79-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PerformanceCentre is to a user in Azure AD.</span></span> <span data-ttu-id="d8c79-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="d8c79-140">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span></span>

<span data-ttu-id="d8c79-141">Per stabilire la relazione di collegamento, in PerformanceCentre assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="d8c79-141">In PerformanceCentre, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d8c79-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con PerformanceCentre, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8c79-142">To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d8c79-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d8c79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d8c79-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8c79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8c79-145">**[Creazione di un utente test per PerformanceCentre](#creating-a-performancecentre-test-user)** : per avere una controparte di Britta Simon in PerformanceCentre collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8c79-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d8c79-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8c79-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8c79-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d8c79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8c79-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8c79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8c79-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="d8c79-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="d8c79-150">**Per configurare l'accesso Single Sign-On di Azure AD con PerformanceCentre, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d8c79-150">**To configure Azure AD single sign-on with PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="d8c79-151">Nella pagina di integrazione dell'applicazione **PerformanceCentre** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-151">In the Azure portal, on the **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d8c79-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d8c79-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="d8c79-155">Nella sezione **URL e dominio PerformanceCentre** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8c79-155">On the **PerformanceCentre Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="d8c79-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8c79-157">a.</span></span> <span data-ttu-id="d8c79-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `http://companyname.performancecentre.com/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="d8c79-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="d8c79-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8c79-159">b.</span></span> <span data-ttu-id="d8c79-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="d8c79-160">In the **Identifier** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d8c79-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d8c79-161">These values are not real.</span></span> <span data-ttu-id="d8c79-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="d8c79-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d8c79-163">Per ottenere questi valori, contattare il [team di supporto clienti di PerformanceCentre](https://www.performancecentre.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="d8c79-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="d8c79-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="d8c79-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="d8c79-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d8c79-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d8c79-168">Nella sezione **Configurazione di PerformanceCentre** fare clic su **Configura PerformanceCentre** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-168">On the **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d8c79-169">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d8c79-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="d8c79-171">Accedere al sito aziendale di **PerformanceCentre** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d8c79-171">Sign-on to your **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="d8c79-172">Nella barra di spostamento sul lato sinistro fare clic su **Configure**(Configura).</span><span class="sxs-lookup"><span data-stu-id="d8c79-172">In the tab on the left side, click **Configure**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][10]

9. <span data-ttu-id="d8c79-174">Nella scheda sul lato sinistro fare clic su **Miscellaneous** (Varie) e quindi su **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-174">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][11]

10. <span data-ttu-id="d8c79-176">Per **Protocol** (Protocollo) selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][12]

11. <span data-ttu-id="d8c79-178">Aprire il file di metadati nel Blocco note, copiarne il contenuto negli Appunti, incollarlo nella casella di testo **Identity Provider Metadata** (Metadati provider di identità) e quindi fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="d8c79-178">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][13]

12. <span data-ttu-id="d8c79-180">Verificare che i valori di **Entity Base URL** (URL base entità) e **Entity ID URL** (URL ID entità) siano corretti.</span><span class="sxs-lookup"><span data-stu-id="d8c79-180">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Single Sign-On di Microsoft Azure AD][14]

> [!TIP]
> <span data-ttu-id="d8c79-182">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d8c79-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d8c79-183">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d8c79-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d8c79-184">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8c79-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8c79-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8c79-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8c79-186">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8c79-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d8c79-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d8c79-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d8c79-189">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d8c79-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8c79-191">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d8c79-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8c79-193">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8c79-195">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8c79-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8c79-197">a.</span><span class="sxs-lookup"><span data-stu-id="d8c79-197">a.</span></span> <span data-ttu-id="d8c79-198">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8c79-199">b.</span><span class="sxs-lookup"><span data-stu-id="d8c79-199">b.</span></span> <span data-ttu-id="d8c79-200">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8c79-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8c79-201">c.</span><span class="sxs-lookup"><span data-stu-id="d8c79-201">c.</span></span> <span data-ttu-id="d8c79-202">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d8c79-203">d.</span><span class="sxs-lookup"><span data-stu-id="d8c79-203">d.</span></span> <span data-ttu-id="d8c79-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="d8c79-205">Creazione di un utente test per PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="d8c79-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="d8c79-206">Questa sezione descrive come creare un utente chiamato Britta Simon in PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="d8c79-206">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="d8c79-207">**Per creare un utente denominato Britta Simon in PerformanceCentre, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d8c79-207">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="d8c79-208">Accedere al sito aziendale di PerformanceCentre come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d8c79-208">Sign on to your PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="d8c79-209">Nel menu a sinistra fare clic su **Interrelate** (Collega) e quindi su **Create Participant** (Crea partecipante).</span><span class="sxs-lookup"><span data-stu-id="d8c79-209">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Crea utente][400]

3. <span data-ttu-id="d8c79-211">Nella finestra di dialogo **Interrelate - Create Participant** (Collega - Crea partecipante) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8c79-211">On the **Interrelate - Create Participant** dialog, perform the following steps:</span></span>
   
    ![Crea utente][401]
    
    <span data-ttu-id="d8c79-213">a.</span><span class="sxs-lookup"><span data-stu-id="d8c79-213">a.</span></span> <span data-ttu-id="d8c79-214">Immettere gli attributi richiesti per Britta Simon nelle caselle di testo corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="d8c79-214">Type the required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="d8c79-215">L'attributo User Name di Britta in PerformanceCentre deve corrispondere al nome utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8c79-215">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span></span>
    
    <span data-ttu-id="d8c79-216">b.</span><span class="sxs-lookup"><span data-stu-id="d8c79-216">b.</span></span> <span data-ttu-id="d8c79-217">Selezionare **Client Administrator** in **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="d8c79-218">c.</span><span class="sxs-lookup"><span data-stu-id="d8c79-218">c.</span></span> <span data-ttu-id="d8c79-219">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-219">Click **Save**.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d8c79-220">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8c79-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d8c79-221">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="d8c79-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PerformanceCentre.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d8c79-223">**Per assegnare Britta Simon a PerformanceCentre, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d8c79-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="d8c79-224">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d8c79-226">Nell'elenco di applicazioni selezionare **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-226">In the applications list, select **PerformanceCentre**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="d8c79-228">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d8c79-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d8c79-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-230">Click **Add** button.</span></span> <span data-ttu-id="d8c79-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d8c79-233">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d8c79-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d8c79-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8c79-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d8c79-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8c79-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d8c79-236">Testing single sign-on</span></span>

<span data-ttu-id="d8c79-237">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d8c79-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="d8c79-238">Quando si fa clic sul riquadro PerformanceCentre nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="d8c79-238">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8c79-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8c79-239">Additional resources</span></span>

* [<span data-ttu-id="d8c79-240">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8c79-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8c79-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8c79-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png


---
title: 'Esercitazione: Integrazione di Azure Active Directory con SilkRoad Life Suite | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SilkRoad Life Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="f6653-103">Esercitazione: Integrazione di Azure Active Directory con SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="f6653-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="f6653-104">Questa esercitazione descrive l'integrazione di SilkRoad Life Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6653-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="f6653-105">L'integrazione di SilkRoad Life Suite con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6653-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="f6653-106">È possibile controllare in Azure AD chi può accedere a SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="f6653-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="f6653-107">È possibile abilitare gli utenti per l'accesso automatico a SilkRoad Life Suite Single Sign-On (SSO) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6653-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="f6653-108">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6653-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6653-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f6653-109">Prerequisites</span></span>
<span data-ttu-id="f6653-110">Per configurare l'integrazione di Azure AD con SilkRoad Life Suite, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6653-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="f6653-111">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6653-111">An Azure AD subscription</span></span>
* <span data-ttu-id="f6653-112">Sottoscrizione di SilkRoad Life Suite abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="f6653-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="f6653-113">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f6653-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="f6653-114">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6653-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f6653-115">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f6653-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f6653-116">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6653-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="f6653-117">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f6653-117">Scenario Description</span></span>
<span data-ttu-id="f6653-118">L'obiettivo di questa esercitazione è quello di testare l'accesso Single Sign-On (SSO) di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f6653-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="f6653-119">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6653-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6653-120">Aggiunta di SilkRoad Life Suite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f6653-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="f6653-121">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6653-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="f6653-122">Aggiungere SilkRoad Life Suite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f6653-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="f6653-123">Per configurare l'integrazione di SilkRoad Life Suite in Azure AD, è necessario aggiungere SilkRoad Life Suite dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f6653-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f6653-124">**Per aggiungere SilkRoad Life Suite dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f6653-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f6653-125">Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f6653-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="f6653-127">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="f6653-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f6653-128">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="f6653-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="f6653-130">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="f6653-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3]

5. <span data-ttu-id="f6653-132">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="f6653-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applicazioni][4]

6. <span data-ttu-id="f6653-134">Nella casella di ricerca digitare **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="f6653-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Applicazioni][5]

7. <span data-ttu-id="f6653-136">Nel riquadro dei risultati selezionare **SilkRoad Life Suite** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f6653-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Applicazioni][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f6653-138">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6653-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f6653-139">Questa sezione descrive come configurare e testare l'accesso SSO di Azure AD con SilkRoad Life Suite in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f6653-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6653-140">Per il funzionamento dell'accesso SSO, Azure AD deve conoscere qual è l'utente di SilkRoad Life Suite che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6653-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="f6653-141">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="f6653-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="f6653-142">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="f6653-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="f6653-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con SilkRoad Life Suite, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6653-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f6653-144">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on)**: per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f6653-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f6653-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6653-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6653-146">**[Creazione di un utente di test di SilkRoad Life Suite](#creating-a-silkroad-life-suite-test-user)** : per avere una controparte di Britta Simon in SilkRoad Life Suite collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6653-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f6653-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6653-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6653-148">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f6653-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f6653-149">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6653-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="f6653-150">Questa sezione descrive come abilitare l'accesso SSO di Azure AD nel portale di Azure classico e configurare l'accesso SSO nell'applicazione SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="f6653-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="f6653-151">**Per configurare Single Sign-On di Azure AD con SilkRoad Life Suite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f6653-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="f6653-152">Accedere al sito aziendale di SilkRoad come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f6653-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="f6653-153">Per ottenere l'accesso all'applicazione SilkRoad Life Suite Authentication per configurare la federazione con Microsoft Azure AD, contattare il supporto SilkRoad o il rappresentante dei servizi SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="f6653-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="f6653-154">Passare a **Service Provider** (Provider di servizi) e quindi fare clic su **Federation Details** (Dettagli federazione).</span><span class="sxs-lookup"><span data-stu-id="f6653-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][10] 

3. <span data-ttu-id="f6653-156">Fare clic su **Download Federation Metadata**(Scarica metadati federazione) e quindi salvare il file di metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="f6653-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][11] 

4. <span data-ttu-id="f6653-158">Nella pagina di integrazione dell'applicazione **SilkRoad Life Suite** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f6653-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 

5. <span data-ttu-id="f6653-160">Nella pagina **Stabilire come si desidera che gli utenti accedano a SilkRoad Life Suite** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f6653-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][7] 

6. <span data-ttu-id="f6653-162">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f6653-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][8]   
 1. <span data-ttu-id="f6653-164">Nella casella di testo **URL di accesso** digitare l'URL usato dagli utenti per accedere al sito SilkRoad Life Suite, ad esempio *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*.</span><span class="sxs-lookup"><span data-stu-id="f6653-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="f6653-165">Aprire il file dei metadati **Silkroad** scaricato.</span><span class="sxs-lookup"><span data-stu-id="f6653-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="f6653-166">Trovare il tag **AssertionConsumerService** e quindi copiare l'attributo **Location**.</span><span class="sxs-lookup"><span data-stu-id="f6653-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Single Sign-On di Microsoft Azure AD][21] 
 4. <span data-ttu-id="f6653-168">Incollare il valore nella casella di testo **URL di risposta** .</span><span class="sxs-lookup"><span data-stu-id="f6653-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="f6653-169">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f6653-169">Click **Next**.</span></span>

6. <span data-ttu-id="f6653-170">Nella pagina **Configura accesso Single Sign-On in SilkRoad Life Suite** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f6653-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][9]  
 1. <span data-ttu-id="f6653-172">Fare clic su Download certificato e quindi salvare il file nel computer.</span><span class="sxs-lookup"><span data-stu-id="f6653-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="f6653-173">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f6653-173">Click **Next**.</span></span>

7. <span data-ttu-id="f6653-174">Nell'applicazione **SilkRoad**, fare clic su **Authentication Sources** (Origini autenticazione).</span><span class="sxs-lookup"><span data-stu-id="f6653-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][12] 

8. <span data-ttu-id="f6653-176">Fare clic su **Add Authentication Source**(Aggiungi origine autenticazione).</span><span class="sxs-lookup"><span data-stu-id="f6653-176">Click **Add Authentication Source**.</span></span> 
   
    ![Accesso Single Sign-On di Azure AD][13] 

9. <span data-ttu-id="f6653-178">Nella sezione **Add Authentication Source** (Aggiungi origine autenticazione) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f6653-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][14]  
 1. <span data-ttu-id="f6653-180">In **Option 2 - Metadata File** (Opzione 2 - File di metadati) fare clic su **Browse** (Sfoglia) per caricare il file di metadati scaricato.</span><span class="sxs-lookup"><span data-stu-id="f6653-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="f6653-181">Fare clic su **Create Identity Provider using File Data**.</span><span class="sxs-lookup"><span data-stu-id="f6653-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="f6653-182">Nella sezione **Authentication Sources** (Origini autenticazione) fare clic su **Edit** (Modifica).</span><span class="sxs-lookup"><span data-stu-id="f6653-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Single Sign-On di Microsoft Azure AD][15] 

11. <span data-ttu-id="f6653-184">Nella finestra di dialogo **Edit Authentication Source** (Modifica origine autenticazione) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f6653-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Single Sign-On di Microsoft Azure AD][16] 
 1. <span data-ttu-id="f6653-186">In **Enabled** (Attivo) selezionare **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="f6653-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="f6653-187">Nella casella di testo **IdP Description** digitare una descrizione per la configurazione, ad esempio *Azure AD SSO*.</span><span class="sxs-lookup"><span data-stu-id="f6653-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="f6653-188">Nella casella di testo **IdP Name** digitare un nome specifico per la configurazione, ad esempio *Azure SP*.</span><span class="sxs-lookup"><span data-stu-id="f6653-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="f6653-189">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="f6653-189">Click **Save**.</span></span>

12. <span data-ttu-id="f6653-190">Disabilitare tutte le altre origini di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f6653-190">Disable all other authentication sources.</span></span> 
    
     ![Single Sign-On di Microsoft Azure AD][17]

13. <span data-ttu-id="f6653-192">Nella pagina **Conferma Single Sign-On** del portale di Azure classico fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f6653-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Single Sign-On di Microsoft Azure AD][18]

14. <span data-ttu-id="f6653-194">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="f6653-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Single Sign-On di Microsoft Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f6653-196">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6653-196">Create an Azure AD test user</span></span>
<span data-ttu-id="f6653-197">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="f6653-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="f6653-199">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f6653-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f6653-200">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f6653-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="f6653-202">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="f6653-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f6653-203">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="f6653-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6653-205">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="f6653-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f6653-207">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f6653-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="f6653-209">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="f6653-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="f6653-210">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6653-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="f6653-211">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f6653-211">Click **Next**.</span></span>

6. <span data-ttu-id="f6653-212">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f6653-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="f6653-214">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f6653-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="f6653-215">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f6653-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="f6653-216">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f6653-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="f6653-217">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f6653-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="f6653-218">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f6653-218">Click **Next**.</span></span>

7. <span data-ttu-id="f6653-219">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="f6653-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f6653-221">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f6653-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="f6653-223">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="f6653-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="f6653-224">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="f6653-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="f6653-225">Creare un utente test di SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="f6653-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="f6653-226">Questa sezione descrive come creare un utente chiamato Britta Simon in SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="f6653-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="f6653-227">Britta deve avere un ID SSO, a volte definito *AuthParam*, che corrisponde al valore **emailaddress** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6653-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="f6653-228">**Per creare un utente test denominato Britta Simon in SilkRoad Life Suite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f6653-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="f6653-229">Chiedere al team di supporto di SilkRoad Life Suite di creare un utente con un valore per l'attributo **SSO ID** equivalente all'**indirizzo di posta elettronica**di Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6653-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f6653-230">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6653-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="f6653-231">Questa sezione descrive come abilitare Britta Simon all'uso dell'accesso SSO di Azure concedendole l'accesso a SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="f6653-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f6653-233">**Per assegnare Britta Simon a SilkRoad Life Suite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f6653-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="f6653-234">Per aprire la visualizzazione applicazioni nel portale di Azure classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="f6653-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assegna utente][201] 

2. <span data-ttu-id="f6653-236">Nell'elenco delle applicazioni selezionare **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="f6653-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Assegna utente][202] 

3. <span data-ttu-id="f6653-238">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="f6653-238">In the menu on the top, click **Users**.</span></span>
   
    ![Assegna utente][203] 

4. <span data-ttu-id="f6653-240">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f6653-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="f6653-241">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="f6653-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="f6653-243">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f6653-243">Test single sign-on</span></span>
<span data-ttu-id="f6653-244">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f6653-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="f6653-245">Quando si fa clic sul riquadro SilkRoad Life Suite nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="f6653-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6653-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f6653-246">Additional Resources</span></span>
* [<span data-ttu-id="f6653-247">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6653-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6653-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6653-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png






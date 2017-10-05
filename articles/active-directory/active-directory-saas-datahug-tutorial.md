---
title: 'Esercitazione: integrazione di Azure Active Directory con Datahug | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Datahug.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="af0bf-103">Esercitazione: Integrazione di Azure Active Directory con Datahug</span><span class="sxs-lookup"><span data-stu-id="af0bf-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="af0bf-104">Questa esercitazione descrive come integrare Datahug con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af0bf-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af0bf-105">L'integrazione di Datahug con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="af0bf-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="af0bf-106">È possibile controllare in Azure AD chi può accedere a Datahug.</span><span class="sxs-lookup"><span data-stu-id="af0bf-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="af0bf-107">È possibile abilitare gli utenti per l'accesso automatico a Datahug (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0bf-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="af0bf-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="af0bf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="af0bf-109">Per altre informazioni sull'integrazione di app SaaS con Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="af0bf-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="af0bf-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af0bf-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af0bf-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="af0bf-111">Prerequisites</span></span>

<span data-ttu-id="af0bf-112">Per configurare l'integrazione di Azure AD con Datahug, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="af0bf-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="af0bf-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0bf-113">An Azure AD subscription</span></span>
- <span data-ttu-id="af0bf-114">Sottoscrizione di Datahug abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="af0bf-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af0bf-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="af0bf-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af0bf-116">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="af0bf-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af0bf-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="af0bf-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="af0bf-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af0bf-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af0bf-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="af0bf-119">Scenario description</span></span>
<span data-ttu-id="af0bf-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="af0bf-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af0bf-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="af0bf-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af0bf-122">Aggiunta di Datahug dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="af0bf-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="af0bf-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0bf-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="af0bf-124">Aggiunta di Datahug dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="af0bf-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="af0bf-125">Per configurare l'integrazione di Datahug in Azure AD, è necessario aggiungere Datahug dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="af0bf-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="af0bf-126">**Per aggiungere Datahug dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="af0bf-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="af0bf-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="af0bf-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="af0bf-129">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="af0bf-130">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-130">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="af0bf-132">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="af0bf-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="af0bf-134">Nella casella di ricerca digitare **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-134">In the search box, type **Datahug**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="af0bf-136">Nel pannello dei risultati selezionare **Datahug** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="af0bf-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="af0bf-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0bf-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="af0bf-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Datahug in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="af0bf-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="af0bf-140">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Datahug che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0bf-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="af0bf-141">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Datahug.</span><span class="sxs-lookup"><span data-stu-id="af0bf-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="af0bf-142">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD come valore dell'attributo **Username** in Datahug.</span><span class="sxs-lookup"><span data-stu-id="af0bf-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="af0bf-143">Per configurare e testare l'accesso Single Sign-On di Azure AD con Datahug, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="af0bf-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="af0bf-144">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="af0bf-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="af0bf-145">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af0bf-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af0bf-146">**[Creazione di un utente test di Datahug](#creating-a-datahug-test-user)**: per avere una controparte di Britta Simon in Datahug collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="af0bf-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="af0bf-147">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0bf-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af0bf-148">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="af0bf-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="af0bf-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0bf-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="af0bf-150">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Datahug.</span><span class="sxs-lookup"><span data-stu-id="af0bf-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="af0bf-151">**Per configurare Single Sign-On di Azure AD con Datahug, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="af0bf-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="af0bf-152">Nella pagina di integrazione dell'applicazione **Datahug** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="af0bf-154">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="af0bf-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="af0bf-156">Nella sezione **URL e dominio Datahug**, se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="af0bf-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="af0bf-158">a.</span><span class="sxs-lookup"><span data-stu-id="af0bf-158">a.</span></span> <span data-ttu-id="af0bf-159">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="af0bf-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="af0bf-160">b.</span><span class="sxs-lookup"><span data-stu-id="af0bf-160">b.</span></span> <span data-ttu-id="af0bf-161">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="af0bf-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="af0bf-162">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="af0bf-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="af0bf-163">se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="af0bf-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="af0bf-165">Nella casella di testo **URL di accesso** digitare l'URL come: `https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="af0bf-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="af0bf-166">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="af0bf-166">These values are not the real.</span></span> <span data-ttu-id="af0bf-167">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="af0bf-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="af0bf-168">In questo caso, è consigliabile usare in Identificatore e in URL di risposta il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="af0bf-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="af0bf-169">Per ottenere questi valori, contattare il [team di supporto clienti di Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="af0bf-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="af0bf-170">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="af0bf-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="af0bf-172">Selezionare **Mostra impostazioni avanzate per la firma di certificati** ed eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af0bf-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="af0bf-174">a.</span><span class="sxs-lookup"><span data-stu-id="af0bf-174">a.</span></span> <span data-ttu-id="af0bf-175">In **Opzione di firma**, selezionare **Firma asserzione SAML**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="af0bf-176">b.</span><span class="sxs-lookup"><span data-stu-id="af0bf-176">b.</span></span> <span data-ttu-id="af0bf-177">In **Algoritmo di firma**, selezionare **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="af0bf-178">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="af0bf-178">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="af0bf-180">Nella sezione **Configurazione di Datahug** fare clic su **Configura Datahug** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="af0bf-181">Copiare l'**ID di entità SAML** e **l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="af0bf-183">Per configurare l'accesso Single Sign-On sul lato **Datahug**, è necessario inviare il **file XML dei metadati**, l'**ID entità SAML** e l'**URL del servizio Single Sign-On SAML** al [supporto Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="af0bf-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="af0bf-184">L'applicazione verrà configurata in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="af0bf-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="af0bf-185">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="af0bf-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="af0bf-186">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="af0bf-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="af0bf-187">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af0bf-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="af0bf-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0bf-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="af0bf-189">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="af0bf-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="af0bf-191">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af0bf-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="af0bf-192">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="af0bf-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="af0bf-194">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="af0bf-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="af0bf-196">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="af0bf-198">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="af0bf-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="af0bf-200">a.</span><span class="sxs-lookup"><span data-stu-id="af0bf-200">a.</span></span> <span data-ttu-id="af0bf-201">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af0bf-202">b.</span><span class="sxs-lookup"><span data-stu-id="af0bf-202">b.</span></span> <span data-ttu-id="af0bf-203">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="af0bf-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af0bf-204">c.</span><span class="sxs-lookup"><span data-stu-id="af0bf-204">c.</span></span> <span data-ttu-id="af0bf-205">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="af0bf-206">d.</span><span class="sxs-lookup"><span data-stu-id="af0bf-206">d.</span></span> <span data-ttu-id="af0bf-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="af0bf-208">Creazione di un utente test di Datahug</span><span class="sxs-lookup"><span data-stu-id="af0bf-208">Creating a Datahug test user</span></span>

<span data-ttu-id="af0bf-209">Per consentire agli utenti di Azure AD di accedere ad Datahug, è necessario eseguirne il provisioning in Datahug.</span><span class="sxs-lookup"><span data-stu-id="af0bf-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="af0bf-210">In Datahug il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="af0bf-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="af0bf-211">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="af0bf-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="af0bf-212">Accedere al sito aziendale di Datahug come amministratore.</span><span class="sxs-lookup"><span data-stu-id="af0bf-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="af0bf-213">Passare il puntatore sull'**ingranaggio** nell'angolo superiore destro e fare clic su **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="af0bf-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![Aggiungere un dipendente](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="af0bf-215">Scegliere **Persone** e fare clic sulla scheda **Aggiungi utenti**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-215">Choose **People** and click the **Add Users** tab</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="af0bf-217">Digitare l'indirizzo di posta elettronica della persona per la quale si vuole creare un account e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="af0bf-219">È possibile inviare all'utente un messaggio di registrazione selezionando la casella di controllo **Invia messaggio di benvenuto**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="af0bf-220">Se si sta creando un account di Salesforce non inviare il messaggio di benvenuto.</span><span class="sxs-lookup"><span data-stu-id="af0bf-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="af0bf-221">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0bf-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="af0bf-222">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Datahug.</span><span class="sxs-lookup"><span data-stu-id="af0bf-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![Assegna utente][200] 

<span data-ttu-id="af0bf-224">**Per assegnare Britta Simon a Datahug, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="af0bf-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="af0bf-225">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="af0bf-227">Nell'elenco delle applicazioni selezionare **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-227">In the applications list, select **Datahug**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="af0bf-229">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="af0bf-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="af0bf-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-231">Click **Add** button.</span></span> <span data-ttu-id="af0bf-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="af0bf-234">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="af0bf-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="af0bf-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af0bf-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af0bf-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="af0bf-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="af0bf-237">Testing single sign-on</span></span>

<span data-ttu-id="af0bf-238">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="af0bf-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="af0bf-239">Quando si fa clic sul riquadro Datahug nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Datahug.</span><span class="sxs-lookup"><span data-stu-id="af0bf-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="af0bf-240">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="af0bf-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="af0bf-241">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="af0bf-241">Additional resources</span></span>

* [<span data-ttu-id="af0bf-242">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af0bf-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af0bf-243">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af0bf-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png


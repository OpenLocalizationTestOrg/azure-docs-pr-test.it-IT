---
title: 'Esercitazione: Integrazione di Azure Active Directory con Front | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Front.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="3e02a-103">Esercitazione: Integrazione di Azure Active Directory con Front</span><span class="sxs-lookup"><span data-stu-id="3e02a-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="3e02a-104">Questa esercitazione descrive come integrare Front con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e02a-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e02a-105">L'integrazione di Front con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e02a-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e02a-106">È possibile controllare in Azure AD chi può accedere a Front.</span><span class="sxs-lookup"><span data-stu-id="3e02a-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="3e02a-107">È possibile abilitare gli utenti per l'accesso automatico a Front (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="3e02a-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3e02a-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e02a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3e02a-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e02a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e02a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3e02a-110">Prerequisites</span></span>

<span data-ttu-id="3e02a-111">Per configurare l'integrazione di Azure AD con Front, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e02a-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="3e02a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e02a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e02a-113">Sottoscrizione di Front abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e02a-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e02a-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3e02a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e02a-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e02a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e02a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3e02a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e02a-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e02a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e02a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3e02a-118">Scenario description</span></span>
<span data-ttu-id="3e02a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3e02a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e02a-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e02a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e02a-121">Aggiunta di Front dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3e02a-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="3e02a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e02a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="3e02a-123">Aggiunta di Front dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3e02a-123">Adding Front from the gallery</span></span>
<span data-ttu-id="3e02a-124">Per configurare l'integrazione di Front in Azure AD, è necessario aggiungere Front dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3e02a-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e02a-125">**Per aggiungere Front dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3e02a-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e02a-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3e02a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="3e02a-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e02a-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="3e02a-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e02a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="3e02a-133">Nella casella di ricerca digitare **Front**, selezionare **Front** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e02a-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Front nell'elenco risultati](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3e02a-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e02a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3e02a-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Front usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3e02a-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e02a-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Front corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e02a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="3e02a-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Front.</span><span class="sxs-lookup"><span data-stu-id="3e02a-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="3e02a-139">Per stabilire la relazione di collegamento, in Front assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="3e02a-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3e02a-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Front, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3e02a-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e02a-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3e02a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e02a-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e02a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e02a-143">**[Creare un utente di test di Front](#create-a-front-test-user)**: per avere una controparte di Britta Simon in Front collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e02a-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e02a-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e02a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e02a-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="3e02a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3e02a-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e02a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3e02a-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Front.</span><span class="sxs-lookup"><span data-stu-id="3e02a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="3e02a-148">**Per configurare Single Sign-On di Azure AD con Front, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3e02a-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="3e02a-149">Nella pagina di integrazione dell'applicazione **Front** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3e02a-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3e02a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="3e02a-153">Nella sezione **URL e dominio Front** seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="3e02a-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="3e02a-155">a.</span><span class="sxs-lookup"><span data-stu-id="3e02a-155">a.</span></span> <span data-ttu-id="3e02a-156">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="3e02a-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="3e02a-157">b.</span><span class="sxs-lookup"><span data-stu-id="3e02a-157">b.</span></span> <span data-ttu-id="3e02a-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="3e02a-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="3e02a-159">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="3e02a-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="3e02a-161">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="3e02a-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3e02a-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="3e02a-162">These values are not real.</span></span> <span data-ttu-id="3e02a-163">Aggiornare questi valori con identificatore, URL di risposta e URL di accesso effettivi, illustrati più avanti in questa esercitazione, oppure contattare il [team di supporto clienti di Front](mailto:support@frontapp.com) per ottenere questi valori.</span><span class="sxs-lookup"><span data-stu-id="3e02a-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="3e02a-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="3e02a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="3e02a-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3e02a-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3e02a-168">Nella sezione **Configurazione di Front** fare clic su **Configura Front** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3e02a-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="3e02a-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="3e02a-171">Accedere al tenant di Front come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3e02a-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="3e02a-172">Passare a **Impostazioni (l'icona dell'ingranaggio in fondo all'intestazione laterale a sinistra) > Preferenze**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="3e02a-174">Fare clic sul collegamento **Single Sign On** .</span><span class="sxs-lookup"><span data-stu-id="3e02a-174">Click **Single Sign On** link.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="3e02a-176">Selezionare **SAML** nell'elenco a discesa **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="3e02a-178">Nella casella di testo **Entry Point** (Punto di ingresso) inserire il valore di **URL servizio Single Sign-On** dalla configurazione guidata dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e02a-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="3e02a-180">Aprire il file del **certificato (Base64)** scaricato nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Certificato di firma**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="3e02a-182">Nella sezione **Service provider settings** (Impostazioni provider di servizi) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3e02a-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="3e02a-184">a.</span><span class="sxs-lookup"><span data-stu-id="3e02a-184">a.</span></span> <span data-ttu-id="3e02a-185">Copiare il valore dell'**ID entità** e incollarlo nella casella di testo **Identificatore** nella sezione **URL e dominio Front** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e02a-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="3e02a-186">b.</span><span class="sxs-lookup"><span data-stu-id="3e02a-186">b.</span></span> <span data-ttu-id="3e02a-187">Copiare il valore dell'**URL ACS** e incollarlo nella casella di testo **URL di accesso** nella sezione **URL e dominio Front** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e02a-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="3e02a-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3e02a-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="3e02a-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="3e02a-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e02a-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="3e02a-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e02a-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e02a-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3e02a-192">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e02a-192">Create an Azure AD test user</span></span>

<span data-ttu-id="3e02a-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e02a-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="3e02a-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e02a-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e02a-196">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="3e02a-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3e02a-198">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3e02a-200">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3e02a-202">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3e02a-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3e02a-204">a.</span><span class="sxs-lookup"><span data-stu-id="3e02a-204">a.</span></span> <span data-ttu-id="3e02a-205">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e02a-206">b.</span><span class="sxs-lookup"><span data-stu-id="3e02a-206">b.</span></span> <span data-ttu-id="3e02a-207">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e02a-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3e02a-208">c.</span><span class="sxs-lookup"><span data-stu-id="3e02a-208">c.</span></span> <span data-ttu-id="3e02a-209">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3e02a-210">d.</span><span class="sxs-lookup"><span data-stu-id="3e02a-210">d.</span></span> <span data-ttu-id="3e02a-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="3e02a-212">Creare un utente test di Front</span><span class="sxs-lookup"><span data-stu-id="3e02a-212">Create a Front test user</span></span>

<span data-ttu-id="3e02a-213">In questa sezione viene creato un utente di nome Britta Simon in Front.</span><span class="sxs-lookup"><span data-stu-id="3e02a-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="3e02a-214">Collaborare con il [team di supporto clienti di Front](mailto:support@frontapp.com) per aggiungere gli utenti nella piattaforma Front.</span><span class="sxs-lookup"><span data-stu-id="3e02a-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="3e02a-215">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3e02a-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3e02a-216">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e02a-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="3e02a-217">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Front.</span><span class="sxs-lookup"><span data-stu-id="3e02a-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="3e02a-219">**Per assegnare Britta Simon a Front, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3e02a-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="3e02a-220">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3e02a-222">Nell'elenco delle applicazioni, selezionare **Front**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-222">In the applications list, select **Front**.</span></span>

    ![Collegamento di Front nell'elenco delle applicazioni](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="3e02a-224">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3e02a-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="3e02a-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-226">Click **Add** button.</span></span> <span data-ttu-id="3e02a-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="3e02a-229">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="3e02a-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e02a-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e02a-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e02a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3e02a-232">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e02a-232">Test single sign-on</span></span>

<span data-ttu-id="3e02a-233">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-on di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3e02a-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="3e02a-234">Quando si fa clic sul riquadro Front nel pannello di accesso, si accederà automaticamente all'applicazione Front.</span><span class="sxs-lookup"><span data-stu-id="3e02a-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3e02a-235">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3e02a-235">Additional resources</span></span>

* [<span data-ttu-id="3e02a-236">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e02a-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e02a-237">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e02a-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png


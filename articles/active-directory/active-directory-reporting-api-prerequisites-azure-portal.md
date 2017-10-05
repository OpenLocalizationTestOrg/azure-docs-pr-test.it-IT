---
title: Prerequisiti di accesso all'API di creazione report di Azure AD | Microsoft Docs
description: Informazioni sui prerequisiti di accesso all'API di creazione report di Azure AD
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5fafd83c337e3c73260d89cdad7409a01ce5855b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="32d92-103">Prerequisiti di accesso all'API di creazione report di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32d92-103">Prerequisites to access the Azure AD reporting API</span></span>

<span data-ttu-id="32d92-104">Le [API di creazione report di Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) forniscono l'accesso ai dati dal codice tramite un set di API basate su REST.</span><span class="sxs-lookup"><span data-stu-id="32d92-104">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="32d92-105">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="32d92-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="32d92-106">L'API di creazione report usa l'autenticazione [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) per autorizzare l'accesso alle API Web.</span><span class="sxs-lookup"><span data-stu-id="32d92-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="32d92-107">Per accedere ai dati di creazione dei report tramite l'API, è necessario disporre di uno dei seguenti ruoli assegnati:</span><span class="sxs-lookup"><span data-stu-id="32d92-107">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="32d92-108">Ruolo con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="32d92-108">Security Reader</span></span>
- <span data-ttu-id="32d92-109">Amministrazione della protezione</span><span class="sxs-lookup"><span data-stu-id="32d92-109">Security Admin</span></span>
- <span data-ttu-id="32d92-110">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="32d92-110">Global Admin</span></span>


<span data-ttu-id="32d92-111">Per preparare l'accesso all'API di creazione report, è necessario:</span><span class="sxs-lookup"><span data-stu-id="32d92-111">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="32d92-112">Registrare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="32d92-112">Register an application</span></span> 
2. <span data-ttu-id="32d92-113">Concedere le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="32d92-113">Grant permissions</span></span> 
3. <span data-ttu-id="32d92-114">Ottenere le impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="32d92-114">Gather configuration settings</span></span> 

<span data-ttu-id="32d92-115">Per domande, problemi o suggerimenti, [inviare un ticket di supporto](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="32d92-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="32d92-116">Registrare un'applicazione Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32d92-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="32d92-117">È necessario registrare un'app, anche se si accede all'API di creazione dei report tramite uno script.</span><span class="sxs-lookup"><span data-stu-id="32d92-117">You need to register an app even if you are accessing the reporting API using a script.</span></span> <span data-ttu-id="32d92-118">Questo consente di avere un **ID applicazione** necessario per una chiamata di autorizzazione e consente al codice di ricevere i token.</span><span class="sxs-lookup"><span data-stu-id="32d92-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="32d92-119">Per configurare la directory per l'accesso all'API di creazione report di Azure AD, è necessario accedere al portale di Azure con un account di amministratore di Azure che è anche membro del ruolo di directory **Amministratore globale** nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32d92-119">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32d92-120">Le applicazioni eseguite con credenziali con privilegi "admin" come questa possono essere molto potenti, quindi assicurarsi di proteggere l'ID e il segreto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32d92-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="32d92-121">**Per registrare un'applicazione Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="32d92-121">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="32d92-122">Nel [portale di Azure ](https://portal.azure.com)fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32d92-122">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="32d92-124">Nel pannello **Azure Active Directory** fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="32d92-124">On the **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="32d92-126">Nel pannello **Registrazioni per l'app** nella barra degli strumenti nella parte superiore fare clic su **Registrazione nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="32d92-126">On the **App registrations** blade, in the toolbar on the top, click **New application registration**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="32d92-128">Nel pannello **Crea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32d92-128">On the **Create** blade, perform the following steps:</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="32d92-130">a.</span><span class="sxs-lookup"><span data-stu-id="32d92-130">a.</span></span> <span data-ttu-id="32d92-131">Nella casella di testo **Nome** digitare `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="32d92-131">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="32d92-132">b.</span><span class="sxs-lookup"><span data-stu-id="32d92-132">b.</span></span> <span data-ttu-id="32d92-133">Per **Tipo di applicazione** selezionare **App Web/API**.</span><span class="sxs-lookup"><span data-stu-id="32d92-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="32d92-134">c.</span><span class="sxs-lookup"><span data-stu-id="32d92-134">c.</span></span> <span data-ttu-id="32d92-135">Nella casella di testo **URL di accesso** digitare `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="32d92-135">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="32d92-136">d.</span><span class="sxs-lookup"><span data-stu-id="32d92-136">d.</span></span> <span data-ttu-id="32d92-137">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="32d92-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="32d92-138">Concedere le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="32d92-138">Grant permissions</span></span> 

<span data-ttu-id="32d92-139">L'obiettivo di questo passaggio è concedere le autorizzazioni **Legge i dati della directory** dell'applicazione all'API di **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32d92-139">The objective of this step is to grant your application **Read directory data** permissions to the **Windows Azure Active Directory** API.</span></span>

![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="32d92-141">**Per concedere l'autorizzazione dell'applicazione per l'uso dell'API:**</span><span class="sxs-lookup"><span data-stu-id="32d92-141">**To grant your application permission to use the API:**</span></span>

1. <span data-ttu-id="32d92-142">Nel pannello **Registrazioni per l'app** dell'elenco delle app fare clic su **Reporting API application** (Creazione di report per l'applicazione dell'API).</span><span class="sxs-lookup"><span data-stu-id="32d92-142">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="32d92-143">Nel pannello **Reporting API application** (Creazione di report per l'applicazione dell'API) fare clic su **Impostazioni** nella barra degli strumenti nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="32d92-143">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="32d92-145">Nel pannello delle **Impostazioni** fare clic su **Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="32d92-145">On the **Settings** blade, click **Required permissions**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="32d92-147">Nel pannello **Autorizzazioni necessarie** fare clic su Windows **Azure Active Directory** nell'elenco delle **API**.</span><span class="sxs-lookup"><span data-stu-id="32d92-147">On the **Required permissions** blade, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="32d92-149">Nel pannello **Abilita accesso** selezionare **Legge i dati della directory**.</span><span class="sxs-lookup"><span data-stu-id="32d92-149">On the **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="32d92-151">Nel barra degli strumenti in alto fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="32d92-151">In the toolbar on the top, click **Save**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="32d92-153">Ottenere le impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="32d92-153">Gather configuration settings</span></span> 
<span data-ttu-id="32d92-154">Questa sezione illustra come ottenere le impostazioni seguenti dalla directory:</span><span class="sxs-lookup"><span data-stu-id="32d92-154">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="32d92-155">Nome di dominio</span><span class="sxs-lookup"><span data-stu-id="32d92-155">Domain name</span></span>
* <span data-ttu-id="32d92-156">ID client</span><span class="sxs-lookup"><span data-stu-id="32d92-156">Client ID</span></span>
* <span data-ttu-id="32d92-157">Segreto client</span><span class="sxs-lookup"><span data-stu-id="32d92-157">Client secret</span></span>

<span data-ttu-id="32d92-158">Questi valori sono necessari quando si configurano le chiamate all'API di creazione report.</span><span class="sxs-lookup"><span data-stu-id="32d92-158">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="32d92-159">Ottenere il nome di dominio</span><span class="sxs-lookup"><span data-stu-id="32d92-159">Get your domain name</span></span>

<span data-ttu-id="32d92-160">**Per ottenere il nome di dominio:**</span><span class="sxs-lookup"><span data-stu-id="32d92-160">**To get your domain name:**</span></span>

1. <span data-ttu-id="32d92-161">Nel [portale di Azure ](https://portal.azure.com)fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32d92-161">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="32d92-163">Nel pannello **Azure Active Directory** fare clic su **Nomi di dominio**.</span><span class="sxs-lookup"><span data-stu-id="32d92-163">On the **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="32d92-165">Copiare il nome del dominio dall'elenco dei domini.</span><span class="sxs-lookup"><span data-stu-id="32d92-165">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="32d92-166">Ottenere l'ID client dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="32d92-166">Get your application's client ID</span></span>

<span data-ttu-id="32d92-167">**Per ottenere l'ID client dell'applicazione:**</span><span class="sxs-lookup"><span data-stu-id="32d92-167">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="32d92-168">Nel [portale di Azure ](https://portal.azure.com)fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32d92-168">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="32d92-170">Nel pannello **Registrazioni per l'app** dell'elenco delle app fare clic su **Reporting API application** (Creazione di report per l'applicazione dell'API).</span><span class="sxs-lookup"><span data-stu-id="32d92-170">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="32d92-171">Nel pannello **Reporting API application** (Creazione di report per l'applicazione dell'API) fare clic su **Fare clic per copiare** nell'**ID applicazione**.</span><span class="sxs-lookup"><span data-stu-id="32d92-171">On the **Reporting API application** blade, at the **Application ID**, click **Click to copy**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="32d92-173">Ottenere il segreto client dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="32d92-173">Get your application's client secret</span></span>
<span data-ttu-id="32d92-174">Per ottenere il segreto client dell'applicazione, è necessario creare una nuova chiave e salvare il relativo valore durante il salvataggio della nuova chiave perché non è più possibile recuperare il valore in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="32d92-174">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="32d92-175">**Per ottenere il segreto client dell'applicazione:**</span><span class="sxs-lookup"><span data-stu-id="32d92-175">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="32d92-176">Nel [portale di Azure ](https://portal.azure.com)fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32d92-176">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="32d92-178">Nel pannello **Registrazioni per l'app** dell'elenco delle app fare clic su **Reporting API application** (Creazione di report per l'applicazione dell'API).</span><span class="sxs-lookup"><span data-stu-id="32d92-178">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="32d92-179">Nel pannello **Reporting API application** (Creazione di report per l'applicazione dell'API) fare clic su **Impostazioni** nella barra degli strumenti nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="32d92-179">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="32d92-181">Nel pannello **Impostazioni**fare clic su **Chiavi**  nella sezione **APIR Access** (Accesso APIR).</span><span class="sxs-lookup"><span data-stu-id="32d92-181">On the **Settings** blade, in the **APIR Access** section, click **Keys**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="32d92-183">Nel pannello **Chiavi** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32d92-183">On the **Keys** blade, perform the following steps:</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="32d92-185">a.</span><span class="sxs-lookup"><span data-stu-id="32d92-185">a.</span></span> <span data-ttu-id="32d92-186">Nella casella di testo **Descrizione** digitare `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="32d92-186">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="32d92-187">b.</span><span class="sxs-lookup"><span data-stu-id="32d92-187">b.</span></span> <span data-ttu-id="32d92-188">Per **Scadenza** selezionare **In 2 years** (In 2 anni).</span><span class="sxs-lookup"><span data-stu-id="32d92-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="32d92-189">c.</span><span class="sxs-lookup"><span data-stu-id="32d92-189">c.</span></span> <span data-ttu-id="32d92-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="32d92-190">Click **Save**.</span></span>

    <span data-ttu-id="32d92-191">d.</span><span class="sxs-lookup"><span data-stu-id="32d92-191">d.</span></span> <span data-ttu-id="32d92-192">Copiare il valore della chiave.</span><span class="sxs-lookup"><span data-stu-id="32d92-192">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="32d92-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32d92-193">Next Steps</span></span>
* <span data-ttu-id="32d92-194">Si desidera accedere ai dati dall'API di creazione report di Azure AD mediante il codice?</span><span class="sxs-lookup"><span data-stu-id="32d92-194">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="32d92-195">Vedere [Introduzione all'API di creazione report di Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="32d92-195">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="32d92-196">Per altre informazioni sulla creazione di report di Azure Active Directory, vedere [Guida alla creazione di report in Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="32d92-196">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  


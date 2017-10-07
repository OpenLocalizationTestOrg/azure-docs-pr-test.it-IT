---
title: aaaPrerequisites tooaccess hello Azure AD reporting API | Documenti Microsoft
description: Informazioni sulle API reporting di hello prerequisiti tooaccess hello Azure AD
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
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="40424-103">Prerequisiti tooaccess hello Azure AD API di creazione di report</span><span class="sxs-lookup"><span data-stu-id="40424-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="40424-104">Hello [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornire i dati di toohello accesso a livello di codice tramite un set di API basata su REST.</span><span class="sxs-lookup"><span data-stu-id="40424-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="40424-105">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="40424-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="40424-106">Hello reporting Usa API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) web toohello di tooauthorize accesso API.</span><span class="sxs-lookup"><span data-stu-id="40424-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="40424-107">tooget accedere toohello segnalazione dei dati tramite l'API di hello, è necessario toohave uno dei seguenti ruoli assegnati hello:</span><span class="sxs-lookup"><span data-stu-id="40424-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="40424-108">Ruolo con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="40424-108">Security Reader</span></span>
- <span data-ttu-id="40424-109">Amministrazione della protezione</span><span class="sxs-lookup"><span data-stu-id="40424-109">Security Admin</span></span>
- <span data-ttu-id="40424-110">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="40424-110">Global Admin</span></span>


<span data-ttu-id="40424-111">tooprepare toohello l'accesso API di report, è necessario:</span><span class="sxs-lookup"><span data-stu-id="40424-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="40424-112">Registrare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="40424-112">Register an application</span></span> 
2. <span data-ttu-id="40424-113">Concedere le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="40424-113">Grant permissions</span></span> 
3. <span data-ttu-id="40424-114">Ottenere le impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="40424-114">Gather configuration settings</span></span> 

<span data-ttu-id="40424-115">Per domande, problemi o suggerimenti, [inviare un ticket di supporto](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="40424-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="40424-116">Registrare un'applicazione Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40424-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="40424-117">Anche se si accede hello API tramite uno script di segnalazione, è necessario tooregister un'app.</span><span class="sxs-lookup"><span data-stu-id="40424-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="40424-118">Ciò consente un **ID applicazione**, che è necessario per una chiamata di autorizzazione e consente il token tooreceive di codice.</span><span class="sxs-lookup"><span data-stu-id="40424-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="40424-119">tooconfigure la directory tooaccess hello Azure AD reporting API, è necessario accedere toohello portale di Azure con un account amministratore di Azure che è anche un membro di hello **amministratore globale** ruolo della directory nel tenant di Azure AD .</span><span class="sxs-lookup"><span data-stu-id="40424-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40424-120">Le applicazioni in esecuzione con le credenziali con privilegi "admin" simile al seguente possono essere molto potente, pertanto essere protetto le credenziali ID/chiave privata che tookeep hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40424-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="40424-121">**tooregister un'applicazione Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="40424-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="40424-122">In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40424-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="40424-124">In hello **Azure Active Directory** pannello, fare clic su **registrazioni di App**.</span><span class="sxs-lookup"><span data-stu-id="40424-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="40424-126">In hello **registrazioni di App** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **nuova registrazione applicazione**.</span><span class="sxs-lookup"><span data-stu-id="40424-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="40424-128">In hello **crea** pannello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="40424-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="40424-130">a.</span><span class="sxs-lookup"><span data-stu-id="40424-130">a.</span></span> <span data-ttu-id="40424-131">In hello **nome** casella tipo `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="40424-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="40424-132">b.</span><span class="sxs-lookup"><span data-stu-id="40424-132">b.</span></span> <span data-ttu-id="40424-133">Per **Tipo di applicazione** selezionare **App Web/API**.</span><span class="sxs-lookup"><span data-stu-id="40424-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="40424-134">c.</span><span class="sxs-lookup"><span data-stu-id="40424-134">c.</span></span> <span data-ttu-id="40424-135">In hello **Sign-on URL** casella tipo `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="40424-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="40424-136">d.</span><span class="sxs-lookup"><span data-stu-id="40424-136">d.</span></span> <span data-ttu-id="40424-137">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="40424-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="40424-138">Concedere le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="40424-138">Grant permissions</span></span> 

<span data-ttu-id="40424-139">obiettivo Hello di questo passaggio è l'applicazione di toogrant **lettura dati directory** autorizzazioni toohello **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="40424-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="40424-141">**toogrant hello di toouse l'autorizzazione applicazione API:**</span><span class="sxs-lookup"><span data-stu-id="40424-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="40424-142">In hello **registrazioni di App** pannello, nell'elenco di App hello, fare clic su **applicazione API Reporting**.</span><span class="sxs-lookup"><span data-stu-id="40424-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="40424-143">In hello **applicazione API Reporting** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="40424-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="40424-145">In hello **impostazioni** pannello, fare clic su **delle autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="40424-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="40424-147">In hello **delle autorizzazioni necessarie** pannello in hello **API** elenco, fare clic su **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40424-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="40424-149">In hello **Abilita accesso** pannello seleziona **lettura dati directory**.</span><span class="sxs-lookup"><span data-stu-id="40424-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="40424-151">Nella barra degli strumenti hello in primo piano hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="40424-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="40424-153">Ottenere le impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="40424-153">Gather configuration settings</span></span> 
<span data-ttu-id="40424-154">In questa sezione illustra come hello tooget seguendo le impostazioni dalla directory:</span><span class="sxs-lookup"><span data-stu-id="40424-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="40424-155">Nome di dominio</span><span class="sxs-lookup"><span data-stu-id="40424-155">Domain name</span></span>
* <span data-ttu-id="40424-156">ID client</span><span class="sxs-lookup"><span data-stu-id="40424-156">Client ID</span></span>
* <span data-ttu-id="40424-157">Segreto client</span><span class="sxs-lookup"><span data-stu-id="40424-157">Client secret</span></span>

<span data-ttu-id="40424-158">Questi valori è necessario quando si configurano le chiamate API di creazione report toohello.</span><span class="sxs-lookup"><span data-stu-id="40424-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="40424-159">Ottenere il nome di dominio</span><span class="sxs-lookup"><span data-stu-id="40424-159">Get your domain name</span></span>

<span data-ttu-id="40424-160">**tooget il nome di dominio:**</span><span class="sxs-lookup"><span data-stu-id="40424-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="40424-161">In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40424-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="40424-163">In hello **Azure Active Directory** pannello, fare clic su **i nomi di dominio**.</span><span class="sxs-lookup"><span data-stu-id="40424-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="40424-165">Copiare il nome di dominio dall'elenco di hello dei domini.</span><span class="sxs-lookup"><span data-stu-id="40424-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="40424-166">Ottenere l'ID client dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="40424-166">Get your application's client ID</span></span>

<span data-ttu-id="40424-167">**tooget ID client dell'applicazione:**</span><span class="sxs-lookup"><span data-stu-id="40424-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="40424-168">In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40424-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="40424-170">In hello **registrazioni di App** pannello, nell'elenco di App hello, fare clic su **applicazione API Reporting**.</span><span class="sxs-lookup"><span data-stu-id="40424-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="40424-171">In hello **applicazione API Reporting** server blade, hello **ID applicazione**, fare clic su **fare clic su toocopy**.</span><span class="sxs-lookup"><span data-stu-id="40424-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="40424-173">Ottenere il segreto client dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="40424-173">Get your application's client secret</span></span>
<span data-ttu-id="40424-174">tooget client dell'applicazione privata, è necessario toocreate una nuova chiave e salvare il relativo valore quando si salvano nuova chiave hello perché non è possibile tooretrieve questo valore in un secondo momento più.</span><span class="sxs-lookup"><span data-stu-id="40424-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="40424-175">**tooget segreto client dell'applicazione:**</span><span class="sxs-lookup"><span data-stu-id="40424-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="40424-176">In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40424-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="40424-178">In hello **registrazioni di App** pannello, nell'elenco di App hello, fare clic su **applicazione API Reporting**.</span><span class="sxs-lookup"><span data-stu-id="40424-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="40424-179">In hello **applicazione API Reporting** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="40424-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="40424-181">In hello **impostazioni** pannello in hello **APIR accesso** fare clic su **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="40424-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="40424-183">In hello **chiavi** pannello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="40424-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="40424-185">a.</span><span class="sxs-lookup"><span data-stu-id="40424-185">a.</span></span> <span data-ttu-id="40424-186">In hello **descrizione** casella tipo `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="40424-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="40424-187">b.</span><span class="sxs-lookup"><span data-stu-id="40424-187">b.</span></span> <span data-ttu-id="40424-188">Per **Scadenza** selezionare **In 2 years** (In 2 anni).</span><span class="sxs-lookup"><span data-stu-id="40424-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="40424-189">c.</span><span class="sxs-lookup"><span data-stu-id="40424-189">c.</span></span> <span data-ttu-id="40424-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="40424-190">Click **Save**.</span></span>

    <span data-ttu-id="40424-191">d.</span><span class="sxs-lookup"><span data-stu-id="40424-191">d.</span></span> <span data-ttu-id="40424-192">Copia valore chiave hello.</span><span class="sxs-lookup"><span data-stu-id="40424-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="40424-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40424-193">Next Steps</span></span>
* <span data-ttu-id="40424-194">È ad esempio tooaccess hello dati da Azure AD hello sarebbe reporting API in modo a livello di codice?</span><span class="sxs-lookup"><span data-stu-id="40424-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="40424-195">Estrarre [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="40424-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="40424-196">Se si desidera toofind ulteriori informazioni sui report di Azure Active Directory, vedere hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="40424-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  


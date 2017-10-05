---
title: Uso di System for Cross-Domain Identity Management per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory ad applicazioni | Microsoft Docs
description: "Azure Active Directory può effettuare automaticamente il provisioning di utenti e gruppi in qualsiasi applicazione o archivio identità gestito da un servizio Web con interfaccia definita nella specifica del protocollo SCIM"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="c052f-103">Uso di System for Cross-Domain Identity Management per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory ad applicazioni</span><span class="sxs-lookup"><span data-stu-id="c052f-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="c052f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c052f-104">Overview</span></span>
<span data-ttu-id="c052f-105">Azure Active Directory (Azure AD) può effettuare automaticamente il provisioning di utenti e gruppi in qualsiasi applicazione o archivio identità gestito da un servizio Web con interfaccia definita nella [specifica del protocollo System for Cross-Domain Identity Management (SCIM) 2.0](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="c052f-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="c052f-106">Azure Active Directory può inviare richieste per creare, modificare o eliminare utenti e gruppi assegnati al servizio Web,</span><span class="sxs-lookup"><span data-stu-id="c052f-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="c052f-107">che converte quindi le richieste in operazioni sull'archivio identità di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c052f-108">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="c052f-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="c052f-109">![][0]
*Figura 1: Provisioning da Azure Active Directory a un archivio identità tramite un servizio Web*</span><span class="sxs-lookup"><span data-stu-id="c052f-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="c052f-110">Questa funzione può essere usata insieme alla funzionalità "bring your own app" in Azure AD per abilitare l'accesso Single Sign-On e il provisioning utenti automatico in applicazioni che offrono o sono gestite da un servizio Web SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="c052f-111">Esistono due casi in cui SCIM viene usato in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c052f-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="c052f-112">**Provisioning di utenti e gruppi in applicazioni che supportano SCIM**: le applicazioni che supportano SCIM 2.0 e usano token di connessione OAuth per l'autenticazione possono essere usate con Azure AD senza interventi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="c052f-113">**Compilazione di una soluzione di provisioning per le applicazioni che supportano il provisioning basato su altre API**: in caso di applicazioni non SCIM, è possibile creare un endpoint SCIM da convertire tra l'endpoint SCIM di Azure AD e qualsiasi API supportata dall'applicazione per il provisioning utente.</span><span class="sxs-lookup"><span data-stu-id="c052f-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="c052f-114">Per facilitare lo sviluppo di un endpoint SCIM, vengono fornite librerie CLI (Common Language Infrastructure) ed esempi di codice che illustrano come creare un endpoint SCIM e convertire messaggi SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="c052f-115">Provisioning di utenti e gruppi in applicazioni che supportano SCIM</span><span class="sxs-lookup"><span data-stu-id="c052f-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="c052f-116">Azure AD può essere configurato in modo da effettuare automaticamente il provisioning di determinati utenti e gruppi in applicazioni che implementano un servizio Web [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) e accettano token di connessione OAuth per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="c052f-117">Nell'ambito della specifica SCIM 2.0, le applicazioni devono soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c052f-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="c052f-118">Supportare la creazione di utenti e/o gruppi, come indicato nella sezione 3.3 del protocollo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c052f-119">Supportare la modifica di utenti e/o gruppi con richieste patch, come indicato nella sezione 3.5.2 del protocollo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c052f-120">Supportare il recupero di una risorsa nota, come indicato nella sezione 3.4.1 del protocollo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c052f-121">Supportare l'interrogazione di utenti e/o gruppi, come indicato nella sezione 3.4.2 del protocollo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="c052f-122">Per impostazione predefinita, gli utenti vengono interrogati da externalId e i gruppi da displayName.</span><span class="sxs-lookup"><span data-stu-id="c052f-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="c052f-123">Supportare l'interrogazione di utenti in base all'ID o al responsabile, come indicato nella sezione 3.4.2 del protocollo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c052f-124">Supportare l'interrogazione di gruppi in base all'ID o ai membri, come indicato nella sezione 3.4.2 del protocollo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c052f-125">Accettare token di connessione OAuth per l'autorizzazione, come indicato nella sezione 2.1 del protocollo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="c052f-126">Verificare la conformità ai requisiti sopra riportati con il provider dell'applicazione o consultando la documentazione fornita dal provider.</span><span class="sxs-lookup"><span data-stu-id="c052f-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="c052f-127">Introduzione</span><span class="sxs-lookup"><span data-stu-id="c052f-127">Getting started</span></span>
<span data-ttu-id="c052f-128">Le applicazioni che supportano il profilo SCIM descritto in questo articolo possono essere connesse ad Azure Active Directory usando la funzionalità "Applicazione non nella raccolta" nella raccolta di applicazioni di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="c052f-129">Una volta stabilita la connessione, Azure AD esegue un processo di sincronizzazione ogni 20 minuti in cui interroga l'endpoint SCIM dell'applicazione in merito agli utenti e ai gruppi assegnati e li crea o li modifica in base alle istruzioni di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="c052f-130">**Per connettere un'applicazione che supporta SCIM:**</span><span class="sxs-lookup"><span data-stu-id="c052f-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="c052f-131">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c052f-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="c052f-132">Passare ad **Azure Active Directory > Applicazioni aziendali e selezionare **Nuova applicazione > Tutte > Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="c052f-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="c052f-133">Immettere un nome per l'applicazione e fare clic sull'icona **Aggiungi** per creare un oggetto app.</span><span class="sxs-lookup"><span data-stu-id="c052f-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="c052f-134">![][1]
  *Figura 2: Raccolta di applicazioni di Azure AD*</span><span class="sxs-lookup"><span data-stu-id="c052f-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="c052f-135">Nella schermata risultante selezionare la scheda **Provisioning** nella colonna sinistra.</span><span class="sxs-lookup"><span data-stu-id="c052f-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="c052f-136">Nel menu **Modalità di provisioning** selezionare **Automatica**.</span><span class="sxs-lookup"><span data-stu-id="c052f-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="c052f-137">![][2]
  *Figura 3: Configurazione del provisioning nel portale di Azure*</span><span class="sxs-lookup"><span data-stu-id="c052f-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="c052f-138">Nel campo **URL tenant** immettere l'URL dell'endpoint SCIM dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="c052f-139">Esempio: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="c052f-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="c052f-140">Se l'endpoint SCIM richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, copiare il token di connessione OAuth nel campo **Token segreto** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c052f-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="c052f-141">Se questo campo viene lasciato vuoto, AD Azure include in ogni richiesta un token di connessione OAuth emesso da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="c052f-142">Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="c052f-143">Fare clic sul pulsante **Test connessione** per fare in modo che Azure Active Directory provi a connettersi all'endpoint SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="c052f-144">Se i tentativi hanno esito negativo, verranno visualizzate informazioni sul tipo di errore.</span><span class="sxs-lookup"><span data-stu-id="c052f-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="c052f-145">Se i tentativi di connessione all'applicazione hanno esito positivo, fare clic su **Salva** per salvare le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="c052f-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="c052f-146">Nella sezione **Mapping** sono disponibili due set selezionabili di mapping degli attributi: uno per gli oggetti utente e uno per gli oggetti gruppo.</span><span class="sxs-lookup"><span data-stu-id="c052f-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="c052f-147">Selezionare ognuno dei due set per esaminare gli attributi sincronizzati da Active Directory di Azure con l'app.</span><span class="sxs-lookup"><span data-stu-id="c052f-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="c052f-148">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli utenti e i gruppi nell'app per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c052f-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="c052f-149">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="c052f-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c052f-150">Facoltativamente, è possibile disattivare la sincronizzazione degli oggetti gruppo disabilitando il mapping relativo ai gruppi.</span><span class="sxs-lookup"><span data-stu-id="c052f-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="c052f-151">In **Impostazioni**, il campo **Ambito** definisce gli utenti e/o i gruppi che devono essere sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="c052f-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="c052f-152">Se si seleziona "Sync only assigned users and groups" ("Sincronizza solo utenti e gruppi assegnati") (scelta consigliata), verranno sincronizzati solo gli utenti e i gruppi assegnati nella scheda **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c052f-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="c052f-153">Al termine della configurazione, impostare lo **Stato del provisioning** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c052f-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="c052f-154">Fare clic su **Salva** per avviare il servizio di provisioning di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="c052f-155">Se si sceglie di sincronizzare solo gli utenti e i gruppi assegnati (scelta consigliata), assicurarsi di selezionare la scheda **Utenti e gruppi** e di assegnare gli utenti e/o i gruppi che si vuole sincronizzare.</span><span class="sxs-lookup"><span data-stu-id="c052f-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="c052f-156">Dopo aver avviato la sincronizzazione iniziale, è possibile usare la scheda **Log di controllo** per monitorare lo stato di avanzamento, che mostra tutte le azioni eseguite dal servizio di provisioning sull'app.</span><span class="sxs-lookup"><span data-stu-id="c052f-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="c052f-157">Per altre informazioni sulla lettura dei log di provisioning di Azure AD, vedere l'esercitazione relativa alla [creazione di report sul provisioning automatico degli account utente](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="c052f-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="c052f-158">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c052f-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="c052f-159">Creazione di una soluzione di provisioning personale per qualsiasi applicazione</span><span class="sxs-lookup"><span data-stu-id="c052f-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="c052f-160">Creando un servizio Web SCIM in grado di interagire con Azure Active Directory, è possibile abilitare l'accesso Single Sign-On e il provisioning utente automatico per qualsiasi applicazione che offra un'API di provisioning utente REST o SOAP.</span><span class="sxs-lookup"><span data-stu-id="c052f-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="c052f-161">Il servizio funziona nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c052f-161">Here’s how it works:</span></span>

1. <span data-ttu-id="c052f-162">Azure AD fornisce una libreria Common Language Infrastructure denominata [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="c052f-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="c052f-163">Gli integratori di sistemi e gli sviluppatori possono usare questa libreria per creare e distribuire un endpoint di servizio Web basato su SCIM in grado di connettere Azure AD all'archivio identità di qualsiasi applicazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="c052f-164">I mapping vengono implementati nel servizio Web per il mapping dello schema utente standardizzato allo schema utente e al protocollo richiesto dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="c052f-165">L'URL dell'endpoint viene registrato in Azure AD come parte di un'applicazione personalizzata nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c052f-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="c052f-166">Gli utenti e i gruppi vengono assegnati a questa applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="c052f-167">In fase di assegnazione, vengono inseriti in una coda per la sincronizzazione con l'applicazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c052f-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="c052f-168">Il processo di sincronizzazione che gestisce la coda viene eseguito ogni 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="c052f-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="c052f-169">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="c052f-169">Code Samples</span></span>
<span data-ttu-id="c052f-170">Per semplificare il processo, viene fornito un set di [esempi di codice](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) che creano un endpoint di servizio Web SCIM e illustrano il provisioning automatico.</span><span class="sxs-lookup"><span data-stu-id="c052f-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="c052f-171">Un esempio è relativo a un provider che gestisce un file con righe di valori delimitati da virgole che rappresentano utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="c052f-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="c052f-172">L'altro esempio è relativo a un provider che agisce sul servizio Amazon Web Services Identity e Access Management.</span><span class="sxs-lookup"><span data-stu-id="c052f-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="c052f-173">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="c052f-173">**Prerequisites**</span></span>

* <span data-ttu-id="c052f-174">Visual Studio 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="c052f-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="c052f-175">Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="c052f-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="c052f-176">Computer Windows che supporta ASP.NET Framework 4.5 da usare come endpoint SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="c052f-177">Questo computer deve essere accessibile dal cloud.</span><span class="sxs-lookup"><span data-stu-id="c052f-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="c052f-178">Una sottoscrizione di Azure con una versione di prova o concessa in licenza di Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="c052f-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="c052f-179">L'esempio relativo ad Amazon AWS richiede librerie di [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="c052f-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="c052f-180">Per altre informazioni, vedere il file README incluso nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="c052f-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="c052f-181">Introduzione</span><span class="sxs-lookup"><span data-stu-id="c052f-181">Getting Started</span></span>
<span data-ttu-id="c052f-182">Il modo più semplice per implementare un endpoint SCIM in grado di accettare richieste di provisioning da Azure AD consiste nel compilare e distribuire l'esempio di codice che fornisce come output gli utenti con provisioning in un file CSV (Comma-Separated Value).</span><span class="sxs-lookup"><span data-stu-id="c052f-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="c052f-183">**Per creare un endpoint SCIM di esempio:**</span><span class="sxs-lookup"><span data-stu-id="c052f-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="c052f-184">Scaricare il pacchetto dell'esempio di codice da [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="c052f-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="c052f-185">Decomprimere il pacchetto e salvarlo nel computer Windows in un percorso analogo a C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="c052f-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="c052f-186">In questa cartella avviare la soluzione FileProvisioningAgent in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c052f-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="c052f-187">Selezionare **Strumenti > Library Package Manager (Gestione pacchetti libreria) > Console di Gestione pacchetti** ed eseguire i comandi seguenti per il progetto FileProvisioningAgent per risolvere i riferimenti alla soluzione:</span><span class="sxs-lookup"><span data-stu-id="c052f-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="c052f-188">Compilare il progetto FileProvisioningAgent.</span><span class="sxs-lookup"><span data-stu-id="c052f-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="c052f-189">Avviare l'applicazione prompt dei comandi in Windows come amministratore e usare il comando **cd** per passare alla cartella **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug**.</span><span class="sxs-lookup"><span data-stu-id="c052f-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="c052f-190">Eseguire il comando seguente, sostituendo <ip-address> con l'indirizzo IP o il nome di dominio del computer Windows:</span><span class="sxs-lookup"><span data-stu-id="c052f-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="c052f-191">In Windows, in **Impostazioni di Windows > Rete e Internet**, selezionare **Windows Firewall > Impostazioni avanzate** e quindi creare una **Nuova regola connessioni in entrata** che consente l'accesso in ingresso alla porta 9000.</span><span class="sxs-lookup"><span data-stu-id="c052f-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="c052f-192">Se il computer Windows si trova dietro un router, è necessario configurare il router in modo che esegua NAT (Network Access Translation) tra la rispettiva porta 9000 esposta a Internet e la porta 9000 nel computer Windows.</span><span class="sxs-lookup"><span data-stu-id="c052f-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="c052f-193">Questo è necessario per consentire ad Azure AD di accedere a questo endpoint sul cloud.</span><span class="sxs-lookup"><span data-stu-id="c052f-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="c052f-194">**Per registrare l'endpoint SCIM di esempio in Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c052f-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="c052f-195">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c052f-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="c052f-196">Passare ad **Azure Active Directory > Applicazioni aziendali e selezionare **Nuova applicazione > Tutte > Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="c052f-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="c052f-197">Immettere un nome per l'applicazione e fare clic sull'icona **Aggiungi** per creare un oggetto app.</span><span class="sxs-lookup"><span data-stu-id="c052f-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="c052f-198">L'oggetto applicazione creato deve rappresentare l'app di destinazione in cui verrà effettuato il provisioning e per cui verrà implementato l'accesso Single Sign-On, non solo l'endpoint SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="c052f-199">Nella schermata risultante selezionare la scheda **Provisioning** nella colonna sinistra.</span><span class="sxs-lookup"><span data-stu-id="c052f-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="c052f-200">Nel menu **Modalità di provisioning** selezionare **Automatica**.</span><span class="sxs-lookup"><span data-stu-id="c052f-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="c052f-201">![][2]
  *Figura 4: Configurazione del provisioning nel portale di Azure*</span><span class="sxs-lookup"><span data-stu-id="c052f-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="c052f-202">Nel campo **URL tenant** immettere l'URL esposto a Internet e la porta dell'endpoint SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="c052f-203">Questi valori saranno simili a http://testmachine.contoso.com:9000 o http://<indirizzo-IP>:9000/, dove <indirizzo-IP> è l'indirizzo IP esposto a Internet.</span><span class="sxs-lookup"><span data-stu-id="c052f-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="c052f-204">Se l'endpoint SCIM richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, copiare il token di connessione OAuth nel campo **Token segreto** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c052f-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="c052f-205">Se questo campo viene lasciato vuoto, AD Azure includerà in ogni richiesta un token di connessione OAuth emesso da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="c052f-206">Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="c052f-207">Fare clic sul pulsante **Test connessione** per fare in modo che Azure Active Directory provi a connettersi all'endpoint SCIM.</span><span class="sxs-lookup"><span data-stu-id="c052f-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="c052f-208">Se i tentativi hanno esito negativo, verranno visualizzate informazioni sul tipo di errore.</span><span class="sxs-lookup"><span data-stu-id="c052f-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="c052f-209">Se i tentativi di connessione all'applicazione hanno esito positivo, fare clic su **Salva** per salvare le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="c052f-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="c052f-210">Nella sezione **Mapping** sono disponibili due set selezionabili di mapping degli attributi: uno per gli oggetti utente e uno per gli oggetti gruppo.</span><span class="sxs-lookup"><span data-stu-id="c052f-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="c052f-211">Selezionare ognuno dei due set per esaminare gli attributi sincronizzati da Active Directory di Azure con l'app.</span><span class="sxs-lookup"><span data-stu-id="c052f-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="c052f-212">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli utenti e i gruppi nell'app per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c052f-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="c052f-213">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="c052f-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="c052f-214">In **Impostazioni**, il campo **Ambito** definisce gli utenti e/o i gruppi che devono essere sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="c052f-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="c052f-215">Se si seleziona "Sync only assigned users and groups" ("Sincronizza solo utenti e gruppi assegnati") (scelta consigliata), verranno sincronizzati solo gli utenti e i gruppi assegnati nella scheda **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c052f-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="c052f-216">Al termine della configurazione, impostare lo **Stato del provisioning** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c052f-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="c052f-217">Fare clic su **Salva** per avviare il servizio di provisioning di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="c052f-218">Se si sceglie di sincronizzare solo gli utenti e i gruppi assegnati (scelta consigliata), assicurarsi di selezionare la scheda **Utenti e gruppi** e di assegnare gli utenti e/o i gruppi che si vuole sincronizzare.</span><span class="sxs-lookup"><span data-stu-id="c052f-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="c052f-219">Dopo aver avviato la sincronizzazione iniziale, è possibile usare la scheda **Log di controllo** per monitorare lo stato di avanzamento, che mostra tutte le azioni eseguite dal servizio di provisioning sull'app.</span><span class="sxs-lookup"><span data-stu-id="c052f-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="c052f-220">Per altre informazioni sulla lettura dei log di provisioning di Azure AD, vedere l'esercitazione relativa alla [creazione di report sul provisioning automatico degli account utente](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="c052f-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="c052f-221">Il passaggio finale della verifica dell'esempio consiste nell'aprire il file TargetFile.csv nella cartella \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug del computer Windows.</span><span class="sxs-lookup"><span data-stu-id="c052f-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="c052f-222">Dopo l'esecuzione del processo di provisioning, questo file include i dettagli di tutti gli utenti e gruppi assegnati e sottoposti a provisioning.</span><span class="sxs-lookup"><span data-stu-id="c052f-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="c052f-223">Librerie di sviluppo</span><span class="sxs-lookup"><span data-stu-id="c052f-223">Development libraries</span></span>
<span data-ttu-id="c052f-224">Per sviluppare un servizio Web personalizzato conforme alla specifica SCIM, è necessario prima di tutto acquisire familiarità con le librerie Microsoft seguenti per accelerare il processo di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="c052f-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="c052f-225">Le librerie CLI (Common Language Infrastructure) vengono messe a disposizione per essere usate con linguaggi basati su questa infrastruttura, ad esempio C#.</span><span class="sxs-lookup"><span data-stu-id="c052f-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="c052f-226">Una di queste librerie, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), dichiara un'interfaccia, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, illustrata nella figura seguente. Uno sviluppatore che usa le librerie implementerà questa interfaccia con una classe a cui è possibile fare riferimento, in modo generico, come provider.</span><span class="sxs-lookup"><span data-stu-id="c052f-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="c052f-227">Le librerie consentono agli sviluppatori di distribuire un servizio Web conforme alla specifica SCIM,</span><span class="sxs-lookup"><span data-stu-id="c052f-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="c052f-228">che può essere ospitato sia in Internet Information Services sia in qualsiasi assembly Common Language Infrastructure eseguibile.</span><span class="sxs-lookup"><span data-stu-id="c052f-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="c052f-229">La richiesta viene convertita in chiamate ai metodi del provider, che saranno programmate dallo sviluppatore per agire su un archivio identità.</span><span class="sxs-lookup"><span data-stu-id="c052f-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="c052f-230">I [gestori di ExpressRoute](http://expressjs.com/guide/routing.html) sono disponibili per l'analisi di oggetti richiesta node.js che rappresentano chiamate, in base alla definizione della specifica SCIM, effettuate a un servizio Web node.js.</span><span class="sxs-lookup"><span data-stu-id="c052f-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="c052f-231">Creazione di un endpoint SCIM personalizzato</span><span class="sxs-lookup"><span data-stu-id="c052f-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="c052f-232">Usando le librerie CLI, gli sviluppatori possono ospitare i servizi in un assembly Common Language Infrastructure eseguibile o in Internet Information Services.</span><span class="sxs-lookup"><span data-stu-id="c052f-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="c052f-233">Ecco un codice di esempio per l'hosting di un servizio in un assembly eseguibile all'indirizzo http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="c052f-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="c052f-234">Questo servizio deve avere un indirizzo HTTP e un certificato di autenticazione server la cui autorità di certificazione radice è una delle seguenti:</span><span class="sxs-lookup"><span data-stu-id="c052f-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="c052f-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="c052f-235">CNNIC</span></span>
* <span data-ttu-id="c052f-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="c052f-236">Comodo</span></span>
* <span data-ttu-id="c052f-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="c052f-237">CyberTrust</span></span>
* <span data-ttu-id="c052f-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="c052f-238">DigiCert</span></span>
* <span data-ttu-id="c052f-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="c052f-239">GeoTrust</span></span>
* <span data-ttu-id="c052f-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="c052f-240">GlobalSign</span></span>
* <span data-ttu-id="c052f-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="c052f-241">Go Daddy</span></span>
* <span data-ttu-id="c052f-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="c052f-242">Verisign</span></span>
* <span data-ttu-id="c052f-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="c052f-243">WoSign</span></span>

<span data-ttu-id="c052f-244">Un certificato di autenticazione server può essere associato a una porta su un host Windows usando l'utilità shell di rete:</span><span class="sxs-lookup"><span data-stu-id="c052f-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="c052f-245">Il valore fornito per l'argomento certhash è l'identificazione personale del certificato, mentre il valore specificato per l'argomento appid è un identificatore univoco globale arbitrario.</span><span class="sxs-lookup"><span data-stu-id="c052f-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="c052f-246">Per ospitare il servizio in Internet Information Services, uno sviluppatore deve creare un assembly della libreria di codice CLA con una classe denominata Startup nello spazio dei nomi predefinito dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="c052f-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="c052f-247">Ecco un esempio di questa classe:</span><span class="sxs-lookup"><span data-stu-id="c052f-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="c052f-248">Gestione dell'autenticazione dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="c052f-248">Handling endpoint authentication</span></span>
<span data-ttu-id="c052f-249">Le richieste da Azure Active Directory includono un token di connessione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="c052f-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="c052f-250">Qualsiasi servizio che riceve la richiesta deve autenticare l'emittente come Azure Active Directory per conto del tenant Azure Active Directory previsto, per l'accesso al servizio Web Graph di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c052f-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="c052f-251">Nel token l'emittente viene identificato da un'attestazione iss, ad esempio, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="c052f-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="c052f-252">In questo esempio, l'indirizzo di base del valore dell'attestazione, https://sts.windows.net, identifica Azure Active Directory come autorità di certificazione, mentre il segmento dell'indirizzo relativo, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, è un identificatore univoco del tenant di Azure Active Directory per conto del quale è stato emesso il token.</span><span class="sxs-lookup"><span data-stu-id="c052f-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="c052f-253">Se il token è stato emesso per l'accesso al servizio Web Graph di Azure Active Directory, l'identificatore di quel servizio, 00000002-0000-0000-c000-000000000000, deve essere incluso nel valore dell'attestazione aud del token.</span><span class="sxs-lookup"><span data-stu-id="c052f-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="c052f-254">Gli sviluppatori che usano le librerie CLA fornite da Microsoft per la creazione di un servizio SCIM possono autenticare le richieste da Azure Active Directory mediante il pacchetto Microsoft.Owin.Security.ActiveDirectory seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c052f-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="c052f-255">In un provider implementare la proprietà Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior facendo in modo che restituisca un metodo da chiamare ogni volta che viene avviato il servizio:</span><span class="sxs-lookup"><span data-stu-id="c052f-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="c052f-256">Aggiungere il codice seguente al metodo, in modo che qualsiasi richiesta a uno degli endpoint del servizio venga autenticata come se includesse un token emesso da Azure Active Directory per conto di un tenant specifico, per l'accesso al servizio Web Graph di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c052f-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="c052f-257">Schema di utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="c052f-257">User and group schema</span></span>
<span data-ttu-id="c052f-258">Azure Active Directory può effettuare il provisioning di due tipi di risorse nei servizi Web SCIM,</span><span class="sxs-lookup"><span data-stu-id="c052f-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="c052f-259">ovvero utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="c052f-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="c052f-260">Le risorse utente sono rilevate dall'identificatore dello schema, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, incluso in questa specifica del protocollo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="c052f-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="c052f-261">Il mapping predefinito degli attributi degli utenti in Azure Active Directory agli attributi delle risorse urn:ietf:params:scim:schemas:extension:enterprise:2.0:User è disponibile nella tabella 1 seguente.</span><span class="sxs-lookup"><span data-stu-id="c052f-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="c052f-262">Le risorse gruppo sono identificate dall'identificatore dello schema, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="c052f-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="c052f-263">La tabella 2 seguente illustra il mapping predefinito degli attributi di gruppi di Azure Active Directory agli attributi delle risorse http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="c052f-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="c052f-264">Tabella 1: mapping predefinito degli attributi utente</span><span class="sxs-lookup"><span data-stu-id="c052f-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="c052f-265">Utente Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c052f-265">Azure Active Directory user</span></span> | <span data-ttu-id="c052f-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="c052f-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="c052f-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="c052f-267">IsSoftDeleted</span></span> |<span data-ttu-id="c052f-268">active</span><span class="sxs-lookup"><span data-stu-id="c052f-268">active</span></span> |
| <span data-ttu-id="c052f-269">displayName</span><span class="sxs-lookup"><span data-stu-id="c052f-269">displayName</span></span> |<span data-ttu-id="c052f-270">displayName</span><span class="sxs-lookup"><span data-stu-id="c052f-270">displayName</span></span> |
| <span data-ttu-id="c052f-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="c052f-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="c052f-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="c052f-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="c052f-273">givenName</span><span class="sxs-lookup"><span data-stu-id="c052f-273">givenName</span></span> |<span data-ttu-id="c052f-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="c052f-274">name.givenName</span></span> |
| <span data-ttu-id="c052f-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="c052f-275">jobTitle</span></span> |<span data-ttu-id="c052f-276">title</span><span class="sxs-lookup"><span data-stu-id="c052f-276">title</span></span> |
| <span data-ttu-id="c052f-277">mail</span><span class="sxs-lookup"><span data-stu-id="c052f-277">mail</span></span> |<span data-ttu-id="c052f-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="c052f-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="c052f-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="c052f-279">mailNickname</span></span> |<span data-ttu-id="c052f-280">externalId</span><span class="sxs-lookup"><span data-stu-id="c052f-280">externalId</span></span> |
| <span data-ttu-id="c052f-281">manager</span><span class="sxs-lookup"><span data-stu-id="c052f-281">manager</span></span> |<span data-ttu-id="c052f-282">manager</span><span class="sxs-lookup"><span data-stu-id="c052f-282">manager</span></span> |
| <span data-ttu-id="c052f-283">mobile</span><span class="sxs-lookup"><span data-stu-id="c052f-283">mobile</span></span> |<span data-ttu-id="c052f-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="c052f-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="c052f-285">objectId</span><span class="sxs-lookup"><span data-stu-id="c052f-285">objectId</span></span> |<span data-ttu-id="c052f-286">id</span><span class="sxs-lookup"><span data-stu-id="c052f-286">id</span></span> |
| <span data-ttu-id="c052f-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="c052f-287">postalCode</span></span> |<span data-ttu-id="c052f-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="c052f-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="c052f-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="c052f-289">proxy-Addresses</span></span> |<span data-ttu-id="c052f-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="c052f-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="c052f-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="c052f-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="c052f-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="c052f-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="c052f-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="c052f-293">streetAddress</span></span> |<span data-ttu-id="c052f-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="c052f-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="c052f-295">surname</span><span class="sxs-lookup"><span data-stu-id="c052f-295">surname</span></span> |<span data-ttu-id="c052f-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="c052f-296">name.familyName</span></span> |
| <span data-ttu-id="c052f-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="c052f-297">telephone-Number</span></span> |<span data-ttu-id="c052f-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="c052f-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="c052f-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="c052f-299">user-PrincipalName</span></span> |<span data-ttu-id="c052f-300">userName</span><span class="sxs-lookup"><span data-stu-id="c052f-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="c052f-301">Tabella 2: mapping predefinito degli attributi gruppo</span><span class="sxs-lookup"><span data-stu-id="c052f-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="c052f-302">Gruppo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c052f-302">Azure Active Directory group</span></span> | <span data-ttu-id="c052f-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="c052f-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="c052f-304">displayName</span><span class="sxs-lookup"><span data-stu-id="c052f-304">displayName</span></span> |<span data-ttu-id="c052f-305">externalId</span><span class="sxs-lookup"><span data-stu-id="c052f-305">externalId</span></span> |
| <span data-ttu-id="c052f-306">mail</span><span class="sxs-lookup"><span data-stu-id="c052f-306">mail</span></span> |<span data-ttu-id="c052f-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="c052f-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="c052f-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="c052f-308">mailNickname</span></span> |<span data-ttu-id="c052f-309">displayName</span><span class="sxs-lookup"><span data-stu-id="c052f-309">displayName</span></span> |
| <span data-ttu-id="c052f-310">Membri di</span><span class="sxs-lookup"><span data-stu-id="c052f-310">members</span></span> |<span data-ttu-id="c052f-311">Membri di</span><span class="sxs-lookup"><span data-stu-id="c052f-311">members</span></span> |
| <span data-ttu-id="c052f-312">objectId</span><span class="sxs-lookup"><span data-stu-id="c052f-312">objectId</span></span> |<span data-ttu-id="c052f-313">id</span><span class="sxs-lookup"><span data-stu-id="c052f-313">id</span></span> |
| <span data-ttu-id="c052f-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="c052f-314">proxyAddresses</span></span> |<span data-ttu-id="c052f-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="c052f-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="c052f-316">Provisioning e deprovisioning utenti</span><span class="sxs-lookup"><span data-stu-id="c052f-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="c052f-317">La figura seguente illustra i messaggi che Azure Active Directory invia al servizio SCIM per gestire il ciclo di vita di un utente in un altro archivio identità.</span><span class="sxs-lookup"><span data-stu-id="c052f-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="c052f-318">Il diagramma illustra anche il modo in cui un servizio SCIM implementato mediante le librerie CLI fornite da Microsoft per la creazione di questi servizi converte queste richieste in chiamate ai metodi di un provider.</span><span class="sxs-lookup"><span data-stu-id="c052f-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="c052f-319">![][4]
*Figura 5: Sequenza di provisioning e deprovisioning utenti*</span><span class="sxs-lookup"><span data-stu-id="c052f-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="c052f-320">Azure Active Directory esegue query nel servizio per trovare un utente con valore dell'attributo externalId corrispondente al valore dell'attributo mailNickname di un utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c052f-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="c052f-321">La query viene espressa come richiesta HTTP (Hypertext Transfer Protocol) analoga a quella dell'esempio, dove jyoung è un esempio di mailNickname di un utente in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c052f-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c052f-322">Se il servizio è stato creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Query del provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="c052f-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="c052f-323">Ecco la firma del metodo:</span><span class="sxs-lookup"><span data-stu-id="c052f-323">Here is the signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="c052f-324">Ecco la definizione dell'interfaccia Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters:</span><span class="sxs-lookup"><span data-stu-id="c052f-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="c052f-325">Nell'esempio seguente di una query per un utente con un determinato valore per l'attributo externalId, i valori degli argomenti passati al metodo Query sono:</span><span class="sxs-lookup"><span data-stu-id="c052f-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="c052f-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="c052f-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="c052f-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="c052f-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="c052f-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="c052f-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="c052f-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="c052f-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="c052f-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="c052f-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="c052f-331">Se la risposta a una query sul servizio Web per cercare un utente con valore dell'attributo externalId corrispondente al valore dell'attributo mailNickname di un utente non restituisce alcun utente, Azure Active Directory richiede che il servizio effettui il provisioning di un utente corrispondente a quello in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c052f-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="c052f-332">Ecco un esempio di questa richiesta:</span><span class="sxs-lookup"><span data-stu-id="c052f-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="c052f-333">Le librerie Common Language Infrastructure fornite da Microsoft per implementare servizi SCIM convertiranno tale richiesta in una chiamata al metodo Create del provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="c052f-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="c052f-334">Il metodo Create ha la firma seguente:</span><span class="sxs-lookup"><span data-stu-id="c052f-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="c052f-335">In una richiesta di provisioning di un utente, il valore dell'argomento resource è un'istanza della classe Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="c052f-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="c052f-336">Core2EnterpriseUser, definita nella libreria Microsoft.SystemForCrossDomainIdentityManagement.Schemas.</span><span class="sxs-lookup"><span data-stu-id="c052f-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="c052f-337">Se la richiesta di provisioning dell'utente ha esito positivo, si prevede che l'implementazione del metodo restituisca un'istanza di Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="c052f-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="c052f-338">Core2EnterpriseUser, con il valore della proprietà Identifier impostato sull'identificatore univoco dell'utente appena sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="c052f-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="c052f-339">Per aggiornare un utente la cui esistenza è nota in un archivio identità gestito da SCIM, Azure Active Directory richiede al servizio lo stato corrente dell'utente con una richiesta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="c052f-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c052f-340">In un servizio creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Retrieve del provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="c052f-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="c052f-341">Ecco la firma del metodo Retrieve:</span><span class="sxs-lookup"><span data-stu-id="c052f-341">Here is the signature of the Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="c052f-342">Nell'esempio di una richiesta per recuperare lo stato corrente di un utente, i valori delle proprietà dell'oggetto fornito come valore dell'argomento parameters sono analoghi ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="c052f-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="c052f-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c052f-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c052f-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c052f-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="c052f-345">Se è necessario aggiornare un attributo reference, Azure Active Directory esegue query sul servizio per determinare se il valore corrente dell'attributo reference nell'archivio identità gestito dal servizio corrisponde già al valore dell'attributo in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c052f-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="c052f-346">Per gli utenti, l'unico attributo il cui valore corrente viene sottoposto a query con questa modalità è l'attributo manager.</span><span class="sxs-lookup"><span data-stu-id="c052f-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="c052f-347">Ecco un esempio di una richiesta per determinare se l'attributo manager di un oggetto utente specifico ha attualmente un determinato valore:</span><span class="sxs-lookup"><span data-stu-id="c052f-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c052f-348">Il valore del parametro attributes della query, id, indica che se esiste un oggetto utente che soddisfa l'espressione fornita come valore del parametro filter della query, il servizio dovrà rispondere con una risorsa urn:ietf:params:scim:schemas:core:2.0:User o urn:ietf:params:scim:schemas:extension:enterprise:2.0:User che include solo il valore dell'attributo id della risorsa.</span><span class="sxs-lookup"><span data-stu-id="c052f-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="c052f-349">Il valore dell'attributo **id** è noto al richiedente,</span><span class="sxs-lookup"><span data-stu-id="c052f-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="c052f-350">poiché è incluso nel valore del parametro filter della query. Il valore viene chiesto per potere richiedere una rappresentazione minima di una risorsa che soddisfa l'espressione di filtro come indicazione dell'eventuale esistenza di questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="c052f-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="c052f-351">Se il servizio è stato creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Query del provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="c052f-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="c052f-352">Il valore delle proprietà dell'oggetto fornito come valore dell'argomento parameters è analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="c052f-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="c052f-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="c052f-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="c052f-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="c052f-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="c052f-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="c052f-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="c052f-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c052f-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c052f-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="c052f-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="c052f-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="c052f-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="c052f-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="c052f-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="c052f-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="c052f-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="c052f-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c052f-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="c052f-362">Il valore dell'indice x può essere 0 e il valore dell'indice y può essere 1 oppure il valore di x può essere 1 e il valore di y può essere 0, in base all'ordine delle espressioni del parametro filter della query.</span><span class="sxs-lookup"><span data-stu-id="c052f-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="c052f-363">Ecco un esempio di una richiesta di Azure Active Directory a un servizio SCIM per l'aggiornamento di un utente:</span><span class="sxs-lookup"><span data-stu-id="c052f-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="c052f-364">Le librerie Microsoft Common Language Infrastructure per implementare servizi SCIM convertiranno la richiesta in una chiamata al metodo Update del provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="c052f-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="c052f-365">Questa è la firma del metodo Update:</span><span class="sxs-lookup"><span data-stu-id="c052f-365">Here is the signature of the Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="c052f-366">Nell'esempio di una richiesta per l'aggiornamento di un utente, i valori delle proprietà dell'oggetto fornito come valore dell'argomento patch sono analoghi ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="c052f-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="c052f-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c052f-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c052f-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c052f-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="c052f-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="c052f-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="c052f-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="c052f-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="c052f-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="c052f-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="c052f-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="c052f-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="c052f-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="c052f-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="c052f-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="c052f-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="c052f-375">Per effettuare il deprovisioning di un utente da un archivio identità gestito da un servizio SCIM, Azure Active Directory invia una richiesta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="c052f-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c052f-376">Se il servizio è stato creato mediante le librerie Common Language Infrastructure fornite da Microsoft per implementare i servizi SCIM, la richiesta viene convertita in una chiamata al metodo Delete del provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="c052f-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="c052f-377">Il metodo ha la firma seguente:</span><span class="sxs-lookup"><span data-stu-id="c052f-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="c052f-378">Nell'esempio di una richiesta per il deprovisioning di un utente, i valori delle proprietà dell'oggetto fornito come valore dell'argomento resourceIdentifier sono analoghi ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="c052f-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="c052f-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c052f-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c052f-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c052f-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="c052f-381">Provisioning e deprovisioning gruppi</span><span class="sxs-lookup"><span data-stu-id="c052f-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="c052f-382">La figura seguente illustra i messaggi che Azure AD invia al servizio SCIM per gestire il ciclo di vita di un gruppo in un altro archivio identità.</span><span class="sxs-lookup"><span data-stu-id="c052f-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="c052f-383">Questi messaggi si differenziano dai messaggi relativi agli utenti in tre modi:</span><span class="sxs-lookup"><span data-stu-id="c052f-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="c052f-384">Lo schema di una risorsa gruppo viene identificato come http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="c052f-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="c052f-385">Le richieste per il recupero di gruppi stipulano che l'attributo members deve essere escluso da qualsiasi risorsa fornita in risposta alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c052f-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="c052f-386">Le richieste per determinare se un attributo reference ha un determinato valore sono richieste relative all'attributo members.</span><span class="sxs-lookup"><span data-stu-id="c052f-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="c052f-387">![][5]
*Figura 6: Sequenza di provisioning e deprovisioning gruppi*</span><span class="sxs-lookup"><span data-stu-id="c052f-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="c052f-388">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="c052f-388">Related articles</span></span>
* [<span data-ttu-id="c052f-389">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c052f-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c052f-390">Automatizzare il provisioning e il deprovisioning utenti in app SaaS</span><span class="sxs-lookup"><span data-stu-id="c052f-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="c052f-391">Personalizzazione dei mapping degli attributi per il Provisioning dell’utente</span><span class="sxs-lookup"><span data-stu-id="c052f-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="c052f-392">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="c052f-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="c052f-393">Ambito dei filtri per il Provisioning utente</span><span class="sxs-lookup"><span data-stu-id="c052f-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="c052f-394">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="c052f-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="c052f-395">Elenco di esercitazioni pratiche sulla procedura di integrazione delle applicazioni SaaS</span><span class="sxs-lookup"><span data-stu-id="c052f-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG

---
title: "Sistema di gestione delle identità tra domini aaaUsing esegue automaticamente il provisioning utenti e gruppi da Azure Active Directory tooapplications | Documenti Microsoft"
description: "Azure Active Directory possono eseguire automaticamente il provisioning degli utenti e gruppi tooany identità o l'applicazione store di applicazioni da un servizio web con interfaccia hello definito nella specifica del protocollo SCIM hello"
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
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="3970b-103">Utilizzo di sistema per il provisioning utenti tooautomatically di gestione delle identità tra domini e gruppi da Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="3970b-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="3970b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3970b-104">Overview</span></span>
<span data-ttu-id="3970b-105">Azure Active Directory (Azure AD) può eseguire automaticamente il provisioning degli utenti e gruppi tooany identità o l'applicazione store di applicazioni da un servizio web con interfaccia hello definita in hello [sistema per domini Identity Management (SCIM) 2.0 Specifica del protocollo](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="3970b-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="3970b-106">Azure Active Directory può inviare richieste toocreate, modificare o eliminare utenti e gruppi toohello web servizio assegnato.</span><span class="sxs-lookup"><span data-stu-id="3970b-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="3970b-107">servizio web Hello può quindi tradurre le richieste di operazioni sull'archivio identità di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3970b-108">Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3970b-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="3970b-109">![][0]
*Figura 1: Provisioning dall'archivio di identità di Azure Active Directory tooan tramite un servizio web*</span><span class="sxs-lookup"><span data-stu-id="3970b-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="3970b-110">Questa funzionalità è utilizzabile in combinazione con funzionalità di "bring la propria app" hello in Azure AD tooenable single sign-on e provisioning per le applicazioni che forniscono o sono applicazioni da un servizio web SCIM automatica degli utenti.</span><span class="sxs-lookup"><span data-stu-id="3970b-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="3970b-111">Esistono due casi in cui SCIM viene usato in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="3970b-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="3970b-112">**Provisioning utenti e gruppi tooapplications che supportano SCIM** applicazioni che supportano SCIM 2.0 e utilizzano i token di connessione OAuth per l'autenticazione funziona con Azure AD senza attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3970b-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="3970b-113">**Compilare la propria soluzione di provisioning per le applicazioni che supportano altri provisioning basato su API** per le applicazioni non SCIM, è possibile creare un tootranslate endpoint SCIM tra endpoint di Azure AD SCIM hello e supporta l'applicazione hello qualsiasi API per il provisioning dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3970b-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="3970b-114">toohelp si sviluppa un endpoint SCIM, si forniscono le librerie di Common Language Infrastructure (CLI) insieme a esempi di codice che illustrano come toodo forniscono un endpoint SCIM e convertire i messaggi SCIM.</span><span class="sxs-lookup"><span data-stu-id="3970b-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="3970b-115">Provisioning di utenti e gruppi tooapplications che supportano SCIM</span><span class="sxs-lookup"><span data-stu-id="3970b-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="3970b-116">Azure AD può essere configurato tooautomatically tooapplications utenti e gruppi a disposizione assegnato che implementano un [sistema per la gestione delle identità tra domini 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) servizio web e di accettare i token di connessione OAuth per l'autenticazione .</span><span class="sxs-lookup"><span data-stu-id="3970b-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="3970b-117">All'interno della specifica di hello SCIM 2.0, le applicazioni devono soddisfare questi requisiti:</span><span class="sxs-lookup"><span data-stu-id="3970b-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="3970b-118">Supporta la creazione di utenti e/o gruppi, come indicato nella sezione 3.3 di protocollo SCIM hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="3970b-119">Supporta la modifica di utenti e/o gruppi con le richieste patch indicato nella sezione 3.5.2 di protocollo SCIM hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="3970b-120">Supporta il recupero di una risorsa in base alle sezione 3.4.1 di hello protocollo SCIM nota.</span><span class="sxs-lookup"><span data-stu-id="3970b-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="3970b-121">Supporta l'esecuzione di query su utenti e/o gruppi, come indicato nella sezione sezione 3.4.2 di protocollo SCIM hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="3970b-122">Per impostazione predefinita, gli utenti vengono interrogati da externalId e i gruppi da displayName.</span><span class="sxs-lookup"><span data-stu-id="3970b-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="3970b-123">Supporta l'esecuzione di query utente tramite ID e dal gestore indicato nella sezione sezione 3.4.2 di protocollo SCIM hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="3970b-124">Supporta l'esecuzione di query gruppi tramite ID e dal membro indicato nella sezione sezione 3.4.2 di protocollo SCIM hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="3970b-125">Accetta i token di connessione OAuth per l'autorizzazione in base alle sezione 2.1 del protocollo SCIM hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="3970b-126">Verificare la conformità ai requisiti sopra riportati con il provider dell'applicazione o consultando la documentazione fornita dal provider.</span><span class="sxs-lookup"><span data-stu-id="3970b-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="3970b-127">introduttiva</span><span class="sxs-lookup"><span data-stu-id="3970b-127">Getting started</span></span>
<span data-ttu-id="3970b-128">Le applicazioni che supportano il profilo SCIM hello descritto in questo articolo possono essere connesso tooAzure Active Directory utilizzando la funzionalità "non raccolta applicazione hello" nella raccolta di applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="3970b-129">Una volta connessi, Azure AD viene eseguito un processo di sincronizzazione ogni 20 minuti in cui viene eseguita una query di endpoint SCIM dell'applicazione hello per assegnata utenti e gruppi e crea o li modifica in base a toohello i dettagli dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="3970b-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="3970b-130">**un'applicazione che supporta SCIM tooconnect:**</span><span class="sxs-lookup"><span data-stu-id="3970b-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="3970b-131">Accedi troppo[hello Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3970b-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="3970b-132">Sfoglia troppo * * Azure Active Directory > applicazioni aziendali e selezionare **nuova applicazione > tutti > applicazione Non raccolta**.</span><span class="sxs-lookup"><span data-stu-id="3970b-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="3970b-133">Immettere un nome per l'applicazione e fare clic su **Aggiungi** icona toocreate un oggetto applicazione.</span><span class="sxs-lookup"><span data-stu-id="3970b-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="3970b-134">![][1]
  *Figura 2: Raccolta di applicazioni di Azure AD*</span><span class="sxs-lookup"><span data-stu-id="3970b-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="3970b-135">Nella schermata risultante hello selezionare hello **Provisioning** scheda nella colonna sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="3970b-136">In hello **modalità di Provisioning** dal menu **automatica**.</span><span class="sxs-lookup"><span data-stu-id="3970b-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="3970b-137">![][2]
  *Figura 3: Configurazione del provisioning in hello portale di Azure*</span><span class="sxs-lookup"><span data-stu-id="3970b-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="3970b-138">In hello **URL Tenant** immettere hello URL dell'endpoint SCIM dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="3970b-139">Esempio: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="3970b-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="3970b-140">Se l'endpoint SCIM hello richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, quindi hello copia necessari token di connessione OAuth nel hello facoltativo **segreto Token** campo.</span><span class="sxs-lookup"><span data-stu-id="3970b-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="3970b-141">Se questo campo viene lasciato vuoto, AD Azure include in ogni richiesta un token di connessione OAuth emesso da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="3970b-142">Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="3970b-143">Fare clic su hello **Test connessione** endpoint SCIM pulsante toohave Azure Active Directory tentativo tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="3970b-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="3970b-144">Se hello tentativi falliscono, informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="3970b-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="3970b-145">Se un'applicazione hello tentativi tooconnect toohello esito negativo, quindi fare clic su **salvare** credenziali di amministratore toosave hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="3970b-146">In hello **mapping** sezione, sono disponibili due set di mapping degli attributi selezionabile: uno per gli oggetti utente e uno per gli oggetti di gruppo.</span><span class="sxs-lookup"><span data-stu-id="3970b-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="3970b-147">Selezionare ogni attributi di hello tooreview uno che vengono sincronizzati da app tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3970b-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="3970b-148">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello utenti e gruppi nell'app per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3970b-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="3970b-149">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="3970b-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3970b-150">È facoltativamente possibile disabilitare la sincronizzazione degli oggetti di gruppo dalla disabilitazione di hello "gruppi" mapping.</span><span class="sxs-lookup"><span data-stu-id="3970b-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="3970b-151">In **impostazioni**, hello **ambito** campo definisce quali gruppi di utenti e o vengono sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="3970b-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="3970b-152">Selezione di "Sincronizzazione assegnata solo gli utenti e gruppi" (scelta consigliata) verranno sincronizzate solo gli utenti e gruppi assegnati in hello **utenti e gruppi** scheda.</span><span class="sxs-lookup"><span data-stu-id="3970b-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="3970b-153">Una volta completata la configurazione, modificare hello **lo stato di Provisioning** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="3970b-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="3970b-154">Fare clic su **salvare** toostart hello servizio provisioning di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="3970b-155">Se la sincronizzazione solo assegnati a utenti e gruppi (scelta consigliati), in certi hello tooselect **utenti e gruppi** scheda e assegnare gli utenti di hello e/o gruppi di cui si desidera toosync.</span><span class="sxs-lookup"><span data-stu-id="3970b-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="3970b-156">Una volta avviata la sincronizzazione iniziale di hello, è possibile utilizzare hello **log di controllo** scheda toomonitor lo stato di avanzamento, che mostra tutte le azioni eseguite da hello provisioning del servizio nella tua app.</span><span class="sxs-lookup"><span data-stu-id="3970b-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="3970b-157">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="3970b-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="3970b-158">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3970b-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="3970b-159">Creazione di una soluzione di provisioning personale per qualsiasi applicazione</span><span class="sxs-lookup"><span data-stu-id="3970b-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="3970b-160">Creando un servizio Web SCIM in grado di interagire con Azure Active Directory, è possibile abilitare l'accesso Single Sign-On e il provisioning utente automatico per qualsiasi applicazione che offra un'API di provisioning utente REST o SOAP.</span><span class="sxs-lookup"><span data-stu-id="3970b-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="3970b-161">Il servizio funziona nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="3970b-161">Here’s how it works:</span></span>

1. <span data-ttu-id="3970b-162">Azure AD fornisce una libreria Common Language Infrastructure denominata [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="3970b-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="3970b-163">Gli sviluppatori e integratori di sistema possono utilizzare toocreate questa libreria e distribuire un endpoint del servizio web basato su SCIM in grado di connettersi archivio identità dell'applicazione di Azure AD tooany.</span><span class="sxs-lookup"><span data-stu-id="3970b-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="3970b-164">I mapping vengono implementati in hello web servizio toomap hello standardizzato schema utente di schema toohello utente e il protocollo richiesto da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="3970b-165">URL dell'endpoint Hello è registrato in Azure AD come parte di un'applicazione personalizzata nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="3970b-166">Utenti e gruppi assegnati toothis applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="3970b-167">Base all'assegnazione, vengono inseriti in un'applicazione di destinazione coda toohello toobe sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="3970b-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="3970b-168">il processo di sincronizzazione Hello gestione coda hello viene eseguito ogni 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="3970b-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="3970b-169">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="3970b-169">Code Samples</span></span>
<span data-ttu-id="3970b-170">toomake questo processo più semplice, un set di [esempi di codice](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) sono incluse la creazione di un endpoint del servizio web SCIM e viene illustrato il provisioning automatico.</span><span class="sxs-lookup"><span data-stu-id="3970b-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="3970b-171">Un esempio è relativo a un provider che gestisce un file con righe di valori delimitati da virgole che rappresentano utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="3970b-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="3970b-172">altri Hello è di un provider che opera su servizio di Amazon Web Services Identity and Access Management hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="3970b-173">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="3970b-173">**Prerequisites**</span></span>

* <span data-ttu-id="3970b-174">Visual Studio 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="3970b-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="3970b-175">Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="3970b-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="3970b-176">Computer Windows che supporta hello ASP.NET 4.5 framework toobe utilizzato come hello endpoint SCIM.</span><span class="sxs-lookup"><span data-stu-id="3970b-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="3970b-177">Il computer deve essere accessibile dal cloud hello</span><span class="sxs-lookup"><span data-stu-id="3970b-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="3970b-178">Una sottoscrizione di Azure con una versione di prova o concessa in licenza di Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="3970b-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="3970b-179">esempio di Amazon AWS Hello richiede di librerie da hello [AWS Toolkit per Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="3970b-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="3970b-180">Per ulteriori informazioni, vedere hello Leggimi file incluso in esempio hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="3970b-181">Introduzione</span><span class="sxs-lookup"><span data-stu-id="3970b-181">Getting Started</span></span>
<span data-ttu-id="3970b-182">tooimplement modo più semplice Hello richiede un endpoint SCIM in grado di accettare il provisioning da Azure AD è toobuild e distribuire l'esempio di codice hello che restituisce hello provisioning utenti tooa valore delimitato da virgole (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="3970b-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="3970b-183">**un endpoint di esempio SCIM toocreate:**</span><span class="sxs-lookup"><span data-stu-id="3970b-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="3970b-184">Download del pacchetto di esempio di codice hello in [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="3970b-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="3970b-185">Decomprimere il pacchetto di hello e posizionarlo nel computer Windows in una posizione, ad esempio C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="3970b-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="3970b-186">In questa cartella, avviare soluzione FileProvisioningAgent hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3970b-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="3970b-187">Selezionare **strumenti > Gestione pacchetti libreria > Console di gestione pacchetti**ed eseguire i seguenti comandi per i riferimenti di soluzione hello tooresolve progetto FileProvisioningAgent hello hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="3970b-188">Compilare il progetto di FileProvisioningAgent hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="3970b-189">Avvio dell'applicazione hello prompt dei comandi di Windows (come amministratore) e utilizzare hello **cd** comando toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** cartella.</span><span class="sxs-lookup"><span data-stu-id="3970b-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="3970b-190">Eseguire hello comando seguente, sostituendo < indirizzo ip > con nome hello IP indirizzo o il dominio del computer Windows hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="3970b-191">In Windows in **impostazioni di Windows > rete e le impostazioni Internet**selezionare hello **Windows Firewall > Impostazioni avanzate**e creare un **regola connessioni in entrata** che Consente l'accesso in ingresso tooport 9000.</span><span class="sxs-lookup"><span data-stu-id="3970b-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="3970b-192">Se il computer di Windows hello è protetto da un router, hello router esigenze toobe configurato tooperform traduzione di accesso di rete tra la porta 9000 che viene esposto toohello internet e la porta 9000 sul computer di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="3970b-193">Questa operazione è necessaria per Azure AD toobe in grado di tooaccess questo endpoint nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="3970b-194">**tooregister hello SCIM endpoint di esempio in Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3970b-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="3970b-195">Accedi troppo[hello Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3970b-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="3970b-196">Sfoglia troppo * * Azure Active Directory > applicazioni aziendali e selezionare **nuova applicazione > tutti > applicazione Non raccolta**.</span><span class="sxs-lookup"><span data-stu-id="3970b-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="3970b-197">Immettere un nome per l'applicazione e fare clic su **Aggiungi** icona toocreate un oggetto applicazione.</span><span class="sxs-lookup"><span data-stu-id="3970b-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="3970b-198">l'oggetto applicazione Hello creato è previsto toorepresent hello destinazione app verrebbe eseguito il provisioning dei tooand implementazione endpoint SCIM single sign-on per e non solo di hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="3970b-199">Nella schermata risultante hello selezionare hello **Provisioning** scheda nella colonna sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="3970b-200">In hello **modalità di Provisioning** dal menu **automatica**.</span><span class="sxs-lookup"><span data-stu-id="3970b-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="3970b-201">![][2]
  *Figura 4: Configurazione del provisioning in hello portale di Azure*</span><span class="sxs-lookup"><span data-stu-id="3970b-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="3970b-202">In hello **URL Tenant** immettere l'URL di hello esposto a internet e la porta dell'endpoint SCIM.</span><span class="sxs-lookup"><span data-stu-id="3970b-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="3970b-203">Si tratterà di un elemento come http://testmachine.contoso.com:9000 o http://<ip-address>:9000/, dove < indirizzo ip > è hello internet esposti IP indirizzo.</span><span class="sxs-lookup"><span data-stu-id="3970b-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="3970b-204">Se l'endpoint SCIM hello richiede un token di connessione OAuth da un'autorità di certificazione diversa da Azure AD, quindi hello copia necessari token di connessione OAuth nel hello facoltativo **segreto Token** campo.</span><span class="sxs-lookup"><span data-stu-id="3970b-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="3970b-205">Se questo campo viene lasciato vuoto, AD Azure includerà in ogni richiesta un token di connessione OAuth emesso da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="3970b-206">Le app che usano Azure AD come provider di identità possono convalidare il token rilasciato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="3970b-207">Fare clic su hello **Test connessione** endpoint SCIM pulsante toohave Azure Active Directory tentativo tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="3970b-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="3970b-208">Se hello tentativi falliscono, informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="3970b-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="3970b-209">Se un'applicazione hello tentativi tooconnect toohello esito negativo, quindi fare clic su **salvare** credenziali di amministratore toosave hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="3970b-210">In hello **mapping** sezione, sono disponibili due set di mapping degli attributi selezionabile: uno per gli oggetti utente e uno per gli oggetti di gruppo.</span><span class="sxs-lookup"><span data-stu-id="3970b-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="3970b-211">Selezionare ogni attributi di hello tooreview uno che vengono sincronizzati da app tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3970b-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="3970b-212">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello utenti e gruppi nell'app per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3970b-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="3970b-213">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="3970b-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="3970b-214">In **impostazioni**, hello **ambito** campo definisce quali gruppi di utenti e o vengono sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="3970b-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="3970b-215">Selezione di "Sincronizzazione assegnata solo gli utenti e gruppi" (scelta consigliata) verranno sincronizzate solo gli utenti e gruppi assegnati in hello **utenti e gruppi** scheda.</span><span class="sxs-lookup"><span data-stu-id="3970b-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="3970b-216">Una volta completata la configurazione, modificare hello **lo stato di Provisioning** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="3970b-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="3970b-217">Fare clic su **salvare** toostart hello servizio provisioning di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="3970b-218">Se la sincronizzazione solo assegnati a utenti e gruppi (scelta consigliati), in certi hello tooselect **utenti e gruppi** scheda e assegnare gli utenti di hello e/o gruppi di cui si desidera toosync.</span><span class="sxs-lookup"><span data-stu-id="3970b-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="3970b-219">Una volta avviata la sincronizzazione iniziale di hello, è possibile utilizzare hello **log di controllo** scheda toomonitor lo stato di avanzamento, che mostra tutte le azioni eseguite da hello provisioning del servizio nella tua app.</span><span class="sxs-lookup"><span data-stu-id="3970b-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="3970b-220">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="3970b-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="3970b-221">passaggio finale Hello verifica esempio hello è hello tooopen TargetFile.csv file nella cartella \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello sul proprio computer Windows.</span><span class="sxs-lookup"><span data-stu-id="3970b-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="3970b-222">Una volta eseguito il processo di provisioning hello, questo file Mostra dettagli hello tutte assegnati e il provisioning di utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="3970b-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="3970b-223">Librerie di sviluppo</span><span class="sxs-lookup"><span data-stu-id="3970b-223">Development libraries</span></span>
<span data-ttu-id="3970b-224">toodevelop il proprio servizio web conforme alla specifica SCIM toohello, acquisire familiarità con hello seguendo le librerie fornite da Microsoft toohelp accelerare il processo di sviluppo hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="3970b-225">Le librerie CLI (Common Language Infrastructure) vengono messe a disposizione per essere usate con linguaggi basati su questa infrastruttura, ad esempio C#.</span><span class="sxs-lookup"><span data-stu-id="3970b-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="3970b-226">Uno di tali raccolte, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), dichiara un'interfaccia, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, illustrata nella seguente figura hello: A gli sviluppatori che utilizzano le librerie di hello implementi tale interfaccia con una classe che può essere indicata, in modo generico, come un provider.</span><span class="sxs-lookup"><span data-stu-id="3970b-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="3970b-227">librerie di Hello consentono hello developer toodeploy un servizio web conforme alla specifica SCIM toohello.</span><span class="sxs-lookup"><span data-stu-id="3970b-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="3970b-228">servizio web Hello può essere sia ospitato all'interno di Internet Information Services o qualsiasi assembly di Common Language Infrastructure eseguibile.</span><span class="sxs-lookup"><span data-stu-id="3970b-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="3970b-229">Richiesta viene tradotta in metodi del provider di chiamate toohello, che potrebbero essere programmati dai toooperate developer hello in un archivio di identità.</span><span class="sxs-lookup"><span data-stu-id="3970b-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="3970b-230">[Express route gestori](http://expressjs.com/guide/routing.html) sono disponibili per l'analisi di oggetti di richiesta di Node. js che rappresentano chiamate (come definito dalla specifica SCIM hello), servizio web di tooa node.js.</span><span class="sxs-lookup"><span data-stu-id="3970b-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="3970b-231">Creazione di un endpoint SCIM personalizzato</span><span class="sxs-lookup"><span data-stu-id="3970b-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="3970b-232">Usa librerie CLI hello, gli sviluppatori che utilizzano tali librerie possono ospitare i servizi in qualsiasi assembly di Common Language Infrastructure eseguibile o in Internet Information Services.</span><span class="sxs-lookup"><span data-stu-id="3970b-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="3970b-233">Di seguito è riportato il codice di esempio per l'hosting di un servizio all'interno di un assembly eseguibile, all'indirizzo hello http://localhost:9000/objectUri:</span><span class="sxs-lookup"><span data-stu-id="3970b-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

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

<span data-ttu-id="3970b-234">Questo servizio deve disporre di un HTTP indirizzo server di autenticazione certificato di cui hello autorità di certificazione radice è uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="3970b-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="3970b-235">CNNIC</span></span>
* <span data-ttu-id="3970b-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="3970b-236">Comodo</span></span>
* <span data-ttu-id="3970b-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="3970b-237">CyberTrust</span></span>
* <span data-ttu-id="3970b-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="3970b-238">DigiCert</span></span>
* <span data-ttu-id="3970b-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="3970b-239">GeoTrust</span></span>
* <span data-ttu-id="3970b-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="3970b-240">GlobalSign</span></span>
* <span data-ttu-id="3970b-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="3970b-241">Go Daddy</span></span>
* <span data-ttu-id="3970b-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="3970b-242">Verisign</span></span>
* <span data-ttu-id="3970b-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="3970b-243">WoSign</span></span>

<span data-ttu-id="3970b-244">Un certificato di autenticazione server può essere associato tooa porta in un host Windows utilizzo hello utilità shell della rete:</span><span class="sxs-lookup"><span data-stu-id="3970b-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="3970b-245">In questo caso, il valore di hello fornito per l'argomento certhash hello è identificazione personale hello del certificato di hello, mentre il valore di hello fornito per l'argomento appid hello è un identificatore univoco globale arbitrario.</span><span class="sxs-lookup"><span data-stu-id="3970b-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="3970b-246">servizio di hello toohost all'interno di Internet Information Services, uno sviluppatore sarebbe compilare un assembly libreria di codice CLA con una classe denominata avvio nello spazio dei nomi predefinito hello dell'assembly hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="3970b-247">Ecco un esempio di questa classe:</span><span class="sxs-lookup"><span data-stu-id="3970b-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="3970b-248">Gestione dell'autenticazione dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="3970b-248">Handling endpoint authentication</span></span>
<span data-ttu-id="3970b-249">Le richieste da Azure Active Directory includono un token di connessione OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3970b-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="3970b-250">Qualsiasi richiesta di servizio ricevente hello deve eseguire l'autenticazione dell'autorità di certificazione hello come Azure Active Directory per conto di tenant di Azure Active Directory hello previsto, per l'accesso toohello servizio web di Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="3970b-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="3970b-251">In token hello emittente hello è identificato da un'attestazione iss, ad esempio, "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="3970b-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="3970b-252">In questo esempio, l'indirizzo di base del valore di attestazione hello, hello https://sts.windows.net, identifica Azure Active Directory come autorità di certificazione hello, mentre il segmento indirizzo relativo, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello è un identificatore univoco di hello Azure Active Tenant di directory per conto di quali hello token è stato rilasciato.</span><span class="sxs-lookup"><span data-stu-id="3970b-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="3970b-253">Se è stato rilasciato il token hello per accedere al servizio web di Azure Active Directory Graph hello, quindi identificatore hello di tale servizio, 00000002-0000-0000-c000-000000000000, devono essere valore hello aud del token hello di attestazioni.</span><span class="sxs-lookup"><span data-stu-id="3970b-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="3970b-254">Gli sviluppatori che utilizzano librerie CLA hello fornite da Microsoft per la creazione di un servizio SCIM possono autenticare le richieste da Azure Active Directory tramite il pacchetto di ActiveDirectory hello attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3970b-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="3970b-255">In un provider, implementare proprietà Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior hello avendolo restituire toobe un metodo chiamato ogni volta che viene avviato il servizio hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

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

2. <span data-ttu-id="3970b-256">Aggiungere hello seguente codice toothat metodo toohave tooany qualsiasi richiesta di endpoint del servizio hello autenticato come bearing un token emesso da Azure Active Directory per conto di un tenant specificato, per l'accesso toohello servizio web di Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="3970b-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="3970b-257">Schema di utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="3970b-257">User and group schema</span></span>
<span data-ttu-id="3970b-258">Azure Active Directory possono eseguire il provisioning di due tipi di servizi web tooSCIM di risorse.</span><span class="sxs-lookup"><span data-stu-id="3970b-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="3970b-259">ovvero utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="3970b-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="3970b-260">Le risorse utente sono identificate dall'identificatore di schema hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, incluso in questa specifica del protocollo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="3970b-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="3970b-261">Nella tabella 1, il mapping predefinito Hello di attributi hello degli utenti in attributi toohello Azure Active Directory delle risorse urn: ietf:params:scim:schemas:extension:enterprise:2.0:User di seguito.</span><span class="sxs-lookup"><span data-stu-id="3970b-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="3970b-262">Risorse del gruppo sono identificate dall'identificatore di schema hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="3970b-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="3970b-263">Tabella 2, di sotto, Mostra hello del mapping predefinito tra gli attributi di hello dei gruppi di attributi di Azure Active Directory toohello http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group risorse.</span><span class="sxs-lookup"><span data-stu-id="3970b-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="3970b-264">Tabella 1: mapping predefinito degli attributi utente</span><span class="sxs-lookup"><span data-stu-id="3970b-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="3970b-265">Utente Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3970b-265">Azure Active Directory user</span></span> | <span data-ttu-id="3970b-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="3970b-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="3970b-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="3970b-267">IsSoftDeleted</span></span> |<span data-ttu-id="3970b-268">active</span><span class="sxs-lookup"><span data-stu-id="3970b-268">active</span></span> |
| <span data-ttu-id="3970b-269">displayName</span><span class="sxs-lookup"><span data-stu-id="3970b-269">displayName</span></span> |<span data-ttu-id="3970b-270">displayName</span><span class="sxs-lookup"><span data-stu-id="3970b-270">displayName</span></span> |
| <span data-ttu-id="3970b-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="3970b-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="3970b-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="3970b-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="3970b-273">givenName</span><span class="sxs-lookup"><span data-stu-id="3970b-273">givenName</span></span> |<span data-ttu-id="3970b-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="3970b-274">name.givenName</span></span> |
| <span data-ttu-id="3970b-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="3970b-275">jobTitle</span></span> |<span data-ttu-id="3970b-276">title</span><span class="sxs-lookup"><span data-stu-id="3970b-276">title</span></span> |
| <span data-ttu-id="3970b-277">mail</span><span class="sxs-lookup"><span data-stu-id="3970b-277">mail</span></span> |<span data-ttu-id="3970b-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="3970b-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="3970b-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="3970b-279">mailNickname</span></span> |<span data-ttu-id="3970b-280">externalId</span><span class="sxs-lookup"><span data-stu-id="3970b-280">externalId</span></span> |
| <span data-ttu-id="3970b-281">manager</span><span class="sxs-lookup"><span data-stu-id="3970b-281">manager</span></span> |<span data-ttu-id="3970b-282">manager</span><span class="sxs-lookup"><span data-stu-id="3970b-282">manager</span></span> |
| <span data-ttu-id="3970b-283">mobile</span><span class="sxs-lookup"><span data-stu-id="3970b-283">mobile</span></span> |<span data-ttu-id="3970b-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="3970b-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="3970b-285">objectId</span><span class="sxs-lookup"><span data-stu-id="3970b-285">objectId</span></span> |<span data-ttu-id="3970b-286">id</span><span class="sxs-lookup"><span data-stu-id="3970b-286">id</span></span> |
| <span data-ttu-id="3970b-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="3970b-287">postalCode</span></span> |<span data-ttu-id="3970b-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="3970b-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="3970b-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="3970b-289">proxy-Addresses</span></span> |<span data-ttu-id="3970b-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="3970b-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="3970b-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="3970b-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="3970b-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="3970b-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="3970b-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="3970b-293">streetAddress</span></span> |<span data-ttu-id="3970b-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="3970b-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="3970b-295">surname</span><span class="sxs-lookup"><span data-stu-id="3970b-295">surname</span></span> |<span data-ttu-id="3970b-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="3970b-296">name.familyName</span></span> |
| <span data-ttu-id="3970b-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="3970b-297">telephone-Number</span></span> |<span data-ttu-id="3970b-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="3970b-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="3970b-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="3970b-299">user-PrincipalName</span></span> |<span data-ttu-id="3970b-300">userName</span><span class="sxs-lookup"><span data-stu-id="3970b-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="3970b-301">Tabella 2: mapping predefinito degli attributi gruppo</span><span class="sxs-lookup"><span data-stu-id="3970b-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="3970b-302">Gruppo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3970b-302">Azure Active Directory group</span></span> | <span data-ttu-id="3970b-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="3970b-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="3970b-304">displayName</span><span class="sxs-lookup"><span data-stu-id="3970b-304">displayName</span></span> |<span data-ttu-id="3970b-305">externalId</span><span class="sxs-lookup"><span data-stu-id="3970b-305">externalId</span></span> |
| <span data-ttu-id="3970b-306">mail</span><span class="sxs-lookup"><span data-stu-id="3970b-306">mail</span></span> |<span data-ttu-id="3970b-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="3970b-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="3970b-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="3970b-308">mailNickname</span></span> |<span data-ttu-id="3970b-309">displayName</span><span class="sxs-lookup"><span data-stu-id="3970b-309">displayName</span></span> |
| <span data-ttu-id="3970b-310">Membri di</span><span class="sxs-lookup"><span data-stu-id="3970b-310">members</span></span> |<span data-ttu-id="3970b-311">Membri di</span><span class="sxs-lookup"><span data-stu-id="3970b-311">members</span></span> |
| <span data-ttu-id="3970b-312">objectId</span><span class="sxs-lookup"><span data-stu-id="3970b-312">objectId</span></span> |<span data-ttu-id="3970b-313">id</span><span class="sxs-lookup"><span data-stu-id="3970b-313">id</span></span> |
| <span data-ttu-id="3970b-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="3970b-314">proxyAddresses</span></span> |<span data-ttu-id="3970b-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="3970b-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="3970b-316">Provisioning e deprovisioning utenti</span><span class="sxs-lookup"><span data-stu-id="3970b-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="3970b-317">Hello nella seguente illustrazione mostra i messaggi hello che Azure Active Directory invia tooa SCIM servizio toomanage hello del ciclo di vita di un utente nell'archivio identità di un altro.</span><span class="sxs-lookup"><span data-stu-id="3970b-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="3970b-318">diagramma di Hello Mostra anche come un servizio SCIM implementato utilizzando librerie CLI hello fornito da Microsoft per la creazione di che tali servizi traducono toohello chiama i metodi di un provider di tali richieste.</span><span class="sxs-lookup"><span data-stu-id="3970b-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="3970b-319">![][4]
*Figura 5: Sequenza di provisioning e deprovisioning utenti*</span><span class="sxs-lookup"><span data-stu-id="3970b-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="3970b-320">Query di Active Directory di Azure hello servizio per un utente con un valore di attributo externalId corrispondente valore dell'attributo mailNickname hello di un utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3970b-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="3970b-321">query Hello viene espresso come una richiesta di protocollo HTTP (Hypertext Transfer), ad esempio in questo esempio, in cui jyoung è un esempio di un mailNickname di un utente in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="3970b-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3970b-322">Se il servizio di hello è stato creato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM, richiesta hello viene convertito in un metodo di Query del provider del servizio hello di toohello chiamata.</span><span class="sxs-lookup"><span data-stu-id="3970b-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="3970b-323">Questa è hello firma del metodo:</span><span class="sxs-lookup"><span data-stu-id="3970b-323">Here is hello signature of that method:</span></span> 
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
  <span data-ttu-id="3970b-324">Di seguito è la definizione hello dell'interfaccia Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="3970b-325">Nel seguente esempio di una query per un utente con un valore specificato per l'attributo externalId hello di hello, i valori degli argomenti di hello passati toohello metodo di Query sono:</span><span class="sxs-lookup"><span data-stu-id="3970b-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="3970b-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="3970b-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="3970b-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="3970b-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="3970b-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="3970b-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="3970b-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="3970b-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="3970b-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="3970b-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="3970b-331">Se nessun utente restituito hello risposta tooa toohello servizio web di query per un utente con un valore di attributo externalId che corrisponda al valore di attributo mailNickname hello di un utente, Azure Active Directory richiede che il provisioning del servizio hello un utente corrispondente toohello uno in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3970b-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="3970b-332">Ecco un esempio di questa richiesta:</span><span class="sxs-lookup"><span data-stu-id="3970b-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="3970b-333">librerie di Common Language Infrastructure Hello fornite da Microsoft per l'implementazione di servizi SCIM Converte la richiesta in toohello una chiamata di metodo di creazione del provider del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="3970b-334">Hello metodo Create con questa firma:</span><span class="sxs-lookup"><span data-stu-id="3970b-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="3970b-335">In una richiesta tooprovision un utente, il valore di hello dell'argomento resource hello è un'istanza di hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="3970b-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="3970b-336">Classe Core2EnterpriseUser definiti nella libreria Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="3970b-337">Se ha esito positivo hello richiesta tooprovision hello utente, quindi hello implementazione del metodo hello è previsto tooreturn un'istanza di hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="3970b-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="3970b-338">Classe Core2EnterpriseUser, con valore hello della proprietà identificatore hello imposta toohello identificatore univoco dell'utente appena sottoposti a provisioning hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="3970b-339">tooupdate un utente, noto in un archivio di identità tooexist applicazioni da un SCIM, Azure Active Directory viene eseguito tramite la richiesta di stato corrente di hello di tale utente dal servizio hello con una richiesta, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3970b-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3970b-340">In un servizio compilato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM richiesta hello viene tradotta in toohello una chiamata di metodo di recupero del provider del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="3970b-341">Questa è hello firma del metodo di recupero hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-341">Here is hello signature of hello Retrieve method:</span></span> 
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
  <span data-ttu-id="3970b-342">Nell'esempio hello di uno stato corrente di hello tooretrieve richiesta di un utente, valori hello proprietà hello dell'oggetto di hello fornito come valore di hello dell'argomento parametri hello sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="3970b-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="3970b-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3970b-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3970b-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3970b-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="3970b-345">Se un attributo di riferimento è toobe aggiornato, quindi Azure Active Directory query hello servizio toodetermine o meno hello valore corrente dell'attributo di riferimento hello nell'archivio identità hello applicazioni dal servizio hello già corrisponde hello di tale attributo in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3970b-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="3970b-346">Per gli utenti, unico attributo hello di quali hello valore corrente viene eseguita una query in questo modo è l'attributo manager hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="3970b-347">Ecco un esempio di una richiesta di toodetermine se l'attributo manager hello di un oggetto utente specifico dispone attualmente di un determinato valore:</span><span class="sxs-lookup"><span data-stu-id="3970b-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3970b-348">valore di Hello hello gli attributi parametro della query, id, significa che se esiste un oggetto utente che soddisfa l'espressione hello fornita come valore di hello del parametro di query di filtro hello, il servizio hello toorespond previsto con un urn: ietf:params:scim:schemas: risorsa core: 2.0:User o urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, inclusi hello solo il valore dell'attributo id della risorsa.</span><span class="sxs-lookup"><span data-stu-id="3970b-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="3970b-349">valore di hello Hello **id** noto toohello richiedente.</span><span class="sxs-lookup"><span data-stu-id="3970b-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="3970b-350">È incluso nel valore di hello del parametro di query di filtro hello; Hello richiede mira effettivamente toorequest una rappresentazione minima di una risorsa esistente che soddisfano l'espressione di filtro hello come indicazione della o meno tale oggetto.</span><span class="sxs-lookup"><span data-stu-id="3970b-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="3970b-351">Se il servizio di hello è stato creato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM, richiesta hello viene convertito in un metodo di Query del provider del servizio hello di toohello chiamata.</span><span class="sxs-lookup"><span data-stu-id="3970b-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="3970b-352">il valore di Hello proprietà hello dell'oggetto di hello fornito come valore di hello dell'argomento parametri hello sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="3970b-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="3970b-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="3970b-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="3970b-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="3970b-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="3970b-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="3970b-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="3970b-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3970b-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3970b-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="3970b-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="3970b-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="3970b-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="3970b-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="3970b-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="3970b-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="3970b-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="3970b-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3970b-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="3970b-362">In questo caso, il valore di hello dell'indice di hello x può essere 0 e valore hello hello indice y può essere 1, o valore hello di x può essere 1 e valore hello y può essere 0, a seconda dell'ordine di hello di espressioni hello hello filtro del parametro della query.</span><span class="sxs-lookup"><span data-stu-id="3970b-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="3970b-363">Di seguito è riportato un esempio di una richiesta da Azure Active Directory tooan SCIM servizio tooupdate un utente:</span><span class="sxs-lookup"><span data-stu-id="3970b-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
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
  <span data-ttu-id="3970b-364">librerie di Microsoft Common Language Infrastructure Hello per l'implementazione di servizi SCIM converte richiesta hello in toohello una chiamata di metodo di aggiornamento del provider del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3970b-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="3970b-365">Questa è hello firma del metodo Update hello:</span><span class="sxs-lookup"><span data-stu-id="3970b-365">Here is hello signature of hello Update method:</span></span> 
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
    <span data-ttu-id="3970b-366">Nell'esempio hello di tooupdate una richiesta utente oggetto hello fornito come valore di hello dell'argomento di patch hello presenta questi valori di proprietà:</span><span class="sxs-lookup"><span data-stu-id="3970b-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="3970b-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3970b-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3970b-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3970b-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="3970b-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="3970b-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="3970b-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="3970b-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="3970b-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="3970b-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="3970b-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="3970b-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="3970b-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="3970b-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="3970b-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="3970b-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="3970b-375">un utente da un archivio di identità di effettuare il provisioning di toode applicazioni da un servizio SCIM, Azure AD invia una richiesta, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3970b-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="3970b-376">Se il servizio di hello è stato creato utilizzando le librerie di Common Language Infrastructure hello fornite da Microsoft per l'implementazione di servizi SCIM, richiesta hello viene convertito in un metodo di eliminazione del provider del servizio di hello di toohello chiamata.</span><span class="sxs-lookup"><span data-stu-id="3970b-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="3970b-377">Il metodo ha la firma seguente:</span><span class="sxs-lookup"><span data-stu-id="3970b-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="3970b-378">oggetto Hello fornito come valore di hello dell'argomento resourceIdentifier hello presenta questi valori di proprietà nell'esempio hello di una richiesta toode a disposizione un utente:</span><span class="sxs-lookup"><span data-stu-id="3970b-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="3970b-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="3970b-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="3970b-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="3970b-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="3970b-381">Provisioning e deprovisioning gruppi</span><span class="sxs-lookup"><span data-stu-id="3970b-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="3970b-382">Hello nella seguente figura mostra i messaggi hello che Azure AcD invia tooa SCIM servizio toomanage hello del ciclo di vita di un gruppo in un altro archivio identità.</span><span class="sxs-lookup"><span data-stu-id="3970b-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="3970b-383">Tali messaggi sono diversi dai messaggi hello riguardano toousers in tre modi:</span><span class="sxs-lookup"><span data-stu-id="3970b-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="3970b-384">schema di Hello di una risorsa del gruppo viene identificato come http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="3970b-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="3970b-385">Richieste tooretrieve gruppi stabiliscono tale attributo membri hello è escluso da qualsiasi risorsa fornita nella richiesta di risposta toohello toobe.</span><span class="sxs-lookup"><span data-stu-id="3970b-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="3970b-386">Se un attributo di riferimento dispone di un determinato valore sono richieste sull'attributo membri hello toodetermine di richieste.</span><span class="sxs-lookup"><span data-stu-id="3970b-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="3970b-387">![][5]
*Figura 6: Sequenza di provisioning e deprovisioning gruppi*</span><span class="sxs-lookup"><span data-stu-id="3970b-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="3970b-388">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="3970b-388">Related articles</span></span>
* [<span data-ttu-id="3970b-389">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3970b-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="3970b-390">Automatizzare tooSaaS utente Provisioning o Deprovisioning App</span><span class="sxs-lookup"><span data-stu-id="3970b-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="3970b-391">Personalizzazione dei mapping degli attributi per il Provisioning dell’utente</span><span class="sxs-lookup"><span data-stu-id="3970b-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="3970b-392">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="3970b-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="3970b-393">Ambito dei filtri per il Provisioning utente</span><span class="sxs-lookup"><span data-stu-id="3970b-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="3970b-394">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="3970b-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="3970b-395">Elenco di esercitazioni sulla tooIntegrate App SaaS</span><span class="sxs-lookup"><span data-stu-id="3970b-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG

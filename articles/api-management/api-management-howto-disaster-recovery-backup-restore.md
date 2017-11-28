---
title: ripristino di emergenza aaaImplement tramite backup e ripristino in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toouse di backup e ripristino di emergenza tooperform in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="03a6c-103">Come tooimplement il ripristino di emergenza tramite servizio di backup e ripristino in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="03a6c-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="03a6c-104">Per la scelta toopublish e gestire le API tramite Gestione API di Azure consente di usufruire di molte errore tolleranza di errore e l'infrastruttura di funzionalità che altrimenti sarebbe toodesign, implementare e gestire.</span><span class="sxs-lookup"><span data-stu-id="03a6c-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="03a6c-105">Hello piattaforma Azure riduce gran parte di potenziali errori a una frazione del costo di hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="03a6c-106">toorecover da problemi di disponibilità hello regione in cui il servizio Gestione API di hosting si deve essere pronta tooreconstitute il servizio in un'area diversa in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="03a6c-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="03a6c-107">A seconda di obiettivi di disponibilità e obiettivo tempo di ripristino si tooreserve un servizio di backup in una o più aree e provare toomaintain loro configurazione e la sincronizzazione con servizi attivi hello contenuto.</span><span class="sxs-lookup"><span data-stu-id="03a6c-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="03a6c-108">backup del servizio Hello e funzionalità di ripristino fornisce hello, i blocchi necessari per implementare la strategia di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="03a6c-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="03a6c-109">Questa guida viene illustrato come le richieste tooauthenticate Gestione risorse di Azure e come toobackup e ripristinare le istanze del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="03a6c-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="03a6c-110">Hello processo di backup e ripristino di un'istanza del servizio Gestione API per il ripristino di emergenza può essere utilizzato anche per la replica delle istanze del servizio Gestione API per scenari come la gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="03a6c-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="03a6c-111">Si noti che ogni backup scade dopo 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="03a6c-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="03a6c-112">Se si tenta di toorestore una copia di backup dopo il periodo di scadenza 30 giorni hello è scaduto, ripristino hello avrà esito negativo con un `Cannot restore: backup expired` messaggio.</span><span class="sxs-lookup"><span data-stu-id="03a6c-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="03a6c-113">Autenticazione delle richieste di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="03a6c-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="03a6c-114">Hello API REST per il backup e ripristino Usa Gestione risorse di Azure e presenta un meccanismo di autenticazione diverso rispetto ai hello API REST per gestire le entità di gestione API.</span><span class="sxs-lookup"><span data-stu-id="03a6c-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="03a6c-115">Hello in questa sezione viene descritta la modalità Azure Resource Manager tooauthenticate richieste.</span><span class="sxs-lookup"><span data-stu-id="03a6c-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="03a6c-116">Per altre informazioni, vedere [Autenticazione delle richieste di Gestione risorse di Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="03a6c-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="03a6c-117">Tutte le attività hello che vengono eseguite sulle risorse usando hello Azure Resource Manager deve essere autenticate con Azure Active Directory tramite hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="03a6c-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="03a6c-118">Aggiungere un tenant di Azure Active Directory toohello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="03a6c-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="03a6c-119">Impostare le autorizzazioni per un'applicazione hello che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="03a6c-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="03a6c-120">Ottenere il token di hello per autenticare le richieste tooAzure Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="03a6c-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="03a6c-121">primo passaggio Hello è toocreate un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="03a6c-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="03a6c-122">Accedere hello [portale di Azure classico](http://manage.windowsazure.com/) mediante sottoscrizione hello che contiene il servizio Gestione API dell'istanza e passare toohello **applicazioni** scheda per il valore predefinito di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="03a6c-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="03a6c-123">Se directory predefinita di hello Azure Active Directory non è visibile tooyour account, l'amministratore di hello contatto di hello toogrant di sottoscrizione di Azure hello richiesto tooyour autorizzazioni account.</span><span class="sxs-lookup"><span data-stu-id="03a6c-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Creare un'applicazione Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="03a6c-125">Fare clic su **Aggiungi**, **Aggiungi un'applicazione che l'organizzazione sta sviluppando**, quindi scegliere **Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="03a6c-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="03a6c-126">Immettere un nome descrittivo e fare clic sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="03a6c-127">Immettere un URL di segnaposto, ad esempio `http://resources` per hello **URI di reindirizzamento**, come è un campo obbligatorio, ma il valore di hello non viene usato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="03a6c-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="03a6c-128">Fare clic su un'applicazione hello toosave hello casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="03a6c-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="03a6c-129">Dopo aver salvata un'applicazione hello, fare clic su **configura**, scorrere verso il basso toohello **autorizzazioni tooother applicazioni** sezione e fare clic su **aggiungere applicazione**.</span><span class="sxs-lookup"><span data-stu-id="03a6c-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![Aggiungere autorizzazioni][api-management-aad-permissions-add]

<span data-ttu-id="03a6c-131">Selezionare **Windows** **API di gestione del servizio di Azure** e fare clic su un'applicazione hello tooadd hello casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="03a6c-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![Aggiungere autorizzazioni][api-management-aad-permissions]

<span data-ttu-id="03a6c-133">Fare clic su **autorizzazioni delegate** accanto a hello appena aggiunto **Windows** **API di gestione del servizio di Azure** applicazione hello casella per **accesso Azure Gestione dei servizi (anteprima)**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="03a6c-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Aggiungere autorizzazioni][api-management-aad-delegated-permissions]

<span data-ttu-id="03a6c-135">Tooinvoking precedente hello API che generano hello backup e ripristino, è necessario tooget un token.</span><span class="sxs-lookup"><span data-stu-id="03a6c-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="03a6c-136">esempio Hello utilizza hello [ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token di hello tooretrieve pacchetto nuget.</span><span class="sxs-lookup"><span data-stu-id="03a6c-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="03a6c-137">Sostituire `{tentand id}`, `{application id}`, e `{redirect uri}` utilizzando hello attenendosi alle istruzioni.</span><span class="sxs-lookup"><span data-stu-id="03a6c-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="03a6c-138">Sostituire `{tenant id}` con l'id tenant hello di hello applicazione Azure Active Directory appena creata.</span><span class="sxs-lookup"><span data-stu-id="03a6c-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="03a6c-139">È possibile accedere id hello facendo **visualizzare endpoint**.</span><span class="sxs-lookup"><span data-stu-id="03a6c-139">You can access hello id by clicking **View endpoints**.</span></span>

![Endpoint][api-management-aad-default-directory]

![Endpoint][api-management-endpoint]

<span data-ttu-id="03a6c-142">Sostituire `{application id}` e `{redirect uri}` utilizzando hello **Id Client** e hello URL da hello **Redirect Uris** sezione dall'applicazione Azure Active Directory **Configura**  scheda.</span><span class="sxs-lookup"><span data-stu-id="03a6c-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Risorse][api-management-aad-resources]

<span data-ttu-id="03a6c-144">Una volta specificati i valori hello, esempio di codice hello deve restituire un token toohello simile esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="03a6c-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![token][api-management-arm-token]

<span data-ttu-id="03a6c-146">Prima di chiamare il metodo hello backup e ripristinare le operazioni descritte nelle sezioni che seguono hello, impostare l'intestazione della richiesta hello autorizzazione per la chiamata REST.</span><span class="sxs-lookup"><span data-stu-id="03a6c-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="03a6c-147"><a name="step1"> </a>Backup di un servizio di Gestione API</span><span class="sxs-lookup"><span data-stu-id="03a6c-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="03a6c-148">tooback backup un hello problema del servizio Gestione API richiesta HTTP seguente:</span><span class="sxs-lookup"><span data-stu-id="03a6c-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="03a6c-149">dove:</span><span class="sxs-lookup"><span data-stu-id="03a6c-149">where:</span></span>

* <span data-ttu-id="03a6c-150">`subscriptionId`-id della sottoscrizione hello contenente il servizio di gestione API hello che si sta tentando di toobackup</span><span class="sxs-lookup"><span data-stu-id="03a6c-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="03a6c-151">`resourceGroupName`-stringa nel formato hello "Api - predefinito-{servizio region}" dove `service-region` identifica hello regione di Azure in cui è ospitato il servizio Gestione API che si sta tentando di toobackup hello, ad esempio,`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="03a6c-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="03a6c-152">`serviceName`-nome hello del servizio Gestione API effettuare un backup di specificata in fase di creazione di hello hello</span><span class="sxs-lookup"><span data-stu-id="03a6c-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="03a6c-153">`api-version` - sostituire con `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="03a6c-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="03a6c-154">Nel corpo della richiesta di hello hello specificare nome account di archiviazione di Azure di destinazione hello, chiave di accesso, nome del contenitore blob e nome backup:</span><span class="sxs-lookup"><span data-stu-id="03a6c-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="03a6c-155">Impostare il valore di hello di hello `Content-Type` intestazione della richiesta troppo`application/json`.</span><span class="sxs-lookup"><span data-stu-id="03a6c-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="03a6c-156">Copia di backup è un'operazione a esecuzione prolungata che potrebbero essere necessari più toocomplete minuti.</span><span class="sxs-lookup"><span data-stu-id="03a6c-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="03a6c-157">Se hello richiesta ha esito positivo e processo di backup hello è stata avviata, riceverai un `202 Accepted` codice di stato di risposta con un `Location` intestazione.</span><span class="sxs-lookup"><span data-stu-id="03a6c-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="03a6c-158">Verificare 'GET' richiede URL di toohello in hello `Location` toofind intestazione stato hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="03a6c-159">Mentre è in corso il backup di hello continuerà tooreceive un codice di stato "202 accettato".</span><span class="sxs-lookup"><span data-stu-id="03a6c-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="03a6c-160">Un codice di risposta `200 OK` indicherà il completamento dell'operazione di backup hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="03a6c-161">Nota: hello seguenti vincoli quando si effettua una richiesta di backup.</span><span class="sxs-lookup"><span data-stu-id="03a6c-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="03a6c-162">**Contenitore** specificato nel corpo della richiesta hello **deve esistere**.</span><span class="sxs-lookup"><span data-stu-id="03a6c-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="03a6c-163">Mentre il backup è in corso, **non tentare di eseguire alcuna operazione di gestione dei servizi** , ad esempio l'aggiornamento o il downgrade di SKU, la modifica di nomi di dominio e così via.</span><span class="sxs-lookup"><span data-stu-id="03a6c-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="03a6c-164">Ripristino di un **backup è garantito solo per 30 giorni** dall'istante hello della creazione.</span><span class="sxs-lookup"><span data-stu-id="03a6c-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="03a6c-165">**Dati di utilizzo** utilizzata per creare report analitica **non è incluso** nel backup hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="03a6c-166">Utilizzare [API REST gestione API di Azure] [ Azure API Management REST API] tooperiodically recuperare i report di analitica per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="03a6c-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="03a6c-167">frequenza di Hello con cui si esegue il backup del servizio avrà effetto sull'obiettivo del punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="03a6c-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="03a6c-168">è consigliabile implementare backup regolari, nonché l'esecuzione di backup su richiesta dopo aver apportato importante toominimize modifica tooyour servizio di gestione API.</span><span class="sxs-lookup"><span data-stu-id="03a6c-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="03a6c-169">**Le modifiche** toohello effettuata configurazione del servizio (ad esempio, API, criteri, aspetto del portale per sviluppatori) durante l'operazione di backup è in corso **potrebbero non essere inclusi nel backup hello e pertanto andranno persi**.</span><span class="sxs-lookup"><span data-stu-id="03a6c-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="03a6c-170"><a name="step2"></a>Ripristino di un servizio di Gestione API</span><span class="sxs-lookup"><span data-stu-id="03a6c-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="03a6c-171">un servizio di gestione API da un backup creato in precedenza toorestore apportare hello seguente richiesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="03a6c-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="03a6c-172">dove:</span><span class="sxs-lookup"><span data-stu-id="03a6c-172">where:</span></span>

* <span data-ttu-id="03a6c-173">`subscriptionId`-id della sottoscrizione hello contenente si ripristina un backup nel servizio di gestione API hello</span><span class="sxs-lookup"><span data-stu-id="03a6c-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="03a6c-174">`resourceGroupName`-stringa nel formato hello "Api - predefinito-{servizio region}" dove `service-region` identifica hello regione di Azure in cui è ospitato hello si ripristina un backup nel servizio di gestione API, ad esempio,`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="03a6c-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="03a6c-175">`serviceName`-nome hello di hello gestione API del servizio in fase di ripristino specificato in fase di hello della creazione</span><span class="sxs-lookup"><span data-stu-id="03a6c-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="03a6c-176">`api-version` - sostituire con `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="03a6c-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="03a6c-177">Nel corpo della richiesta di hello hello specificare percorso file di backup hello, ad esempio nome account di archiviazione di Azure, chiave di accesso, nome del contenitore blob e nome backup:</span><span class="sxs-lookup"><span data-stu-id="03a6c-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="03a6c-178">Impostare il valore di hello di hello `Content-Type` intestazione della richiesta troppo`application/json`.</span><span class="sxs-lookup"><span data-stu-id="03a6c-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="03a6c-179">Il ripristino è un'operazione a esecuzione prolungata che potrebbe essere too30 o altre toocomplete minuti.</span><span class="sxs-lookup"><span data-stu-id="03a6c-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="03a6c-180">Se hello richiesta è stata completata ed è stato avviato il processo di ripristino hello si riceverà un `202 Accepted` codice di stato di risposta con un `Location` intestazione.</span><span class="sxs-lookup"><span data-stu-id="03a6c-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="03a6c-181">Verificare 'GET' richiede URL di toohello in hello `Location` toofind intestazione stato hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="03a6c-182">Durante l'esecuzione di restore hello continuerà tooreceive '202 accettato' codice di stato.</span><span class="sxs-lookup"><span data-stu-id="03a6c-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="03a6c-183">Un codice di risposta `200 OK` indicherà il completamento dell'operazione di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03a6c-184">**Hello SKU** del servizio hello in fase di ripristino **deve corrispondere** hello SKU di hello backup del servizio in corso il ripristino.</span><span class="sxs-lookup"><span data-stu-id="03a6c-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="03a6c-185">**Le modifiche** toohello effettuata configurazione del servizio (ad esempio, API, criteri, aspetto del portale per sviluppatori) durante l'operazione di ripristino è in corso **potrebbero essere sovrascritti**.</span><span class="sxs-lookup"><span data-stu-id="03a6c-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="03a6c-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03a6c-186">Next steps</span></span>
<span data-ttu-id="03a6c-187">Estrarre hello seguente blog di Microsoft per le due procedure dettagliate diverse del processo di backup/ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="03a6c-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="03a6c-188">Replicare account di Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="03a6c-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="03a6c-189">Grazie a tooGisela per articolo toothis contributo.</span><span class="sxs-lookup"><span data-stu-id="03a6c-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="03a6c-190">Gestione API di Azure: Backup e ripristino della configurazione</span><span class="sxs-lookup"><span data-stu-id="03a6c-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="03a6c-191">approccio Hello dettagliata Stuart non corrisponde a informazioni aggiuntive ufficiale hello ma è molto interessante.</span><span class="sxs-lookup"><span data-stu-id="03a6c-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png

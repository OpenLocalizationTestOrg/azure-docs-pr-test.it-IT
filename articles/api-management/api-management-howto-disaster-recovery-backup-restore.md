---
title: Implementare il ripristino di emergenza usando il backup e il ripristino in Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come usare il backup e il ripristino per eseguire il ripristino di emergenza in Gestione API di Azure.
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="a4aee-103">Come implementare il ripristino di emergenza usando il backup e il ripristino dei servizi in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a4aee-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="a4aee-104">Scegliendo di pubblicare e gestire le API tramite Gestione API di Azure è possibile sfruttare molte funzionalità di tolleranza di errore e di infrastruttura che sarebbe altrimenti necessario progettare, implementare e gestire.</span><span class="sxs-lookup"><span data-stu-id="a4aee-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="a4aee-105">La piattaforma di Azure permette di mitigare una vasta gamma di potenziali errori a un costo nettamente inferiore.</span><span class="sxs-lookup"><span data-stu-id="a4aee-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="a4aee-106">Per risolvere i problemi di disponibilità che colpiscono l'area in cui è ospitato il servizio di Gestione API, è necessario essere pronti a ripristinare il servizio in un'area diversa in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="a4aee-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="a4aee-107">In base ai propri obiettivi in termini di disponibilità e tempi di ripristino, è consigliabile riservare un servizio di backup in una o più aree e provare a mantenere sincronizzati la configurazione e il contenuto con il servizio attivo.</span><span class="sxs-lookup"><span data-stu-id="a4aee-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="a4aee-108">La funzionalità di backup e ripristino dei servizi fornisce il blocco predefinito necessario per implementare la propria strategia di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="a4aee-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="a4aee-109">Questa guida descrive come autenticare le richieste di Gestione risorse di Azure e come eseguire il backup e ripristinare le istanze del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a4aee-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="a4aee-110">Il processo di backup e ripristino di un'istanza del servizio Gestione API per il ripristino di emergenza può essere usato anche per la replica delle istanze del servizio Gestione API per scenari quali la gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="a4aee-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="a4aee-111">Si noti che ogni backup scade dopo 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="a4aee-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="a4aee-112">Se si tenta di ripristinare un backup dopo la scadenza del periodo di 30 giorni, il ripristino avrà esito negativo e verrà visualizzato il messaggio `Cannot restore: backup expired` .</span><span class="sxs-lookup"><span data-stu-id="a4aee-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="a4aee-113">Autenticazione delle richieste di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="a4aee-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a4aee-114">L'API REST per il backup e ripristino usa Gestione risorse di Azure e include un meccanismo di autenticazione diverso rispetto alle API REST per la gestione delle entità di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a4aee-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="a4aee-115">I passaggi descritti in questa sezione descrivono come autenticare le richieste di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4aee-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="a4aee-116">Per altre informazioni, vedere [Autenticazione delle richieste di Gestione risorse di Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4aee-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="a4aee-117">Tutte le attività che è possibile eseguire sulle risorse tramite Gestione risorse di Azure devono essere autenticate con Azure Active Directory usando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="a4aee-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="a4aee-118">Aggiungere un'applicazione al tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4aee-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="a4aee-119">Impostare le autorizzazioni per l'applicazione aggiunta.</span><span class="sxs-lookup"><span data-stu-id="a4aee-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="a4aee-120">Ottenere il token per autenticare le richieste a Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4aee-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="a4aee-121">Il primo passaggio consiste nel creare un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4aee-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="a4aee-122">Accedere al [portale di Azure classico](http://manage.windowsazure.com/) usando la sottoscrizione che include l'istanza del servizio Gestione API e passare alla scheda **Applicazioni** per la directory predefinita di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4aee-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="a4aee-123">Se la directory predefinita di Azure Active Directory non è visibile nel proprio account, contattare l'amministratore della sottoscrizione di Azure perché conceda le autorizzazioni necessarie per l'account.</span><span class="sxs-lookup"><span data-stu-id="a4aee-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Creare un'applicazione Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="a4aee-125">Fare clic su **Aggiungi**, **Aggiungi un'applicazione che l'organizzazione sta sviluppando**, quindi scegliere **Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="a4aee-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="a4aee-126">Immettere un nome descrittivo e fare clic sulla freccia Avanti.</span><span class="sxs-lookup"><span data-stu-id="a4aee-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="a4aee-127">Immettere un URL di segnaposto, ad esempio `http://resources` per **URI di reindirizzamento**, che è un campo obbligatorio, ma il valore non viene usato in seguito.</span><span class="sxs-lookup"><span data-stu-id="a4aee-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="a4aee-128">Selezionare la casella di controllo per salvare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4aee-128">Click the check box to save the application.</span></span>

<span data-ttu-id="a4aee-129">Dopo il salvataggio dell'applicazione, fare clic su **Configura**, scorrere verso il basso fino alla sezione **Autorizzazioni per altre applicazioni** e fare clic su **Aggiungi applicazione**.</span><span class="sxs-lookup"><span data-stu-id="a4aee-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![Aggiungere autorizzazioni][api-management-aad-permissions-add]

<span data-ttu-id="a4aee-131">Selezionare **Windows** **API di gestione del servizio Microsoft Azure** e fare clic sulla casella di controllo per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4aee-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![Aggiungere autorizzazioni][api-management-aad-permissions]

<span data-ttu-id="a4aee-133">Fare clic su **Autorizzazioni delegate** accanto all'applicazione di **Windows** **API di gestione del servizio Microsoft Azure** appena aggiunta, selezionare la casella per **Accesso a Gestione del servizio Azure (anteprima)** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a4aee-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Aggiungere autorizzazioni][api-management-aad-delegated-permissions]

<span data-ttu-id="a4aee-135">Prima di richiamare le API che generano il backup e ripristino, è necessario ottenere un token.</span><span class="sxs-lookup"><span data-stu-id="a4aee-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="a4aee-136">L'esempio seguente usa il pacchetto NuGet [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) per recuperare il token.</span><span class="sxs-lookup"><span data-stu-id="a4aee-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="a4aee-137">Sostituire `{tentand id}`, `{application id}` e `{redirect uri}` usando le istruzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="a4aee-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="a4aee-138">Sostituire `{tenant id}` con l'ID tenant dell'applicazione Azure Active Directory appena creata.</span><span class="sxs-lookup"><span data-stu-id="a4aee-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="a4aee-139">È possibile accedere all'ID facendo clic su **Visualizza endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a4aee-139">You can access the id by clicking **View endpoints**.</span></span>

![Endpoint][api-management-aad-default-directory]

![Endpoint][api-management-endpoint]

<span data-ttu-id="a4aee-142">Sostituire `{application id}` e `{redirect uri}` usando l'**ID client** e l'URL dalla sezione **URI di reindirizzamento** dalla scheda **Configura** dell'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4aee-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Risorse][api-management-aad-resources]

<span data-ttu-id="a4aee-144">Dopo avere specificato i valori, l'esempio di codice dovrebbe restituire un token simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="a4aee-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![Token][api-management-arm-token]

<span data-ttu-id="a4aee-146">Prima di chiamare le operazioni di backup e ripristino descritte nelle sezioni seguenti, impostare l'intestazione della richiesta di autorizzazione per la chiamata REST.</span><span class="sxs-lookup"><span data-stu-id="a4aee-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="a4aee-147"><a name="step1"> </a>Backup di un servizio di Gestione API</span><span class="sxs-lookup"><span data-stu-id="a4aee-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="a4aee-148">Per eseguire il backup di un servizio di gestione API, emettere la seguente richiesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="a4aee-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="a4aee-149">dove:</span><span class="sxs-lookup"><span data-stu-id="a4aee-149">where:</span></span>

* <span data-ttu-id="a4aee-150">`subscriptionId` : ID della sottoscrizione contenente il servizio di Gestione API di cui si sta tentando di eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="a4aee-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="a4aee-151">`resourceGroupName`: una stringa nel formato "Api-Default-{service-region}", dove `service-region` identifica l'area di Azure in cui è ospitato il servizio di Gestione API di cui si sta tentando di eseguire il backup, ad esempio `North-Central-US`.</span><span class="sxs-lookup"><span data-stu-id="a4aee-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="a4aee-152">`serviceName` : il nome del servizio di Gestione API di cui sta eseguendo il backup specificato quando è stato creato.</span><span class="sxs-lookup"><span data-stu-id="a4aee-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="a4aee-153">`api-version` - sostituire con `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="a4aee-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="a4aee-154">Nel corpo della richiesta, specificare il nome dell'account di archiviazione, la chiave di accesso, il nome del contenitore BLOB e il nome del backup di destinazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="a4aee-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="a4aee-155">Impostare il valore dell'intestazione della richiesta `Content-Type` su `application/json`.</span><span class="sxs-lookup"><span data-stu-id="a4aee-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="a4aee-156">Il backup è un'operazione a lunga esecuzione che potrebbe richiedere diversi minuti per essere completata.</span><span class="sxs-lookup"><span data-stu-id="a4aee-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="a4aee-157">Se la richiesta viene eseguita correttamente e il processo di backup viene avviato, si riceverà un codice di stato risposta `202 Accepted` con un'intestazione `Location`.</span><span class="sxs-lookup"><span data-stu-id="a4aee-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="a4aee-158">Effettuare richieste "GET" all'URL nell'intestazione `Location` per conoscere lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="a4aee-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="a4aee-159">Durante l'esecuzione del backup si continuerà a ricevere il codice di stato "202 - Accettato".</span><span class="sxs-lookup"><span data-stu-id="a4aee-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="a4aee-160">Il codice risposta `200 OK` indicherà il completamento dell'operazione di backup.</span><span class="sxs-lookup"><span data-stu-id="a4aee-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="a4aee-161">Quando si crea una richiesta di backup, occorre notare i vincoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="a4aee-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="a4aee-162">Il **contenitore** specificato nel corpo della richiesta **deve esistere**.</span><span class="sxs-lookup"><span data-stu-id="a4aee-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="a4aee-163">Mentre il backup è in corso, **non tentare di eseguire alcuna operazione di gestione dei servizi** , ad esempio l'aggiornamento o il downgrade di SKU, la modifica di nomi di dominio e così via.</span><span class="sxs-lookup"><span data-stu-id="a4aee-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="a4aee-164">Il ripristino di un **backup è garantito solo per 30 giorni** dal momento della sua creazione.</span><span class="sxs-lookup"><span data-stu-id="a4aee-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="a4aee-165">I **dati di utilizzo** usati per creare report analitici **non sono inclusi** nel backup.</span><span class="sxs-lookup"><span data-stu-id="a4aee-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="a4aee-166">Usare l'[API REST di Gestione API di Azure][Azure API Management REST API] per recuperare periodicamente i report analitici e custodirli al sicuro.</span><span class="sxs-lookup"><span data-stu-id="a4aee-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="a4aee-167">La frequenza con cui si eseguono i backup dei servizi influenzerà i propri obiettivi relativi ai punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="a4aee-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="a4aee-168">Per ridurla al minimo, si consiglia di implementare backup regolari e di eseguire backup su richiesta dopo aver apportato modifiche importanti al servizio di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a4aee-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="a4aee-169">Le **modifiche** apportate alla configurazione del servizio (ad esempio alle API, ai criteri, all'aspetto del portale per sviluppatori) durante l'esecuzione del processo di backup **potrebbero non essere incluse nel backup e potrebbero quindi andare perse**.</span><span class="sxs-lookup"><span data-stu-id="a4aee-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="a4aee-170"><a name="step2"> </a>Ripristino di un servizio di Gestione API</span><span class="sxs-lookup"><span data-stu-id="a4aee-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="a4aee-171">Per ripristinare un servizio di Gestione API da un backup creato in precedenza, creare la seguente richiesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="a4aee-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="a4aee-172">dove:</span><span class="sxs-lookup"><span data-stu-id="a4aee-172">where:</span></span>

* <span data-ttu-id="a4aee-173">`subscriptionId` : ID della sottoscrizione contenente il servizio di Gestione API in cui si sta ripristinando un backup.</span><span class="sxs-lookup"><span data-stu-id="a4aee-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="a4aee-174">`resourceGroupName`: una stringa nel formato "Api-Default-{service-region}", dove `service-region` identifica l'area di Azure in cui è ospitato il servizio di Gestione API in cui si ripristinando un backup, ad esempio `North-Central-US`.</span><span class="sxs-lookup"><span data-stu-id="a4aee-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="a4aee-175">`serviceName` : il nome del servizio di Gestione API in cui si sta effettuando il ripristino specificato quando è stato creato.</span><span class="sxs-lookup"><span data-stu-id="a4aee-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="a4aee-176">`api-version` - sostituire con `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="a4aee-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="a4aee-177">Nel corpo della richiesta, specificare la posizione del file di backup, ad esempio il nome dell'account di archiviazione, la chiave di accesso, il nome del contenitore BLOB e il nome del backup di Azure:</span><span class="sxs-lookup"><span data-stu-id="a4aee-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="a4aee-178">Impostare il valore dell'intestazione della richiesta `Content-Type` su `application/json`.</span><span class="sxs-lookup"><span data-stu-id="a4aee-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="a4aee-179">Il ripristino è un'operazione a lunga esecuzione che potrebbe richiedere 30 minuti o più per essere completata.</span><span class="sxs-lookup"><span data-stu-id="a4aee-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="a4aee-180">Se la richiesta viene eseguita correttamente e il processo di ripristino viene avviato, si riceverà un codice di stato risposta `202 Accepted` con un'intestazione `Location`.</span><span class="sxs-lookup"><span data-stu-id="a4aee-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="a4aee-181">Effettuare richieste "GET" all'URL nell'intestazione `Location` per conoscere lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="a4aee-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="a4aee-182">Durante l'esecuzione del ripristino si continuerà a ricevere il codice di stato "202 - Accettato".</span><span class="sxs-lookup"><span data-stu-id="a4aee-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="a4aee-183">Il codice risposta `200 OK` indicherà il completamento dell'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="a4aee-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4aee-184">Lo **SKU** del servizio in cui si effettua il ripristino **deve corrispondere** allo SKU del servizio sottoposto a backup da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="a4aee-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="a4aee-185">Le **modifiche** apportate alla configurazione del servizio (ad esempio alle API, ai criteri, all'aspetto del portale per sviluppatori) durante l'operazione di ripristino **potrebbero essere sovrascritte**.</span><span class="sxs-lookup"><span data-stu-id="a4aee-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a4aee-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4aee-186">Next steps</span></span>
<span data-ttu-id="a4aee-187">Consultare i blog Microsoft seguenti per due diverse procedure dettagliate del processo di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="a4aee-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="a4aee-188">Replicare account di Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a4aee-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="a4aee-189">Grazie a Gisela per il contributo fornito per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a4aee-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="a4aee-190">Gestione API di Azure: Backup e ripristino della configurazione</span><span class="sxs-lookup"><span data-stu-id="a4aee-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="a4aee-191">L'approccio descritto da Stuart corrisponde alle linee guida ufficiali, ma è molto interessante.</span><span class="sxs-lookup"><span data-stu-id="a4aee-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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

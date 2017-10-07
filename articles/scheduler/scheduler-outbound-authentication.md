---
title: aaaScheduler autenticazione in uscita
description: "Autenticazione in uscita dell'Utilità di pianificazione"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="1fabf-103">Autenticazione in uscita dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="1fabf-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="1fabf-104">I processi dell'utilità di pianificazione potrebbe essere necessario toocall out tooservices che richiedono l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="1fabf-105">In questo modo, un servizio chiamato può determinare se il processo di pianificazione hello può accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="1fabf-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="1fabf-106">Alcuni di questi servizi includono altri servizi di Azure, Salesforce.com, Facebook e siti Web custom protetti.</span><span class="sxs-lookup"><span data-stu-id="1fabf-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="1fabf-107">Aggiunta e rimozione di autenticazione</span><span class="sxs-lookup"><span data-stu-id="1fabf-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="1fabf-108">Aggiunta di autenticazione tooa dell'utilità di pianificazione è semplice: aggiungere un elemento figlio JSON `authentication` toohello `request` elemento durante la creazione o l'aggiornamento del processo.</span><span class="sxs-lookup"><span data-stu-id="1fabf-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="1fabf-109">I segreti passati servizio Utilità di pianificazione toohello in una richiesta PUT, PATCH o POST-come parte di hello `authentication` oggetto: non vengono mai restituiti nelle risposte.</span><span class="sxs-lookup"><span data-stu-id="1fabf-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="1fabf-110">Nelle risposte, le informazioni segrete sono impostate toonull o potrebbero essere un token pubblico che rappresenta l'entità hello autenticato.</span><span class="sxs-lookup"><span data-stu-id="1fabf-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="1fabf-111">autenticazione tooremove, PUT o PATCH in modo esplicito, il processo di hello impostazione hello `authentication` toonull dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="1fabf-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="1fabf-112">Nessuna proprietà di autenticazione verrà visualizzata nella risposta.</span><span class="sxs-lookup"><span data-stu-id="1fabf-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="1fabf-113">Hello supportato solo tipi di autenticazione sono attualmente hello `ClientCertificate` modello (per l'utilizzo di certificati client SSL/TLS di hello), hello `Basic` del modello (per l'autenticazione di base) e hello `ActiveDirectoryOAuth` modello (per OAuth di Active Directory autenticazione).</span><span class="sxs-lookup"><span data-stu-id="1fabf-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="1fabf-114">Corpo della richiesta per l'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1fabf-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="1fabf-115">Quando si aggiunge l'autenticazione utilizzando hello `ClientCertificate` del modello, specificare i seguenti elementi aggiuntivi nel corpo della richiesta hello hello.</span><span class="sxs-lookup"><span data-stu-id="1fabf-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="1fabf-116">Elemento</span><span class="sxs-lookup"><span data-stu-id="1fabf-116">Element</span></span> | <span data-ttu-id="1fabf-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1fabf-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1fabf-118">*authentication (elemento padre)*</span><span class="sxs-lookup"><span data-stu-id="1fabf-118">*authentication (parent element)*</span></span> |<span data-ttu-id="1fabf-119">Oggetto di autenticazione per l'utilizzo di un certificato client SSL.</span><span class="sxs-lookup"><span data-stu-id="1fabf-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="1fabf-120">*type*</span><span class="sxs-lookup"><span data-stu-id="1fabf-120">*type*</span></span> |<span data-ttu-id="1fabf-121">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-121">Required.</span></span> <span data-ttu-id="1fabf-122">Tipo di autenticazione. Per i certificati client SSL, deve essere il valore di hello `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1fabf-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="1fabf-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="1fabf-123">*pfx*</span></span> |<span data-ttu-id="1fabf-124">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-124">Required.</span></span> <span data-ttu-id="1fabf-125">Contenuto con codifica Base64 del file PFX hello.</span><span class="sxs-lookup"><span data-stu-id="1fabf-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="1fabf-126">*password*</span><span class="sxs-lookup"><span data-stu-id="1fabf-126">*password*</span></span> |<span data-ttu-id="1fabf-127">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-127">Required.</span></span> <span data-ttu-id="1fabf-128">File PFX hello tooaccess delle password.</span><span class="sxs-lookup"><span data-stu-id="1fabf-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="1fabf-129">Corpo della risposta per l'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1fabf-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="1fabf-130">Quando viene inviata una richiesta con informazioni di autenticazione, risposta hello contiene hello segue gli elementi correlati all'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1fabf-131">Elemento</span><span class="sxs-lookup"><span data-stu-id="1fabf-131">Element</span></span> | <span data-ttu-id="1fabf-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1fabf-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1fabf-133">*authentication (elemento padre)*</span><span class="sxs-lookup"><span data-stu-id="1fabf-133">*authentication (parent element)*</span></span> |<span data-ttu-id="1fabf-134">Oggetto di autenticazione per l'utilizzo di un certificato client SSL.</span><span class="sxs-lookup"><span data-stu-id="1fabf-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="1fabf-135">*type*</span><span class="sxs-lookup"><span data-stu-id="1fabf-135">*type*</span></span> |<span data-ttu-id="1fabf-136">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-136">Type of authentication.</span></span> <span data-ttu-id="1fabf-137">Per i certificati client SSL, il valore di hello è `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1fabf-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="1fabf-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="1fabf-138">*certificateThumbprint*</span></span> |<span data-ttu-id="1fabf-139">identificazione personale Hello del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="1fabf-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="1fabf-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="1fabf-140">*certificateSubjectName*</span></span> |<span data-ttu-id="1fabf-141">Hello nome distinto del soggetto del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="1fabf-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="1fabf-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="1fabf-142">*certificateExpiration*</span></span> |<span data-ttu-id="1fabf-143">Data di scadenza Hello del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="1fabf-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="1fabf-144">Richiesta REST di esempio per l'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1fabf-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="1fabf-145">Risposta REST di esempio per l'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1fabf-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="1fabf-146">Corpo della richiesta per l'autenticazione di Base</span><span class="sxs-lookup"><span data-stu-id="1fabf-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="1fabf-147">Quando si aggiunge l'autenticazione utilizzando hello `Basic` del modello, specificare i seguenti elementi aggiuntivi nel corpo della richiesta hello hello.</span><span class="sxs-lookup"><span data-stu-id="1fabf-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="1fabf-148">Elemento</span><span class="sxs-lookup"><span data-stu-id="1fabf-148">Element</span></span> | <span data-ttu-id="1fabf-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1fabf-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1fabf-150">*authentication (elemento padre)*</span><span class="sxs-lookup"><span data-stu-id="1fabf-150">*authentication (parent element)*</span></span> |<span data-ttu-id="1fabf-151">Oggetto di autenticazione per l’utilizzo dell'autenticazione di Base.</span><span class="sxs-lookup"><span data-stu-id="1fabf-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="1fabf-152">*type*</span><span class="sxs-lookup"><span data-stu-id="1fabf-152">*type*</span></span> |<span data-ttu-id="1fabf-153">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-153">Required.</span></span> <span data-ttu-id="1fabf-154">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-154">Type of authentication.</span></span> <span data-ttu-id="1fabf-155">L'autenticazione di base, deve essere il valore di hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1fabf-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="1fabf-156">*username*</span><span class="sxs-lookup"><span data-stu-id="1fabf-156">*username*</span></span> |<span data-ttu-id="1fabf-157">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-157">Required.</span></span> <span data-ttu-id="1fabf-158">Nome utente tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="1fabf-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="1fabf-159">*password*</span><span class="sxs-lookup"><span data-stu-id="1fabf-159">*password*</span></span> |<span data-ttu-id="1fabf-160">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-160">Required.</span></span> <span data-ttu-id="1fabf-161">Tooauthenticate password.</span><span class="sxs-lookup"><span data-stu-id="1fabf-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="1fabf-162">Corpo della risposta per l'autenticazione di Base</span><span class="sxs-lookup"><span data-stu-id="1fabf-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="1fabf-163">Quando viene inviata una richiesta con informazioni di autenticazione, risposta hello contiene hello segue gli elementi correlati all'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1fabf-164">Elemento</span><span class="sxs-lookup"><span data-stu-id="1fabf-164">Element</span></span> | <span data-ttu-id="1fabf-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1fabf-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1fabf-166">*authentication (elemento padre)*</span><span class="sxs-lookup"><span data-stu-id="1fabf-166">*authentication (parent element)*</span></span> |<span data-ttu-id="1fabf-167">Oggetto di autenticazione per l’utilizzo dell'autenticazione di Base.</span><span class="sxs-lookup"><span data-stu-id="1fabf-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="1fabf-168">*type*</span><span class="sxs-lookup"><span data-stu-id="1fabf-168">*type*</span></span> |<span data-ttu-id="1fabf-169">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-169">Type of authentication.</span></span> <span data-ttu-id="1fabf-170">L'autenticazione di base, il valore di hello è `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1fabf-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="1fabf-171">*username*</span><span class="sxs-lookup"><span data-stu-id="1fabf-171">*username*</span></span> |<span data-ttu-id="1fabf-172">Hello autenticazione nome utente.</span><span class="sxs-lookup"><span data-stu-id="1fabf-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="1fabf-173">Richiesta REST di esempio per l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="1fabf-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="1fabf-174">Risposta REST di esempio per l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="1fabf-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1fabf-175">Corpo della richiesta per l'autenticazione ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1fabf-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="1fabf-176">Quando si aggiunge l'autenticazione utilizzando hello `ActiveDirectoryOAuth` del modello, specificare i seguenti elementi aggiuntivi nel corpo della richiesta hello hello.</span><span class="sxs-lookup"><span data-stu-id="1fabf-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="1fabf-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="1fabf-177">Element</span></span> | <span data-ttu-id="1fabf-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1fabf-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1fabf-179">*authentication (elemento padre)*</span><span class="sxs-lookup"><span data-stu-id="1fabf-179">*authentication (parent element)*</span></span> |<span data-ttu-id="1fabf-180">Oggetto di autenticazione per l'autenticazione basata su ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="1fabf-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="1fabf-181">*type*</span><span class="sxs-lookup"><span data-stu-id="1fabf-181">*type*</span></span> |<span data-ttu-id="1fabf-182">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-182">Required.</span></span> <span data-ttu-id="1fabf-183">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-183">Type of authentication.</span></span> <span data-ttu-id="1fabf-184">Per l'autenticazione ActiveDirectoryOAuth, il valore di hello deve essere `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="1fabf-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="1fabf-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="1fabf-185">*tenant*</span></span> |<span data-ttu-id="1fabf-186">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-186">Required.</span></span> <span data-ttu-id="1fabf-187">Identificatore del tenant Hello per tenant hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fabf-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="1fabf-188">*audience*</span><span class="sxs-lookup"><span data-stu-id="1fabf-188">*audience*</span></span> |<span data-ttu-id="1fabf-189">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-189">Required.</span></span> <span data-ttu-id="1fabf-190">Toohttps://management.core.windows.net/ è impostato.</span><span class="sxs-lookup"><span data-stu-id="1fabf-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="1fabf-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="1fabf-191">*clientId*</span></span> |<span data-ttu-id="1fabf-192">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-192">Required.</span></span> <span data-ttu-id="1fabf-193">Fornire l'identificatore hello del client per hello applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fabf-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="1fabf-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="1fabf-194">*secret*</span></span> |<span data-ttu-id="1fabf-195">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1fabf-195">Required.</span></span> <span data-ttu-id="1fabf-196">Segreto del client hello che sta richiedendo hello token.</span><span class="sxs-lookup"><span data-stu-id="1fabf-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="1fabf-197">Determinazione del l'identificatore del tenant</span><span class="sxs-lookup"><span data-stu-id="1fabf-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="1fabf-198">È possibile trovare l'identificatore del tenant per il tenant di Azure AD hello hello eseguendo `Get-AzureAccount` in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fabf-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1fabf-199">Corpo della risposta per l'autenticazione ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1fabf-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="1fabf-200">Quando viene inviata una richiesta con informazioni di autenticazione, risposta hello contiene hello segue gli elementi correlati all'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1fabf-201">Elemento</span><span class="sxs-lookup"><span data-stu-id="1fabf-201">Element</span></span> | <span data-ttu-id="1fabf-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1fabf-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1fabf-203">*authentication (elemento padre)*</span><span class="sxs-lookup"><span data-stu-id="1fabf-203">*authentication (parent element)*</span></span> |<span data-ttu-id="1fabf-204">Oggetto di autenticazione per l'autenticazione basata su ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="1fabf-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="1fabf-205">*type*</span><span class="sxs-lookup"><span data-stu-id="1fabf-205">*type*</span></span> |<span data-ttu-id="1fabf-206">Tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1fabf-206">Type of authentication.</span></span> <span data-ttu-id="1fabf-207">Per l'autenticazione ActiveDirectoryOAuth, il valore di hello è `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="1fabf-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="1fabf-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="1fabf-208">*tenant*</span></span> |<span data-ttu-id="1fabf-209">Identificatore del tenant Hello per tenant hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fabf-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="1fabf-210">*audience*</span><span class="sxs-lookup"><span data-stu-id="1fabf-210">*audience*</span></span> |<span data-ttu-id="1fabf-211">Toohttps://management.core.windows.net/ è impostato.</span><span class="sxs-lookup"><span data-stu-id="1fabf-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="1fabf-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="1fabf-212">*clientId*</span></span> |<span data-ttu-id="1fabf-213">Hello identificatore client per un'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fabf-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1fabf-214">Richiesta REST di esempio per l'autenticazione ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1fabf-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1fabf-215">Risposta REST di esempio per l'autenticazione ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1fabf-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="1fabf-216">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1fabf-216">See Also</span></span>
 [<span data-ttu-id="1fabf-217">Che cos'è l'Utilità di pianificazione?</span><span class="sxs-lookup"><span data-stu-id="1fabf-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="1fabf-218">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1fabf-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="1fabf-219">Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="1fabf-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="1fabf-220">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1fabf-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="1fabf-221">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1fabf-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="1fabf-222">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1fabf-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="1fabf-223">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1fabf-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="1fabf-224">Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1fabf-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)


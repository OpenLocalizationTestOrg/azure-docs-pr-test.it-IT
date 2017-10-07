---
title: criteri di autenticazione di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui criteri di autenticazione hello disponibili per l'utilizzo in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="1d219-103">Criteri di autenticazione di Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="1d219-103">API Management authentication policies</span></span>
<span data-ttu-id="1d219-104">In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="1d219-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="1d219-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="1d219-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="1d219-106"><a name="AuthenticationPolicies"></a> Criteri di autenticazione</span><span class="sxs-lookup"><span data-stu-id="1d219-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="1d219-107">[Autenticazione con base](api-management-authentication-policies.md#Basic): consente di eseguire l'autenticazione con un servizio back-end tramite l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="1d219-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="1d219-108">[Autenticazione con certificato](api-management-authentication-policies.md#ClientCertificate): consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.</span><span class="sxs-lookup"><span data-stu-id="1d219-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="1d219-109"><a name="Basic"></a> Autenticazione con base</span><span class="sxs-lookup"><span data-stu-id="1d219-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="1d219-110">Hello utilizzare `authentication-basic` tooauthenticate criteri con un servizio back-end mediante autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="1d219-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="1d219-111">Questo criterio imposta toohello intestazione autorizzazione HTTP di hello credenziali toohello corrispondente valore fornite nei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="1d219-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1d219-112">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="1d219-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="1d219-113">Esempio</span><span class="sxs-lookup"><span data-stu-id="1d219-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="1d219-114">Elementi</span><span class="sxs-lookup"><span data-stu-id="1d219-114">Elements</span></span>  
  
|<span data-ttu-id="1d219-115">Nome</span><span class="sxs-lookup"><span data-stu-id="1d219-115">Name</span></span>|<span data-ttu-id="1d219-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d219-116">Description</span></span>|<span data-ttu-id="1d219-117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1d219-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="1d219-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="1d219-118">authentication-basic</span></span>|<span data-ttu-id="1d219-119">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="1d219-119">Root element.</span></span>|<span data-ttu-id="1d219-120">Sì</span><span class="sxs-lookup"><span data-stu-id="1d219-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1d219-121">Attributi</span><span class="sxs-lookup"><span data-stu-id="1d219-121">Attributes</span></span>  
  
|<span data-ttu-id="1d219-122">Nome</span><span class="sxs-lookup"><span data-stu-id="1d219-122">Name</span></span>|<span data-ttu-id="1d219-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d219-123">Description</span></span>|<span data-ttu-id="1d219-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1d219-124">Required</span></span>|<span data-ttu-id="1d219-125">Default</span><span class="sxs-lookup"><span data-stu-id="1d219-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="1d219-126">username</span><span class="sxs-lookup"><span data-stu-id="1d219-126">username</span></span>|<span data-ttu-id="1d219-127">Specifica nome utente hello della credenziale di base hello.</span><span class="sxs-lookup"><span data-stu-id="1d219-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="1d219-128">Sì</span><span class="sxs-lookup"><span data-stu-id="1d219-128">Yes</span></span>|<span data-ttu-id="1d219-129">N/D</span><span class="sxs-lookup"><span data-stu-id="1d219-129">N/A</span></span>|  
|<span data-ttu-id="1d219-130">password</span><span class="sxs-lookup"><span data-stu-id="1d219-130">password</span></span>|<span data-ttu-id="1d219-131">Specifica la password di hello della credenziale di base hello.</span><span class="sxs-lookup"><span data-stu-id="1d219-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="1d219-132">Sì</span><span class="sxs-lookup"><span data-stu-id="1d219-132">Yes</span></span>|<span data-ttu-id="1d219-133">N/D</span><span class="sxs-lookup"><span data-stu-id="1d219-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1d219-134">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="1d219-134">Usage</span></span>  
 <span data-ttu-id="1d219-135">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1d219-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1d219-136">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="1d219-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="1d219-137">**Ambiti del criterio:** API</span><span class="sxs-lookup"><span data-stu-id="1d219-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="1d219-138"><a name="ClientCertificate"></a> Autenticazione con certificato client</span><span class="sxs-lookup"><span data-stu-id="1d219-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="1d219-139">Hello utilizzare `authentication-certificate` tooauthenticate criteri con un servizio back-end tramite certificato client.</span><span class="sxs-lookup"><span data-stu-id="1d219-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="1d219-140">certificato di Hello deve toobe [installato in Gestione API](http://go.microsoft.com/fwlink/?LinkID=511599) primo ed è identificato dalla relativa identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="1d219-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1d219-141">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="1d219-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="1d219-142">Esempio</span><span class="sxs-lookup"><span data-stu-id="1d219-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="1d219-143">Elementi</span><span class="sxs-lookup"><span data-stu-id="1d219-143">Elements</span></span>  
  
|<span data-ttu-id="1d219-144">Nome</span><span class="sxs-lookup"><span data-stu-id="1d219-144">Name</span></span>|<span data-ttu-id="1d219-145">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d219-145">Description</span></span>|<span data-ttu-id="1d219-146">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1d219-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="1d219-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="1d219-147">authentication-certificate</span></span>|<span data-ttu-id="1d219-148">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="1d219-148">Root element.</span></span>|<span data-ttu-id="1d219-149">Sì</span><span class="sxs-lookup"><span data-stu-id="1d219-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1d219-150">Attributi</span><span class="sxs-lookup"><span data-stu-id="1d219-150">Attributes</span></span>  
  
|<span data-ttu-id="1d219-151">Nome</span><span class="sxs-lookup"><span data-stu-id="1d219-151">Name</span></span>|<span data-ttu-id="1d219-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1d219-152">Description</span></span>|<span data-ttu-id="1d219-153">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1d219-153">Required</span></span>|<span data-ttu-id="1d219-154">Default</span><span class="sxs-lookup"><span data-stu-id="1d219-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="1d219-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="1d219-155">thumbprint</span></span>|<span data-ttu-id="1d219-156">Hello identificazione personale del certificato client hello.</span><span class="sxs-lookup"><span data-stu-id="1d219-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="1d219-157">Sì</span><span class="sxs-lookup"><span data-stu-id="1d219-157">Yes</span></span>|<span data-ttu-id="1d219-158">N/D</span><span class="sxs-lookup"><span data-stu-id="1d219-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1d219-159">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="1d219-159">Usage</span></span>  
 <span data-ttu-id="1d219-160">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1d219-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1d219-161">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="1d219-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="1d219-162">**Ambiti del criterio:** API</span><span class="sxs-lookup"><span data-stu-id="1d219-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="1d219-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d219-163">Next steps</span></span>
<span data-ttu-id="1d219-164">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1d219-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
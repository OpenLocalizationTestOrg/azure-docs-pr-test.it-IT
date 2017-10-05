---
title: Criteri di autenticazione di Gestione API di Azure | Documentazione Microsoft
description: Informazioni sui criteri di autenticazione disponibili per l'uso in Gestione API di Azure.
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
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="ccb52-103">Criteri di autenticazione di Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="ccb52-103">API Management authentication policies</span></span>
<span data-ttu-id="ccb52-104">Questo argomento fornisce un riferimento per i seguenti criteri di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="ccb52-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="ccb52-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="ccb52-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="ccb52-106"><a name="AuthenticationPolicies"></a> Criteri di autenticazione</span><span class="sxs-lookup"><span data-stu-id="ccb52-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="ccb52-107">[Autenticazione con base](api-management-authentication-policies.md#Basic): consente di eseguire l'autenticazione con un servizio back-end tramite l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="ccb52-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="ccb52-108">[Autenticazione con certificato](api-management-authentication-policies.md#ClientCertificate): consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.</span><span class="sxs-lookup"><span data-stu-id="ccb52-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="ccb52-109"><a name="Basic"></a> Autenticazione con base</span><span class="sxs-lookup"><span data-stu-id="ccb52-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="ccb52-110">Usare il criterio `authentication-basic` per eseguire l'autenticazione con un servizio di back-end tramite l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="ccb52-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="ccb52-111">Questo criterio imposta l'intestazione di autorizzazione HTTP sul valore corrispondente alle credenziali specificate nei criteri.</span><span class="sxs-lookup"><span data-stu-id="ccb52-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ccb52-112">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="ccb52-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="ccb52-113">Esempio</span><span class="sxs-lookup"><span data-stu-id="ccb52-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="ccb52-114">Elementi</span><span class="sxs-lookup"><span data-stu-id="ccb52-114">Elements</span></span>  
  
|<span data-ttu-id="ccb52-115">Nome</span><span class="sxs-lookup"><span data-stu-id="ccb52-115">Name</span></span>|<span data-ttu-id="ccb52-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ccb52-116">Description</span></span>|<span data-ttu-id="ccb52-117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ccb52-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ccb52-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="ccb52-118">authentication-basic</span></span>|<span data-ttu-id="ccb52-119">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="ccb52-119">Root element.</span></span>|<span data-ttu-id="ccb52-120">Sì</span><span class="sxs-lookup"><span data-stu-id="ccb52-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ccb52-121">Attributi</span><span class="sxs-lookup"><span data-stu-id="ccb52-121">Attributes</span></span>  
  
|<span data-ttu-id="ccb52-122">Nome</span><span class="sxs-lookup"><span data-stu-id="ccb52-122">Name</span></span>|<span data-ttu-id="ccb52-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ccb52-123">Description</span></span>|<span data-ttu-id="ccb52-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ccb52-124">Required</span></span>|<span data-ttu-id="ccb52-125">Default</span><span class="sxs-lookup"><span data-stu-id="ccb52-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ccb52-126">username</span><span class="sxs-lookup"><span data-stu-id="ccb52-126">username</span></span>|<span data-ttu-id="ccb52-127">Specifica il nome utente della credenziale di base.</span><span class="sxs-lookup"><span data-stu-id="ccb52-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="ccb52-128">Sì</span><span class="sxs-lookup"><span data-stu-id="ccb52-128">Yes</span></span>|<span data-ttu-id="ccb52-129">N/D</span><span class="sxs-lookup"><span data-stu-id="ccb52-129">N/A</span></span>|  
|<span data-ttu-id="ccb52-130">password</span><span class="sxs-lookup"><span data-stu-id="ccb52-130">password</span></span>|<span data-ttu-id="ccb52-131">Specifica la password della credenziale di base.</span><span class="sxs-lookup"><span data-stu-id="ccb52-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="ccb52-132">Sì</span><span class="sxs-lookup"><span data-stu-id="ccb52-132">Yes</span></span>|<span data-ttu-id="ccb52-133">N/D</span><span class="sxs-lookup"><span data-stu-id="ccb52-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ccb52-134">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="ccb52-134">Usage</span></span>  
 <span data-ttu-id="ccb52-135">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="ccb52-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ccb52-136">**Sezioni del criterio:** in ingresso</span><span class="sxs-lookup"><span data-stu-id="ccb52-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ccb52-137">**Ambiti del criterio:** API</span><span class="sxs-lookup"><span data-stu-id="ccb52-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="ccb52-138"><a name="ClientCertificate"></a> Autenticazione con certificato client</span><span class="sxs-lookup"><span data-stu-id="ccb52-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="ccb52-139">Usare il criterio `authentication-certificate` per eseguire l'autenticazione con un servizio di back-end tramite il certificato client.</span><span class="sxs-lookup"><span data-stu-id="ccb52-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="ccb52-140">Il certificato deve essere prima [installato in Gestione API](http://go.microsoft.com/fwlink/?LinkID=511599) e viene identificato tramite la relativa identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="ccb52-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ccb52-141">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="ccb52-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="ccb52-142">Esempio</span><span class="sxs-lookup"><span data-stu-id="ccb52-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="ccb52-143">Elementi</span><span class="sxs-lookup"><span data-stu-id="ccb52-143">Elements</span></span>  
  
|<span data-ttu-id="ccb52-144">Nome</span><span class="sxs-lookup"><span data-stu-id="ccb52-144">Name</span></span>|<span data-ttu-id="ccb52-145">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ccb52-145">Description</span></span>|<span data-ttu-id="ccb52-146">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ccb52-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ccb52-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="ccb52-147">authentication-certificate</span></span>|<span data-ttu-id="ccb52-148">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="ccb52-148">Root element.</span></span>|<span data-ttu-id="ccb52-149">Sì</span><span class="sxs-lookup"><span data-stu-id="ccb52-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ccb52-150">Attributi</span><span class="sxs-lookup"><span data-stu-id="ccb52-150">Attributes</span></span>  
  
|<span data-ttu-id="ccb52-151">Nome</span><span class="sxs-lookup"><span data-stu-id="ccb52-151">Name</span></span>|<span data-ttu-id="ccb52-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ccb52-152">Description</span></span>|<span data-ttu-id="ccb52-153">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ccb52-153">Required</span></span>|<span data-ttu-id="ccb52-154">Default</span><span class="sxs-lookup"><span data-stu-id="ccb52-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ccb52-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="ccb52-155">thumbprint</span></span>|<span data-ttu-id="ccb52-156">Identificazione personale del certificato client.</span><span class="sxs-lookup"><span data-stu-id="ccb52-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="ccb52-157">Sì</span><span class="sxs-lookup"><span data-stu-id="ccb52-157">Yes</span></span>|<span data-ttu-id="ccb52-158">N/D</span><span class="sxs-lookup"><span data-stu-id="ccb52-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ccb52-159">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="ccb52-159">Usage</span></span>  
 <span data-ttu-id="ccb52-160">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="ccb52-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ccb52-161">**Sezioni del criterio:** in ingresso</span><span class="sxs-lookup"><span data-stu-id="ccb52-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ccb52-162">**Ambiti del criterio:** API</span><span class="sxs-lookup"><span data-stu-id="ccb52-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="ccb52-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ccb52-163">Next steps</span></span>
<span data-ttu-id="ccb52-164">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ccb52-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
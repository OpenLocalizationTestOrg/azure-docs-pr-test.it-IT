---
title: 'Elenco di errori e soluzioni per le app per la logica B2B: servizio App di Azure | Microsoft Docs'
description: Elenco di errori e soluzioni per le app per la logica B2B
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="a261f-103">Elenco di errori e soluzioni per le app per la logica B2B</span><span class="sxs-lookup"><span data-stu-id="a261f-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="a261f-104">Questo articolo consente di risolvere gli errori che si possono verificare negli scenari con le app per la logica B2B e suggerisce le azioni appropriate per la correzione degli errori.</span><span class="sxs-lookup"><span data-stu-id="a261f-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="a261f-105">Risoluzione dell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="a261f-106">* Non sono stati trovati accordi</span><span class="sxs-lookup"><span data-stu-id="a261f-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="a261f-107">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-107">Error description</span></span> | <span data-ttu-id="a261f-108">Non sono stati trovati accordi con parametri di risoluzione del contratto</span><span class="sxs-lookup"><span data-stu-id="a261f-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="a261f-109">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-109">User action</span></span> | <span data-ttu-id="a261f-110">L'accordo deve essere aggiunto all'account di integrazione con le identità di business concordate.</span><span class="sxs-lookup"><span data-stu-id="a261f-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="a261f-111">Le identità di business devono corrispondere agli ID dei messaggi di input</span><span class="sxs-lookup"><span data-stu-id="a261f-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="a261f-112">* Non sono stati trovati accordi con le identità</span><span class="sxs-lookup"><span data-stu-id="a261f-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a261f-113">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-113">Error description</span></span> | <span data-ttu-id="a261f-114">Non sono stati trovati accordi con le identità: 'AS2Identity'::'Partner1' e 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="a261f-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="a261f-115">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-115">User action</span></span> | <span data-ttu-id="a261f-116">Configurata un'intestazione AS2-From o AS2-To non valida per l'accordo.</span><span class="sxs-lookup"><span data-stu-id="a261f-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="a261f-117">Correggere l'intestazione AS2-From o AS2-To del messaggio AS2 o l'accordo in modo da assicurare la corrispondenza degli ID AS2 presenti nelle intestazioni del messaggio AS2 con le configurazioni dell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="a261f-118">AS2</span><span class="sxs-lookup"><span data-stu-id="a261f-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="a261f-119">* Intestazioni del messaggio AS2 mancanti</span><span class="sxs-lookup"><span data-stu-id="a261f-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="a261f-120">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-120">Error description</span></span>| <span data-ttu-id="a261f-121">Intestazioni AS2 non valide.</span><span class="sxs-lookup"><span data-stu-id="a261f-121">Invalid AS2 headers.</span></span> <span data-ttu-id="a261f-122">Una delle intestazioni "AS2-To" o "AS2-From" è vuota</span><span class="sxs-lookup"><span data-stu-id="a261f-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="a261f-123">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-123">User action</span></span> | <span data-ttu-id="a261f-124">Ricevuto un messaggio AS2 che non contiene l'intestazione AS2-From o AS2-To o entrambe le intestazioni.</span><span class="sxs-lookup"><span data-stu-id="a261f-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="a261f-125">Controllare le intestazioni AS2-From e AS2-To del messaggio AS2 e correggerle in base alla configurazione dell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="a261f-126">* Corpo e intestazioni del messaggio AS2 mancanti</span><span class="sxs-lookup"><span data-stu-id="a261f-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="a261f-127">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-127">Error description</span></span>| <span data-ttu-id="a261f-128">Il contenuto della richiesta è null o vuoto</span><span class="sxs-lookup"><span data-stu-id="a261f-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="a261f-129">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-129">User action</span></span> | <span data-ttu-id="a261f-130">Ricevuto un messaggio AS2 che non contiene il corpo del messaggio</span><span class="sxs-lookup"><span data-stu-id="a261f-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="a261f-131">* Errore di decrittografia del messaggio AS2</span><span class="sxs-lookup"><span data-stu-id="a261f-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a261f-132">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-132">Error description</span></span> |  <span data-ttu-id="a261f-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="a261f-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="a261f-134">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-134">User action</span></span> | <span data-ttu-id="a261f-135">Aggiungere @base64ToBinary a AS2Message prima dell'invio al partner</span><span class="sxs-lookup"><span data-stu-id="a261f-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="a261f-136">* Errore di decrittografia della notifica sulla ricezione del messaggio</span><span class="sxs-lookup"><span data-stu-id="a261f-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a261f-137">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-137">Error description</span></span> |  <span data-ttu-id="a261f-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="a261f-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="a261f-139">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-139">User action</span></span> | <span data-ttu-id="a261f-140">Aggiungere @base64ToBinary alla notifica sulla ricezione del messaggio prima dell'invio al partner</span><span class="sxs-lookup"><span data-stu-id="a261f-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="a261f-141">* Certificato di firma mancante</span><span class="sxs-lookup"><span data-stu-id="a261f-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="a261f-142">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-142">Error description</span></span>| <span data-ttu-id="a261f-143">Certificato di firma non configurato per l'entità AS2.</span><span class="sxs-lookup"><span data-stu-id="a261f-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="a261f-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="a261f-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="a261f-145">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-145">User action</span></span> | <span data-ttu-id="a261f-146">Configurare le impostazioni dell'accordo AS2 con il certificato corretto per la firma</span><span class="sxs-lookup"><span data-stu-id="a261f-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="a261f-147">X12 ed EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a261f-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="a261f-148">* Trovato spazio iniziale o finale</span><span class="sxs-lookup"><span data-stu-id="a261f-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="a261f-149">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-149">Error description</span></span> | <span data-ttu-id="a261f-150">Errore rilevato durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="a261f-150">Error encountered during parsing.</span></span> <span data-ttu-id="a261f-151">Il set di transazioni Edifact con ID "123456" contenuto nell'interscambio (senza gruppo) con ID "987654", ID mittente "Partner1", ID ricevitore "Partner2" viene sospeso con i seguenti errori: trovato separatore iniziale o finale</span><span class="sxs-lookup"><span data-stu-id="a261f-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="a261f-152">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-152">User action</span></span> | <span data-ttu-id="a261f-153">Configurare le impostazioni dell'accordo in modo da consentire lo spazio iniziale e finale.</span><span class="sxs-lookup"><span data-stu-id="a261f-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="a261f-154">Modificare le impostazioni dell'accordo in modo che consentano lo spazio iniziale e finale</span><span class="sxs-lookup"><span data-stu-id="a261f-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![consentire spazio](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="a261f-156">* Controllo duplicati abilitato nell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="a261f-157">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-157">Error description</span></span> | <span data-ttu-id="a261f-158">Numero di controllo duplicato</span><span class="sxs-lookup"><span data-stu-id="a261f-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="a261f-159">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-159">User action</span></span> | <span data-ttu-id="a261f-160">Questo errore indica che il messaggio ricevuto contiene numeri di controllo duplicati.</span><span class="sxs-lookup"><span data-stu-id="a261f-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="a261f-161">Correggere il numero di controllo e inviare nuovamente il messaggio</span><span class="sxs-lookup"><span data-stu-id="a261f-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="a261f-162">* Schema mancante nell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="a261f-163">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-163">Error description</span></span> | <span data-ttu-id="a261f-164">Errore rilevato durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="a261f-164">Error encountered during parsing.</span></span> <span data-ttu-id="a261f-165">Il set di transazioni X12 con ID "564220001" contenuto nel gruppo funzionale con ID "56422", in interscambio con ID "000056422", con ID mittente "12345678       ", ID ricevitore "87654321       " viene sospeso con i seguenti errori: "Il messaggio presenta un tipo di documento non previsto e non è stato risolto in nessuno degli schemi esistenti configurati nell'accordo"</span><span class="sxs-lookup"><span data-stu-id="a261f-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="a261f-166">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-166">User action</span></span> | <span data-ttu-id="a261f-167">Configurare lo schema nelle impostazioni dell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="a261f-168">* Schema non corretto nell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="a261f-169">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-169">Error description</span></span> | <span data-ttu-id="a261f-170">Il messaggio ha un tipo di documento sconosciuto e non è stato risolto in nessuno degli schemi esistenti configurati nell'accordo.</span><span class="sxs-lookup"><span data-stu-id="a261f-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="a261f-171">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-171">User action</span></span> | <span data-ttu-id="a261f-172">Configurare lo schema corretto nelle impostazioni dell'accordo</span><span class="sxs-lookup"><span data-stu-id="a261f-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="a261f-173">File flat</span><span class="sxs-lookup"><span data-stu-id="a261f-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="a261f-174">* Messaggio di input senza corpo</span><span class="sxs-lookup"><span data-stu-id="a261f-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a261f-175">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="a261f-175">Error description</span></span> | <span data-ttu-id="a261f-176">Modello non valido.</span><span class="sxs-lookup"><span data-stu-id="a261f-176">InvalidTemplate.</span></span> <span data-ttu-id="a261f-177">Impossibile elaborare le espressioni del linguaggio del modello negli input dell'azione "Flat_File_Decoding", riga "1" e colonna "1902". Per la proprietà obbligatoria "content" è previsto un valore ma risulta null.</span><span class="sxs-lookup"><span data-stu-id="a261f-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="a261f-178">Percorso ".'.</span><span class="sxs-lookup"><span data-stu-id="a261f-178">Path ''.'.</span></span> |
| <span data-ttu-id="a261f-179">Azione utente</span><span class="sxs-lookup"><span data-stu-id="a261f-179">User action</span></span> | <span data-ttu-id="a261f-180">Questo errore indica che il messaggio di input non contiene un corpo</span><span class="sxs-lookup"><span data-stu-id="a261f-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="a261f-181">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a261f-181">Learn more</span></span>
[<span data-ttu-id="a261f-182">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a261f-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
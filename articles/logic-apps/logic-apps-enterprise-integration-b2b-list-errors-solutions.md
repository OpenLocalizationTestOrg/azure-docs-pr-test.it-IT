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
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="9ace5-103">Elenco di errori e soluzioni per le app per la logica B2B</span><span class="sxs-lookup"><span data-stu-id="9ace5-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="9ace5-104">Questo articolo consente di risolvere gli errori che si possono verificare negli scenari con le app per la logica B2B e suggerisce le azioni appropriate per la correzione degli errori.</span><span class="sxs-lookup"><span data-stu-id="9ace5-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="9ace5-105">Risoluzione dell'accordo</span><span class="sxs-lookup"><span data-stu-id="9ace5-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="9ace5-106">* Non sono stati trovati accordi</span><span class="sxs-lookup"><span data-stu-id="9ace5-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="9ace5-107">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-107">Error description</span></span> | <span data-ttu-id="9ace5-108">Non sono stati trovati accordi con parametri di risoluzione del contratto</span><span class="sxs-lookup"><span data-stu-id="9ace5-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="9ace5-109">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-109">User action</span></span> | <span data-ttu-id="9ace5-110">contratto Hello deve essere aggiunti come account di integrazione toohello con identità di business concordata.</span><span class="sxs-lookup"><span data-stu-id="9ace5-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="9ace5-111">identità di business Hello devono corrispondere gli ID di messaggio di input toohello</span><span class="sxs-lookup"><span data-stu-id="9ace5-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="9ace5-112">* Non sono stati trovati accordi con le identità</span><span class="sxs-lookup"><span data-stu-id="9ace5-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9ace5-113">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-113">Error description</span></span> | <span data-ttu-id="9ace5-114">Non sono stati trovati accordi con le identità: 'AS2Identity'::'Partner1' e 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="9ace5-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="9ace5-115">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-115">User action</span></span> | <span data-ttu-id="9ace5-116">AS2 non valido-da o per l'accordo AS2-tooconfigured.</span><span class="sxs-lookup"><span data-stu-id="9ace5-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="9ace5-117">Il messaggio AS2 corretto AS2-da o le intestazioni con configurazioni di contratto del messaggio AS2 tooheaders o contratto ID toomatch AS2 AS2</span><span class="sxs-lookup"><span data-stu-id="9ace5-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="9ace5-118">AS2</span><span class="sxs-lookup"><span data-stu-id="9ace5-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="9ace5-119">* Intestazioni del messaggio AS2 mancanti</span><span class="sxs-lookup"><span data-stu-id="9ace5-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="9ace5-120">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-120">Error description</span></span>| <span data-ttu-id="9ace5-121">Intestazioni AS2 non valide.</span><span class="sxs-lookup"><span data-stu-id="9ace5-121">Invalid AS2 headers.</span></span> <span data-ttu-id="9ace5-122">Una delle intestazioni "AS2-To" o "AS2-From" è vuota</span><span class="sxs-lookup"><span data-stu-id="9ace5-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="9ace5-123">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-123">User action</span></span> | <span data-ttu-id="9ace5-124">È stato ricevuto un messaggio AS2 che non conteneva hello AS2-da AS2 tooor o entrambe le intestazioni.</span><span class="sxs-lookup"><span data-stu-id="9ace5-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="9ace5-125">Controllare il messaggio AS2 AS2-da e AS2 tooheaders e correggerli in base alla configurazione di contratto</span><span class="sxs-lookup"><span data-stu-id="9ace5-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="9ace5-126">* Corpo e intestazioni del messaggio AS2 mancanti</span><span class="sxs-lookup"><span data-stu-id="9ace5-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="9ace5-127">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-127">Error description</span></span>| <span data-ttu-id="9ace5-128">contenuto della richiesta Hello è null o vuoto</span><span class="sxs-lookup"><span data-stu-id="9ace5-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="9ace5-129">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-129">User action</span></span> | <span data-ttu-id="9ace5-130">È stato ricevuto un messaggio AS2 che non contiene il corpo del messaggio hello</span><span class="sxs-lookup"><span data-stu-id="9ace5-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="9ace5-131">* Errore di decrittografia del messaggio AS2</span><span class="sxs-lookup"><span data-stu-id="9ace5-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9ace5-132">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-132">Error description</span></span> |  <span data-ttu-id="9ace5-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="9ace5-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="9ace5-134">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-134">User action</span></span> | <span data-ttu-id="9ace5-135">Aggiungere @base64ToBinary tooAS2Message prima dell'invio toopartner</span><span class="sxs-lookup"><span data-stu-id="9ace5-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="9ace5-136">* Errore di decrittografia della notifica sulla ricezione del messaggio</span><span class="sxs-lookup"><span data-stu-id="9ace5-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9ace5-137">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-137">Error description</span></span> |  <span data-ttu-id="9ace5-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="9ace5-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="9ace5-139">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-139">User action</span></span> | <span data-ttu-id="9ace5-140">Aggiungere @base64ToBinary tooMDN prima dell'invio toopartner</span><span class="sxs-lookup"><span data-stu-id="9ace5-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="9ace5-141">* Certificato di firma mancante</span><span class="sxs-lookup"><span data-stu-id="9ace5-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="9ace5-142">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-142">Error description</span></span>| <span data-ttu-id="9ace5-143">Hello certificato di firma non è stato configurato per l'entità AS2.</span><span class="sxs-lookup"><span data-stu-id="9ace5-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="9ace5-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="9ace5-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="9ace5-145">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-145">User action</span></span> | <span data-ttu-id="9ace5-146">Configurare le impostazioni dell'accordo AS2 con il certificato corretto per la firma</span><span class="sxs-lookup"><span data-stu-id="9ace5-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="9ace5-147">X12 ed EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9ace5-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="9ace5-148">* Trovato spazio iniziale o finale</span><span class="sxs-lookup"><span data-stu-id="9ace5-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="9ace5-149">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-149">Error description</span></span> | <span data-ttu-id="9ace5-150">Errore rilevato durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="9ace5-150">Error encountered during parsing.</span></span> <span data-ttu-id="9ace5-151">salve Edifact set di transazioni con id ' 123456 'contenuto nell'interscambio (senza gruppo) con id ' 987654', ID mittente 'Partner1', id ricevitore 'Partner2' verrà sospeso con i seguenti errori: separatore iniziali finali trovato</span><span class="sxs-lookup"><span data-stu-id="9ace5-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="9ace5-152">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-152">User action</span></span> | <span data-ttu-id="9ace5-153">Hello contratto impostazioni toobe configurato tooallow spazi iniziali e finali.</span><span class="sxs-lookup"><span data-stu-id="9ace5-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="9ace5-154">Modifica contratto impostazioni tooallow spazi iniziali e finali</span><span class="sxs-lookup"><span data-stu-id="9ace5-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![consentire spazio](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="9ace5-156">* Controllo duplicati è abilitata nell'accordo hello</span><span class="sxs-lookup"><span data-stu-id="9ace5-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="9ace5-157">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-157">Error description</span></span> | <span data-ttu-id="9ace5-158">Numero di controllo duplicato</span><span class="sxs-lookup"><span data-stu-id="9ace5-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="9ace5-159">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-159">User action</span></span> | <span data-ttu-id="9ace5-160">Questo errore indica che il messaggio hello ricevuto ha numeri di controllo duplicati.</span><span class="sxs-lookup"><span data-stu-id="9ace5-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="9ace5-161">Correggere il numero di controllo hello e inviare di nuovo il messaggio hello</span><span class="sxs-lookup"><span data-stu-id="9ace5-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="9ace5-162">* Schema mancante nell'accordo hello</span><span class="sxs-lookup"><span data-stu-id="9ace5-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="9ace5-163">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-163">Error description</span></span> | <span data-ttu-id="9ace5-164">Errore rilevato durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="9ace5-164">Error encountered during parsing.</span></span> <span data-ttu-id="9ace5-165">set di transazioni Hello X12 con id '564220001' contenuto nel gruppo funzionale con id '56422', nell'interscambio con id '000056422', ID mittente ' 12345678', id ricevitore ' 87654321 ' verrà sospeso. errori seguenti "messaggio hello ha un ty documento sconosciuto PE e non è stato risolto tooany degli schemi esistenti di hello configurato nel contratto hello "</span><span class="sxs-lookup"><span data-stu-id="9ace5-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="9ace5-166">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-166">User action</span></span> | <span data-ttu-id="9ace5-167">Configurare le impostazioni dell'accordo hello dello schema</span><span class="sxs-lookup"><span data-stu-id="9ace5-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="9ace5-168">* Schema errato nell'accordo hello</span><span class="sxs-lookup"><span data-stu-id="9ace5-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="9ace5-169">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-169">Error description</span></span> | <span data-ttu-id="9ace5-170">messaggio Hello è un tipo di documento sconosciuto e non è stato risolto tooany degli schemi esistenti di hello configurato nel contratto hello.</span><span class="sxs-lookup"><span data-stu-id="9ace5-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="9ace5-171">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-171">User action</span></span> | <span data-ttu-id="9ace5-172">Configurare le impostazioni dell'accordo hello schema corretto</span><span class="sxs-lookup"><span data-stu-id="9ace5-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="9ace5-173">File flat</span><span class="sxs-lookup"><span data-stu-id="9ace5-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="9ace5-174">* Messaggio di input senza corpo</span><span class="sxs-lookup"><span data-stu-id="9ace5-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="9ace5-175">Descrizione dell'errore</span><span class="sxs-lookup"><span data-stu-id="9ace5-175">Error description</span></span> | <span data-ttu-id="9ace5-176">Modello non valido.</span><span class="sxs-lookup"><span data-stu-id="9ace5-176">InvalidTemplate.</span></span> <span data-ttu-id="9ace5-177">Espressioni di linguaggio di modello non è possibile tooprocess in input di azione 'Flat_File_Decoding' alla riga '1' e alla colonna '1902': ' necessarie proprietà 'content' prevede un valore, ma è null.</span><span class="sxs-lookup"><span data-stu-id="9ace5-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="9ace5-178">Percorso ".'.</span><span class="sxs-lookup"><span data-stu-id="9ace5-178">Path ''.'.</span></span> |
| <span data-ttu-id="9ace5-179">Azione utente</span><span class="sxs-lookup"><span data-stu-id="9ace5-179">User action</span></span> | <span data-ttu-id="9ace5-180">Questo errore indica che non contiene un corpo messaggio di input hello</span><span class="sxs-lookup"><span data-stu-id="9ace5-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="9ace5-181">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="9ace5-181">Learn more</span></span>
[<span data-ttu-id="9ace5-182">Altre informazioni su hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="9ace5-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)

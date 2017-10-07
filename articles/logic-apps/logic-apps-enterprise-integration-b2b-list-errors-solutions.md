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
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Elenco di errori e soluzioni per le app per la logica B2B  
Questo articolo consente di risolvere gli errori che si possono verificare negli scenari con le app per la logica B2B e suggerisce le azioni appropriate per la correzione degli errori.


## <a name="agreement-resolution"></a>Risoluzione dell'accordo

### <a name="no-agreement-found"></a>* Non sono stati trovati accordi 

|   |   |  
|---|---|
| Descrizione dell'errore | Non sono stati trovati accordi con parametri di risoluzione del contratto|    
| Azione utente | contratto Hello deve essere aggiunti come account di integrazione toohello con identità di business concordata.</br> identità di business Hello devono corrispondere gli ID di messaggio di input toohello|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* Non sono stati trovati accordi con le identità

|   |   | 
|---|---|
| Descrizione dell'errore | Non sono stati trovati accordi con le identità: 'AS2Identity'::'Partner1' e 'AS2Identity'::'Partner3'| 
| Azione utente | AS2 non valido-da o per l'accordo AS2-tooconfigured. </br> Il messaggio AS2 corretto AS2-da o le intestazioni con configurazioni di contratto del messaggio AS2 tooheaders o contratto ID toomatch AS2 AS2 |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* Intestazioni del messaggio AS2 mancanti  

|   |   |  
|---|---|
| Descrizione dell'errore| Intestazioni AS2 non valide. Una delle intestazioni "AS2-To" o "AS2-From" è vuota| 
| Azione utente | È stato ricevuto un messaggio AS2 che non conteneva hello AS2-da AS2 tooor o entrambe le intestazioni. </br> Controllare il messaggio AS2 AS2-da e AS2 tooheaders e correggerli in base alla configurazione di contratto |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Corpo e intestazioni del messaggio AS2 mancanti    

|   |   |  
|---|---|
| Descrizione dell'errore| contenuto della richiesta Hello è null o vuoto | 
| Azione utente | È stato ricevuto un messaggio AS2 che non contiene il corpo del messaggio hello |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* Errore di decrittografia del messaggio AS2

|   |   | 
|---|---|
| Descrizione dell'errore |  [processed/Error: decryption-failed] | 
| Azione utente | Aggiungere @base64ToBinary tooAS2Message prima dell'invio toopartner 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* Errore di decrittografia della notifica sulla ricezione del messaggio

|   |   | 
|---|---|
| Descrizione dell'errore |  [processed/Error: decryption-failed] | 
| Azione utente | Aggiungere @base64ToBinary tooMDN prima dell'invio toopartner 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* Certificato di firma mancante

|   |   |  
|---|---|
| Descrizione dell'errore| Hello certificato di firma non è stato configurato per l'entità AS2. </br> AS2-From: partner1 AS2-To: partner2 | 
| Azione utente | Configurare le impostazioni dell'accordo AS2 con il certificato corretto per la firma |
|  |  | 

## <a name="x12-and-edifact"></a>X12 ed EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Trovato spazio iniziale o finale    
    
|   |   | 
|---|---|
| Descrizione dell'errore | Errore rilevato durante l'analisi. salve Edifact set di transazioni con id ' 123456 'contenuto nell'interscambio (senza gruppo) con id ' 987654', ID mittente 'Partner1', id ricevitore 'Partner2' verrà sospeso con i seguenti errori: separatore iniziali finali trovato |
| Azione utente | Hello contratto impostazioni toobe configurato tooallow spazi iniziali e finali. </br> Modifica contratto impostazioni tooallow spazi iniziali e finali |
|   |   |

![consentire spazio](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Controllo duplicati è abilitata nell'accordo hello

|   |   | 
|---|---| 
| Descrizione dell'errore | Numero di controllo duplicato |
| Azione utente | Questo errore indica che il messaggio hello ricevuto ha numeri di controllo duplicati. </br> Correggere il numero di controllo hello e inviare di nuovo il messaggio hello |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Schema mancante nell'accordo hello

|   |   | 
|---|---| 
| Descrizione dell'errore | Errore rilevato durante l'analisi. set di transazioni Hello X12 con id '564220001' contenuto nel gruppo funzionale con id '56422', nell'interscambio con id '000056422', ID mittente ' 12345678', id ricevitore ' 87654321 ' verrà sospeso. errori seguenti "messaggio hello ha un ty documento sconosciuto PE e non è stato risolto tooany degli schemi esistenti di hello configurato nel contratto hello " |
| Azione utente | Configurare le impostazioni dell'accordo hello dello schema  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Schema errato nell'accordo hello

|   |   | 
|---|---| 
| Descrizione dell'errore | messaggio Hello è un tipo di documento sconosciuto e non è stato risolto tooany degli schemi esistenti di hello configurato nel contratto hello. |
| Azione utente | Configurare le impostazioni dell'accordo hello schema corretto  |
|   |   |

## <a name="flat-file"></a>File flat

### <a name="-input-message-with-no-body"></a>* Messaggio di input senza corpo

|   |   | 
|---|---|
| Descrizione dell'errore | Modello non valido. Espressioni di linguaggio di modello non è possibile tooprocess in input di azione 'Flat_File_Decoding' alla riga '1' e alla colonna '1902': ' necessarie proprietà 'content' prevede un valore, ma è null. Percorso ".'. |
| Azione utente | Questo errore indica che non contiene un corpo messaggio di input hello |
|   |   | 

## <a name="learn-more"></a>Altre informazioni
[Altre informazioni su hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md)

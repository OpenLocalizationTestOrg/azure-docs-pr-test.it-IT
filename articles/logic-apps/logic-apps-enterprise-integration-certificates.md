---
title: i certificati aaaUsing con Enterprise Integration Pack | Documenti Microsoft
description: Informazioni su come toouse certificati con hello Enterprise Integration Pack | App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Informazioni sui certificati ed Enterprise Integration Pack
## <a name="overview"></a>Panoramica
Integrazione di Enterprise utilizza le comunicazioni di certificati toosecure B2B. È possibile usare due tipi di certificati nelle app di Enterprise Integration:

* Certificati pubblici, che devono essere acquistati da un'autorità di certificazione (CA).
* Certificati privati, che si possono rilasciare personalmente. In alcuni casi, questi certificati sono autofirmati tooas cui viene fatto riferimento.

## <a name="what-are-certificates"></a>Che cosa sono i certificati?
I certificati sono documenti digitali per verificare l'identità hello di partecipanti hello comunicazioni elettroniche e che inoltre proteggere le comunicazioni elettroniche.

## <a name="why-use-certificates"></a>Perché usare i certificati?
In alcuni casi è necessario garantire la riservatezza delle comunicazioni B2B. Integrazione di Enterprise utilizza i certificati toosecure queste comunicazioni in due modi:

* Grazie alla crittografia contenuto hello dei messaggi
* Apponendo una firma digitale ai messaggi  

## <a name="upload-a-public-certificate"></a>Caricare un certificato pubblico

toouse un *certificato pubblico* nelle App logica con funzionalità B2B, è innanzitutto necessario certificato hello tooupload nell'account di integrazione.  

Dopo aver caricato un certificato, è disponibile toohelp è proteggere i messaggi B2B quando si definiscono le relative proprietà in hello [contratti](logic-apps-enterprise-integration-agreements.md) creati.  

Ecco i passaggi dettagliati per caricare i certificati pubblici nell'account di integrazione dopo l'accesso al portale di Azure toohello hello:

1. Selezionare **più servizi** e immettere **integrazione** nella casella di ricerca di hello filtro. Selezionare **account di integrazione** dall'elenco dei risultati hello     
![Selezionare Esplora](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Selezionare hello integrazione account toowhich si desidera tooadd hello certificato.  
![Selezionare hello integrazione account toowhich si desidera tooadd hello certificato](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Seleziona hello **certificati** riquadro.  
![Riquadro hello selezionare certificati](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. In hello **certificati** pannello visualizzato, seleziona hello **Aggiungi** pulsante.   
![Pulsante Aggiungi hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Immettere un **nome** per il certificato e quindi selezionare hello tipo di certificato come **pubblica** dall'elenco a discesa hello.  
6. Icona della cartella selezionare hello sul lato destro hello di hello **certificato** casella di testo. Quando si apre il selettore di file hello, individuare e selezionare il file di certificato hello cui account di integrazione tooyour tooupload.
7. Selezionare il certificato di hello, quindi **OK** nel selettore file hello. Questa convalida e carica hello certificato tooyour integrazione account.
8. Infine, eseguire il backup su hello **Aggiungi certificato** blade, seleziona hello **OK** pulsante.  
![Selezionare pulsante OK hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Seleziona hello **certificati** riquadro. Dovrebbe essere hello appena aggiunto certificato.  
![Vedere il nuovo certificato di hello](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Caricare un certificato privato

toouse un *certificato privato* nelle App logica con funzionalità B2B, è possibile caricare un account di integrazione tooyour certificato privato da hello richiede alla procedura seguente

1. [Caricare il tooKey chiave privata insieme di credenziali](../key-vault/key-vault-get-started.md "informazioni sull'insieme di credenziali chiave") e fornire un **nome chiave** 
   
   > [!TIP]
   > È necessario autorizzare le operazioni di App per la logica tooperform in insieme di credenziali chiave. È possibile concedere l'entità di servizio App per la logica di accesso toohello utilizzando hello comando PowerShell seguente:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Dopo aver acquisito passaggio precedente hello, aggiungere un account di toointegration certificato privato.

Seguenti sono hello i passaggi dettagliati per il caricamento dei certificati privati all'account di integrazione dopo l'accesso toohello portale di Azure:  
 
1. Selezionare hello integrazione account toowhich si desidera che il certificato di hello tooadd e si seleziona hello **certificati** riquadro.  
![Riquadro hello selezionare certificati](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. In hello **certificati** pannello visualizzato, seleziona hello **Aggiungi** pulsante.   
![Pulsante Aggiungi hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Immettere un **nome** per il certificato e il tipo di certificato selezionare hello come **privata** dall'elenco a discesa hello.   
4. Selezionare l'icona della cartella hello sul lato destro hello di hello **certificato** casella di testo. Quando si apre il selettore di file hello, trovare hello corrispondente certificato pubblico che si desidera l'account di integrazione tooyour tooupload.   
   
   > [!Note]
   > Durante l'aggiunta di un certificato privato è importante tooadd corrispondente pubblica certificato tooshow in [accordo AS2](logic-apps-enterprise-integration-as2.md) ricevere e inviare le impostazioni per la firma e crittografia dei messaggi hello.
   > 
   >   

5. Seleziona hello **gruppo di risorse**, **insieme di credenziali chiave**, **nome chiave** e seleziona hello **OK** pulsante.  
![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Seleziona hello **certificati** riquadro. Dovrebbe essere hello appena aggiunto certificato.
![Vedere il nuovo certificato di hello](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Creare un contratto B2B](logic-apps-enterprise-integration-agreements.md)  
* [Altre informazioni sull'insieme di credenziali delle chiavi](../key-vault/key-vault-get-started.md "Informazioni sull'insieme di credenziali delle chiavi")  


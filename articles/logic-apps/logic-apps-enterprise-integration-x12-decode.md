---
title: i messaggi X12 aaaDecode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e generare i riconoscimenti con decodificatore messaggio hello X12 in hello Enterprise Integration Pack per le app di logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Decodificare X12 messaggi per le app di Azure logica con hello Enterprise Integration Pack

Con connettore di messaggi hello Decode X12, è possibile convalidare la busta hello contro un accordo tra partner commerciali, la convalida EDI e proprietà specifiche del partner, suddividere gli interscambi in set di transazioni o mantenere gli interscambi intera e generare Riconoscimenti per transazioni elaborate. toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure. È necessario disporre di un connettore di messaggio integrazione account toouse hello Decode X12.
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.
* Un [contratto X12](logic-apps-enterprise-integration-x12.md) già definito nell'account di integrazione.

## <a name="decode-x12-messages"></a>Messaggi Decode X12

1. [Creare un'app per la logica](logic-apps-create-a-logic-app.md).

2. connettore di messaggi Hello Decode X12 non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.

3.  Nella casella di ricerca hello, immettere "x12" per il filtro. Selezionare **X12 - Decodifica il messaggio X12**.
   
    ![Cercare "X12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione. Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect. 

    ![Fornire i dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    Le proprietà con l'asterisco sono obbligatorie.

    | Proprietà | Dettagli |
    | --- | --- |
    | Nome connessione * |Immettere un nome per la connessione. |
    | Account di integrazione * |Immettere un nome per l'account di integrazione. Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure. |

5.  Al termine, i dettagli relativi alla connessione dovrebbero essere simile toothis esempio. toofinish della creazione della connessione, scegliere **crea**.
   
    ![dettagli della connessione all'account di integrazione](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. Dopo aver creata la connessione, come illustrato in questo esempio, selezionare toodecode messaggio file flat di hello X12.

    ![connessione all'account di integrazione creata](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    Ad esempio:

    ![Selezionare il messaggio con il file flat X12 da decodificare](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>Dettagli Decode X12

connettore Decode Hello X12 esegue queste attività:

* Convalida la busta hello contro l'accordo tra partner commerciali
* Convalida le proprietà EDI e specifiche del partner.
  * Convalida strutturale EDI e convalida estesa dello schema.
  * Convalida della struttura di hello della busta dell'interscambio hello.
  * Convalida dello schema della busta hello rispetto allo schema di controllo hello.
  * Convalida dello schema di elementi di dati di set di transazioni hello rispetto allo schema di messaggio hello.
  * Convalida EDI eseguita sugli elementi dati del set di transazioni. 
* Verifica che hello interscambio, gruppo e transazioni set di numeri di controllo non siano duplicati
  * Verifica numero di controllo di interscambio hello con gli interscambi ricevuti in precedenza.
  * Verifica numero di controllo gruppo hello con gli altri numeri di controllo di gruppo nell'interscambio hello.
  * Controlla il numero di controllo del set di transazioni hello con gli altri numeri di controllo set transazioni in tale gruppo.
* Suddivide hello interscambio in set di transazioni o mantiene hello intero interscambio:
  * Suddivide l'interscambio in set di transazioni - sospende i set di transazioni in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni. 
  azione di decodifica Hello X12 restituisce solo i set di transazioni che non superano la convalida troppo`badMessages`e restituisce hello transazioni rimanenti imposta troppo`goodMessages`.
  * Suddivide l'interscambio in set di transazioni - sospende l'interscambio in caso di errore: suddivide l'interscambio in set di transazioni e analizza ogni set di transazioni. 
  Se i set di convalida non riuscita di interscambio hello uno o più transazioni, l'azione Decode hello X12 output tutti hello set di transazioni nell'interscambio troppo`badMessages`.
  * Mantieni interscambio - Sospendi set transazioni in caso di errore: interscambio hello Preserve e processo hello intero interscambio in batch. 
  azione di decodifica Hello X12 restituisce solo i set di transazioni che non superano la convalida troppo`badMessages`e restituisce hello transazioni rimanenti imposta troppo`goodMessages`.
  * Mantieni interscambio - Sospendi interscambio in caso di errore: interscambio hello Preserve e processo hello intero interscambio in batch. 
  Se i set di convalida non riuscita di interscambio hello uno o più transazioni, l'azione Decode hello X12 output tutti hello set di transazioni nell'interscambio troppo`badMessages`. 
* Genera un riconoscimento tecnico e/o funzionale (se configurata).
  * Un riconoscimento tecnico viene generato in seguito alla convalida dell'intestazione. Hello riconoscimento tecnico segnala hello lo stato di elaborazione hello di un'intestazione di interscambio e trailer da ricevitore dell'indirizzo hello.
  * Un riconoscimento funzionale viene generato in seguito alla convalida del corpo. riconoscimento funzionale Hello segnala ogni errore rilevato durante l'elaborazione di hello ricevuto documento

## <a name="view-hello-swagger"></a>Swagger hello vista
Vedere hello [swagger dettagli](/connectors/x12/). 

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Enterprise Integration Pack hello](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 


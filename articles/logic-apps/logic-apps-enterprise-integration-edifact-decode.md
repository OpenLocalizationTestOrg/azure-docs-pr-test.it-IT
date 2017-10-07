---
title: i messaggi EDIFACT aaaDecode - App Azure per la logica | Documenti Microsoft
description: Convalida EDI e generare i riconoscimenti con decodificatore messaggio EDIFACT di hello in hello Enterprise Integration Pack per le app di logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Decodificare i messaggi EDIFACT per le app di Azure logica con hello Enterprise Integration Pack

Con connettore di messaggi hello decodificare EDIFACT, si può convalidare EDI e proprietà specifiche del partner, suddividere gli interscambi in set di transazioni o mantenere gli interscambi intera e generare riconoscimenti per transazioni elaborate. toouse questo connettore, è necessario aggiungere hello connettore tooan trigger nell'app logica esistente.

## <a name="before-you-start"></a>Prima di iniziare

Ecco gli elementi di hello che è necessario:

* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [account di integrazione](logic-apps-enterprise-integration-create-integration-account.md) già definito e associato alla sottoscrizione di Azure. È necessario disporre di un connettore di messaggio integrazione account toouse hello decodificare EDIFACT. 
* Almeno due [partner](logic-apps-enterprise-integration-partners.md) già definiti nell'account di integrazione.
* Un [contratto EDIFACT](logic-apps-enterprise-integration-edifact.md) già definito nell'account di integrazione.

## <a name="decode-edifact-messages"></a>Decodificare messaggi EDIFACT

1. [Creare un'app per la logica](logic-apps-create-a-logic-app.md).

2. connettore di messaggi Hello decodificare EDIFACT non dispone di trigger, pertanto è necessario aggiungere un trigger per avviare l'app di logica, ad esempio un trigger di richiesta. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'app di logica di azione tooyour.

3. Nella casella di ricerca hello, immettere "EDIFACT" come filtro. Selezionare **Decodifica il messaggio EDIFACT**.
   
    ![ricerca di EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Se è stato creato in precedenza tutte le connessioni tooyour account di integrazione, viene chiesto toocreate ora tale connessione. Nome della connessione, quindi selezionare account di integrazione hello che si desidera tooconnect.
   
    ![creare un account di integrazione](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Le proprietà con l'asterisco sono obbligatorie.

    | Proprietà | Dettagli |
    | --- | --- |
    | Nome connessione * |Immettere un nome per la connessione. |
    | Account di integrazione * |Immettere un nome per l'account di integrazione. Assicurarsi che l'app di account e la logica di integrazione siano hello nello stesso percorso di Azure. |

4. Al termine della creazione della connessione toofinish, scegliere **crea**. Dettagli relativi alla connessione dovrebbero essere simile toothis esempio:

    ![dettagli dell'account di integrazione](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Dopo aver creata la connessione, come illustrato in questo esempio, selezionare toodecode messaggio file flat di hello EDIFACT.

    ![connessione all'account di integrazione creata](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Ad esempio:

    ![Selezionare il messaggio con il file flat EDIFACT da decodificare](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>Dettagli decodificatore EDIFACT

connettore di decodificare EDIFACT Hello esegue queste attività: 

* Convalida la busta hello contro l'accordo tra partner commerciali.
* Risolve l'accordo hello associando qualificatore mittente hello & identificatore qualificatore ricevitore e identificatore.
* Suddivide un interscambio in più transazioni quando interscambio hello ha più di una transazione in base hello del contratto di configurazione delle impostazioni di ricezione.
* Disassembla l'interscambio hello.
* Convalida le proprietà EDI e specifiche del partner, comprese:
  * Convalida della struttura di busta interscambio hello
  * Convalida dello schema della busta hello rispetto allo schema di controllo hello
  * Convalida dello schema di elementi di dati di set di transazioni hello rispetto allo schema di messaggio hello
  * Convalida EDI eseguita sugli elementi dati del set di transazioni.
* Verifica che hello interscambio, gruppo e transazioni set di numeri di controllo non siano duplicati (se configurata) 
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
* Genera un riconoscimento tecnico (controllo) e/o funzionale (se configurata).
  * Un riconoscimento tecnico o hello ACK CONTRL segnala i risultati di hello di un controllo sintattico dell'interscambio ricevuto hello completo.
  * Un riconoscimento funzionale riconosce l'accettazione o il rifiuto di un interscambio o un gruppo ricevuto.

## <a name="view-swagger-file"></a>Visualizzare il file Swagger
vedere i dettagli di Swagger hello tooview per connettore EDIFACT hello, [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack") 


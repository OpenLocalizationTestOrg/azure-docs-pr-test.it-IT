---
title: concetti di griglia eventi aaaAzure
description: Vengono descritti il servizio Griglia di eventi di Azure e i concetti correlati. Vengono definiti diversi componenti chiave di Griglia di eventi.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Concetti di Griglia di eventi di Azure

i concetti principali di Hello nella griglia di eventi di Azure sono:

## <a name="events"></a>Events

Un evento è una quantità minima di hello di informazioni che descrive un elemento che si sono verificati nel sistema hello.  Ogni evento dispone di informazioni comuni, ad esempio: origine dell'evento hello, hello ora ha avuto luogo e l'identificatore univoco.  Ogni evento dispone di informazioni specifiche che sono solo toohello rilevanti evento specifico. Ad esempio, un evento su un nuovo file viene creato in archiviazione di Azure contiene i dettagli sul file hello, ad esempio il valore di lastTimeModified hello. In alternativa, un evento su un riavvio della macchina virtuale contiene il nome di hello della macchina virtuale hello e hello motivo per il riavvio.

## <a name="event-sourcespublishers"></a>Origini/autori di eventi

Un'origine eventi è in cui si verifica l'evento di hello. Archiviazione di Azure ad esempio, è l'origine eventi hello per blob creato gli eventi. L'infrastruttura di Azure VM è l'origine evento hello per gli eventi di macchina virtuale. Le origini eventi sono responsabili per la pubblicazione di eventi tooEvent griglia.

## <a name="topics"></a>Argomenti

Gli autori classificano gli eventi in argomenti. argomento Hello include un endpoint in cui i server di pubblicazione hello invia eventi. toorespond toocertain tipi di eventi, i sottoscrittori decidere quali toosubscribe argomenti per. Negli argomenti vengono anche uno schema di eventi in modo che i sottoscrittori possono individuare come tooconsume hello eventi in modo appropriato.

Gli argomenti di sistema sono argomenti predefiniti forniti dai servizi di Azure. Gli argomenti personalizzati sono argomenti di applicazioni e di terze parti.

## <a name="event-subscriptions"></a>Sottoscrizioni di eventi

Una sottoscrizione indica a Griglia di eventi gli eventi relativi a un argomento che il sottoscrittore è interessato a ricevere.  Una sottoscrizione contiene inoltre informazioni su come gli eventi devono essere consegnati toohello sottoscrittore.

## <a name="event-handlers"></a>Gestori eventi

Dal punto di vista della griglia di eventi, un gestore eventi è hello in cui viene inviato l'evento hello. gestore di Hello accetta alcuni eventi di hello tooprocess azione ulteriore.  Griglia di eventi supporta diversi tipi di sottoscrittori. In base al tipo di sottoscrittore hello griglia eventi segue diversi meccanismi tooguarantee hello hello evento inviato.  Per i gestori HTTP webhook evento, evento hello viene ritentata fino a quando il gestore di hello restituisce un codice di stato `200 – OK`. Per la coda di archiviazione di Azure, gli eventi di hello vengono ritentati fino a quando non hello servizio di accodamento è in grado di toosuccessfully push messaggio hello di processo in coda hello.

## <a name="filters"></a>Filtri

Quando si sottoscrive tooa argomento, è possibile filtrare gli eventi di hello inviati toohello endpoint. È possibile filtrare in base a tipo di evento o criterio di oggetto. Per altre informazioni, vedere [Schema di sottoscrizione per Griglia di eventi](subscription-creation-schema.md).

## <a name="security"></a>Sicurezza

L'evento fornisce la protezione per la sottoscrizione tootopics e pubblicazione di argomenti. Quando la sottoscrizione, è necessario disporre delle autorizzazioni appropriate per la risorsa hello o un argomento. Per la pubblicazione, è necessario disporre di un token di firma di accesso condiviso o l'autenticazione con chiave per l'argomento hello. Per altre informazioni, vedere [Event Grid security and authentication](security-authentication.md) (Sicurezza e autenticazione di Griglia di eventi).

## <a name="failed-delivery"></a>Recapito non riuscito

Quando la griglia di eventi non riescono a confermare che un evento è stato ricevuto dall'endpoint del sottoscrittore hello, redelivers evento hello. Per altre informazioni, vedere [Recapito di messaggi di Griglia di eventi e nuovi tentativi](delivery-and-retry.md).

## <a name="next-steps"></a>Passaggi successivi

* Per un'introduzione tooEvent griglia, vedere [sulla griglia di eventi](overview.md).
* tooquickly informazioni introduttive sull'utilizzo della griglia di eventi, vedere [route e creare eventi personalizzati con griglia di eventi di Azure](custom-event-quickstart.md).

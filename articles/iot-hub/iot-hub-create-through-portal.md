---
title: aaaUse hello toocreate portale Azure un IoT Hub | Documenti Microsoft
description: Come toocreate, gestire ed eliminare hub IoT di Azure tramite hello portale di Azure. Include informazioni su piani tariffari, ridimensionamento, sicurezza e configurazione della messaggistica.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>Creazione di un hub IoT utilizzando hello portale di Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

L'articolo illustra:

* Come toofind hello servizio IoT Hub in hello portale di Azure.
* Come toocreate e gestire hub IoT.

## <a name="where-toofind-hello-iot-hub-service"></a>Dove toofind hello servizio IoT Hub

È possibile trovare hello servizio IoT Hub in hello posizioni nel portale di hello seguenti:

* Scegliere **+ Nuovo** e quindi scegliere **Internet delle cose**.
* In hello Marketplace, scegliere **Internet of Things**.

## <a name="create-an-iot-hub"></a>Creare un hub IoT

È possibile creare un hub IoT utilizzando hello dei seguenti metodi:

* Hello **+ nuovo** opzione apre il pannello hello mostrato nella seguente cattura di schermata hello. Hello passaggi per la creazione di hub IoT hello tramite questo metodo e marketplace hello sono identici.
* In hello Marketplace, scegliere **crea** pannello hello tooopen illustrato nella seguente cattura di schermata hello.

Hello nelle sezioni seguenti vengono descritti hello diversi passaggi toocreate un hub IoT:

### <a name="choose-hello-name-of-hello-iot-hub"></a>Scegliere nome hello dell'hub IoT hello

un hub IoT toocreate, è necessario assegnare un nome hub IoT hello. Questo nome deve essere univoco in tutti gli hub IoT.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>Scegliere hello a livello di prezzo

È possibile scegliere fra quattro piani: **Gratuito**, **Standard 1**, **Standard 2** e **Standard S3**. livello gratuito Hello consente solo 500 toobe dispositivi connessi hub IoT toohello e too8, 000 messaggi al giorno.

**S1 standard**: edizione hello S1 utilizzare per le soluzioni IoT con un numero elevato di dispositivi che ogni genera piccole quantità di dati. Ogni unità dell'edizione hello S1 consente backup too400, 000 messaggi al giorno per tutti i dispositivi connessi.

**S2 standard**: edizione hello S2 utilizzare per le soluzioni di IoT in cui i dispositivi generare grandi quantità di dati. Ogni unità dell'edizione S2 hello consente backup too6 milioni di messaggi al giorno tra tutti i dispositivi connessi.

**S3 standard**: edizione hello S3 utilizzare per le soluzioni di IoT che generano grandi quantità di dati. Ogni unità dell'edizione S3 hello consente backup too300 milioni di messaggi al giorno tra tutti i dispositivi connessi.

![][4]

> [!NOTE]
> L'hub IoT consente solo un hub gratuito per sottoscrizione di Azure.

### <a name="iot-hub-units"></a>Unità hub IoT

numero di Hello di messaggi consentiti per ogni unità al giorno dipende dal livello di prezzo dell'hub. Ad esempio, se si desidera in ingresso di IoT hub toosupport di 700.000 messaggi hello, selezionare due unità di livello S1.

### <a name="device-toocloud-partitions-and-resource-group"></a>Le partizioni toocloud dispositivo e gruppo di risorse

È possibile modificare il numero di hello di partizioni per un hub IoT. numero di partizioni di Hello predefinito è 4, è possibile scegliere un numero diverso dall'elenco a discesa hello.

Non è necessario tooexplicitly creare un gruppo di risorse vuoto. Quando si crea una risorsa, è possibile scegliere entrambi toocreate un nuovo o utilizzare un gruppo di risorse esistente.

![][5]

### <a name="choose-subscription"></a>Scegliere la sottoscrizione

IoT Hub Azure automaticamente hello elenchi di account utente di hello le sottoscrizioni di Azure è collegato. È possibile scegliere l'hub IoT per hello sottoscrizione di Azure tooassociate hello.

### <a name="choose-hello-location"></a>Scegliere percorso hello

opzione del percorso Hello fornisce un elenco delle aree di hello in cui sono disponibili IoT Hub.

### <a name="create-hello-iot-hub"></a>Creazione di hub IoT hello

Dopo aver completato tutti i passaggi precedenti, è possibile creare l'hub IoT hello. Fare clic su **crea** toostart hello toocreate processo back-end e distribuire l'hub IoT hello con le opzioni di hello scelto.

Come il tempo per hello distribuzione back-end toorun nei server di percorso appropriato hello può richiedere alcuni minuti toocreate hello l'hub IoT.

## <a name="change-hello-settings-of-hello-iot-hub"></a>Modificare le impostazioni di hello dell'hub IoT hello

È possibile modificare le impostazioni di hello di un hub IoT esistente dopo averlo creato da hello pannello IoT Hub.

![][8]

**Criteri di accesso condiviso**: I criteri definiscono autorizzazioni hello per i dispositivi e servizi tooIoT tooconnect Hub. È possibile accedere a questi criteri facendo clic su **Criteri di accesso condiviso** in **Generale**. In questo pannello è possibile modificare i criteri esistenti o aggiungerne di nuovi.

### <a name="create-a-policy"></a>Creare un criterio

* Fare clic su **Aggiungi** tooopen un pannello. È possibile immettere il nuovo nome di criterio hello e autorizzazioni hello che si desidera tooassociate con questo criterio, come illustrato nell'esempio hello figura:

    Sono disponibili numerose autorizzazioni che possono essere associate a questi criteri condivisi. Hello **Registro di sistema leggere** e **scrittura del Registro di sistema** criteri concedono in lettura e registro identità toohello diritti di accesso in scrittura. Opzione hello scrittura automaticamente sceglie l'opzione di lettura hello.

    Hello **servizio connettersi** vengono concesse autorizzazioni tooaccess gli endpoint del servizio, ad esempio **ricevere da dispositivo a cloud**. Hello **dispositivo connettersi** criteri concedono le autorizzazioni per l'invio e ricezione di messaggi utilizzando gli endpoint IoT Hub sul lato dispositivo hello.

* Fare clic su **crea** tooadd questo nuovo elenco di criteri toohello esistente.

![][10]

## <a name="endpoints"></a>Endpoint

Fare clic su **endpoint** toodisplay un elenco di endpoint per l'hub IoT hello che si desidera modificare. Esistono due tipi di endpoint: gli endpoint che sono integrati in hub IoT hello e gli endpoint aggiunti hub IoT toohello dopo la sua creazione.

![][11]

### <a name="built-in-endpoints"></a>Endpoint predefiniti

Esistono due endpoint predefiniti: **Cloud feedback toodevice** e **eventi**.

* **Cloud feedback toodevice** impostazioni: questa impostazione non ha due impostazioni secondarie: **Cloud tooDevice TTL** (time-to-live) e **periodo di conservazione** (in ore) per i messaggi hello. Quando il primo crea un hub IoT, entrambe queste impostazioni hanno il valore predefinito hello di un'ora. tooadjust queste impostazioni, utilizzare dispositivi di scorrimento hello o digitare i valori hello.
* Impostazioni **Eventi**: questa impostazione presenta diverse impostazioni secondarie, alcune delle quali sono di sola lettura. Hello seguente elenco vengono descritte queste impostazioni:

  * **Partizioni**: un valore predefinito viene impostato quando viene creato l'hub IoT hello. È possibile modificare il numero di hello di partizioni tramite questa impostazione.

  * **Nome compatibile con Hub eventi e l'endpoint**: quando viene creato l'hub IoT hello, un Hub eventi è stato creato internamente che è necessario accessibili toounder determinate circostanze. Non è possibile personalizzare i valori di nome e l'endpoint di hello compatibile con Hub eventi, ma è possibile copiarli facendo **copia**.

  * **Periodo di conservazione**: giorno tooone l'impostazione predefinita, ma è possibile modificarlo tramite l'elenco a discesa hello. Questo valore è espresso in giorni per l'impostazione di dispositivo a cloud hello.

  * **Gruppi di consumer**: gruppi di Consumer consentono a più messaggi di tooread Reader in modo indipendente dall'hub IoT hello. Ogni hub IoT viene creato con un gruppo di consumer predefinito. Tuttavia, è possibile aggiungere o eliminare l'hub IoT tooyour gruppi di consumer con questa impostazione.

  > [!NOTE]
  > gruppo di consumer predefinito Hello non può essere modificato o eliminato.

### <a name="custom-endpoints"></a>Endpoint personalizzati

È possibile aggiungere endpoint personalizzati su hub IoT utilizzando portale hello. Da hello **endpoint** pannello, fare clic su **Aggiungi** in hello tooopen superiore hello **aggiungere endpoint** blade. Immettere informazioni hello necessarie, quindi fare clic su **OK**. L'endpoint personalizzato è ora elencata in hello principale **endpoint** blade.

![][13]

Altre informazioni sugli endpoint personalizzati sono disponibili in [Reference - IoT hub endpoints][lnk-devguide-endpoints] (Riferimenti: endpoint di hub IoT).

## <a name="routes"></a>Route

Fare clic su **route** toomanage come IoT Hub recapita i messaggi da dispositivo a cloud.

![][14]

È possibile aggiungere l'hub IoT tooyour route facendo **Aggiungi** nella parte superiore di hello di hello **route*** immissione delle informazioni necessarie hello e facendo clic su pannello **OK**. La route è quindi elencata in hello principale **route** blade. È possibile modificare una route selezionandola nell'elenco di hello di route. tooenable una route, selezionarlo nell'elenco di hello di route e impostare hello **abilitato** attivare o disattivare troppo**Off**. modifica di hello toosave, fare clic su **OK** nella parte inferiore di hello del pannello hello.

![][15]

## <a name="pricing-and-scale"></a>Prezzi e scalabilità

Hello prezzi di un hub IoT esistente può essere modificato tramite hello **prezzi** le impostazioni, con hello le eccezioni seguenti:

* Nell'implementazione corrente di hello, un hub IoT con uno SKU disponibile non è possibile modificare tooone livelli di hello, SKU a pagamento, o viceversa.
* Può esistere solo un hub IoT di livello gratuito nella sottoscrizione di Azure hello.

![][12]

È possibile spostare da un livello superiore di toolower solo quando il numero di hello di messaggi inviati del giorno corrente superano la quota di hello per livello più basso hello. Ad esempio, se il numero di hello di messaggi al giorno supera 400.000, hello livello per hello IoT hub può essere modificato. Tuttavia, se si modifica il livello di S1 toohello hub IoT hello è limitata per tale giorno.

## <a name="delete-hello-iot-hub"></a>Eliminare l'hub IoT hello

È possibile esplorare l'hub IoT toohello desiderato toodelete facendo **Sfoglia**, e scegliendo hello toodelete hub appropriato. toodelete hello hub IoT, fare clic su hello **eliminare** pulsante sotto il nome dell'hub IoT hello.

## <a name="next-steps"></a>Passaggi successivi

Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:

* [Gestire in blocco i dispositivi IoT][lnk-bulk]
* [Metriche di Hub IoT][lnk-metrics]
* [Monitoraggio delle operazioni][lnk-monitor]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con IoT Edge][lnk-iotedge]
* [Soluzione IoT da hello la messa a terra sicura][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md

---
title: gestione aaaDevice con l'IoT Hub Azure | Documenti Microsoft
description: 'Panoramica della gestione dei dispositivi nell''hub IoT di Azure: modelli di gestione del ciclo di vita dei dispositivi aziendali, ad esempio riavvio, ripristino delle impostazioni predefinite, aggiornamento del firmware, configurazione, dispositivi gemelli, query e processi.'
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>Panoramica della gestione dei dispositivi con l'hub IoT
## <a name="introduction"></a>Introduzione
IoT Hub Azure offre funzionalità di hello e un modello di estendibilità che consentono di dispositivo e soluzioni di gestione dei dispositivi affidabile toobuild gli sviluppatori back-end. Intervallo di dispositivi da sensori vincolati e unico scopo MicroController, i gateway toopowerful indirizzare le comunicazioni per i gruppi di dispositivi.  Inoltre, casi d'uso hello e requisiti per gli operatori di IoT variano significativamente in settori.  Nonostante questa variante, la gestione dei dispositivi con l'IoT Hub fornisce funzionalità di hello, modelli e codice librerie toocater tooa insieme eterogeneo di dispositivi e utenti finali.

Una parte essenziale della creazione di una soluzione di IoT aziendale ha esito positivo è tooprovide una strategia per la gestiscono degli operatori di gestione in corso di hello della propria raccolta di dispositivi. Operatori di IoT richiedono strumenti semplici e affidabili e le applicazioni che consentono loro toofocus su hello più aspetti strategici delle mansioni che esercitano. Questo articolo include:

* Una breve panoramica di gestione di Azure IoT Hub approccio toodevice.
* Una descrizione dei comuni principi di gestione dei dispositivi.
* Descrizione del ciclo di vita del dispositivo hello.
* Una panoramica sui comuni modelli di gestione dei dispositivi.

## <a name="device-management-principles"></a>Principi di gestione dei dispositivi
IoT è accompagnata da un set univoco di problemi di gestione di dispositivi e ogni soluzione di classe enterprise è necessario risolvere hello principi seguenti:

![Grafico dei principi di gestione dei dispositivi][img-dm_principles]

* **Scala e automazione**: IoT soluzioni richiedono strumenti semplici che è possono automatizzare le attività di routine e abilitare le operazioni di dimensioni relativamente ridotte personale toomanage milioni di dispositivi. Quotidiane, operatori prevede che le operazioni del dispositivo toohandle in modalità remota, in blocco, e tooonly un avviso quando si verificano problemi che richiedono la loro attenzione diretta.
* **Apertura e la compatibilità**: ecosistema dispositivo hello è particolarmente diverse. Gli strumenti di gestione devono essere tooaccommodate personalizzata una vasta gamma di protocolli, le classi di dispositivi e piattaforme. Gli operatori devono essere in grado di toosupport molti tipi di dispositivi, da hello più vincolati incorporato chips processo singolo, toopowerful e computer completamente funzionale.
* **Riconoscimento del contesto**: gli ambienti IoT sono dinamici e in continua evoluzione. L'affidabilità del servizio è fondamentale. Operazioni di gestione dei dispositivi devono essere prese in hello account seguenti fattori tooensure tale manutenzione tempi di inattività non influiscono sulle operazioni aziendali critici o creare condizioni pericolose:
    * Finestre di manutenzione del contratto di servizio
    * Stato di rete e di alimentazione
    * Condizioni in uso
    * Georilevazione dei dispositivi
* **Molti ruoli del servizio**: il supporto per i flussi di lavoro univoco hello e i processi dei ruoli operazioni IoT è essenziale. personale addetto alle operazioni di Hello devono funzionare harmoniously con hello a causa di limitazioni dei reparti IT interni.  Anche individuano modi sostenibile toosurface in tempo reale dispositivi operazioni informazioni toosupervisors e altri ruoli di gestione di business.

## <a name="device-lifecycle"></a>Ciclo di vita dei dispositivi
È presente un set di fasi di gestione generale dei dispositivi che sono comuni tooall enterprise IoT progetti. In Azure IoT, sono disponibili cinque fasi all'interno del ciclo di vita di hello dispositivo:

![Hello cinque fasi di ciclo di vita dei dispositivi Azure IoT: pianificare, eseguire il provisioning, configurare, monitorare, ritirare][img-device_lifecycle]

All'interno di ognuna di queste cinque fasi, esistono diversi requisiti di operatore di dispositivo che devono essere soddisfatte tooprovide una soluzione completa:

* **Pianificare**: toocreate operatori una combinazione di metadati di dispositivo che consente loro tooeasily e accuratamente la query per abilitare e associate a un gruppo di dispositivi per le operazioni di gestione delle operazioni bulk. È possibile utilizzare hello dispositivo doppi toostore metadati dispositivo sotto forma di hello di tag e proprietà.
  
    *Ulteriori informazioni*: [introduzione gemelli dispositivo][lnk-twins-getstarted], [comprendere gemelli dispositivo][lnk-twins-devguide], [come proprietà di un doppio dispositivo toouse][lnk-twin-properties].
* **Eseguire il provisioning**: in modo sicuro il provisioning di nuovi dispositivi tooIoT Hub e abilitare gli operatori tooimmediately individuare funzionalità del dispositivo.  Utilizzare le identità di hello Hub IoT identità del Registro di sistema toocreate flessibile dispositivi e le credenziali e per eseguire questa operazione in blocco tramite un processo. Compilare i dispositivi tooreport le funzionalità e le condizioni tramite le proprietà di dispositivo in un doppio dispositivo hello.
  
    *Ulteriori informazioni*: [gestire le identità dispositivo][lnk-identity-registry], [Bulk di gestione delle identità del dispositivo][lnk-bulk-identity], [Come dispositivo toouse doppio proprietà][lnk-twin-properties].
* **Configurare**: bulk facilitare le modifiche di configurazione e del firmware Aggiorna toodevices mantenendo l'integrità e sicurezza. Per eseguire queste operazioni di gestione dei dispositivi in blocco, usare le proprietà desiderate oppure metodi diretti e processi di trasmissione.
  
    *Ulteriori informazioni*: [utilizzare metodi diretti][lnk-c2d-methods], [richiamare un metodo diretto su un dispositivo][lnk-methods-devguide], [come proprietà di un doppio dispositivo toouse][lnk-twin-properties], [pianificazione e i processi di broadcast][lnk-jobs], [pianificare i processi su più dispositivi] [lnk-jobs-devguide].
* **Monitoraggio**: monitorare l'integrità raccolta generale del dispositivo, lo stato di hello di operazioni in corso e tooissues operatori avvisi che potrebbero richiedere attenzione.  Applicare hello dispositivo doppi tooallow dispositivi tooreport in tempo reale condizioni operative e lo stato delle operazioni di aggiornamento. Problemi di compilazione report del dashboard potente che hello superficie di attacco più immediato tramite query gemelli di dispositivo.
  
    *Ulteriori informazioni*: [come dispositivo toouse doppio proprietà][lnk-twin-properties], [linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ lnk-query-language].
* **Ritirare**: sostituire o rimuovere i dispositivi dopo un errore, eseguire l'aggiornamento del ciclo, o alla fine di hello della durata del servizio hello.  Utilizzare informazioni sul dispositivo di hello dispositivo doppi toomaintain se dispositivo fisico hello viene sostituito o archiviati se è stata ritirata. Utilizzare hello del Registro di sistema di IoT Hub identità per rilasciare in modo sicuro identità di dispositivi e le credenziali.
  
    *Ulteriori informazioni*: [come dispositivo toouse doppio proprietà][lnk-twin-properties], [gestire le identità dispositivo][lnk-identity-registry].

## <a name="device-management-patterns"></a>Modelli di gestione dei dispositivi
IoT Hub consente hello seguente insieme di modelli di gestione di dispositivi.  Hello [esercitazioni sulla gestione di dispositivi] [ lnk-get-started] illustrano in dettaglio come tooextend toofit questi modelli dello scenario esatto e come toodesign nuovi modelli basati su tali modelli di base.

* **Riavviare il computer** -app back-end hello informa dispositivo hello tramite un metodo diretto che ha riavviato.  proprietà tooupdate hello riavvio stato del dispositivo hello stato segnalato Hello dispositivo utilizza hello.
  
    ![Grafico del modello di riavvio della gestione dei dispositivi][img-reboot_pattern]
* **Impostazioni di fabbrica** -app back-end hello informa dispositivo hello tramite un metodo diretto che è stata avviata una ripristino delle impostazioni predefinite.  Hello dispositivo utilizza hello segnalato factory di hello tooupdate proprietà reimpostare lo stato del dispositivo hello.
  
    ![Grafico del modello di ripristino delle impostazioni predefinite della gestione dei dispositivi][img-facreset_pattern]
* **Configurazione** -app back-end hello utilizza hello desiderato proprietà tooconfigure software in esecuzione sul dispositivo hello.  Hello dispositivo utilizza hello segnalato lo stato di configurazione tooupdate di proprietà del dispositivo hello.
  
    ![Grafico del modello di configurazione della gestione dei dispositivi][img-config_pattern]
* **Aggiornamento del firmware** -app back-end hello informa dispositivo hello tramite un metodo diretto che è stata avviata l'aggiornamento del firmware.  dispositivo Hello avvia un'immagine di processo in più passaggi toodownload hello del firmware, applicare l'immagine del firmware hello e infine riconnettersi toohello servizio IoT Hub.  Durante l'intero processo di più passaggi hello, hello dispositivo utilizza hello segnalato lo stato di avanzamento di proprietà tooupdate hello e lo stato del dispositivo hello.
  
    ![Grafico del modello di aggiornamento del firmware della gestione dei dispositivi][img-fwupdate_pattern]
* **Reporting di stato e avanzamento** -back-end di hello soluzione esegue query di un doppio dispositivo, in un set di dispositivi, tooreport stato hello e lo stato di avanzamento delle azioni in esecuzione su dispositivi hello.
  
    ![Grafico del modello di creazione di report sull'avanzamento e sullo stato della gestione dei dispositivi][img-report_progress_pattern]

## <a name="next-steps"></a>Passaggi successivi
capacità di Hello, modelli e librerie di codice forniti per la gestione dei dispositivi, l'IoT Hub consentono di applicazioni di IoT toocreate che soddisfino i requisiti di operatore IoT enterprise in ogni fase del ciclo di vita di dispositivo.

toocontinue apprendimento sulle funzionalità di gestione di dispositivi hello in IoT Hub, vedere hello [iniziare con la gestione dei dispositivi] [ lnk-get-started] esercitazione.

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md

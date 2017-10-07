---
title: aaaSecure il Internet delle cose (IoT) in Azure | Documenti Microsoft
description: " I servizi di Azure IoT (Internet delle cose) offrono una vasta gamma di funzionalità. In questo articolo consente di comprendere come toosecure soluzioni IoT in Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Informazioni generali sulla sicurezza di Internet delle cose
I servizi di Azure IoT (Internet delle cose) offrono una vasta gamma di funzionalità. Questi servizi di livello aziendale consentono di:

* Raccogliere dati dai dispositivi
* Analizzare i flussi dei dati in movimento
* Archiviare ed eseguire query su set di dati di grandi dimensioni
* Visualizzare i dati in tempo reale e cronologici
* Eseguire l'integrazione con i sistemi back-office

Queste funzionalità, Azure IoT Suite pacchetti insieme toodeliver Azure più servizi con le estensioni personalizzate come soluzioni preconfigurate. Queste soluzioni preconfigurate sono implementazioni di base di modelli di soluzione IoT comuni che consentono di tooreduce hello tempo si toodeliver soluzioni IoT. Utilizza hello IoT software development kit, è possibile personalizzare ed estendere toomeet queste soluzioni i propri requisiti. È anche possibile usare queste soluzioni come esempi o modelli durante lo sviluppo di nuove soluzioni IoT.

gruppo di Azure IoT Hello è una potente soluzione alle esigenze IoT. Tuttavia, è della massima importanza che le soluzioni IoT sono progettate tenendo presente dall'inizio hello la sicurezza. A causa di hello determinato dal numero dei dispositivi IoT, eventuali problemi di sicurezza possono diventare rapidamente un evento esteso con conseguenze significative.

toohelp è comprendere come toosecure soluzioni IoT, abbiamo hello le seguenti informazioni.

## <a name="security-architecture"></a>Architettura di sicurezza
Quando si progetta un sistema, è importante toounderstand minacce potenziali di hello toothat sistema e add difese appropriate di conseguenza, sistema di hello è progettato e architettura. È importante poiché la comprensione di come un utente malintenzionato potrebbe essere in grado di toocompromise un sistema consente di verificare che le misure di attenuazione appropriate siano soddisfatti dall'inizio di hello, toodesign hello prodotto dall'inizio hello con particolare attenzione alla sicurezza.

Informazioni sull'architettura di sicurezza IoT sono disponibili in [Architettura di sicurezza di Internet delle cose](../iot-suite/iot-security-architecture.md).

Questo articolo illustra hello seguenti argomenti:

* [La sicurezza inizia con un modello di rischio](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [Sicurezza in IoT](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Modellazione hello Azure IoT architettura di riferimento di minaccia](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Protezione da hello messa a terra
Hello IoT pone univoco sicurezza, privacy e conformità sfide toobusinesses in tutto il mondo. A differenza di tecnologia informatica tradizionale in cui questi problemi riguardano software e la relativa implementazione, IoT riguarda cosa accade quando cyber hello e mondi fisico hello convergono. Per proteggere IoT soluzioni, è necessario garantire un provisioning sicuro dei dispositivi, la connettività protetta tra questi dispositivi e cloud hello e protezione dei dati nel cloud hello durante l'elaborazione e archiviazione. A sfavore di queste funzionalità, tuttavia, giocano fattori quali dispositivi vincolati alle risorse, la distribuzione geografica delle implementazioni e l'inclusione di numerosi dispositivi in un'unica soluzione.

È possibile ottenere informazioni come protezione toohandle in queste aree leggendo [sicurezza di Internet delle cose da hello messa a terra](../iot-suite/securing-iot-ground-up.md).

Hello descritti hello seguenti argomenti:

* [Infrastruttura sicura da hello messa a terra](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure: protezione dell'infrastruttura IoT aziendale](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>Procedure consigliate
Proteggere un'infrastruttura IoT richiede una strategia di sicurezza rigorosa e approfondita. Dalla protezione dati nel cloud hello, proteggere l'integrità dei dati in transito su hello rete internet pubblica, i dispositivi provisioning toosecurely, ogni livello si basa maggiori garanzie di sicurezza di hello intera infrastruttura.

Informazioni sulle procedure consigliate per la sicurezza di Internet delle cose sono disponibili in [Procedure consigliate per la sicurezza di Internet delle cose](../iot-suite/iot-security-best-practices.md).

Hello descritti hello seguenti argomenti:

* [Produttore/integratore di hardware IoT](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [Sviluppatore di soluzioni IoT](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [Distributore di soluzioni IoT](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [Operatore di soluzioni IoT](../iot-suite/iot-security-best-practices.md#iot-solution-operator)

---
title: specifiche tecniche aaaStorSimple | Documenti Microsoft
description: "Vengono descritte le specifiche tecniche hello e le informazioni sulla conformità per i componenti hardware di StorSimple hello sugli standard normativi."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 98fa3307e2a929551c74e8b3179bb0fb61c0ab53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="technical-specifications-and-compliance-for-hello-storsimple-device"></a>Specifiche tecniche e conformità per il dispositivo StorSimple hello

## <a name="overview"></a>Panoramica

componenti hardware Hello del dispositivo StorSimple di Microsoft Azure rispettare le specifiche tecniche toohello e sugli standard normativi descritti in questo articolo. specifiche tecniche Hello descrivono capacità di archiviazione di alimentazione e raffreddamento moduli PCM (), unità disco, hello ed enclosure. le informazioni sulla conformità Hello copre elementi come standard internazionali, sicurezza e le emissioni di e i cavi.

## <a name="power-and-cooling-module-specifications"></a>Specifiche del modulo di alimentazione e raffreddamento

dispositivo StorSimple Hello ha due 100-240 V doppia ventola e conformi a SBB raffreddamento moduli PCM (Power). Fornisce una configurazione di alimentazione ridondante. Caso di guasto di un PCM, dispositivo hello proseguirà normalmente toooperate in hello viene sostituito l'altro PCM finché hello non modulo.

Hello enclosure EBOD Usa un PCM a 580 W ed enclosure principale ne usa un PCM a 764 W. Hello nelle tabelle seguenti sono specifiche tecniche hello elenco associate hello PCM.

| Specifiche | PCM 580 W (EBOD) | PCM 764 W (principale) |
| --- | --- | --- |
| Potenza massima in uscita |580 W |764 |
| Frequenza |50/60 Hz |50/60 Hz |
| Selezione intervallo di voltaggio |Intervallo automatico: 90 – 264 V CA, 47/63 Hz |Intervallo automatico: 90 - 264 V CA, 47/63 Hz |
| Afflusso di corrente massimo |20 A |20 A |
| Correzione del fattore di potenza |Voltaggio di ingresso nominale > 95% |Voltaggio di ingresso nominale > 95% |
| Armoniche |Conforme allo standard N61000-3-2 |Conforme allo standard N61000-3-2 |
| Output |Tensione di standby 5V @ 2.0 A |Tensione di standby 5V @ 2.7 A |
| +5V @ 42 A |+5V @ 40 A | |
| +12V @ 38 A |+12V @ 38 A | |
| Collegabile "hot" |Sì |Sì |
| LED e commutatori |Commutatore CA ACCESO/SPENTO e quattro indicatori LED di stato |Commutatore CA ACCESO/SPENTO e sei indicatori LED di stato |
| Raffreddamento chassis |Ventole di raffreddamento assiale con controllo di velocità della ventola variabile |Ventole di raffreddamento assiale con controllo di velocità della ventola variabile |

## <a name="power-consumption-statistics"></a>Statistiche sul consumo energetico

Hello nella tabella seguente elenca i dati di utilizzo tipico power hello (valori effettivi possono variare da hello pubblicato) per hello diversi modelli del dispositivo StorSimple.

| Condizioni | CA 240 V | CA 240 V | CA 240 V | CA 110 V | CA 110 V | CA 110 V |
| --- | --- | --- | --- | --- | --- | --- |
|  Ventole lente, unità inattive |1,45 A |0,31 kW |1057,76 BTU/h |3,19 A |0,34 kW |1160,13 BTU/h |
|  Ventole lente, accesso alle unità |1,54 A |0,33 kW |1126,01 BTU/h |3,27 A |0,36 kW |1228,37 BTU/h |
|  Ventole veloci, unità inattive, due PSU alimentati |2,14 A |0,49 kW |1671,95 BTU/h |4,99 A |0,54 kW |1842,56 BTU/h |
|  Ventole veloci, unità inattive, un PSU alimentato uno inattivo |2,05 A |0,48 kW |1637,83 BTU/h |4,58 A |0,50 kW |1706,07 BTU/h |
|  Ventole veloci, accesso alle unità, due PSU alimentati |2,26 A |0,51 kW |1740,19 BTU/h |4,95 A |0,54 kW |1842,56 BTU/h |
|  Ventole veloci, accesso alle unità, un PSU alimentato uno inattivo |2,14 A |0,49 kW |1671,95 BTU/h |4,81 A |0,53 kW |1808,44 BTU/h |

## <a name="disk-drive-specifications"></a>Specifiche unità disco

Il dispositivo StorSimple supporta backup too12 le unità disco SAS Serial Attached SCSI () da 3,5 pollici form factor. unità effettive Hello può essere una combinazione di unità SSD (unità SSD) o dischi rigidi (HDD), a seconda della configurazione del prodotto hello. 12 alloggiamenti per unità disco Hello si trovano in una configurazione 3 x 4 davanti enclosure hello. Hello enclosure EBOD consente l'archiviazione aggiuntiva per 12 unità disco. Si tratta sempre di HDD.

## <a name="storage-specifications"></a>Specifiche di archiviazione

dispositivi StorSimple Hello con una combinazione di dischi rigidi e unità SSD per entrambi hello 8100 e 8600. capacità utilizzabile totale Hello per hello 8100 e 8600 sono circa 15 TB e 38 TB. Hello nella tabella seguente illustra i dettagli di hello delle unità SSD e HDD capacità del cloud nel contesto di hello di hello della capacità della soluzione StorSimple.

| Modello del dispositivo / Capacità | 8100 | 8600 |
| --- | --- | --- |
| Numero di unità disco rigido |8 |19 |
| Numero di unità SSD |4 |5 |
| Capacità della singola unità disco rigido |4 TB |4 TB |
| Capacità della singola unità SSD |400 GB |800 GB |
| Capacità di riserva |4 TB |4 TB |
| Capacità utilizzabile dell'unità disco rigido |14 TB |36 TB |
| Capacità utilizzabile dell'unità SSD |800 GB |2 TB |
| Capacità utilizzabile totale* |~ 15 TB |~ 38 TB |
| Capacità massima della soluzione (incluso il cloud) |200 TB |500 TB |

<sup>* </sup>- *capacità utilizzabile totale Hello include la capacità di hello disponibile per i dati, metadati e i buffer.*

## <a name="enclosure-dimensions-and-weight-specifications"></a>Specifiche su peso e dimensioni dello chassis

Hello seguente elenco di tabelle hello varie specifiche di enclosure per dimensioni e peso.

### <a name="enclosure-dimensions"></a>Dimensioni dello chassis

Hello nella tabella seguente elenca le dimensioni di hello dell'enclosure hello in millimetri e pollici.

| Chassis | Millimetri | Pollici |
| --- | --- | --- |
| Altezza: |87,9 |3,46 |
| Larghezza tra la flangia di montaggio |483 |19,02 |
| Larghezza tra il corpo dello chassis |443 |17,44 |
| Profondità dalla tooextremity flangia di montaggio del corpo dell'enclosure |577 |22,72 |
| Profondità da operazioni pannello toofurthest estremità dell'enclosure |630,5 |24,82 |
| Profondità dalla flangia toofurthest estremità dell'enclosure di montaggio |603 |23,74 |

### <a name="enclosure-weight"></a>Peso chassis

A seconda della configurazione di hello, un'enclosure principale completamente carico può pesare da 21 too33 kg e richiede due persone toohandle è.

| Chassis | Peso |
| --- | --- |
| Peso massimo (dipende dalla configurazione hello) |Da 30 a 33 kg |
| Vuoto (nessuna unità montata) |Da 21 a 23 kg |

## <a name="enclosure-environment-specifications"></a>Specifiche ambientali dello chassis

In questa sezione elenca l'ambiente di enclosure di hello specifiche toohello correlati. temperatura Hello, umidità, altitudine, resistenza agli urti, resistenza alle vibrazioni, orientamento, sicurezza e compatibilità elettromagnetiche (EMC) sono inclusi in questa categoria.

### <a name="temperature-and-humidity"></a>Temperatura e umidità

| Chassis | Intervallo di temperatura ambientale | Umidità relativa all'ambiente | Bulbo umido massimo |
| --- | --- | --- | --- |
| Operativo |Da 5°C a 35°C (da 41°F a 95°F) |Dal 20% all'80% senza condensa |28°C (82°F) |
| Non operativo |Da -40° a 70°C (da 40°F a 158°F) |Dal 5% al 100% senza condensa |29°C (84°F) |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>Flusso d'aria, altitudine, scosse, vibrazione, orientamento, sicurezza ed EMC

| Chassis | Specifiche operative |
| --- | --- |
| Flusso d'aria |Flusso d'aria è anteriore toorear. Il sistema deve essere utilizzato con un'installazione a bassa pressione e scarico posteriore. La pressione posteriore creata dalle porte del rack e da ostacoli non deve superare i 5 Pascal (colonna d'acqua da 0,5 mm). |
| Altitudine, operativa |da-30 metri too3045 metri (too10 piedi-100, piedi 000) con temperatura massima deallocare classificati da 5 ° C sopra piedi 7000. |
| Altitudine, non operativa |da-305 metri too12, 192 metri (too40 piedi-1.000, 000 piedi) |
| Scossa, operativo |5 g 10 ms ½ sinusoidali |
| Scossa, non operativo |30 g 10 ms ½ sinusoidali |
| Vibrazione, operativa |0,21g RMS 5-500 Hz casuali |
| Vibrazione, non operativa |1,04 g RMS 2-200 Hz casuali |
| Vibrazione, trasferimento |3 g 2-200 Hz sinusoidali |
| Orientamento e montaggio |Montaggio rack da 19" (2 unità EIA) |
| Guide rack |rack di profondità almeno 700 mm (31.50 pollici) toofit conformi a IEC 297 |
| Sicurezza e approvazioni |CE e UL EN 61000-3, IEC 61000-3, UL 61000-3 |
| EMC |EN55022 (CISPR - A), FCC A |

## <a name="international-standards-compliance"></a>Conformità agli standard internazionali

Il dispositivo StorSimple di Microsoft Azure è conforme ai seguenti standard internazionali hello:  

* CE - EN 60950 - 1
* CB report tooIEC 60950-1
* UL e cUL tooUL 60950-1

## <a name="safety-compliance"></a>Conformità di sicurezza

Il dispositivo di Microsoft Azure StorSimple soddisfa hello standard di sicurezza seguenti:

* Approvazione del tipo di prodotto di sistema: UL, cUL, CE
* Conformità di sicurezza: UL 60950, IEC 60950, EN 60950

## <a name="emc-compliance"></a>Conformità EMC

Il dispositivo di Microsoft Azure StorSimple soddisfa hello seguenti classificazioni EMC.

### <a name="emissions"></a>Emissioni

dispositivo Hello è conforme a EMC per i livelli di emissioni Radiate e condotte.

* Livelli dei limiti delle emissioni effettuate: CFR 47 Part 15B Class A EN55022 Class A CISPR Class A
* Livelli dei limiti delle emissioni irradiate: CFR 47 Part 15B Class A EN55022 Class A CISPR Class A

### <a name="harmonics-and-flicker"></a>Armoniche e sfarfallio

Hello dispositivo è conforme a EN61000-3-2/3.

### <a name="immunity-limit-levels"></a>Livelli del limite di immunità

dispositivo Hello è conforme a EN55024.

## <a name="ac-power-cord-compliance"></a>Conformità del cavo di alimentazione CA

plug Hello e hello completo cavo di alimentazione deve soddisfare gli standard di hello appropriati per hello paese in cui hello viene usato il dispositivo e devono disporre di omologazioni di sicurezza considerate accettabili in tale paese. nelle tabelle seguenti Hello sono standard di elenco per hello USA ed Europa.

### <a name="ac-power-cords---usa-must-be-nrtl-listed"></a>Cavi di alimentazione CA - Stati Uniti (devono essere elencati NRTL)

| Componente | Specifiche |
| --- | --- |
| Tipo di cavo |SV o SVT, 18 AWG minimo, 3 conduttori, lunghezza massima pari a 2,0 metri |
| Spina |Spina NEMA 5-15P con messa a terra classificata 120 V, 10 A oppure IEC 320 C14, 250 V, 10 A |
| Presa elettrica |IEC 320 C-13, 250 V, 10 A |

### <a name="ac-power-cords---europe"></a>Cavi di alimentazione CA - Europa

| Componente | Specifiche |
| --- | --- |
| Tipo di cavo |Armonizzate, H05-VVF-3G1.0 |
| Presa elettrica |IEC 320 C-13, 250 V, 10 A |

## <a name="supported-network-cables"></a>Cavi di rete supportati

Per le interfacce di rete hello 10 GbE, DATA 2 e DATA 3, vedere toohello [elenco dei moduli e i cavi di rete supportati](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).

## <a name="next-steps"></a>Passaggi successivi

Si è ora pronto toodeploy un dispositivo StorSimple nel Data Center. Per altre informazioni, vedere [Distribuire un dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md).


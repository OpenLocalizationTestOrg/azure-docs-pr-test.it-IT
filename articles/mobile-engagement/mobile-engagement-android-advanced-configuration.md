---
title: configurazione aaaAdvanced per Azure Mobile Engagement SDK Android
description: Vengono descritte le opzioni di configurazione inclusi manifesto Android con Azure Mobile Engagement SDK Android hello avanzate hello
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Configurazione avanzata di Android SDK per Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Windows universale](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

Questa procedura viene descritto come tooconfigure varie opzioni di configurazione per le app Android di Azure Mobile Engagement.

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>Requisiti di autorizzazione
Alcune opzioni richiedono autorizzazioni specifiche, ognuno dei quali sono elencati di seguito per riferimento e in linea nella funzionalità specifiche di hello. Aggiungere questi toohello autorizzazioni AndroidManifest.xml del progetto, immediatamente prima o dopo hello `<application>` tag.

codice di autorizzazione Hello deve toolook hello seguente, in cui si compila le autorizzazioni appropriate hello dalla tabella hello che segue.

    <uses-permission android:name="android.permission.[specific permission]"/>


| Autorizzazione | Quando si usa |
| --- | --- |
| INTERNET |Obbligatorio. Per report di base |
| ACCESS_NETWORK_STATE |Obbligatorio. Per report di base |
| RECEIVE_BOOT_COMPLETED |Obbligatorio. tooshow Center notifiche hello dopo il riavvio del dispositivo |
| WAKE_LOCK |Consigliato. Abilita la raccolta dei dati quando si usa il WiFi o quando lo schermo è spento |
| VIBRATE |Facoltativo. Abilita la vibrazione alla ricezione delle notifiche |
| DOWNLOAD_WITHOUT_NOTIFICATION |Facoltativo. Abilita la notifica generale di Android |
| WRITE_EXTERNAL_STORAGE |Facoltativo. Abilita la notifica generale di Android |
| ACCESS_COARSE_LOCATION |Facoltativo. Abilita la segnalazione della posizione in tempo reale |
| ACCESS_FINE_LOCATION |Facoltativo. Abilita la segnalazione della posizione basata su GPS |

A partire da Android M, [alcune autorizzazioni vengono gestite in fase di esecuzione](mobile-engagement-android-location-reporting.md#android-m-permissions).

Se si sta già utilizzando ``ACCESS_FINE_LOCATION``, è necessario tooalso utilizzare ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Opzioni di configurazione del file manifesto Android
### <a name="crash-report"></a>Segnalazione di arresto anomalo 
segnalazioni di arresti anomali toodisable, aggiungere il codice tra hello `<application>` e `</application>` tag:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Soglia del burst
Per impostazione predefinita, i report del servizio di Engagement hello registra in tempo reale. Se la relazione dei log applicazioni variano frequentemente, è meglio toobuffer hello registri e tooreport usarle in una sola volta in volta regolare base (denominata "potenziamento in modalità"). toodo in tal caso, aggiungere il codice tra hello `<application>` e `</application>` tag:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Modalità burst leggermente aumenta la durata della batteria hello ma ha un impatto sulle hello Engagement Monitor: durata di tutte le sessioni e i processi vengono arrotondati toohello burst soglia (in questo modo, le sessioni e i processi è inferiore a soglia burst hello potrebbe non essere visibile). La soglia di burst non dovrebbe essere maggiore di 30000 (30 secondi).

### <a name="session-timeout"></a>Timeout della sessione
 È possibile terminare un'attività premendo hello **Home** o **nuovamente** chiave telefonicamente impostazione hello inattivo o per passare a un'altra applicazione. Per impostazione predefinita, una sessione viene terminata dieci secondi dopo la fine di hello del relativo ultima attività. Ciò consente di evitare una divisione di sessione, ogni utente hello in fase di chiusura e restituisce toohello applicazione rapidamente, che possono verificarsi quando l'utente hello preleva un'immagine, verifica una notifica e così via. È opportuno toomodify questo parametro. toodo in tal caso, aggiungere il codice tra hello `<application>` e `</application>` tag:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Disabilitare la segnalazione di log
### <a name="using-a-method-call"></a>Uso di una chiamata del metodo
Se si desidera toostop Engagement l'invio di log, è possibile chiamare:

    EngagementAgent.getInstance(context).setEnabled(false);

Questa chiamata è persistente: usa un file di preferenze condivise.

Se Engagement è attivo quando si chiama questa funzione, potrebbe richiedere un minuto per hello servizio toostop. Tuttavia, non verrà avviato servizio hello hello tutti successivo avvio di un'applicazione hello.

È possibile abilitare nuovamente reporting chiamando hello stessa funzione con log `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integrazione nella propria classe `PreferenceActivity`
Invece di chiamare questa funzione, è anche possibile integrare questa impostazione direttamente nella classe `PreferenceActivity` esistente.

È possibile configurare le preferenze di file (con modalità desiderata di hello) toouse di Engagement in hello `AndroidManifest.xml` file con `application meta-data`:

* Hello `engagement:agent:settings:name` chiave è utilizzata toodefine hello nome del file di preferenze condivise hello.
* Hello `engagement:agent:settings:mode` chiave è la modalità di hello toodefine utilizzate del file di preferenze condivise hello. Utilizzare hello stessa modalità come il `PreferenceActivity`. modalità Hello deve essere passata come un numero: se si utilizza una combinazione di flag costante nel codice, controllare il valore totale di hello.

Engagement sempre utilizza hello `engagement:key` booleano chiave all'interno di file di preferenze hello per la gestione di questa impostazione.

Hello in seguito ad esempio `AndroidManifest.xml` Mostra hello valori predefiniti:

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

È quindi possibile aggiungere un `CheckBoxPreference` nel layout delle preferenze come segue quello hello:

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />

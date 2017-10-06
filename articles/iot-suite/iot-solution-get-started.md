---
title: 'Esempio di IoT di Azure MyDriving: Avvio rapido | Documentazione Microsoft'
description: "Introduzione a un'applicazione che è una dimostrazione completa di come tooarchitect un sistema IoT utilizzando Microsoft Azure, tra cui flusso Analitica, Machine Learning e hub eventi."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a>Sistema IoT MyDriving: Avvio rapido
MyDriving è un sistema che illustra hello progettazione e implementazione di una tipica [Internet of Things](iot-suite-overview.md) soluzione (IoT) che raccoglie i dati di telemetria dai dispositivi, elabora i dati nel cloud hello e si applica l'apprendimento tooprovide una risposta adattiva. dimostrazione di Hello registra i dati sulle visite Auto, utilizzando i dati dal telefono cellulare e un adattatore che raccoglie informazioni dal sistema di controllo dell'automobile. Usa questi commenti e suggerimenti di dati tooprovide al proprio approccio Guida gli utenti tooother di confronto.

Hello reale MyDriving mira tooget per iniziare a creare la propria soluzione IoT. Ma prima di esso, possibile iniziare a usarlo con hello MyDriving app stessa, come un membro del team utente test. Ciò offre un'esperienza di app hello e sistema hello dietro come un consumer, prima di addentrarsi nell'architettura di hello. Introduce anche tooHockeyApp, un modo sporadico della gestione delle distribuzioni di alfa e beta hello degli utenti tootest app.

## <a name="use-hello-mobile-experience"></a>Utilizzare l'esperienza per dispositivi mobili hello
Se si dispone di un dispositivo Android, iOS o Windows 10, è possibile utilizzare app MyDriving hello.

### <a name="android-and-windows-10-mobile-installation"></a>Installazione di Android e Windows 10 Mobile
Nel dispositivo:

1. Consentire le app di sviluppo:
   
   * Android: in **Impostazioni**,  > **Sicurezza**, consentire le app da **Origini sconosciute**.
   * Windows 10: in **Impostazioni** > , **Aggiornamenti** > **Per gli sviluppatori**, impostare **Modalità sviluppatore**.
2. Unirsi al team di test beta mediante l'iscrizione o l'accesso a [HockeyApp](https://rink.hockeyapp.net). HockeyApp rende facile toodistribute prime versioni di utenti tootest app.
   
   Se si usa Windows 10, è possibile utilizzare browser Edge hello.
   
   Se fosse un partecipante di compilazione 2016, accedi hello stesso posta elettronica dell'account Microsoft che è registrato per la conferenza hello, utilizzando uno dei pulsanti Microsoft hello. L'iscrizione a HockeyApp è già stata eseguita.
   
   ![Schermata di accesso di HockeyApp](./media/iot-solution-get-started/image1.png)
3. Scaricare e installare l'applicazione hello da qui:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Sono disponibili due elementi. Installare il certificato di hello in **persone attendibili**. Installare quindi l'applicazione hello.

*Eventuali problemi di avvio applicazione hello in Windows 10 Mobile?* Il telefono potrebbe non essere aggiornato alla versione più recente. Assicurarsi di aver ottenuto gli aggiornamenti più recenti di hello, o installare:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>Installazione di iOS
Se si è partecipato compilazione 2016, scaricare l'applicazione hello come membro del team di test in HockeyApp:

1. Nel dispositivo iOS accedere troppo[HockeyApp](https://rink.hockeyapp.net).
   Utilizzare uno dei pulsanti di accesso Microsoft hello e Accedi con hello stesso posta elettronica dell'account Microsoft che è stato registrato con conferenza hello. (Non usare i campi di posta elettronica e password hello).
   
   ![Schermata di accesso di HockeyApp](./media/iot-solution-get-started/image1.png)
2. Nel dashboard HockeyApp hello, selezionare MyDriving e scaricarlo.
3. Autorizzare versione beta di hello da HockeyApp:
   
   a. Andare troppo**impostazioni** > **generale** > **profili e la gestione dei dispositivi.**
   
   b. Trust hello **Bit stadio GmbH** certificato.

Se non viene risolto compilazione 2016, è possibile compilare e distribuire app hello manualmente:

1. Scaricare codice hello [da GitHub].
2. Compilare e distribuire l'app [con Xamarin].

Informazioni su altre in hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Ottenere un adattatore OBD (facoltativo)
Questo aspetto è parte di hello che rende questa un reale sistema Internet of Things! È possibile utilizzare l'applicazione hello senza uno, ma è più divertente reali hello e non sono costosi.

Sistemi diagnostici (OBD) sono una funzionalità hello di un'automobile che hello garage utilizza tootune backup Auto e diagnosticare rumori dispari e spie. A meno che la macchina è di grande antichità, sono disponibili un socket in un punto qualsiasi in cabine hello, in genere dietro flap in dashboard hello. Con connettore di destra hello, è possibile ottenere le metriche delle prestazioni del motore di hello e apportare alcune modifiche. È possibile acquistare un connettore OBD economici da posizioni di solito hello. Si connette tramite Bluetooth o Wi-Fi app tooan sul telefono.

In questo caso, verrà tooconnect cloud toohello Auto. connessione diretta di Hello da hello OBD è tooyour telefono, ma l'app funziona come un relè. Dati di telemetria dell'automobile viene inviato retta toohello MyDriving IoT hub, in cui è elaborato toolog i viaggi e valutare il proprio stile di Guida.

un dispositivo OBD tooconnect:

1. Verificare che il veicolo abbia una presa OBD.
2. Ottenere un adattatore OBD:
   
   * Se si usa un telefono Android o Windows, è necessario un adattatore OBD II abilitato per Bluetooth. In questo caso, è stato usato [BAFX Products 34t5 Bluetooth OBDII Scan Tool].
   * Se si usa un telefono iOS, è necessario un adattatore OBD abilitato per Wi-Fi. In questo caso, è stato usato [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].
3. Seguire le istruzioni di hello forniti con il tooconnect adapter OBD è tooyour phone. Tenere presente hello segue:
   
   * Una scheda Bluetooth deve essere abbinata a telefono hello hello **impostazioni** pagina.
   * Un adapter Wi-Fi deve avere un indirizzo in 192.168.xxx.xxx intervallo hello.
4. Se si hanno diverse automobili, è possibile usare un adattatore distinto per ogni macchina (per un massimo di 3).

Se non si dispone di un adapter OBD, hello app invierà ancora percorso e dati sulla velocità dal nuovo toohello di ricevitore GPS del telefono hello terminano e verranno richiesto se si desidera un OBD toosimulate.

È possibile trovare informazioni sull'utilizzo di dati dalla scheda OBD hello app hello e sulle opzioni per creare il proprio dispositivo OBD nella sezione 2.1, "Dispositivi IoT" in hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Utilizzare l'applicazione hello
Avviare l'applicazione hello. È presente un iniziale toowalk Guida introduttiva illustra il funzionamento.

### <a name="track-your-trips"></a>Tenere traccia dei viaggi.
Toccare hello pulsante record (big cerchio rosso in basso hello hello) toostart un andata e ritorno e nuovamente tooend.

![Illustrazione del pulsante di hello record di rilevamento di andata e ritorno](./media/iot-solution-get-started/image2.png)

Ogni volta che si avvia un andata e ritorno, se è presente alcun dispositivo OBD, verrà chiesto se si desidera che il simulatore di hello toouse.

Alla fine hello un andata e ritorno, toccare hello stop e sarà visualizzato un riepilogo.

![Esempio di riepilogo di un viaggio](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Esaminare i viaggi
![Esempio di una viaggio precedente](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Esaminare il profilo
![Esempio di un profilo dello stile di guida](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Inviateci i commenti e suggerimenti sul test
Perché abbiamo creato MyDriving toohelp iniziare subito a usare i propri sistemi IoT, si desidera certamente toohear da parte dell'utente, sulle modalità di funzionamento. Indicare se:

* Si sono riscontrate difficoltà o problematiche.
* C'è un punto di estensione che potrebbe renderlo scenario tooyour più adatto.
* Trovare un tooaccomplish modo più efficiente determinate esigenze.
* Si hanno altri suggerimenti per migliorare MyDriving o questa documentazione.

All'interno di hello MyDriving app, è possibile utilizzare il meccanismo di feedback hello incorporato HockeyApp: in iOS e Android, è sufficiente specificare il telefono un agitazione oppure utilizzare hello **Feedback** comando di menu. In questo modo viene applicato automaticamente uno screenshot in modo che il destinatario sappia di cosa si sta parlando. E se sono presenti eventuali ingrato arresti anomali del sistema, HockeyApp raccoglie tootell i registri di arresto anomalo del sistema hello ci su di essi. È inoltre possibile assegnare i commenti e suggerimenti tramite hello [portale HockeyApp].

È anche possibile registrare un [problema in GitHub] o lasciare un commento qui di seguito (versione en-us).

Saremo lieti toohearing da parte dell'utente.

## <a name="next-steps"></a>Passaggi successivi
* Esplorare hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs) toounderstand come è stato progettato e costruito hello intero sistema MyDriving.
* [Creare e distribuire un sistema personalizzato](iot-solution-build-system.md) con gli script di Azure Resource Manager. Hello [Guida di riferimento MyDriving](http://aka.ms/mydrivingdocs) anche in modo semplificato le aree in cui ti hello la maggior parte delle personalizzazioni.

[da GitHub]: https://github.com/Azure-Samples/MyDriving
[con Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[portale HockeyApp]: https://rink.hockeyapp.org
[problema in GitHub]: https://github.com/Azure-Samples/MyDriving/issues

---
title: opzioni di Azure Mobile Engagement SDK Android reporting aaaAdvanced
description: Viene descritto come toodo avanzate reporting toocapture analitica per Azure Mobile Engagement SDK Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Segnalazione avanzata con Engagement in Android
> [!div class="op_single_selector"]
> * [Windows universale](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Questo argomento descrive scenari di segnalazione aggiuntivi nell'applicazione Android. È possibile applicare queste app toohello opzioni creato in hello [Introduzione](mobile-engagement-android-get-started.md) esercitazione.

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

esercitazione Hello è completata è stata volutamente semplice e diretto, ma vi sono le opzioni avanzate è possibile scegliere.

## <a name="modifying-your-activity-classes"></a>Modifica delle classi `Activity`
In hello [esercitazione introduttiva](mobile-engagement-android-get-started.md), tutti toodo era stata toomake il `*Activity` sottoclassi ereditano hello corrispondente `Engagement*Activity` classi. Se, ad esempio, l'attività legacy estende `ListActivity`, si fa in modo di estendere `EngagementListActivity`.

> [!IMPORTANT]
> Quando si utilizza `EngagementListActivity` o `EngagementExpandableListActivity`, assicurarsi che tutte le chiamate troppo`requestWindowFeature(...);` diventa troppo prima chiamata hello`super.onCreate(...);`, in caso contrario si verifica un arresto anomalo.
> 
> 

È possibile trovare queste classi in hello `src` cartella e possono copiare nel progetto. classi di Hello sono anche in hello **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Metodo alternativo: chiamare manualmente `startActivity()` e `endActivity()`
Se non è possibile o non si desidera toooverload il `Activity` classi, è possibile invece iniziare e terminare le attività chiamando hello `EngagementAgent`del diretta dei metodi.

> [!IMPORTANT]
> Hello, Android SDK non chiama mai hello `endActivity()` (metodo), anche quando viene chiusa l'applicazione hello (in Android, non chiudere le applicazioni sono mai). È pertanto *elevata* consigliato hello toocall `startActivity()` metodo hello `onResume` callback di *tutti* le attività e hello `endActivity()` metodo hello `onPause()` callback di *tutti* delle attività. Si tratta di hello solo modo toobe assicurarsi che le sessioni non vengano comunicate. Se una sessione viene perso, hello servizio Engagement non disconnette mai dal back-end Engagement hello (dal momento che il servizio di hello rimane connesso, purché una sessione è in sospeso).
> 
> 

Di seguito è fornito un esempio:

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

Questo esempio è simile toohello `EngagementActivity` classe e le sue varianti, il cui codice sorgente viene fornito in hello `src` cartella.

## <a name="using-applicationoncreate"></a>Uso di Application.onCreate()
Inserire nel codice `Application.onCreate()` e in un'altra applicazione callback viene eseguito per tutti i processi dell'applicazione, incluso hello Engagement servizio. Potrebbe disporre gli effetti collaterali indesiderati, come le allocazioni di memoria non necessari e i thread nel processo di Engagement hello, o duplicato broadcast ricevitori o servizi.

Se esegue l'override `Application.onCreate()`, è consigliabile aggiungere hello seguente frammento di codice all'inizio di hello del `Application.onCreate()` funzione:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

È possibile eseguire hello stessa operazione per `Application.onTerminate()`, `Application.onLowMemory()`, e `Application.onConfigurationChanged(...)`.

È anche possibile estendere `EngagementApplication` anziché estensione `Application`: hello callback `Application.onCreate()` hello controllo processo e chiama `Application.onApplicationProcessCreate()` solo se il processo corrente hello è non hello uno hello Engagement servizio di hosting, hello stesse regole valide per Hello altre richiamate.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Tag nel file AndroidManifest.xml hello
Nel tag di servizio hello nel file AndroidManifest.xml hello, hello `android:label` attributo consente un nome hello toochoose di hello servizio Engagement così come viene visualizzato agli utenti di tooend nella schermata di "Servizi in esecuzione" hello del telefono. È consigliabile impostare questo attributo troppo`"<Your application name>Service"` (ad esempio, `"AcmeFunGameService"`).

Se si specifica hello `android:process` attributo assicura che hello viene eseguito il servizio Engagement in un processo (Engagement in esecuzione nella stessa procedura adottata l'applicazione esegue il thread principale o dell'interfaccia utente potenzialmente tempi hello).

## <a name="building-with-proguard"></a>Compilazione con ProGuard
Se si compila il pacchetto dell'applicazione con ProGuard, è necessario tookeep alcune classi. È possibile utilizzare hello seguente frammento di configurazione:

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }

---
title: le procedure di aggiornamento di Phone Silverlight SDK aaaWindows
description: Procedure di aggiornamento di Azure Mobile Engagement SDK per Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Procedure di aggiornamento dell'SDK per Windows Phone Silverlight
Se è già stata integrata una versione precedente di Windows SDK nell'applicazione, è necessario hello tooconsider seguenti punti quando si aggiorna hello SDK.

È possibile toofollow varie procedure se sono saltate diverse versioni di hello SDK. Ad esempio se si esegue la migrazione da 0.10.1 too0.11.0 è toofirst seguire hello "da 0.9.0 too0.10.1" routine quindi hello "da 0.10.1 too0.11.0" stored procedure.

## <a name="from-200-too330"></a>Da 2.0.0 too3.3.0
### <a name="test-logs"></a>Log di test
Registri della console prodotti da hello SDK ora possono essere attivato/disattivato/filtrato. toocustomize, questa proprietà hello aggiornamento `EngagementAgent.Instance.TestLogEnabled` tooone del valore di hello disponibile hello `EngagementTestLogLevel` enumerazione, ad esempio:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>Da 1.1.1 too2.0.0
Hello seguenti viene descritto come toomigrate un'integrazione SDK da hello Capptain servizio offerto da Capptain SAS in un'app con Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain e Mobile Engagement non sono hello stessi servizi e procedura di hello indicata di seguito solo evidenziata come toomigrate hello app client. Migrazione hello SDK nell'applicazione hello verrà non la migrazione dei dati dai server di hello Capptain server toohello Mobile Engagement
> 
> 

Se si esegue la migrazione da una versione precedente, consultare prima hello Capptain sito web toomigrate too1.1.1 quindi applicare hello procedura

### <a name="nuget-package"></a>Pacchetto NuGet
Sostituire **Capptain.WindowsPhone** con il pacchetto NuGet **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Applicazione di Mobile Engagement
Hello SDK viene utilizzato il termine hello `Engagement`. È necessario tooupdate toomatch il progetto questa modifica.

È necessario toouninstall il pacchetto nuget Capptain corrente. Si consideri che verranno rimosse tutte le modifiche nella cartella Risorse di Capptain. Se si desidera tookeep tali file, creare una copia di essi.

Successivamente, installare il pacchetto di hello nuovo impegno di Microsoft Azure nuget nel progetto. È possibile trovarlo direttamente sul sito Web di [NuGet](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Sostituisce questa azione, tutti i file di risorse utilizzate da Engagement e hello nuova DLL Engagement tooyour aggiunge i riferimenti al progetto.

Hai tooclean riferimenti del progetto eliminando i riferimenti DLL Capptain. Se non si apporta questa, versione di hello di Capptain è in conflitto e si verificheranno gli errori.

Se è stato personalizzato Capptain risorse, copiare il contenuto del file precedente e incollarli in nuovi file di Engagement hello. Si noti che i file xaml sia cs toobe aggiornato.

Dopo avere completato questi passaggi è sufficiente tooreplace precedente Capptain i riferimenti basati sui nuovi riferimenti di Engagement hello.

1. Tutti gli spazi dei nomi di Capptain avere toobe aggiornato.
   
    Prima della migrazione:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Dopo la migrazione:
   
        using Microsoft.Azure.Engagement;
2. Tutte le classi Capptain che contengono "Capptain" devono contenere "Engagement".
   
    Prima della migrazione:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Dopo la migrazione:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Per i file xaml cambiano anche attributi e spazio dei nomi di Capptain.
   
    Prima della migrazione:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Dopo la migrazione:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Per altre risorse come le immagini Capptain di hello, si noti che sono anche stati rinominati toouse "Engagement".

### <a name="application-id--sdk-key"></a>ID applicazione / chiave SDK
Engagement utilizza una stringa di connessione. Non si dispone toospecify un ID applicazione e una chiave SDK con Engagement Mobile, è sufficiente toospecify una stringa di connessione. È possibile configurarla nel file EngagementConfiguration.

configurazione di Engagement Hello può essere impostate nel `Resources\EngagementConfiguration.xml` file del progetto.

Modificare questo toospecify file:

* La stringa di connessione dell'applicazione tra i tag `<connectionString>` and `<\connectionString>`.

Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

stringa di connessione Hello per l'applicazione viene visualizzato nel portale di Azure classico hello.

### <a name="items-name-change"></a>Modifica del nome di elementi
Tutti gli elementi denominati *capptain* sono stati rinominati in *engagement*. Analogamente, per *Capptain* troppo*Engagement*.

Esempi di elementi di Capptain di uso comune:

* CapptainConfiguration è diventato EngagementConfiguration
* CapptainAgent è diventato EngagementAgent
* CapptainReach è diventato EngagementReach
* CapptainHttpConfig è diventato EngagementHttpConfig
* GetCapptainPageName è diventato GetEngagementPageName

Si noti la ridenominazione influisce anche sui metodi sottoposti a override.


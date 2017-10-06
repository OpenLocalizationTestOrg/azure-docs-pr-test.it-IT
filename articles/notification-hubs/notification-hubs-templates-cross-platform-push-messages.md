---
title: aaaTemplates
description: In questo argomento vengono illustrati i modelli per Hub di notifica di Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>Modelli
## <a name="overview"></a>Panoramica
I modelli consentono un client applicazione toospecify hello formato esatto delle notifiche di hello che tooreceive desiderati. Utilizzo di modelli, un'app consentono di realizzare diversi diversi vantaggi, tra cui hello seguenti:

* Un back-end indipendente dalla piattaforma
* Notifiche personalizzate
* Indipendenza dalla versione del client
* Localizzazione semplice

In questa sezione vengono forniti due esempi approfonditi come le notifiche indipendente dalla piattaforma toosend modelli toouse tutti i dispositivi di destinazione su piattaforme e toopersonalize broadcast dispositivo tooeach di notifica.

## <a name="using-templates-cross-platform"></a>Utilizzo di modelli multipiattaforma
le notifiche push in modo standard toosend Hello è toosend, per ogni notifica che viene inviato, toobe un payload specifico tooplatform notifica di servizi (WNS, APN). Ad esempio, un avviso tooAPNS, toosend payload hello è un oggetto Json di hello seguente formato:

    {"aps": {"alert" : "Hello!" }}

toosend un messaggio di tipo avviso popup simile in un'applicazione Windows Store, payload XML hello è come segue:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

È possibile creare payload simili per MPNS (Windows Phone) e piattaforme GCM (Android).

Questo requisito forza hello app back-end tooproduce diversi payload per ogni piattaforma e rende effettivamente responsabile della parte del livello di presentazione hello di hello app back-end hello. Alcuni dei problemi riguardano la localizzazione e i layout grafici (soprattutto per applicazioni di Windows Store che comprendono notifiche per vari tipi di riquadri).

funzionalità del modello di hub di notifica Hello consente un app toocreate speciali registrazioni client, le registrazioni del modello, che includono inoltre toohello set di tag, un modello di chiamata. funzionalità del modello di hub di notifica Hello consente dispositivi tooassociate app client con i modelli se si lavora con installazioni (scelta consigliate) o registrazioni. Dato hello precedenti esempi di payload, hello solo le informazioni indipendente dalla piattaforma sono hello effettivo messaggio di avviso (Hello!). Un modello è un set di istruzioni per l'Hub di notifica di hello in modalità tooformat un indipendente dalla piattaforma dei messaggi per la registrazione di hello di app client specifico. In hello sopra riportato, messaggio indipendente dalla piattaforma di hello è una singola proprietà: **messaggio = Hello!**.

Hello seguente immagine illustra hello sopra processo:

![](./media/notification-hubs-templates/notification-hubs-hello.png)

modello di Hello per la registrazione dell'app client iOS hello è come segue:

    {"aps": {"alert": "$(message)"}}

modello di Hello corrispondente per l'applicazione client di Windows Store hello è:

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

Si noti che hello effettivo del messaggio viene sostituito per hello espressione $(messaggio). Questa espressione indica hello Hub di notifica, ogni volta che invia un messaggio toothis registrazione particolare, un messaggio che segue viene switch in valore comune hello toobuild.

Se utilizza il modello di installazione, chiave "modelli" installazione di hello contiene un formato JSON di più modelli. Se si lavora con modello di registrazione, hello applicazione client può creare più registrazioni in ordine toouse più modelli. ad esempio, un modello per i messaggi di avviso e un modello di riquadro aggiornamenti. Inoltre, le applicazioni client possono unire registrazioni native (registrazioni senza modello) e registrazioni con modello.

Hub di notifica Hello invia una notifica per ogni modello, senza considerare se appartengono toohello app client stesso. Questo comportamento può essere notifiche indipendente dalla piattaforma tootranslate utilizzati in altre notifiche. Ad esempio, hello toohello di messaggi indipendenti dalla piattaforma stessa che hub di notifica possono essere convertiti perfettamente in un avviso di tipo avviso popup e un aggiornamento del riquadro, senza richiedere hello informati toobe di back-end. Si noti che alcune piattaforme (ad esempio, iOS) potrebbero comprime più notifiche toohello stesso dispositivo, se vengono inviati in un breve periodo di tempo.

## <a name="using-templates-for-personalization"></a>Utilizzo di modelli per la personalizzazione
Modelli di toousing un altro vantaggio è hello possibilità toouse sulla personalizzazione di hub di notifica tooperform per la registrazione delle notifiche. Si consideri ad esempio un'app meteo che consente di visualizzare un riquadro con condizioni climatiche hello in una posizione specifica. Un utente può scegliere tra gradi Celsius o Fahrenheit e una previsione singola o di cinque giorni. Utilizzo di modelli, ogni installazione di app client può registrare per formato hello richiesto (1 giorno Celsius, 1 giorno Fahrenheit, 5 giorni Celsius, 5 giorni Fahrenheit), e back-end hello invia un messaggio singolo che contiene tutte le informazioni di hello obbligatoria toofill quelli modelli (ad esempio, cinque giorni previsione con gradi Celsius e Fahrenheit).

modello Hello per hello un giorno previsione con Celsius temperature è come segue:

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

toohello messaggio Hello Hub di notifica contiene hello tutte le proprietà seguenti:

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

Utilizzando questo modello, back-end hello Invia solo un singolo messaggio senza opzioni di personalizzazione specifiche toostore per gli utenti di app hello. Hello seguente immagine illustra questo scenario:

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>Come modelli tooregister
vedere tooregister con modelli utilizzando il modello di installazione hello (scelta consigliato) o il modello di registrazione, hello [gestione registrazione](notification-hubs-push-notification-registration-management.md).

## <a name="template-expression-language"></a>Linguaggio di espressione dei modelli
I modelli sono tooXML limitato o formati di documenti JSON. Inoltre, è possibile inserire solo le espressioni in particolari punti: ad esempio, attributi dei nodi o valori per il formato XML, valori delle proprietà di stringa per il formato JSON.

Hello nella tabella seguente mostra linguaggio hello consentita nei modelli:

| Expression | Descrizione |
| --- | --- |
| $(prop) |Proprietà dell'evento tooan riferimento con il nome specificato hello. I nomi delle proprietà non distinguono tra maiuscole e minuscole. Questa espressione viene risolta in valore di testo della proprietà hello o in una stringa vuota se hello proprietà non è presente. |
| $(prop, n) |Come sopra, ma hello testo in modo esplicito troncato in corrispondenza di n caratteri, ad esempio $(titolo, 20) consente di ritagliare hello contenuto della proprietà title hello a 20 caratteri. |
| .(prop, n) |Come sopra, ma hello testo è Posposto con tre punti, come viene tagliato. dimensioni totali di Hello di hello troncato stringa e il suffisso hello non superi i n caratteri. . (titolo, 20) con una proprietà di input dei risultati "This is a riga di titolo hello" in **tratta titolo hello...** |
| %(prop) |Too$(name) simili, ad eccezione del fatto che l'output hello è con codifica URI. |
| #(prop) |Utilizzata nei modelli JSON (ad esempio, per modelli iOS e Android).<br><br>Questa funzione può essere utilizzata esattamente uguali hello come $(prop) specificata in precedenza, tranne quando sono usati nei modelli JSON (ad esempio, i modelli di Apple). In questo caso, se questa funzione non racchiusi tra "{','}" (ad esempio, 'myJsonProperty': '(nome) #'), e restituisce il numero di tooa in formato Javascript, ad esempio, regexp: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((a &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, quindi hello output JSON è un numero.<br><br>Ad esempio, ' badge : '#(name)' diventa 'badge' : 40 (e non '40'). |
| 'text' o "text" |Valore letterale. I valori letterali contengono testo arbitrario racchiuso tra virgolette singole o doppie. |
| expr1 + expr2 |operatore di concatenazione Hello unione di due espressioni in un'unica stringa. |

le espressioni di Hello possono essere qualsiasi di hello precedente form.

Quando si usa la concatenazione, intera espressione hello deve essere racchiuso tra {}. Ad esempio, {$(prop) + ' - ' + $(prop2)}. |

Esempio hello non è ad esempio, un modello XML valido:

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


Come spiegato in precedenza, quando si utilizza la concatenazione, le espressioni devono essere racchiuse tra parentesi graffe. Ad esempio:

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>


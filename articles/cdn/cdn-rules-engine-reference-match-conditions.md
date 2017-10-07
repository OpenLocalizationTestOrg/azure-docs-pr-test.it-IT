---
title: condizioni di corrispondenza del motore regole di aaaAzure CDN | Documenti Microsoft
description: "Documentazione di riferimento per le funzionalità e condizioni di corrispondenza del motore regole della rete CDN di Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Condizioni di corrispondenza del motore regole della rete CDN di Azure
Questo argomento elenca le descrizioni dettagliate dei hello disponibili le condizioni di corrispondenza per Azure rete CDN (Content Delivery) [motore regole di business](cdn-rules-engine.md).

Hello seconda parte di una regola è la condizione di corrispondenza hello. Una condizione di corrispondenza identifica specifici tipi di richieste per cui verrà eseguito un set di funzionalità.

Ad esempio, potrebbe essere utilizzato toofilter richieste per il contenuto in una determinata posizione, generato da un paese o l'indirizzo IP specifico o dalle informazioni di intestazione.

## <a name="always"></a>Sempre

Hello sempre condizione di corrispondenza è progettato tooapply impostare un valore predefinito di funzionalità tooall richieste.

## <a name="device"></a>Dispositivo

condizione di corrispondenza dispositivo Hello identifica le richieste effettuate da un dispositivo mobile in base alle relative proprietà.  Il rilevamento del dispositivo mobile viene eseguito tramite [WURFL](http://wurfl.sourceforge.net/).  Le funzionalità di WURFL e le variabili del motore regole della rete CDN sono elencate di seguito.

> [!NOTE] 
> variabili di Hello riportate di seguito sono supportate in hello **modificare intestazione di richiesta Client** e **modifica intestazione risposta Client** funzionalità.

Funzionalità | Variabile | Descrizione | Valore/i di esempio
-----------|----------|-------------|----------------
Brand Name (Nome marchio) | %{wurfl_cap_brand_name} | Stringa che indica il nome del marchio hello del dispositivo hello. | Samsung
Device OS (Sistema operativo dispositivo) | %{wurfl_cap_device_os} | Stringa che indica i sistemi operativi hello nel dispositivo hello. | IOS
Device OS Version (Versione sistema operativo dispositivo) | %{wurfl_cap_device_os_version} | Stringa che indica il numero di versione hello del sistema operativo installato nel dispositivo hello hello. | 1.0.1
Dual Orientation (Orientamento doppio) | %{wurfl_cap_dual_orientation} | Valore booleano che indica se il dispositivo hello supporta orientamento doppio. | true
HTML Preferred DTD (DTD preferito HTML) | %{wurfl_cap_html_preferred_dtd} | Stringa che indica la definizione tipo del dispositivo mobile hello preferito documento (DTD) per il contenuto HTML. | Nessuno<br/>xhtml_basic<br/>html5
Image Inlining (Incorporamento immagini) | %{wurfl_cap_image_inlining} | Immagini con codifica un valore booleano che indica se il dispositivo hello supporta Base64. | false
Is Android (È Android) | %{wurfl_vcap_is_android} | Valore booleano che indica se il dispositivo hello utilizza hello del sistema operativo Android. | true
Is IOS (È IOS) | %{wurfl_vcap_is_ios} | Valore booleano che indica se il dispositivo hello utilizza iOS. | false
Is Smart TV (È una smart TV) | %{wurfl_cap_is_smarttv} | Valore booleano che indica se il dispositivo di hello è un televisore smart. | false
Is Smartphone (È uno smartphone) | %{wurfl_vcap_is_smartphone} | Valore booleano che indica se il dispositivo di hello è uno smartphone. | true
Is Tablet (È un tablet) | %{wurfl_cap_is_tablet} | Valore booleano che indica se il dispositivo di hello è un tablet. Questa descrizione è indipendente dal sistema operativo. | true
Is Wireless Device (È un dispositivo wireless) | %{wurfl_cap_is_wireless_device} | Valore booleano che indica se il dispositivo hello viene considerato un dispositivo senza fili. | true
Marketing Name (Nome marketing) | %{wurfl_cap_marketing_name} | Stringa che indica nome marketing del dispositivo hello. | BlackBerry 8100 Pearl
Mobile Browser (Browser per dispositivi mobili) | %{wurfl_cap_mobile_browser} | Stringa che indica il browser hello utilizzato toorequest contenuto dal dispositivo hello. | Chrome
Mobile Browser Version (Versione browser per dispositivi mobili) | %{wurfl_cap_mobile_browser_version} | Stringa che indica la versione di hello del browser hello utilizzato toorequest contenuto dal dispositivo hello. | 31
Model Name (Nome modello) | %{wurfl_cap_model_name} | Stringa che indica il nome di modello del dispositivo hello. | s3
Download progressivo | %{wurfl_cap_progressive_download} | Valore booleano che indica se hello supporta hello la riproduzione di audio e video mentre è ancora corso il download. | true
Data di rilascio | %{wurfl_cap_release_date} | Una stringa che indica l'anno di hello e il mese in cui hello dispositivo è stato aggiunto il database WURFL toohello.<br/><br/>Formato: `yyyy_mm` | 2013_december
Resolution Height (Altezza risoluzione) | %{wurfl_cap_resolution_height} | Valore intero che indica l'altezza del dispositivo hello in pixel. | 768
Resolution Width (Larghezza risoluzione) | %{wurfl_cap_resolution_width} | Valore intero che indica la larghezza del dispositivo hello in pixel. | 1024


## <a name="location"></a>Percorso

Questi corrispondono alle condizioni richieste tooidentify progettata in base alla posizione del richiedente hello.

Nome | Scopo
-----|--------
Numero AS | Identifica le richieste che hanno origine da una determinata rete.
Paese | Identifica le richieste originate da hello specificato paesi.


## <a name="origin"></a>Origine

Questi corrispondono alle condizioni sono progettate tooidentify richieste che l'archiviazione tooCDN punto o un server di origine cliente.

Nome | Scopo
-----|--------
Origine CDN | Identifica le richieste di contenuto nell'archivio della rete CDN.
Origine cliente | Identifica le richieste di contenuto in uno specifico server di origine del cliente.


## <a name="request"></a>Richiesta

Questi corrispondono alle condizioni richieste tooidentify progettata in base alle relative proprietà.

Nome | Scopo
-----|--------
Indirizzo IP client | Identifica le richieste che hanno origine da un determinato indirizzo IP.
Parametro cookie | Controlli hello cookie associati a ogni richiesta di hello specificato valore.
Espressione regolare parametro cookie | Controlla i cookie hello associati a ogni richiesta di hello specificato di espressione regolare.
CNAME periferico | Identifica le richieste che puntano a bordo specifico tooa CNAME.
Dominio di riferimento | Identifica le richieste che sono state definite da hello specificato hostname(s).
Valore letterale intestazione richiesta | Identifica le richieste che contengono hello specificato intestazione set tooa specificati uno o più valori.
Espressione regolare intestazione richiesta | Identifica le richieste che contengono hello specificato intestazione set tooa corrispondente hello specificato espressione regolare.
Carattere jolly intestazione richiesta | Identifica le richieste che contengono hello specificato valore tooa che corrisponde a modello specificato hello impostare l'intestazione.
Metodo richiesta | Identifica le richieste in base al relativo metodo HTTP.
Schema richiesta | Identifica le richieste in base al relativo protocollo HTTP.

## <a name="url"></a>URL

Questi corrispondono alle condizioni sono richieste tooidentify progettata in base i relativi URL.

Nome | Scopo
-----|--------
Directory percorso URL | Identifica le richieste in base al percorso relativo.
Estensione percorso URL | Identifica le richieste in base all'estensione del nome file.
Nome file percorso URL | Identifica le richieste in base al nome del file.
Valore letterale percorso URL | Confronta una richiesta del percorso relativo toohello valore specificato.
Espressione regolare percorso URL | Confronta una richiesta di percorso relativo toohello espressione regolare specificato.
Carattere jolly percorso URL | Confronta criterio specificato toohello percorso relativo di una richiesta.
Valore letterale query URL | Confronta una richiesta del valore toohello di stringa di query specificato.
Parametro query URL | Identifica le richieste che contengono query di hello specificato parametro della stringa di valore tooa che corrisponde a un criterio specificato.
Espressione regolare query URL | Identifica le richieste che contengono query di hello specificato parametro della stringa di valore tooa che corrisponde a un'espressione regolare specificata.
Carattere jolly query URL | Confronta hello specificato valori in una stringa di query della richiesta di hello.


## <a name="next-steps"></a>Passaggi successivi
* [Panoramica della rete CDN di Azure](cdn-overview.md)
* [Informazioni di riferimento sul motore regole](cdn-rules-engine-reference.md)
* [Espressioni condizionali del motore regole](cdn-rules-engine-reference-conditional-expressions.md)
* [Funzionalità del motore regole](cdn-rules-engine-reference-features.md)
* [Override del comportamento HTTP predefinito utilizzando il motore regole di hello](cdn-rules-engine.md)


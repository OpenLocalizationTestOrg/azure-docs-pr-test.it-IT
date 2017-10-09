---
title: aaaTroubleshoot Analitica in Azure Application Insights | Documenti Microsoft
description: 'Problemi con Application Insights Analytics? Inizia da qui. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Risoluzione dei problemi di Analytics in Application Insights
Problemi con [Application Insights Analytics](app-insights-analytics.md)? Inizia da qui. Analitica è hello potente strumento di ricerca di Azure Application Insights.

## <a name="limits"></a>Limiti
* Al momento, i risultati della query sono toojust limitato più di una settimana di dati passati.
* Browser su cui eseguiamo i test: versioni più recenti di Chrome, Edge e Internet Explorer.

## <a name="known-incompatible-browser-extensions"></a>Estensioni del browser dall'incompatibilità nota
* Ghostery

Disabilitare l'estensione hello o utilizzare un browser diverso.

## <a name="e-a"></a> "Errore imprevisto"
![Schermata di errore imprevisto](./media/app-insights-analytics-troubleshooting/010.png)

Si è verificato un errore interno durante il runtime del portale: eccezione non gestita.

* Eseguire la pulizia della cache del browser hello. 

## <a name="e-b"></a>403.... riprovare tooreload
![403.... riprovare tooreload](./media/app-insights-analytics-troubleshooting/020.png)

Si è verificato un errore correlato all'autenticazione (durante l'autenticazione o durante la generazione del token di accesso). portale Hello può in alcun modo troppo ripristinare senza modificare le impostazioni del browser.

* Verificare [sono abilitati i cookie di terze parti](#cookies) nel browser hello. 

## <a name="authentication"></a>403 ... verificare l'area di sicurezza
![403 ... verify security zone](./media/app-insights-analytics-troubleshooting/030.png)

Si è verificato un errore correlato all'autenticazione (durante l'autenticazione o durante la generazione del token di accesso). portale Hello può in alcun modo troppo ripristinare senza modificare le impostazioni del browser.

1. Verificare [sono abilitati i cookie di terze parti](#cookies) nel browser hello. 
2. È stato usato un preferito, un segnalibro o un collegamento salvato tooopen hello Analitica portale? È eseguito l'accesso con credenziali diverse da quello utilizzato al momento del salvataggio collegamento hello?
3. Provare a utilizzare una finestra del browser privata/in incognito (dopo aver chiuso tutte le finestre di questo tipo). È necessario tooprovide le credenziali. 
4. Aprire un'altra finestra del browser (comune) e andare troppo[Azure](https://portal.azure.com). Uscire, Aprire il collegamento e accedere con le credenziali corrette hello.
5. Gli utenti di Edge e Internet Explorer possono ricevere questo errore anche quando le impostazioni delle zone attendibili non sono supportate.
   
    Verificare sia [portale Analitica](https://analytics.applicationinsights.io) e [portale di Azure Active Directory](https://portal.azure.com) in hello stessa area di protezione:
   
   * In Internet Explorer aprire **Opzioni Internet**, **Sicurezza**, **Siti attendibili**, **Siti**:
     
     ![Finestra di dialogo Opzioni Internet, l'aggiunta di un sito tooTrusted siti](./media/app-insights-analytics-troubleshooting/033.png)
     
     Nell'elenco di siti Web hello, se uno qualsiasi dei hello URL seguenti sono incluso, assicurarsi che tale hello ad altri utenti sono inoltre inclusi:
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Resource not found
![404 ... resource not found](./media/app-insights-analytics-troubleshooting/040.png)

Una risorsa dell'applicazione è stata eliminata da Application Insights e non è più disponibile. Questa situazione può verificarsi se è stato salvato nella pagina hello URL toohello Analitica.

## <a name="e-e"></a>403 ... No authorization
![403 ... not authorized](./media/app-insights-analytics-troubleshooting/050.png)

Non si dispone dell'autorizzazione tooopen questa applicazione in Analitica.

* Sono stati ottenuti hello collegamento da un altro utente? Chiedere che la hello toomake [lettori o collaboratori per questo gruppo di risorse](app-insights-resources-roles-access-control.md).
* È stato salvato il collegamento hello utilizzando credenziali diverse? Aprire hello [portale di Azure](https://portal.azure.com), disconnettersi e quindi provare questo collegamento, fornendo le credenziali corrette hello.

## <a name="html-storage"></a>403 ... HTML5 Storage
Il portale utilizza HTML5 localStorage e sessionStorage.

* Chrome: Impostazioni, Privacy, Impostazioni contenuti.
* Internet Explorer: Opzioni Internet, scheda Avanzate, Sicurezza, Abilita archiviazione DOM

![403... provare archiviazione tooenable HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Sottoscrizione non trovata
![404 ... Sottoscrizione non trovata](./media/app-insights-analytics-troubleshooting/070.png)

Hello URL è valido. 

* Aprire una risorsa applicazione hello in [portale Application Insights](https://portal.azure.com). Quindi sul pulsante hello Analitica.

## <a name="e-h"></a>404 ... la pagina non esiste
![404 ... Page does not exist](./media/app-insights-analytics-troubleshooting/080.png)

Hello URL è valido.

* Aprire una risorsa applicazione hello in [portale Application Insights](https://portal.azure.com). Quindi sul pulsante hello Analitica.

## <a name="cookies"></a>Abilitare i cookie di terze parti
  Vedere [come toodisable terze parti cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), ma è necessario troppo**abilitare** li.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]


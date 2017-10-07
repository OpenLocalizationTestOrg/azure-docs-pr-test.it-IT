---
title: riferimento per le impostazioni di roaming aaaWindows 10 | Documenti Microsoft
description: "Un elenco completo di tutte le impostazioni di hello che verrà eseguito il backup in Windows 10 o spostate."
services: active-directory
keywords: enterprise state roaming, cloud windows
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 17cffc3e-2928-4235-91f7-a685bd6bdcbf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 381e2220b698bb0e477c207984ff96c03ed132ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-roaming-settings-reference"></a>Riferimento alle impostazioni di roaming di Windows 10
di seguito Hello è un elenco completo di tutte le impostazioni di hello che verrà eseguito il backup in Windows 10 o spostate. 

## <a name="devices-and-endpoints"></a>Dispositivi ed endpoint
Vedere hello seguente tabella per un riepilogo di hello dispositivi e i tipi di account che sono supportati dalla sincronizzazione hello, backup e ripristino framework in Windows 10.

| Tipo di account e operazione | Desktop | Mobile |
| --- | --- | --- |
| Azure Active Directory: sincronizzazione |Sì |No |
| Azure Active Directory: backup e ripristino |No |No |
| Account Microsoft: sincronizzazione |Sì |Sì |
| Account Microsoft: backup e ripristino |No |Sì |

## <a name="what-is-backup"></a>Cosa si intende per backup
Impostazioni di Windows in genere di sincronizzazione per impostazione predefinita, ma alcune impostazioni sono solo il backup, ad esempio elenco hello delle applicazioni installate in un dispositivo. Al momento il backup è disponibile solo per i dispositivi mobili e non è fruibile dagli utenti del servizio Enterprise State Roaming. Backup utilizza un account Microsoft e archivia le impostazioni di hello e dati dell'applicazione in OneDrive. Se un utente disabilita la sincronizzazione sul dispositivo hello utilizza hello impostazioni app, i dati dell'applicazione che in genere si sincronizza diventano solo backup. Dati di backup è accessibile solo tramite l'operazione di ripristino hello durante la prima esecuzione di un nuovo dispositivo hello. I backup può essere disabilitati tramite le impostazioni di dispositivo, hello e possono essere gestiti ed eliminati tramite hello OneDrive account utente.

## <a name="windows-settings-overview"></a>Panoramica sulle impostazioni di Windows
Hello seguenti gruppi di impostazioni sono disponibili per la sincronizzazione di utenti finali tooenable o disabilitare le impostazioni nei dispositivi Windows 10.

* Tema: sfondo del desktop, icona utente, posizione della barra delle applicazioni e così via. 
* Impostazioni di Internet Explorer: cronologia esplorazioni, URL tipizzati, Preferiti e così via. 
* Password: [Casella di sicurezza delle credenziali di Windows](https://technet.microsoft.com/library/jj554668.aspx), inclusi i profili Wi-Fi. 
* Preferenze lingua: dizionario per il controllo ortografico, impostazioni della lingua del sistema. 
* Accessibilità: Assistente vocale, tastiera su schermo, lente di ingrandimento. 
* Altre impostazioni di Windows: vedere la sezione Dettagli relativi alle impostazioni di Windows.

![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-individual-sync-settings.png)

La sincronizzazione del gruppo di impostazioni del browser Edge (Preferiti, Elenco di lettura) può essere abilitata o disabilitata dagli utenti finali tramite la relativa opzione del menu Impostazioni del browser Edge.

![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-sync-content.png)

## <a name="windows-settings-details"></a>Dettagli relativi alle impostazioni di Windows
In hello nella tabella seguente, le altre voci nella colonna di gruppo di impostazioni hello fa riferimento toosettings che possono essere disattivati passando tooSettings > account > Sincronizza le impostazioni > Impostazioni di altre finestre. 

Interne voci nella colonna di gruppo di impostazioni hello riferimento toosettings e App che può essere disabilitata solo nella sincronizzazione all'interno di hello app stessa o disabilitare la sincronizzazione per l'intero dispositivo hello utilizzando Gestione dei dispositivi mobili (MDM) o le impostazioni di criteri di gruppo.
Impostazioni che non eseguono il roaming o sincronizzazione non apparterrà tooa gruppo.

| Impostazioni | Desktop | Mobile | Gruppo |
| --- | --- | --- | --- |
| **Account**: immagine dell'account |sync |X |Tema |
| **Account**: altre impostazioni account |X |X | |
| **Banda larga mobile avanzata**: nome della rete di Condivisione connessione Internet, che consente il rilevamento automatico degli hotspot Wi-Fi per dispositivi mobili tramite Bluetooth |X |X |Password |
| **Dati app**: singole app possono sincronizzare i dati |backup sincronizzazione |backup sincronizzazione |Interne |
| **Elenco app**: elenco delle app installate |X |backup |Altre |
| **Bluetooth**: tutte le impostazioni Bluetooth |X |X | |
| **Prompt dei comandi**: impostazioni dei valori predefiniti del prompt dei comandi |sync |X | |
| **Credenziali**: Casella di sicurezza delle credenziali |sync |sync |password |
| **Data, ora e opzioni internazionali**: ora automatica (sincronizzazione con l'ora Internet) |sync |sync |Lingua |
| **Data, ora e opzioni internazionali**: formato a 24 ore |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: data e ora |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: fuso orario | |X |Lingua |
| **Data, ora e opzioni internazionali**: ora legale |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: paese/area geografica |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: primo giorno della settimana |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: formato regionale (impostazioni locali) |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: data breve |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: data estesa |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: ora breve |sync |X |Lingua |
| **Data, ora e opzioni internazionali**: ora estesa |sync |X |Lingua |
| **Personalizzazione del desktop**: tema del desktop (sfondo, colore di sistema, segnali acustici sistema predefiniti, screen saver) |sync |X |Tema |
| **Personalizzazione del desktop**: sfondo presentazione |sync |X |Tema |
| **Personalizzazione del desktop**: impostazioni della barra delle applicazioni (posizione, Nascondi automaticamente e così via) |sync |X |Tema |
| **Personalizzazione del desktop**: layout della schermata Start |X |backup | |
| **Dispositivi**: si è connessi troppo stampanti condivise|X |X |Altre |
| **Browser Edge**: Elenco di lettura |sync |sync |Interne |
| **Browser Edge**: Preferiti |sync |sync |Interne |
| **Browser Edge**: siti principali <sup> [[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: URL digitati <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: impostazioni barra Preferiti <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: Mostra pulsante home hello <sup> [[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: blocca popup <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: Chiedi quali toodo con ogni download <sup> [[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: offrono le password toosave <sup> [[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: invia richieste Do Not Track <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: salva i dati immessi nei moduli <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: mostra suggerimenti per la ricerca e i siti durante la digitazione <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: preferenze cookie <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: consenti ai siti di archiviare le licenze per i contenuti multimediali protetti nel dispositivo <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Browser Edge**: impostazione utilità per la lettura dello schermo <sup>[[1]](#footnote-1)</sup> |sync |sync |Interne |
| **Contrasto elevato**: abilitazione/disabilitazione |sync |X |Accessibilità |
| **Contrasto elevato**: impostazioni del tema |sync |X |Accessibilità |
| **Internet Explorer**: schede aperte (URL e titolo) |sync |sync |Internet Explorer |
| **Internet Explorer**: Elenco di lettura |sync |sync |Internet Explorer |
| **Internet Explorer**: URL digitati |sync |sync |Internet Explorer |
| **Internet Explorer**: cronologia esplorazioni |sync |sync |Internet Explorer |
| **Internet Explorer**: Preferiti |sync |sync |Internet Explorer |
| **Internet Explorer**: URL esclusi |sync |sync |Internet Explorer |
| **Internet Explorer**: home page |sync |sync |Internet Explorer |
| **Internet Explorer**: suggerimenti dominio |sync |sync |Internet Explorer |
| **Tastiera**: abilitazione/disabilitazione della tastiera su schermo |sync |X |Accessibilità |
| **Tastiera**: Attiva Tasti permanenti (disabilitati per impostazione predefinita) |sync |X |Accessibilità |
| **Tastiera**: Attiva Filtro tasti (disabilitato per impostazione predefinita) |sync |X |Accessibilità |
| **Tastiera**: Attiva Segnali acustici (disabilitati per impostazione predefinita) |sync |X |Accessibilità |
| **Internet Explorer**: cinese (QWERTY), abilitazione dell'apprendimento automatico della lingua del dominio |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), abilitazione della classificazione dinamica dei candidati |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), set di caratteri cinese semplificato |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), set di caratteri cinese tradizionale |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), Pinyin fuzzy |sync |backup |Lingua |
| **Lingua**: cinese (QWERTY), coppie fuzzy |sync |backup |Lingua |
| **Lingua**: cinese (QWERTY), Pinyin completo |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), Pinyin doppio |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), correzione automatica lettura |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), cambio tastiera C/E, MAIUSC |sync |X |Lingua |
| **Lingua**: cinese (QWERTY), cambio tastiera C/E, CTRL |sync |X |Lingua |
| **Lingua**: cinese (WUBI), Modalità di input a singolo carattere |sync |X |Lingua |
| **Lingua**: WUBI CHS - Mostra hello rimanenti codifica di candidate hello |sync |X |Lingua |
| **Lingua**: cinese (WUBI), Emetti un segnale acustico se la codifica 4 non è valida |sync |X |Lingua |
| **Lingua**: Bopomofo cinese tradizionale, incluso CJK estensione A |sync |X |Lingua |
| **Lingua**: IME giapponese, digitazione predittiva e parole personalizzate |sync |sync |Lingua |
| **Lingua**: IME coreano |X |X |Lingua |
| **Lingua**: riconoscimento della grafia |X |X |Lingua |
| **Lingua**: profilo lingua |sync |backup |Lingua |
| **Lingua**: controllo ortografico, correzione automatica ed evidenziazione degli errori di ortografia |sync |backup |Lingua |
| **Lingua**: elenco delle tastiere |sync |backup |Lingua |
| **Schermata di blocco**: tutte le impostazioni della schermata di blocco |X |X | |
| **Lente di ingrandimento**: abilitazione/disabilitazione (master) |X |X |Accessibilità |
| **Lente di ingrandimento**: Attiva inversione colori (disattivata per impostazione predefinita) |sync |X |Accessibilità |
| **Lente di ingrandimento**: rilevamento - seguire hello stato attivo della tastiera |sync |X |Accessibilità |
| **Lente di ingrandimento**: rilevamento - cursore del mouse di seguire hello |sync |X |Accessibilità |
| **Lente di ingrandimento**: avvio all'accesso dell'utente (disabilitato per impostazione predefinita) |sync |X |Accessibilità |
| **Mouse**: modificare dimensioni hello del cursore del mouse |sync |X |Altro |
| **Mouse**: modificare il colore di hello del cursore del mouse |sync |X |Altre |
| **Mouse**: tutte le altre impostazioni |X |X | |
| **Assistente vocale**: avvio veloce |sync |X |Accessibilità |
| **Assistente vocale**: gli utenti possono modificare la tonalità di voce dell'Assistente vocale |sync |X |Accessibilità |
| **Assistente vocale**: gli utenti possono abilitare/disabilitare la lettura di suggerimenti per gli elementi comuni da parte dell'Assistente vocale (abilitata per impostazione predefinita) |sync |X |Accessibilità |
| **Assistente vocale**: gli utenti possono abilitare/disabilitare la lettura dei caratteri digitati (abilitata per impostazione predefinita) |sync |X |Accessibilità |
| **Assistente vocale**: gli utenti possono abilitare/disabilitare la lettura delle parole digitate (abilitata per impostazione predefinita) |sync |X |Accessibilità |
| **Assistente vocale**: il cursore di inserimento segue l'Assistente vocale (abilitata per impostazione predefinita) |sync |X |Accessibilità |
| **Assistente vocale**: Abilita evidenziazione visiva del cursore dell'Assistente vocale (abilitata per impostazione predefinita) |sync |X |Accessibilità |
| **Assistente vocale**: Riproduci segnali acustici (abilitata per impostazione predefinita) |sync |X |Accessibilità |
| **Assistente vocale**: attivazione della tastiera tocco hello quando si solleva il dito (disattivato per impostazione predefinita) |sync |X |Accessibilità |
| **Facilità di accesso**: impostare lo spessore del cursore intermittente hello hello |sync |X |Accessibilità |
| **Accessibilità**: Rimuovi immagini di sfondo (disabilitata per impostazione predefinita) |sync |X |Accessibilità |
| **Alimentazione e sospensione**: tutte le impostazioni |X |X | |
| **Personalizzazione della schermata Start**: colore principale (solo telefono) |X |sync |Tema |
| **Digitazione**: dizionario per il controllo ortografico |sync |backup |Lingua |
| **Digitazione**: Correggi automaticamente errori di ortografia |sync |backup |Lingua |
| **Digitazione**: Evidenzia errori di ortografia |sync |backup |Lingua |
| **Digitazione**: Mostra suggerimenti di testo durante la digitazione |sync |backup |Lingua |
| **Digitazione**: Aggiungi uno spazio quando scelgo un suggerimento di testo |sync |backup |Lingua |
| **Digitare**: aggiungere un punto dopo che un doppio tocco barra spaziatrice hello |sync |backup |Lingua |
| **Digitare**: maiuscola hello di ogni frase |sync |backup |Lingua |
| **Digitazione**: Usa tutte maiuscole dopo doppio tocco del tasto MAIUSC |sync |backup |Lingua |
| **Digitazione**: Riproduci suoni tasti durante la digitazione |sync |backup |Lingua |
| **Digitazione**: dati di personalizzazione per la tastiera virtuale |sync |backup |Lingua |
| **Wi-Fi**: profili Wi-Fi (solo WPA) |sync |sync |Password |

###### <a name="footnote-1"></a>Nota 1
Versione minima sistema operativo supportata di Windows Creators Update (Build 15063). 

## <a name="related-topics"></a>Argomenti correlati
* [Panoramica di Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Abilitare Enterprise State Roaming in Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Domande frequenti su impostazioni e dati in roaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Criteri di gruppo e impostazioni del software MDM per la sincronizzazione delle impostazioni](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Risoluzione dei problemi](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

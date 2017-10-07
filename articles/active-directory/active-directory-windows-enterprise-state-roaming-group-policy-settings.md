---
title: impostazioni dei criteri e MDM aaaGroup | Documenti Microsoft
description: "Fornisce informazioni sulle impostazioni di Criteri di gruppo e di gestione di dispositivi mobili che dovrebbero essere usate in dispositivi di proprietà aziendale. Questi criteri sono applicati toohello intero dispositivo utente."
services: active-directory
keywords: informazioni sulle impostazioni di Criteri di gruppo e gestione di dispositivi mobili per Enterprise State Roaming, Enterprise State Roaming, cloud windows
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>Impostazioni di Criteri di gruppo e di gestione di dispositivi mobili
Poiché questi criteri sono applicati toohello intero dispositivo utente, usare questi criteri di gruppo e impostazioni dei dispositivi mobili (MDM) di gestione solo per i dispositivi di proprietà dell'azienda. L'applicazione di una sincronizzazione di impostazioni toodisable criteri MDM per un uso personale, dispositivi di proprietà dell'utente un impatto negativo utilizzare hello del dispositivo. Inoltre, altri account utente sul dispositivo hello interesserà anche da criteri di hello.

Aziende che desiderano toomanage roaming per i dispositivi personali di (non gestiti) è possibile utilizzare hello tooenable portale Azure o disabilitare il roaming, anziché utilizzare i criteri di gruppo o MDM.
Hello le tabelle seguenti vengono descritte le impostazioni dei criteri di hello disponibili.

## <a name="mdm-settings"></a>Impostazioni di gestione di dispositivi mobili
le impostazioni dei criteri di gestione dei dispositivi mobili Hello applicano tooboth Windows 10 e Windows 10 Mobile.  Il supporto per Windows 10 Mobile esiste solo per il roaming basato su account Microsoft tramite l’account OneDrive dell’utente.  Consultare troppo la sezione "Endpoint e i dispositivi" per informazioni dettagliate su quali dispositivi sono supportati per Azure AD in base la sincronizzazione.

| Nome | Descrizione |
| --- | --- |
| Allow Microsoft Account Connection |Consente agli utenti tooauthenticate utilizzando un account Microsoft sul dispositivo hello |
| Allow Sync My Settings |Consente le impostazioni di Windows tooroam utenti e i dati dell'app; La disabilitazione di questo criterio verrà disattivata la sincronizzazione, nonché i backup su dispositivi mobili |

## <a name="group-policy-settings"></a>Impostazioni di Criteri di gruppo
le impostazioni di criteri di gruppo Hello si applicano i dispositivi tooWindows 10 tooan aggiunti a un dominio di Active Directory. tabella Hello include anche le impostazioni legacy che verrebbe visualizzato toomanage impostazioni di sincronizzazione, ma che non funzionano per Enterprise stato Roaming per Windows 10, indicate con "non utilizzare' nella descrizione hello.

| Nome | Descrizione |
| --- | --- |
| Account: blocca gli account Microsoft |Questa impostazione dei criteri impedisce agli utenti di aggiungere nuovi account Microsoft nel computer |
| Non sincronizzare |Impedisce che le impostazioni di Windows tooroam utenti e i dati dell'app |
| Non sincronizzare gruppo personalizza |Disabilita la sincronizzazione del gruppo di temi hello |
| Non sincronizzare impostazioni browser |Disabilita la sincronizzazione del gruppo di Internet Explorer hello |
| Non sincronizzare password |Disabilita la sincronizzazione del gruppo Password |
| Non sincronizzare altre impostazioni di Windows |Disabilita la sincronizzazione del gruppo Altre impostazioni di Windows |
| Non sincronizzare personalizzazione desktop |Non usare questa impostazione perché non ha alcun effetto |
| Non sincronizzare connessioni a consumo |Disabilita il roaming nelle connessioni a consumo come le connessioni 3G per i cellulari |
| Non sincronizzare le app |Non usare questa impostazione perché non ha alcun effetto |
| Non sincronizzare impostazioni app |Disabilita il roaming dei dati delle app |
| Non sincronizzare impostazioni Start |Non usare questa impostazione perché non ha alcun effetto |

## <a name="related-topics"></a>Argomenti correlati
* [Panoramica di Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Abilitare Enterprise State Roaming in Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Domande frequenti su impostazioni e dati in roaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Riferimento alle impostazioni di roaming di Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Risoluzione dei problemi](active-directory-windows-enterprise-state-roaming-troubleshooting.md)


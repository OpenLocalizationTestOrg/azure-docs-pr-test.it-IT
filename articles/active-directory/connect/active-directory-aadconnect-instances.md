---
title: 'Azure AD Connect: Istanze del servizio di sincronizzazione | Documentazione Microsoft'
description: Questa pagina contiene considerazioni speciali per le istanze di Azure AD.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: Considerazioni speciali per le istanze
Azure AD Connect è più utilizzata con l'istanza di hello world wide di Azure AD e Office 365. Ma esistono anche altre istanze e hanno requisiti diversi per gli URL e altre considerazioni speciali.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Germany
Hello [Microsoft Cloud Germania](http://www.microsoft.de/cloud-deutschland) è un cloud sovrani gestito da un dominio trusted in tedesco di dati.

| Tooopen URL server proxy |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| +Elenchi di revoche dei certificati |

Quando si accede nel tenant di Azure AD tooyour, è necessario utilizzare un account nel dominio onmicrosoft.de hello.

Funzionalità attualmente non è presente in Germania Cloud Microsoft hello:

* **Azure AD Connect Health** non è disponibile.
* **Aggiornamenti automatici** non è disponibile.
* **Writeback delle password** è disponibile in anteprima con Azure AD Connect versione 1.1.570.0 e successive.
* Altri servizi di Azure AD Premium non sono disponibili.

## <a name="microsoft-azure-government-cloud"></a>Cloud di Microsoft Azure per enti pubblici
Hello [cloud di Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/) è un cloud per governo degli Stati Uniti.

È stato supportato da versioni precedenti di DirSync. Da compilazione 1.1.180 di Azure AD Connect, hello prossima generazione di cloud hello è supportato. Questa generazione utilizza gli endpoint di base solo Stati Uniti e di un elenco di URL tooopen nel server proxy.

| Tooopen URL server proxy |
| --- |
| \*.microsoftonline.com |
| \*. microsoftonline.us |
| \*.gov.us.microsoftonline.com |
| +Elenchi di revoche dei certificati |

Azure AD Connect non è in grado di tooautomatically rilevare che si trova nel cloud per enti pubblici hello tenant di Azure AD. È invece necessario hello tootake seguente azioni quando si installa Azure AD Connect.

1. Avviare l'installazione di Azure AD Connect hello.
2. Quando viene visualizzata prima pagina hello in cui è richiesta la hello tooaccept contratto di licenza, non continuare, ma lasciare la procedura guidata installazione hello in esecuzione.
3. Avviare regedit e modificare la chiave del Registro di sistema hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valore `2`.
4. Tornare indietro toohello Azure AD Connect installazione guidata, accettare l'EULA hello e continuare. Durante l'installazione, assicurarsi che hello toouse **configurazione personalizzata** percorso di installazione (e non l'installazione rapida). Quindi continuare l'installazione di hello come di consueto.

Funzionalità attualmente non è presente nel cloud di Microsoft Azure per enti pubblici hello:

* **Azure AD Connect Health** non è disponibile.
* **Aggiornamenti automatici** non è disponibile.
* **Writeback delle password** è disponibile in anteprima con Azure AD Connect versione 1.1.570.0 e successive.
* Altri servizi di Azure AD Premium non sono disponibili.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

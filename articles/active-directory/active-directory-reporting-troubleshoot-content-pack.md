---
title: "Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory | Microsoft Docs"
description: "Offre un elenco dei messaggi di errore del pacchetto di contenuto delle attività di Azure Active Directory e i passaggi per risolvere il problema."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: b22f387a0338246c7586f0f0735b4612a796691a
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2018
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory 


Quando si usa il pacchetto di contenuto di Power BI per l'anteprima di Azure Active Directory, è possibile che si verifichino gli errori seguenti: 

- [Aggiornamento non riuscito](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [L'aggiornamento delle credenziali dell'origine dati non è riuscito](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [L'importazione dei dati richiede troppo tempo](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Questo argomento offre informazioni sulle possibili cause e su come risolvere questi errori.
 
## <a name="refresh-failed"></a>Aggiornamento non riuscito 
 
**Modalità di esposizione dell'errore**: messaggio di posta elettronica inviato da Power BI o stato di errore nella cronologia aggiornamenti. 


| Causa | Modalità di correzione |
| ---   | ---        |
| Gli errori di aggiornamento non riuscito possono verificarsi quando le credenziali degli utenti che si connettono al pacchetto di contenuto sono state reimpostate ma non sono state aggiornate nelle impostazioni di connessione del pacchetto di contenuto. | Individuare in Power BI il set di dati corrispondente al dashboard dei log attività di Azure Active Directory (log attività di Azure Active Directory), scegliere Pianifica aggiornamento e quindi immettere le credenziali di Azure AD. |
| Un aggiornamento può non riuscire a causa di problemi relativi ai dati nel pacchetto di contenuto sottostante. | Inviare un ticket di supporto. Per informazioni dettagliate, vedere [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md) (Come ottenere supporto per Azure Active Directory).|
 
 
## <a name="failed-to-update-data-source-credentials"></a>L'aggiornamento delle credenziali dell'origine dati non è riuscito 
 
**Modalità di esposizione dell'errore**: in Power BI durante la connessione al pacchetto di contenuto dei log attività di Azure Active Directory (anteprima). 

| Causa | Modalità di correzione |
| ---   | ---        |
| L'utente che sta tentando di connettersi non è un amministratore globale, non dispone di un ruolo con autorizzazioni di lettura per la sicurezza né di amministratore della sicurezza. | Per accedere ai pacchetti di contenuto, usare un account di amministratore globale, con autorizzazioni di lettura per la sicurezza o di amministratore della sicurezza. |
| Il tenant non è un tenant Premium o non include almeno un utente con un file di licenza Premium. | Inviare un ticket di supporto. Per informazioni dettagliate, vedere [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md) (Come ottenere supporto per Azure Active Directory).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>L'importazione dei dati richiede troppo tempo 
 
**Modalità di esposizione dell'errore**: in Power BI dopo la connessione del pacchetto di contenuto viene avviato il processo di importazione dei dati per preparare il dashboard per il log attività di Azure Active Directory. Viene visualizzato il messaggio "*Importazione dei dati in corso...*"  

| Causa | Modalità di correzione |
| ---   | ---        |
| A seconda delle dimensioni del tenant, questo passaggio può richiedere da alcuni minuti a 30 minuti. | Attendere. Se entro un'ora il messaggio non cambia e non viene visualizzato il dashboard, inviare un ticket di supporto. Per informazioni dettagliate, vedere [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md) (Come ottenere supporto per Azure Active Directory).|

## <a name="next-steps"></a>Passaggi successivi

Per installare il pacchetto di contenuto di Power BI per l'anteprima di Azure Active Directory, fare clic su [qui](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).



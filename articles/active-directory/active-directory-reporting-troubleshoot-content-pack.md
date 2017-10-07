---
title: "Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory | Microsoft Docs"
description: "Fornisce un elenco di messaggi di errore di hello attività di Azure Active Directory contenuto pack e i passaggi toofix li."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Risoluzione dei problemi relativi ai pacchetti di contenuto dei log attività di Azure Active Directory 


Quando si lavora con hello pacchetto di contenuto di Power BI per l'anteprima di Azure Active Directory, è possibile che si verifichino hello gli errori seguenti: 

- [Aggiornamento non riuscito](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Credenziali dell'origine dati tooupdate non riuscita](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [L'importazione dei dati richiede troppo tempo](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
In questo argomento vengono fornite informazioni sulle possibili cause di hello e come toofix questi errori.
 
## <a name="refresh-failed"></a>Aggiornamento non riuscito 
 
**La modalità in cui viene esposto l'errore**: messaggio di posta elettronica da Power BI o stato di errore nella cronologia dell'aggiornamento hello. 


| Causa | Come toofix |
| ---   | ---        |
| Aggiornare l'errore possono verificarsi errori quando le credenziali di hello di utenti hello connessione toohello pacchetto di contenuto sono state reimpostare ma non aggiornate nelle impostazioni di connessione hello di hello del pacchetto di contenuto hello. | In Power BI, è possibile individuare hello set di dati corrispondente toohello dashboard log attività di Azure Active Directory (registri dell'attività di Azure Active Directory), scegliere la pianificazione dell'aggiornamento e quindi immettere le credenziali di Azure AD. |
| Un aggiornamento può non riuscire a causa di problemi di toodata hello sottostante pacchetto di contenuto. | Inviare un ticket di supporto. Per ulteriori informazioni, vedere [come tooget il supporto per Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Credenziali dell'origine dati tooupdate non riuscita 
 
**La modalità in cui viene esposto l'errore**: In Power BI, quando ci si connette toohello pacchetto di contenuto (anteprima) log attività di Azure Active Directory. 

| Causa | Come toofix |
| ---   | ---        |
| utente che si connette Hello è né un amministratore globale né un lettore di sicurezza o un amministratore di protezione. | Utilizzare un account che è un amministratore globale o un lettore di protezione o una protezione admin tooaccess hello pacchetti di contenuto. |
| Il tenant non è un tenant Premium o non include almeno un utente con un file di licenza Premium. | Inviare un ticket di supporto. Per ulteriori informazioni, vedere [come tooget il supporto per Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>L'importazione dei dati richiede troppo tempo 
 
**La modalità in cui viene esposto l'errore**: In Power BI, dopo avere connesso il pacchetto di contenuto, processo di importazione dati hello inizia tooprepare dashboard per il log attività di Azure Active Directory. Viene visualizzato il messaggio hello: "*l'importazione di dati...* "  

| Causa | Come toofix |
| ---   | ---        |
| A seconda delle dimensioni di hello del tenant, questo passaggio potrebbe richiedere da alcuni minuti too30 minuti. | Attendere. Se il messaggio hello non cambia tooshowing dashboard entro un'ora, inviare un ticket di supporto. Per ulteriori informazioni, vedere [come tooget il supporto per Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Passaggi successivi

Fare clic su hello tooinstall pacchetto di contenuto Power BI per Azure Active Directory anteprima [qui](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).



---
title: domande frequenti di Active Directory Reporting su aaaAzure | Documenti Microsoft
description: Domande frequenti sulla creazione di report in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>Domande frequenti sulla creazione di report in Azure Active Directory

In questo articolo vengono fornite le risposte toofrequently domande frequenti (FAQ) sulla creazione di report di Azure Active Directory.  
Per altre informazioni, vedere la pagina relativa alla [creazione di report in Azure Active Directory](active-directory-reporting-azure-portal.md) 

**D: qual è la conservazione dei dati hello per i log di attività (controllo e accessi) nel portale di Azure hello?** 

**R:** forniamo 7 giorni di dati per i clienti gratuiti e passando tooan Azure AD Premium 1 o 2 Premium licenza, è possibile accedere a dati per i giorni too30. Per altri dettagli sulla conservazione, vedere la pagina relativa ai [criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md).

--- 

**D: come tempo fino a quando non vengono visualizzati i dati di attività hello dopo aver completato le attività?**

**R:** log attività di controllo con una latenza compresa tra 15 minuti tooan ora. Log attività di accesso con una latenza compreso tra 15 minuti per la maggior parte dei record e le ore too2 per alcuni record.

---

**D: è necessario toobe che un'attività di amministratore globale toosee hello registra nel portale di Azure hello tooget dati o tramite API hello?**

**R:** No. Può essere un **lettore sicurezza**, un **amministratore responsabile della sicurezza** o **amministratore globale** toosee segnalano i dati nel portale di Azure o accedendovi mediante hello API.

---

**D: è possibile ottenere informazioni di log attività di Office 365 tramite il portale di Azure hello?**

**R:** anche attività di Office 365 e Azure AD attività registri condividere molte delle risorse della directory hello, se si desidera una visualizzazione completa di hello log attività di Office 365, è necessario passare informazioni del log attività di Office 365 tooget toohello il centro di amministrazione di Office 365.

---


**D: quali API utilizzare tooget informazioni sui log attività di Office 365?**

**R:** hello tooaccess API di gestione di Office 365 di usare hello [log attività di Office 365 tramite un'API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**D: Quanti record è possibile scaricare dal portale di Azure?**

**R:** è possibile scaricare i record too120K da hello portale di Azure. record Hello sono ordinati per *più recente* e per impostazione predefinita, si visualizza record hello K 120 più recente. 

---

**D: come numero di record è query tramite le attività di hello API?**

**R:** è possibile eseguire query dei milioni record too1 (se non si utilizza l'operatore top hello, che ordina i record di hello più recente). Se si utilizza l'operatore "top" hello, è possibile eseguire query dei record too500K. È possibile trovare esempi di query in modalità toouse hello API qui [qui](active-directory-reporting-api-getting-started.md).

---

**D: Come ottenere una licenza Premium?**

**R:** vedere [Introduzione a Azure Active Directory Premium](active-directory-get-started-premium.md) per una domanda toothis di risposta.

---

**D: In quanto tempo è possibile visualizzare le attività dopo aver acquistato una licenza Premium?**

**R:** se si dispongono già dei dati di attività come una licenza gratuita, quindi è possibile visualizzare hello stessi dati. Se non si dispone di dati, saranno necessari uno o due giorni.

---

**D: È possibile visualizzare i dati del mese precedente dopo avere acquistato una licenza Azure AD Premium?**

**R:** se di recente si è passati versione Premium tooa (inclusi una versione di valutazione), è possibile visualizzare inizialmente dati backup too7 giorni. Quando i dati vengono accumulati, verranno visualizzati i giorni too30.

---

**Q: è un evento di rischio di protezione dell'identità, ma vengono non visualizzati Accedi corrispondente in hello tutti gli accessi. È normale?**

**R:** Sì, la protezione dell'identità valuta il rischio per tutti i flussi di autenticazione, sia interattivi che non interattivi. Tuttavia, tutti i report solo accessi Mostra solo hello accessi interattivi.

---

**D: come è possibile scaricare report "Utenti contrassegno i rischi" hello nel portale di Azure?**

**R:** toodownload opzione hello *utenti contrassegno i rischi* report verranno aggiunte presto.

---

**D: come si capisce perché un accesso o un utente è stato contrassegnato rischiose hello portale di Azure?**

**R:** clienti edizione Premium per altre informazioni su hello sottostante gli eventi di rischio, fare clic sull'utente hello in "Utenti contrassegno i rischi" o facendo clic su "Rischiosi accessi" hello. I clienti di edizione Free e Basic ottenere toosee agli utenti di rischio hello e accessi senza hello sottostante informazioni sugli eventi di rischio.

---

**D: come vengono calcolati gli indirizzi IP in accessi hello e report accessi rischiosa??**

**R:** gli indirizzi IP vengono rilasciati in modo che non sia disponibile alcuna connessione definitivo tra un indirizzo IP e in cui si trova fisicamente computer hello con tale indirizzo. Questo è complicato da fattori quali i provider di dispositivi mobili e VPN con il rilascio di indirizzi IP da pool centrale spesso molto distanti da dove dispositivo client hello viene effettivamente utilizzato. Dato hello precedente, la conversione di posizione fisica tooa di indirizzo IP è un lavoro migliore in base alle tracce, i dati del Registro di sistema, ricerche inverse e altre informazioni. 

---

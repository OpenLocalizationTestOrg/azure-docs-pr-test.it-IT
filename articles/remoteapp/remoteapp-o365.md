---
title: aaaUsing Office con Azure RemoteApp | Documenti Microsoft
description: Informazioni sull'interazione tra Office e Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Usare Office con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Sono disponibili due opzioni per l'hosting di applicazioni di Office in Azure RemoteApp: Office 365 ProPlus o la versione di valutazione di Office 2013 Professional Plus.

**Salve, non tutti sanno che è disponibile un nuovo articolo migliore che presto sostituirà questo attuale. Estrarre [come toouse l'abbonamento a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md). Vengono illustrate tutte le informazioni di hello che è necessario per l'uso di Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
È possibile creare una raccolta RemoteApp utilizzando l'immagine modello Office 365 ProPlus hello. Questa opzione consente di tooextend il tooRemoteApp servizio Office 365. È necessario disporre di un piano di sottoscrizione esistente e gli utenti devono avere una licenza per hello servizio Office 365 ProPlus, autonomo o tramite i piani di servizio hello Office 365.

RemoteApp supporta l'attivazione di computer condivisi di Office 365. Quando si abilitare l'attivazione di Computer condivisi e utilizzare hello [strumento di distribuzione di Office](http://www.microsoft.com/download/details.aspx?id=36778) per l'installazione, Office 365 ProPlus Installa senza essere attivato. Quando un utente accede a una raccolta che contiene Office 365, è necessario controllare toosee se è stato eseguito il provisioning utente hello per Office 365 ProPlus. Se in tal caso, Office attiva temporaneamente Office 365 ProPlus - questa attivazione viene mantenuto fino a quando i segnali che gli utenti fuori servizio hello.

toouse attivazione Computer condivise di Office 365, è necessario toocreate un [modello personalizzato](remoteapp-create-custom-image.md) e installare Office 365 ProPlus, seguendo [queste direzioni](https://technet.microsoft.com/library/dn782858.aspx).

È possibile gestire le licenze di Office 365 degli utenti in hello [il portale di amministrazione di Office 365](https://portal.office365.com/). Per altre informazioni, vedere la pagina relativa ai [piani di servizio di Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Versione di valutazione di Office 2013 Professional Plus
Durante la valutazione di 30 giorni di RemoteApp, è possibile usare hello Office 2013 Professional Plus (versione di valutazione) modello immagine toocreate una raccolta RemoteApp. È possibile assegnare gli utenti toothis valutazione insieme utilizzando gli account di lavoro di Azure Active Directory o un account di Microsoft. Non è necessaria una sottoscrizione aggiuntiva.

Si tratta di pneumatici di hello tookick un'opzione utilissima e avere una visione ottima per Office in RemoteApp. Questa opzione è però solo prevista per scopi di valutazione e di test. Le raccolte RemoteApp create utilizzando l'immagine modello di hello Office 2013 Professional Plus (versione di valutazione) non possono essere passato tooproduction modalità e verranno disabilitate al termine di hello del periodo di prova hello.

## <a name="switching-from-trial-tooproduction"></a>Il passaggio dalla versione di valutazione tooproduction
Quando si avvia la versione di valutazione gratuita di 30 giorni, una nota nella sezione RemoteApp del portale hello hello indicherà quanto tempo rimanenti in versione di valutazione di hello prima è necessario tooa tootransition a pagamento di account. È possibile attivare l'account e commutatore tooproduction la modalità di utilizzo collegamento hello in questa nota.

Quando si attiva l'account, questo influirà su tutte le raccolte RemoteApp hello nell'account.

* Le raccolte che sono in esecuzione con Windows Server 2012 R2 hello o immagini modello Office 365 ProPlus hello passerà tooproduction senza problemi. Tutti i dati e le impostazioni utente, comprese le sessioni in corso, rimarranno invariate.
* Se sono state caricate immagini modello personalizzate, anche la transizione delle raccolte che usano tali immagini avverrà facilmente e in modo trasparente.
* immagine di Hello Office 2013 Professional Plus (versione di valutazione) modello è destinato esclusivamente alla valutazione. Le raccolte in esecuzione con l'immagine modello non possono essere passato tooproduction. Queste raccolte verranno messe in stato di "disabilitazione".

Se non eseguire la transizione modalità tooproduction scadenza hello della versione di valutazione, verranno disabilitate le raccolte RemoteApp. Non occorre preoccuparsi: le impostazioni e dati utente vengono salvati per un altro 90 giorni, in modo non è ancora possibile attivare la modalità di tooproduction e commutatore senza alcuna perdita di dati.


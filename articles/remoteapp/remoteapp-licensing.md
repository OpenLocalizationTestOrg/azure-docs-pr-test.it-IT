---
title: licenze RemoteApp aaaAzure | Documenti Microsoft
description: Informazioni sul funzionamento delle licenze in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Funzionamento delle licenze in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Pertanto, hai configurato il servizio di Azure RemoteApp, creato i modelli e sono pronti toopublish App tooyour utenti. Ma è ancora uno toofigure cosa ultimo out: gestione delle licenze. Solo come funziona sulle licenze per connessione RemoteApp e App hello che si condivide tramite RemoteApp?

RemoteApp non richiede licenze Windows o licenze CAL per Desktop remoto. La sottoscrizione si occupa di hello lato RemoteApp stesso. (Vedere i dettagli di hello di hello [piani tariffari](https://azure.microsoft.com/pricing/details/remoteapp).)

Se si utilizza una delle immagini hello incluso nella sottoscrizione, è possibile condividere le app di hello installate su quell'immagine senza la necessità di una licenza separata. Ad esempio, se si utilizza hello Windows Server 2012 R2 modello immagine toobuild la raccolta, è possibile condividere System Center Endpoint Protection con gli utenti. Hello solo eccezioni toothis regola sono Office 365 ProPlus, che richiede una sottoscrizione separata, e Office 2013, che non possono essere condivisi in una raccolta di produzione.

Se si desidera toouse hello Office 365 modello immagine che viene fornito con RemoteApp, è necessario che un *esistente* Office 365 ProPlus piano. Hello che lo stesso vale per qualsiasi app di Office 365 di pubblicare un modello personalizzato. È necessario tooactivate hello App con la propria sottoscrizione. Questo vale sia per le sottoscrizioni di valutazione che per quelle a pagamento. Se si desidera l'immagine modello di Office 365 hello toouse durante la valutazione di hello, *e si dispone già di una sottoscrizione*, andare troppo toohello Office 365 pagina[iscriversi](https://go.microsoft.com/fwlink/p/?LinkID=403802) per una sottoscrizione di valutazione. Per altre informazioni, vedere la pagina relativa al [funzionamento di RemoteApp e Office in combinazione](remoteapp-o365.md) .

Se, durante il periodo di valutazione di hello, non si desidera sottoscrizione di valutazione di Office 365 tooget, utilizzare l'immagine di modello di Office 2013 Professional Plus hello dotato di RemoteApp. Questa immagine modello può essere usata solo per 30 giorni e non può essere convertita in una raccolta a pagamento.

Per altre applicazioni, è necessario assicurarsi di disporre di hello licenza tooshare hello app toomake.

Riassumendo, È possibile pubblicare qualsiasi app che si ha diritto legalmente tooshare. Ed è necessario che sia effettivamente toomake intitolata tooshare programmi.

Si noti che non è possibile usare una licenza CAL o un contratto multilicenza in una raccolta nel cloud. Si *possibile* utilizzare un'applicazione di tooactivate contratto multilicenza nella raccolta ibrida (ad eccezione di Office). È sufficiente tooinstall sul modello di immagine da hello supporti Volume License. Seguire le informazioni di hello di licenze di tooinstall fornitore dell'applicazione hello in un ambiente di Desktop remoto.


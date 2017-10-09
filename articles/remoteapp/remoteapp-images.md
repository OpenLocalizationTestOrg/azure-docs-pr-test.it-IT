---
title: aaaWhat si trova in immagini modello RemoteApp di Azure di hello? | Microsoft Docs
description: Informazioni sulle immagini modello hello incluse con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Che cos'è immagini modello RemoteApp di Azure di hello?
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

La sottoscrizione di Azure RemoteApp include tre immagini modello:

* Windows Server 2012
* Microsoft Office 365 ProPlus (richiede una sottoscrizione di Office 365)
* Microsoft Office 2013 Professional Plus (solo versione di valutazione)

> [!IMPORTANT]
> La sottoscrizione di Azure RemoteApp consente di accedere software toohello nelle immagini di hello, con l'eccezione hello di Office 365 ProPlus, che richiede una sottoscrizione separata, e Office 2013, non può essere utilizzato nell'ambiente di produzione. Ciò significa che è possibile condividere i programmi hello o App sulle immagini modello hello con gli utenti. Ad esempio, se si crea una raccolta che usi l'immagine di Windows Server 2012 R2 hello, è possibile pubblicare System Center Endpoint Protection per gli utenti tooaccess tramite RemoteApp.
> 
> Estrarre hello [RemoteApp licenze dettagli](remoteapp-licensing.md) per ulteriori informazioni. E [utilizzando Office con Azure RemoteApp](remoteapp-o365.md) per hello informazioni sulle licenze di Office.
> 
> 

Di seguito sono riportati i dettagli sul contenuto di ogni immagine.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ("hello vaniglia immagine")
Questa immagine è basata su sistema operativo Microsoft Windows Server 2012 R2 Datacenter e hello seguenti ruoli e funzionalità installati toomeet requisiti di hello per le immagini modello RemoteApp di Azure:

* .NET Framework 4.5, 3.5.1, 3.5
* Esperienza desktop
* Servizi di riconoscimento della grafia
* Media Foundation
* Host sessione Desktop remoto.
* Windows PowerShell 4.0
* Windows PowerShell ISE
* Supporto WoW64

Questa immagine presenta anche hello seguendo le applicazioni installate:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (sottoscrizione necessaria)
Office 365 è hello più applicazione richiesta, pertanto è creata un'immagine di "custom" toowork con.

Questa immagine è un'estensione dell'immagine di vaniglia hello e hello seguenti componenti di Microsoft Office 365 ProPlus installato inoltre componenti toohello descritti nell'immagine di Windows Server 2012 R2 hello:

* Accesso
* Excel
* Lync
* OneNote
* OneDrive for Business (si noti che l'agente di sincronizzazione hello non è supportato per l'utilizzo con Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Strumenti di correzione di Microsoft Office

immagine di Hello include anche Visio Pro e progetto Pro.

E hello applicazioni, di seguito:

* SQL Native client
* Driver ODBC
* Client di data mining di SQL Server
* Client MasterDataServices
* Microsoft Publisher
* PowerQuery
* PowerMap

La piena funzionalità delle app di Office 365 ProPlus è disponibile solo per gli utenti che dispongono di un piano di Office 365 ProPlus. Per ulteriori informazioni sulla sottoscrizione di Office 365 hello vedere piani [i piani di servizio di Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). Altre domande? Estrarre hello [Office 365 + RemoteApp](remoteapp-o365.md) informazioni. Controllare inoltre il nuovo articolo hello, [come toouse l'abbonamento a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md).

Si noti che è necessario toolicense Office 365 ProPlus Visio Pro e progetto Pro separatamente, ognuna di esse presenta la propria licenza.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (solo versione di valutazione)
Durante il periodo di valutazione gratuita di hello, è possibile testare il servizio di hello con immagine di hello Office 2013.

Questa immagine è un'estensione dell'immagine di vaniglia hello e hello seguenti componenti di Microsoft Office 2013 Professional Plus installato inoltre componenti toohello descritti nell'immagine di Windows Server 2012 R2 hello:

* Accesso
* Excel
* Lync
* OneNote
* OneDrive for Business (si noti che l'agente di sincronizzazione hello non è supportato per l'utilizzo con Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Strumenti di correzione di Microsoft Office

> [!IMPORTANT]
> **Informazioni legali** : questa immagine non include una licenza di Microsoft Office e *non può essere usata per ambienti di produzione*. immagine di Office 2013 Professional Plus Hello è solo per uso versione di valutazione. Se si desidera toouse Office App in Azure RemoteApp per la produzione, è necessario l'immagine di Office 365 ProPlus hello toouse. Per altre informazioni sulla licenza di Office, vedere [Usare Office 365 con Azure RemoteApp](remoteapp-o365.md)
> 
> 


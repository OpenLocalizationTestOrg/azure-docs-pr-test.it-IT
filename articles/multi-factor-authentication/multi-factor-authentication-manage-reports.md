---
title: report di utilizzo e aaaAccess per Azure MFA | Documenti Microsoft
description: "Descrive come toouse hello funzionalità di Azure multi-Factor Authentication - report."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Report in Azure Multi-Factor Authentication
Azure Multi-Factor Authentication offre diversi report che possono essere utilizzati dall'utente e dall'organizzazione. Questi report sono accessibili tramite il portale di gestione di multi-Factor Authentication hello. Hello seguito è riportato un elenco di report disponibili hello:

| Report | Descrizione |
|:--- |:--- |
| Utilizzo |utilizzo di Hello report visualizza informazioni sull'utilizzo complessivo, riepilogo utenti e i dettagli dell'utente. |
| Stato server |Questo report visualizza lo stato di hello dei server di multi-Factor Authentication associati all'account. |
| Cronologia utenti bloccati |Questi report mostrano la cronologia di hello di richieste tooblock o sblocco degli utenti. |
| Cronologia utenti bypass |Mostra la cronologia hello di richieste toobypass multi-Factor Authentication per il numero di telefono dell'utente. |
| Avviso di illecito |Mostra una cronologia degli avvisi di illecito inviati durante l'intervallo di date hello specificato. |
| Queued |Consente di elencare i report accodati da elaborare e i relativi stati. Un report di hello toodownload o della vista di collegamento è disponibile quando viene completata hello del report. |

## <a name="view-reports"></a>Visualizzazione dei report
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Hello sinistra, selezionare Active Directory.
3. Attenersi a una di queste due opzioni, a seconda che vengano usati provider di autenticazione:
   * **Opzione 1**: fare clic sulla scheda provider multi-Factor Authentication hello. Selezionare il provider di autenticazione a più fattori e fare clic su hello **Gestisci** pulsante nella parte inferiore di hello.
   * **Opzione 2**: selezionare il toohello directory e andare **configura** scheda. Hello multi-factor authentication, selezionare nella sezione **Gestisci impostazioni servizio**. Nella parte inferiore di hello della pagina di impostazioni di servizio di autenticazione a più fattori hello, fare clic su hello Go toohello collegamento del portale.
4. Nel portale di gestione di Azure multi-Factor Authentication hello, selezionare il tipo di hello di report che si desidera hello **visualizzare un Report** sezione hello riquadro di spostamento sinistro.

<center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center>


**Risorse aggiuntive**

* [Per gli utenti](end-user/multi-factor-authentication-end-user.md)
* [Azure Multi-Factor Authentication su MSDN](https://msdn.microsoft.com/library/azure/dn249471.aspx)

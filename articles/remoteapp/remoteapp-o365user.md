---
title: aaaHow toouse Azure RemoteApp con gli account utente di Office 365 | Documenti Microsoft
description: Informazioni su come toouse Azure RemoteApp con l'account utente di Office 365
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Come toouse Azure RemoteApp con gli account utente di Office 365
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Se si dispone di una sottoscrizione Office 365, si dispone di Azure Active Directory che archivia i nomi utente e password utilizzati tooaccess servizi di Office 365. Ad esempio, quando gli utenti attivano Office 365 ProPlus autenticano contro toocheck di Azure AD per le licenze. La maggior parte dei clienti potrebbero ad esempio toouse hello stessa directory con Azure RemoteApp.

Se si distribuisce Azure RemoteApp, è molto probabile che venga usata una sottoscrizione di Azure associata a un Azure AD diverso. In ordine toouse la directory di Office 365, sarà necessario toomove hello sottoscrizione di Azure in tale directory.

Per informazioni su come le applicazioni client toodeploy Office 365, vedere [come toouse l'abbonamento a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Fase 1: Registrare la sottoscrizione gratuita di Office 365 Azure Active Directory
Se si utilizza hello portale di Azure classico, utilizzare i passaggi di hello in [registrare la sottoscrizione di Azure Active Directory gratuita](https://technet.microsoft.com/library/dn832618.aspx) tooget tooyour di accesso amministrativo AD Azure tramite il portale di gestione di Azure hello. Come risultato di hello di questo processo si deve essere in grado di toolog nel portale di Azure hello e vedere la directory non esiste: a questo punto non verrà visualizzato molto più poiché hello sottoscrizione di Azure completo in uso con Azure RemoteApp è in una directory diversa.

Memorizza nome hello e la password dell'account di amministratore hello creato in questo passaggio, saranno necessari nella fase 2.

Se si utilizza hello portale di Azure, consultare [come tooregister e attivare un gratuita di Azure Active Directory tramite il portale di Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Fase 2: Hello modifica AD Azure associata alla sottoscrizione di Azure.
Verrà toochange la sottoscrizione di Azure dalla directory corrente nella directory di Office 365 hello che è utilizzati nella fase 1.

Seguire le istruzioni di hello descritte [tenant di Azure Active Directory modifica hello in Azure RemoteApp](remoteapp-changetenant.md). È necessario prestare particolare attenzione toohello alla procedura seguente:

* Passaggio 1: Se è stato distribuito Azure RemoteApp (ARA) nella sottoscrizione, assicurarsi di rimuovere innanzitutto tutti gli account utente di Azure AD da qualsiasi raccolta ARA, prima di qualsiasi altra operazione. In alternativa, è possibile valutare l’eliminazione delle raccolte esistenti.
* Passaggio 2: Questo è un passaggio critico. È necessario un account Microsoft toouse (ad esempio @outlook.com) come un amministratore del servizio nella sottoscrizione hello; infatti, non abbiamo tutti gli account utente da hello esistente sottoscrizione di Azure AD collegato toohello – in questo caso, non sarà in grado di toomove è tooa di Azure AD.
* Passaggio &#4;: Quando si aggiunge una directory esistente, sistema hello chiederà toosign con account di amministratore hello per tale directory. Verificare che account di amministratore hello toouse dalla fase 1.
* Passaggio &#5;: Cambiare directory padre hello della directory di Office 365 tooyour sottoscrizione hello. risultato finale Hello necessario che in Impostazioni -> Sottoscrizioni sottoscrizione Elenca directory hello Office 365. 
  ![Spostarsi nella directory padre hello di sottoscrizione hello](./media/remoteapp-o365user/settings.png)

A questo punto la sottoscrizione di Azure RemoteApp è associata il Office 365, Azure AD; con Azure RemoteApp, è possibile utilizzare account utente di Office 365 esistente hello!


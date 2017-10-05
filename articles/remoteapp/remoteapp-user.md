---
title: Aggiungere un utente alla raccolta di Azure RemoteApp | Microsoft Docs
description: Informazioni su come aggiungere utenti alla raccolta di Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a>Come aggiungere un utente alla raccolta di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Prima che gli utenti possano visualizzare e usare le app in Azure RemoteApp, è necessario concedere loro l'accesso alla raccolta. Questo è estremamente semplice: nella scheda **Accesso utente** immettere le informazioni relative all'account dell'utente e quindi fare clic sul segno di spunta.

Quali informazioni sull'account sono necessarie? Dipende dal tipo di raccolta creata (cloud o ibrida) e dall'uso o meno di Office 365 ProPlus in tale raccolta.

## <a name="supported-user-identities"></a>Identità degli utenti supportate
I diversi tipi di raccolta (cloud e ibridi) supportano l'uso di diverse identità utente per l'accesso alle applicazioni.  

Per una raccolta ibrida di RemoteApp, è necessario configurare un'infrastruttura di dominio Active Directory locale e un tenant di Azure Active Directory con l'integrazione della directory (e, facoltativamente, Single Sign-On). Inoltre, è necessario creare alcuni oggetti Active Directory nella directory locale.  

Per una raccolta nel cloud di RemoteApp, a tutti gli utenti che dispongono di identità di supporto per Azure Active Directory è possibile concedere l'accesso utente a RemoteApp in modo che comprenda gli account Microsoft.  Vedere la tabella riportata di seguito.

Gli utenti di Office 365 sono utenti di Azure Active Directory. Agli utenti che dispongono di account ibridi con sincronizzazione della directory di Azure Active Directory è possibile concedere l'accesso utente in una distribuzione ibrida di RemoteApp.   

È possibile usare questa tabella come riferimento rapido per le identità supportate nella propria raccolta e per i requisiti di Active Directory.

| Account utente | Cloud | Ibrido |
| --- | --- | --- |
| Account Microsoft |Sì |No |
| Azure Active Directory (Azure AD) | | |
| Solo cloud Azure AD |Sì |No |
| Sincronizzazione Active Directory con sincronizzazione password |Sì |Sì |
| Sincronizzazione Active Directory senza sincronizzazione password |Sì |No |
| Sincronizzazione Active Directory con ADFS |Sì |sì |
| [Provider di identità di terze parti supportati da Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx), ad esempio Ping |sì |Sì |
| Autenticazione a più fattori |Sì |Sì |

Per [altre informazioni](remoteapp-ad.md) , vedere Configurare Azure Active Directory per RemoteApp.

> [!NOTE]
> Gli utenti di Azure Active Directory devono provenire dal tenant associato alla sottoscrizione. (è possibile visualizzare e modificare la sottoscrizione nella scheda **Impostazioni** nel portale. Per altre informazioni, vedere l'articolo relativo alla [modifica del tenant di Azure Active Directory usato da RemoteApp](remoteapp-changetenant.md) ).
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informazioni sugli account utente di Office 365 ProPlus
Se si usa l'immagine modello di Office 365 ProPlus nella raccolta *o* se è stata creata un'immagine personalizzata che usa Office 365, è possibile solo aggiungere gli utenti di Azure Active Directory che dispongono di sottoscrizioni a Office 365 per il dominio predefinito della sottoscrizione. Per altre informazioni, vedere l'articolo relativo all' [uso di Office 365 con Azure RemoteApp](remoteapp-o365.md) .


---
title: aaaSetting aggiunta di Azure AD per gli utenti | Documenti Microsoft
description: Viene illustrato come gli amministratori possono configurare Aggiunta da Azure AD per la directory locale e la registrazione del dispositivo.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Configurazione di Aggiunta ad Azure AD nell'organizzazione
Prima di configurare Azure Active Directory Join (aggiunta di Azure AD), si desidera eseguire la sincronizzazione tooeither configurare la directory locale del cloud toohello utenti oppure creare manualmente gli account gestiti in Azure AD.

Istruzioni dettagliate per la sincronizzazione del tooAzure gli utenti locali Active Directory è trattata nella [integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

toomanually creare e gestire gli utenti in Azure AD, fare riferimento troppo[Gestione utenti in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Configurare la registrazione dei dispositivi
1. Accedere toohello portale di Azure come amministratore.
2. Nel riquadro sinistro di hello selezionare **Active Directory**.
3. In hello **Directory** scheda, selezionare la directory.
4. Seleziona hello **configura** scheda.
5. Passare toohello **dispositivi** sezione.
6. In hello **dispositivi** scheda, impostare hello seguenti:  
   * **MASSIMO numero di dispositivi PER utente**: selezionare hello il numero massimo di dispositivi che un utente può disporre di Azure AD.  Se un utente raggiunge questa quota, non sarà in grado di tooadd altri dispositivi fino alla rimozione di uno o più dispositivi esistenti.
   * **TooJOIN multi-FACTOR Authentication RICHIEDENDO dispositivi**: specificare se gli utenti sono necessari tooprovide una seconda autenticazione fattori toojoin loro tooAzure dispositivo Active Directory. Per ulteriori informazioni su Azure multi-Factor Authentication, vedere [Introduzione ad Azure multi-Factor Authentication nel cloud hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **Gli utenti possono AZURE AD aggiungere dispositivi**: selezionare hello utenti e gruppi che sono consentiti toojoin dispositivi tooAzure Active Directory.
   * **I dispositivi aggiunti AD altri amministratori ON AZURE**: con Azure AD Premium o hello Enterprise Mobility Suite (EMS), è possibile scegliere gli utenti che dispongono di diritti di amministratore locale toohello dispositivo. Per impostazione predefinita, agli amministratori globali e ai proprietari dei dispositivi vengono sempre concessi i diritti di amministratore locale.

<center>![Configurare la registrazione dei dispositivi](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

Dopo aver impostato l'aggiunta di Azure AD per gli utenti, è possibile connettere tooAzure AD tramite aziendale o dispositivi personali.

Di seguito sono tre scenari hello è possibile utilizzare il tooset utenti tooenable aggiunta di Azure AD:

* Gli utenti di aggiungere un dispositivo di proprietà dell'azienda direttamente tooAzure Active Directory.
* Toohello dispositivo aggiunta al dominio una proprietà dell'azienda di utenti Active Directory locale, quindi estesa hello dispositivo tooAzure Active Directory.
* Gli utenti di aggiungere lavoro o scuola account tooWindows su un dispositivo personale

## <a name="additional-information"></a>Informazioni aggiuntive
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)


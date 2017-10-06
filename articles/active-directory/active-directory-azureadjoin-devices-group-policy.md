---
title: si verifica nel aaaConnect tooAzure di dispositivi appartenenti a un dominio Active Directory per Windows 10 | Documenti Microsoft
description: Viene illustrato come gli amministratori possono configurare rete di criteri di gruppo tooenable dispositivi toobe toohello dominio aziendale.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10
Aggiunta a un dominio è organizzazioni modalità tradizionale hello avere stabilito la connessione di dispositivi per lavoro hello ultimi 15 anni e altro ancora. È abilitato toosign utenti nei dispositivi tootheir utilizzando il proprio lavoro di Windows Server Active Directory (Active Directory) o scuola e consentiti toofully IT di gestire questi dispositivi. Le organizzazioni si basano su metodi tooprovision dispositivi toousers imaging e in genere utilizzare criteri di gruppo o System Center Configuration Manager (SCCM) toomanage li.


Aggiunta a un dominio Windows 10 vengono fornite hello seguenti vantaggi dopo aver connesso i dispositivi tooAzure Active Directory (Azure AD):

* Single sign-on (SSO) tooAzure AD risorse da qualsiasi posizione
* Accedere a toohello enterprise, Windows Store utilizzando lavoro o scuola account (necessari account di Microsoft)
* Roaming delle impostazioni utente tra dispositivi conforme ai criteri dell'organizzazione usando account aziendali o dell'istituto di istruzione, non è necessario un account Microsoft.
* Autenticazione avanzata e pratico accesso all'account aziendale o dell'istituto di istruzione con Windows Hello for Business e Windows Hello
* Toorestrict possibilità di accedere solo toodevices conformi con le impostazioni di criteri di gruppo di dispositivi aziendali

## <a name="prerequisites"></a>Prerequisiti
Aggiunta a un dominio continua toobe utile. Tuttavia, tooget i vantaggi di hello Azure AD di SSO, il roaming delle impostazioni con o lavoro o scuola account e accedere tooWindows archivio con lavoro o scuola account, sarà necessario hello seguenti:

* Sottoscrizione di Azure AD
* Azure AD Connect tooextend hello locale tooAzure di directory Active Directory
* Criteri impostati tooconnect tooAzure di dispositivi appartenenti a un dominio Active Directory
* Build di Windows 10 (build 10551 o successiva) per i dispositivi.

tooenable Windows Hello for Business e di Windows Hello, è necessario anche seguenti hello:

- **Infrastruttura a chiave pubblica (PKI)** per il rilascio di certificati utente.

- **System Center Configuration Manager Current Branch** -è necessario tooinstall versione 1606 o migliori.  
Per altre informazioni, vedere: 
    - [Documentazione per System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Blog del team di System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Impostazioni di Windows Hello for Business in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Come requisito distribuzione PKI toohello alternativo, è possibile eseguire il seguente hello:

* Disporre di alcuni controller di dominio con Servizi di dominio Active Directory di Windows Server 2016.

tooenable l'accesso condizionale, è possibile creare le impostazioni di criteri di gruppo che consentono di accedere ai dispositivi aggiunti a un toodomain con nessun altre distribuzioni. controllo di accesso toomanage basata sulla conformità del dispositivo hello, sarà necessario seguente hello:

* System Center Configuration Manager Current Branch (1606 o versione successiva) per scenari Windows Hello for Business

## <a name="deployment-instructions"></a>Istruzioni per la distribuzione

toodeploy, seguire la procedura seguente hello elencata in [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Passaggio successivo
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)


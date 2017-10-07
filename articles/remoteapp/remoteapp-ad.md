---
title: aaaAzure AD + requisiti di Active Directory per Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooset backup toowork di Active Directory con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Azure AD + requisiti di Active Directory per Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Per la raccolta ibrida di RemoteApp di Azure o per una raccolta di cloud che si desidera toofederate con Active Directory Connect, è necessario seguente hello toodo.

### <a name="connect-azure-ad-and-active-directory"></a>Connettersi AD Azure e ad Active Directory
Se si desidera tooconnect tenant di Azure AD e gli ambienti di Active Directory locale, utilizzare AD Connect. Verranno visualizzate solo [4 clic](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello due directory.

Nota - la sincronizzazione delle Directory è necessaria per le raccolte ibride.

### <a name="make-sure-your-domaincom-match"></a>Controllare la corrispondenza del valore "@domain.com"
Prima di iniziare, verificare che tale hello UPN per il suffisso di hello corrispondenze foresta locale del dominio di Azure AD. 

Dopo aver configurato il suffisso di dominio UPN hello in Azure AD, tutti gli utenti che accedono in Azure RemoteApp vengono registrati come "utente @<hello suffix you set up>." Assicurarsi che gli utenti possono anche accedere con hello stesso user@suffix nel dominio locale hello. In alcuni casi è possibile impostare un nome di dominio in Azure AD quando si specifica un suffisso di dominio diverso per hello utente in locale. In questo caso, gli utenti sarà in grado di tooconnect tooany dominio computer o alle risorse tramite Azure RemoteApp.

Se, ad esempio, impostare il suffisso di dominio UPN in AAD come contoso.com, ma alcuni utenti in locale o Active Directory sono configurati toolog con @contoso.uk, gli utenti non saranno hello raccolta ARA toocorrectly in grado di accedere. Gli utenti che UPN in AAD e Active Directory deve essere uguale hello per le possibili toobe account di accesso di hello"

### <a name="create-objects-for-azure-remoteapp"></a>Creare gli oggetti per RemoteApp di Azure
È inoltre necessario hello toocreate seguendo gli oggetti di Active Directory locale:

* Un account servizio tooprovide accesso toodomain alle risorse per i programmi RemoteApp creando un join di dominio locale toohello punti finali di host sessione Desktop remoto.
* Un'unità organizzativa (OU) toocontain RemoteApp gli oggetti macchina. Utilizzo di hello unità Organizzativa è account hello tooisolate consigliata (ma non obbligatorio) e i criteri che verranno utilizzati con RemoteApp.

È necessario entrambi gli oggetti quando si crea la raccolta RemoteApp, pertanto è necessario che toodo questi passaggi prima.


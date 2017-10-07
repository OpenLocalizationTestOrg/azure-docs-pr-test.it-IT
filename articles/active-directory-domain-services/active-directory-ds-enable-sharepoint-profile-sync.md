---
title: 'Servizi di dominio di Azure Active Directory: Abilitare il supporto per il servizio profilo utente di SharePoint | Documentazione Microsoft'
description: Configurare la sincronizzazione dei profili toosupport domini gestiti Azure Active Directory Domain Services per SharePoint Server
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Configurare la sincronizzazione di profilo toosupport un dominio gestito di SharePoint Server
SharePoint Server include un servizio profili utente utilizzato per la sincronizzazione dei profili utente. tooset backup hello servizio profili utente, le autorizzazioni appropriate necessario toobe concesse per un dominio Active Directory. Per ulteriori informazioni, vedere [Concedere a Servizi di dominio di Active Directory le autorizzazioni per la sincronizzazione dei profili in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

In questo articolo viene illustrato come è possibile configurare i servizio di sincronizzazione dei profili utente di SharePoint Server di servizi di dominio Active Directory di Azure domini gestiti toodeploy hello.

## <a name="hello-aad-dc-service-accounts-group"></a>gruppo 'Account di servizio controller di dominio di AAD' Hello
Un gruppo di sicurezza denominato '**gli account del servizio controller di dominio AAD**' è disponibile all'interno di hello 'Utenti' unità organizzativa nel dominio gestito. È possibile visualizzare questo gruppo di hello **Active Directory Users and Computers** snap-in MMC nel dominio gestito.

![Il gruppo di sicurezza AAD DC Service Accounts](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

I membri di questo gruppo di sicurezza sono delegata hello seguenti privilegi:
- il privilegio 'Replica delle modifiche di Directory' Hello nella directory principale di hello DSE di hello gestiti dominio.
- il privilegio 'Replica delle modifiche di Directory' nel contesto dei nomi di configurazione hello Hello (cn = contenitore della configurazione) di hello gestito dominio.

Questo gruppo di sicurezza è anche un membro del gruppo incorporato hello **l'accesso compatibile precedente a Windows 2000**.

![Il gruppo di sicurezza AAD DC Service Accounts](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Abilitare la sincronizzazione dei profili utente di SharePoint Server di toosupport dominio gestito
È possibile aggiungere l'account di servizio hello usato per toohello sincronizzazione profilo utente di SharePoint **gli account del servizio controller di dominio AAD** gruppo. Di conseguenza, l'account di sincronizzazione hello Ottiene directory toohello modifiche tooreplicate di privilegi adeguati. Questo passaggio di configurazione consente correttamente toowork sincronizzazione profilo utente di SharePoint Server.

![AAD DC Service Accounts - aggiunta di membri](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - aggiunta di membri](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Contenuti correlati
* [Riferimento tecnico - Concedere a Servizi di dominio di Active Directory le autorizzazioni per la sincronizzazione dei profili in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)

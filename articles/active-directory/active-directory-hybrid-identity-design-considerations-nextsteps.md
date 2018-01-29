---
title: "Considerazioni di progettazione per la soluzione ibrida di gestione delle identità di Azure Active Directory: passaggi successivi | Documentazione Microsoft"
description: "Riepilogo e passaggi successivi dopo la lettura della guida sulla progettazione dell'identità ibrida"
documentationcenter: 
services: active-directory
author: billmath
manager: mtillman
editor: 
ms.assetid: 02d48768-ea9e-4bfe-ae54-b54c4bd0a789
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 29c045af81134847321d9ef69943f0154e9ee5a0
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations--next-steps"></a>Considerazioni di progettazione dell'identità ibrida di Azure Active Directory - Passaggi successivi
Dopo aver definito i requisiti ed esaminato tutte le opzioni per la soluzione di gestione dei dispositivi mobili, è possibile eseguire i passaggi successivi per la distribuzione dell'infrastruttura di supporto adatta alle esigenze dell'utente e dell'organizzazione.

## <a name="hybrid-identity-solutions"></a>Soluzioni di identità ibrida
-Sfruttare i vantaggi offerti da scenari di soluzioni adatti alle proprie esigenze è un ottimo modo per verificare e pianificare i dettagli della distribuzione di un'infrastruttura di gestione dei dispositivi mobili. Le soluzioni seguenti descrivono molti dei più comuni scenari di gestione dei dispositivi mobili:

* La [soluzione per la gestione di dispositivi mobili e PC negli ambienti aziendali](https://technet.microsoft.com/library/dn582037.aspx) consente di gestire i dispositivi mobili estendendo l'infrastruttura di System Center 2012 Configuration Manager locale nel cloud con Microsoft Intune. Questa infrastruttura ibrida consente ai professionisti IT in ambienti di medie e grandi dimensioni di abilitare BYOD e accesso remoto riducendo la complessità amministrativa.
* La [soluzione per la gestione di dispositivi mobili per Configuration Manager 2007](https://technet.microsoft.com/library/dn508400.aspx) consente di gestire i dispositivi mobili quando l'infrastruttura si trova su System Center Configuration Manager 2007. Questa soluzione illustra come configurare un singolo server che esegue System Center 2012 Configuration Manager, in questo modo è possibile quindi eseguire Microsoft Intune e sfruttare la capacità MDM.
* La [soluzione per la gestione dei dispositivi mobili negli ambienti di piccole dimensioni](https://technet.microsoft.com/library/dn715906.aspx) è destinata alle piccole aziende che devono supportare MDM. Illustra come usare Microsoft Intune per estendere l'infrastruttura corrente per il supporto della gestione dei dispositivi mobili e BYOD. Questa soluzione descrive lo scenario più semplice supportato per l'uso di Microsoft Intune in una configurazione autonoma, solo cloud senza server locali.

## <a name="hybrid-identity-documentation"></a>Documentazione di identità ibrida
I contenuti concettuali, sulla pianificazione delle procedure, sulla distribuzione e sull'amministrazione sono utili quando si implementa la soluzione di gestione dei dispositivi mobili:

* [Microsoft System Center](https://technet.microsoft.com/library/cc507089.aspx) consentono di acquisizione e consolidare le conoscenze su infrastruttura, criteri, processi e procedure consigliate in modo che il personale IT possa creare sistemi gestibili e automatizzare le operazioni.
* [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) è un servizio di gestione di dispositivi basato sul cloud che consente di gestire computer e dispositivi mobili e proteggere le informazioni della società.
* [MDM per Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) consente di gestire e proteggere i dispositivi mobili quando sono connessi all'organizzazione di Office 365. È possibile usare MDM per Office 365 per impostare regole di accesso e criteri di sicurezza dei dispositivi e per cancellare i dispositivi mobili, se vengono persi o rubati.

## <a name="hybrid-identity-resources"></a>Risorse di identità ibrida
Il monitoraggio frequente di queste risorse consente di ottenere informazioni sulle notizie più recenti e aggiornamenti relativi alle soluzioni di gestione dei dispositivi mobili:

* [Blog di Microsoft Enterprise Mobility](http://blogs.technet.com/b/enterprisemobility/)
* [Blog di Microsoft In The Cloud](http://blogs.technet.com/b/in_the_cloud/)
* [Blog di Microsoft Intune](http://blogs.technet.com/b/microsoftintune/)
* [Blog di Microsoft System Center Configuration Manager](http://blogs.technet.com/b/configurationmgr/)
* [Blog del team di Microsoft System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/)

## <a name="see-also"></a>Vedere anche 
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)


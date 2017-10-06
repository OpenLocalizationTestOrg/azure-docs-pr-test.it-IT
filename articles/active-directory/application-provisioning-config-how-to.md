---
title: applicazione raccolta tooan AD Azure il provisioning degli utenti aaaHow tooconfigure | Documenti Microsoft
description: "Come è possibile configurare rapidamente account utente di provisioning e deprovisioning tooapplications già nella raccolta di Azure Active Directory dell'applicazione hello"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>Come utente tooconfigure provisioning applicazione raccolta tooan Azure AD

*Provisioning dell'account utente* è hello atto della creazione, aggiornamento e/o la disabilitazione di record di account utente nell'archivio profili utente locale di un'applicazione. La maggior parte dei cloud e le applicazioni SaaS archiviano hello utenti ruoli e le autorizzazioni in un proprio archivio di profilo utente locale e la presenza di tale record utente nell'archivio locale è *obbligatorio* per single sign-on e accesso di toowork.

Nel portale di Azure hello, hello **Provisioning** scheda nel riquadro di spostamento a sinistra di hello per un'applicazione aziendale vengono visualizzate le modalità di provisioning sono supportate per l'app. Può essere uno dei due valori:

## <a name="configuring-an-application-for-manual-provisioning"></a>Configurazione di un'applicazione per il Provisioning manuale

*Manuale* provisioning significa che gli account utente devono essere creati manualmente utilizzando i metodi di hello forniti da tale app. Potrebbe essere necessario accedere a un portale amministrativo dell'applicazione e aggiungere gli utenti usando un'interfaccia utente basata sul Web. Oppure caricare un foglio di calcolo con i dettagli degli account utente, usando un meccanismo fornito dall'applicazione. Consultare la documentazione di hello fornite da app hello, o contatto hello sono disponibili meccanismi di sviluppatore toodetermine wat.

Se manuale è in modalità solo hello visualizzato per una determinata applicazione, significa che non automatico AD Azure provisioning connettore è ancora stata creata per l'applicazione hello. O significa app di hello non non supporto hello utente prerequisito API di gestione al quale toobuild un connettore di provisioning automatico.

Se si desidera supporto toorequest per il provisioning automatico per un'applicazione specificata, è possibile compilare una richiesta di <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Configurazione di un'applicazione per il Provisioning automatico

*Automatico* significa che è stato sviluppato un connettore di provisioning Azure AD per l'applicazione. Per ulteriori informazioni su hello Azure AD, il provisioning di servizio e il relativo funzionamento, vedere [tooSaaS automatizzare Provisioning e Deprovisioning applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Per ulteriori informazioni su utenti specifici tooprovision e l'applicazione di tooan gruppi, vedere [la gestione di provisioning dell'account utente per applicazioni aziendali](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

Hello tooenable necessari passaggi effettivi e configurare il provisioning automatico variano a seconda dell'applicazione hello.

>[!NOTE]
>È consigliabile iniziare dalla ricerca hello toosetting specifico dell'esercitazione di programma di installazione di provisioning per l'applicazione e seguenti tooconfigure tali passaggi app hello sia Azure AD toocreate hello connessione provisioning. 
>
>

Esercitazioni di App sono reperibile in [elenco di esercitazioni sulla procedura tooIntegrate App SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Tooconsider una cosa importante quando l'impostazione di provisioning essere tooreview e configurare i mapping degli attributi hello e flussi di lavoro che definiscono quale flusso di proprietà utente (o gruppo) dall'applicazione toohello Azure AD. Ciò include l'impostazione di hello "proprietà corrispondente" che toouniquely utilizzati da identificare e corrisponde agli utenti o i gruppi tra i sistemi di hello due. Per altre informazioni su questo processo importante.

## <a name="next-steps"></a>Passaggi successivi
[Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)


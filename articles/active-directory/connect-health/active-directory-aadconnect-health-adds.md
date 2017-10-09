---
title: Azure AD Connect Health con AD DS aaaUsing | Documenti Microsoft
description: "Si tratta hello Azure AD Connect Health pagina verrà illustrate le modalità toomonitor di dominio Active Directory."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Uso di Azure AD Connect Health con Servizi di dominio Active Directory
Hello seguente documentazione è toomonitoring specifico Active Directory Domain Services con Azure AD Connect Health. versioni supportata di Hello di dominio Active Directory sono: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.

Per altre informazioni sul monitoraggio di AD FS con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md). Per informazioni sul monitoraggio di Azure Active Directory Connect (Sincronizzazione) con Azure AD Connect Health, vedere [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md).

![Azure AD Connect Health per Servizi di dominio Active Directory](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Avvisi di Azure AD Connect Health per Servizi di dominio Active Directory
salve sezione avvisi all'interno di Azure AD Connect Health per AD DS, si fornisce un elenco di avvisi attivi e risolti, il controller di dominio tooyour correlati. Selezione di un avviso attivo o risolto apre un nuovo pannello con altre informazioni, insieme a procedure di risoluzione e collegamenti toosupporting documentazione. Ogni tipo di avviso può avere una o più istanze, che corrispondono tooeach hello dei controller di dominio interessati da quel particolare avviso. Nella parte inferiore di hello della pannello avviso hello, fare doppio clic un tooopen di controller di dominio interessato un pannello con altre informazioni dettagliate su tale istanza di avviso aggiuntivo.

All'interno di questo pannello, è possibile abilitare le notifiche di posta elettronica per avvisi e modificare l'intervallo di tempo di hello nella visualizzazione. Espande l'intervallo di tempo hello consente avvisi risolti precedenti toosee.

![Errore del servizio di sincronizzazione Azure AD Connect](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Dashboard dei controller di dominio
Questo dashboard offre una visualizzazione topologica dell'ambiente, oltre a metriche operative chiave e allo stato di integrità di ogni controller di dominio monitorato. le metriche Hello presentato identificare tooquickly, qualsiasi controller di dominio che potrebbero richiedere ulteriori indagini. Per impostazione predefinita, viene visualizzato solo un subset di colonne hello. Tuttavia, è possibile trovare l'intero set di colonne disponibili di hello facendo doppio clic sul comando colonne hello. La selezione delle colonne hello che è più rilevante, attiva il dashboard in un unico e facile inserire integrità hello tooview dell'ambiente di dominio Active Directory.

![Controller di dominio](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

I controller di dominio possono essere raggruppati in base al rispettivo dominio o un sito, è utile per comprendere topologia dell'ambiente hello. Infine, se si fa doppio clic sull'intestazione di blade hello, dashboard hello Ottimizza tooutilize hello-schermi disponibili. La visualizzazione più grande è utile quando vengono mostrate più colonne.

## <a name="replication-status-dashboard"></a>Dashboard Stato replica
Questo dashboard fornisce una visualizzazione hello replica e lo stato di topologia di replica del controller di dominio monitorati. stato Hello del tentativo di replica più recente di hello è elencato, insieme a documentazione utile per qualsiasi errore che viene trovato. È possibile fare doppio clic su un controller di dominio con un errore, un nuovo pannello con informazioni tooopen, ad esempio: informazioni dettagliate sull'errore hello, consigliata di procedure di risoluzione e collegamenti a documentazione tootroubleshooting.

![Stato replica](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Monitoraggio
Questa funzionalità fornisce grafica delle tendenze di diversi contatori delle prestazioni, che vengono sempre raccolti da ogni controller di dominio monitorato hello. Le prestazioni di un controller di dominio possono essere facilmente confrontate con quelle di tutti gli altri controller di dominio monitorati nella foresta. È inoltre possibile visualizzare più contatori delle prestazioni affiancati; ciò è utile durante la risoluzione dei problemi nell'ambiente.

![Monitoraggio](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Per impostazione predefinita, è stata preselezionata quattro contatori di prestazioni. Tuttavia, è possibile includere altri menu Filtro hello e selezionando o deselezionando i contatori di prestazioni desiderati. Inoltre, è possibile fare doppio clic su tooopen di graph un contatore delle prestazioni un nuovo pannello, che include i punti dati per ogni controller di dominio monitorato hello.

## <a name="related-links"></a>Collegamenti correlati
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installazione dell'agente di Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operazioni di Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md)
* [Domande frequenti su Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Cronologia delle versioni di Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)


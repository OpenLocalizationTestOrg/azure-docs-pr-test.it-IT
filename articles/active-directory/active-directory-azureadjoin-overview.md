---
title: "dispositivi di tooWindows 10 funzionalità cloud aaaExtending tramite Azure Active Directory Join | Documenti Microsoft"
description: Fornisce una panoramica dettagliata di come i dispositivi Windows 10 possono utilizzare aggiunta ad Azure AD tooget registrato in Azure Active Directory.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join
## <a name="what-is-azure-active-directory-join"></a>Informazioni su Aggiunta ad Azure Active Directory
Azure Active Directory Join (aggiunta di Azure AD) è una funzionalità hello che registra un dispositivo di proprietà dell'azienda nella gestione di Azure Active Directory tooenable centralizzata del dispositivo hello. Rende possibile per gli utenti, ad esempio dipendenti studenti tooconnect toohello enterprise cloud e tramite Azure Active Directory. In questo modo semplificato le distribuzioni di Windows e accesso tooorganizational App e risorse da qualsiasi dispositivo Windows, sia aziendali e personali (BYOD).

Aggiunta ad Azure AD è destinato alle aziende basate prima di tutto o esclusivamente sul cloud, in genere piccole e medie imprese che non hanno un'infrastruttura Windows Server Active Directory locale. Che aggiunta AD Azure, detto possibile e verrà inoltre essere utilizzati da organizzazioni di grandi dimensioni nei dispositivi che sono in grado di eseguire un join tradizionale dominio (i dispositivi mobili, ad esempio), oppure per gli utenti che necessitano principalmente tooaccess Office 365 o altre applicazioni SaaS integrate con Azure AD.

Sebbene l'aggiunta al dominio tradizionale hello offre ancora hello locale migliore esperienza nei dispositivi che sono in grado di un join di dominio, aggiunta ad Azure AD è adatto per i dispositivi che non sono aggiunta a un dominio. Aggiunta ad Azure AD è anche adatto per la gestione degli utenti nel cloud hello. usando funzionalità di gestione di dispositivi mobili anziché attraverso strumenti di gestione del dominio tradizionali, come Criteri di gruppo e System Center Configuration Manager (SCCM).

![Panoramica dei dispositivi aziendali e dei dispositivi personali con Azure AD e Active Directory in locale](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Vantaggi dell'adozione di Aggiunta ad Azure AD
* **Le aziende che sono in gran parte in hello cloud**: se è stato spostato o si sta spostando tooa modello in cui si sta riducendo il footprint locale e si desidera più nel cloud hello toooperate, aggiunta di Azure AD possono trarre vantaggio è. Gli account Azure AD creati manualmente o con la sincronizzazione di Active Directory in locale In entrambi i casi, si dispone di un account di Azure AD ed è possibile utilizzarlo toosign in tooWindows 10. Gli utenti possono creare un join tooAzure i computer Active Directory tramite l'esperienza di out-of-box hello (configurazione guidata) o tramite il menu di impostazioni hello. Dopo l'aggiunta, gli utenti utilizzeranno single sign-on (SSO) accesso toocloud risorse come Office 365, nel browser o nelle applicazioni di Office.
* **Istituti**: uno degli scenari di hello abbiamo ricevuto spesso sui è che istituti di istruzione sono due tipi di utente: studenti e docenti. I membri di istituti di istruzione vengono considerati appartenenti a lungo termine organizzazione hello, pertanto è sempre consigliabile creare gli account locali per tali. Tuttavia, gli studenti sono shorter-term membri dell'organizzazione hello e pertanto possono essere gestiti in Azure AD. Ciò significa che può essere inserita scala directory cloud toohello anziché archiviata in locale. Significa anche che studenti possano accedere tooWindows con gli account di Azure AD e ottenere l'accesso alle risorse di 365 tooOffice, nel browser o nelle applicazioni di Office.
* **Le aziende di vendita al dettaglio**: un altro scenario abbiamo saputo sui clienti è i desiderio toomanage stagionale più facilmente.  Anche in questo caso, è possibile creare account locali per i dipendenti a tempo pieno con contratti a lungo termine in computer aggiunti a un dominio. Ma stagionale appartengono shorter-term org hello, pertanto è consigliabile toomanage li in cui le licenze utente possono essere più facilmente spostate. La creazione di questi account utente nel cloud hello con licenze di Office 365 consente hello utenti tooget hello vantaggi accesso tooWindows e applicazioni di Office con un account di Azure AD. e offre ai datori di lavoro una maggiore flessibilità con le relative licenze al termine della collaborazione.
* **Altre aziende**: l'aggiunta degli utenti ad Azure AD può rappresentare un vantaggio anche se si gestiscono gli utenti nell'istanza di Active Directory locale. Azure AD, infatti, semplifica notevolmente l'esperienza di aggiunta, la gestione efficiente dei dispositivi e la registrazione per la gestione di dispositivi mobili automatica, oltre a offrire funzionalità Single Sign-On per le risorse locali e di Azure AD.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Funzionalità offerte da Aggiunta di Azure AD
Con l'aggiunta di Azure AD, verrà restituito il seguente di hello:

* **Il provisioning automatico dei dispositivi di proprietà dell'azienda**: con Windows 10, gli utenti possono configurare un nuovo dispositivo preallocano esperienza out-of-box hello, senza coinvolgere IT.
* **Supporto per fattori di forma moderna**: aggiunta AD Azure funziona anche su dispositivi che non hanno dominio tradizionale hello aggiungere funzionalità.  
* **Supporto per gli account aziendali esistenti**: gli utenti non è più necessario toocreate e gestire un un tooget di account Microsoft personale hello un'esperienza ottimale su dispositivi rilasciato da società, come avveniva con Windows 8. Possono usare l'account aziendale esistente in Azure AD. Per molte organizzazioni, ciò significa essenzialmente che gli utenti possono configurare e accedere tooWindows con hello stesso credenziali che usano tooaccess Office 365.
* **Registrazione per la gestione automatica dei dispositivi mobili**: i dispositivi possono essere registrati automaticamente in Gestione dei dispositivi mobili quando si è connessi AD tooAzure. Il processo funziona con Microsoft Intune e soluzioni partner di gestione di dispositivi mobili. Quando la gestione dei dispositivi è terminata con Intune, gli amministratori IT possono monitor/gestire i dispositivi aggiunti AD Azure insieme ai dispositivi aggiunti a un dominio nella console di gestione di hello SCCM.
* **Single sign-on toocompany risorse**: gli utenti ottengono accesso single sign-on da tooapps desktop di Windows hello e risorse nel cloud di hello, ad esempio Office 365 e migliaia di applicazioni di business che si basano su Azure AD per l'autenticazione tramite [Di azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). I dispositivi di proprietà dell'azienda che vengono unite in join tooAzure AD sfruttare le risorse locali tooon SSO anche quando il dispositivo di hello non è in una rete aziendale e da qualsiasi posizione queste risorse vengono esposte tramite hello [Proxy dell'applicazione AD Azure](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **Roaming dello stato del sistema operativo**: impostazioni di accessibilità, siti Web, password Wi-Fi e altre impostazioni vengono sincronizzati in tutti i dispositivi di proprietà della società senza la necessità di un account Microsoft personale.
* **Aziendale di Windows Store**: hello Windows Store supporta l'acquisizione di app e di licenza con l'account di Azure AD. Le organizzazioni possono App contratti multilicenza e renderli disponibili toohello utenti nella propria organizzazione.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Differenze di funzionamento dei dispositivi con Aggiunta ad Azure AD
| Dispositivi aziendali (dominio locale tooon unita in join) | Dispositivi aziendali (cloud toohello unita in join) | Dispositivo personale |
| --- | --- | --- |
| Gli utenti possono accedere a Windows con le credenziali dell'account aziendale, come già accade attualmente. |Gli utenti possono accedere tooWindows con le credenziali di lavoro che sono gestite in Azure AD. Questo riguarda i dispositivi aziendali in tre scenari: <ol><li>Hello organizzazione non dispone di Active Directory in locale (ad esempio, una piccola azienda).</li><li>organizzazione di Hello non è possibile creare tutti gli account utente in Active Directory (ad esempio, gli account per studenti, consulenti o stagionali non vengono creati in Active Directory).</li><li>organizzazione di Hello dispone di dispositivi aziendali che non possono essere unita in join tooan (locale) dominio, quali telefoni e Tablet che eseguono uno SKU di dispositivi mobili (ad esempio, un dispositivo secondaria eseguita tooa factory/retail piano).</li></ol> Aggiunta ad Azure AD supporta l'aggiunta di dispositivi aziendali per le organizzazioni federate e quelle gestite. |Gli utenti accedono tooWindows con le credenziali dell'account Microsoft personale (nessun cambiamento). |
| Gli utenti hanno accesso tooroaming impostazioni ed enterprise di hello Windows Store. Questi servizi funzionano con gli account aziendali e non richiedono un account Microsoft personale. Questa operazione richiede le organizzazioni tooconnect loro tooAzure di Active Directory locale AD. |Gli utenti possono eseguire la configurazione self-service. Possono passare tramite hello prima esecuzione (FRX) tramite l'account aziendale come un'alternativa toohaving IT hello il provisioning dei dispositivi, anche se entrambi i metodi sono supportati. |Gli utenti possono aggiungere facilmente un account aziendale gestito in Active Directory o Azure AD. |
| Gli utenti hanno il possibilità SSO da app desktop toowork hello, siti Web e di risorse, sia alle risorse locali e le app cloud che usano Azure AD per l'autenticazione. |I dispositivi vengono registrati automaticamente nella directory dell'organizzazione hello (Azure AD) e registrati automaticamente in Gestione dei dispositivi mobili. Questa è una funzionalità di Azure AD Premium. |Gli utenti hanno il possibilità SSO tutte le App e toowebsites/risorse con questo account aziendale. |
| Gli utenti possono aggiungere loro tooaccess di account Microsoft personale immagini personali e i file senza conseguenze per i dati aziendali. (Impostazioni di roaming continuano toowork con l'account aziendale). account Microsoft Hello consente SSO e non è più unità hello roaming delle impostazioni. |Gli utenti possono eseguire una reimpostazione password self-service su winlogon, vale a dire che possono reimpostare una password dimenticata. Questa è una funzionalità di Azure AD Premium. |Gli utenti hanno accesso toohello enterprise Windows Store in modo che possano acquisire e usare le app line-of-business dai dispositivi personali. |

## <a name="additional-information"></a>Informazioni aggiuntive
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticazione delle identità senza password con Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)


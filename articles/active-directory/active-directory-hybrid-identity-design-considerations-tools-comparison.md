---
title: "Confronto degli strumenti di integrazione directory per la soluzione ibrida di gestione delle identità | Microsoft Docs"
description: Questa pagina fornisce una tabella completa che confronta hello vari strumenti di integrazione di directory che possono essere utilizzati per l'integrazione di directory.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Confronto degli strumenti di integrazione directory per la soluzione ibrida di gestione delle identità
Negli anni hello gli strumenti di integrazione directory hello hanno crescita e l'evoluzione.  Questo documento è toohelp forniscono una visualizzazione consolidata di questi strumenti e un confronto delle funzionalità di hello che sono disponibili in ciascuno.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect include funzionalità precedentemente rilasciate come Dirsync e AAD Sync e componenti hello. Questi strumenti non vengono non è più rilasciati singolarmente e tutti i futuri miglioramenti verranno inclusi in aggiornamenti tooAzure AD connettersi, in modo da sapere sempre dove tooget hello funzionalità più recenti.
> 
> DirSync e Azure AD Sync sono funzionalità deprecate. Altre informazioni sono disponibili [qui](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

Utilizzare hello seguente chiave per ognuna delle tabelle di hello.

● = Disponibile  
VF = Versione futura  
AP = Anteprima pubblica  

## <a name="on-premises-toocloud-synchronization"></a>TooCloud sincronizzazione locale
| Funzionalità | Azure Active Directory Connect | Servizi di sincronizzazione di Azure Active Directory (AAD Sync) | Strumento di sincronizzazione di Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Connettersi toosingle foresta di Active Directory locale |● |● |● |● |● |
| Connettersi toomultiple locale foreste Active Directory |● |● | |● |● |
| Connettersi toomultiple organizzazioni di Exchange in locale |● | | | | |
| La connessione di directory LDAP di toosingle locale |VF | | |● |● |
| Connettersi toomultiple nelle directory LDAP locale |VF | | |● |● |
| La connessione locale tooon AD e le directory LDAP locali |VF | | |● |● |
| Connettere i sistemi toocustom (ad esempio SQL, Oracle, MySQL e così via) |VF | | |● |● |
| Sincronizzazione di attributi definiti dall'utente (estensioni della directory) |● | | | | |
| Connettersi HR tooon locale (ad esempio, SAP, Oracle e-business, PeopleSoft) |VF | | |● |● |
| Supporta le regole di sincronizzazione FIM e connettori per i sistemi locali tooon il provisioning. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>Sincronizzazione locale tooOn cloud
| Funzionalità | Azure Active Directory Connect | Servizi di sincronizzazione di Azure Active Directory | Strumento di sincronizzazione di Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Writeback di dispositivi |● | |● | | |
| Writeback degli attributi (per una distribuzione ibrida di Exchange) |● |● |● |● |● |
| Writeback di oggetti gruppo |● | | | | |
| Writeback delle password (da password reimpostate autonomamente e modificate) |● |● | | | |

## <a name="authentication-feature-support"></a>Supporto delle funzionalità di autenticazione
| Funzionalità | Azure Active Directory Connect | Servizi di sincronizzazione di Azure Active Directory | Strumento di sincronizzazione di Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Sincronizzazione delle password per una singola foresta AD locale |● |● |● | | |
| Sincronizzazione delle password per più foreste AD locali |● |● | | | |
| Single Sign-On con federazione |● |● |● |● |● |
| Writeback delle password (da password reimpostate autonomamente e modificate) |● |● | | | |

## <a name="set-up-and-installation"></a>Configurazione e installazione
| Funzionalità | Azure Active Directory Connect | Servizi di sincronizzazione di Azure Active Directory | Strumento di sincronizzazione di Azure Active Directory (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Supporta l'installazione in un controller di dominio |● |● |● | |
| Supporta l'installazione con SQL Express |● |● |● | |
| Aggiornamento facile da DirSync |● | | | |
| Localizzazione di tooWindows Admin UX lingue del Server |● |● |● | |
| Localizzazione di utente finale UX tooWindows lingue del Server | | | |● |
| Supporto per Windows Server 2008 e Windows Server 2008 R2 |● per la sincronizzazione, non per la federazione |● |● |● |
| Supporto per Windows Server 2012 e Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filtro e configurazione
| Funzionalità | Azure Active Directory Connect | Servizi di sincronizzazione di Azure Active Directory | Strumento di sincronizzazione di Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Filtro di domini e unità organizzative |● |● |● |● |● |
| Filtro in base ai valori di attributo degli oggetti |● |● |● |● |● |
| Consentire a un set minimo di sincronizzato toobe attributi (MinSync) |● |● | | | |
| Consenti toobe di modelli di servizio diverso applicato per i flussi di attributi |● |● | | | |
| Consentire la rimozione di attributi da passano dal tooAzure AD Active Directory |● |● | | | |
| Personalizzazione avanzata dei flussi di attributi |● |● | |● |● |

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).


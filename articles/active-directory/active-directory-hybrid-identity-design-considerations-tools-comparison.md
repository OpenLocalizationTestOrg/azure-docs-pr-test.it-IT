---
title: "Confronto degli strumenti di integrazione directory per la soluzione ibrida di gestione delle identità | Microsoft Docs"
description: Questa pagina contiene tabelle complete che confrontano i vari strumenti che possono essere usati per l'integrazione directory.
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/09/2018
ms.author: billmath
ms.openlocfilehash: 78ca910b4dfd5a706d2f1df7f70291fb48f096f5
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/11/2018
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Confronto degli strumenti di integrazione directory per la soluzione ibrida di gestione delle identità
Nel corso degli anni gli strumenti di integrazione di directory sono aumentati e si sono evoluti.  Questo documento offre una panoramica consolidata di questi strumenti e un confronto delle funzionalità disponibili in ognuno.

<!-- The hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect include i componenti e le funzionalità resi disponibili in precedenza come DirSync e AAD Sync. Questi strumenti non vengono più resi disponibili singolarmente e tutti i miglioramenti futuri verranno inclusi negli aggiornamenti per Azure AD Connect, in modo da poter individuare sempre da dove ottenere la funzionalità più aggiornata.
> 
> DirSync e Azure AD Sync sono funzionalità deprecate. Altre informazioni sono disponibili [qui](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

Usare la seguente chiave per ognuna delle tabelle.

● = Disponibile  
VF = Versione futura  
AP = Anteprima pubblica  

## <a name="on-premises-to-cloud-synchronization"></a>Sincronizzazione da locale a cloud
| Funzionalità | Azure Active Directory Connect | Servizi di sincronizzazione di Azure Active Directory (AAD Sync) | Strumento di sincronizzazione di Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Connessione a singola foresta AD locale |● |● |● |● |● |
| Connessione a più foreste AD locali |● |● | |● |● |
| Connessione a più organizzazioni di Exchange |● | | | | |
| Connessione a singola directory LDAP locale |●* | | |● |● |
| Connessione a più directory LDAP locali |●*  | | |● |● |
| Connessione a più directory AD locali e LDAP locali |●* | | |● |● |
| Connessione a sistemi personalizzati (ad esempio, SQL, Oracle, MySQL e così via) |VF | | |● |● |
| Sincronizzazione di attributi definiti dall'utente (estensioni della directory) |● | | | | |
| Connessione alle risorse umane locali (ad esempio, SAP, Oracle eBusiness, PeopleSoft) |VF | | |● |● |
| Supporto delle regole di sincronizzazione FIM e dei connettori per il provisioning ai sistemi locali. | | | |● |● |
&#42; Attualmente, sono supportate due opzioni.  Sono:
   1. È possibile usare il connettore LDAP generico e abilitarlo all'esterno di Azure AD Connect.  Questa opzione è complessa e richiede un partner per l'onboarding e un contratto di supporto tecnico Premier per la gestione.  Questa opzione consente di gestire directory LDAP singole o multiple.
   2. È possibile sviluppare soluzioni personalizzate per lo spostamento di oggetti da LDAP ad Active Directory.  Sincronizzare quindi gli oggetti con Azure AD Connect.  È possibile usare MIM o FIM come soluzioni per lo spostamento di oggetti.

## <a name="cloud-to-on-premises-synchronization"></a>Sincronizzazione da cloud a locale
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
| Localizzazione dell'esperienza utente per l'amministratore nelle lingue di Windows Server |● |● |● | |
| Localizzazione dell'esperienza utente per l'utente finale nelle lingue di Windows Server | | | |● |
| Supporto per Windows Server 2008 e Windows Server 2008 R2 |● per la sincronizzazione, non per la federazione |● |● |● |
| Supporto per Windows Server 2012 e Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filtro e configurazione
| Funzionalità | Azure Active Directory Connect | Servizi di sincronizzazione di Azure Active Directory | Strumento di sincronizzazione di Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Filtro di domini e unità organizzative |● |● |● |● |● |
| Filtro in base ai valori di attributo degli oggetti |● |● |● |● |● |
| Possibilità di sincronizzare un set minimo di attributi (MinSync) |● |● | | | |
| Possibilità di applicare differenti modelli di servizio ai flussi di attributi |● |● | | | |
| Possibilità di interrompere il flusso di attributi da AD ad Azure AD |● |● | | | |
| Personalizzazione avanzata dei flussi di attributi |● |● | |● |● |

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).


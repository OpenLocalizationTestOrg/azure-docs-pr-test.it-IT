---
title: Riferimento al protocollo SAML AD aaaAzure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica dei profili di Single Sign-On e Single Sign-Out SAML hello in Azure Active Directory.
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: priyamo
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: d712289b16dc40a6b43a96fadef729c55cdaac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Utilizzo di protocollo SAML hello Azure Active Directory
Azure Active Directory (Azure AD) utilizza hello SAML 2.0 protocollo tooenable tooprovide single sign-on esperienza tootheir utenti applicazioni. Hello [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) e [Single Sign-Out](active-directory-single-sign-out-protocol-reference.md) profili SAML di Azure AD viene illustrato l'utilizzo di asserzioni SAML, protocolli e le associazioni nel servizio del provider di identità hello.

Protocollo SAML richiede che il provider di identità hello (Azure AD) e informazioni di tooexchange hello service provider (un'applicazione hello) su se stesse.

Quando un'applicazione viene registrata con Azure AD, sviluppatore di app hello registra le informazioni correlate alla federazione con Azure AD. Ciò include hello **URI di reindirizzamento** e **Metadata URI** dell'applicazione hello.

Azure AD Usa hello **Metadata URI** di hello tooretrieve servizio cloud di hello URI del servizio cloud hello di disconnessione hello e di chiave di firma. Se un'applicazione hello non supporta un URI dei metadati, hello sviluppatore deve contattare il Microsoft supporto tooprovide hello logout URI e chiave di firma.

Azure Active Directory espone endpoint di Single Sign-On e Single Sign-Out specifici del tenant e comuni (indipendenti dal tenant). Questi URL rappresentano percorsi indirizzabili, non sono solo identificatori, è quindi possibile passare toohello endpoint tooread hello metadati.

* endpoint Hello specifico del Tenant si trova in `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Hello <TenantDomainName> segnaposto rappresenta un nome di dominio registrato o il GUID TenantID di un tenant di Azure AD. Ad esempio, si trova hello metadati della federazione di tenant contoso.com hello: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* endpoint indipendente dal Tenant Hello si trova in `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. In questo indirizzo dell'endpoint, **comuni** viene visualizzata, anziché un nome di dominio tenant o ID.

Per informazioni sui documenti di metadati di federazione hello in Azure AD pubblica, vedere [i metadati della federazione](active-directory-federation-metadata.md).

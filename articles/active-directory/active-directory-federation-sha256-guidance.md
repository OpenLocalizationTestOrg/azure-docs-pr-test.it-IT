---
title: algoritmo hash della firma aaaChange per Office 365 trust della relying party | Documenti Microsoft
description: Questa pagina fornisce le linee guida per la modifica dell'algoritmo SHA per il trust federativo con Office 365
keywords: SHA1,SHA256,O365,federazione,aadconnect,adfs,ad fs,modifica algoritmo hash della firma,trust federativo,trust della relying party
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Modificare l'algoritmo hash della firma relativo al trust della relying party di Office 365
## <a name="overview"></a>Panoramica
Active Directory Federation Services (ADFS) firma relativo tooensure di Azure Active Directory tooMicrosoft i token che non possa essere manomessa. Questa firma può essere basata sull'algoritmo SHA1 o SHA256. Azure Active Directory supporta ora i token firmati con un algoritmo SHA256, ed è consigliabile impostare hello tooSHA256 algoritmo di firma di token per il livello più alto di hello di sicurezza. Questo articolo descrive i passaggi di hello necessari toohello di algoritmo di firma di token hello tooset più sicuro il livello SHA256.

>[!NOTE]
>Microsoft consiglia l'utilizzo di SHA256 come algoritmo di hello per la firma di token è più sicuro rispetto a SHA1 ma SHA1 rimane comunque un'opzione supportata.

## <a name="change-hello-token-signing-algorithm"></a>Modificare l'algoritmo di firma di token hello
Dopo aver impostato l'algoritmo di firma hello con uno dei hello due processi, AD FS firma token hello per Office 365 trust della relying party con SHA256. Non è necessario di tutte le modifiche di configurazione aggiuntive toomake e questa modifica non ha alcun impatto sul tooaccess possibilità Office 365 o di altre applicazioni di Azure AD.

### <a name="ad-fs-management-console"></a>Console di gestione di AD FS
1. Aprire console di gestione di hello AD ADFS nel server di hello primario AD FS.
2. Espandere il nodo di hello AD FS e fare clic su **Relying Party Trusts**.
3. Fare clic con il pulsante destro del mouse sul trust della relying party di Office 365/Azure e scegliere **Proprietà**.
4. Seleziona hello **avanzate** scheda e l'algoritmo hash protetto hello selezionare SHA256.
5. Fare clic su **OK**.

![Algoritmo di firma SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>Cmdlet di AD FS PowerShell
1. Aprire PowerShell da qualsiasi server AD FS con privilegi di amministratore.
2. Algoritmo hash protetto di hello set tramite hello **Set-AdfsRelyingPartyTrust** cmdlet.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>Vedere anche
* [Ripristinare il trust di Office 365 con Azure AD Connect](connect/active-directory-aadconnect-federation-management.md#repairthetrust)


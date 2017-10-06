---
title: "scenari di aaaAdvanced con autenticazione a più fattori di Azure e VPN di terze parti"
description: Guide dettagliate per la configurazione per Azure MFA toointegrate con Cisco, Citrix e Juniper.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Scenari avanzati con Azure Multi-Factor Authentication e soluzioni VPN di terze parti
Azure multi-Factor Authentication può essere utilizzato tooseamlessly connettersi con diverse soluzioni VPN di terze parti. Questo articolo è incentrato su dispositivo VPN di ASA Cisco®, un accessorio VPN SSL NetScaler di Citrix e hello Juniper reti Secure accesso/Pulse Secure connessione protetta SSL dispositivo VPN. Abbiamo creato configuration Guide tooaddress queste Appliance comuni tre, ma Server multi-Factor Authentication è possibile integrare con la maggior parte dei sistemi che utilizzano RADIUS, LDAP, IIS o l'autenticazione basata sulle attestazioni tooAD ADFS. Per informazioni più dettagliate, vedere la sezione relativa alle [configurazioni del server Multi-Factor Authentication](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Dispositivo VPN Cisco ASA e Azure Multi-Factor Authentication
Azure multi-Factor Authentication si integra con la VPN di ASA Cisco® accessorio tooprovide una sicurezza aggiuntiva per gli account di accesso Cisco AnyConnect® VPN e accesso al portale.  Questa operazione può essere eseguita utilizzando un protocollo LDAP o RADIUS hello.  Consente di selezionare una delle seguenti toodownload hello dettagliate dettagliate per la configurazione di hello.

| Guida alla configurazione | Descrizione |
| --- | --- |
| [Configurazione del dispositivo VPN Cisco ASA con Anyconnect e Azure MFA per LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Integrare il dispositivo VPN Cisco ASA con Azure MFA tramite LDAP |
| [Configurazione del dispositivo VPN Cisco ASA con Anyconnect e Azure MFA per RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Integrare il dispositivo VPN Cisco ASA con Azure MFA tramite RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>Dispositivo VPN Citrix NetScaler SSL e Azure Multi-Factor Authentication
Azure multi-Factor Authentication si integra con la sicurezza aggiuntiva di tooprovide accessorio VPN SSL NetScaler di Citrix per gli account di accesso di Citrix NetScaler SSL VPN e accesso al portale.  Questa operazione può essere eseguita utilizzando un protocollo LDAP o RADIUS hello.  Consente di selezionare una delle seguenti toodownload hello dettagliate dettagliate per la configurazione di hello.

| Guida alla configurazione | Descrizione |
| --- | --- |
| [Configurazione del dispositivo VPN SSL Citrix NetScaler e Azure MFA per LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Integrare il dispositivo VPN SSL Citrix NetScaler con Azure MFA tramite LDAP |
| [Configurazione del dispositivo VPN SSL Citrix NetScaler e Azure MFA per RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Integrare il dispositivo VPN SSL Citrix NetScaler con Azure MFA tramite RADIUS |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Client VPN SSL Juniper/Pulse Secure e Azure Multi-Factor Authentication
Azure multi-Factor Authentication si integra con la sicurezza aggiuntiva di tooprovide accessorio Juniper/Pulse Secure SSL VPN per gli account di accesso Juniper/Pulse Secure SSL VPN e accesso al portale.  Questa operazione può essere eseguita utilizzando un protocollo LDAP o RADIUS hello.  Consente di selezionare una delle seguenti toodownload hello dettagliate dettagliate per la configurazione di hello.

| Guida alla configurazione | Descrizione |
| --- | --- |
| [Configurazione del client VPN SSA Juniper/Pulse Secure e Azure MFA per LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Integrare il client VPN SSL Juniper/Pulse Secure con Azure MFA tramite LDAP |
| [Configurazione del client VPN SSA Juniper/Pulse Secure e Azure MFA per RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Integrare il client VPN SSL Juniper/Pulse Secure con Azure MFA tramite RADIUS |

## <a name="next-steps"></a>Passaggi successivi

- [Aumentare l'infrastruttura di autenticazione esistente con estensione dei criteri di rete hello Azure multi-Factor Authentication](multi-factor-authentication-nps-extension.md)

- [Configurare le impostazioni di Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md)
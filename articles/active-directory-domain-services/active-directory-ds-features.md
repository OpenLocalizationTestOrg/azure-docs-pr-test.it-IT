---
title: "Azure Active Directory Domain Services: funzionalità | Microsoft Docs"
description: "Funzionalità di Servizi di dominio Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Servizi di dominio Azure Active Directory
## <a name="features"></a>Funzionalità
Hello seguenti caratteristiche sono disponibile nei domini dei servizi di dominio Azure Active Directory gestiti.

* **Esperienza di distribuzione semplice:** bastano pochi clic per abilitare Servizi di dominio Azure AD per il tenant di Azure AD. È possibile eseguire velocemente il provisioning del dominio gestito, indipendentemente dal fatto che il tenant di Azure AD sia basato sul cloud o sincronizzato con la directory locale.
* **Supporto per l'aggiunta al dominio:** è facilmente possibile computer aggiunta al dominio hello il dominio gestito è disponibile nella rete virtuale di Azure. esperienza di aggiunta al dominio Hello in Windows client e Server di sistemi operativi funziona perfettamente con domini serviti da servizi di dominio Active Directory di Azure. È inoltre possibile usare gli strumenti automatizzati per l'aggiunta al dominio per questi domini.
* **Una sola istanza di dominio per ogni directory di Azure AD:** è possibile creare un singolo dominio di Active Directory per ogni directory di Azure AD.
* **Creare domini con nomi personalizzati**: è possibile creare domini con nomi personalizzati, ad esempio "contoso100.com", tramite Servizi di dominio Azure AD. È possibile usare i nomi di dominio sia verificati che non verificati. Facoltativamente, è possibile creare un dominio con il suffisso di dominio predefinito hello (ovvero, ' *. c o m ') offerto da directory di Azure AD.
* **Integrate con Azure AD:** non necessario tooconfigure o gestire la replica di servizi di dominio Active Directory tooAzure. Gli account utente, le appartenenze ai gruppi e le credenziali utente (password) dalla directory di Azure AD sono automaticamente disponibili in Servizi di dominio Azure AD. Nuovi utenti, gruppi o modifiche tooattributes dal tenant di Azure AD o la directory locale sono automaticamente sincronizzati tooAzure AD servizi di dominio.
* **Autenticazione NTLM e Kerberos:** con il supporto per l'autenticazione NTLM e Kerberos, è possibile distribuire applicazioni basate sull'autenticazione integrata di Windows.
* **Usare le credenziali e/o le password aziendali:** le password degli utenti nel tenant di Azure AD sono valide per Servizi di dominio Azure AD. Gli utenti possono utilizzare le proprie macchine toodomain join credenziali aziendali, accedere in modo interattivo o tramite desktop remoto e autenticare dominio gestito hello.
* **Supporto di lettura di binding LDAP & LDAP:** è possibile utilizzare le applicazioni basate su LDAP associa gli utenti di tooauthenticate nei domini serviti da servizi di dominio Active Directory di Azure. Inoltre, le applicazioni che utilizzano LDAP gli attributi di utente/computer tooquery dalla directory hello possono inoltre funzionare nei servizi di dominio Active Directory di Azure di operazioni di lettura.
* **LDAP sicuro (LDAPS):** è possibile abilitare l'accesso toohello directory tramite LDAP sicuro (LDAPS). L'accesso LDAP sicuro è disponibile in rete virtuale di hello per impostazione predefinita. Tuttavia, è possibile abilitare facoltativamente l'accesso LDAP sicuro tramite hello internet.
* **Criteri di gruppo:** è possibile usare un singola incorporata oggetto Criteri di gruppo ogni per hello utenti e computer di conformità tooenforce contenitori con i criteri di sicurezza necessarie per gli account utente e computer appartenenti a un dominio. È anche possibile creare propri oggetti Criteri di gruppo personalizzate e assegnare loro le unità organizzative toocustom troppo[gestire criteri di gruppo](active-directory-ds-admin-guide-administer-group-policy.md).
* **Gestire DNS:** i membri del gruppo 'Administrators di controller di dominio di AAD' hello possono gestire DNS per il dominio gestito tramite amministrazione DNS familiarità degli strumenti, ad esempio hello snap-in MMC di amministrazione DNS.
* **Creare unità organizzative (OU) personalizzato:** i membri del gruppo 'Administrators di controller di dominio di AAD' hello è possono creare unità organizzative personalizzate nel dominio gestito hello. A questi utenti vengono concessi privilegi amministrativi completi sulle unità organizzative personalizzate e quindi possono aggiungere e rimuovere account di servizio, computer, gruppi e così via all'interno di queste unità organizzative personalizzate.
* **Disponibile in più aree di Azure:** hello vedere [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/) tooknow pagina hello aree di Azure in cui sono disponibili servizi di dominio di Azure AD.
* **Disponibilità elevata:** Servizi di dominio Azure AD offre un'elevata disponibilità per il dominio. Questa funzionalità offre garanzia hello del servizio tempo di attività e della resilienza toofailures superiore. Predefiniti di monitoraggio offerte monitoraggio e aggiornamento automatizzato dagli errori adottando nuove istanze di tooreplace non riuscito di istanze e tooprovide continua del servizio per il dominio.
* **Utilizzare gli strumenti di gestione familiarità:** è possibile utilizzare strumenti di gestione di Windows Server Active Directory comuni, ad esempio i domini gestiti tooadminister centro di amministrazione di Active Directory o Active Directory PowerShell hello.

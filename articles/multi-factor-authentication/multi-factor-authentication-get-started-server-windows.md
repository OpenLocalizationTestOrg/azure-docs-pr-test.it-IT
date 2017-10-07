---
title: "aaaWindows l'autenticazione e Server di autenticazione a più fattori di Azure | Documenti Microsoft"
description: Si tratta hello Azure multi-factor authentication pagina di supporto della distribuzione di autenticazione di Windows e il Server Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>L'autenticazione di Windows e Azure il Server Multi-Factor Authentication
Utilizzare sezione autenticazione di Windows hello di hello del Server Azure multi-Factor Authentication tooenable e configurare l'autenticazione di Windows per le applicazioni. Prima di configurare l'autenticazione di Windows, tenere hello seguente elenco presente:

* Dopo l'installazione, riavviare hello Azure multi-Factor Authentication per effetto di tootake di servizi Terminal.
* Se non sono nell'elenco di utenti hello 'Corrispondenza utente richiedono Azure multi-Factor Authentication' è selezionata, non sarà in grado di toolog macchina hello dopo il riavvio.
* Indirizzi IP attendibili dipende se applicazione hello di fornire l'indirizzo IP con l'autenticazione di hello hello del client. Attualmente solo la funzione Servizi Terminal è supportata.  

> [!NOTE]
> Questa funzionalità non è supportato toosecure di servizi Terminal in Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure un'applicazione con l'autenticazione di Windows, utilizzare hello seguente procedura.
1. In hello del Server Azure multi-Factor Authentication fare clic sull'icona di autenticazione di Windows hello.
   ![Autenticazione di Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Controllare hello **abilitare l'autenticazione di Windows** casella di controllo. Per impostazione predefinita, questa casella è deselezionata.
3. scheda applicazioni Hello consente hello amministratore tooconfigure uno o più applicazioni per l'autenticazione di Windows.
4. Selezionare un server o l'applicazione: specificare se i server o l'applicazione hello è abilitata. Fare clic su **OK**.
5. Fare clic su **Aggiungi...**
6. scheda indirizzi IP attendibili Hello consente tooskip Azure multi-Factor Authentication per le sessioni Windows provenienti da IP specifici. Ad esempio, se i dipendenti usano un'applicazione hello da office hello e da casa, si può decidere che non si desidera far squillare per Azure multi-Factor Authentication in ufficio hello loro telefoni. A tale scopo, è necessario specificare subnet dell'ufficio hello come voce di indirizzi IP attendibili.
7. Fare clic su **Aggiungi...**
8. Selezionare **IP singolo** se si desidera tooskip un singolo indirizzo IP.
9. Selezionare **intervallo IP** se si desidera tooskip un intero intervallo IP. Esempio: 10.63.193.1-10.63.193.100.
10. Selezionare **Subnet** se si desidera toospecify un intervallo di indirizzi IP utilizzando la notazione di subnet. Immettere l'IP iniziale della subnet hello e selezionare hello netmask appropriata dall'elenco a discesa hello.
11. Fare clic su **OK**.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare dispositivi VPN di terze parti per il server Azure MFA](multi-factor-authentication-advanced-vpn-configurations.md)

- [Aumentare l'infrastruttura di autenticazione esistente con hello estensione dei criteri di rete per Azure MFA](multi-factor-authentication-nps-extension.md)

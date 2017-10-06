---
title: aaaConnect tooAzure di servizio App di Azure esistente del Database per MySQL | Documenti Microsoft
description: "Istruzioni per la modalità di connessione un tooAzure di servizio App di Azure esistente Database tooproperly per MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Connettersi a un servizio App di Azure tooAzure Database esistente per il server MySQL
Questo documento viene illustrato come Database di Azure tooconnect un tooyour di servizio App di Azure esistente per il server MySQL.

## <a name="before-you-begin"></a>Prima di iniziare
Accedi toohello [portale di Azure](https://portal.azure.com). Creare un database di Azure per il server MySQL. Per informazioni dettagliate, vedere troppo[come toocreate del Database per il server MySQL dal portale di Azure](quickstart-create-mysql-server-database-using-azure-portal.md) o [come toocreate Azure Database per il server di MySQL con CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Attualmente sono disponibili due soluzioni tooenable di accesso da un Database di Azure di tooan di servizio App di Azure per MySQL. Entrambe le soluzioni implicano la configurazione di regole firewall a livello di server.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Soluzione 1 - creare un tooallow regola firewall di tutti gli indirizzi IP
Il Database di Azure per MySQL offre la sicurezza di accesso usando un tooprotect firewall i dati. Quando la connessione da un Database di tooAzure servizio App di Azure per il server MySQL, tenere presente che hello in uscita, gli indirizzi IP di servizio App sono dinamico in natura. 

disponibilità di hello tooensure del servizio App di Azure, è consigliabile utilizzare questo tooallow soluzione tutti gli indirizzi IP.

> [!NOTE]
> Microsoft sta lavorando per un tooavoid soluzione a lungo termine consentendo tutti gli indirizzi IP per servizi di Azure tooconnect tooAzure Database MySQL.

1. Nel Pannello di server MySQL hello, in impostazioni fare clic su **sicurezza della connessione** tooopen hello sicurezza della connessione pannello hello Database di Azure per MySQL.

   ![Portale di Azure: fare clic su Sicurezza connessione](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Compilare i campi **NOME REGOLA**, **INDIRIZZO IP INIZIALE** e **INDIRIZZO IP FINALE**. Fare quindi clic su **Salva**.
   - Nome regola: Allow-All-IPs
   - Indirizzo IP iniziale: 0.0.0.0
   - Indirizzo IP finale: 255.255.255.255

   ![Portale di Azure - Aggiungere tutti gli indirizzi IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Soluzione 2: creare un firewall tooexplicitly regola consentire gli indirizzi IP in uscita
È possibile aggiungere in modo esplicito che tutti hello gli indirizzi IP in uscita del servizio App di Azure.

1. Nel Pannello proprietà del servizio App hello, visualizzare il **indirizzo IP in uscita**.

   ![Portale di Azure - Visualizzare gli indirizzi IP in uscita](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. Nel Pannello di sicurezza di connessione MySQL hello, aggiungere indirizzi IP in uscita, uno alla volta.

   ![Portale di Azure - Aggiungere indirizzi IP in modo esplicito](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Ricordare troppo**salvare** regole del firewall.

Anche se hello servizio App di Azure tenta costante di indirizzi IP tookeep nel tempo, vi sono casi in cui è possano modificare gli indirizzi IP hello. Ad esempio, quando hello ricicli app si verifica un'operazione di scala o quando vengono aggiunti nuovi computer in Azure dati internazionali centri capacità hello tooincrease. Quando si modifica indirizzi IP hello app hello potrebbe subire tempi di inattività in caso di hello non può più connettersi toohello MySQL server. Quando si sceglie una delle soluzioni precedenti hello, prendere in considerazione questo potenziale.

## <a name="ssl-configuration"></a>Configurazione SSL
Il database di Azure per MySQL ha abilitato SSL per impostazione predefinita. Se l'applicazione non utilizza SSL tooconnect toohello database, è necessario toodisable SSL sul server MySQL. Per informazioni dettagliate su come tooconfigure SSL, vedere [utilizzando SSL con il Database di Azure per MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulle stringhe di connessione, fare riferimento troppo[le stringhe di connessione](howto-connection-string.md).

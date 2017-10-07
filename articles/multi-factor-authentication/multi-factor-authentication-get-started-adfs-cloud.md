---
title: risorse del cloud con Azure MFA e AD FS aaaSecure | Documenti Microsoft
description: "Si tratta hello Azure multi-Factor authentication pagina che descrive la modalità di avvio tooget con Azure MFA e AD FS in cloud hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Protezione delle risorse cloud con Azure Multi-Factor Authentication e AD FS
Se l'organizzazione è federata con Azure Active Directory, usare Azure multi-Factor Authentication o Active Directory Federation Services (ADFS) toosecure risorse che hanno effettuato l'accesso AD Azure. Utilizzare hello seguendo le risorse di Azure Active Directory toosecure procedure con Azure multi-Factor Authentication o Active Directory Federation Services.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Proteggere le risorse Azure AD con ADFS
toosecure la risorsa cloud, impostare una regola attestazioni, in modo che Active Directory Federation Services genera hello multipleauthn attestazione quando un utente esegue la verifica completata. Questa attestazione viene passata in tooAzure Active Directory. Seguire questa procedura toowalk passaggi hello:


1. Aprire il componente di gestione di ADFS.
2. A sinistra di hello, selezionare **Relying Party Trusts**.
3. Fare clic con il pulsante destro del mouse su **Piattaforma delle identità di Microsoft Office 365** e selezionare **Modifica regole attestazione**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. In Regole di trasformazione rilascio fare clic su **Aggiungi regola**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. In aggiunta guidata regole attestazione trasformare hello, selezionare **Pass Through or Filter an Incoming Claim** hello elenco a discesa e fare clic su **Avanti**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Assegnare un nome alla regola. 
7. Selezionare **riferimenti dei metodi di autenticazione** come hello in arrivo tipo di attestazione.
8. Selezionare **Pass-through di tutti i valori attestazione**.
    ![Aggiunta guidata regole attestazione di trasformazione](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Fare clic su **Finish**. Chiudere la console di gestione di ADFS hello Active Directory.

## <a name="trusted-ips-for-federated-users"></a>Indirizzi IP attendibili per utenti federati
Indirizzi IP attendibili consente agli amministratori di verifica in due passaggi di tooby passare per gli indirizzi IP specifici o per gli utenti federati con richieste provenienti dalla propria rete intranet. Hello nelle sezioni seguenti descrivono come tooconfigure Azure multi-Factor Authentication attendibili gli indirizzi IP con gli utenti federati e verifica in due passaggi di elementi da ignorare quando una richiesta proviene da una rete intranet gli utenti federati. Questo risultato viene ottenuto mediante la configurazione di ADFS toouse pass-through o filtro di un modello di attestazione in ingresso con hello il tipo di attestazione all'interno della rete aziendale.

Questo esempio usa Office 365 per l'attendibilità del componente.

### <a name="configure-hello-ad-fs-claims-rules"></a>Configurare le regole delle attestazioni ADFS hello
Hello è necessario innanzitutto toodo è tooconfigure hello ADFS attestazioni. Creare due regole attestazioni, uno per hello all'interno della rete aziendale attestazione di tipo e un'altra per mantenere gli utenti connessi.

1. Aprire il componente di gestione di ADFS.
2. A sinistra di hello, selezionare **Relying Party Trusts**.
3. Fare clic con il pulsante destro del mouse su **Piattaforma delle identità di Microsoft Office 365** e selezionare **Modifica regole attestazione...**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. In Regole di trasformazione rilascio fare clic su **Aggiungi regola.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. In aggiunta guidata regole attestazione trasformare hello, selezionare **Pass Through or Filter an Incoming Claim** hello elenco a discesa e fare clic su **Avanti**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. In hello casella tooClaim regola nome successivo, assegnare alla regola un nome. Ad esempio: InternoReteAziend.
7. Dall'elenco a discesa hello, tipo di attestazione tooIncoming successivo, selezionare **all'interno della rete aziendale**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Fare clic su **Fine**.
9. In Regole di trasformazione rilascio fare clic su **Aggiungi regola**.
10. In aggiunta guidata regole attestazione trasformare hello, selezionare **inviare attestazioni mediante una regola personalizzata** hello elenco a discesa e fare clic su **Avanti**.
11. Nella casella hello sotto Nome regola attestazione: immettere *Keep Users Signed In*.
12. Nella casella regola personalizzata di hello, immettere:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Fare clic su **Fine**.
14. Fare clic su **Apply**.
15. Fare clic su **OK**.
16. Chiudere Gestione ADFS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Configurare gli indirizzi IP attendibili di Azure Multi-Factor Authentication con utenti federati
Ora che le attestazioni hello sono presenti, è possibile configurare indirizzi IP attendibili.

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. A sinistra di hello, fare clic su **Active Directory**.
3. Nella Directory, selezionare la directory di hello in cui si desidera tooset di indirizzi IP attendibili.
4. Nella Directory selezionata hello, fare clic su **configura**.
5. Nella sezione di hello multi-factor authentication, fare clic su **Gestisci impostazioni servizio**.
6. Nella pagina Impostazioni servizio hello in indirizzi IP attendibili, selezionare **ignorare multi-factor-autenticazione per le richieste dagli utenti federati nella intranet**.  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Fare clic su **save**.
8. Una volta applicati gli aggiornamenti di hello, fare clic su **chiudere**.

La procedura è terminata. A questo punto, gli utenti federati di Office 365 dovrebbero rimanere solo toouse MFA quando un'attestazione proviene dalla rete intranet aziendale di hello esterno.

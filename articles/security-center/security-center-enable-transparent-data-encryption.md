---
title: Transparent Data Encryption nel Centro protezione Azure aaaEnable | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * abilitare Transparent Data Encryption * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Abilitare Transparent Data Encryption nel Centro sicurezza di Azure
Il Centro sicurezza di Azure consiglia di abilitare Transparent Data Encryption (TDE) nel database SQL, se non è già abilitato. Transparent Data Encryption consente di proteggere i dati e consente di soddisfare i requisiti di conformità grazie alla crittografia del database, i backup associati e i file di log delle transazioni inattivi, senza richiedere modifiche tooyour applicazione. vedere più toolearn [Transparent Data Encryption con il Database di SQL Azure](https://msdn.microsoft.com/library/dn948096).

Questa indicazione si applica toohello solo servizio di SQL Azure non include SQL in esecuzione nelle macchine virtuali.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **abilitare Transparent Data Encryption**.
   ![Abilita Transparent Data Encryption][1]
2. Verrà visualizzata hello **abilitare Transparent Data Encryption nel database SQL** blade. Selezionare un tooenable di database SQL Transparent Data Encryption.
   ![Selezionare database SQL tooenable TDE nel][2]
3. In hello **crittografia dati trasparente** pannello seleziona **ON** sotto la crittografia dei dati e selezionare **salvare** nella barra multifunzione superiore hello del pannello hello.
   ![Attivare la crittografia TDE][3]

   Una volta TDE è abilitata nel hello selezionati database SQL, hello **lo stato di crittografia** cambierà troppo**Encrypted**.    

   ![Stato della crittografia][4]

## <a name="see-also"></a>Vedere anche
In questo articolo ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Abilitazione di Transparent Data Encryption". toolearn ulteriori informazioni su TDE SQL, vedere l'esempio hello:

* [Transparent Data Encryption con il database SQL di Azure](https://msdn.microsoft.com/library/dn948096)
* [Introduzione a Transparent Data Encryption (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png

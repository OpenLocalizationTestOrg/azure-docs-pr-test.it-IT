---
title: aggiornamenti del sistema aaaApply in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello indicazioni Centro sicurezza di Azure * * applicare gli aggiornamenti di sistema * * e * * riavviare il sistema dopo gli aggiornamenti di sistema * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Applicare gli aggiornamenti del sistema nel Centro sicurezza di Azure
Il Centro sicurezza di Azure monitora ogni giorno le macchine virtuali (VM) Windows e Linux alla ricerca di eventuali aggiornamenti mancanti del sistema operativo. Il Centro sicurezza recupera un elenco di aggiornamenti di sicurezza e critici disponibili da Windows Update o Windows Server Update Services (WSUS), in base al servizio configurato nella macchina virtuale Windows.  Centro sicurezza PC controlla anche per gli aggiornamenti più recenti di hello nei sistemi Linux. Se nella macchina virtuale non è stato applicato un aggiornamento del sistema, il Centro sicurezza ne consiglierà l'applicazione.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **applicare gli aggiornamenti di sistema**.

   ![Applicare gli aggiornamenti di sistema][1]
2. Hello **applicare gli aggiornamenti di sistema** pannello verrà aperto un elenco di macchine virtuali privi di aggiornamenti di sistema. Selezionare una macchina virtuale.

   ![Selezionare una macchina virtuale][2]
3. Viene visualizzato un pannello che mostra un elenco di aggiornamenti mancanti per la VM. Selezionare un aggiornamento del sistema. In questo esempio viene selezionato l'aggiornamento KB3156016.

   ![Aggiornamenti della sicurezza mancanti][3]

4. Seguire i passaggi hello hello **aggiornamento della sicurezza** tooapply pannello hello aggiornamento mancante.

   ![Aggiornamento della sicurezza][4]

## <a name="reboot-after-system-updates"></a>Riavviare dopo gli aggiornamenti del sistema
1. Restituire toohello **indicazioni** blade. Dopo l'applicazione degli aggiornamenti del sistema è stata generata una nuova voce, denominata **Riavvia dopo gli aggiornamenti del sistema**. Questa voce indica che è necessario che il processo tooreboot hello VM toocomplete hello di applicazione degli aggiornamenti di sistema.

   ![Riavviare dopo gli aggiornamenti del sistema][5]
2. Selezionare **Riavvia dopo gli aggiornamenti del sistema**. Verrà visualizzata **è un riavvio in sospeso toocomplete gli aggiornamenti del sistema** blade che visualizza un elenco di macchine virtuali che è necessario toorestart toocomplete hello applica il processo di aggiornamento del sistema.

   ![Riavvio in sospeso][6]

Riavviare hello VM dal processo di hello toocomplete Azure.

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png

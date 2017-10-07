---
title: soluzioni per i partner aaaManaging nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento illustra come Centro sicurezza di Azure consente di monitoraggio in uno stato di integrità hello panoramica delle soluzioni di partner integrato con la sottoscrizione di Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure
Questo documento illustra come toomonitor hello lo stato di integrità delle soluzioni di partner in Centro sicurezza di Azure.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione. Questo argomento non costituisce una guida dettagliata.
>
>

## <a name="monitoring-partner-solutions"></a>Monitoraggio delle soluzioni dei partner
Hello **soluzioni Partner** riquadro hello **Centro sicurezza PC** consente di blade monitorare in uno stato di integrità hello immediatamente partner delle soluzioni dell'utente che vengono integrati con la sottoscrizione di Azure.

![Riquadro Soluzioni partner][1]

Hello **soluzioni Partner** riquadro Visualizza il numero di hello di soluzioni per i partner integrato con la sottoscrizione. Se non esistono soluzioni integrate, riquadro hello viene visualizzato il numero di hello zero.

integrità di hello tooview partner delle soluzioni dell'utente:

1. Seleziona hello **soluzioni Partner** riquadro. Hello **soluzioni Partner** apre blade che visualizza un elenco di partner delle soluzioni dell'utente connesso tooSecurity Center.

   ![Soluzioni partner][3]

   può essere stato Hello di una soluzione di partner:

   * Protetto (verde): nessun problema di integrità.
   * Danneggiato (rosso): è presente un problema di integrità che richiede attenzione immediata.
   * Segnalazione arresto (arancione) - soluzione hello è stato arrestato reporting relativa integrità.
   * Lo stato di protezione sconosciuto (arancione) - stato hello della soluzione hello è sconosciuto al momento a causa di processo tooa non riuscito di aggiungere una nuova soluzione esistente toohello di risorse.
   * Non segnalato (grigio) - non è stato segnalato qualsiasi soluzione hello ancora, lo stato di una soluzione potrebbe essere segnalato se recentemente è stato connesso e viene effettuata la distribuzione.

2. Selezionare una soluzione dei partner. In questo esempio, consente di seleziona hello **Qualys** soluzione.  Un pannello apre visualizzando lo stato di hello della soluzione di partner hello e della soluzione hello le risorse associate. Selezionare **console soluzione** esperienza di gestione dei partner hello tooopen per questa soluzione.

   ![Dettagli della soluzione di un partner][4]
3. Tornare indietro toohello **Qualys** pannello e selezionare **collegamento VM**. Hello **collegamento applicazioni** apre blade. Qui è possibile connettersi soluzione partner toohello di risorse.

   ![Collegamento risorse toopartner soluzione][5]

## <a name="next-steps"></a>Passaggi successivi
In questo documento è stato introdotto toohello **soluzioni dei Partner** riquadro in Centro sicurezza PC. toolearn ulteriori informazioni su Centro di sicurezza, vedere hello seguenti articoli:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) , informazioni come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni facilitano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) , ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png

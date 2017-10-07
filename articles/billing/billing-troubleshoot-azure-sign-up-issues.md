---
title: aaaTroubleshoot Azure problemi relativi alla sottoscrizione | Documenti Microsoft
description: Viene descritto come tootroubleshoot alcuni comuni Azure iscrivermi problemi.
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Risolvere i problemi di iscrizione per Azure
Se non è possibile effettuare l'iscrizione per Azure, è possibile usare i suggerimenti di hello problemi comuni di tootroubleshoot questo articolo. In caso di problemi con la carta di credito durante l'iscrizione, vedere [La carta di credito o di debito viene rifiutata quando si tenta di eseguire l'iscrizione ad Azure](billing-credit-card-fails-during-azure-sign-up.md). Se si dispone di un account Azure, ma non è possibile accedere, vedere [non riesco ad accedere in toomanage la sottoscrizione di Azure](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>L'indicatore di stato si blocca nella sezione "Verifica dell'identità mediante smart card"

verifica dell'identità hello toocomplete tramite carta, è necessario consentire i cookie di terze parti per il browser.

![Schermata di hello verifica dell'identità dalla sezione card sporgente durante l'iscrizione](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Questa procedura hello utilizzare tooupdate le impostazioni dei cookie del browser.

1. Se si utilizza Chrome, andare troppo**impostazioni** > **Mostra impostazioni avanzate** > **Privacy** > **contenuto impostazioni**. Deselezionare **Blocca cookie di terze parti e dati dei siti**.
2. Se si utilizza Edge, andare troppo**impostazioni** > **Visualizza impostazioni avanzate** > **cookie**. Selezionare **Non bloccare i cookie**.
3. Aggiornare la pagina di iscrizione Azure hello e controllare se è stato risolto il problema di hello.
4. Se l'aggiornamento hello non risolve il problema di hello, chiudere e riavviare il browser, quindi riprovare.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Il modulo della carta di credito non supporta il mio indirizzo di fatturazione
L'indirizzo di fatturazione deve toobe paese hello selezionato in hello **sull'utente** sezione. Assicurarsi di selezionare paese corretto hello.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Assenza di messaggi di testo o chiamate durante la verifica dell'account di sottoscrizione
Mentre è in genere molto più veloce, potrebbe richiedere fino a toofour minuti per la verifica codice toobe recapitati. numero di telefono Hello che immesso per la verifica non vengono memorizzato come un numero di contatto per l'account di hello.

Altri suggerimenti:
* Un numero di telefono VOIP non può essere utilizzato per il processo di verifica telefonica hello.
* Numero di telefono hello doppio segno che immesso, incluso il codice di paese hello selezionato nel menu a discesa hello.
* Se il telefono non può ricevere messaggi di testo (SMS), provare a hello **chiamare me** opzione.
* Verificare che il telefono possa ricevere chiamate o messaggi SMS da un numero proveniente dagli Stati Uniti.

Quando viene visualizzato il messaggio di testo hello o telefonata, immettere il codice che viene visualizzato nella casella di testo hello.

## <a name="credit-card-declined-or-not-accepted"></a>Carta di credito rifiutata o non accettata
Le carte di credito o debito virtuali o prepagate non sono accettate come opzione di pagamento per l'iscrizione ad Azure. vedere in quale altro può causare il toobe card rifiutato, toosee [la carta di debito o carta di credito è stato rifiutato in Azure per l'abbonamento](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"La prova gratuita non è disponibile"
Hai già usato una sottoscrizione di Azure in hello precedente? Hello Azure condizioni per l'utilizzo limita l'attivazione di valutazione gratuita solo per un utente che è nuovo tooAzure. Se quindi si è già usato un qualsiasi altro tipo di sottoscrizione di Azure, non è possibile attivare una versione di valutazione gratuita. Considerare l'iscrizione per una [sottoscrizione con pagamento in base al consumo](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Ho visto un addebito sul mio account della versione di valutazione gratuita
Potrebbe essere visualizzato un piccolo verifica contenere sull'account della carta di credito dopo l'iscrizione, che viene rimosso entro 3 giorni too5. Se si è preoccupati della gestione dei costi, leggere altre informazioni per [evitare costi imprevisti](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Non è possibile attivare un piano con vantaggi di Azure, ad esempio MSDN, BizSpark, BizSparkPlus o MPN
Assicurarsi che si usi hello diritto Accedi credenziali. Controllare quindi hello vantaggio programma toomake certi della tua idoneo. 

* MSDN
  * Verificare lo stato di idoneità nella [pagina dell'account MSDN](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Se non è possibile verificare lo stato dell'utente, contattare hello [assistenza clienti sottoscrizioni MSDN](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Accedi toohello [BizSpark portale](https://www.microsoft.com/bizspark/default.aspx#start-two) e verificare lo stato di idoneità per BizSpark e BizSpark Plus.
  * Se non è possibile verificare lo stato, è possibile [Guida nei forum BizSpark hello](http://aka.ms/bzforums).
* MPN
  * Accedi toohello [portale MPN](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) e verificare lo stato di idoneità. Se si dispone di hello appropriato [competenze piattaforma Cloud](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), è possibile usufruire di vantaggi aggiuntivi.
  * Se non è possibile verificare lo stato, contattare il [supporto tecnico di MPN](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Non è possibile attivare una nuova sottoscrizione di Azure in Open
toocreate una sottoscrizione di Azure In Open, è necessario disporre di una chiave di attivazione di servizio in linea (OSA) valida con almeno un tooit associato token Azure In Open. Se non è disponibile una chiave di attivazione del servizio online, contattare uno dei partner Microsoft elencati in [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.

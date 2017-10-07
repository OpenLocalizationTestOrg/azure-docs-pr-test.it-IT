---
title: "aaa \"non può accedere l'errore di applicazione aziendale quando si usa un'applicazione Proxy dell'applicazione | Documenti di Microsoft\""
description: Come accesso comune tooresolve problemi con applicazioni di Proxy dell'applicazione AD Azure.
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>Errore "Can't Access this Corporate Application" (Impossibile accedere all'applicazione aziendale) quando si usa un'applicazione Proxy di applicazione

Questo articolo è utile tootroubleshoot comuni problemi quando viene visualizzato un errore "Impossibile accedere questa app aziendale" in un'applicazione Proxy dell'applicazione AD Azure.

## <a name="overview"></a>Panoramica
Quando viene visualizzato questo errore, pagina hello inoltre condividere un codice di stato. Tale codice è probabilmente una delle seguenti hello:

-   **Timeout gateway**: hello servizio Proxy di applicazione è connettore hello tooreach non è possibile. In genere, ciò indica un problema con assegnazione di hello connettore, connettore stesso o hello le regole relative alle connettore hello di rete.

-   **Gateway non valido**: connettore hello è un'applicazione back-end non è possibile tooreach hello. Ciò potrebbe indicare un errore di configurazione dell'applicazione hello.

-   **Non è consentito**: utente hello non è un'applicazione hello tooaccess autorizzati. Questa situazione può verificarsi quando hello non assegnati toohello applicazione in Azure Active Directory, o se nel back-end hello hello utente non dispone di un'applicazione hello tooaccess autorizzazione.

codice hello toofind, esaminare il testo hello hello basso a sinistra del messaggio di errore hello per il campo "Codice di stato" hello. Cercare inoltre eventuali note in basso a molto hello della pagina hello con suggerimenti aggiuntivi.

   ![Errore di timeout del gateway](./media/application-proxy/connection-problem.png)

Per informazioni dettagliate su come tootroubleshoot hello causa radice di tali errori e altre informazioni sulle correzioni suggerite, vedere hello corrispondente sezione riportata di seguito.

## <a name="gateway-timeout-errors"></a>Errori di timeout del gateway

Quando il servizio di hello tenta connettore hello tooreach e non è possibile toowithin hello timeout finestra, si verifica un timeout di gateway. Questo è in genere causato da un'applicazione assegnata tooa connettore gruppo con i connettori non funzionante o alcune porte necessarie a hello connettore non sono aperti.


## <a name="bad-gateway-errors"></a>Errori di gateway non valido

Un errore di gateway non valido indica che tale connettore hello è un'applicazione back-end non è possibile tooreach hello. Assicurarsi che sia stata pubblicata un'applicazione hello corretto. Inesattezze comuni che causano questo errore:

-   Un errore di digitazione o di un errore nell'URL interno hello

-   La pubblicazione non radice hello applicazione hello. Ad esempio, la pubblicazione <http://expenses/reimbursement> tentando tooaccess <http://expenses>

-   Problemi di configurazione di delega vincolata Kerberos (KCD) hello

-   Problemi relativi all'applicazione back-end hello

## <a name="forbidden-errors"></a>Errori di accesso non consentito

Se viene visualizzato un errore non consentito, utente hello non è stato assegnato toohello applicazione. È possibile in Azure Active Directory o in un'applicazione hello back-end.

toolearn come applicazione di toohello tooassign utenti in Azure, vedere hello [documentazione configurazione](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).

Se si conferma l'utente hello viene assegnato toohello applicazione in Azure, controllo configurazione utente hello in un'applicazione hello back-end. Se si utilizza la delega vincolata Kerberos o l'autenticazione integrata di Windows, consultare la pagina di risoluzione dei problemi KCD per alcune linee guida.

## <a name="check-hello-applications-internal-url"></a>Controllare l'URL dell'applicazione hello interno

Come primo passaggio rapido, controllare, verificare e correggere URL interno hello aprendo un'applicazione hello tramite **applicazioni aziendali**, quindi selezionando hello **Proxy dell'applicazione** menu. Verificare che sia hello interno URL sia corretto, hello quello utilizzato dall'applicazione hello tooaccess rete locale.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Verificare un'applicazione hello sia assegnata tooa connettore gruppo di lavoro

un'applicazione hello tooverify viene assegnata tooa connettore gruppo di lavoro:

1.  Aprire l'applicazione hello nel portale di hello passando troppo**Azure Active Directory**, fare clic su **applicazioni aziendali**, quindi **tutte le applicazioni.** Aprire l'applicazione hello, quindi selezionare **Proxy dell'applicazione** dal menu a sinistra di hello.

2.  Esaminare il campo di gruppo di connettori hello. Se sono non presenti connettori attivi nel gruppo di hello, viene visualizzato un avviso. Se tutti gli avvisi non è visibile, passare troppo "verificare tutte le porte richieste siano consentito".

3.  Se si tratta di hello gruppo sbagliato connettore, utilizzare hello a discesa gruppo corretto di tooselect hello e confermare che non è più visualizzare gli avvisi. Se si tratta di hello destinato a gruppo di connettori, fare clic su pagina hello avviso messaggio tooopen hello con gestione Connector.

4.  Da qui, esistono alcuni modi toodrill in:

  * Spostare un connettore attivo nel gruppo di hello: se si dispone di un connettore attivo che deve appartenere toothis gruppo e che dispone di visibilità toohello l'applicazione back-end di destinazione, è possibile spostare hello connettore nel gruppo hello assegnato. toodo questa operazione, scegliere hello connettore. Nel campo "Gruppo di connettori" hello, utilizzare il gruppo corretto hello tooselect elenco a discesa hello e fare clic su Salva.

  * Scaricare un nuovo connettore per tale gruppo: in questa pagina, è possibile ottenere il collegamento hello troppo[scaricare un nuovo connettore](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download). esigenze del connettore Hello toobe installato in un computer con l'applicazione di back-end toohello of di visibilità diretto e si trova in genere hello applicazione hello nello stesso server. Hello utilizzare scaricare toodownload collegamento connettore un connettore nel computer di destinazione hello. Successivamente, fare clic su hello connettore e utilizzare hello "Gruppo di connettori" elenco a discesa toomake che appartiene a gruppo corretto toohello.

  * Provare a utilizzare un connettore inattivo: se un connettore viene illustrato come inattivo, è il servizio di hello tooreach non è possibile. Si tratta in genere a causa di toosome necessarie porte bloccate. toosolve questo problema, spostare nella troppo "verificare che tutte le porte necessarie siano consentito".

Dopo l'utilizzo di questi passaggi applicazione hello tooensure è gruppo tooa assegnato all'utilizzo di connettori, un'applicazione hello test nuovamente. Se ancora non funziona, continuare toohello nella sezione successiva.

## <a name="check-all-required-ports-are-whitelisted"></a>Controllare che tutte le porte richieste siano inserite nell'elenco degli elementi consentiti

tooverify tutti necessari porte siano aperte, vedere la documentazione sull'apertura di porte. Se tutte le porte hello necessarie sono aperte, spostare toohello nella sezione successiva.

## <a name="check-for-other-connector-errors"></a>Verificare la presenza di altri errori del connettore

Se nessuno dei precedente hello risolvere il problema di hello, il passaggio successivo hello è toolook per problemi o errori con hello connettore stesso. È possibile visualizzare alcuni errori comuni in hello [Troubleshoot documento](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). 

È possibile anche visualizzare direttamente hello connettore registri tooidentify gli eventuali errori. Molti dei nostri messaggi di errore essere in grado di tooshare consigli più specifici per le correzioni. vedere i log hello tooview, toolearn [documentazione dei connettori](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="additional-resolutions"></a>Risorse aggiuntive

Se hello precedente non risolve il problema di hello, esistono diverse possibili cause. problema di hello tooidentify:

Se l'applicazione è configurata toouse integrata autenticazione di Windows (IWA), un'applicazione hello test senza single sign-on. In caso contrario, spostare toohello successivo paragrafo. un'applicazione hello toocheck senza single sign-on, aprire l'applicazione tramite **applicazioni aziendali,** e passare toohello **Single Sign-On** menu. Hello Modifica elenco a discesa da "Autenticazione integrata di Windows" troppo "Azure AD single sign-on disabilitato". 

Aprire un browser e provare nuovamente l'applicazione hello tooaccess. Deve essere richiesto per l'autenticazione e ottenere in un'applicazione hello. Se il funzionamento, configurazione della delega vincolata Kerberos (KCD) di hello che consente accesso hello single sign-on è hello problema. vedere pagina risolvere i problemi di delega vincolata Kerberos hello.

Se si continua l'errore hello toosee, andare in hello connettore è installato, aprire un browser e tentativo tooreach hello URL interno utilizzato per un'applicazione hello toohello macchina. Hello connettore opera come un altro client da hello nello stesso computer. Se non è possibile raggiungere l'applicazione hello, perché tale macchina è un'applicazione hello tooreach non è possibile provare a utilizzare o utilizzare un connettore in un server che è in grado di tooaccess hello dell'applicazione.

Se è possibile raggiungere l'applicazione hello da tale computer, toolook per problemi o errori con hello connettore stesso. È possibile visualizzare alcuni errori comuni in hello [Troubleshoot documento](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). È possibile anche visualizzare direttamente hello connettore registri tooidentify gli eventuali errori. Molti dei nostri messaggi di errore essere in grado di tooshare consigli più specifici per le correzioni. vedere i log hello tooview, toolearn [documentazione dei connettori](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="next-steps"></a>Passaggi successivi
[Comprendere i connettori del proxy applicazione Azure AD](application-proxy-understand-connectors.md)

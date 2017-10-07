---
title: risorse di rete CDN di Azure aaaSecuring con l'autenticazione token | Documenti Microsoft
description: Utilizzo risorse di autenticazione del token toosecure accesso tooyour rete CDN di Azure.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Protezione di asset della rete CDN di Azure con l'autenticazione basata su token

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Panoramica

L'autenticazione del token è un meccanismo che consente di tooprevent rete CDN di Azure da risorse toounauthorized ai client un accesso.  Questa operazione viene in genere eseguita tooprevent "hotlinking" del contenuto, in un altro sito Web, spesso una bacheca, utilizza le risorse senza autorizzazione.  Questo può avere effetto sui costi di distribuzione di contenuti. Abilitando questa funzionalità sulla rete CDN, le richieste verranno autenticate dal bordo CDN POP prima di recapitare contenuto hello. 

## <a name="how-it-works"></a>Funzionamento

L'autenticazione del token di verifica le richieste vengono generate da un sito attendibile richiedendo toocontain le richieste di un valore di token che contengono informazioni codificate richiedente hello. Il contenuto verrà solo servito toorequester quando hello requisiti hello soddisfa le informazioni di codifica, in caso contrario richieste rifiutate. È possibile impostare il requisito di hello utilizzando uno o più parametri seguenti.

- Paese: consente o nega le richieste che hanno origine dai paesi specificati.  [Elenco di codici paesi validi.](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL: Consenti solo toorequest asset o il percorso specificato.  
- Host: consentire o negare le richieste con host specificato nell'intestazione della richiesta hello.
- Referrer: consentire o negare toorequest referrer specificato.
- Indirizzo IP: consente solo le richieste che hanno origine da un indirizzo IP o da una subnet IP specifica.
- Protocollo: Consenti o Blocca richieste basate sul protocollo hello utilizzato contenuto hello toorequest.
- Ora di scadenza: assegnare una data e ora tooensure periodo che un collegamento solo rimane valido per un periodo di tempo limitato.

Vedere l'esempio di configurazione dettagliato per ogni parametro.

## <a name="reference-architecture"></a>Architettura di riferimento

Vedere di seguito un'architettura di riferimento di configurazione dell'autenticazione del token nella rete CDN toowork con l'App Web.

![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Logica di convalida dei token nell'endpoint di rete CDN
    
Questo grafico illustra come la rete CDN di Azure convalida la richiesta client quando viene configurata l'autenticazione basata su token nell'endpoint di rete CDN.

![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Configurazione dell'autenticazione basata su token

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il profilo CDN tooyour e quindi fare clic su hello **Gestisci** portale supplementare di pulsante toolaunch hello.

    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Passare il mouse su **HTTP grandi**, quindi fare clic su **Authentication Token** nel riquadro a comparsa hello. In questa scheda si configureranno la chiave di crittografia e i parametri di crittografia.

    1. Immettere una chiave di crittografia univoca per **Chiave primaria**.  Immetterne un'altra per **Backup Key** (Chiave di backup).

        ![Chiave di configurazione per l'autenticazione basata su token di rete CDN](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Configurare i parametri di crittografia con lo strumento di crittografia. Consentire o negare le richieste in base a ora di scadenza, paese, referrer, protocollo e IP client. È possibile usare qualsiasi combinazione.

        ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - ec-expire: assegna un'ora di scadenza di un token dopo un periodo di tempo specificato. Richieste inviate dopo la data di scadenza hello verrà negato. Questo parametro usa il timestamp Unix, basato sui secondi dal periodo standard 1/1/1970 00:00:00 GMT. È possibile usare strumenti online tooprovide conversioni ora solare e l'ora di Unix.)  Ad esempio, se si desidera tooset toobe token hello scadute al 31/12/2016 12:00:00 GMT, utilizzare l'ora di Unix hello: 1483185600 come indicato di seguito:
    
        ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - CE-url-Consenti: consente di asset di tootailor token tooa specifico o il percorso. Limita accesso toorequests il cui URL è iniziare con un percorso specifico. È possibile inserire più percorsi separandoli con una virgola. Gli URL distinguono tra maiuscole e minuscole. In base al requisito di hello, è possibile impostare livelli diversi di tooprovide valore diverso di accesso. Di seguito sono elencati alcuni scenari:
        
            Se l'URL è: http://www.mydomain.com/pictures/city/strasbourg.png. Vedere il valore di input "" e di conseguenza il livello di accesso

            1. Valore di input "/": tutte le richieste verranno consentite
            2. Valore di input "/ immagini": hello tutte le richieste di seguito consentirà
            
                - http://www.mydomain.com/pictures.png
                - http://www.mydomain.com/pictures/city/strasbourg.png
                - http://www.mydomain.com/picturesnew/city/strasbourgh.png
            3. Valore di input "/pictures/": verranno consentite solo le richieste per /pictures/
            4. Valore di input "/pictures/city/strasbourg.png": consente solo le richieste per questo asset
    
        ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - ec-country-allow: consente solo le richieste che hanno origine da uno o più paesi specificati. Le richieste che hanno origine da tutti gli altri paesi verranno negate. Utilizzare tooset codice paese i parametri di hello e separare ogni codice di paese con una virgola. Ad esempio, se si desidera accedere tooallow da Stati Uniti e in Francia, input US, FR nella colonna hello come di seguito.  
        
        ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - ec-country-deny: nega le richieste che hanno origine da uno o più paesi specificati. Le richieste che hanno origine da tutti gli altri paesi verranno consentite. Utilizzare tooset codice paese i parametri di hello e separare ogni codice di paese con una virgola. Ad esempio, se si desidera accedere toodeny da Stati Uniti e in Francia, l'input US, FR nella colonna hello.
    
        - ec-ref-allow: consente solo le richieste dal referrer specificato. Un riferimento identifica hello URL della pagina web hello collegato toohello risorsa richiesta. valore del parametro Hello referrer non deve includere il protocollo di hello. È possibile inserire un nome host e/o un determinato percorso in tale nome host. È anche possibile aggiungere più referrer in un singolo parametro separandoli con una virgola. Se è stato specificato un valore di riferimento, ma informazioni referrer hello non viene inviate la richiesta di hello causa toosome la configurazione del browser, tali richieste verranno negate per impostazione predefinita. È possibile assegnare "Mancante" o un valore vuoto nel tooallow parametro hello queste richieste con informazioni di riferimento mancante. È anche possibile usare "*. consoto.com" tooallow tutti i sottodomini di consoto.com.  Ad esempio, se si desidera accedere tooallow per le richieste da www.consoto.com, tutti i sottodomini in consoto2.com ed erquests con reffers vuoto o mancante, valore di sotto di input:
        
        ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - ec-ref-deny: nega le richieste dal referrer specificato. Fare riferimento toodetails e riportato nel parametro "ec-ref-Consenti".
         
        - ec-proto-allow: consente solo le richieste dal protocollo specificato, ad esempio http o https.
        
        ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - ec-proto-deny: nega le richieste dal protocollo specificato, ad esempio http o https.
    
        - CE clientip: limita l'indirizzo IP del richiedente toospecified di accesso. Sono supportati sia IPV4 che IPV6. È possibile specificare un solo indirizzo IP o una sola subnet IP per la richiesta.
            
        ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. È possibile testare il token con lo strumento di decrittazione hello.

    4. È anche possibile personalizzare il tipo di hello della risposta che verrà restituito toouser quando richiesta viene negata. Per impostazione predefinita, si usa 403.

3. Ora fare clic sulla scheda **Motore regole di business** in **HTTP Large** (Large HTTP). Verrà utilizzarla scheda toodefine percorsi tooapply hello, abilitare la funzionalità di autenticazione del token hello e abilitare l'autenticazione con token aggiuntiva relative funzionalità.

    - Utilizzare asset toodefine di colonna "IF" o il percorso che si desidera eseguire l'autenticazione token tooapply. 
    - Fare clic su tooadd "Token Auth" dal tipo di autenticazione token tooenable hello funzionalità elenco a discesa.
        
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. In hello **motore regole di business** scheda, esistono alcune funzionalità aggiuntive, è possibile abilitare.
    
    - Codice di autorizzazione di negazione del token: determina il tipo di hello di risposta che verrà restituito toouser quando una richiesta viene negata. Regole impostate qui sostituirà hello denial codice impostazione scheda autenticazione token hello.
    - Token auth ignorare: determina se i token toovalidate URL usato sarà tra maiuscole e minuscole.
    - Parametro di token di autenticazione: rinominare query di autenticazione token hello parametro della stringa di visualizzazione in hello richiesta URL. 
        
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-token-auth/cdn-rules-engine2.png)

5. È possibile personalizzare il token che è un'applicazione che genera un token per le funzionalità di autenticazione basata su token. Il codice sorgente è accessibile qui in [GitHub](https://github.com/VerizonDigital/ectoken).
I linguaggi disponibili includono:
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Prezzi dei provider e funzionalità della rete CDN di Azure

Vedere hello [Panoramica della rete CDN](cdn-overview.md) argomento.

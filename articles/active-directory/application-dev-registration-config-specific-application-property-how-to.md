---
title: toofill aaaHow i campi specifici per un'applicazione sviluppata | Documenti Microsoft
description: Informazioni aggiuntive su come toofill out specifici campi quando si registra un'applicazione sviluppata personalizzata con Azure AD
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
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>Come toofill i campi specifici per un'applicazione personalizzata

In questo articolo è fornita una breve descrizione di tutti i campi disponibili hello nel modulo di registrazione applicazione hello in hello [portale di Azure](https://portal.azure.com).

## <a name="register-a-new-application"></a>Registrare una nuova applicazione

-   tooregister una nuova applicazione, passare toohello [portale di Azure](https://portal.azure.com).

-   Dal riquadro di spostamento a sinistra di hello, fare clic su **Azure Active Directory.**

-   Scegliere **Registrazioni per l'app** e fare clic su **Aggiungi**.

-   Aprire il modulo di registrazione applicazione hello.

## <a name="fields-in-hello-application-registration-form"></a>Campi nel modulo di registrazione applicazione hello


| Campo            | Descrizione                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Nome             | nome di Hello dell'applicazione hello. Deve essere minimo di quattro caratteri.                |
| Tipo di applicazione | **App Web/API Web**: un'applicazione Web, un'API Web o entrambe 
| |**Nativa**: un'applicazione che può essere installata in un computer o dispositivo utente           |
| URL di accesso      | URL di Hello in cui gli utenti possono accedere in toouse dell'applicazione                                  |

Dopo avere compilato hello sopra i campi, un'applicazione hello essere registrato nel portale di Azure hello e si reindirizzati toohello pagina dell'applicazione. Hello **impostazioni** nel riquadro applicazione hello apre la pagina Impostazioni di hello, che dispone di più campi per l'utente toocustomize l'applicazione. tabella di Hello seguente descrive tutti i campi nella pagina Impostazioni hello hello. Si noti che viene visualizzato solo un sottoinsieme di questi campi, a seconda se è stata creata un'applicazione Web o un'applicazione nativa.

| Campo           | Descrizione                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID applicazione  | Quando si registra un'applicazione, Azure AD assegna un ID all'applicazione. ID applicazione Hello può essere utilizzato toouniquely identificare l'applicazione in tooAzure le richieste di autenticazione AD, nonché risorse tooaccess come hello API Graph.                                                          |
| URI dell'ID dell'app      | Deve essere un URI univoco, in genere di modulo hello **https://&lt;tenant\_nome&gt;/&lt;applicazione\_nome&gt;.** Durante il flusso di concessione di autorizzazione hello, viene utilizzato come identificatore univoco toospecify hello risorsa quale token hello deve essere emesso per. Anch'essa diventa hello 'aud' attestazione nel token di accesso hello rilasciato. |
| Carica nuovo logo | È possibile utilizzare questo tooupload un logo per l'applicazione. logo di Hello devono essere in formato BMP, jpg o PNG e dimensioni del file hello devono essere minore di 100KB. dimensioni di Hello per immagine hello devono essere 215 x 215 pixel, con dimensioni dell'immagine centrale di 94 x 94 pixel.                                                       |
| URL della home page   | Si tratta di hello sign-on URL specificato durante la registrazione dell'applicazione.                                                                                                                                                                                                                                              |
| URL di chiusura sessione      | L'URL di disconnessione di disconnessione singola hello. Azure AD invierà un URL della richiesta di disconnessione toothis utente hello Cancella la sessione con Azure AD con qualsiasi altra applicazione registrata.                                                                                                                                       |
| Multi-tenant  | Consente di specificare se un'applicazione hello può essere utilizzata da più tenant. In genere, ciò significa che le organizzazioni esterne è possono utilizzare l'applicazione la registrazione al proprio tenant e la concessione di dati dell'organizzazione accesso tootheir.                                                                   |
| URL di risposta      | URL di risposta Hello sono endpoint hello in Azure AD restituisce tutti i token che richiede l'applicazione.                                                                                                                                                                                                          |
| URI di reindirizzamento   | Per le applicazioni native, è in utente hello sia inviato toofollowing di autorizzazione ha esito positivo. Fornisce l'applicazione in hello OAuth 2.0 richiesta corrisponde a uno dei valori hello registrato nel portale di hello URI di reindirizzamento di Azure verifica Active Directory che hello.                                                            |
| Chiavi            | È possibile creare chiavi tooprogrammatically accedere ad API web protette da Azure AD senza alcuna interazione dell'utente. Da hello \* \*chiavi\* \* immettere una data di scadenza chiave di descrizione e hello e salvare toogenerate hello chiave. Assicurarsi che toosave in un punto sicuro, come, non sarà in grado di tooaccess posticipato.             |

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md)

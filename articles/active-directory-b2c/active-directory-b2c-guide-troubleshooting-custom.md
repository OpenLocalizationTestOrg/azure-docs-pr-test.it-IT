---
title: 'Azure Active Directory B2C: Risoluzione dei problemi dei criteri personalizzati| Microsoft Docs'
description: Informazioni sugli approcci toosolving errori quando si lavora con i criteri personalizzati in Azure Active Directory.
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Risoluzione dei problemi del framework di esperienza di gestione delle identità e criteri personalizzati di Azure AD B2C

Se si usa Azure Active Directory B2C (Azure AD B2C) di criteri personalizzati, potrebbero verificarsi problemi di impostazione hello Framework esperienza identità nel relativo formato XML di linguaggio dei criteri.  Criteri personalizzati di apprendimento toowrite possibile imparare un nuovo linguaggio. Questo articolo descrive gli strumenti e suggerimenti che consentono di individuare e risolvere rapidamente i problemi. 

> [!NOTE]
> Questo articolo è incentrato sulla risoluzione dei problemi della configurazione dei criteri personalizzati di Azure AD B2C. Non si occupa di hello relying applicazione di terze parti o la libreria di identità.

## <a name="xml-editing"></a>Modifica dell'XML

Hello errore più comune per l'impostazione di criteri personalizzati è correttamente formattato XML. Un buon editor XML è essenziale. Un editor XML valido visualizza il codice XML in modo nativo, applica un colore specifico ai contenuti, precompila i termini comuni, mantiene indicizzati gli elementi XML e riesce a eseguire la convalida con lo schema. Seguono due editor XML tra i più validi:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Notepad++](https://notepad-plus-plus.org/)

La convalida dello schema XML identifica gli errori prima del caricamento del file XML. Nella cartella radice di hello del pacchetto hello, ottenere hello XML schema definition TrustFrameworkPolicy_0.3.0.0.xsd. Per ulteriori informazioni, nella documentazione di hello dell'editor XML, cercare *strumenti XML* e *convalida XML*.

Una revisione delle regole XML può risultare utile. Azure AD B2C rifiuta qualsiasi errore di formattazione XML che rileva. Un codice XML non correttamente formattato può restituire a volte messaggi di errore fuorvianti.

## <a name="upload-policies-and-policy-validation"></a>Convalida dei criteri e del caricamento dei criteri

 La convalida del caricamento del file XML è automatica. La maggior parte degli errori causano hello toofail di caricamento. Convalida include i file dei criteri che si sta caricando hello. Include inoltre una catena di hello di file troppo fa riferimento di file di caricamento hello (hello file dei criteri relying party, hello estensioni file e file di base hello). 
 
 Gli errori di convalida comuni includono seguente hello.

Frammento con errore: `... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Hello ClaimType valore potrebbe essere errato o non esiste nello schema di hello.
* ClaimType valori devono essere definiti in almeno uno dei file hello nei criteri di hello. 
    Ad esempio: ` <ClaimType Id="socialIdpUserId">`
* Se ClaimType è definita nel file di estensioni di hello, ma viene usato anche in un valore TechnicalProfile nel file di base hello, caricamento di file di base hello genera un errore.

Frammento con errore: `...makes a reference tooa ClaimsTransformation with id...`
* salve le cause di errore hello potrebbe essere hello uguale a quello di errore ClaimType hello.

Frammento con errore: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Verificare che il valore di ID tenant in hello hello  **\<TrustFrameworkPolicy\>**  e  **\<BasePolicy\>**  elementi corrispondono alla destinazione di Azure Active Directory B2C tenant.  

## <a name="troubleshoot-hello-runtime"></a>Risoluzione dei problemi di runtime hello

* Utilizzare `Run Now` e `https://jwt.io` tootest i criteri in modo indipendente da al web e applicazioni per dispositivi mobili. Questo sito Web funziona come un'applicazione relying party. Visualizza il contenuto di hello di hello JSON Web Token (JWT) che viene generato per i criteri di Azure Active Directory B2C. toocreate un'applicazione di test nel Framework di esperienza di identità, hello di utilizzare i valori seguenti:
    * Nome: TestApp
    * App Web/API Web: no
    * Client nativo: no

* scambio di hello tootrace di messaggi tra il browser client e Azure Active Directory B2C, utilizzare [Fiddler](http://www.telerik.com/fiddler). Consente di ottenere un'indicazione del punto in cui il percorso utente genera errori nei passaggi di orchestrazione.

* In **modalità di sviluppo**, utilizzare **Application Insights** attività hello tootrace del percorso Framework esperienza identità utente. In **modalità di sviluppo**, è possibile osservare exchange hello di attestazioni tra hello Framework esperienza di identità e hello varie attestazioni i provider che sono definiti dai profili tecnici, ad esempio il provider di identità, servizi basati su API directory di utenti di Azure Active Directory B2C Hello e altri servizi, ad esempio Azure Multi-Factor autenticazione.  

## <a name="recommended-practices"></a>Procedure consigliate

**Mantenere più versioni degli scenari. Raggrupparli in un progetto con l'applicazione.** base Hello, estensioni e i file di relying party dipendono direttamente tra loro. Salvarli come gruppo. Come criteri tooyour vengono aggiunte nuove funzionalità, è possibile mantenere le versioni di lavoro separato. Le versioni operative fase nel proprio file di sistema con il codice dell'applicazione hello che interagiscono con.  Le applicazioni potrebbero richiamare diversi criteri relying party in un tenant. Diventano dipende hello attestazioni che si aspettano da criteri di Azure Active Directory B2C.

**Sviluppare e testare i profili tecnici con percorsi utente noti.** Utilizzare testata starter pack criteri tooset dei profili del tecnici. Testarli separatamente prima di includerli nel proprio percorso utente.

**Sviluppare e testare i percorsi utente con profili tecnici testati.** Modificare i passaggi dell'orchestrazione hello di un proprio processo utente in modo incrementale. Compilare progressivamente gli scenari previsti.

## <a name="next-steps"></a>Passaggi successivi

* In GitHub scaricare hello [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) con estensione zip.

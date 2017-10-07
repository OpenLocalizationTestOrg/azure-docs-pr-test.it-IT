---
title: 'Azure Active Directory B2C: uso della personalizzazione della lingua | Microsoft Docs'
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C: uso della personalizzazione della lingua

>[!NOTE] 
>Questa funzionalità è disponibile in anteprima pubblica.  È consigliabile usare un tenant di test quando si usa questa funzionalità.  Noi non pianifichiamo su eventuali modifiche di rilievo dalla versione di hello anteprima toohello disponibilità generale, ma si riserva toomake destra hello funzionalità di hello tooimprove tali modifiche.  Dopo aver una funzionalità tootry possibilità, fornire commenti e suggerimenti sulle proprie esperienze e come è possibile renderlo migliori.  È possibile fornire commenti e suggerimenti tramite il portale di Azure hello con lo strumento di faccia smile hello in alto a destra hello.   Se è un requisito aziendale per toogo si usa questa funzionalità in fase di anteprima hello in tempo reale, è possibile fornire assistenza e materiale sussidiario corretto hello informano gli scenari.  È possibile scrivere a [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).

Personalizzazione di lingua consente toochange utente viaggio tooa lingua diversa toosuit alle esigenze.  Sono disponibili traduzioni in 36 lingue. Vedere a tal proposito la sezione [Informazioni aggiuntive](#additional-information).  Anche se l'esperienza viene fornita solo per un singolo linguaggio, è possibile personalizzare il testo su hello pagine toosuit le proprie esigenze.  

## <a name="how-does-language-customization-work"></a>Funzionamento della personalizzazione della lingua
Personalizzazione di lingua consente tooselect quali lingue sono disponibile in consentirti di utente.  Dopo aver abilitato la funzionalità di hello, è possibile fornire parametri di stringa di query hello, ui_locales, dall'applicazione.  Quando si chiama in Azure Active Directory B2C, si convertono le impostazioni locali toohello pagina indicata.  Con tipo di configurazione offre controllo completo sulle lingue hello in consentirti di utente e Ignora impostazioni della lingua del browser del cliente hello hello. Potrebbe non essere necessario un tale livello di controllo sulle lingue visualizzate dal cliente.  Se non si fornisce un parametro ui_locales, esperienza del cliente hello è determinato dalle impostazioni del browser.  È comunque possibile controllare quali lingue sono consentirti di utente tradotti tooby aggiungendolo come una lingua supportata.  Se il browser di un cliente è set tooshow una lingua non si desidera toosupport quindi language hello che è stata selezionata come verrà visualizzato un valore predefinito nelle impostazioni cultura supportate.

1. **interfaccia utente-impostazioni locali specificato linguaggio** -dopo aver abilitato la personalizzazione di lingua, consentirti di utente sono toohello tradotti lingua specificata
2. **Browser richiesto language** -se è stata specificata alcuna interfaccia utente-impostazioni locali, converte toohello browser richiesto Java **se è stata inclusa nelle lingue supportate**
3. **Lingua predefinita di criteri** -se il browser hello non specifica una lingua o specifica che non è supportato, converte toohello linguaggio predefinito dei criteri

>[!NOTE]
>Se si utilizza gli attributi personalizzati dell'utente, è necessario tooprovide propria traduzioni. Per informazioni dettagliate, vedere la sezione [Personalizzazione delle stringhe](#customize-your-strings).
>

## <a name="support-uilocales-requested-languages"></a>Supporto di lingue richieste dal parametro ui_locales 
Abilitando 'Personalizzazione Language' in un criterio, è ora possibile controllare il linguaggio hello del viaggio utente hello aggiungendo il parametro ui_locales hello.
1. [Seguire questi blade di funzionalità passaggi toonavigate toohello B2C hello portale di Azure.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. Passare tooa criteri che si desidera tooenable per le traduzioni.
3. Fare clic su **Personalizzazione della lingua**.
4. Leggere con attenzione l'avviso hello.  Non è possibile disabilitare la personalizzazione della lingua dopo averla abilitata.
5. Attivare la funzionalità di hello e fare clic su **OK**.
6. Salvare il criterio in hello nell'angolo superiore sinistro del **Modifica criterio** blade.

## <a name="select-which-languages-your-user-journey-supports"></a>Selezione delle lingue supportate dal percorso utente 
Creare un elenco delle lingue consentiti per il toobe viaggio utente tradotto in quando non viene fornito il parametro ui_locales hello.
1. Assicurarsi che la personalizzazione della lingua sia abilitata nei criteri in base alle istruzioni precedenti.
2. Nel pannello **Modifica criterio** selezionare **Personalizzazione della lingua**.
3. Il cursore si sposterà tooyour **lingue supportate** blade.  Da qui è possibile selezionare **Aggiungi lingua**.
4. Selezionare tutte le lingue che si desidera toobe supportati hello.  

>[!NOTE]
>Se non viene specificato un parametro ui_locales, pagina hello viene lingua del browser del cliente toohello tradotto solo se è presente in questo elenco
>

5. Fare clic su **Ok** nella parte inferiore di hello
6. Chiude hello **personalizzazione Language** blade e **salvare** i criteri.

## <a name="customize-your-strings"></a>Personalizzazione delle stringhe
'Personalizzazione language' consente toocustomize qualsiasi stringa in consentirti di utente.
1. Verificare che i criteri sono "personalizzazione di linguaggio' abilitata da istruzioni precedenti hello.
2. Nel pannello **Modifica criterio** selezionare **Personalizzazione della lingua**.
3. Scegliere dal menu di navigazione a sinistra di hello **scaricare il contenuto**.
4. Selezionare hello pagina tooedit.
5. Nell'elenco a discesa hello, selezionare il linguaggio di hello desiderato tooedit per.
6. Fare clic su **Download**. 

Questi passaggi consentono di un file JSON che è possibile utilizzare toostart modifica le stringhe.

### <a name="changing-any-string-on-hello-page"></a>La modifica di qualsiasi stringa nella pagina hello
1. Aprire hello file JSON scaricati da istruzioni precedenti in un editor di JSON.
2. Trova hello desiderati toochange.  È possibile trovare hello `StringId` della stringa hello si sta cercando, o cercare hello `Value` desiderato toochange.
3. Hello aggiornamento `Value` attributo con i dati da visualizzare.
4. Salvare il file hello e caricare le modifiche.

### <a name="changing-extension-attributes"></a>Modifica degli attributi di estensione
Se si sta cercando un attributo personalizzato utente stringa hello toochange o tooadd uno toohello JSON, è in hello seguente formato:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Se è necessario toooverride una stringa, assicurarsi che hello tooset `Override` valore troppo`true`.  Se non viene modificato il valore di hello, voce hello viene ignorato. 
>

Sostituire `<ExtensionAttribute>` con nome hello dell'attributo utente personalizzata.  
Sostituire `<ExtensionAttributeValue>` con hello nuova stringa toobe visualizzato.

### <a name="using-localizedcollections"></a>Uso di LocalizedCollections
Se si desidera tooprovide un elenco di set di valori per le risposte, è necessario toocreate un `LocalizedCollections`.  `LocalizedCollections` è una matrice di coppie `Name`-`Value`.  Hello `Name` è ciò che viene visualizzato e hello `Value` è ciò che viene restituito nell'attestazione hello.  tooadd un `LocalizedCollections`, ha hello seguente formato:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Se è necessario toooverride una stringa, assicurarsi che hello tooset `Override` valore troppo`true`.  Se non viene modificato il valore di hello, voce hello viene ignorato. 
>

* `ElementId`è hello utente attributo da questo `LocalizedCollections` è una risposta a
* `Name`hello valore mostrato toohello utente
* `Value`è ciò che viene restituito nell'attestazione hello quando questa opzione è selezionata

### <a name="upload-your-changes"></a>Caricamento delle modifiche
1. Dopo aver completato i file JSON di hello modifiche tooyour, spostarsi indietro tooyour B2C tenant.
2. Nel pannello **Modifica criterio** selezionare **Personalizzazione della lingua**.
3. Scegliere dal menu di navigazione a sinistra di hello **caricare contenuto**.
4. Selezionare hello pagina tooupload le modifiche apportate.
5. Se si desidera un linguaggio che ci hai fornito in precedenza un formato JSON per tooupload, è necessario toodelete hello precedente la voce.  È possibile eliminarla, fare clic su hello `...` hello destra di quella lingua e selezionare **eliminare**.
6. Fare clic su **Aggiungi** in alto a sinistra di hello.
7. Selezionare la lingua hello del file JSON.
8. Fare clic su pulsante cartella hello hello destra e selezionare il file JSON.
9. Fare clic su hello **caricare** pulsante nella parte inferiore di hello del pannello hello.
10. Tornare indietro tooyour **Modifica criterio** pannello e fare clic su **salvare**.

## <a name="additional-information"></a>Informazioni aggiuntive
### <a name="recommendations-for-language-customization"></a>Raccomandazioni per la personalizzazione della lingua
È consigliabile solo inserimento in risorse di lingua tooyour voci per le stringhe si in modo esplicito tooreplace desiderata.  Si applica un file toohello limite di dimensioni che viene compilato da tutte le traduzioni di JSON.  Se i file troppo grande, impatto sulle prestazioni di hello del percorso utente.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>Dopo aver abilitato la personalizzazione della lingua le etichette di personalizzazione dell'interfaccia utente della pagina vengono rimosse
Quando si abilita la personalizzazione della lingua, le modifiche precedenti apportate alle etichette usando la personalizzazione dell'interfaccia utente della pagina vengono rimosse, ad eccezione degli attributi utente personalizzati.  Questa modifica viene eseguita conflitti tooavoid nella quale è possibile modificare le stringhe.  È possibile continuare le etichette e le altre stringhe toochange caricando le risorse della lingua in 'Personalizzazione Language'.
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Microsoft è commit tooprovide hello più aggiornate di traduzioni per l'utilizzo
Microsoft continuerà a migliorare le traduzioni e a garantirne la conformità.  Verrà identificare bug e le modifiche nella terminologia globale e rendere gli aggiornamenti di hello che funzioneranno perfettamente nella consentirti di utente.
### <a name="support-for-right-to-left-languages"></a>Supporto per lingue da destra a sinistra
Non è disponibile il supporto per le lingue da destra a sinistra; se è necessaria questa funzionalità, richiederla in [Azure Feedback](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).
### <a name="social-identity-provider-translations"></a>Traduzioni per provider di identità basati su social network
Offriamo hello ui_locales gli account di accesso OIDC parametro toosocial ma non viene rispettate da alcuni provider di identità di social networking, inclusi Facebook e Google. 
### <a name="browser-behavior"></a>Comportamento dei browser
Chrome e Firefox sia richiesta per la lingua di set e se è una lingua supportata, viene visualizzato prima predefinito hello.  Bordo attualmente non viene richiesta una lingua e passa una lingua predefinita toohello retta.
### <a name="known-issues"></a>Problemi noti
* Caricamento delle risorse di lingua per la pagina di autenticazione a più fattori hello nei criteri di modifica del profilo è attualmente disponibile.
* `LocalizedCollections`non vengono generati per i valori quando è richiesto dal tipo di risposta hello
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>Per le lingue non supportate,
Ci stiamo pianificazione tooprovide un'estensione di questa funzionalità che consente una risorsa JSON verso 'lingue personalizzate' tooupload.  funzione Hello consente nome hello toospecify e linguaggio del codice per qualsiasi lingua e fornire *tutti* hello traduzioni per tale lingua.  Per usufruire di questa funzionalità, inviare lo scenario a [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).  

### <a name="what-languages-are-supported"></a>Quali lingue sono supportate?

| Lingua              | Codice lingua |
|-----------------------|---------------|
| Bengalese                | bn            |
| Ceco                 | cs            |
| Danese                | da            |
| Tedesco                | de            |
| Greco                 | el            |
| Inglese               | en            |
| Spagnolo               | es            |
| Finlandese               | fi            |
| Francese                | fr            |
| Gujarati              | gu            |
| Hindi                 | hi            |
| Croato              | hr            |
| Ungherese             | hu            |
| Italiano               | it            |
| Giapponese              | ja            |
| Kannada               | kn            |
| Coreano                | ko            |
| Malayalam             | ml            |
| Marathi               | mr            |
| Malese                 | ms            |
| Norvegese bokmål      | nb            |
| Olandese                 | nl            |
| Punjabi               | pa            |
| Polacco                | pl            |
| Portoghese (Brasile)   | pt-br         |
| Portoghese (Portogallo) | pt-pt         |
| Romeno              | ro            |
| Russo               | ru            |
| Slovacco                | sk            |
| Svedese               | sv            |
| Tamil                 | ta            |
| Telugu                | te            |
| Thai                  | th            |
| Turco               | tr            |
| Cinese (semplificato)  | zh-hans       |
| Cinese (tradizionale) | zh-hant       |

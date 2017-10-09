---
title: espressioni di criteri di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sulle espressioni di criteri in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: ea160028-fc04-4782-aa26-4b8329df3448
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 79da0d6ca3963307ec811a33aaac3d63a7abd97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policy-expressions"></a>Espressioni di criteri di Gestione API
La sintassi delle espressioni di criteri è C# 6.0. Ogni espressione ha accesso toohello fornito in modo implicito [contesto](api-management-policy-expressions.md#ContextVariables) variabile e un consentiti [subset](api-management-policy-expressions.md#CLRTypes) dei tipi .NET Framework.  
  
> [!NOTE]
>  Per ulteriori informazioni sulle espressioni di criteri, vedere hello [espressioni di criteri](https://azure.microsoft.com/documentation/videos/policy-expressions-in-azure-api-management/) video.  
>   
>  Per una dimostrazione relativa alla configurazione dei criteri usando le espressioni, vedere l'[episodio 177 di Cloud Cover su altre funzionalità di Gestione API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). In questo video contiene hello seguito alle dimostrazioni di espressione di criteri.  
>   
>  -   10:30 - vedere come il criterio tooapply hello API livello toosupply contesto informazioni toohello back-end servizio utilizzando hello [impostare il parametro di stringa di query](api-management-transformation-policies.md#SetQueryStringParameter) e [intestazione HTTP impostare](api-management-transformation-policies.md#SetHTTPheader) criteri. 12:10 è una dimostrazione di chiamata di un'operazione nel portale per sviluppatori hello in cui è possibile visualizzare questi criteri al lavoro.  
> -   13:50 - vedere come hello toouse [convalidare JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre criteri-autorizzare l'accesso toooperations basata sulle attestazioni di token. Avanzamento rapido too15:00 criteri hello toosee configurati nell'editor Criteri di hello e quindi too18:50 per una dimostrazione di chiamata di un'operazione dal portale per sviluppatori di hello con e senza hello necessari token di autorizzazione.  
> -   Vedere 21:00 - come toouse un [API controllo](https://azure.microsoft.com/documentation/articles/api-management-howto-api-inspector/) toosee come criteri vengono valutati e risultati delle valutazioni hello hello di traccia.  
> -   25:25 - vedere come espressioni di criteri toouse con hello [ottenere dalla cache](api-management-caching-policies.md#GetFromCache) e [archivio toocache](api-management-caching-policies.md#StoreToCache) risposta di gestione API tooconfigure criteri che corrispondenze hello risposta la memorizzazione nella cache di hello permanenza nella cache il servizio back-end come specificato da hello backup del servizio `Cache-Control` direttiva.  
> -   34:30 - vedere come contenuto tooperform applicando un filtro per la rimozione degli elementi di dati dalla risposta hello ricevuto dal servizio back-end hello utilizzando hello [flusso di controllo](api-management-advanced-policies.md#choose) e [impostare corpo](api-management-transformation-policies.md#SetBody) criteri. Inizia dal 31:50 toosee Cenni preliminari [hello scuro Sky previsione API](https://developer.forecast.io/) utilizzato per questa dimostrazione.  
> -   le istruzioni dei criteri di hello toodownload utilizzate in questo video, vedere hello [esempi di gestione api/criteri](https://github.com/Azure/api-management-samples/tree/master/policies) repository github.  
  
  
##  <a name="Syntax"></a> Sintassi  
 Le espressioni a istruzione singola sono racchiuse tra `@(expression)`, dove `expression` è un'istruzione di espressione C# ben formata.  
  
 Le espressioni a più istruzioni sono racchiuse tra `@{expression}`. Tutti i percorsi di codice all'interno di espressioni a più istruzioni devono terminare con un'istruzione `return`.  
  
##  <a name="PolicyExpressionsExamples"></a> Esempi  
  
```  
@(true)  
  
@((1+1).ToString())  
  
@("Hi There".Length)  
  
@(Regex.Match(context.Response.Headers.GetValueOrDefault("Cache-Control",""), @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value)  
  
@(context.Variables.ContainsKey("maxAge") ? int.Parse((string)context.Variables["maxAge"]) : 3600)  
  
@{   
  string value;   
  if (context.Request.Headers.TryGetValue("Authorization", out value))   
  {   
    return Encoding.UTF8.GetString(Convert.FromBase64String(value));  
  }   
  else   
  {   
    return null;  
  }  
}  
```  
  
##  <a name="PolicyExpressionsUsage"></a> Uso  
 Espressioni possono essere utilizzate come valori di attributo o valori di testo in uno qualsiasi di hello gestione API [criteri](api-management-policies.md), a meno che il riferimento di criteri di hello specifica in caso contrario.  
  
> [!IMPORTANT]
>  Si noti che quando si usano le espressioni di criteri, esiste solo limitata verifica hello delle espressioni di criteri quando il criterio di hello è definito. Poiché le espressioni di hello vengono eseguite in fase di esecuzione nella pipeline in ingresso o in uscita di hello dal gateway hello, eventuali eccezioni di runtime generate da espressioni di criteri hello comporterà un errore di runtime nella chiamata API hello.  
  
##  <a name="CLRTypes"></a> Tipi di .NET Framework consentiti nelle espressioni di criteri  
 Hello nella tabella seguente sono elencati i tipi di .NET Framework hello e i membri che sono consentiti nelle espressioni di criteri.  
  
|Tipo CLR|Metodi supportati|  
|--------------|-----------------------|  
|Newtonsoft.Json.Linq.Extensions|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JArray|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JConstructor|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JContainer|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JObject|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JProperty|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JRaw|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JToken|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JTokenType|Tutti i metodi sono supportati|  
|Newtonsoft.Json.Linq.JValue|Tutti i metodi sono supportati|  
|System.Collections.Generic.IReadOnlyCollection<T\>|Tutti|  
|System.Collections.Generic.IReadOnlyDictionary<TKey,  TValue>|Tutti|  
|System.Collections.Generic.ISet<TKey, TValue>|Tutti|  
|System.Collections.Generic.KeyValuePair<TKey,  TValue>|Chiave, valore|  
|System.Collections.Generic.List<TKey, TValue>|Tutti|  
|System.Collections.Generic.Queue<TKey, TValue>|Tutti|  
|System.Collections.Generic.Stack<TKey, TValue>|Tutti|  
|System.Convert|Tutti|  
|System.DateTime|Tutti|  
|System.DateTimeKind|UTC|  
|System.DateTimeOffset|Tutti|  
|System.Decimal|Tutti|  
|System.Double|Tutti|  
|System.Guid|Tutti|  
|System.IEnumerable<T\>|Tutti|  
|System.IEnumerator<T\>|Tutti|  
|System.Int16|Tutti|  
|System.Int32|Tutti|  
|System.Int64|Tutti|  
|System.Linq.Enumerable<T\>|Tutti i metodi sono supportati|  
|System.Math|Tutti|  
|System.MidpointRounding|Tutti|  
|System.Nullable<T\>|Tutti|  
|System.Random|Tutti|  
|System.SByte|Tutti|  
|System.Security.Cryptography. HMACSHA384|Tutti|  
|System.Security.Cryptography. HMACSHA512|Tutti|  
|System.Security.Cryptography.HashAlgorithm|Tutti|  
|System.Security.Cryptography.HMAC|Tutti|  
|System.Security.Cryptography.HMACMD5|Tutti|  
|System.Security.Cryptography.HMACSHA1|Tutti|  
|System.Security.Cryptography.HMACSHA256|Tutti|  
|System.Security.Cryptography.KeyedHashAlgorithm|Tutti|  
|System.Security.Cryptography.MD5|Tutti|  
|System.Security.Cryptography.RNGCryptoServiceProvider|Tutti|  
|System.Security.Cryptography.SHA1|Tutti|  
|System.Security.Cryptography.SHA1Managed|Tutti|  
|System.Security.Cryptography.SHA256|Tutti|  
|System.Security.Cryptography.SHA256Managed|Tutti|  
|System.Security.Cryptography.SHA384|Tutti|  
|System.Security.Cryptography.SHA384Managed|Tutti|  
|System.Security.Cryptography.SHA512|Tutti|  
|System.Security.Cryptography.SHA512Managed|Tutti|  
|System.Single|Tutti|  
|System.String|Tutti|  
|System.StringSplitOptions|Tutti|  
|System.Text.Encoding|Tutti|  
|System.Text.RegularExpressions.Capture|Indice, lunghezza, valore|  
|System.Text.RegularExpressions.CaptureCollection|Conteggio, elemento|  
|System.Text.RegularExpressions.Group|Acquisizioni, esito positivo|  
|System.Text.RegularExpressions.GroupCollection|Conteggio, elemento|  
|System.Text.RegularExpressions.Match|Empty, Groups, Result|  
|System.Text.RegularExpressions.Regex|.ctor, IsMatch, Match, Matches, Replace|  
|System.Text.RegularExpressions.RegexOptions|Compiled, IgnoreCase, IgnorePatternWhitespace, Multiline, None, RightToLeft, Singleline|  
|System.TimeSpan|Tutti|  
|System.Tuple|Tutti|  
|System.UInt16|Tutti|  
|System.UInt32|Tutti|  
|System.UInt64|Tutti|  
|System.Uri|Tutti|  
|System.Xml.Linq.Extensions|Tutti i metodi sono supportati|  
|System.Xml.Linq.XAttribute|Tutti i metodi sono supportati|  
|System.Xml.Linq.XCData|Tutti i metodi sono supportati|  
|System.Xml.Linq.XComment|Tutti i metodi sono supportati|  
|System.Xml.Linq.XContainer|Tutti i metodi sono supportati|  
|System.Xml.Linq.XDeclaration|Tutti i metodi sono supportati|  
|System.Xml.Linq.XDocument|Tutti i metodi sono supportati|  
|System.Xml.Linq.XDocumentType|Tutti i metodi sono supportati|  
|System.Xml.Linq.XElement|Tutti i metodi sono supportati|  
|System.Xml.Linq.XName|Tutti i metodi sono supportati|  
|System.Xml.Linq.XNamespace|Tutti i metodi sono supportati|  
|System.Xml.Linq.XNode|Tutti i metodi sono supportati|  
|System.Xml.Linq.XNodeDocumentOrderComparer|Tutti i metodi sono supportati|  
|System.Xml.Linq.XNodeEqualityComparer|Tutti i metodi sono supportati|  
|System.Xml.Linq.XObject|Tutti i metodi sono supportati|  
|System.Xml.Linq.XProcessingInstruction|Tutti i metodi sono supportati|  
|System.Xml.Linq.XText|Tutti i metodi sono supportati|  
|System.Xml.XmlNodeType|Tutti|  
  
##  <a name="ContextVariables"></a> Variabile di contesto  
 Una variabile denominata `context` è disponibile in modo implicito in ogni [espressione](api-management-policy-expressions.md#Syntax) di criteri. I suoi membri forniscono informazioni pertinenti toohello `\request`. Tutti i hello `context` membri sono di sola lettura.  
  
|Variabile di contesto|Metodi, proprietà e valori di parametro consentiti|  
|----------------------|-------------------------------------------------------|  
|context|Api: IApi<br /><br /> Distribuzione<br /><br /> LastError<br /><br /> Operazione<br /><br /> Prodotto<br /><br /> Richiesta<br /><br /> RequestId: string<br /><br /> Response<br /><br /> Sottoscrizione<br /><br /> Tracing: bool<br /><br /> Utente<br /><br /> Variables:IReadOnlyDictionary<string, object><br /><br /> void Trace(message: string)|  
|context.Api|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> ServiceUrl: IUrl|  
|context.Deployment|Region: string<br /><br /> ServiceName: string|  
|context.LastError|Source: string<br /><br /> Reason: string<br /><br /> Message: string<br /><br /> Scope: string<br /><br /> Section: string<br /><br /> Path: string<br /><br /> PolicyId: string<br /><br /> Per ulteriori informazioni su context.LastError, vedere [Gestione degli errori](api-management-error-handling-policies.md).|  
|context.Operation|Id: string<br /><br /> Method: string<br /><br /> Name: string<br /><br /> UrlTemplate: string|  
|context.Product|Apis: IEnumerable<IApi\><br /><br /> ApprovalRequired: bool<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Name: string<br /><br /> State: enum ProductState {NotPublished, Published}<br /><br /> SubscriptionLimit: int?<br /><br /> SubscriptionRequired: bool|  
|context.Request|Body: IMessageBody<br /><br /> Certificate: System.Security.Cryptography.X509Certificates.X509Certificate2<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> IpAddress: string<br /><br /> MatchedParameters: IReadOnlyDictionary<string, string><br /><br /> Method: string<br /><br /> OriginalUrl:IUrl<br /><br /> Url: IUrl|  
|string context.Request.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> Restituisce separati da virgole i valori di intestazione di richiesta o `defaultValue` se non viene trovata intestazione hello.|  
|context.Response|Body: IMessageBody<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> StatusCode: int<br /><br /> StatusReason: string|  
|string context.Response.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> Restituisce i valori delle intestazioni di risposta separati da virgole o `defaultValue` se non viene trovata intestazione hello.|  
|context.Subscription|CreatedTime: DateTime<br /><br /> EndDate: DateTime?<br /><br /> Id: string<br /><br /> Key: string<br /><br /> Name: string<br /><br /> PrimaryKey: string<br /><br /> SecondaryKey: string<br /><br /> StartDate: DateTime?|  
|context.User|Email: string<br /><br /> FirstName: string<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Identities: IEnumerable<IUserIdentity\><br /><br /> LastName: string<br /><br /> Note: string<br /><br /> RegistrationDate: DateTime|  
|IApi|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> Protocols: IEnumerable<string\><br /><br /> ServiceUrl: IUrl<br /><br /> SubscriptionKeyParameterNames: ISubscriptionKeyParameterNames|  
|IGroup|Id: string<br /><br /> Name: string|  
|IMessageBody|As<T\>(preserveContent: bool = false): Where T: string, JObject, JToken, JArray, XNode, XElement, XDocument<br /><br /> Hello `context.Request.Body.As<T>` e `context.Response.Body.As<T>` metodi vengono utilizzati tooread organismi in un tipo specificato di un messaggio di richiesta e risposta `T`. Per impostazione predefinita hello metodo utilizza hello originale messaggio flusso del corpo e reneders disponibile dopo di esso restituisce. tooavoid che mediante il metodo hello operano su una copia del flusso del corpo hello, hello set `preserveContent` parametro troppo`true`. Passare [qui](api-management-transformation-policies.md#SetBody) toosee un esempio.|  
|IUrl|Host: string<br /><br /> Path: string<br /><br /> Port: int<br /><br /> Query: IReadOnlyDictionary<string, string[]><br /><br /> QueryString: string<br /><br /> Scheme: string|  
|IUserIdentity|Id: string<br /><br /> Provider: string|  
|ISubscriptionKeyParameterNames|Header: string<br /><br /> Query: string|  
|string IUrl.Query.GetValueOrDefault(queryParameterName: string, defaultValue: string)|queryParameterName: string<br /><br /> defaultValue: string<br /><br /> Restituisce separati da virgole i valori di parametro di query o `defaultValue` se non viene trovato il parametro hello.|  
|T context.Variables.GetValueOrDefault<T\>(variableName: string, defaultValue: T)|variableName: string<br /><br /> defaultValue: T<br /><br /> Restituisce il valore della variabile cast tootype `T` o `defaultValue` se hello variabile non viene trovata.<br /><br /> Questo metodo genera un'eccezione se hello tipo specificato non corrisponde hello al tipo effettivo di hello restituito variabile.|  
|BasicAuthCredentials AsBasic(input: this string)|input: string<br /><br /> Se il parametro di input hello contiene un valore di intestazione di richiesta di autorizzazione di autenticazione HTTP di base valido, il metodo hello restituisce un oggetto di tipo `BasicAuthCredentials`; in caso contrario hello restituisce null.|  
|bool TryParseBasic(input: this string, result: out BasicAuthCredentials)|input: string<br /><br /> result: out BasicAuthCredentials<br /><br /> Se il parametro di input hello contiene un valore di intestazione di richiesta di autorizzazione di autenticazione HTTP di base valido, il metodo di hello restituisce `true` e parametro hello del risultato contiene un valore di tipo `BasicAuthCredentials`; in caso contrario metodo hello restituisce `false`.|  
|BasicAuthCredentials|Password: string<br /><br /> UserId: string|  
|Jwt AsJwt(input: this string)|input: string<br /><br /> Se il parametro di input hello contiene un valore di token JWT valido, il metodo hello restituisce un oggetto di tipo `Jwt`; in caso contrario metodo hello restituisce `null`.|  
|bool TryParseJwt(input: this string, result: out Jwt)|input: string<br /><br /> result: out Jwt<br /><br /> Se il parametro di input hello contiene un valore di token JWT valido, il metodo di hello restituisce `true` e parametro hello del risultato contiene un valore di tipo `Jwt`; in caso contrario metodo hello restituisce `false`.|  
|Jwt|Algorithm: string<br /><br /> Audience: IEnumerable<string\><br /><br /> Claims: IReadOnlyDictionary<string, string[]><br /><br /> ExpirationTime: DateTime?<br /><br /> Id: string<br /><br /> Issuer: string<br /><br /> NotBefore: DateTime?<br /><br /> Subject: string<br /><br /> Type: string|  
|string Jwt.Claims.GetValueOrDefault(claimName: string, defaultValue: string)|claimName: string<br /><br /> defaultValue: string<br /><br /> Restituisce i valori attestazione separati da virgole o `defaultValue` se non viene trovata intestazione hello.|

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  

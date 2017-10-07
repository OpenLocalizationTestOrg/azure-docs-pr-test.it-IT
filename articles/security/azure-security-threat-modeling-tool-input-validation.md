---
title: Convalida - modellazione strumento Microsoft Threat - Azure aaaInput | Documenti Microsoft
description: misure di attenuazione esposte in hello strumento di modellazione del rischio di minacce per la
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>Infrastruttura di sicurezza: convalida dell'input - Procedure di mitigazione 
| Prodotto o servizio | Articolo |
| --------------- | ------- |
| **Applicazione Web** | <ul><li>[Disabilitare gli script XSLT per tutte le trasformazioni con fogli di stile non attendibili](#disable-xslt)</li><li>[Verificare che ogni pagina che potrebbe includere contenuti controllabili dall'utente rifiuti esplicitamente l'analisi MIME automatica](#out-sniffing)</li><li>[Applicare la protezione avanzata o la disabilitazione della risoluzione di entità XML](#xml-resolution)</li><li>[Verifica della canonizzazione degli URL nelle applicazioni che utilizzano http.sys](#app-verification)</li><li>[Verificare la presenza dei controlli appropriati quando si accettano file dagli utenti](#controls-users)</li><li>[Verificare che nell'applicazione Web vengano usati parametri indipendenti dai tipi per l'accesso ai dati](#typesafe)</li><li>[Utilizzare un modello separato l'associazione di classi o filtro elenchi tooprevent MVC assegnazione massa vulnerabilità](#binding-mvc)</li><li>[Codificare web non attendibile output precedente toorendering](#rendering)</li><li>[Eseguire la convalida dell'input e applicare filtri a tutte le proprietà del modello di tipo stringa](#typemodel)</li><li>[Applicazione della purificazione nei campi modulo che accettano tutti i caratteri, ad esempio un editor di testo RTF](#richtext)</li><li>[Non assegnare toosinks elementi DOM che non dispongono di codifica incorporato](#inbuilt-encode)</li><li>[Convalidare tutti i reindirizzamenti all'interno di un'applicazione hello sono chiuso o completati in modo sicuro](#redirect-safe)</li><li>[Implementare la convalida dell'input in un tutti i parametri di tipo stringa accettati dai metodi del controller](#string-method)</li><li>[Impostare il timeout del limite superiore per l'elaborazione DoS tooprevent a causa di espressioni regolari toobad delle espressioni regolari](#dos-expression)</li><li>[Evitare di usare Html.Raw nelle visualizzazioni Razor](#html-razor)</li></ul> | 
| **Database** | <ul><li>[Non usare query dinamiche nelle stored procedure](#stored-proc)</li></ul> |
| **API Web** | <ul><li>[Verificare l'esecuzione della convalida dei modelli nei metodi di API Web](#validation-api)</li><li>[Implementare la convalida dell'input in tutti i parametri di tipo stringa accettati dai metodi di API Web](#string-api)</li><li>[Verificare che nell'API Web vengano usati parametri indipendenti dai tipi per l'accesso ai dati](#typesafe-api)</li></ul> | 
| **Azure Document DB** | <ul><li>[Usare query SQL con parametri per DocumentDB](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[WCF: convalida dell'input tramite l'associazione allo schema](#schema-binding)</li><li>[WCF: convalida dell'input tramite controlli parametro](#parameters)</li></ul> |

## <a id="disable-xslt"></a>Disabilitare gli script XSLT per tutte le trasformazioni con fogli di stile non attendibili

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Sicurezza XSLT ](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [Proprietà XsltSettings.EnableScript](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **Passaggi** | XSLT supporta lo scripting all'interno di fogli di stile tramite hello `<msxml:script>` elemento. In questo modo le funzioni personalizzate toobe utilizzato in una trasformazione XSLT. Hello script viene eseguito nel contesto di hello del processo di hello eseguendo hello trasformazione. Script XSLT deve essere disabilitato in un'esecuzione tooprevent ambiente non attendibile di codice non attendibile. *Se si utilizza .NET:* script XSLT sono disattivati per impostazione predefinita; tuttavia, è necessario assicurarsi che non è stato in modo esplicito abilitato tramite hello `XsltSettings.EnableScript` proprietà.|

### <a name="example"></a>Esempio 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Esempio
Se si utilizza con MSXML 6.0, script XSLT sono disattivati per impostazione predefinita. Tuttavia, è necessario assicurarsi che non è stato in modo esplicito abilitato tramite proprietà dell'oggetto DOM XML hello AllowXsltScript. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Esempio
Se si usa MSXML 5 o versione inferiore, gli script XSLT sono abilitati per impostazione predefinita e devono essere disabilitati in modo esplicito. Impostare hello DOM XML oggetto proprietà AllowXsltScript toofalse. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>Verificare che ogni pagina che potrebbe includere contenuti controllabili dall'utente rifiuti esplicitamente l'analisi MIME automatica

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [IE8 Security Part V: Comprehensive Protection](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx) (Sicurezza di IE8 parte V: protezione completa)  |
| **Passaggi** | <p>Per ogni pagina che può contenere contenuto controllabile utente, è necessario utilizzare l'intestazione HTTP hello `X-Content-Type-Options:nosniff`. toocomply con questo requisito, è possibile che l'intestazione obbligatoria hello set da una pagina solo per le pagine che possono contenere contenuto controllabile dall'utente oppure è possibile impostare a livello globale per tutte le pagine di un'applicazione hello.</p><p>Ogni tipo di file recapitato da un server web è associato un [tipo MIME](http://en.wikipedia.org/wiki/Mime_type) (chiamato anche un *contenuto-tipo*) che descrive la natura hello del contenuto di hello (vale a dire, immagine, testo, applicazione e così via)</p><p>intestazione X-contenuto-tipo-Options Hello è un'intestazione HTTP che consente agli sviluppatori toospecify che il loro contenuto non è deve essere rilevato la presenza di MIME. Questa intestazione è progettato toomitigate analisi MIME attacchi. Il supporto per questa intestazione è stato aggiunto in Internet Explorer 8 (IE8).</p><p>Solo gli utenti di Internet Explorer 8 (IE8) potranno usufruire di X-Content-Type-Options. Le versioni precedenti di Internet Explorer non rispettano attualmente intestazione X-contenuto-tipo-Options hello</p><p>Internet Explorer 8 (e versioni successive) sono hello solo funzionalità di rifiuto esplicito per analisi MIME tooimplement i browser principali. Se e quando altri browser principali (Firefox, Safari, Chrome) implementare funzionalità simili, questa indicazione sarà sintassi tooinclude aggiornato per tali browser nonché</p>|

### <a name="example"></a>Esempio
intestazione obbligatoria hello di tooenable globalmente per tutte le pagine applicazione hello, è possibile eseguire una delle seguenti hello: 

* Aggiungi intestazione hello nel file Web. config hello se un'applicazione hello è ospitata da Internet Information Services (IIS) 7 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Aggiungi intestazione hello tramite hello applicazione globale\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* Implementare un modulo HTTP personalizzato 

``` 
public class XContentTypeOptionsModule : IHttpModule 
  {
    #region IHttpModule Members 
    public void Dispose() 
    { 

    } 
    public void Init(HttpApplication context)
    { 
      context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders); 
    } 
    #endregion 
    void context_PreSendRequestHeaders(object sender, EventArgs e) 
      { 
        HttpApplication application = sender as HttpApplication; 
        if (application == null) 
          return; 
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* È possibile abilitare l'intestazione di richiesta hello solo per le pagine specifiche aggiungendolo tooindividual risposte: 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>Applicare la protezione avanzata o la disabilitazione della risoluzione di entità XML

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Espansione di entità XML](http://capec.mitre.org/data/definitions/197.html), [Attacchi Denial of Service e difese in XML](http://msdn.microsoft.com/magazine/ee335713.aspx), [Cenni preliminari sulla sicurezza MSXML](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [Procedure consigliate per la protezione del codice MSXML](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [Informazioni di riferimento sul protocollo NSXMLParserDelegate](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html), [Risoluzione di riferimenti esterni](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **Passaggi**| <p>Anche se non è ampiamente utilizzata, è disponibile una funzionalità del XML che consente di entità macro hello XML parser tooexpand con i valori definiti nel documento hello stesso o da origini esterne. Ad esempio, documento hello potrebbe definire un'entità "companyname" con valore hello "Microsoft", in modo che ogni volta hello testo "&companyname;" viene visualizzato nel documento di hello, verrà automaticamente sostituito con il testo hello Microsoft. In alternativa, il documento hello potrebbe definire un'entità "MSFTStock" che fa riferimento a un web esterno servizio toofetch hello valore corrente di scorte Microsoft.</p><p>Quindi qualsiasi momento "&MSFTStock;" viene visualizzato nel documento di hello, verrà automaticamente sostituito con prezzo azionario corrente hello. Tuttavia, questa funzionalità può essere sfruttato toocreate rifiuto delle condizioni service (DoS). Un utente malintenzionato è possibile nidificare più entità toocreate un'espansione esponenziale XML di validità che utilizza tutta la memoria disponibile nel sistema hello. </p><p>In alternativa, Jeff può creare un riferimento esterno che consente di trasmettere back un'infinito quantità di dati o che si blocchi semplicemente thread hello. Di conseguenza, tutti i team necessario disabilitare la risoluzione dell'entità XML interno e/o esterni completamente se l'applicazione non usarlo oppure manualmente limitare la quantità hello di memoria e tempo applicazione hello può utilizzare per la risoluzione di entità se questa funzionalità è assolutamente necessario. Se la risoluzione di entità non è richiesta dall'applicazione, disabilitarla. </p>|

### <a name="example"></a>Esempio
Per il codice di .NET Framework, è possibile utilizzare hello approcci seguenti:

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
Si noti il valore predefinito di hello di `ProhibitDtd` in `XmlReaderSettings` è true, ma in `XmlTextReader` è false. Se si utilizza XmlReaderSettings, non è necessario tooset ProhibitDtd tootrue in modo esplicito, ma per i migliori risultati sicurezza è consigliabile effettuare. Si noti che la classe XmlDocument hello consente inoltre la risoluzione dell'entità per impostazione predefinita. 

### <a name="example"></a>Esempio
la risoluzione dell'entità toodisable per XmlDocument, utilizzare hello `XmlDocument.Load(XmlReader)` overload di hello metodo Load e impostare hello proprietà appropriate nella risoluzione toodisable dell'argomento XmlReader hello, come illustrato nel seguente codice hello: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>Esempio
Se la disabilitazione di risoluzione di entità non è possibile per l'applicazione, impostare hello XmlReaderSettings.MaxCharactersFromEntities tooa ragionevole valore della proprietà in base alle esigenze dell'applicazione tooyour. Questo sarà limitato impatto hello di potenziali attacchi di espansione esponenziale. Hello seguente codice viene fornito un esempio di questo approccio: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>Esempio
Se è necessario tooresolve inline entità ma non è necessario tooresolve le entità esterne, impostare hello XmlReaderSettings.XmlResolver proprietà toonull. ad esempio: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Si noti che in MSXML6, ProhibitDTD è impostare tootrue (disattivare l'elaborazione della DTD) per impostazione predefinita. Per il codice Apple OSX/iOS, è possibile usare due parser XML: NSXMLParser e libXML2. 

## <a id="app-verification"></a>Verifica della canonizzazione degli URL nelle applicazioni che utilizzano http.sys

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Tutte le applicazioni che usano http.sys devono seguire le linee guida seguenti:</p><ul><li>Limitare hello URL lunghezza toono 16.384 più caratteri (ASCII o Unicode). Si tratta di hello assoluto lunghezza massima URL in base all'impostazione di Internet Information Services (IIS) 6 hello predefinito. Se possibile, i siti Web devono cercare di mantenere una lunghezza inferiore a tale massimo.</li><li>Utilizzare hello standard i/o file classi di .NET Framework (ad esempio FileStream) come questi si avvale di hello regole canonizzazione in hello .NET FX</li><li>Compilare in modo esplicito un elenco di nomi file noti consentiti.</li><li>Rifiutare in modo esplicito i nomi file noti che non verranno gestiti con rifiuti tramite UrlScan, ossia i file con estensione exe, bat, cmd, com, htw, ida, idq, htr, idc, shtm[l], stm, printer, ini, pol e dat.</li><li>Consente di rilevare hello le eccezioni seguenti:<ul><li>System.ArgumentException (per i nomi di dispositivo)</li><li>System.NotSupportedException (per i flussi di dati)</li><li>System.IO.FileNotFoundException (per i nomi file preceduti da carattere di escape non validi)</li><li>System.IO.DirectoryNotFoundException (per le directory precedute da carattere di escape non valide)</li></ul></li><li>*Non* richiamano tooWin32 file I/O APIs. In un URL non valido restituito normalmente un utente di 400 errore toohello e registrare errore reale hello.</li></ul>|

## <a id="controls-users"></a>Verificare la presenza dei controlli appropriati quando si accettano file dagli utenti

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload) (Caricamento di file senza restrizioni), [File Signature Table](http://www.garykessler.net/library/file_sigs.html) (Tabella delle firme dei file) |
| **Passaggi** | <p>I file caricati rappresentano un rischio significativo di tooapplications.</p><p>Hello molti attacchi è innanzitutto tooget attaccato alcuni toobe sistema toohello di codice. Attacco hello deve quindi solo toofind un codice di hello tooget modo eseguito. L'utilizzo di caricare un file consente autore dell'attacco hello eseguire innanzitutto hello. conseguenze Hello di caricamento del file senza restrizioni possono variare, incluse acquisizione completa del sistema, un overload di file system o un database, sistemi tooback-end di attacchi e semplice alterazione di inoltro.</p><p>Dipende da quale applicazione hello non con file hello caricato e in particolare in cui è archiviato. La convalida sul lato server dei caricamenti di file non è disponibile. Per la funzionalità di caricamento file devono essere implementati i controlli di sicurezza seguenti:</p><ul><li>Controllo dell'estensione di file (deve essere accettato solo un set valido di tipi di file consentiti)</li><li>Limite di dimensione massima dei file</li><li>File non deve essere caricato toowebroot; percorso di Hello deve essere una directory sul disco non di sistema</li><li>Convenzione di denominazione da seguire, in modo che hello nome del file caricato presentano alcuni casualità, pertanto come tooprevent sovrascrive i file</li><li>I file devono essere esaminati per antivirus prima della scrittura su disco toohello</li><li>Verificare che per i caratteri dannosi vengano convalidati nome del file hello e altri metadati (ad esempio, un percorso di file)</li><li>Firma del file di formato deve essere verificata, un utente di caricare un file masqueraded tooprevent (ad esempio, il caricamento di un file exe modificando l'estensione tootxt)</li></ul>| 

### <a name="example"></a>Esempio
Per ultimo punto di hello sulla convalida della firma di formato di file, vedere la classe toohello sotto per informazioni dettagliate: 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>Verificare che nell'applicazione Web vengano usati parametri indipendenti dai tipi per l'accesso ai dati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Se si utilizza la raccolta di parametri hello, SQL considera hello input è un valore letterale anziché come codice eseguibile. raccolta di parametri Hello può essere tooenforce utilizzati vincoli di tipo e lunghezza su dati di input. I valori di fuori intervallo hello generano un'eccezione. Se non vengono utilizzati parametri SQL indipendenti dai tipi, gli utenti malintenzionati potrebbero essere attacchi intrusivi nel codice in grado di tooexecute incorporati nell'input non filtrato hello.</p><p>Utilizzare i parametri indipendenti dai tipi quando costruzione SQL esegue una query tooavoid possibili attacchi SQL injection che possono verificarsi con input non filtrato. È possibile usare parametri indipendenti dai tipi con stored procedure e con istruzioni SQL dinamiche. I parametri vengono considerati come valori letterali dal database hello e non come codice eseguibile. Viene anche eseguito il controllo del tipo e della lunghezza dei parametri.</p>|

### <a name="example"></a>Esempio 
Hello codice seguente viene illustrato come toouse parametri di tipo sicuro con hello SqlParameterCollection quando si chiama una stored procedure. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Nel precedente esempio di codice di hello, hello input non può essere più lungo di 11 caratteri. Se i dati di hello non è conforme toohello tipo o la lunghezza definita dal parametro hello, hello classe SqlParameter genera un'eccezione. 

## <a id="binding-mvc"></a>Utilizzare un modello separato l'associazione di classi o filtro elenchi tooprevent MVC assegnazione massa vulnerabilità

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Gli attributi dei metadati](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [pubblica chiave sicurezza attenuazione delle vulnerabilità e](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [tooMass Guida completa assegnazione in ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [Introduzione a Entity Framework con MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **Passaggi** | <ul><li>**Quando è consigliabile controllare eventuali vulnerabilità all'overposting?** Le vulnerabilità all'overposting si possono verificare ovunque si associno classi modello dall'input utente. I framework come MVC possono rappresentare i dati utente in classi .NET personalizzate, tra cui Plain Old CLR Object (POCO). MVC popola automaticamente queste classi di modello con i dati di richiesta di hello, fornendo in modo adeguato per la gestione di input dell'utente. Quando tali classi includono proprietà che non deve essere impostata dall'utente hello, un'applicazione hello può essere vulnerabili attacchi tooover registrazione, che consentono il controllo utente di dati che l'applicazione hello mai usata. Come associazione di modelli MVC, tecnologie di accesso ai database, ad esempio BizTalk Mapper relazionale/come Entity Framework supportano spesso anche l'utilizzo di dati del database toorepresent oggetti POCO. Queste classi di modello di dati forniscono hello stesso facilitare la gestione dei dati di database come MVC avviene nella gestione di input dell'utente. Poiché il database sia MVC e hello supporta modelli simili, come gli oggetti POCO, sembra hello tooreuse facile stesso classi per entrambi gli scopi. Questo ha esito negativo dell'esercitazione toopreserve separazione di problemi e è un'area comune in cui sono di proprietà non intenzionali esposti toomodel associazione, l'abilitazione di attacchi di registrazione in eccesso.</li><li>**Perché non è consentito usare my classi del modello di database non filtrato come azioni di MVC toomy parametri? -** Associazione del modello MVC perché assocerà qualsiasi elemento in tale classe. Anche se i dati non viene visualizzata nella vista, che un utente malintenzionato può inviare una richiesta HTTP con i dati inclusi hello e MVC verrà grazie associarlo perché l'azione che la classe di database è la forma hello dei dati è necessario accettare input dell'utente.</li><li>**Perché devo interessano hello forma utilizzata per l'associazione modello? -** L'associazione di modelli utilizzando ASP.NET MVC con i modelli di ampi espone gli attacchi tooover registrazione un'applicazione. Dati dell'applicazione gli utenti malintenzionati toochange oltre quali hello dello sviluppatore, ad esempio si esegue l'override di prezzo hello per un elemento o hello privilegi di sicurezza per un account è stato possibile abilitare la registrazione in eccesso. Le applicazioni devono utilizzare specifici per le operazioni di associazione modelli (o elenchi di filtri di proprietà consentiti specifico) tooprovide un contratto esplicito per i quali tooallow di input non attendibile tramite l'associazione di modelli.</li><li>**La presenza di modelli di associazione separati è solo una duplicazione del codice?** No, è una separazione dei compiti. Se si riutilizzano i modelli di database nei metodi di azione, sono segnalare qualsiasi proprietà (o secondari) in una classe può essere impostata dall'utente hello in una richiesta HTTP. Se non si desidera toodo MVC, è necessario un elenco di filtri o tooshow di forma una classe separata MVC quali dati possono provenire da invece l'input dell'utente.</li><li>**Se dispone di modelli di binding distinto per l'input dell'utente, è necessario tooduplicate tutti gli attributi di annotazione my dati? -** Non necessariamente. È possibile utilizzare MetadataTypeAttribute sui metadati di toohello toolink per la classe modello hello database in una classe di associazione del modello. Si noti solo che hello tipo a cui fa riferimento hello MetadataTypeAttribute devono essere un subset di hello riferimento al tipo (può avere un numero inferiore di proprietà, ma non più).</li><li>**Lo spostamento di dati tra i modelli dell'input utente e i modelli del database è un'attività tediosa. È possibile copiare semplicemente tutte le proprietà con la reflection?** Sì. Hello devono solo le proprietà che vengono visualizzati nei modelli di associazione hello hello quelli che significa toobe sicuri per l'input dell'utente. Non vi è alcun motivo di sicurezza che impedisce l'utilizzo di reflection toocopy su tutte le proprietà che esistono in comune tra questi due modelli.</li><li>**Come funziona [Bind(Exclude ="â€¦")]? È possibile usare questo attributo anziché modelli di associazione separati?** Questo approccio non è consigliabile. Usando [Bind(Exclude ="â€¦")], qualsiasi nuova proprietà è associabile per impostazione predefinita. Quando viene aggiunta una nuova proprietà, elementi di tookeep tooremember un passaggio aggiuntivo è sicuro, anziché con progettazione hello essere protetto per impostazione predefinita. A seconda di sviluppatore hello è rischioso controllo elenco ogni volta che viene aggiunta una proprietà.</li><li>**[Bind(Include ="â€¦")] è utile per le operazioni di modifica?** No. [Bind(Include ="â€¦")] è adatto solo per operazioni di tipo INSERT, ossia per l'aggiunta di nuovi dati. Per le operazioni di aggiornamento stile (revisione dei dati esistenti), utilizzare un altro approccio, ad esempio con i modelli di associazione separati o passando un elenco delle proprietà consentite tooUpdateModel TryUpdateModel esplicito. Aggiunta di un [associare (Include = "¦ â €")] attributo in un'operazione di modifica significa che MVC crea un'istanza dell'oggetto e imposta solo hello elencate le proprietà, chiudere tutti gli altri valori predefiniti. Quando viene mantenuti dati hello, che sostituirà completamente entità esistente hello, reimpostare i valori hello relativi alle impostazioni predefinite tootheir proprietà omesso. Ad esempio, se è stato omesso IsAdmin da un [associare (Include = "¦ â €")] attributo in un'operazione di modifica, qualsiasi utente il cui nome è stato modificato tramite questa azione sarebbe tooIsAdmin reset = false (qualsiasi utente modificato comporterebbe la perdita dello stato di amministratore). Se si desidera tooprevent Aggiorna le proprietà di toocertain, utilizzare uno dei hello altri approcci sopra. Si noti che alcune versioni degli strumenti MVC generano classi controller con [Bind(Include ="â€¦")] nelle azioni di modifica e prevedono che la rimozione di una proprietà dall'elenco impedisca attacchi di overposting. Tuttavia, come descritto in precedenza, questo approccio non funziona come previsto e invece reimposterà i valori predefiniti di hello omesso proprietà tootheir di tutti i dati.</li><li>**Per le operazioni di creazione, esistono controindicazioni all'uso di [Bind(Include ="â€¦")] anziché di modelli di associazione separati?** Sì. Per prima cosa, questo approccio non funziona per gli scenari di modifica e richiede quindi la gestione di due approcci separati per la mitigazione di tutte le vulnerabilità all'overposting. I modelli di associazione secondo, separato applicano la separazione dei compiti tra forma hello utilizzata per la forma di input e hello utente utilizzata per la persistenza, un elemento [associare (Include = "â €¦")] non include. In terzo luogo, si noti che [associare (Include = "â €¦")] possono gestire solo le proprietà di primo livello; è possibile consentire solo parti di sottoproprietà (ad esempio "Details.Name") nell'attributo hello. Infine ed eventualmente soprattutto, utilizzando [associare (Include = "â €¦")] consente di aggiungere un passaggio aggiuntivo che deve essere memorizzato qualsiasi classe di hello ora viene utilizzata per l'associazione di modelli. Se un nuovo metodo di azione associa direttamente la classe di dati toohello e dimentica tooinclude un [associare (Include = "¦ â €")] attributo, può essere vulnerabile tooover registrazione attacchi, in modo hello [associare (Include = "¦ â €")] approccio è leggermente meno sicura per impostazione predefinita. Se si utilizza [associare (Include = "â €¦")], prestare attenzione sempre tooremember toospecify, ogni volta che le classi di dati vengono visualizzati come parametri di metodo di azione.</li><li>**Per le operazioni di creazione, per quanto riguarda l'inserimento di hello [associare (Include = "â €¦")] attributo sulla classe di modello hello stessa? Non questo approccio evita hello necessità tooremember inserimento hello attributo in ogni metodo di azione? -** Questo approccio funziona in alcuni casi. Utilizzo [associare (Include = "â €¦")] sul tipo di modello hello stesso (anziché su parametri di azione utilizzando questa classe), evitare di hello tooinclude tooremember necessità di hello [associare (Include = "â €¦")] attributo in ogni metodo di azione. Utilizzo efficiente di attributo hello direttamente sulla classe hello crea un'area separata della superficie di questa classe per scopi di associazione del modello. Questo approccio, tuttavia, supporta una sola forma di associazione di modelli per classe modello. Se un metodo di azione richiesta tooallow associazione del modello di un campo (ad esempio, un amministratore di sola azione che aggiorna i ruoli utente) e altre azioni tooprevent di associazione di modelli di questo campo, questo approccio non funzionerà. Ogni classe può avere solo una forma di associazione del modello; Se diverse azioni necessario forme associazione modello diverso, è necessario toorepresent queste forme utilizzando entrambe le classi di modello separato associazione separare o separare [associare (Include = "â €¦")] attributi sui metodi di azione hello.</li><li>**Che cosa sono i modelli di associazione? Sono che essi hello stesso elemento sotto forma di visualizzazione di modelli? -** Sono due concetti correlati. termine Hello tooa classe del modello utilizzato in un'azione fa riferimento di modello di associazione è l'elenco di parametri (forma hello passato dal metodo di azione toohello associazione modello MVC). modello di visualizzazione termine Hello fa riferimento a classe di modello tooa passata da una vista tooa metodo di azione. Utilizzo di un modello di visualizzazione specifica è un approccio comune per passare dati da una vista tooa metodo di azione. Spesso, questa forma è particolarmente adatta per l'associazione di modelli e modello di visualizzazione di hello termine può essere utilizzato toorefer hello stesso modello utilizzato in entrambe le posizioni. toobe preciso, questa procedura comunica in particolare sull'associazione di modelli, porre l'attenzione sulla forma hello passato toohello azione, che è la cosa importante per scopi di assegnazione di massa.</li></ul>| 

## <a id="rendering"></a>Codificare web non attendibile output precedente toorendering

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, Web Form, MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Come tooprevent Cross-site scripting in ASP.NET](http://msdn.microsoft.com/library/ms998274.aspx), [Cross-site Scripting](http://cwe.mitre.org/data/definitions/79.html), [foglio irregolarità prevenzione di XSS (Cross-Site Scripting)](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **Passaggi** | Cross-site scripting (comunemente abbreviato XSS) è un vettore di attacco per servizi online o qualsiasi componente o l'applicazione che elabora l'input dal web hello. Vulnerabilità XSS potrebbe consentire un utente malintenzionato tooexecute script su un altro computer mediante un'applicazione web vulnerabile. Script dannosi possono essere toosteal utilizzati cookie e in caso contrario manomettere macchina della vittima tramite JavaScript. È possibile impedire attacchi XSS convalidando l'input utente e verificando che il formato e la codifica siano corretti prima di eseguirne il rendering in una pagina Web. La convalida dell'input e la codifica dell'output possono essere eseguite con Web Protection Library. Per codice gestito (C\#, Visual Basic.NET e così via), utilizzare uno o più appropriato di metodi di codifica da hello libreria Web protezione (Anti-XSS), a seconda del contesto di hello in Ottiene che viene presentato l'input dell'utente hello:| 

### <a name="example"></a>Esempio

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>Eseguire la convalida dell'input e applicare filtri a tutte le proprietà del modello di tipo stringa

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Adding Validation](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation) (Aggiunta della convalida), [Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx) (Convalida dei dati del modello in un'applicazione MVC), [Principi guida per le applicazioni ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Passaggi** | <p>Tutti i parametri di input hello devono essere convalidati prima che vengano utilizzate in tooensure applicazione hello che un'applicazione hello è protette contro gli input dell'utente malintenzionato. Convalidare i valori di input hello utilizzando le convalide di espressione regolare sul lato server con una strategia di convalida whitelist. Input utente unsanitized / parametri passati a metodi toohello possono causare codice vulnerabilità di tipo injection.</p><p>Per le applicazioni Web, i punti di ingresso possono includere anche campi modulo, stringhe di query, cookie, intestazioni HTTP e parametri del servizio Web.</p><p>Hello seguenti controlli di convalida dell'input devono essere eseguiti durante l'associazione di modelli:</p><ul><li>le proprietà del modello Hello devono essere annotate con l'annotazione RegularExpression, per accettare i caratteri consentiti e la lunghezza massima consentita</li><li>i metodi del controller Hello devono eseguire ModelState validità</li></ul>|

## <a id="richtext"></a>Applicazione della purificazione nei campi modulo che accettano tutti i caratteri, ad esempio un editor di testo RTF

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Encode Unsafe Input](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3) (Codificare l'input non sicuro), [HtmlSanitizer](https://github.com/mganss/HtmlSanitizer) |
| **Passaggi** | <p>Identificare tutti i tag di markup statico che si desidera toouse. Una pratica comune è la formattazione di elementi toosafe HTML, ad esempio toorestrict `<b>` (grassetto) e `<i>` (in corsivo).</p><p>Prima di scrivere dati hello, codificare in formato HTML. In questo modo di qualsiasi script dannoso-safe, di conseguenza toobe gestito come testo, non come codice eseguibile.</p><ol><li>Disabilitare la richiesta ASP.NET convalida aggiungendo hello hello ValidateRequest = "false" attributo toohello @ direttiva della pagina</li><li>Codificare l'input di stringa hello con metodo HtmlEncode hello</li><li>Usa chiamata relativo tooselectively metodo Replace rimuovere hello codifica per gli elementi di hello HTML che si desidera toopermit e StringBuilder</li></ol><p>Hello riferimenti pagina aggiuntivo hello disabilita la convalida delle richieste ASP.NET impostando `ValidateRequest="false"`. Si codifica in HTML hello di input e consente in modo selettivo hello `<b>` e `<i>` in alternativa, può anche essere usata una libreria .NET per la purificazione dei processi HTML.</p><p>HtmlSanitizer è una libreria .NET per la pulizia dei frammenti HTML e documenti da costrutti che possono causare attacchi tooXSS. Usa AngleSharp tooparse, modificare e il rendering di HTML e CSS. HtmlSanitizer può essere installato come un pacchetto NuGet e hello l'input dell'utente può essere passato tramite HTML o CSS purificazione i metodi pertinenti, come applicabile, sul lato server hello. Si noti che la purificazione deve essere presa in considerazione come controllo di sicurezza solo come ultima opzione.</p><p>La convalida dell'input e la codifica dell'output sono considerati controlli di sicurezza più efficienti.</p> |

## <a id="inbuilt-encode"></a>Non assegnare toosinks elementi DOM che non dispongono di codifica incorporato

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | Molte funzioni JavaScript non eseguono la codifica per impostazione predefinita. Quando si assegnano gli elementi tooDOM di input non attendibile tramite tali funzioni, può comportare tra le esecuzioni di script (XSS) del sito.| 

### <a name="example"></a>Esempio
Gli esempi seguenti non sono sicuri: 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
Non usare `innerHtml`. Usare invece `innerText`. Analogamente, usare `$("#elm").text()` invece di `$("#elm").html()`. 

## <a id="redirect-safe"></a>Convalidare tutti i reindirizzamenti all'interno di un'applicazione hello sono chiuso o completati in modo sicuro

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Hello Framework di autorizzazione OAuth 2.0 - redirector aperto](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **Passaggi** | <p>Progettazione di applicazioni che richiedono percorso fornito dall'utente di reindirizzamento tooa necessario vincolare hello reindirizzamento possibili destinazioni tooa "sicura" elenco predefinito di siti o domini. Tutti i reindirizzamenti di un'applicazione hello devono essere chiuso/safe.</p><p>toodo questo:</p><ul><li>Identificare tutti i reindirizzamenti.</li><li>Implementare una procedura di mitigazione appropriata per ogni reindirizzamento. Le procedure di mitigazione appropriate includono un elenco elementi consentiti di reindirizzamento o la conferma dell'utente. Se un servizio o un sito Web con una vulnerabilità causata da reindirizzamenti aperti usa i provider di identità Facebook/OAuth/OpenID, un utente malintenzionato può rubare il token di accesso di un utente e rappresentare tale utente. Si tratta di un rischio inerente quando si utilizza OAuth, è documentata nella RFC 6749 "hello Framework di autorizzazione OAuth 2.0", sezione 10.15 "aprire reindirizza" in modo analogo, le credenziali degli utenti possono essere compromessa da attacchi di phishing spear utilizzano reindirizzamenti aperti</li></ul>|

## <a id="string-method"></a>Implementare la convalida dell'input in un tutti i parametri di tipo stringa accettati dai metodi del controller

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx) (Convalida dei dati del modello in un'applicazione MVC), [Principi guida per le applicazioni ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Passaggi** | Per i metodi che accettano come argomento solo un tipo di dati primitivo e non modelli, deve essere eseguita la convalida dell'input con un'espressione regolare. In questo caso, è necessario usare Regex.IsMatch con un criterio regex valido. Se non corrisponde a input hello hello di espressione regolare specificata, controllo deve non procedere e deve essere visualizzato un avviso adeguato riguardante un errore di convalida.| 

## <a id="dos-expression"></a>Impostare il timeout del limite superiore per l'elaborazione DoS tooprevent a causa di espressioni regolari toobad delle espressioni regolari

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, Web Form, MVC 5, MVC 6  |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Proprietà DefaultRegexMatchTimeout](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **Passaggi** | tooensure attacchi denial of service contro creato in espressioni regolari, che causano un lotto del backtracking, l'impostazione di timeout predefinito globale hello. Se il tempo di elaborazione hello impiega più tempo hello è definito un limite superiore, genera un'eccezione di Timeout. Se non è configurato, il timeout di hello sarebbe infinito.| 

### <a name="example"></a>Esempio
Ad esempio, hello seguente configurazione genererà un RegexMatchTimeoutException, se l'elaborazione di hello richiede più di 5 secondi: 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>Evitare di usare Html.Raw nelle visualizzazioni Razor

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Applicazione Web. | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| Passaggio | Le pagine Web ASP.Net (Razor) eseguono la codifica HTML automatica. A tutte le stringhe stampate da nugget di codice incorporati (blocchi @) viene applicata automaticamente la codifica HTML. Quando viene richiamato `HtmlHelper.Raw`, tuttavia, questo metodo restituisce markup senza codifica HTML. Se `Html.Raw()` metodo helper viene utilizzato, consente di ignorare hello codifica protezione automatica che fornisce Razor.|

### <a name="example"></a>Esempio
L'esempio seguente non è sicuro: 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
Non utilizzare `Html.Raw()` a meno che non è necessario toodisplay markup. Questo metodo non esegue implicitamente la codifica dell'output. Usare altri helper ASP.NET, ad esempio `@Html.DisplayFor()` 

## <a id="stored-proc"></a>Non usare query dinamiche nelle stored procedure

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Database | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Un attacco SQL injection sfrutta le vulnerabilità nei comandi arbitrari di convalida dell'input toorun nel database di hello. Può verificarsi quando l'applicazione utilizza input tooconstruct dinamica tooaccess istruzioni SQL hello database. nonché se il codice usa stored procedure costituite da stringhe passate contenenti input utente non elaborato. Utilizza hello attacco SQL injection, autore dell'attacco hello può eseguire comandi arbitrari nel database di hello. Tutte le istruzioni SQL (incluso istruzioni SQL hello nelle stored procedure) devono essere con parametri. Istruzioni SQL con parametri accetterà i caratteri che hanno un significato speciale tooSQL (ad esempio, la virgoletta singola) senza problemi in quanto sono fortemente tipizzati. |

### <a name="example"></a>Esempio
L'esempio seguente è una stored procedure dinamica non sicura: 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>Esempio
Di seguito è hello stessa stored procedure è stata implementata in modo sicuro: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>Verificare l'esecuzione della convalida dei modelli nei metodi di API Web

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Model Validation in ASP.NET Web API ](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) (Convalida dei modelli in un'API Web ASP.NET) |
| **Passaggi** | Quando un client invia l'API web tooa di dati, è prima di eseguire qualsiasi elaborazione dati hello toovalidate obbligatorio. Per ASP.NET Web API che accettano i modelli come input, utilizzare le annotazioni dei dati sulle regole di convalida di modelli tooset sulle proprietà hello del modello di hello.|

### <a name="example"></a>Esempio
Hello seguente codice illustra hello stesso: 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>Esempio
Nel metodo di azione hello del controller API hello, validità del modello di hello è toobe verificate in modo esplicito come illustrato di seguito: 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Implementare la convalida dell'input in tutti i parametri di tipo stringa accettati dai metodi di API Web

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, MVC 5, MVC 6 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx) (Convalida dei dati del modello in un'applicazione MVC), [Principi guida per le applicazioni ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Passaggi** | Per i metodi che accettano come argomento solo un tipo di dati primitivo e non modelli, deve essere eseguita la convalida dell'input con un'espressione regolare. In questo caso, è necessario usare Regex.IsMatch con un criterio regex valido. Se non corrisponde a input hello hello di espressione regolare specificata, controllo deve non procedere e deve essere visualizzato un avviso adeguato riguardante un errore di convalida.|

## <a id="typesafe-api"></a>Verificare che nell'API Web vengano usati parametri indipendenti dai tipi per l'accesso ai dati

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | N/D  |
| **Passaggi** | <p>Se si utilizza la raccolta di parametri hello, SQL considera hello input è un valore letterale anziché come codice eseguibile. raccolta di parametri Hello può essere tooenforce utilizzati vincoli di tipo e lunghezza su dati di input. I valori di fuori intervallo hello generano un'eccezione. Se non vengono utilizzati parametri SQL indipendenti dai tipi, gli utenti malintenzionati potrebbero essere attacchi intrusivi nel codice in grado di tooexecute incorporati nell'input non filtrato hello.</p><p>Utilizzare i parametri indipendenti dai tipi quando costruzione SQL esegue una query tooavoid possibili attacchi SQL injection che possono verificarsi con input non filtrato. È possibile usare parametri indipendenti dai tipi con stored procedure e con istruzioni SQL dinamiche. I parametri vengono considerati come valori letterali dal database hello e non come codice eseguibile. Viene anche eseguito il controllo del tipo e della lunghezza dei parametri.</p>|

### <a name="example"></a>Esempio
Hello codice seguente viene illustrato come toouse parametri di tipo sicuro con hello SqlParameterCollection quando si chiama una stored procedure. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Nel precedente esempio di codice di hello, hello input non può essere più lungo di 11 caratteri. Se i dati di hello non è conforme toohello tipo o la lunghezza definita dal parametro hello, hello classe SqlParameter genera un'eccezione. 

## <a id="sql-docdb"></a>Usare query SQL con parametri per Cosmos DB

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [Announcing SQL Parameterization in DocumentDB](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) (Annuncio della parametrizzazione SQL in DocumentDB) |
| **Passaggi** | Nonostante DocumentDB supporti solo query di sola lettura, se le query vengono costruite con la concatenazione con input utente sono comunque possibili attacchi SQL injection. Potrebbe essere possibile per un toodata di accesso utente toogain che non devono accedere all'interno di hello stessa raccolta creando una query SQL dannose. Se le query vengono costruite in base all'input utente, usare query SQL con parametri. |

## <a id="schema-binding"></a>WCF: convalida dell'input tramite l'associazione allo schema

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **Passaggi** | <p>Mancanza di convalida di clienti potenziali attacchi intrusivi nel codice di tipo toodifferent.</p><p>Convalida del messaggio rappresenta una linea di difesa per la protezione dell'applicazione WCF hello. Con questo approccio, si convalidano i messaggi mediante operazioni del servizio WCF tooprotect schemi da attacchi esterni da un client dannoso. Convalidare tutti i messaggi ricevuti dal client di hello client tooprotect hello da attacchi esterni da un servizio dannoso. Convalida del messaggio rende un toovalidate possibili messaggi quando operazioni utilizzano contratti di messaggio o contratti dati, che non possono essere eseguiti tramite la convalida dei parametri. Convalida del messaggio consente toocreate la logica di convalida all'interno di schemi, in tal modo fornendo più flessibilità e ridurre i tempi di sviluppo. Gli schemi possono essere riutilizzati tra applicazioni diverse all'interno dell'organizzazione hello, creazione di standard per la rappresentazione di dati. Inoltre, convalida dei messaggi consente operazioni tooprotect quando utilizzano tipi di dati più complessi che coinvolgono contratti che rappresenta la logica di business.</p><p>convalida del messaggio tooperform, è innanzitutto necessario generare uno schema che rappresenta le operazioni di hello dei tipi di dati del servizio e hello utilizzati da tali operazioni. È quindi possibile creare una classe .NET che implementa un controllo dei messaggi client personalizzate e dispatcher personalizzato messaggi controllo toovalidate hello messaggi inviati/ricevuti da e verso il servizio di hello. Implementare una convalida del messaggio tooenable comportamento dell'endpoint personalizzato sul client hello e servizio hello. Infine, si implementa un elemento di configurazione personalizzata su una classe hello consente tooexpose hello estesi comportamento dell'endpoint nel file di configurazione hello del client di hello o un servizio di hello"</p>|

## <a id="parameters"></a>WCF: convalida dell'input tramite controlli parametro

| Titolo                   | Dettagli      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase SDL**               | Compilare |  
| **Tecnologie applicabili** | Generico, .NET Framework 3 |
| **Attributes (Attributi) (Attributi)**              | N/D  |
| **Riferimenti**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **Passaggi** | <p>Convalida di input e i dati rappresenta un importante difesa nella protezione hello dell'applicazione WCF. È necessario convalidare tutti i parametri esposti in WCF operazioni tooprotect hello del servizio da attacchi esterni da un client dannoso. Al contrario, è anche necessario convalidare tutti i valori restituiti ricevuti dal client di hello client tooprotect hello da attacchi esterni da un servizio dannoso</p><p>WCF fornisce punti di estendibilità diversi che consentono di comportamento di runtime WCF hello toocustomize mediante la creazione di estensioni personalizzate. Messaggio di controllo e i controlli del parametro sono due meccanismi di estensibilità utilizzato toogain maggiore controllo sui dati hello passando tra un client e un servizio. È necessario utilizzare i controlli del parametro per la convalida dell'input e utilizzare i controlli messaggi solo quando è necessario l'intero messaggio hello tooinspect trasferimento da e verso un servizio.</p><p>convalida dell'input tooperform, generare una classe .NET che implementa un controllo del parametro personalizzato in parametri toovalidate ordine sulle operazioni nel servizio. Quindi implementare una convalida tooenable comportamento di endpoint personalizzato nel client hello e servizio hello. Infine, un elemento di configurazione personalizzato verrà implementata nella classe hello che consente di tooexpose hello estesi comportamento dell'endpoint nel file di configurazione hello del client di hello o un servizio di hello</p>|

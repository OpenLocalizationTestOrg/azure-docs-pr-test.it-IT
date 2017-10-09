---
title: aaaLearn sui criteri di sicurezza di Azure microservizi | Documenti Microsoft
description: Una panoramica di come toorun un'applicazione di Service Fabric nel sistema e gli account di sicurezza locale, compreso il punto di SetupEntry hello in cui un'applicazione deve tooperform alcune privilegiato azione prima che venga avviato
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a>Configurare i criteri di sicurezza per l'applicazione
Tramite Azure Service Fabric, è possibile proteggere le applicazioni in esecuzione nel cluster hello con account utente diversi. Service Fabric consente anche di hello sicuro le risorse usate dalle applicazioni in fase di hello della distribuzione con account utente di hello, ad esempio, file, directory e i certificati. In questo modo le applicazioni in esecuzione, anche in un ambiente ospitato condiviso, sono reciprocamente protette.

Per impostazione predefinita, le applicazioni di Service Fabric eseguiti con account di hello cui viene eseguito il processo Fabric.exe hello. Service Fabric fornisce anche funzionalità di hello toorun applicazioni tramite un account di sistema locale, che viene specificato nel manifesto dell'applicazione hello o un account utente locale. I tipi di account supportati dal sistema locale sono **LocalUser**, **NetworkService**, **LocalService** e **LocalSystem**.

 Quando si esegue Service Fabric in Windows Server nel Data Center tramite il programma di installazione di hello autonomo, è possibile utilizzare l'account di dominio Active Directory, inclusi gli account del servizio gestito di gruppo.

È possibile definire e creare gruppi di utenti in modo che è possibile aggiungere uno o più utenti tooeach gruppo toobe gestiti insieme. Ciò è utile quando sono presenti più utenti per i punti di ingresso del servizio diverso e devono toohave determinati privilegi comune che sono disponibili a livello di gruppo hello.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Configurare i criteri di hello per un punto di ingresso del programma di installazione del servizio
Come descritto in hello [modello applicativo](service-fabric-application-model.md), hello punto di ingresso, il programma di installazione **SetupEntryPoint**, è un punto di ingresso con privilegi che viene eseguito con hello stesso credenziali come Service Fabric (in genere hello *NetworkService* account) prima di qualsiasi altro punto di ingresso. file eseguibile Hello specificato da **EntryPoint** è in genere l'host del servizio hello con esecuzione prolungata. Pertanto, con una voce di programma di installazione separato punto si evita host del servizio hello toorun eseguibile con privilegi elevati per lunghi periodi di tempo. Hello eseguibile che **EntryPoint** specifica viene eseguito dopo **SetupEntryPoint** termina correttamente. Hello processo risultante viene monitorato e riavviato e inizia nuovamente con **SetupEntryPoint** se mai termina o arresti anomali.

esempio Hello è riportato un esempio di manifesto servizio semplice che mostra hello SetupEntryPoint e il punto di ingresso principale per il servizio hello hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a>Configurare i criteri di hello utilizzando un account locale
Dopo aver configurato hello servizio toohave un punto di ingresso del programma di installazione, è possibile modificare le autorizzazioni di sicurezza hello utilizzabile nel manifesto dell'applicazione hello. Hello di esempio seguente viene illustrato come tooconfigure hello toorun servizio con privilegi di account utente amministratore.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

Creare prima di tutto una sezione **Principals** con un nome utente, ad esempio SetupAdminUser. Questo indica che l'utente hello è un membro del gruppo di amministratori di sistema hello.

Quindi, in hello **oggetto ServiceManifestImport** sezione, configurare un criterio tooapply questa entità troppo**SetupEntryPoint**. In questo modo Service Fabric che quando hello **MySetup.bat** file viene eseguito, dovrebbe essere `RunAs` con privilegi di amministratore. Disponendo di *non* applicato a un punto di ingresso principale toohello criteri, il codice hello in **MyServiceHost.exe** viene eseguito il sistema hello **NetworkService** account. Si tratta di account predefinito hello che vengono eseguiti tutti i punti di ingresso del servizio.

Aggiungere ora hello file MySetup.bat toohello Visual Studio progetto tootest hello privilegi di amministratore. In Visual Studio, fare clic sul progetto servizio hello e aggiungere un nuovo file denominato MySetup.bat.

Verificare quindi che file MySetup.bat hello è incluso nel pacchetto di servizio hello. Per impostazione predefinita, non è incluso. Selezionare il file hello, menu di scelta rapida hello tooget destro e scegliere **proprietà**. Nella finestra di dialogo Proprietà hello, assicurarsi che **copiare tooOutput Directory** è troppo**copia se più recente**. Vedere la seguente schermata hello.

![CopyToOutput di Visual Studio per il file batch SetupEntryPoint][image1]

Ora aprire il file MySetup.bat hello e aggiungere hello seguenti comandi:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Successivamente, compilare e distribuire cluster di sviluppo locale tooa soluzione hello. Dopo aver avviato il servizio di hello, come illustrato in Service Fabric Explorer, è possibile visualizzare che file hello MySetup.bat ha avuto esito positivo in un due modi. Avviare un prompt dei comandi di PowerShell e digitare:

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Quindi, annotare il nome di hello del nodo di hello in cui il servizio di hello è stato distribuito e avviato, ad esempio, in Service Fabric Explorer - nodo 2. Passare toohello applicazione istanza lavoro cartella toofind hello file out.txt che Mostra valore hello **TestVariable**. Ad esempio, se questo servizio è stato distribuito tooNode 2, è possibile passare il percorso di toothis per hello **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Configurare criteri di hello tramite gli account di sistema locale
Spesso, è preferibile toorun script di avvio hello utilizzando un account di sistema locale anziché un account amministratore. Esecuzione di criteri di RunAs hello come membro del gruppo Administrators in genere non funziona correttamente poiché macchine dispongono di controllo accesso utente (UAC) abilitata per impostazione predefinita hello. In questi casi, **hello consiglia hello toorun SetupEntryPoint come LocalSystem, anziché come un gruppo di utenti locale aggiunto tooAdministrators**. Hello riportato di seguito impostazione hello SetupEntryPoint toorun come LocalSystem:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>Avviare i comandi PowerShell da un punto di ingresso dell'installazione
toorun PowerShell da hello **SetupEntryPoint** punto, è possibile eseguire **PowerShell.exe** in un file batch che punta tooa PowerShell file. Aggiungere innanzitutto un progetto di servizio toohello file di PowerShell, ad esempio, **MySetup.ps1**. Ricordare hello tooset *copia se più recente* proprietà in modo che tale file hello è anche incluso nel pacchetto di servizio hello. Hello esempio seguente viene illustrato un file batch di esempio che avvia un file di PowerShell denominato MySetup.ps1, che consente di impostare una variabile di ambiente system denominata **TestVariable**.

MySetup.bat toostart un file di PowerShell:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

Nel file PowerShell hello aggiungere hello tooset una variabile di ambiente di sistema seguente:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> Per impostazione predefinita, quando viene eseguito il file batch di hello, Cerca nella cartella dell'applicazione hello **lavoro** per i file. In questo caso, quando MySetup.bat è in esecuzione, si vuole che questo hello toofind MySetup.ps1 file hello stessa cartella, ovvero un'applicazione hello **pacchetto di codice** cartella. toochange questa cartella, la cartella di lavoro hello set:
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a>Uso del reindirizzamento della console per il debug locale
In alcuni casi, è utile toosee output della console hello dall'esecuzione di uno script a scopo di debug. toodo, è possibile impostare un criterio di reindirizzamento della console, che scrive file tooa output di hello. Hello file di output viene chiamato cartella dell'applicazione scritta toohello **log** nel nodo hello in cui un'applicazione hello viene distribuita ed eseguita. (Vedere dove toofind in hello sopra riportato.)

> [!WARNING]
> Non utilizzare mai criterio di reindirizzamento console hello in un'applicazione che viene distribuita nell'ambiente di produzione, perché ciò può influire sul failover dell'applicazione hello. Usare questa opzione *solo* a scopo di sviluppo e debug locale.  
> 
> 

Hello esempio seguente viene illustrato il reindirizzamento della console con un valore FileRetentionCount impostazione hello:

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Se si modifica ora hello MySetup.ps1 file toowrite un **Echo** comando, si scriverà toohello i file di output a scopo di debug:

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Dopo avere eseguito il debug dello script, rimuovere immediatamente i criteri di reindirizzamento della console**.

## <a name="configure-a-policy-for-service-code-packages"></a>Configurare i criteri per i pacchetti di codice del servizio
In hello passaggi precedenti, si è visto come tooapply un tooSetupEntryPoint criteri RunAs. Vediamo un po' più approfondita in come entità diverse toocreate che possono essere applicate come servizio criteri.

### <a name="create-local-user-groups"></a>Creare gruppi di utenti locali
È possibile definire e creare gruppi di utenti che consentono di utilizzare uno o più utenti toobe aggiunto tooa del gruppo. Ciò è utile se sono presenti più utenti per i punti di ingresso del servizio diverso e devono toohave determinati privilegi comune che sono disponibili a livello di gruppo hello. Hello esempio seguente viene illustrato un gruppo locale denominato **LocalAdminGroup** che disponga dei privilegi di amministratore. Due utenti, Customer1 e Customer2, diventano membri di questo gruppo locale.

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a>Creare utenti locali
È possibile creare un utente locale che può essere utilizzati toohelp protetto come un servizio all'interno di un'applicazione hello. Quando un **UtenteLocale** tipo di account viene specificato nella sezione di entità hello del manifesto dell'applicazione hello, Service Fabric crea gli account utente locali nei computer in cui viene distribuita un'applicazione hello. Per impostazione predefinita, questi account non dispone hello nomi identici a quelli specificati in un'applicazione hello manifesto (ad esempio, nel seguente esempio hello Customer3). Vengono invece generati in modo dinamico e hanno password casuali.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Se un'applicazione richiede che la password e account utente di hello corrispondere in tutti i computer (ad esempio, l'autenticazione NTLM tooenable), manifesto del cluster hello necessario impostare NTLMAuthenticationEnabled tootrue. Hello manifesto del cluster deve inoltre specificare un NTLMAuthenticationPasswordSecret utilizzato toogenerate hello stessa password in tutti i computer.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Assegnare i criteri toohello pacchetti di codice di servizio
Hello **RunAsPolicy** sezione un **oggetto ServiceManifestImport** Specifica account hello dalla sezione entità hello che deve essere utilizzati toorun un pacchetto di codice. Codice pacchetti dal servizio hello manifesto inoltre associa gli account utente nella sezione delle entità hello. È possibile specificare questo valore per il programma di installazione di hello o i punti di ingresso principale o è possibile specificare `All` tooapply è tooboth. Hello seguente illustra i diversi criteri applicati:

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Se **EntryPointType** non viene specificato, impostazione predefinita di hello è tooEntryPointType = "Main". Specifica di **SetupEntryPoint** è particolarmente utile quando si desidera toorun determinate operazioni di installazione con privilegi elevati con un account di sistema. codice di servizio effettivo Hello può essere eseguito con un account con privilegi inferiori.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Applicare un pacchetti di codice predefiniti criteri tooall servizio
Utilizzare hello **DefaultRunAsPolicy** toospecify sezione un account utente predefinito per tutti i pacchetti di codice che non dispongono di uno specifico **RunAsPolicy** definito. Se la maggior parte dei pacchetti di codice hello specificati nel manifesto del servizio hello utilizzato da un'applicazione è necessario toorun in hello stesso utente, hello applicazione possono essere definite solo criteri con tale account utente RunAs predefiniti. Hello esempio seguente specifica che se un pacchetto di codice non dispone di un **RunAsPolicy** specificato, il pacchetto di codice hello deve essere in esecuzione hello **MyDefaultAccount** specificato nella sezione delle entità hello.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Uso di un utente o un gruppo di dominio di Active Directory
Per un'istanza di Service Fabric è stato installato in Windows Server tramite il programma di installazione di hello autonomo, è possibile eseguire il servizio di hello con le credenziali di hello per un account utente o gruppo di Active Directory. Si tratta di Active Directory locale nel dominio e non di Azure Active Directory (Azure AD). Usando un utente di dominio o un gruppo, possono quindi accedere altre risorse nel dominio hello (ad esempio, le condivisioni di file) che sono state concesse autorizzazioni.

Hello riportato di seguito un utente di Active Directory denominato *TestUser* con loro dominio password crittografata usando un certificato denominato *NomeCert*. È possibile utilizzare hello `Invoke-ServiceFabricEncryptText` testo secret crittografato hello toocreate del comando PowerShell. Vedere [Gestione dei segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).

È necessario distribuire la chiave privata hello del hello certificato toodecrypt hello password toohello computer utilizzando un metodo fuori banda (in Azure, si tratta di con Azure Resource Manager). Quindi quando Service Fabric distribuisce computer toohello pacchetto del servizio hello, è in grado di toodecrypt hello segreto e (insieme al nome utente hello) l'autenticazione con Active Directory toorun con tali credenziali.

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a>Usare un account del servizio gestito del gruppo.
Per un'istanza di Service Fabric è stato installato in Windows Server tramite il programma di installazione di hello autonomo, è possibile eseguire il servizio di hello come un gruppo di Account del servizio gestito (gMSA). Si noti che si tratta di Active Directory locale nel dominio e non di Azure Active Directory (Azure AD). Utilizzando un account non è disponibile la password o archiviata in hello `Application Manifest`.

Hello esempio seguente viene illustrato come toocreate un account gestito denominato *svc Test$*; come toodeploy grado di gestire i nodi del cluster toohello account del servizio; e come tooconfigure hello dell'entità utente.

##### <a name="prerequisites"></a>Prerequisiti.
- dominio Hello richiede una chiave radice del servizio distribuzione CHIAVI.
- dominio Hello deve toobe in un Windows Server 2012 o un livello di funzionalità in un secondo momento.

##### <a name="example"></a>Esempio
1. Dispone un amministratore di dominio active directory creare un account del servizio gestito di gruppo utilizzando hello `New-ADServiceAccount` cmdlet e assicurarsi che hello `PrincipalsAllowedToRetrieveManagedPassword` include tutti i nodi del cluster hello service fabric. Si noti che `AccountName`, `DnsHostName` e `ServicePrincipalName` devono essere univoci.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. In ognuno dei nodi del cluster di infrastruttura servizio hello (ad esempio, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), installare e testare hello gMSA.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Configurazione dell'entità utente hello e configurare hello RunAsPolicy tooreference hello utente.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Assegnare un criterio di accesso di sicurezza per gli endpoint HTTP e HTTPS
Se si applica a un servizio di tooa criteri RunAs e manifesto del servizio hello dichiara le risorse di endpoint con protocollo hello HTTP, è necessario specificare un **SecurityAccessPolicy** tooensure che porte allocato endpoint toothese siano correttamente controllo di accesso elencate per hello account utente RunAs cui viene eseguito il servizio di hello. In caso contrario, **http.sys** dispone di accesso toohello servizio e ottenere gli errori con chiamate da client hello. esempio Hello applica endpoint dell'account hello Customer1 tooan chiamato **EndpointName**, che fornisce i diritti di accesso completo.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Per l'endpoint HTTPS hello, è inoltre tooindicate nome di hello del client di toohello tooreturn certificato hello. È possibile farlo tramite **EndpointBindingPolicy**, con il certificato di hello definito in una sezione di certificati nel manifesto dell'applicazione hello.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Aggiornamento di più applicazioni con endpoint https
È necessario fare attenzione toobe non toouse hello **stessa porta** per istanze diverse di hello stessa applicazione quando si usa http**s**. motivo di Hello è che Service Fabric non sarà in grado di tooupgrade cert di hello per una delle istanze dell'applicazione hello. Ad esempio, se l'applicazione 1 o dell'applicazione 2 entrambi desidera tooupgrade loro toocert cert 1, 2. Quando si verifica l'aggiornamento di hello, Service Fabric potrebbero essere eliminate registrazione cert 1 hello con http.sys anche se hello altre applicazioni in uso. tooprevent, Service Fabric rileva che esiste già un'altra istanza dell'applicazione registrata sulla porta hello con certificato hello (scadenza toohttp.sys) e l'operazione di hello ha esito negativo.

Pertanto Service Fabric supporta l'aggiornamento di due servizi diversi utilizzando **hello stessa porta** in istanze diverse dell'applicazione. In altre parole, non è possibile utilizzare hello stesso certificato in servizi diversi in hello stessa porta. Se è necessario toohave condivisa certificato sul hello stessa porta, è necessario tooensure tale hello i servizi vengono inseriti in computer diversi con vincoli di posizionamento. In alternativa, utilizzare le porte dinamiche di Service Fabric se possibile per ogni servizio in ogni istanza dell'applicazione. 

Se viene visualizzato un errore di aggiornamento con https, un avviso di errore indicante che "hello API HTTP Server di Windows non supporta più certificati per le applicazioni che condividono una porta."

## <a name="a-complete-application-manifest-example"></a>Esempio completo del manifesto dell'applicazione
Hello manifesto dell'applicazione di seguito sono illustrati molti dei hello impostazioni diverse:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
* [Comprendere il modello di applicazione hello](service-fabric-application-model.md)
* [Specificare le risorse in un manifesto del servizio](service-fabric-service-manifest-resources.md)
* [Distribuire un'applicazione](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png

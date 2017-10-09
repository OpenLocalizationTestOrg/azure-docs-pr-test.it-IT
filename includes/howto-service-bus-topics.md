## <a name="what-are-service-bus-topics-and-subscriptions"></a>Cosa sono gli argomenti e le sottoscrizioni del bus di servizio?
Gli argomenti e le sottoscrizioni del bus di servizio supportano un modello di comunicazione con messaggistica di *pubblicazione-sottoscrizione* . Quando si usano gli argomenti e le sottoscrizioni, i componenti di un'applicazione distribuita non comunicano direttamente l'uno con l'altro, ma scambiano messaggi tramite un argomento, che agisce da intermediario.

![Concetti relativi agli argomenti](./media/howto-service-bus-topics/sb-topics-01.png)

Diversamente dalle code del bus di servizio, in cui ogni messaggio viene elaborato da un unico consumer, gli argomenti e le sottoscrizioni offrono una forma di comunicazione "uno a molti" tramite un modello di pubblicazione-sottoscrizione. È possibile registrare l'argomento di tooa più sottoscrizioni. Quando l'argomento tooa viene inviato un messaggio, viene quindi reso disponibile tooeach sottoscrizione toohandle o il processo in modo indipendente.

Un argomento tooa sottoscrizione simile a una coda virtuale che riceve copie dei messaggi hello inviati toohello argomento. Facoltativamente, è possibile registrare le regole di filtro per un argomento in una base per ogni sottoscrizione, che consentono di toofilter o limitare l'argomento tooa i messaggi vengono ricevuti dal quale le sottoscrizioni dell'argomento.

Le sottoscrizioni e gli argomenti del Bus di servizio consentono di tooscale ed elaborare un numero molto elevato di messaggi tra molti utenti e applicazioni.

## <a name="create-a-namespace"></a>Creare uno spazio dei nomi
toobegin utilizzando gli argomenti del Bus di servizio e le sottoscrizioni in Azure, è innanzitutto necessario creare un *spazio dei nomi servizio*. Uno spazio dei nomi fornisce un contenitore di ambito per fare riferimento alle risorse del bus di servizio all'interno dell'applicazione.

toocreate uno spazio dei nomi:

1. Accesso toohello [portale di Azure][Azure portal].
2. Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, quindi fare clic su **Enterprise Integration**, quindi fare clic su **Bus di servizio**.
3. In hello **Crea spazio dei nomi** finestra di dialogo immettere un nome di spazio dei nomi. sistema di Hello controlla immediatamente toosee se nome hello è disponibile.
4. Dopo il nome di spazio dei nomi che hello è disponibile, scegliere hello tariffario (Basic, Standard o Premium).
5. In hello **sottoscrizione** campo, scegliere una sottoscrizione di Azure in cui lo spazio dei nomi di toocreate hello.
6. In hello **gruppo di risorse** selezionare un gruppo di risorse esistente in cui hello dello spazio dei nomi in tempo reale oppure crearne uno nuovo.      
7. In **percorso**, scegliere hello paese in cui lo spazio dei nomi deve essere ospitato.
   
    ![Crea spazio dei nomi][create-namespace]
8. Fare clic su hello **crea** pulsante. sistema Hello ora crea uno spazio dei nomi e viene abilitato. Potrebbe essere toowait alcuni minuti per le risorse di hello sistema esegue il provisioning per l'account.

### <a name="obtain-hello-credentials"></a>Ottenere le credenziali di hello
1. Nell'elenco di hello degli spazi dei nomi, fare clic su hello appena creato il nome dello spazio dei nomi.
2. In hello **dello spazio dei nomi Service Bus** pannello, fare clic su **criteri di accesso condiviso**.
3. In hello **criteri di accesso condiviso** pannello, fare clic su **RootManageSharedAccessKey**.
   
    ![connection-info][connection-info]
4. In hello **criteri: RootManageSharedAccessKey** pannello, fare clic su pulsante Copia hello Avanti troppo**chiave – primario di stringa di connessione**, negli Appunti toocopy hello connessione stringa tooyour per un uso successivo.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png



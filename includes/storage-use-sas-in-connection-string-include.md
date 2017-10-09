Se si dispone di un URL di firma di accesso condiviso che consente di accedere tooresources in un account di archiviazione, è possibile utilizzare hello firma di accesso condiviso in una stringa di connessione. Poiché hello SAS contiene richiesta hello tooauthenticate necessarie informazioni di hello, una stringa di connessione con una firma di accesso condiviso fornisce protocollo hello, endpoint del servizio hello e hello credenziali necessarie tooaccess hello risorse.

toocreate una stringa di connessione che include una firma di accesso condiviso, specificare la stringa hello in hello seguente formato:

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

Ogni endpoint del servizio è facoltativo, anche se la stringa di connessione hello deve contenere almeno uno.

> [!NOTE]
> La procedura consigliata prevede l'uso di HTTPS con la firma di accesso condiviso.
>
> Se si specifica una firma di accesso condiviso in una stringa di connessione in un file di configurazione, potrebbe essere tooencode caratteri speciali nell'URL hello.
>
>

### <a name="service-sas-example"></a>Esempio di firma di accesso condiviso del servizio
Ecco un esempio di stringa di connessione che include una firma di accesso condiviso del servizio per l'archiviazione BLOB:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

Di seguito è riportato un esempio di hello stessa stringa di connessione con la codifica dei caratteri speciali:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>Esempio di firma di accesso condiviso dell'account
Ecco un esempio di stringa di connessione che include una firma di accesso condiviso dell'account per l'archivio BLOB e file. Si noti che sono specificati gli endpoint per entrambi i servizi:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

Di seguito è riportato un esempio di hello stessa stringa di connessione con la codifica URL:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```


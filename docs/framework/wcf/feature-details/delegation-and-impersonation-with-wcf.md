---
title: "Delegierung und Identit&#228;tswechsel mit WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Identitätswechsel [WCF]"
  - "Delegierung [WCF]"
ms.assetid: 110e60f7-5b03-4b69-b667-31721b8e3152
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Delegierung und Identit&#228;tswechsel mit WCF
Der *Identitätswechsel* ist ein gängiges Verfahren, das Dienste verwenden, um den Clientzugriff auf die Ressourcen einer Dienstdomäne zu beschränken. Dienstdomänenressourcen können entweder Computerressourcen, wie lokale Dateien \(Identitätswechsel\), oder eine Ressource auf einem anderen Computer, z. B. eine Dateifreigabe \(Delegierung\), sein. Eine Beispielanwendung finden Sie unter [Durchführen eines Identitätswechsels für den Client](../../../../docs/framework/wcf/samples/impersonating-the-client.md). Ein Beispiel zur Verwendung von Identitätswechsel finden Sie unter [Vorgehensweise: Annahme der Clientidentität durch einen Dienst](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md).  
  
> [!IMPORTANT]
>  Beim Identitätswechsel eines Clients in einem Dienst wird der Dienst mit den Anmeldeinformationen des Clients ausgeführt, die höhere Rechte besitzen können als der Serverprozess.  
  
## Übersicht  
 In der Regel ruft ein Client einen Dienst auf, damit dieser eine Aktion für ihn ausführt. Der Identitätswechsel ermöglicht es dem Dienst, während der Ausführung der Aktion als Client zu fungieren. Die Delegierung ermöglicht es einem Front\-End\-Dienst, die Clientanforderung so an einen Back\-End\-Dienst weiterzuleiten, dass auch der Back\-End\-Dienst die Identität des Clients annehmen kann. Der Identitätswechsel wird meist als Möglichkeit verwendet, mit der überprüft werden kann, ob ein Client zur Durchführung einer bestimmten Aktion berechtigt ist. Die Delegierung stellt dagegen eine Möglichkeit dar, die Fähigkeit zum Identitätswechsel und die Clientidentität an einen Back\-End\-Dienst zu übertragen. Die Delegierung ist eine Windows\-Domänenfunktion, die verwendet werden kann, wenn eine auf Kerberos basierende Authentifizierung durchgeführt wird. Delegierung und Identitätsübergabe sind zwei verschiedene Dinge. Weil bei der Delegierung die Fähigkeit zur Annahme der Identität des Clients übertragen wird, ohne das Kennwort des Clients zu besitzen, handelt es sich um einen Vorgang mit höheren Sicherheitsberechtigungen als die Identitätsübergabe.  
  
 Sowohl Identitätswechsel als auch Delegierung erfordern, dass der Client eine Windows\-Identität besitzt. Wenn der Client keine Windows\-Identität besitzt, dann besteht nur die Möglichkeit, die Identität des Clients dem zweiten Dienst zu übertragen.  
  
## Grundlagen des Identitätswechsels  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] unterstützt den Identitätswechsel für eine Vielzahl von Clientanmeldeinformationen. In diesem Thema wird die Dienstmodellunterstützung für den Identitätswechsel des Aufrufers während der Implementierung einer Dienstmethode beschrieben. Außerdem werden allgemeine Bereitstellungsszenarien erörtert, die Identitätswechsel und SOAP\-Sicherheit und [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Optionen in diesen Szenarien beinhalten.  
  
 Der Schwerpunkt dieses Themas liegt auf dem Identitätswechsel und der Delegierung in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] bei Verwendung der SOAP\-Sicherheit. Sie können den Identitätswechsel und die Delegierung auch mit [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verwenden, wenn Sie die Transportsicherheit nutzen, wie unter [Identitätswechsel und Transportsicherheit](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md) beschrieben.  
  
## Zwei Methoden  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-SOAP\-Sicherheit verfügt über zwei verschiedene Methode zum Durchführen von Identitätswechsel. Die verwendete Methode hängt von der Bindung ab. Die eine Methode besteht im Identitätswechsel von einem Windows\-Token aus, das von SSPI \(Security Support Provider Interface\) oder der Kerberos\-Authentifizierung stammt, die dann im Cache des Diensts gespeichert wird. Die zweite Methode besteht im Identitätswechsel von einem Windows\-Token aus, das von Kerberos\-Erweiterungen stammt, insgesamt als *Service\-for\-User* \(S4U\) bezeichnet.  
  
### Identitätswechsel mit im Cache gespeichertem Token  
 Sie können einen Identitätswechsel mit einem im Cache gespeicherten Token folgendermaßen ausführen:  
  
-   Mit <xref:System.ServiceModel.WSHttpBinding>, <xref:System.ServiceModel.WSDualHttpBinding> und <xref:System.ServiceModel.NetTcpBinding> mit Windows\-Clientanmeldeinformationen.  
  
-   Mit <xref:System.ServiceModel.BasicHttpBinding>, mit einem <xref:System.ServiceModel.BasicHttpSecurityMode>, der auf die <xref:System.ServiceModel.BasicHttpSecurityMode>\-Anmeldeinformationen eingestellt ist, oder einer anderen Standardbindung, bei der der Client Benutzernamen\-Anmeldeinformationen präsentiert, die der Dienst einem gültigen Windows\-Konto zuordnen kann.  
  
-   Mit jeder <xref:System.ServiceModel.Channels.CustomBinding>, die Windows\-Clientanmeldeinformationen verwendet, bei denen `requireCancellation` auf `true` eingestellt ist. \(Die Eigenschaft ist für folgende Klassen verfügbar: <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters>, <xref:System.ServiceModel.Security.Tokens.SslSecurityTokenParameters> und <xref:System.ServiceModel.Security.Tokens.SspiSecurityTokenParameters>.\) Bei Verwendung einer sicheren Konversation auf der Bindung muss die `requireCancellation`\-Eigenschaft auch auf `true` eingestellt sein.  
  
-   Mit jeder <xref:System.ServiceModel.Channels.CustomBinding>, bei der der Client Benutzernamen\-Anmeldeinformationen präsentiert. Bei Verwendung einer sicheren Konversation auf der Bindung muss die `requireCancellation`\-Eigenschaft auch auf `true` eingestellt sein.  
  
### Auf S4U basierender Identitätswechsel  
 Sie können einen auf S4U basierenden Identitätswechsel folgendermaßen ausführen:  
  
-   Mit <xref:System.ServiceModel.WSHttpBinding>, <xref:System.ServiceModel.WSDualHttpBinding> und <xref:System.ServiceModel.NetTcpBinding> mit Zertifikatclient\-Anmeldeinformationen, die der Dienst einem gültigen Windows\-Konto zuordnen kann.  
  
-   Mit jeder <xref:System.ServiceModel.Channels.CustomBinding>, die Windows\-Clientanmeldeinformationen verwendet, bei denen die `requireCancellation`\-Eigenschaft auf `false` eingestellt ist.  
  
-   Mit jeder <xref:System.ServiceModel.Channels.CustomBinding>, die einen Benutzernamen oder Windows\-Clientanmeldeinformationen und eine sichere Konversation verwendet, wobei die `requireCancellation`\-Eigenschaft auf `false` eingestellt ist.  
  
 Inwieweit der Dienst die Identität des Clients annehmen kann, hängt von den Rechten ab, die das Dienstkonto beim Versuch des Identitätswechsels besitzt, vom verwendeten Typ des Identitätswechsels und möglicherweise vom Ausmaß des Identitätswechsels, den der Client zulässt.  
  
> [!NOTE]
>  Wenn Client und Dienst auf demselben Computer ausgeführt werden und der Client unter einem Systemkonto \(z. B. unter `Local System` oder `Network Service`\) ausgeführt wird, kann kein Clientidentitätswechsel vorgenommen werden, wenn mit Token für den Sicherheitszustandskontext eine Sicherheitsverbindung hergestellt wird. Eine Windows Forms\- oder Konsolenanwendung wird in der Regel unter dem derzeit angemeldeten Konto ausgeführt, sodass für dieses Konto standardmäßig ein Identitätswechsel durchgeführt werden kann. Wenn es sich bei dem Client jedoch um eine [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]\-Seite handelt, die auf [!INCLUDE[iis601](../../../../includes/iis601-md.md)] oder [!INCLUDE[iisver](../../../../includes/iisver-md.md)] gehostet wird, wird der Client standardmäßig unter dem `Network Service`\-Konto ausgeführt. Alle vom System bereitgestellten Bindungen, die Sicherheitssitzungen unterstützen, verwenden standardmäßig ein zustandsloses Token für den Sicherheitskontext. Wenn es sich bei dem Client jedoch um eine [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]\-Seite handelt und sichere Sitzungen mit zustandsbehafteten SCTs verwendet werden, kann kein Clientidentitätswechsel durchgeführt werden.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] zur Verwendung von zustandsbehafteten SCTs in sicheren Sitzungen finden Sie unter [Vorgehensweise: Erstellen eines Tokens für den Sicherheitskontext einer sicheren Sitzung](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
## Identitätswechsel in einer Dienstmethode: Deklaratives Modell  
 Die meisten Identitätswechselszenarien umfassen das Ausführen der Dienstmethode im Aufruferkontext.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] bietet eine Identitätswechselfunktion, die dies erleichtert, indem der Benutzer die Anforderung für den Identitätswechsel im <xref:System.ServiceModel.OperationBehaviorAttribute>\-Attribut festlegen kann. Im folgenden Codebeispiel nimmt die [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Infrastruktur die Identität des Aufrufers an, bevor die `Hello`\-Methode ausgeführt wird. Jeder Versuch, auf die systemeigenen Ressourcen innerhalb der `Hello`\-Methode zuzugreifen, ist nur erfolgreich, wenn die Zugriffsteuerungsliste der Ressource dem Aufrufer Zugriffsrechte erlaubt. Zum Aktivieren des Identitätswechsels legen Sie die <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A>\-Eigenschaft auf einen der <xref:System.ServiceModel.ImpersonationOption>\-Enumerationswerte fest, entweder auf <xref:System.ServiceModel.ImpersonationOption?displayProperty=fullName> oder auf <xref:System.ServiceModel.ImpersonationOption?displayProperty=fullName>, wie im folgenden Beispiel dargestellt.  
  
> [!NOTE]
>  Wenn ein Dienst höhere Anmeldeinformationen besitzt als der Remoteclient, werden die Anmeldeinformationen des Diensts verwendet, wenn die <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A>\-Eigenschaft auf <xref:System.ServiceModel.ImpersonationOption> eingestellt ist. Wenn also ein Benutzer mit niedrigen Rechten seine Anmeldeinformationen angibt, führt ein Dienst mit höheren Rechten die Methode mit den Anmeldeinformationen des Diensts aus und kann Ressourcen verwenden, die der Benutzer mit den niedrigen Rechten sonst keinesfalls verwenden könnte.  
  
 [!code-csharp[c_ImpersonationAndDelegation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#1)]
 [!code-vb[c_ImpersonationAndDelegation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#1)]  
  
 Die [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Infrastruktur kann die Identität des Aufrufers nur annehmen, wenn der Aufrufer mit Anmeldeinformationen authentifiziert wird, die einem Windows\-Benutzerkonto zugeordnet werden können. Wenn der Dienst für die Authentifizierung mit Anmeldeinformationen konfiguriert ist, die keinem Windows\-Konto zugeordnet werden können, wird die Dienstmethode nicht ausgeführt.  
  
> [!NOTE]
>  Unter [!INCLUDE[wxp](../../../../includes/wxp-md.md)] schlägt der Identitätswechsel beim Erstellen eines zustandsbehafteten SCT fehl, was zu einer <xref:System.InvalidOperationException> führt.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Nicht unterstützte Szenarien](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md).  
  
## Identitätswechsel in einer Dienstmethode: Imperatives Modell  
 Mitunter benötigt ein Aufrufer nicht die gesamte Dienstmethode für den Identitätswechsel, sondern nur einen Teil der Methode. In diesem Fall rufen Sie die Windows\-Identität des Aufrufers innerhalb der Dienstmethode ab, und führen Sie den Identitätswechsel imperativ durch. Verwenden Sie dazu die <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A>\-Eigenschaft des <xref:System.ServiceModel.ServiceSecurityContext>, um eine Instanz der <xref:System.Security.Principal.WindowsIdentity>\-Klasse zurückzugeben und die <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A>\-Methode vor dem Verwenden der Instanz aufzurufen.  
  
> [!NOTE]
>  Stellen Sie sicher, dass Sie die [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]`Using`\-Anweisung oder die C\# `using`\-Anweisung verwenden, um den Identitätswechsel automatisch rückgängig zu machen. Wenn Sie die Anweisung nicht verwenden oder wenn Sie eine andere Programmiersprache als [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] oder C\# verwenden, müssen Sie die Identitätswechselebene zurücksetzen. Wird dies versäumt, kann dies die Grundlage für Denial\-of\-Service\-Angriffe und Rechteerweiterungsangriffe bilden.  
  
 [!code-csharp[c_ImpersonationAndDelegation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#2)]
 [!code-vb[c_ImpersonationAndDelegation#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#2)]  
  
## Identitätswechsel für alle Dienstmethoden  
 In einigen Fällen müssen Sie alle Methoden eines Diensts im Kontext eines Aufrufers ausführen. Statt diese Funktion explizit für jede Methode einzeln zu aktivieren, verwenden Sie das <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>. Wie im folgenden Code dargestellt, legen Sie die <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ImpersonateCallerForAllOperations%2A>\-Eigenschaft auf `true` fest. Das <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> wird aus den Verhaltenssammlungen der <xref:System.ServiceModel.ServiceHost>\-Klasse abgerufen. Beachten Sie außerdem, dass die `Impersonation`\-Eigenschaft des auf jede Methode angewendeten <xref:System.ServiceModel.OperationBehaviorAttribute> ebenfalls entweder auf <xref:System.ServiceModel.ImpersonationOption> oder <xref:System.ServiceModel.ImpersonationOption> eingestellt sein muss.  
  
 [!code-csharp[c_ImpersonationAndDelegation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#3)]
 [!code-vb[c_ImpersonationAndDelegation#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#3)]  
  
 In der folgenden Tabelle wird das [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-Verhalten für alle möglichen Kombinationen aus `ImpersonationOption` und `ImpersonateCallerForAllServiceOperations` beschrieben.  
  
|`ImpersonationOption`|`ImpersonateCallerForAllServiceOperations`|Verhalten|  
|---------------------------|------------------------------------------------|---------------|  
|Erforderlich|nicht verfügbar|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nimmt die Identität des Aufrufers an|  
|Allowed|false|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nimmt die Identität des Aufrufers nicht an|  
|Allowed|true|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nimmt die Identität des Aufrufers an|  
|NotAllowed|false|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nimmt die Identität des Aufrufers nicht an|  
|NotAllowed|true|Disallowed. \(Eine <xref:System.InvalidOperationException> wird ausgelöst.\)|  
  
## Identitätswechselebene aus Windows\-Anmeldeinformationen und Identitätswechsel mit im Cache gespeichertem Token  
 In einigen Szenarien besitzt der Client eine Teilkontrolle über die Ebene des Identitätswechsels, den der Dienst bei Verwendung von Windows\-Clientanmeldeinformationen ausführt. Ein Szenario tritt auf, wenn der Client die Identitätswechselebene "Anonymous" angibt. Das andere Szenario liegt vor, wenn Sie einen Identitätswechsel mit einem im Cache gespeicherten Token ausführen. Legen Sie hierfür die <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A>\-Eigenschaft der <xref:System.ServiceModel.Security.WindowsClientCredential>\-Klasse fest, auf die als Eigenschaft der generischen <xref:System.ServiceModel.ChannelFactory%601>\-Klasse zugegriffen wird.  
  
> [!NOTE]
>  Durch Angeben der Identitätswechselebene "Anonymous" meldet sich der Client anonym beim Dienst an. Der Dienst muss daher anonyme Anmeldungen zulassen, unabhängig davon, ob ein Identitätswechsel durchgeführt wird.  
  
 Der Client kann die Identitätswechselebene als <xref:System.Security.Principal.TokenImpersonationLevel>, <xref:System.Security.Principal.TokenImpersonationLevel>, <xref:System.Security.Principal.TokenImpersonationLevel> oder <xref:System.Security.Principal.TokenImpersonationLevel> angeben. Es wird nur ein Token auf der angegebenen Ebene erstellt, wie im folgenden Code veranschaulicht.  
  
 [!code-csharp[c_ImpersonationAndDelegation#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#4)]
 [!code-vb[c_ImpersonationAndDelegation#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#4)]  
  
 In der folgenden Tabelle wird die Identitätswechselebene angegeben, die der Dienst bei einem Identitätswechsel mit einem im Cache gespeicherten Token erhält.  
  
|`AllowedImpersonationLevel`\-Wert|Der Dienst hat das `SeImpersonatePrivilege`|Dienst und Client sind delegierungsfähig.|`ImpersonationLevel` mit im Cache gespeichertem Token|  
|---------------------------------------|-------------------------------------------------|-----------------------------------------------|-----------------------------------------------------------|  
|Anonym|Ja|nicht verfügbar|Identitätswechsel|  
|Anonym|Nein|nicht verfügbar|Identifikation|  
|Identifikation|nicht verfügbar|nicht verfügbar|Identifikation|  
|Identitätswechsel|Ja|nicht verfügbar|Identitätswechsel|  
|Identitätswechsel|Nein|nicht verfügbar|Identifikation|  
|Delegierung|Ja|Ja|Delegierung|  
|Delegierung|Ja|Nein|Identitätswechsel|  
|Delegierung|Nein|nicht verfügbar|Identifikation|  
  
## Identitätswechselebene aus Benutzernamen\-Anmeldeinformationen und Identitätswechsel mit im Cache gespeichertem Token  
 Durch Weitergabe des Benutzernamens und Kennworts an den Dienst ermöglicht ein Client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], sich als dieser Benutzer anzumelden. Dies entspricht einem Festlegen der `AllowedImpersonationLevel`\-Eigenschaft auf <xref:System.Security.Principal.TokenImpersonationLevel>. \(Die `AllowedImpersonationLevel` ist in der <xref:System.ServiceModel.Security.WindowsClientCredential>\-Klasse und in der <xref:System.ServiceModel.Security.HttpDigestClientCredential>\-Klasse verfügbar.\) In der folgenden Tabelle wird die Identitätswechselebene angegeben, die erhalten wird, wenn der Dienst Benutzernamen\-Anmeldeinformationen empfängt.  
  
|`AllowedImpersonationLevel`|Der Dienst hat das `SeImpersonatePrivilege`|Dienst und Client sind delegierungsfähig.|`ImpersonationLevel` mit im Cache gespeichertem Token|  
|---------------------------------|-------------------------------------------------|-----------------------------------------------|-----------------------------------------------------------|  
|nicht verfügbar|Ja|Ja|Delegierung|  
|nicht verfügbar|Ja|Nein|Identitätswechsel|  
|nicht verfügbar|Nein|nicht verfügbar|Identifikation|  
  
## Identitätswechselebene aus einem auf S4U basierenden Identitätswechsel  
  
|Der Dienst hat das `SeTcbPrivilege`|Der Dienst hat das `SeImpersonatePrivilege`|Dienst und Client sind delegierungsfähig.|`ImpersonationLevel` mit im Cache gespeichertem Token|  
|-----------------------------------------|-------------------------------------------------|-----------------------------------------------|-----------------------------------------------------------|  
|Ja|Ja|nicht verfügbar|Identitätswechsel|  
|Ja|Nein|nicht verfügbar|Identifikation|  
|Nein|nicht verfügbar|nicht verfügbar|Identifikation|  
  
## Zuordnen eines Clientzertifikats zu einem Windows\-Konto  
 Ein Client kann sich gegenüber einem Dienst mithilfe eines Zertifikats ausweisen; der Dienst kann angewiesen werden, den Client mittels Active Directory einem vorhandenen Konto zuzuordnen. Im folgenden XML wird gezeigt, wie der Dienst so konfiguriert wird, dass er das Zertifikat zuordnet:  
  
```xml  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="MapToWindowsAccount">  
      <serviceCredentials>  
        <clientCertificate>  
          <authentication mapClientCertificateToWindowsAccount="true" />  
        </clientCertificate>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
 Im folgenden Code wird gezeigt, wie der Dienst konfiguriert wird:  
  
```  
  
// Create a binding that sets a certificate as the client credential type.  
WSHttpBinding b = new WSHttpBinding();  
b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
// Create a service host that maps the certificate to a Windows account.  
Uri httpUri = new Uri("http://localhost/Calculator");  
ServiceHost sh = new ServiceHost(typeof(HelloService), httpUri);  
sh.Credentials.ClientCertificate.Authentication.MapClientCertificateToWindowsAccount = true;  
  
```  
  
## Delegierung  
 Damit ein Dienst an einen Back\-End\-Dienst delegiert werden kann, muss er sich gegenüber dem Back\-End\-Dienst mittels bilateraler \(SSPI ohne Rückgriff auf NTLM\) oder direkter Kerberos\-Authentifizierung unter Verwendung der Windows\-Identität des Clients authentifizieren. Um einen Dienst an einen Back\-End\-Dienst zu delegieren, erstellen Sie eine <xref:System.ServiceModel.ChannelFactory%601> und einen Kanal und leiten die Kommunikation über diesen Kanal, solange die Identität des Clients angenommen wird. Bei dieser Form der Delegierung hängt die maximale Entfernung zwischen Back\-End\-Dienst und Front\-End\-Dienst von der Identitätswechselebene des Front\-End\-Diensts ab. Wenn die Identitätswechselebene <xref:System.Security.Principal.TokenImpersonationLevel> festgelegt wird, müssen Front\-End\- und Back\-End\-Dienst auf dem gleichen Computer ausgeführt werden. Wenn die Identitätswechselebene <xref:System.Security.Principal.TokenImpersonationLevel> verwendet wird, können Front\-End\- und Back\-End\-Dienst auf unterschiedlichen Computern oder dem gleichen Computer ausgeführt werden. Ein Identitätswechsel auf Delegierungsebene erfordert, dass die Windows\-Domänenrichtlinie entsprechend konfiguriert wurde, um eine Delegierung zuzulassen. Weitere Informationen zum Konfigurieren von Active Directory für die Delegierung finden Sie unter [Enabling Delegated Authentication](http://go.microsoft.com/fwlink/?LinkId=99690).  
  
> [!NOTE]
>  Wenn sich der Client dem Front\-End\-Dienst gegenüber mit einem Benutzernamen und einem Kennwort authentifiziert, die einem Windows\-Konto für den Back\-End\-Dienst entsprechen, dann kann sich der Front\-End\-Dienst durch erneute Angabe des Benutzernamens und des Kennworts des Clients dem Back\-End\-Dienst gegenüber authentifizieren. Dies ist eine besonders mächtige Form der Identitätsübergabe, weil die Weitergabe von Benutzernamen und Kennwort an den Back\-End\-Dienst diesen in die Lage versetzt, einen Identitätswechsel durchzuführen. Weil Kerberos nicht verwendet wird, stellt dieser Vorgang jedoch keine Delegierung dar. Die Delegierung betreffende Active Directory\-Steuerelemente gelten nicht für die Authentifizierung durch Benutzername und Kennwort.  
  
### Delegierungsfähigkeit als Funktion der Identitätswechselebene  
  
|Ebene des Identitätswechsels|Dienst kann eine prozessübergreifende Delegierung ausführen|Dienst kann eine computerübergreifende Delegierung ausführen|  
|----------------------------------|-----------------------------------------------------------------|------------------------------------------------------------------|  
|<xref:System.Security.Principal.TokenImpersonationLevel>|Nein|Nein|  
|<xref:System.Security.Principal.TokenImpersonationLevel>|Ja|Nein|  
|<xref:System.Security.Principal.TokenImpersonationLevel>|Ja|Ja|  
  
 Im folgenden Codebeispiel wird die Verwendung der Delegierung veranschaulicht.  
  
 [!code-csharp[c_delegation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_delegation/cs/source.cs#1)]
 [!code-vb[c_delegation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_delegation/vb/source.vb#1)]  
  
### Konfigurieren einer Anwendung für die Verwendung der eingeschränkten Delegierung  
 Die eingeschränkte Delegierung kann erst verwendet werden, nachdem Absender, Empfänger und Domänencontroller entsprechend konfiguriert wurden. Die folgende Prozedur listet die Schritte auf, die eine eingeschränkte Delegierung ermöglichen. Nähere Angaben zu den Unterschieden zwischen Delegierung und eingeschränkter Delegierung finden Sie in dem Abschnitt unter [Windows Server 2003 Kerberos Extensions](http://go.microsoft.com/fwlink/?LinkId=100194), der sich mit eingeschränkter Delegierung befasst \(Seite möglicherweise auf Englisch\).  
  
1.  Deaktivieren Sie auf dem Domänencontroller das Kontrollkästchen **Konto ist vertraulich und kann nicht delegiert werden** für das Konto, unter dem die Clientanwendung ausgeführt wird.  
  
2.  Aktivieren Sie auf dem Domänencontroller das Kontrollkästchen **Konto wird für Delegierungszwecke vertraut** für das Konto, unter dem die Clientanwendung ausgeführt wird.  
  
3.  Konfigurieren Sie auf dem Domänencontroller den Computer der mittleren Schicht, sodass diesem für Delegierungszwecke vertraut wird, indem Sie auf die Option **Computer für Delegierungszwecke vertrauen** klicken.  
  
4.  Konfigurieren Sie auf dem Domänencontroller den Computer der mittleren Schicht für die Verwendung der eingeschränkten Delegierung, indem Sie auf die Option **Computer nur für Delegierungszwecke angegebener Dienste vertrauen** klicken.  
  
 Ausführlichere Anweisungen zum Konfigurieren der eingeschränkten Delegierung finden Sie in den folgenden MSDN\-Themen:  
  
-   [Problembehandlung der Kerberos\-Delegierung \(Seite möglicherweise auf Englisch\)](http://go.microsoft.com/fwlink/?LinkId=36724)  
  
-   [Kerberos\-Protokollübergang und eingeschränkte Delegierung](http://go.microsoft.com/fwlink/?LinkId=36725)  
  
## Siehe auch  
 <xref:System.ServiceModel.OperationBehaviorAttribute>   
 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A>   
 <xref:System.ServiceModel.ImpersonationOption>   
 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A>   
 <xref:System.ServiceModel.ServiceSecurityContext>   
 <xref:System.Security.Principal.WindowsIdentity>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ImpersonateCallerForAllOperations%2A>   
 <xref:System.ServiceModel.ServiceHost>   
 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A>   
 <xref:System.ServiceModel.Security.WindowsClientCredential>   
 <xref:System.ServiceModel.ChannelFactory%601>   
 <xref:System.Security.Principal.TokenImpersonationLevel>   
 [Identitätswechsel und Transportsicherheit](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md)   
 [Durchführen eines Identitätswechsels für den Client](../../../../docs/framework/wcf/samples/impersonating-the-client.md)   
 [Vorgehensweise: Annahme der Clientidentität durch einen Dienst](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)   
 [ServiceModel Metadata Utility\-Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
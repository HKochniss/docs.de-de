---
title: 'Vorgehensweise: Verwenden eines benutzerdefinierten Benutzernamens und eines Kennwort-Validierungssteuerelements'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, username and password
ms.assetid: 8e08b74b-fa44-4018-b63d-0d0805f85e3f
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: ee138c52c8cdd63137bf3c468ebbdd064d60d443
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-use-a-custom-user-name-and-password-validator"></a>Vorgehensweise: Verwenden eines benutzerdefinierten Benutzernamens und eines Kennwort-Validierungssteuerelements
Wenn ein Benutzername und ein Kennwort für die Authentifizierung verwendet werden, verwendet [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] standardmäßig Windows zum Überprüfen des Benutzernamens und des Kennworts. Allerdings [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ermöglicht benutzerdefinierten Benutzernamen- und Kennwort-Authentifizierungsschemas, auch bekannt als *Validierungssteuerelemente*. Zum Verwenden eines benutzerdefinierten Benutzernamen- und Kennwort-Validierungssteuerelements erstellen und konfigurieren Sie eine Klasse, die sich von <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> ableitet.  
  
 Eine beispielanwendung finden Sie unter [Benutzer und Kennwort-Validierungssteuerelement](../../../../docs/framework/wcf/samples/user-name-password-validator.md).  
  
### <a name="to-create-a-custom-user-name-and-password-validator"></a>So erstellen Sie ein benutzerdefiniertes Benutzernamen- und Kennwort-Validierungssteuerelement  
  
1.  Erstellen Sie eine von der <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>-Klasse abgeleitete Klasse.  
  
     [!code-csharp[C_CustomUsernameAndPasswordValidator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#3)]
     [!code-vb[C_CustomUsernameAndPasswordValidator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#3)]  
  
2.  Implementieren Sie ein benutzerdefiniertes Authentifizierungsschema, indem Sie die <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>-Methode außer Kraft setzen.  
  
     Verwenden Sie nicht den Code des folgenden Beispiels, der die <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>-Methode in einer Produktionsumgebung außer Kraft setzt. Ersetzen Sie den Code mit dem benutzerdefinierten Benutzernamen- und Kennwort-Validierungsschema. Möglicherweise müssen der Benutzername und das zugehörige Kennwort aus einer Datenbank abgerufen werden.  
  
     Um dem Client Authentifizierungsfehler zurückzugeben, lösen Sie in der <xref:System.ServiceModel.FaultException>-Methode eine <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> aus.  
  
     [!code-csharp[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#4)]
     [!code-vb[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#4)]  
  
### <a name="to-configure-a-service-to-use-a-custom-user-name-and-password-validator"></a>So konfigurieren Sie einen Dienst für das Verwenden eines benutzerdefinierten Benutzernamen- und Kennwort-Validierungssteuerelements  
  
1.  Konfigurieren Sie eine Bindung, die Nachrichtensicherheit über jedes beliebige Transportprotokoll oder Sicherheit auf Transportebene über HTTP(S) verwendet.  
  
     Bei Verwendung von nachrichtensicherheit fügen Sie eine der vom System bereitgestellte Bindungen, wie z. B. eine [ \<WsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md), oder ein [ \<CustomBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) die Sicherheit unterstützt für Nachrichten und die `UserName` Anmeldeinformationstyp.  
  
     Wenn Sie Sicherheit auf Transportebene über HTTP(s) verwenden, fügen Sie entweder die [ \<WsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) oder [ \<BasicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), [ \< NetTcpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md) oder ein [ \<CustomBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) , HTTP (S) verwendet und die `Basic` -Authentifizierungsschema.  
  
    > [!NOTE]
    >  Wenn Sie [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] oder höher verwenden, können Sie ein benutzerdefiniertes Benutzernamen- und Kennwort-Validierungssteuerelement mit Nachrichten- und Transportsicherheit nutzen. In Verbindung mit [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] kann ein benutzerdefiniertes Benutzername- und Kennwort-Validierungssteuerelement nur mit Nachrichtensicherheit verwendet werden.  
  
    > [!TIP]
    >  Weitere Informationen zur Verwendung von \<NetTcpBinding > in diesem Kontext finden Sie unter [ \<Sicherheit >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)  
  
    1.  In der Konfigurationsdatei unter der [ \<system.serviceModel >](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) Element, Hinzufügen einer [ \<Bindungen >](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) Element.  
  
    2.  Hinzufügen einer [ \<WsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) oder [ \<BasicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) Element im Abschnitt über Bindungen. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Erstellen einer [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] binding-Element, finden Sie unter [wie: Angeben einer Dienstbindung in einer Konfiguration](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
    3.  Legen Sie die `mode` Attribut des der [ \<Sicherheit >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md) oder [ \<Sicherheit >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md) auf `Message`, `Transport`, `or``TransportWithMessageCredential`.  
  
    4.  Legen Sie die `clientCredentialType` Attribut von der [ \<Nachricht >](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) oder [ \<Transport >](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md).  
  
         Legen Sie bei Verwendung von nachrichtensicherheit die `clientCredentialType` Attribut des der [ \<Nachricht >](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) auf `UserName`.  
  
         Wenn Sicherheit auf Transportebene über HTTP(s) verwenden, legen Sie die `clientCredentialType` Attribut des der [ \<Transport >](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md) oder [ \<Transport >](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-basichttpbinding.md) auf `Basic`.  
  
        > [!NOTE]
        >  Wenn ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Dienst in Internet Information Services (IIS) unter Verwendung von Sicherheit auf Transportebene gehostet wird und die <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.UserNamePasswordValidationMode%2A>-Eigenschaft auf <xref:System.ServiceModel.Security.UserNamePasswordValidationMode.Custom> festgelegt ist, dann verwendet das benutzerdefinierte Authentifizierungsschema eine Teilmenge der Windows-Authentifizierung. Das liegt daran, dass IIS in diesem Szenario die Windows-Authentifizierung ausführt, bevor [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] den benutzerdefinierten Authentifizierer aufruft  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Erstellen einer [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] binding-Element, finden Sie unter [wie: Angeben einer Dienstbindung in einer Konfiguration](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
     Das folgende Beispiel zeigt den Konfigurationscode für die Bindung.  
  
    ```xml  
    <system.serviceModel>   
      <bindings>  
      <wsHttpBinding>  
          <binding name="Binding1">  
            <security mode="Message">  
              <message clientCredentialType="UserName" />  
            </security>  
          </binding>          
        </wsHttpBinding>  
      </bindings>  
    </system.serviceModel>  
    ```  
  
2.  Konfigurieren Sie ein Verhalten, das angibt, dass ein benutzerdefiniertes Benutzername- und Kennwort-Validierungssteuerelement verwendet wird, um Benutzernamen/Kennwort-Paare für eingehende <xref:System.IdentityModel.Tokens.UserNameSecurityToken>-Sicherheitstoken zu überprüfen.  
  
    1.  Als untergeordnetes Element der [ \<system.serviceModel >](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) Element, Hinzufügen einer [ \<Verhalten >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) Element.  
  
    2.  Hinzufügen einer [ \<ServiceBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) auf die [ \<Verhalten >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) Element.  
  
    3.  Hinzufügen einer [ \<Verhalten >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) Element, und legen die `name` -Attribut auf einen geeigneten Wert.  
  
    4.  Hinzufügen einer [ \<ServiceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) auf die [ \<Verhalten >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) Element.  
  
    5.  Hinzufügen einer [ \<UserNameAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md) auf die [ \<ServiceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md).  
  
    6.  Legen Sie `userNamePasswordValidationMode` auf `Custom` fest  
  
        > [!IMPORTANT]
        >  Wenn der `userNamePasswordValidationMode`-Wert nicht festgelegt wird, verwendet [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] die Windows-Authentifizierung anstatt des benutzerdefinierten Benutzernamen- und Kennwort-Validierungssteuerelements.  
  
    7.  Legen Sie den `customUserNamePasswordValidatorType` auf den Typ fest, der das benutzerdefinierte Benutzernamen- und Kennwort-Validierungssteuerelement darstellt.  
  
     Im folgenden Beispiel sehen Sie das `<serviceCredentials>`-Fragment bis zu diesem Punkt:  
  
    ```xml  
    <serviceCredentials>  
      <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.CalculatorService.CustomUserNameValidator, service" />  
    </serviceCredentials>  
    ```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird veranschaulicht, wie ein benutzerdefiniertes Benutzernamen- und Kennwort-Validierungssteuerelement erstellt wird. Verwenden Sie nicht den Code, der die <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>-Methode in einer Produktionsumgebung außer Kraft setzt. Ersetzen Sie den Code mit dem benutzerdefinierten Benutzernamen- und Kennwort-Validierungsschema. Möglicherweise müssen der Benutzername und das zugehörige Kennwort aus einer Datenbank abgerufen werden.  
  
 [!code-csharp[C_CustomUsernameAndPasswordValidator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#1)]
 [!code-vb[C_CustomUsernameAndPasswordValidator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#1)]  
[!code-csharp[C_CustomUsernameAndPasswordValidator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#2)]
[!code-vb[C_CustomUsernameAndPasswordValidator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#2)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>  
 [Vorgehensweise: Verwenden des ASP.NET-Mitgliedschaftsanbieters](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)  
 [Authentifizierung](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)

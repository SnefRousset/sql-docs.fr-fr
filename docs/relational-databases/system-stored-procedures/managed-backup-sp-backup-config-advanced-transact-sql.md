---
title: managed_backup.sp_backup_config_advanced (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_optional
- sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional
dev_langs:
- TSQL
helpviewer_keywords:
- sp_backup_config_optional
- managed_backup.sp_backup_config_optional
ms.assetid: 4fae8193-1f88-48fd-a94a-4786efe8d6af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 86db5a13ab1bdac2b35c6d5128ba1b2234bc24b7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52536404"
---
# <a name="managedbackupspbackupconfigadvanced-transact-sql"></a>managed_backup.sp_backup_config_advanced (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configure les paramètres avancés pour [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```vb  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="Arguments"></a> Arguments  
 @database_name  
 Le nom de la base de données, permettant la gestion de sauvegarde sur une base de données spécifique. Si NULL ou *, cette sauvegarde managée s’appliqu’à toutes les bases de données sur le serveur.  
  
 @encryption_algorithm  
 Nom de l'algorithme de chiffrement utilisé lors de la sauvegarde pour chiffrer le fichier de sauvegarde. Le @encryption_algorithm est **SYSNAME**. C'est un paramètre requis lorsque vous configurez la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pour la première fois pour la base de données. Spécifiez **NO_ENCRYPTION** si vous ne souhaitez pas chiffrer le fichier de sauvegarde. Lorsque vous modifiez le [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] paramètres de configuration, ce paramètre est facultatif : si le paramètre n’est pas spécifié, puis les valeurs de configuration existantes sont conservées. Les valeurs autorisées pour ce paramètre sont :  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 Pour plus d'informations sur les algorithmes de chiffrement, consultez [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
 @encryptor_type  
 Le type de chiffreur, ce qui peut être soit « certificat » ou « ASYMMETRIC_KEY ». Le @encryptor_type est **nvarchar (32)**. Ce paramètre est facultatif si vous spécifiez NO_ENCRYPTION pour le @encryption_algorithm paramètre.  
  
 @encryptor_name  
 Nom d'un certificat ou d'une clé asymétrique qui existe, utilisé pour chiffrer la sauvegarde. Le @encryptor_name est **SYSNAME**. Si vous utilisez une clé asymétrique, elle doit être configurée avec la gestion de clés extensible (EKM). Ce paramètre est facultatif si vous spécifiez NO_ENCRYPTION pour le @encryption_algorithm paramètre.  
  
 Pour plus d’informations, consultez [Gestion de clés extensible &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 @local_cache_path  
 Ce paramètre n’est pas encore pris en charge.  
  
## <a name="return-code-value"></a>Valeur du code de retour  
 0 (réussite) ou 1 (échec)  
  
## <a name="security"></a>Sécurité  
  
### <a name="permissions"></a>Autorisations  
 Nécessite l’appartenance au **db_backupoperator** rôle, de base de données avec **ALTER ANY CREDENTIAL** autorisations, et **EXECUTE** autorisations sur **sp_delete_ backuphistory** procédure stockée.  
  
## <a name="examples"></a>Exemples  
 L’exemple suivant définit les options de configuration avancées pour [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] pour l’instance de SQL Server.  
  
```  
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>Voir aussi  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  

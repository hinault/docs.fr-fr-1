---
title: "Sérialisation binaire"
ms.date: 01/02/2018
ms.prod: .net
ms.topic: article
helpviewer_keywords:
- binary serialization
- serialization, about serialization
- deserialization
- binary serialization, about serialization
- binary serialization, .net core serialization
- serialization, cross-framework
ms.assetid: 2b1ea3be-1152-4032-b2b3-07794054c405
caps.latest.revision: 
author: ViktorHofer
ms.author: mairaw
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 509d29ee2a6fe2f0b9d63d1cf69919a3de41bac2
ms.sourcegitcommit: 099aa20d9b6450d1b7452d782a55771a6ad8ff35
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/05/2018
---
# <a name="binary-serialization"></a>Sérialisation binaire

La sérialisation peut être définie comme le processus de stockage de l'état d'un objet sur un support de stockage. Pendant ce processus, les champs publics et privés de l'objet et le nom de la classe, y compris l'assembly contenant la classe, sont convertis en un flux de données d'octets, écrit ensuite dans un flux de données. Lorsque l'objet est désérialisé par la suite, un clone exact de l'objet d'origine est créé.

Lorsque vous implémentez un mécanisme de sérialisation dans un environnement orienté objet, vous devez faire plusieurs compromis entre facilité d'utilisation et souplesse. Le processus peut être automatisé en grande partie, à condition que vous puissiez suffisamment le contrôler. Par exemple, dans certaines situations, la sérialisation binaire simple n'est pas suffisante ou une raison particulière peut exiger la définition des champs à sérialiser. Les sections suivantes étudient le mécanisme de sérialisation fiable fourni avec .NET et mettent en évidence plusieurs fonctionnalités importantes qui vous permettent de personnaliser le processus en fonction de vos besoins.

> [!NOTE]
> L'état d'un objet encodé UTF-8 ou UTF-7 n'est pas préservé si l'objet est sérialisé et désérialisé à l'aide de différentes versions du .NET Framework.

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

Étant donné que la nature de la sérialisation binaire autorise la modification des membres privés à l’intérieur d’un objet, et par conséquent la modification de l’état de ce dernier, d’autres infrastructures de sérialisation qui opèrent sur la surface publique de l’API, comme JSON.NET, sont recommandées.

## <a name="binary-serialization-in-net-core"></a>Sérialisation binaire dans .NET Core

.NET Core prend en charge la sérialisation binaire avec un sous-ensemble de types. Vous trouverez la liste des types pris en charge dans la section [Types sérialisables](#serializable-types). L’ensemble défini des types est garanti comme étant sérialisable entre le .NET Framework 4.5.1 et versions ultérieures et .NET Core 2.0 et versions ultérieures. D’autres implémentations de .NET, tels que Mono, ne sont pas officiellement prises en charge mais devraient également fonctionner.

### <a name="serializable-types"></a>Types sérialisables

- <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderInternalCompilerException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.AccessViolationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.AggregateException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.AppDomainUnloadedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ApplicationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ArgumentException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ArgumentNullException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ArgumentOutOfRangeException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ArithmeticException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Array?displayProperty=nameWithType>   
- <xref:System.ArraySegment%601?displayProperty=nameWithType>   
- <xref:System.ArrayTypeMismatchException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Attribute?displayProperty=nameWithType>
- <xref:System.BadImageFormatException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Boolean?displayProperty=nameWithType>   
- <xref:System.Byte?displayProperty=nameWithType>   
- <xref:System.CannotUnloadAppDomainException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Char?displayProperty=nameWithType>   
- <xref:System.Collections.ArrayList?displayProperty=nameWithType>   
- <xref:System.Collections.BitArray?displayProperty=nameWithType>   
- <xref:System.Collections.Comparer?displayProperty=nameWithType>   
- <xref:System.Collections.DictionaryEntry?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.Comparer%601?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.EqualityComparer%601?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.HashSet%601?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Collections.Generic.KeyValuePair%602?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.LinkedList%601?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.SortedList%602?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.SortedSet%601?displayProperty=nameWithType>   
- <xref:System.Collections.Generic.Stack%601?displayProperty=nameWithType>   
- <xref:System.Collections.Hashtable?displayProperty=nameWithType>   
- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=nameWithType>   
- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=nameWithType>   
- <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType>   
- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=nameWithType>   
- <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=nameWithType>   
- <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType>   
- <xref:System.Collections.Queue?displayProperty=nameWithType>   
- <xref:System.Collections.SortedList?displayProperty=nameWithType>   
- <xref:System.Collections.Specialized.HybridDictionary?displayProperty=nameWithType>   
- <xref:System.Collections.Specialized.ListDictionary?displayProperty=nameWithType>   
- <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=nameWithType>   
- <xref:System.Collections.Specialized.StringCollection?displayProperty=nameWithType>   
- <xref:System.Collections.Specialized.StringDictionary?displayProperty=nameWithType>   
- <xref:System.Collections.Stack?displayProperty=nameWithType>   
- `System.Collections.Generic.NonRandomizedStringEqualityComparer`<!--zz <xref:System.Collections.Generic.NonRandomizedStringEqualityComparer?displayProperty=nameWithType> --> (disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ComponentModel.BindingList%601?displayProperty=nameWithType>   
- <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ComponentModel.Design.CheckoutException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ComponentModel.InvalidAsynchronousStateException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ComponentModel.LicenseException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures, la sérialisation à partir de .NET Framework vers le .NET Core n'est pas pris en charge)
- <xref:System.ComponentModel.WarningException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ComponentModel.Win32Exception?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Configuration.ConfigurationErrorsException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Configuration.ConfigurationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Configuration.Provider.ProviderException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Configuration.SettingsPropertyIsReadOnlyException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Configuration.SettingsPropertyNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Configuration.SettingsPropertyWrongTypeException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ContextMarshalException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DBNull?displayProperty=nameWithType>(disponible dans .NET Core 2.0.2 et versions ultérieures)   
- <xref:System.Data.Common.DbException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.ConstraintException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.DBConcurrencyException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.DataException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.DataSet?displayProperty=nameWithType>   
- <xref:System.Data.DataTable?displayProperty=nameWithType>   
- <xref:System.Data.DeletedRowInaccessibleException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.DuplicateNameException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.EvaluateException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.InRowChangingEventException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.InvalidConstraintException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.InvalidExpressionException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.MissingPrimaryKeyException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.NoNullAllowedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.Odbc.OdbcException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.OperationAbortedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.PropertyCollection?displayProperty=nameWithType>   
- <xref:System.Data.ReadOnlyException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.RowNotInTableException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.SqlClient.SqlException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures, la sérialisation à partir de .NET Framework vers le .NET Core n'est pas pris en charge)
- <xref:System.Data.SqlTypes.SqlAlreadyFilledException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.SqlTypes.SqlBoolean?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlByte?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlDateTime?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlDouble?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlGuid?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlInt16?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlInt32?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlInt64?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlNotFilledException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.SqlTypes.SqlNullValueException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.SqlTypes.SqlString?displayProperty=nameWithType>   
- <xref:System.Data.SqlTypes.SqlTruncateException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.SqlTypes.SqlTypeException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.StrongTypingException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.SyntaxErrorException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Data.VersionNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DataMisalignedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DateTime?displayProperty=nameWithType>   
- <xref:System.DateTimeOffset?displayProperty=nameWithType>   
- <xref:System.Decimal?displayProperty=nameWithType>   
- `System.Diagnostics.Contracts.ContractException`<!--zz <xref:System.Diagnostics.Contracts.ContractException?displayProperty=nameWithType> --> (disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Diagnostics.Tracing.EventSourceException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.AccountManagement.MultipleMatchesException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.AccountManagement.NoMatchingPrincipalException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.AccountManagement.PasswordException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.AccountManagement.PrincipalException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.AccountManagement.PrincipalExistsException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.AccountManagement.PrincipalOperationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.AccountManagement.PrincipalServerDownException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectExistsException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryOperationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryServerDownException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.ActiveDirectory.ForestTrustCollisionException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.ActiveDirectory.SyncFromAllServersOperationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.DirectoryServicesCOMException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.Protocols.BerConversionException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.Protocols.DirectoryException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.Protocols.DirectoryOperationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.Protocols.LdapException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DirectoryServices.Protocols.TlsOperationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DivideByZeroException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.DllNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Double?displayProperty=nameWithType>   
- <xref:System.Drawing.Color?displayProperty=nameWithType>   
- <xref:System.Drawing.Point?displayProperty=nameWithType>   
- <xref:System.Drawing.PointF?displayProperty=nameWithType>   
- <xref:System.Drawing.Rectangle?displayProperty=nameWithType>   
- <xref:System.Drawing.RectangleF?displayProperty=nameWithType>   
- <xref:System.Drawing.Size?displayProperty=nameWithType>   
- <xref:System.Drawing.SizeF?displayProperty=nameWithType>   
- <xref:System.DuplicateWaitObjectException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.EntryPointNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Enum?displayProperty=nameWithType>   
- <xref:System.EventArgs?displayProperty=nameWithType>(disponible dans .NET Core 2.0.6 et versions ultérieures)
- <xref:System.Exception?displayProperty=nameWithType>   
- <xref:System.ExecutionEngineException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.FieldAccessException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.FormatException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Globalization.CompareInfo?displayProperty=nameWithType>   
- <xref:System.Globalization.CultureNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Globalization.SortVersion?displayProperty=nameWithType>   
- <xref:System.Guid?displayProperty=nameWithType>   
- `System.IO.Compression.ZLibException`<!--zz <xref:System.IO.Compression.ZLibException?displayProperty=nameWithType --> (disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.DriveNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.EndOfStreamException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.FileFormatException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.FileLoadException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.FileNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.IOException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.InternalBufferOverflowException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.InvalidDataException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.IsolatedStorage.IsolatedStorageException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IO.PathTooLongException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.IndexOutOfRangeException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.InsufficientExecutionStackException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.InsufficientMemoryException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Int16?displayProperty=nameWithType>   
- <xref:System.Int32?displayProperty=nameWithType>   
- <xref:System.Int64?displayProperty=nameWithType>   
- <xref:System.IntPtr?displayProperty=nameWithType>   
- <xref:System.InvalidCastException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.InvalidOperationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.InvalidProgramException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.InvalidTimeZoneException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.MemberAccessException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.MethodAccessException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.MissingFieldException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.MissingMemberException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.MissingMethodException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.MulticastNotSupportedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.Cookie?displayProperty=nameWithType>   
- <xref:System.Net.CookieCollection?displayProperty=nameWithType>   
- <xref:System.Net.CookieContainer?displayProperty=nameWithType>   
- <xref:System.Net.CookieException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.HttpListenerException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.Mail.SmtpException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.Mail.SmtpFailedRecipientException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.Mail.SmtpFailedRecipientsException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.NetworkInformation.NetworkInformationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.NetworkInformation.PingException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.ProtocolViolationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.Sockets.SocketException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.WebException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Net.WebSockets.WebSocketException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.NotFiniteNumberException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.NotImplementedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.NotSupportedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.NullReferenceException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Nullable%601?displayProperty=nameWithType>   
- <xref:System.Numerics.BigInteger?displayProperty=nameWithType>   
- <xref:System.Numerics.Complex?displayProperty=nameWithType>   
- <xref:System.Object?displayProperty=nameWithType>   
- <xref:System.ObjectDisposedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.OperationCanceledException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.OutOfMemoryException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.OverflowException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.PlatformNotSupportedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.RankException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Reflection.AmbiguousMatchException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Reflection.CustomAttributeFormatException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Reflection.InvalidFilterCriteriaException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Reflection.ReflectionTypeLoadException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures, la sérialisation à partir de .NET Framework vers le .NET Core n'est pas pris en charge)
- <xref:System.Reflection.TargetException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Reflection.TargetInvocationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Reflection.TargetParameterCountException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Resources.MissingManifestResourceException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Resources.MissingSatelliteAssemblyException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.CompilerServices.RuntimeWrappedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.COMException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.ExternalException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.InvalidComObjectException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.InvalidOleVariantTypeException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.MarshalDirectiveException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.SEHException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.Serialization.InvalidDataContractException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Runtime.Serialization.SerializationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.SByte?displayProperty=nameWithType>   
- <xref:System.Security.AccessControl.PrivilegeNotHeldException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.Authentication.AuthenticationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.Authentication.InvalidCredentialException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.Cryptography.CryptographicException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.Cryptography.CryptographicUnexpectedOperationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- `System.Security.Cryptography.Xml.CryptoSignedXmlRecursionException`<!--zz <xref:System.Security.Cryptography.Xml.CryptoSignedXmlRecursionException?displayProperty=nameWithType --> (disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.HostProtectionException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.Policy.PolicyException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.Principal.IdentityNotMappedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.SecurityException?displayProperty=nameWithType>(disponible dans le .NET Core 2.0.4 et versions ultérieures, les données de sérialisation limitée)
- <xref:System.Security.VerificationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Security.XmlSyntaxException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ServiceProcess.TimeoutException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Single?displayProperty=nameWithType>   
- <xref:System.StackOverflowException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.String?displayProperty=nameWithType>   
- <xref:System.StringComparer?displayProperty=nameWithType>   
- <xref:System.SystemException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Text.DecoderFallbackException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Text.EncoderFallbackException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Text.RegularExpressions.RegexMatchTimeoutException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Text.StringBuilder?displayProperty=nameWithType>   
- <xref:System.Threading.AbandonedMutexException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.BarrierPostPhaseException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.LockRecursionException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.SemaphoreFullException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.SynchronizationLockException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.Tasks.TaskCanceledException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.Tasks.TaskSchedulerException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.ThreadAbortException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.ThreadInterruptedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.ThreadStartException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.ThreadStateException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Threading.WaitHandleCannotBeOpenedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.TimeSpan?displayProperty=nameWithType>   
- <xref:System.TimeZoneInfo.AdjustmentRule?displayProperty=nameWithType>   
- <xref:System.TimeZoneInfo?displayProperty=nameWithType>   
- <xref:System.TimeZoneNotFoundException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.TimeoutException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Transactions.TransactionAbortedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Transactions.TransactionException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Transactions.TransactionInDoubtException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Transactions.TransactionManagerCommunicationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Transactions.TransactionPromotionException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Tuple?displayProperty=nameWithType>   
- <xref:System.TypeAccessException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.TypeInitializationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.TypeLoadException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.TypeUnloadedException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.UInt16?displayProperty=nameWithType>   
- <xref:System.UInt32?displayProperty=nameWithType>   
- <xref:System.UInt64?displayProperty=nameWithType>   
- <xref:System.UIntPtr?displayProperty=nameWithType>   
- <xref:System.UnauthorizedAccessException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Uri?displayProperty=nameWithType>   
- <xref:System.UriFormatException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.ValueTuple?displayProperty=nameWithType>(non sérialisable dans .NET Framework 4.7 et versions antérieures)  
- <xref:System.ValueType?displayProperty=nameWithType>   
- <xref:System.Version?displayProperty=nameWithType>   
- <xref:System.WeakReference%601?displayProperty=nameWithType>   
- <xref:System.WeakReference?displayProperty=nameWithType>   
- <xref:System.Xml.Schema.XmlSchemaException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Xml.Schema.XmlSchemaInferenceException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Xml.Schema.XmlSchemaValidationException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Xml.XPath.XPathException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Xml.XmlException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Xml.Xsl.XsltCompileException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)
- <xref:System.Xml.Xsl.XsltException?displayProperty=nameWithType>(disponible dans .NET Core 2.0.4 et versions ultérieures)

## <a name="in-this-section"></a>Dans cette section

 [Concepts de la sérialisation](../../../docs/standard/serialization/serialization-concepts.md)  
 Aborde deux scénarios où la sérialisation est utile : conservation des données en stockage et passage d'objets sur des domaines d'application.  
  
 [Sérialisation de base](../../../docs/standard/serialization/basic-serialization.md)  
 Décrit comment utiliser les formateurs binaires et SOAP pour sérialiser des objets.  
  
 [Sérialisation sélective](../../../docs/standard/serialization/selective-serialization.md)  
 Décrit comment empêcher certains membres d'une classe d'être sérialisés.  
  
 [Sérialisation personnalisée](../../../docs/standard/serialization/custom-serialization.md)  
 Décrit comment personnaliser la sérialisation d’une classe en utilisant l’interface <xref:System.Runtime.Serialization.ISerializable>.  
  
 [Étapes du processus de sérialisation](../../../docs/standard/serialization/steps-in-the-serialization-process.md)  
 Décrit le plan d'action de la sérialisation lorsque la méthode <xref:System.Runtime.Serialization.Formatter.Serialize%2A> est appelée sur un formateur.  
  
 [Sérialisation avec tolérance de version](../../../docs/standard/serialization/version-tolerant-serialization.md)  
 Explique comment créer des types sérialisables qui peuvent être modifiés avec le temps sans que les applications ne lèvent d'exceptions.  
  
 [Indications concernant la sérialisation](../../../docs/standard/serialization/serialization-guidelines.md)  
 Fournit des indications générales pour décider quand sérialiser un objet.  
  
## <a name="reference"></a>Référence  
 <xref:System.Runtime.Serialization>  
 Contient des classes qui peuvent être utilisées pour sérialiser et désérialiser des objets.  
  
## <a name="related-sections"></a>Rubriques connexes  
 [Sérialisation XML et SOAP](../../../docs/standard/serialization/xml-and-soap-serialization.md)  
 Décrit le mécanisme de sérialisation XML inclus avec le Common Language Runtime.  
  
 [Sécurité et sérialisation](../../../docs/framework/misc/security-and-serialization.md)  
 Décrit les indications de codage sécurisé à suivre lors de l'écriture du code qui exécute la sérialisation.  
  
 [Objets distants](http://msdn.microsoft.com/library/515686e6-0a8d-42f7-8188-73abede57c58)  
 Décrit les différentes méthodes de communication disponibles dans le .NET Framework pour les communications distantes.  
  
 [Création de services Web XML à l’aide de clients de service Web XML et ASP.NET](http://msdn.microsoft.com/library/1e64af78-d705-4384-b08d-591a45f4379c)  
 Fournit des rubriques qui décrivent et expliquent comment programmer des services Web XML créés à l'aide d'ASP.NET.

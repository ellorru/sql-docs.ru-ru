---
title: Развертывание приложения уровня данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploydacwizard.updateconfiguration.f1
- sql12.swb.deploydacwizard.selectdac.f1
- sql12.swb.deploydacwizard.deploydac.f1
- sql12.swb.deploydacwizard.introduction.f1
- sql12.swb.deploydacwizard.summary.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00208b1c0f11faf8f392e47e275c7e239249d3d6
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783070"
---
# <a name="deploy-a-data-tier-application"></a>Развертывание приложения уровня данных
  Приложение уровня данных (DAC) вы можете развернуть из пакета DAC на существующем экземпляре [!INCLUDE[ssDE](../../includes/ssde-md.md)] или [!INCLUDE[ssSDS](../../includes/sssds-md.md)] с помощью мастера или скрипта Powershell. Процесс развертывания регистрирует экземпляр приложения уровня данных путем сохранения определения приложения уровня данных в системной базе данных **msdb** (**master** в [!INCLUDE[ssSDS](../../includes/sssds-md.md)]), создает базу данных и заполняет ее всеми объектами базы данных, заданными в приложении уровня данных.  
  
-   **Перед началом работы**  [Служебная программа SQL Server](#SQLUtility), [Параметры базы данных и параметры](#DBOptSettings), [ограничения](#LimitationsRestrictions), [Предварительные требования](#Prerequisites), [Безопасность](#Security), [разрешения](#Permissions)  
  
-   **Развертывание приложения уровня данных с помощью:**  [Мастер развертывания приложения уровня данных](#UsingDeployDACWizard), [PowerShell](#DeployDACPowerShell)  
  
##  <a name="BeforeBegin"></a> Перед началом  
 Один и тот же пакет приложения уровня данных может быть развернут на одном экземпляре компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] несколько раз, но каждый раз можно развертывать только по одному пакету. На экземпляре компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]имя экземпляра приложения уровня данных, указанное для каждого развертывания, должно быть уникальным.  
  
###  <a name="SQLUtility"></a>служебная программа SQL Server  
 Если приложение уровня данных развертывается на управляемом экземпляре компонента Database Engine, развернутое приложение уровня данных будет включено в служебную программу SQL Server при следующей отправке набора элементов сбора программы из экземпляра в пункт управления программой. После этого приложение уровня данных появится в узле **Развернутые приложения уровня данных** в окне [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Развернутые приложения уровня данных** details page.  
  
###  <a name="DBOptSettings"></a> Настройка параметров баз данных  
 По умолчанию база данных, созданная при развертывании, получит все параметры по умолчанию из инструкции CREATE DATABASE, кроме следующих.  
  
-   Параметры сортировки и уровень совместимости базы данных устанавливаются в соответствии со значениями, заданными в пакете DAC. Пакет приложения уровня данных (DAC), созданный на основе проекта базы данных в средствах разработчика SQL Server (SQL Server Developer Tools), использует значения, заданные в проекте базы данных. Пакет, извлеченный из существующей базы данных, использует значения этой базы данных.  
  
-   Некоторые параметры баз данных, например имя базы данных и пути к файлам, можно изменять на странице **Обновление конфигурации** . При развертывании в [!INCLUDE[ssSDS](../../includes/sssds-md.md)]пути файлов задавать нельзя.  
  
 Некоторые параметры баз данных, например TRUSTWORTHY, DB_CHAINING и HONOR_BROKER_PRIORITY, нельзя изменять в рамках процедуры развертывания. Физические свойства, например количество файловых групп или количество и размер файлов, нельзя изменять в рамках процедуры развертывания. После завершения развертывания можно настроить базу данных с помощью инструкции ALTER DATABASE, среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]или программы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.  
  
###  <a name="LimitationsRestrictions"></a> Ограничения  
 Развернуть приложение уровня данных можно на экземпляре компонента [!INCLUDE[ssSDS](../../includes/sssds-md.md)]или экземпляре [!INCLUDE[ssDE](../../includes/ssde-md.md)] , где выполняется [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] с пакетом обновления 4 (SP4) или более поздней версии. Приложение уровня данных, созданное с помощью более поздней версии, может содержать объекты, неподдерживаемые в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Невозможно развернуть данные приложения уровня данных для экземпляров [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Рекомендуется не выполнять развертывание пакетов DAC, полученных из неизвестных или ненадежных источников. Эти пакеты могут содержать вредоносный код, который может выполнить непредусмотренный код Transact-SQL или вызвать ошибки, изменив схему. Прежде чем использовать пакет из неизвестного или ненадежного источника, распакуйте приложение уровня данных и проверьте такой код, как хранимые процедуры или другой пользовательский код. Дополнительные сведения о том, как выполнить эти проверки, см. в разделе [Validate a DAC Package](validate-a-dac-package.md).  
  
###  <a name="Security"></a> безопасность  
 Для повышения безопасности имена входа, использующие проверку подлинности SQL Server, хранятся в пакете DAC без пароля. При развертывании или обновлении пакета имя входа создается как отключенное имя входа с созданным паролем. Чтобы включить имена входа, войдите в систему под учетной записью, имеющей разрешение ALTER ANY LOGIN и с помощью команды ALTER LOGIN включите имя входа и присвойте ему новый пароль, который можно передать пользователю. Это не требуется для имен входа, использующих проверку подлинности Windows, поскольку SQL Server не управляет их паролями.  
  
####  <a name="Permissions"></a> Permissions  
 Развертывать приложения уровня данных могут только члены предопределенных ролей сервера **sysadmin** или **serveradmin** либо члены предопределенной роли сервера **dbcreator** с разрешениями ALTER ANY LOGIN. Встроенная учетная запись системного администратора [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с именем **sa** также может развертывать приложения уровня данных. При развертывании DAC с именами входа в [!INCLUDE[ssSDS](../../includes/sssds-md.md)] необходимо иметь членство в ролях loginmanager или serveradmin. При развертывании приложения уровня данных без имен входа в [!INCLUDE[ssSDS](../../includes/sssds-md.md)] необходимо членство в ролях dbmanager или serveradmin.  
  
##  <a name="UsingDeployDACWizard"></a>Использование мастера развертывания приложения уровня данных  
 **Развертывание приложения уровня данных с помощью мастера**  
  
1.  В **обозревателе объектов**раскройте узел экземпляра, в котором нужно развернуть приложение уровня данных.  
  
2.  Щелкните правой кнопкой мыши узел **Базы данных** и выберите **Развернуть приложение уровня данных…** .  
  
3.  Выполните шаги в диалоговых окнах мастера.  
  
    -   [Вводная страница](#Introduction)  
  
    -   [Страница «Выбор пакета приложения уровня данных»](#Select_dac_package)  
  
    -   [Страница «Просмотр политики»](#Review_policy)  
  
    -   [Страница «Обновление конфигурации»](#Update_configuration)  
  
    -   [Страница «Сводка»](#Summary)  
  
    -   [Страница развертывания](#Deploy)  
  
##  <a name="Introduction"></a> Вводная страница  
 На этой странице описаны шаги развертывания приложения уровня данных.  
  
 **Больше не показывать эту страницу.** — щелкните этот флажок, чтобы предотвратить отображение этой страницы в будущем.  
  
 **Далее >** — переход на страницу **Выбор пакета приложения уровня данных**.  
  
 **Отмена** — завершение работы мастера без развертывания приложения уровня данных.  
  
##  <a name="Select_dac_package"></a>Страница «Выбор пакета приложения уровня данных»  
 Эта страница используется для указания пакета приложения уровня данных, содержащего приложение уровня данных для развертывания. Страница проходит через три состояния.  
  
### <a name="select-the-dac-package"></a>Выбор пакета DAC  
 Чтобы выбрать пакет DAC для развертывания, воспользуйтесь первоначальным состоянием страницы. Пакет DAC должен представлять собой работоспособный файл пакета DAC с расширением DACPAC.  
  
 **Пакет приложения уровня данных** — указание пути и имени файла пакета приложения уровня данных, содержащего приложение уровня данных для развертывания. Чтобы указать расположение пакета DAC, можно нажать кнопку **Обзор** в правой части окна.  
  
 **Имя приложения** — доступное только для чтения поле, в котором отображается имя, присвоенное пакету приложения уровня данных при создании или извлечении из базы данных.  
  
 **Версия** — доступное только для чтения поле, в котором отображается версия, присвоенная пакету DAC при создании или извлечении из базы данных.  
  
 **Описание** — доступное только для чтения поле, в котором отображается описание, сделанное при создании или извлечении пакета DAC из базы данных.  
  
 **\< Назад** — возврат на страницу **Введение** .  
  
 **Далее >**  — отображается индикатор выполнения, когда мастер подтверждает, что выбранный файл является исправным пакетом приложения уровня данных.  
  
 **Отмена** — мастер прекращает работу без развертывания DAC.  
  
### <a name="validating-the-dac-package"></a>Проверка пакета DAC  
 Отображается индикатор выполнения, когда мастер подтверждает, что выбранный файл является исправным пакетом DAC. Если пакет приложения уровня данных прошел проверку, то мастер перейдет на итоговую версию страницы **Выбор пакета** , на которой можно ознакомиться с результатами проверки. Если файл не является исправным пакетом DAC, то мастер остается на странице **Выбор пакета DAC**. Выберите другой исправный пакет DAC, либо выйдите из мастера и создайте новый пакет DAC.  
  
 **Проверка содержимого DAC** — индикатор выполнения, отражающий текущее состояние процесса выполнения.  
  
 **\< Previous** — возврат к начальному состоянию страницы **Выбор пакета** .  
  
 **Далее >**  — переход к окончательной версии страницы **Выбор пакета**.  
  
 **Отмена** — мастер прекращает работу без развертывания DAC.  
  
##  <a name="Review_policy"></a> Страница «Просмотр политики»  
 На этой странице можно просмотреть результаты проверки политики выбора на сервере DAC, если у DAC есть политика. Политика выбора сервера приложения уровня данных является необязательной. Она назначается приложению уровня данных при его создании в среде Visual Studio. Политика с помощью аспектов политики выбора серверов задает условия, которым экземпляр компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] должен соответствовать, чтобы на нем можно было размещать DAC.  
  
 **Результаты оценки условий политики** — доступный только для чтения отчет, в котором говорится, удовлетворены ли условия политики развертывания приложения уровня данных. Результаты проверки каждого из условий выводятся отдельной строкой.  
  
 Следующие политики выбора сервера всегда возвращают значение False при развертывании DAC в [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: версия операционной системы, язык, включенные именованные каналы, платформа и включенный протокол TCP.  
  
 **Игнорировать нарушения политики** — установите этот флажок, чтобы приступить к развертыванию, если не удалось соблюсти одно или несколько условий политики. Этот параметр следует выбирать только при уверенности, что ни одно из невыполненных условий не будет препятствовать успешной работе DAC.  
  
 **\< Previous** — возврат на страницу **Выбор пакета** .  
  
 **Далее >** — переход на страницу **Обновление конфигурации**.  
  
 **Отмена** — мастер прекращает работу без развертывания DAC.  
  
##  <a name="Update_configuration"></a>Страница «Обновление конфигурации»  
 Эта страница используется для указания имен разворачиваемого экземпляра приложения уровня данных и базы данных, создаваемой при развертывании, а также задания параметров базы данных.  
  
 **Имя базы данных:** — укажите имя базы данных, которая будет создана при развертывании. По умолчанию указывается имя базы данных-источника, из которой было извлечено приложение уровня данных. Имя должно быть уникальным на данном экземпляре компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] и должно соответствовать правилам для идентификаторов компонентов [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 При изменении имени базы данных имена файлов данных и журналов также изменятся с учетом этого нового значения.  
  
 Имя базы данных также используется в качестве имени экземпляра приложения уровня данных. Имя экземпляра отображается в узле для приложения уровня данных, расположенном в узле **Приложения уровня данных** в **Обозревателе объектов**или в узле **Развернутые приложения уровня данных** в **Обозревателе программ**.  
  
 Следующие параметры не применяются к [!INCLUDE[ssSDS](../../includes/sssds-md.md)]и не отображаются при выполнении развертывания в [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 **Использовать расположение базы данных по умолчанию** — установите этот параметр, чтобы файлы данных и журналов базы данных создавались в расположении экземпляра компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]по умолчанию. Имена файлов будут сформированы с использованием имени базы данных.  
  
 **Указать файлы базы данных** — выберите этот параметр, чтобы указать другое расположение или имя для файлов данных и журнала.  
  
 **Имя файла данных и путь к нему:** — укажите полный путь к файлу данных и его имя. В этом поле содержится путь и имя файла по умолчанию. Измените строку в этом поле, чтобы изменить значение по умолчанию, либо с помощью кнопки «Обзор» перейдите в папку, в которую следует поместить файл данных.  
  
 **Имя файла журнала и путь к нему:** — укажите полный путь и имя файла журнала. В этом поле содержится путь и имя файла по умолчанию. Измените строку в этом поле, чтобы изменить значение по умолчанию, либо с помощью кнопки **Обзор** перейдите в папку, в которую следует поместить файл журнала.  
  
 **\< Previous** — возврат на страницу **Выбор пакета приложения уровня** данных.  
  
 **Далее >** — переход к странице **Сводка**.  
  
 **Отмена** — мастер прекращает работу без развертывания DAC.  
  
##  <a name="Summary"></a> Страница «Сводка»  
 На этой странице можно ознакомиться с действиями, которые будут выполнены мастером при развертывании приложения уровня данных.  
  
 **Следующие параметры будут использоваться для развертывания приложения уровня данных.** Просмотрите отображенные сведения для проверки правильности произведенных действий. В этом окне отображается выбранный пакет приложения уровня данных, а также имя, указанное для развертываемого экземпляра приложения уровня данных. В этом окне также отображаются параметры, которые будут использоваться при создании базы данных, связанной с этим приложением уровня данных.  
  
 **\< Previous** — возврат на страницу **конфигурации обновления** для изменения выбора.  
  
 **Далее >** — развертывание приложения уровня данных и отображение результатов на странице **Развертывание DAC**.  
  
 **Отмена** — мастер прекращает работу без развертывания DAC.  
  
##  <a name="Deploy"></a>Страница развертывания  
 Эта страница сообщает об успешном или неуспешном завершении операции развертывания.  
  
 **Развертывание приложения уровня данных** — сообщает об успехе или неуспехе каждого действия, предпринятого для развертывания приложения уровня данных. Просмотрите эти сведения, чтобы выяснить результаты каждого действия. Для каждого действия, в котором обнаружена ошибка, предусмотрена ссылка в столбце **Результат** . Выберите эту ссылку, чтобы просмотреть отчет об ошибках, относящихся данному действию.  
  
 **Сохранить отчет** — сохранить отчет о развертывании в HTML-файле. В этом файле содержится отчет о состоянии каждого из действий, в том числе все выданные сообщения об ошибках. По умолчанию используется папка «SQL Server Management Studio\DAC Packages», вложенная в папку Documents рабочего каталога учетной записи пользователя Windows.  
  
 **Готово** — завершает работу мастера.  
  
##  <a name="DeployDACPowerShell"></a> Использование PowerShell  
 **Развертывание приложения уровня данных с помощью метода Install () в скрипте PowerShell**  
  
1.  Создайте объект SMO Server и задайте его экземпляру, в котором хотите развернуть приложение уровня данных.  
  
2.  Откройте объект `ServerConnection` и подключитесь к тому же экземпляру.  
  
3.  Используйте `System.IO.File` для загрузки файла пакета приложения уровня данных.  
  
4.  Используйте `add_DacActionStarted` и `add_DacActionFinished`, чтобы подписаться на события приложения уровня данных.  
  
5.  Задайте `DatabaseDeploymentProperties`.  
  
6.  Используйте метод `DacStore.Install` для развертывания приложения уровня данных.  
  
7.  Закройте файловый поток, используемый для чтения файла пакета приложения уровня данных.  
  
### <a name="example-powershell"></a>Пример (PowerShell)  
 В следующем примере приложение уровня данных MyApplication развертывается на экземпляре [!INCLUDE[ssDE](../../includes/ssde-md.md)]по умолчанию с использованием определения приложения уровня данных из пакета MyApplication.dacpac.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>См. также  
 [Приложения уровня данных](data-tier-applications.md)   
 [Извлечение приложения уровня данных из базы данных](extract-a-dac-from-a-database.md)   
 [Идентификаторы баз данных](../databases/database-identifiers.md)  

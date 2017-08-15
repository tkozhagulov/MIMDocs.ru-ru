---
title: "Справочник по конфигурации отображения элемента управления ресурса (XML)| Документация Майкрософт"
description: 
keywords: 
author: fimguy
ms.author: fimguy
manager: mbaldwin
ms.date: 05/1/2017
ms.topic: reference
ms.prod: identity-manager-2016
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 
ms.openlocfilehash: c6ed843fb15b150fc934062945ab76ba32d72d33
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="resource-control-display-configuration-xml-reference"></a>Справочник по конфигурации отображения элемента управления ресурса (XML)

Ресурсы конфигурации отображения элемента управления ресурса (RCDC) определяются пользователем. Они позволяют управлять отображением других ресурсов в хранилище данных Microsoft Identity Manager (MIM) 2016 с пакетом обновления 1 (SP1) в пользовательском интерфейсе. Каждый ресурс RCDC содержит XML-файл конфигурации, с помощью которого можно добавлять, изменять или удалять текст и элементы управления пользовательского интерфейса. MIM 2016 SP1 предоставляет несколько стандартных ресурсов RCDC, но вы можете создавать настраиваемые ресурсы RCDC для настраиваемых ресурсов. Дополнительные сведения об использовании пользовательского интерфейса RCDC на портале FIM см. в статье [Introduction to Configuring and Customizing the FIM Portal](http://go.microsoft.com/fwlink/?LinkID=165848) (Общие сведения о конфигурации и настройке портала FIM).


## <a name="known-issues"></a>Известные проблемы

Для многих элементов управления RCDC значения по умолчанию не поддерживаются.

В этом выпуске значения по умолчанию поддерживаются только для элемента управления "Кнопка". Для раскрывающегося списка эту проблему можно решить, указав значение по умолчанию, не связанное с любым другим значением, чтобы пользователь мог изменить выбор. Что касается других элементов управления, следует использовать рабочий процесс авторизации, чтобы указать значение по умолчанию при отправке запроса.

## <a name="basic-structure"></a>Основная структура

XML-данные для ресурса RCDC состоят из одного XML-элемента **ObjectControlConfiguration.**

>[!NOTE]
Полную схему XSD см. в приложении A "Стандартная схема XSD" этого документа.

Ниже приведена схема XSD для элемента ObjectControlConfiguration:

```XML
<xsd:element name="ObjectControlConfiguration"\>
  <xsd:complexType\>
    <xsd:sequence\>
      <xsd:element ref="my:ObjectDataSource" minOccurs="0" maxOccurs="32"/>
      <xsd:element ref="my:XmlDataSource" minOccurs="0" maxOccurs="32"/>
      <xsd:element ref="my:Panel"/>
      <xsd:element ref="my:Events" minOccurs="0" maxOccurs="1"/>
    </xsd:sequence>
    <xsd:attribute ref="my:TypeName"/>
    <xsd:anyAttribute processContents="lax" namespace="http://www.w3.org/XML/1998/namespace"/>
  </xsd:complexType>
</xsd:element>
```



Элемент **ObjectControlConfiguration** содержит следующие компоненты.

1.  **ObjectDataSource**: этот элемент определяет атрибут TypeName для класса источника данных, используемого элементом управления ресурса (RC). Описание и определение схемы см. в разделе "Источники данных" этого документа. Элемент **ObjectControlConfiguration** может содержать до 32 узлов элемента **ObjectDataSource**.

2.  **XmlDataSource**: это простой источник данных. Чаще всего он используется, чтобы определить макет страницы сводки. Описание и определение схемы см. в разделе "Источники данных" этого документа. Элемент **ObjectControlConfiguration** может содержать до 32 узлов элемента **XmlDataSource**.

3.  **Panel**: администратор может настроить макет страницы RCDC, изменив элементы, содержащиеся в элементах Panel. Дополнительные сведения см. в разделе "Элемент Panel" этого документа. Элемент **ObjectControlConfiguration** должен содержать только один элемент Panel.

4.  **Event**: администраторы не могут добавлять настраиваемый код программной части, так как эта функция ограничена. Это событие, которое генерируется панелью или элементом управления в результате изменения состояния. Дополнительные сведения см. в разделе "Элемент Event" этого документа. Элемент **ObjectControlConfiguration** может при необходимости содержать один элемент **Event**. В целом настраиваемые элементы **Event** не поддерживаются, если эта возможность не добавлена специально в рамках последующей оптимизации.

## <a name="data-sources"></a>Источники данных

Microsoft Identity Manager использует источники данных, чтобы привязывать данные к компонентам пользовательского интерфейса. Это помогает разделить данные и уровень их представления. Есть два типа источников данных для конфигурации ресурса RCDC: **ObjectDataSource** и **XmlDataSource**.

-   Источники **ObjectDataSource** определяют класс Microsoft .NET, который предоставляет данные для RC. Есть фиксированный набор доступных типов ObjectDataSource, которые администратор может по выбору использовать при создании RCDC.

-   Источники **XMLDataSource** обеспечивают простой способ структурирования XML-данных. Они могут использоваться администраторами для предоставления настраиваемых данных. XML-данные нужно указать непосредственно в RCDC, если вы не используете встроенную предопределенную структуру XML. Встроенная XML-структура используется для создания страниц сводки в RC.

В RCDC эти источники данных можно привязать к атрибутам элементов управления пользовательского интерфейса, которые определены в RCDC для создания пользовательского интерфейса.

### <a name="objectdatasource"></a>ObjectDataSource

В таблице ниже описаны общие типы источников данных,которые предоставляет Microsoft Identity Manager. Они доступны для всех типов ресурсов (если не указано иное).

| TypeName                        | Описание     | Поддерживает двустороннюю привязку | Поддерживаемый синтаксис привязки        |
|----------------|-----------|-------------------------|--------------|
| PrimaryResourceObjectDataSource | Представляет ресурс FIM 2010, который создается, изменяется или просматривается. Путь в строке привязки является именем атрибута. Обратите внимание, что тип ресурса указывается в атрибуте RCDC TargetObjectType, а не в атрибуте RCDC.ConfigurationData. | Да                     | [AttributeName]: значение атрибута объекта, заданное в соответствии с его именем.    |
| PrimaryResourceDeltaDataSource  | Этот источник данных создает XML-файл изменений для сравнения исходного и текущего состояние ресурса FIM 2010. Созданный XML-файл изменений используется элементом управления сводки RC, чтобы преобразовать пользовательский интерфейс для просмотра в соответствии с запросом, отправляемым пользователем.                                    | Нет                      | DeltaXml: </br> используется вместе с элементом управления сводки для отображения разницы в значениях.                                                 |
| PrimaryResourceRightsDataSource | Этот источник данных предоставляет встроенные права для каждого атрибута ресурса FIM 2010. Это позволяет RC до отправки определить разрешения пользователя для конкретного атрибута и соответствующим образом преобразовать его пользовательский интерфейс для просмотра.                     | Нет                      | [AttributeName]                                                                                         |
| SchemaDataSource                | Этот источник данных предоставляет доступ к информации, связанной со схемами, включая отображаемое имя и описание, а также тип ресурса. Кроме того, предоставляется доступ к сведениям о том, является ли атрибут обязательным.                                                                                             | Нет                      | [AttributeName].**Required**: логическое значение, указывающее, является ли значение атрибута обязательным. <br/> [AttributeName].**DisplayNameString**: значение, указывающее отображаемое имя привязки. <br/>[AttributeName].**DescriptionString**: значение, указывающее описание привязки. <br/>[AttributeName].StringRegexString: значение, указывающее регулярное выражение строки для привязки. <br/>[AttributeName].**DisplayName** <br/> [AttributeName].**Description** <br/> [AttributeName]. [AttributeName].**IntergerValueMinimum** <br/>[AttributeName].**IntergerValueMaximum** <br/>[AttributeName].**LocalizedAllowedValues**|
| DomainDataSource                | Этот источник данных предоставляет перечисление доменов, исходя из ресурсов конфигурации домена. Обратите внимание, что этот источник данных можно использовать только в RCDC для ресурсов групп и пользователей.                                                                           | Да                     | Домен           |

Ниже приведен фрагмент RCDC, который привязывает три источника данных к элементу управления UocTextBox, чтобы изменить атрибут Description для группы.

```XML
<my:ObjectDataSource my:TypeName="PrimaryResourceObjectDataSource" my:Name="object" my:Parameters=""/>
<my:ObjectDataSource my:TypeName="SchemaDataSource" my:Name="schema"/>
<my:ObjectDataSource my:TypeName="PrimaryResourceRightsDataSource" my:Name="rights"/>

     <my:Control my:Name="Description" my:TypeName="UocTextBox" my:Caption="{Binding Source=schema, Path=Description.DisplayName}" my:RightsLevel="{Binding Source=rights, Path=Description}">
          <my:Properties>
               <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=DisplayName.Required}"/>
               <my:Property my:Name="Rows" my:Value="3"/>
               <my:Property my:Name="Columns" my:Value="60"/>
               <my:Property my:Name="MaxLength" my:Value="450"/>
               <my:Property my:Name="Text" my:Value="{Binding Source=object, Path=Description, Mode=TwoWay}"/>
          </my:Properties>
     </my:Control>
```

### <a name="xmldatasource"></a>XMLDataSource

С помощью **XMLDataSource** можно указать пользовательские данные, которые RCDC будет использовать для определенного ресурса. В этом случае в RCDC нужно указать XML-данные. Кроме того, этот источник данных можно использовать для обращения к встроенной структуру XML-данных, чтобы преобразовать пользовательский интерфейс страниц сводки для просмотра. Вы можете управлять типом используемого источника **XMLDataSource**, определив его в RCDC.


| TypeName                 | Описание   | | |
|--------------------------|------------|
| **XMLDataSource**            | Источник данных представляет XML-данные в формате XSL или внедренного XSL. <br/>**Формат XSL:** <br/> Microsoft.IdentityManagement.WebUI.Controls.dll<my:XmlDataSource my:Name=" <br/>summaryTransformXsl"my:Parameters=”Microsoft.IdentityManagement.WebUI.Controls.Resources.DefaultSummary.xsl”> </my:XmlDataSource><br/> **Формат внедренного XSL:** <br/> <my:XmlDataSource my:Name="RequestStatusTransformXsl"> <br/> <xsl:stylesheet version="1.0" xmlns:xsl=http://www.w3.org/1999/XSL/Transform <br/> xmlns:msxsl="urn:schemas-microsoft-com:xslt"><br/></xsl:stylesheet></my:XmlDataSource>                       |Нет | ```Xpath[;namespaces]``` <br/> Where:Xpath — это допустимое XML-выражение xpath для выбора необходимой заметки, чаще всего — "/" (корневой каталог). <br/>Пространства имен — это необязательный список строк prefix=URI, разделенных точкой с запятой, которые используются, чтобы выражение xpath выполнялось в соответствии с XML с пространством имен. |
| **ReferenceDeltaDataSource** | Источник данных представляет разницу в значениях многозначных ссылочных атрибутов. Он используется только в RCDC для группы и набора. <br/> Источник данных не ограничивается группами или наборами, но для отправки значения этой разницы требуется изменить код в узле RCDC. Сейчас этот источник данных распознают только узлы группы и набора.  | Да                      | [AttributeName].Add: [AttributeName] представляет ссылочный атрибут; возвращаются данные добавления для разницы в значениях. <br/> Пример: [ReferenceAttribute].Add <br/>Пример: ```<my:Property my:Name="Value" my:Value="{Binding Source=delta, Path=ExplicitMember.Add, Mode=TwoWay}" />``` <br/>[AttributeName].Remove: [AttributeName] представляет ссылочный атрибут; возвращаются данные удаления для разницы в значениях. <br/> DeltaXml |
|**RequestDetailsDataSource**| Источник данных представляет атрибут RequestParameter для объектов Request. Параметр определяет максимальное число значений, отображаемых для многозначных атрибутов. Используется только в RCDC для запроса. ```<my:ObjectDataSource my:TypeName="RequestDetailsDataSource" my:Name="requestDetails" my:Parameters="1000" />```| Нет | DeltaXml |
|**RequestStatusDataSource**| Источник данных представляет атрибут **RequestStatusDetails** для объектов Request. <br/>Он используется только в RCDC для запроса.  | Нет | DeltaXml |

-   Определение пользовательского источника данных XML:

 ```XML
   <my:XmlDataSource my:Name="MyCustomData" >
   %Insert custom, properly formatted XML data here%
   </my:XmlDataSource>
   ```

-   Чтобы использовать XSL встроенного элемента управления сводки, определите источник данных следующим образом:

```XML
<my:XmlDataSource my:Name="summaryTransformXsl" my:Parameters="Microsoft.IdentityManagement.WebUI.Controls.Resources.DefaultSummary.xsl" />
```

 Если вы создаете RCDC для типа настраиваемого ресурса, этот метод можно использовать, чтобы страница сводки ресурса автоматически преобразовывалась для просмотра.

Пример создания вкладки со сводкой в RCDC с использованием PrimaryResourceDeltaDataSource с XMLDataSource и встроенного кода XSL:

```XML
<my:ObjectDataSource my:TypeName="PrimaryResourceDeltaDataSource" my:Name="delta" />
<my:XmlDataSource my:Name="summaryTransformXsl" my:Parameters="Microsoft.IdentityManagement.WebUI.Controls.Resources.DefaultSummary.xsl" />

<my:Grouping my:Name="summaryGroup" my:Caption="Summary” my:IsSummary="true">
     <my:Control my:Name="summaryControl" my:TypeName="UocHtmlSummary" my:ExpandArea="true">
          <my:Properties>
               <my:Property my:Name="ModificationsXml" my:Value="{Binding Source=delta, Path=DeltaXml}" />
              <my:Property my:Name="TransformXsl" my:Value="{Binding Source=summaryTransformXsl, Path=/}" />
          </my:Properties>
     </my:Control>
</my:Grouping>
```

Кроме того, пользователь может заменить элемент XmlDataSource, указанный ранее, используя следующий формат, чтобы определить настраиваемый макет для страницы сводки. Для справки см. XSL-код сводки по умолчанию FIM 2010, представленный в приложении B этого документа.

```XML
<my:XmlDataSource my:Name="summaryTransformXsl">
     Insert valid XSL code here
</my:XmlDataSource>
```
### <a name="schema-for-data-sources"></a>Схема для источников данных
Ниже приведены схемы XSD для двух типов источников данных:

```XML
<xsd:element name="ObjectDataSource">
     <xsd:complexType>
          <xsd:sequence/>
          <xsd:attribute ref="my:TypeName"/>
          <xsd:attribute ref="my:Name"/>
          <xsd:attribute ref="my:Parameters"/>
     </xsd:complexType>
</xsd:element>
<xsd:element name="XmlDataSource">
     <xsd:complexType  mixed="true">
          <xsd:sequence>
              <xsd:any minOccurs="0" maxOccurs="unbounded" processContents="lax"/>
          </xsd:sequence>
          <xsd:attribute ref="my:Name"/>
          <xsd:attribute ref="my:Parameters"/>
    </xsd:complexType>
</xsd:element>
```

## <a name="events"></a>Элемент Event
Элемент Event определяет изменение состояния для элемента Control. Расширяемость этого элемента ограничена, так как нельзя написать пользовательскую функцию (обработчик), чтобы определить поведение после активации события. Один и тот же элемент Event можно использовать в элементе Panel. Дополнительные сведения см. в разделе "Элемент Panel" этого документа. Ниже приведена схема XSD для элемента Event:

```XML
<xsd:element name="Events">
     <xsd:complexType>
          <xsd:sequence>
               <xsd:element ref="my:Event" minOccurs="1" maxOccurs="16"/>
          </xsd:sequence>
     </xsd:complexType>
</xsd:element>
<xsd:element name="Event">
     xsd:complexType>
          <xsd:simpleContent>
               <xsd:extension base="xsd:string">
                    xsd:attribute ref="my:Name"/>
                    <xsd:attribute ref="my:Handler"/>
               </xsd:extension>
          </xsd:simpleContent>
     </xsd:complexType>
     </xsd:element>
```


Event — это пустой элемент, который имеет два атрибута.

**Атрибуты:**

1.  **Name**: это уникальное имя события. В **ObjectControlConfiguration** поддерживается только событие Load. Это событие активируется при первой загрузке страницы.

2.  **Handler**: это уникальное имя обработчика события. При активации события обычно вызывается программный метод, обрабатывающий изменение состояния для элемента управления. Не поддерживаются следующие сценарии: удаление существующего обработчика из существующего элемента управления, создание обработчика и его присоединение к существующему или новому элементу управления.

Пример:

Ниже приведен пример элемента Event.
```XML
<my:Events>
    <my:Event my:Name="Load" my:Handler="OnLoad"/>
</my:Events>
```

**Panel**


Panel — это основной элемент в макете RCDC. Ниже приведена схема XSD для элемента Panel.

```XML
<xsd:element name="Panel">
     <xsd:complexType>
          <xsd:sequence>
               <xsd:element ref="my:Grouping" minOccurs="1" maxOccurs="16"/>
          </xsd:sequence>
          <xsd:attribute ref="my:Name"/>
          <xsd:attribute ref="my:DisplayAsWizard"/>
          <xsd:attribute ref="my:Caption"/>
          <xsd:attribute ref="my:AutoValidate"/>
     </xsd:complexType>
</xsd:element>
```

Этот элемент содержит повторяющийся элемент — Grouping. Дополнительные сведения см. в разделе "Элемент Grouping" этого документа.

Элемент Panel содержит четыре атрибута.

1.  **Name**: имя панели. Это обязательный атрибут строкового типа.

2.  **DisplayAsWizard**: сейчас не рекомендуется использовать этот атрибут. Режимы мастера или вкладки для макета определяет в RCDC соответствующий атрибут VerbContext. Если свойство имеет значение 0 (режим создания), используется режим мастера. В других случаях используется режим вкладки. Дополнительные сведения см. в статье "Introduction to Configuring and Customizing the FIM Portal" (Общие сведения о конфигурации и настройке портала FIM).

3.  **Caption**: сейчас не рекомендуется использовать этот атрибут. Пользователь может указать заголовки для страницы, включив элемент Group, содержащий только сведения о заголовках. Дополнительные сведения см. в разделе "Элемент Grouping" этого документа.

4.  **AutoValidate**: это необязательный логический атрибут. Если задано значение true, для каждого элемента управления на текущей вкладке активируется проверка. Если атрибут отсутствует, по умолчанию устанавливается значение true. Атрибут можно использовать в сочетании со свойством RegularExpression. Дополнительные сведения см. в описании свойства RegularExpression в этом документе.

## <a name="grouping"></a>Элемент Grouping

Элемент Grouping определяет общий макет элемента Panel. Он используется как контейнер, который группирует отдельные элементы управления в различных разделах и вкладках. Ниже приведена схема XSD для элемента Grouping.

```XML
<xsd:element name="Grouping">
     <xsd:complexType>
          <xsd:sequence>
               <xsd:element ref="my:Help" minOccurs="0"  maxOccurs="1"/>
               <xsd:element ref="my:Control" minOccurs="1" maxOccurs="256"/>
               <xsd:element ref="my:Events" minOccurs="0" maxOccurs="1"/>
          </xsd:sequence>
          <xsd:attribute ref="my:Name"/>
          <xsd:attribute ref="my:Caption"/>
          <xsd:attribute ref="my:Description"/>
          <xsd:attribute ref="my:Enabled"/>
          <xsd:attribute ref="my:Visible"/>
          <xsd:attribute ref="my:IsHeader"/>
          <xsd:attribute ref="my:IsSummary"/>
     </xsd:complexType>
</xsd:element>
```


Есть три типа элементов **Grouping**:

1.  **Header Grouping**: это необязательный элемент. В элементе **Panel** можно использовать только один элемент Header Grouping. Этот элемент отображается в верхней части панели как заголовок.
    Для него можно использовать только один элемент UocCaptionControl. Пример элемента Header Grouping см. в разделе "Пример".

2.  **Content Groupings**: требуется по крайней мере один такой элемент. В элементе Panel можно использовать несколько таких элементов. Элемент Content Grouping отображается как основное содержимое страницы RCDC. Каждый такой элемент отображается как вкладка на одной и той же панели. Он может содержать от 1 до 256 элементов управления. Пример элемента **Content Grouping** см. в разделе "Пример".

3.  **Summary Groupings**: необязательный элемент. В элементе Panel можно использовать только один такой элемент. Элемент Summary Grouping отображается как последняя вкладка на панели. Для этого элемента можно использовать только один элемент **UocHtmlSummary**. Он позволяет отобразить изменения, внесенные пользователем перед отправкой запроса. Пример элемента Summary Grouping см. в разделе "Пример".

Элемент Grouping каждого типа содержит следующие элементы.

1.  **Help**: этот элемент предоставляет текст справки на вкладке. Также его можно использовать, чтобы добавить ссылку на файл справки для вкладки.

2.  **Controls**: сведения об этом элементе см. в разделе "Элемент Control" этого документа. Каждый группирующий элемент должен содержать от 1 до 256 элементов управления включительно. Число зависит от типа группирующего элемента.

3.  **Event**: сведения об этом элементе см. в разделе "Элемент Event" этого документа. Для каждого группирующего элемента можно использовать один элемент Event (необязательно). Ниже перечислены элементы Event, которые поддерживаются элементом Grouping.

    - **BeforeLeave**: это событие активируется, когда пользователь собирается закрыть вкладку группирующего элемента содержимого.
    - **AfterEnter**: это событие активируется, когда пользователь собирается открыть вкладку группирующего элемента содержимого.

Атрибуты:

1.  **Name**: обязательное имя элемента Grouping. Атрибут **Name** должен быть уникальным в пределах элемента **Panel**.

2.  **Caption**: элемент **Caption** отображается как текст заголовка в элементе Header Grouping. Он отображается как заголовок вкладки для группирующего элемента Content Grouping или Summary Grouping.

3.  **Description**: необязательный строковый атрибут. **Description** применяется только к элементу Content Grouping. Используйте этот элемент, чтобы предоставить пользователю некоторые сведения о данных в пределах вкладки.

  >[!NOTE]
  Если этот атрибут используется для элемента Summary Grouping, код XML считается недопустимым. Если этот атрибут используется для элемента Header Grouping, код XML считается допустимым, но игнорируется.

4.  **Enabled**: необязательный логический атрибут. Если он отсутствует, задается значение true. Если задано значение false, для пользователя отображается вкладка в состоянии "Отключено". Этот атрибут применяется только к элементу Content Grouping.

  >[!NOTE]
  Если этот атрибут используется для элемента Summary Grouping, код XML считается недопустимым. Если этот атрибут используется для элемента Header Grouping, код XML считается допустимым, но игнорируется.

5.  **Visible**: вы можете скрыть вкладку страницы RCDC или ее заголовок, задав для этого атрибута значение false. По умолчанию для этого необязательного атрибута логического типа задано значение true. Этот атрибут применяется только к элементу Content Grouping.

  >[!NOTE]
  Если в элементе Panel используется только один элемент Content Grouping, эта функция не работает. Если в элементе Panel используется несколько элементов Content Grouping, поведение функции аналогично описанному выше.

6.  **IsHeader**: это необязательный логический атрибут, который определяет, принадлежит ли элемент Grouping к типу Header Grouping. Если этот атрибут не указан, задается значение false.

7.  **IsSummary**: это необязательный логический атрибут, который определяет, принадлежит ли элемент Grouping к типу Summary Grouping. Если этот атрибут не указан, задается значение false.

![XML конфигурации RCD](media/rcd-configuration-xml-reference/image005.jpg)

В примере кода XML ниже создается элемент Header Grouping, представленный выше. Элемент Header Grouping — это область с текстом "Sample Header Grouping".

```XML
<!--Sample for a Header Grouping-->
<my:Grouping my:Name="HeaderGroupingSample" my:IsHeader="true">
     <my:Control my:Name="SampleHeaderCaption" my:TypeName="UocCaptionControl" my:ExpandArea="true" my:Caption="Sample Header Grouping">
          <my:Properties>
               <my:Property my:Name="MaxHeight" my:Value="32"/>
               <my:Property my:Name="MaxWidth" my:Value="32"/>
          </my:Properties>
      </my:Control>
</my:Grouping>
<!--End of Header Grouping Sample-->
```

![XML конфигурации RCD](media\rcd-configuration-xml-reference/image007.jpg)

В примере кода XML ниже создается элемент Content Grouping, представленный выше. Элемент Content Grouping — это крайняя вкладка слева с текстом **Sample Content Grouping**.

```XML
<!--Sample for a Content Grouping-->
<my:Grouping my:Name="ContentGroupingSample" my:Caption="Sample Content Grouping" my:Description="Some description for content grouping">
     <my:Control my:Name="DisplayName" my:TypeName="UocTextBox" my:Caption="Display name" my:Description="This is the display name of the set.">
          <my:Properties>
               <my:Property my:Name="Required" my:Value="True"/>
               <my:Property my:Name="MaxLength" my:Value="128"/>
               <my:Property my:Name="Text" my:Value="{Binding Source=object, Path=DisplayName, Mode=TwoWay}"/>
          </my:Properties>
     </my:Control>
</my:Grouping>
<!--End of Content Grouping Sample-->
```

![XML конфигурации RCD](media/rcd-configuration-xml-reference/image010.jpg)

В примере кода XML ниже создается элемент Summary Grouping, представленный выше. Элемент Summary Grouping — это крайняя вкладка справа с текстом **Summary**.

```XML
<!--Sample for a Summary Grouping-->
<my:Grouping my:Name="Summary" my:Caption="Sample Summary Grouping" my:IsSummary="true">
     <my:Control my:Name="SummaryControl" my:TypeName="UocHtmlSummary" my:ExpandArea="true">
          <my:Properties>
               <my:Property my:Name="ModificationsXml" my:Value="{Binding Source=delta, Path=DeltaXml}"/>
               <my:Property my:Name="TransformXsl" my:Value="{Binding Source=summaryTransformXsl, Path=/}"/>
          </my:Properties>
     </my:Control>
</my:Grouping>
<!--End of Summary Grouping Sample-->
```
### <a name="help"></a>Справка

При необходимости в элемент Grouping или Control можно включить элемент Help. В элементе Grouping нужно использовать этот элемент первым. Это текстовая справка для пользователей, предоставляющая точные сведения. Ниже приведена схема XSD для элемента Help:

```XML
<xsd:element name="Help">
     <xsd:complexType>
          <xsd:sequence/>
          <xsd:attribute ref="my:HelpText"/>
          <xsd:attribute ref="my:Link"/>
     </xsd:complexType>
</xsd:element>
```
Ниже приведен пример элемента Help:
```XML
<my:Help my:HelpText="Some Help Text for Group Basic Info" my:Link="03e258a0-609b-44f4-8417-4defdb6cb5e9.htm#bkmk_grouping_GroupingBasicInfo" />
```

### <a name="control"></a>Элемент Control

Элемент Grouping содержит один или несколько элементов Control. Элементы Control — основные элементы в RCDC. Элемент Grouping можно настроить, определив различные элементы Control, которые в нем содержатся. Ниже приведена схема XSD для элемента Control:

```XML
<xsd:element name="Control">
     <xsd:complexType>
          <xsd:sequence>
               <xsd:element ref="my:Help" minOccurs="0"  maxOccurs="1"/>
               <xsd:element ref="my:CustomProperties" minOccurs="0"  maxOccurs="1"/>
               <xsd:element ref="my:Options" minOccurs="0"  maxOccurs="1"/>
               <xsd:element ref="my:Buttons" minOccurs="0"  maxOccurs="1"/>
               <xsd:element ref="my:Properties" minOccurs="0"  maxOccurs="1"/>
               <xsd:element ref="my:Events" minOccurs="0" maxOccurs="1"/>
          </xsd:sequence>
          <xsd:attribute ref="my:Name"/>
          <xsd:attribute ref="my:TypeName"/>
          <xsd:attribute ref="my:Caption"/>
          <xsd:attribute ref="my:Enabled"/>
          <xsd:attribute ref="my:Visible"/>
          <xsd:attribute ref="my:Description"/>
          <xsd:attribute ref="my:ExpandArea"/>
          <xsd:attribute ref="my:Hint"/>
          <xsd:attribute ref="my:AutoPostback"/>
          <xsd:attribute ref="my:RightsLevel"/>
     </xsd:complexType>
</xsd:element>
```

Элемент Control содержит следующие элементы.

1.  **Help**: этот элемент игнорируется. Он работает только в элементе Grouping.

2.  **CustomProperties**: этот элемент не поддерживается.

3.  **Options**: этот элемент используется только в сочетании с элементами Control **UocDropDownList** или **UocRadioButtonList**. Он не работает с другими элементами Control. Структуру этого элемента см. в разделе "Элемент Options" этого документа. Особенности его использования с элементом Control см. в разделе "Отдельные элементы управления" этого документа.

4.  **Buttons**: этот элемент используется только в сочетании с элементом Control **UocListView**. Он не работает для других элементов управления. Дополнительные сведения см. в разделе "Элемент управления UocListView" этого документа.

5.  Properties: этот элемент используется во всех элементах Control для определения дополнительных особенностей их поведения. Сведения об этом элементе см. в разделе "Элемент Properties" этого документа.

6.  **Event**: структура этого элемента описана в разделе "Элемент Event" этого документа. Ознакомьтесь с определениями отдельных элементов Control, чтобы определить, какие для них используются события.

Элемент Control содержит следующие атрибуты.

1.  **Name**: это имя элемента Control. Имя элемента Control должно быть уникальным в пределах каждой панели. Это обязательный атрибут строкового типа.

2.  **TypeName**: этот атрибут указывает тип элемента Control. Это обязательный атрибут строкового типа. Имена каждого элемента управления см. в разделе "Отдельные элементы управления".

3.  **Caption**: этот атрибут позволяет включить заголовок для элемента управления.
    Заголовок обычно представлен отображаемым именем данных, для отображения или ввода которых используется этот элемент управления. Можно явно указать значение для заголовка или связать его с отображаемым именем для атрибута схемы. Заголовок отображается в крайней левой части элемента управления стандартного размера. Если элемент управления развернут во весь экран, заголовок отображается над ним. Это необязательный атрибут строкового типа. Сведения о том, как привязать источник данных к значению атрибута или свойства см. в разделе "Элемент Property".

   В примере ниже показано, как использовать заголовок явным образом.

   ```XML
      <my:Control my:Name="ExplicitAlias" my:TypeName="UocTextBox" my:Caption="Explicit Alias">…<my:Control/>
   ```
     В примере ниже показано, как использовать заголовок с источником данных. Если вы использовали шаблон для источника данных, описанного выше, такой источник является схемой. Рекомендуем привязать атрибут DisplayName к атрибуту Caption.

    ```XML
    <my:Control my:Name="DynamicAlias" my:TypeName="UocTextBox" my:Caption="{Binding Source=schema, Path=Alias.DisplayName, Mode=OneWay}">…<my:Control/>
    ```
4.  Enabled: это необязательный атрибут логического типа. Установив для этого атрибута значение false, пользователь может отключить элемент Control. По умолчанию задано значение true.

5.  Visible: это необязательный атрибут логического типа. Его можно использовать для скрытия всего элемента управления. По умолчанию задано значение true.

6.  Description: это необязательный атрибут строкового типа. Он позволяет включить описание, которое поможет пользователю понять, что нужно поместить в элемент управления и какие функции он выполняет. Можно явно указать значение для описания или связать его с данными описания для атрибута схемы. <br/>Элемент Description отображается в крайней левой части элемента управления стандартного размера под заголовком. Если элемент управления развернут во весь экран, описание отображается в верхней части элемента управления под заголовком. Сведения о том, как привязать источник данных к атрибуту или значению свойства см. в разделе "Элемент Property" этого документа.

7.  В следующем примере показано, как использовать элемент Description явным образом:
  ```XML
  <my:Control my:Name="ExplicitAlias" my:TypeName="UocTextBox" my:Caption="Explicit Alias" my:Description="This is explicit description.">…<my:Control/>
  ```
  В примере показано, как использовать элемент Description с источником данных. Если вы использовали шаблон для источника данных, описанного выше, такой источник является **схемой**. Рекомендуем привязать элемент **Description** к атрибуту Description.
  ```XML
  <my:Control my:Name="DynamicAlias" my:TypeName="UocTextBox" my:Caption="{Binding Source=schema, Path=Alias.DisplayName, Mode=OneWay}" my:Description="{Binding Source=schema, Path=Alias.Description, Mode=OneWay}">…<my:Control/>
  ````
8. ExpandArea: этот атрибут указывает, развернут ли элемент управления во весь экран. Это необязательный атрибут логического типа. По умолчанию задано значение false.

    >[!NOTE]
    Если для этого атрибута задано значение true, атрибуты Caption и Description отключены. Чтобы добавить заголовок для развернутого элемента управления, используйте элемент управления UocLabel.
9. **Hint**: это необязательный атрибут строкового типа. Текст в атрибуте Hint помогает пользователю понять, какие входные данные допустимы для элемента управления. Атрибут Hint отображается под элементом управления.

10.  **AutoPostback**: это необязательный атрибут логического типа. Значение по умолчанию — false. Если задано значение false, при обновлении страницы элемент управления не обновляется. Сведения об AutoPostback см. в описании свойства элемента управления пользовательского интерфейса Microsoft ASP.NET с тем же именем.

11. **RightsLevel**: это необязательный атрибут строкового типа. Этот атрибут можно связать с источником данных только со встроенными правами. Этот элемент управления динамически включен или отключен в зависимости от прав пользователя. Сведения о том, как привязать источники данных к значению атрибута или свойства см. в разделе "Элемент Property" этого документа.

    В примере показано, как использовать атрибут **RightsLevel** с источником данных. Если вы использовали шаблон для источника данных, описанного выше, такой источник является набором **прав**. Используйте имя атрибута в качестве пути.

### <a name="properties"></a>Элемент Property

Элемент Property можно использовать для дальнейшей настройки поведения каждого элемента управления. Property является пустым элементом. Ниже приведена схема XSD для элемента Property.
```XML
<xsd:element name="Properties">
     <xsd:complexType>
          <xsd:sequence>
               <xsd:element ref="my:Property" minOccurs="1" maxOccurs="32"/>
          </xsd:sequence>
     </xsd:complexType>
</xsd:element>
<xsd:element name="Property">
     <xsd:complexType>
          <xsd:simpleContent>
               <xsd:extension base="xsd:string">
                    <xsd:attribute ref="my:Name"/>
                    <xsd:attribute ref="my:Value"/>
               </xsd:extension>
          </xsd:simpleContent>
     </xsd:complexType>
</xsd:element>
```



Для каждого элемента Property используется два обязательных атрибута:

1.  **Name**: этот атрибут строкового типа является уникальным именем элемента Property.
    Различные элементы управления имеют разные свойства. Есть некоторые общие свойства, которые могут использоваться для всех элементов управления. Дополнительные сведения доступных для определенного элемента управления именах см. в разделах "Общие свойства" и "Отдельные элементы управления".

2.  **Value**: это значение элемента Property. Тип данных значения зависит от того, какому свойству они присвоены. Разрешенный формат значений для определенных свойств см. в следующем разделе.

Некоторые элементы Property можно привязать к информации из источника данных. Для этого нужно использовать указанный ниже формат строки. Сведения о том, как привязать отдельные свойства к источнику данных, см. в разделе "Отдельные элементы управления".

```
<my:Property my:Name="Required" my:Value="[Formatted String]"/>

Formatted String :=  “{Binding “ + [SourceExpression] + “,” + [PathExpression] + “,” + [ModeExpression]? + “}”

SourceExpression:= “Source=” + [ObjectDataSourceName]

PathExpression:= “Path=” + [AttributeName]|[AttributePropertyName]

ModeExpression:= “Mode=” + [ModeChoice]

ModeChoice:= “OneWay”|”TwoWay”

ObjectDataSourceName:= The value of any string assign to node /ObjectControlConfiguration/ObjectDataSource/Name.

AttributeName:= valid schema attribute name from the data source.

AttributePropertyName:= valid property name of a schema attribute from the data source.

````
**ПРИМЕР:**

```XML
<my:Property my:Name="Text" my:Value="{Binding Source=object, Path=DisplayName, Mode=TwoWay}"/>
<my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=DisplayName.Required}"/>

```



<a name="common-properties"></a>Общие свойства
-----------------

Все элементы управления RCDC, указанные в этом документе, могут иметь описанные ниже общие свойства. Можно использовать эти свойства, определяемые элементами Property, в сочетании с другими, характерными для различных элементов управления.

1.  Required: это свойство указывает, является ли поле обязательным. В обязательном поле необходимо указать значение. Для строкового ввода пустое значение не поддерживается. Необязательное поле может быть пустым. Если поле является обязательным и в нем не указано значение, в верхней части элемента управления для ввода отобразится сообщение об ошибке. Вы можете явно указать, является ли поле обязательным. Кроме того, можно привязать поле к информации схемы с определенной привязкой между атрибутом и типом ресурса. Если это свойство отсутствует, элемент управления ввода по умолчанию является необязательным.

   Ниже приведен пример применения явного значения для этого свойства:

    ```XML
    <my:Property my:Name="Required" my:Value="True"/>
    ```
   В примере используется источник динамических данных для этого свойства. Если вы использовали шаблон для источника данных, описанного выше, такой источник является схемой. В качестве пути используйте \<имя атрибута\>.Required.

    ```XML
    <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=DisplayName.Required}"/>
    ```
2. **ReadOnly**: если задать для этого свойства значение true, пользователь может получить доступ к элементу управления только для чтения. Это необязательный атрибут логического типа.
    По умолчанию задано значение false. Но иногда поведение этого свойства перезаписывается типом прав пользователя для привязки данных к элементу управления. Например, если у пользователя нет прав обновлять поле, а поле привязано к встроенным правам, такой пользователь может просматривать данные в режиме только для чтения, даже если для этого свойства задано значение false.

3.  **RegularExpression**: это свойство определяет ограничения значения в элементе управления. Значение этого свойства представлены в форматах, поддерживаемых в стандарте .NET StringRegex. Дополнительные сведения см. в статье [.NET Framework Regular Expressions](http://go.microsoft.com/fwlink/?LinkId=165361) (Регулярные выражения в .NET Framework). Если элемент управления используется для ввода значения, значение проверяется по ограничению, указанному в этом свойстве, когда пользователь пытается покинуть текущую страницу.
    Сообщение об ошибке отображается в верхней части элемента управления, который содержит недопустимые входные данные. Пользователь может явно указать строковое регулярное выражение. Пользователь также может привязать его к информации схемы для определенного атрибута. По умолчанию, если это свойство отсутствует, элемент управления не проверяет входные строки в соответствии с ограничениями.
    Ниже приведен пример применения явного значения для этого свойства:

    ```XML
    <my:Property my:Name="RegularExpression" my:Value="[A-Z]*"/>
    ```
    В примере используется источник динамических данных для этого свойства. Если вы использовали шаблон для источника данных, описанного выше, такой источник является схемой. Для элемента Path используйте <attribute name>.StringRegex.
    ```XML
    <my:Property my:Name="RegularExpression" my:Value="{Binding Source=schema, Path=Alias.StringRegex, Mode=OneWay}"/>
    ```
4.  Visible: это необязательный атрибут логического типа. Его можно использовать для скрытия всего элемента управления. По умолчанию задано значение true.

### <a name="options"></a>Элемент Options

Элемент Options включает один или несколько подузлов параметров. Он используется только в сочетании с элементами управления UocRadioButtonList и UocDropDownList. Дополнительные сведения об их использовании см. в разделе "Отдельные элементы управления". Ниже приведена схема XSD для элемента Options.

```XML
<xsd:element name="Options">
     <xsd:complexType>
          <xsd:sequence>
               <xsd:element ref="my:Option" minOccurs="0" maxOccurs="unbounded"/>
          </xsd:sequence>
     </xsd:complexType>
</xsd:element>
<xsd:element name="Option">
     <xsd:complexType>
          <xsd:simpleContent>
               <xsd:extension base="xsd:string">
                    <xsd:attribute ref="my:Value"/>
                    <xsd:attribute ref="my:Caption"/>
                    <xsd:attribute ref="my:Hint"/>
               </xsd:extension>
          </xsd:simpleContent>
     </xsd:complexType>
</xsd:element>
```


Атрибуты:

1.  Value: это обязательный атрибут строкового типа. Значение атрибута должно быть уникальным в пределах одного элемента управления. Можно использовать символы без учета регистра и только от A до Z.

2.  Caption: этот обязательный атрибут является отображаемым именем каждого элемента Option.

3.  Hint: это необязательный атрибут. Он позволяет предоставлять пользователю дополнительные сведения и указания.

### <a name="environment-variables"></a>Переменные среды

В таблице ниже приведены переменные среды, которые можно использовать в любой конфигурации RCDC.

| Переменная | description |
|--------|--------|
| `<LoginID>`       | Отображает ИД вошедшего пользователя.           |
| `<LoginDomain>`   | Отображает домен вошедшего пользователя.       |
| `<Today>  `       | Отображает текущую дату и время.                                |
| `<FromToday_nnn>` | Отображает текущую дату, nnn и время. nnn — целое число.  |
| `<ObjectID> `     | ИД первичного ресурса RCDC.                                     |
| `<Attribute_xxx>` | Возвращает указанный атрибут (xxx) первичного ресурса RCDC. |

### <a name="debugging-xml-configuration-files"></a>Отладка XML-файлов конфигурации


При разработке или изменении XML-файлов конфигурации для RCDC можно снизить число ошибок, проверив XML в соответствии с XSD-файлами с помощью редактора, например Microsoft Visual Studio®. Дополнительные сведения см. в статье [An Introduction to the XML Tools in Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkID=74512) (Общие сведения о средствах XML в Visual Studio 2005).

### <a name="customizing-a-help-file"></a>Настройка файла справки

Если вы создаете ресурсы и атрибуты, возможно, вам потребуется обновить существующие файлы справки на портале FIM, добавив содержимое для настроенных ресурсов. Файлы справки на портале FIM представлены в формате HTM и могут быть изменены вручную.

>[!IMPORTANT]
Дополнительные сведения о создании настраиваемых атрибутов см. в руководстве по управлению настраиваемыми ресурсами и атрибутами в FIM 2010.

>[!IMPORTANT]
В этом разделе отсутствуют сведения об основах форматирования и редактирования HTML-документов. Чтобы изменить файлы справки, необходимы навыки редактирования HTML.


**Расположение файлов справки**: все файлы справки для портала Microsoft Identity Management 2016 SP1 расположены в следующей папке на сервере службы MIM:

  `<ProgramFiles>\Common Files\Microsoft Shared\Web Server Extensions\12\Template\Layouts\MSILM2\Help\1033\html`

**Как найти соответствующий файл справки**: все файлы справки для портала FIM снабжены глобальными уникальными идентификаторами (GUID). Вот как найти правильный файл для настраиваемого ресурса:

1.  На портале FIM откройте файл справки на странице портала, которую нужно настроить.

2.  Щелкните правой кнопкой мыши файл справки и выберите **Свойства**.

3.  Выделите и скопируйте файл `<GUID\>.htm` в поле "URL-адрес".

4.  Перейдите к папке, где хранятся файлы справки и найдите этот файл.

**Добавление содержимого для нового атрибута**: вот как добавить описательное содержимое для нового атрибута в пределах существующего группирующего элемента (вкладки):

1.  Определите и найдите соответствующий файл справки.

2.  Откройте файл в редакторе HTML.

3.  Найдите расположение для добавления содержимого. Как правило это дополнительный абзац, например:

`<p xmlns="">A new paragraph with customized information.</p>`

Также это может быть элемент, вставленный в существующий список, например:
```
<li class="unordered"><b>First Name</b> – The first name of the User.<br>

<li class="unordered"><b>Last Name</b> - The last name of the User.<br>

<li class="unordered"><b>Added a new line</b><br>
```

**Добавление содержимого для нового группирующего элемента**: большинство страниц портала FIM снабжено несколькими элементами Grouping (или вкладками). В сопутствующих файлах справки есть разделы с закладками, относящиеся к каждому элементу Grouping. В разделах указаны закладки в формате HTML. Ниже приведен пример HTML для вкладки рабочих сведений из файла справки, предназначенного для страницы создания пользователя на портале FIM:

```
<a name="bkmk_grouping_WorkInfo" xmlns=""></a><h3 class="subHeading" xmlns="">Work Info</h3><p class="subHeading" xmlns=""></p><div class="subSection" xmlns="">
```

Для нее установлена ссылка в элементе Grouping **WorkInfo**, который содержится в XML-файле данных конфигурации для RCDC **конфигурации для создания пользователей**. Обратите внимание, что имя файла `\<GUID\>.htm` и закладка указаны в параметре my:Link:

```
<my:Grouping my:Name="WorkInfo" my:Caption="%SYMBOL_WorkInfoTabCaption_END%" my:Enabled="true" my:Visible="true"> <my:Help my:HelpText="%SYMBOL_WorkInfoTabHelpText_END%" my:Link="5e18a08b-4b20-48b8-90c6-c20f6cbeeb44.htm#bkmk_grouping_WorkInfo"/>
```

**Примеры простых элементов управления**

На следующем изображении показан пример простых элементов управления "Текстовое поле" в разных режимах.

Пример.

![](media/rcd-configuration-xml-reference/image016.gif)

В следующем фрагменте кода создается первый элемент управления "Текстовое поле", использующий явно выраженный текст для всех все атрибутов и свойств:

```
<!-- Sample for a simple control to use explicit information. (with hints)-->
<my:Control my:Name="ExplicitControl" my:TypeName="UocTextBox" my:Caption="Explicit Control" my:Description="This is explicit description." my:Hint="This is a Hint (enter any text).">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="True"/>
          <my:Property my:Name="RegularExpression" my:Value="[A-Z]*"/>
          <my:Property my:Name="Text" my:Value="Enter Information Here"/>
     </my:Properties>
</my:Control>
<!-- End of Sample for a simple control to use explicit information.-->

```


В следующем фрагменте кода создается второй элемент управления "Текстовое поле", который использует динамическую привязку, чтобы связать элемент управления с другим источником данных:

```
<!-- Sample for a simple control to use stored data information.-->
<my:Control my:Name="DynamicControl" my:TypeName="UocTextBox" my:Caption="{Binding Source=schema, Path=DisplayName.DisplayName, Mode=OneWay}" my:Description="{Binding Source=schema, Path=DisplayName.Description, Mode=OneWay}" my:RightsLevel="{Binding Source=rights, Path=DisplayName, Mode=OneWay}">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=DisplayName.Required, Mode=OneWay}"/>
          <my:Property my:Name="RegularExpression" my:Value="{Binding Source=schema, Path=DisplayName.StringRegex, Mode=OneWay}"/>
          <my:Property my:Name="Text" my:Value="{Binding Source=object, Path=DisplayName, Mode=TwoWay}"/>
     </my:Properties>
</my:Control>
<!-- End of Sample for a simple control to use stored data information.-->
```


В следующем фрагменте кода создается третий развернутый элемент управления "Текстовое поле" с меткой:

```
<!-- Sample for a simple expanded control with caption control.-->
<my:Control my:Name="SampleExpandLabel" my:TypeName="UocLabel" my:ExpandArea="true">
     <my:Properties>
          <my:Property my:Name="Text" my:Value="This is an expanded control."/>
     </my:Properties>
</my:Control>
<my:Control my:Name="ExpandedControl" my:TypeName="UocTextBox"
          my:ExpandArea="true">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="false"/>
          <my:Property my:Name="Columns" my:Value="40"/>
          <my:Property my:Name="Text" my:Value="Expanded control (enter text)"/>
     </my:Properties>
</my:Control>
<!-- End of Sample for a simple expanded control.-->
```

Во фрагменте кода ниже создается четвертый отключенный элемент управления "Текстовое поле".
Хотя видимого различия для включенного и отключенного состояния этого элемента управления нет, пользователь больше не сможет вводить данные в текстовое поле.

```
<!-- Sample for a simple disabled control.-->
<my:Control my:Name="DisabledControl" my:TypeName="UocTextBox" my:Caption="Disabled Control" my:Description="This is disabled simple control." my:Enabled="false">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="false"/>
          <my:Property my:Name="MaxLength" my:Value="128"/>
          <my:Property my:Name="Text" my:Value="Disabled control"/>
     </my:Properties>
</my:Control>
<!-- End of Sample for a simple disabled control.-->
```
## <a name="individual-controls"></a>Отдельные элементы управления

### <a name="uocbutton"></a>UocButton

**Имя**: UocButton.

**Описание**: это простой элемент управления ''Кнопка'', который можно использовать для активации определенных действий. Но использование этого элемента управления ограничено, так как вы не можете указать собственный обработчик.

**Свойства**:

1.  **Все общие свойства**: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  **Text**: это свойство определяет текст, отображаемый на кнопке. Это необязательный атрибут строкового типа. Свойство Text имеет явное строковое значение.

Событие:

   • **OnButtonClicked**: это событие возникает при нажатии кнопки.

Пример.

![](media/rcd-configuration-xml-reference/image017.png)


В следующем сегменте XML создается простая кнопка:

```
<!--Sample enabled simple button control-->
<my:Control my:Name="ButtonControl" my:TypeName="UocButton" my:Caption="SampleButton" my:Description="This is a simple button."
my:Hint="Click the button">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="True"/>
          <my:Property my:Name="Text" my:Value="Click Me"/>
     </my:Properties>
</my:Control>
<!--End of sample enabled simple button control -->
```

### <a name="uoccaptioncontrol"></a>UocCaptionControl

**Имя**: UocCaptionControl

**Описание**: этот элемент управления используется для отображения заголовка страницы RCDC. Он используется только как единственный элемент управления в группирующем элементе заголовка.
Использование в любом другом контексте может вызывать ошибки портала или неполадки с преобразованием для просмотра.

**Режим**: только для чтения (OneWay).

**Свойства:**

1.  **Все общие свойства**: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  **MaxHeight:** это свойство задает максимальную высоту значка в области заголовка. Это свойство является необязательным. Оно принимает целочисленное значение в пикселях. Значение по умолчанию — 32 пикселя.

Пример.

![](media/rcd-configuration-xml-reference/image020.jpg)

В следующем фрагменте кода создается элемент **Header Caption**:
```
<!--Sample header caption control-->
<my:Control my:Name="SampleHeaderCaption" my:TypeName="UocCaptionControl" my:ExpandArea="true" my:Caption="Header Caption" my:Description="Description Starts here.">
     <my:Properties>
          <my:Property my:Name="MaxHeight" my:Value="32"/>
          <my:Property my:Name="MaxWidth" my:Value="32"/>
     </my:Properties>
</my:Control>
<!--End of sample header caption control-->

```


В следующем фрагменте кода создается элемент **Explicit Content Caption**:

```
<my:Control my:Name="SampleContentCaption" my:TypeName="UocCaptionControl" my:ExpandArea="true" my:Caption="Sample Explicit Content Caption" my:Description="Explicit content caption with smaller icon">
     <my:Properties>
          <my:Property my:Name="MaxHeight" my:Value="20"/>
          <my:Property my:Name="MaxWidth" my:Value="20"/>
     </my:Properties>
</my:Control>
<!--End of sample caption-->
```

В следующем фрагменте кода создается динамический заголовок **Display Name**:
```
<!--Sample content dynamic caption-->
<my:Control my:Name="Caption3" my:TypeName="UocCaptionControl" my:Caption="{Binding Source=schema, Path=DisplayName.DisplayName, Mode=OneWay}" my:Description="{Binding Source=schema, Path=DisplayName.Description, Mode=OneWay}"/>
<!--End of sample caption -->
```

### <a name="uoccheckbox"></a>UocCheckBox

**Имя**: UocCheckBox.

Описание: это простой элемент управления "Флажок". Рекомендуем привязать этот элемент управления к данным логического типа. Его можно использовать как элемент управления только для чтения или как обновляемый элемент управления. Это зависит от данных, к которым он привязывается.

>[!NOTE]
Если элемент управления "Флажок" используется в режиме правки для отображения логического атрибута, которому ранее не присвоено значение, в этом выпуске RC задает для него значение **false** при щелчке кнопки **OK** в режиме правки. Чтобы решить эту проблему, можно всегда создавать логический атрибут, который приравнивает отсутствие к значению **false**, или использовать другие элементы управления для логических атрибутов, например переключатель.

**Свойства**:

1.  **Все общие свойства**: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  **DefaultValue**: это необязательное свойство логического типа. По умолчанию задано значение false. Это поле указывает для флажка поведение по умолчанию.
    Его можно задать явным образом.

3.  **Checked**: это необязательное свойство логического типа. По умолчанию задано значение false. Это значение перезаписывает свойство DefaultValue, если оно используется вместе с DefaultValue. Это поле определяет поведение флажка. Как и DefaultValue, его можно задать явным образом или привязать к данным с сервера.

4.  **Text**: это необязательный атрибут строкового типа. Текст отображается справа от флажка. Это свойство можно использовать, чтобы указать текст, который содержит дополнительные сведения для пользователя.

**События**:

   • CheckedChanged: это событие возникает, когда состояние флажка изменяется.

В примере ниже создается пользовательская привязка между типом настраиваемого ресурса и атрибутом **IsConfigurationType**. В RCDC для типа настраиваемого ресурса используется XML.

Пример.

![](media/rcd-configuration-xml-reference/image022.png)

Во фрагменте кода ниже создается **динамический флажок**, показанный выше как Dynamic Check Box. Этот тип привязки в общем более универсален и полезен, чем явно заданный флажок. Атрибут должен принадлежать к текущему типу ресурсов.

```
<!--Sample dynamic check box-->
<my:Control my:Name="SampleDynamicCheckBox" my:TypeName="UocCheckBox" my:Caption="Dynamic Check Box" my:Description="This is a dynamic check box. It saves to data source." my:RightsLevel="{Binding Source=rights, Path=IsConfigurationType}">
     <my:Properties>
          <my:Property my:Name="Text" my:Value="{Binding Source=schema, Path=IsConfigurationType.DisplayName, Mode=OneWay}"/>
          <my:Property my:Name="Checked" my:Value="{Binding Source=object, Path=IsConfigurationType, Mode=TwoWay}"/>
     </my:Properties>
</my:Control>
<!--End of sample dynamic check box -->
```


### <a name="uoccommonmultivaluecontrol"></a>UocCommonMultiValueControl

**Описание**: это элемент управления "Многострочное текстовое поле", поддерживающий форматирование специальных строк. Каждое значение в многозначных записях в текстовом поле отделено от других точкой с запятой (;) или разрывом строки. Рекомендуем привязать этот элемент управления к данным многозначных коротких строк целочисленного типа. Этот элемент управления поддерживает режим только для чтения и обновляемый режим.

**Свойства**:

1.  **Все общие свойства**: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  **DataType**: это обязательный атрибут строкового типа. Для него можно явным образом указать значения **String, Integer** или **DateTime**. Кроме того, можно привязать атрибут к свойству **DataType** атрибута схемы. Многозначные ссылочные данные должны обрабатываться элементами **UOCListView** или **UOCIdentityPicker**. Многозначные логические данные не поддерживаются.

3.  **Rows**: это необязательный атрибут строкового типа. Он позволяет определить высоту поля в цифрах. По умолчанию задано значение 1.

4.  **Columns**: это необязательный атрибут целочисленного типа. Он позволяет определить ширину поля в цифрах. По умолчанию задано значение
    20.

5.  **Value**: это необязательный атрибут строкового типа. Этот атрибут можно привязать только к источнику данных.

События:

   • **ValueListChanged**: это событие активируется, если текущее значение элемента управления изменяется.

В примере ниже создается многозначный строковый атрибут с именем **AMultiValueString**, затем он привязывается к типу настраиваемого ресурса. Этот пример работает только после создания такой привязки.

**Пример:**

![](media/rcd-configuration-xml-reference/image024.jpg)

За отображение данных выше отвечает следующий фрагмент кода:

```
<!--Sample multivalue control-->
<my:Control my:Name="SampleDynamicMultiValueControl" my:TypeName="UocCommonMultiValueControl" my:Caption="{Binding Source=schema, Path=AMultiValueString.DisplayName, Mode=OneWay}" my:Description="{Binding Source=schema, Path=AMultiValueString.Description, Mode=OneWay}" my:RightsLevel="{Binding Source=rights, Path=AMultiValueString}">
     <my:Properties>
          <my:Property my:Name="Rows" my:Value="6"/>
          <my:Property my:Name="Columns" my:Value="60"/>
          <my:Property my:Name="DataType" my:Value="String"/>
          <!--not supported for above property my:Value={Binding Source=schema, Path=AMultiValueString.DataType, Mode=OneWay}"/>-->
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=AMultiValueString, Mode=TwoWay}"/>
     </my:Properties>
</my:Control>
<!--End of sample multivalue control -->
```



### <a name="uocdatetimecontrol"></a>UocDateTimeControl


**Имя**: UocDateTimeControl

**Description**: элемент схож с элементом управления "Текстовое поле", но для элемента **Description** поддерживается только определенный формат. В режиме только для чтения он отображается в виде метки. Поддерживаемый формат входной строки см. в описании свойства **DateTimeFormat** в этом разделе.

**Свойства**:

1.  **Все общие свойства**: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  **DateTimeFormat**: это необязательный атрибут строкового типа. Поддерживаются форматы DateTime или DateOnly. По умолчанию задано значение DateTime.
    а. Формат DateTime: атрибут представлен в формате мм/дд/гггг чч:мм:сс AM.

      <[!NOTE]
      Независимо от установки разницы пользователем поддерживаются оба формата — **DateTime** и **DateOnly**.
3.  **Value**: это необязательный атрибут строкового типа. Можно привязать этот атрибут к источнику данных ресурса. Значение этого атрибута должно быть представлено в надлежащем формате даты и времени.

События:

   • **DateTimeChanged**: это событие возникает, если изменяется значение даты и времени.

Пример.

![](media/rcd-configuration-xml-reference/image027.jpg)

В следующем фрагменте кода создается первый элемент управления **DateTime**:

```
<!--Sample explicit DateTime control-->
<my:Control my:Name="SampleExplicitDateTimeControl" my:TypeName="UocDateTimeControl" my:Caption="Explicit Date Time Control" my:Description="The data shown here is explicit and in date time format.">
     <my:Properties>
          <my:Property my:Name="DateTimeFormat" my:Value="DateTime"/>
          <my:Property my:Name="Value" my:Value="11/11/2008 00:00:00"/>
     </my:Properties>
</my:Control>
<!--End of sample explicit DateTime control -->
```


В следующем фрагменте кода создается второй элемент управления **DateTime**: Если вы использовали пример кода в разделе источников данных, атрибут **ExpirationTime** привязан ко всем типам ресурсов. Поэтому его можно использовать со следующим кодом:

```
<!--Sample dynamic DateTime control-->
<my:Control my:Name="SampleDynamicDateTimeControl" my:TypeName="UocDateTimeControl" my:Caption="{Binding Source=schema, Path=ExpirationTime.DisplayName, Mode=OneWay}" my:Description="{Binding Source=schema, Path=ExpirationTime.Description, Mode=OneWay}" my:RightsLevel="{Binding Source=rights, Path=ExpirationTime}">
     <my:Properties>
          <my:Property my:Name="DateTimeFormat" my:Value="DateOnly"/>
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=ExpirationTime, Mode=TwoWay}"/>
     </my:Properties>
</my:Control>
<!--End of dynamic explicit DateTime control -->
```



### <a name="uocdropdownlist"></a>UocDropDownList

**Имя**: UocDropDownList

Описание: это простой элемент управления "Раскрывающийся список". Этот элемент управления обычно используется, если нужно выбрать параметры из определенного набора вариантов. Для этого элемента управления подходят типы данных строки, целого числа, даты и времени и логического значения.

**Свойства**:

1.  **Все общие свойства**: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  **ValuePath**: свойство для получения атрибута Value из ItemSource. Если для ItemSource указано Custom, для пути к значению задается значение Value. Свойство привязывается к полю Value в элементе Option, который будет рассматриваться далее в этом документе.

3.  **CaptionPath**: свойство для получения атрибута Value из ItemSource. Если для ItemSource указано Custom, для пути к значению задается значение Caption. Свойство привязывается к полю Caption в элементе Option, который будет рассматриваться далее в этом документе.

4.  **HintPath**: свойство для получения атрибута Value из ItemSource. Если для ItemSource указано Custom, для пути к значению задается значение Hint. Свойство привязывается к полю Hint в элементе Option, который будет рассматриваться далее в этом документе.

5.  **ItemSource**: коллекция ListControlItems, которая определяет выбор в списке. Пользователь может явно задать значение Custom и использовать элемент Option, чтобы указать строковое значение.

6.  **SelectedValue**: выбранное значение. Это обязательное свойство строкового типа. Это свойство привязывается к данным строки из источника данных.

События:

  • SelectedIndexChanged: это событие возникает, если выбор в раскрывающемся списке изменяется.

Параметры:

Дополнительные сведения см. в разделе "Элемент Option" этого документа.

1.  **Value**: значение Value из одного элемента Option можно установить для любой строки, содержащей допустимые входные данные из источника данных, к которому привязан элемент управления.

2.  **Caption**: для Caption можно задать любое строковое значение.

3.  **Hint**: для Hint можно задать любое строковое значение.

Пример.

![](media/rcd-configuration-xml-reference/image030.jpg)


![](media/rcd-configuration-xml-reference/image031.jpg)

>[!NOTE]
Чтобы пример кода работал, привяжите существующий атрибут **Scope** строкового типа к типу настраиваемого ресурса, к которому применяется RCDC.


В этом фрагменте кода создается раскрывающийся список:

```
<!--Sample for drop-down list control-->
<my:Control my:Name="Scope" my:TypeName="UocDropDownList" my:Caption="{Binding Source=schema, Path=Scope.DisplayName}" my:RightsLevel="{Binding Source=rights, Path=Scope}">
     <my:Options>
          <my:Option my:Value="DomainLocal" my:Caption="Domain Local" my:Hint="to secure a local resource (i.e. a file share on your computer)" />
          <my:Option my:Value="Global" my:Caption="Global" my:Hint="to secure resources across your team or division" />
          <my:Option my:Value="Universal" my:Caption="Universal" my:Hint="to use this group across your organization" />
     </my:Options>
     <my:Properties>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=Scope.Required" />
          <my:Property my:Name="ValuePath" my:Value="Value" />
          <my:Property my:Name="CaptionPath" my:Value="Caption" />
          <my:Property my:Name="HintPath" my:Value="Hint" />
          <my:Property my:Name="ItemSource" my:Value="Custom" />
          <my:Property my:Name="SelectedValue" my:Value="{Binding Source=object, Path=Scope, Mode=TwoWay}" />
     </my:Properties>
</my:Control>
<!--End of Sample for drop-down list control-->
```


### <a name="uocfiledownload"></a>UocFileDownload

Имя: UocFileDownload.

Описание: этот элемент управления содержит гиперссылку. Если щелкнуть гиперссылку, откроется страница Windows для сохранения файла. Пользователь может сохранить файл на своем локальном диске.
Кроме того, поддерживается параметр "Открыть", если Internet Explorer может преобразовать формат файла для просмотра. Типы данных, с которыми рекомендуется использовать этот элемент управления, — отформатированная строка (XML) и двоичные данные.

>[!NOTE]
В этом выпуске Microsoft Identity Manager 2016 SP1 пользователь должен закрыть окно Internet Explorer, в котором был открыт файл, а затем обновить страницу. После обновления окна Internet Explorer можно начать загрузку, чтобы повторно сохранить или открыть тот же файл в исходном окне.


Свойства:

1.  **Все общие свойства**: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  **Text**: это необязательный атрибут строкового типа, определяющий текст гиперссылки. Пользователь может указать для этого свойства явно определенную строку.

3.  **Value**: это обязательный атрибут. Он указывает привязку атрибута на сервере, содержимое с которого требуется скачать.

4.  **PromptedFileName**: это необязательный атрибут строкового типа. Это имя файла, предлагаемое пользователю при сохранении загруженного файла.

5.  **ContentType**: это обязательный атрибут строкового типа. Это тип файла, в котором сохраняются данные. Поддерживаются два варианта строк — текст или двоичные данные. Если это текст, возвращаемое значение будет считаться длинной строкой.
    Если это двоичные данные, возвращаемое значение будет считаться значением byte[]. Если выбран текст, можно добавить суффикс, чтобы указать тип формата для текста (необязательно). Например, допустимым является формат text/xml.


>[!NOTE]
Если к этому элементу управления привязано пустое значение, он отсутствует в гиперссылке для активации действия скачивания. Это происходит, так как элементы для скачивания отсутствуют.


**События**:

Для этого элемента управления события отсутствуют.

**Пример**:

![](media/rcd-configuration-xml-reference/image035.png)


>[!NOTE]
Перед передачей этого примера файла нужно создать привязку между типом настраиваемого ресурса и существующим атрибутом ConfigurationData.


В следующем фрагменте кода создается элемент управления для загрузки файлов, представленный изображении выше:

```
<!--Sample dynamic download control-->
<my:Control my:Name="SampleDynamicFileDownloadControl" my:TypeName="UocFileDownload" my:Caption="{Binding Source=schema, Path=ConfigurationData.DisplayName, Mode=OneWay}" my:Description="{Binding Source=schema, Path=ConfigurationData.Description, Mode=OneWay}" my:RightsLevel="{Binding Source=rights, Path=ConfigurationData}">
     <my:Properties>
          <my:Property my:Name="Text" my:Value="Download Dummy xml"/>
          <my:Property my:Name="PromptedFileName" my:Value="DummyXML.xml"/>
          <my:Property my:Name="ContentType" my:Value="text/xml"/>
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=ConfigurationData}"/>
     </my:Properties>
</my:Control>
<!--End of dynamic download control -->
```


### <a name="uocfileupload"></a>UocFileUpload

**Имя**: UocFileUpload

**Описание**: этот элемент управления содержит текстовое поле, в котором отображается расположение локального файла для передачи, кнопка обзора для файла и кнопки передачи. Когда пользователь нажимает кнопку обзора, открывается окно Windows для открытия файла. Пользователь может выбрать для передачи один файл на своем локальном диске. При выборе файла в текстовом поле отображается его расположение. При нажатии кнопки передачи файл передается в клиентский локальный источник данных. Содержимое файла еще не отправлено на сервер. Типы данных, с которыми рекомендуется использовать этого элемент управления, — отформатированная строка (XML) или двоичные данные.

>[!NOTE]
Для отображения хода выполнения или состояния передачи индикация не предусмотрена. Когда файл передается в локальный источник данных, текстовое поле очищается.


Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  Value: это обязательный атрибут. Определяет привязку атрибута к схеме на сервере, на который передаются данные.

3.  ContentType: это необязательный атрибут строкового типа. Это тип данных файла, который сохраняется на сервере. Для него можно задать текст или двоичные данные. Если свойство отсутствует, по умолчанию задаются двоичные данные.

4.  MaxFileSize: это необязательный атрибут строкового типа. MaxFileSize определяет максимальный размер передаваемого файла. По умолчанию, если свойство отсутствует, максимальный размер составляет 1 мегабайт (МБ).

5.  PromptedForNoValue: это необязательный атрибут строкового типа. Он определяет текст, отображаемый для пользователя, если передача файла не выполняется.

События:

   • FileUploaded: это событие создается, если файл успешно передан.

Пример.

![](media/rcd-configuration-xml-reference/image040.png)

>[!NOTE]
Чтобы пример кода ниже работал, создайте атрибут двоичного типа с именем ABinaryAttribute и привязку между типом настраиваемого ресурса и этим атрибутом.


В следующем фрагменте кода создается элемент управления для передачи файлов, представленный на изображении выше:
```
<!--Sample dynamic upload control-->
<my:Control my:Name="SampleDynamicFileUploadControl" my:TypeName="UocFileUpload" my:Caption="{Binding Source=schema, Path=ABinaryAttribute.DisplayName, Mode=OneWay}" my:Description="{Binding Source=schema, Path=ABinaryAttribute.Description, Mode=OneWay}” my:RightsLevel="{Binding Source=rights, Path=ABinaryAttribute}">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=ABinaryAttribute.Required}"/>
          <my:Property my:Name="ContentType" my:Value="Binary"/>
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=ABinaryAttribute, Mode=TwoWay}"/>
     </my:Properties>
</my:Control>
<!--End of dynamic upload control -->
```

### <a name="uocfilterbuilder"></a>UocFilterBuilder

Имя: UocFilterBuilder.

Описание: это сложный элемент управления, который позволяет пользователю преобразовать выражение XPath MIM 2016 для просмотра. Некоторые выражения XPath не поддерживаются. Сведения об использовании построителя фильтров см. в соответствующем разделе справки.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  PermittedObjectTypes: определяет список типов ресурсов, которые должны отображаться в инструкции select для построителя фильтров. Сведения об использовании построителя фильтров см. в соответствующем разделе справки. Строка представлена в формате ResourceTypeA, ResourceTypeB, где каждый тип ресурса отделяется запятой (,).

3.  Value: это значение, с помощью которого построитель фильтров преобразуется для просмотра.
    Поддерживается только привязка к данным строкового типа, содержащим выражение XPath. Для привязки этого элемента управления рекомендуется использовать атрибут Filter.

4.  PreviewButtonVisible: это необязательное свойство логического типа. Если это свойство имеет значение false, кнопка предварительного просмотра не отображается. По умолчанию задано значение true. Эту кнопку можно использовать в сочетании с элементом управления "Представление списка" для предварительного просмотра результатов выражения XPath.

5.  ExcludeGroupMembership: это логическое свойство. Если для этого свойства задано значение true, нельзя создать фильтр, использующий \<ссылочный атрибут\> (например, ResourceID) и являющийся элементом \<объекта группы\>. Другими словами, если для этого свойства задано значение true, нельзя создать фильтр, использующий каталог членства в группах.

6.  PreviewButtonCaption: это необязательная строка. Если для PreviewButtonVisible задано значение true, можно использовать это свойство, чтобы присвоить кнопке настраиваемый текст. Текст отображается на кнопке предварительного просмотра.

События:

   • OnFilterChanged: это событие активируется, если содержимое построителя фильтров изменяется.

Пример.

![](media/rcd-configuration-xml-reference/image044.png)

>[!NOTE]
Прежде чем использовать этот пример кода, создайте привязку между существующим атрибутом Filter и типа настраиваемого ресурса.


Ниже приведен пример кода, который включает элемент управления UOCLabel, простой построитель фильтров с PermittedObjectTypes и представление списка предварительного просмотра. Укажите для свойства представления списка ListFilter и свойства построителя фильтров Value один и тот же атрибут источника данных, чтобы связать их.

```
<!--Sample filter builder with preview list-->
<my:Control my:Name="ComplexFilterBuilderLabel" my:TypeName="UocLabel" my:ExpandArea="true">
     <my:Properties>
          <my:Property my:Name="Text" my:Value="This is a Filter Builder with preview."/>
     </my:Properties>
</my:Control>
<my:Control my:Name="ComplexFilterBuilder" my:TypeName="UocFilterBuilder" my:RightsLevel="{Binding Source=rights, Path=Filter}" my:ExpandArea="true">
     <my:Properties>
          <my:Property my:Name="PermittedObjectTypes" my:Value="Person,Group" />
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=Filter, Mode=TwoWay}" />
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=Filter.Required, Mode=OneWay}" />
     </my:Properties>
</my:Control>
<my:Control my:Name="FilterBuilderwithpreview" my:TypeName="UocListView" my:ExpandArea="true">
     <my:Properties>
          <my:Property my:Name="ColumnsToDisplay" my:Value="DisplayName,ObjectType,AccountName" />
          <my:Property my:Name="EmptyResultText" my:Value="There is no members according to the filter definition." />
       <my:Property my:Name="PageSize" my:Value="10" />
       <my:Property my:Name="ShowTitleBar" my:Value="false" />
       <my:Property my:Name="ShowActionBar" my:Value="false" />
       <my:Property my:Name="ShowPreview" my:Value="false" />
       <my:Property my:Name="ShowSearchControl" my:Value="false" />
       <my:Property my:Name="EnableSelection" my:Value="false" />
       <my:Property my:Name="SingleSelection" my:Value="false" />
       <my:Property my:Name="ItemClickBehavior" my:Value=" ModelessDialog "/>
       <my:Property my:Name="ListFilter" my:Value="{Binding Source=object, Path=Filter}" />
     </my:Properties>
</my:Control>
<!--end of sample filter builder with preview-->
```


<a name="uochtmlsummary"></a>UocHtmlSummary
--------------

Имя: UocHtmlSummary.

Описание: вы можете использовать этот элемент управления, чтобы определить страницу сводки на странице RCDC.
Страница сводки отображается после того, как пользователь отправит запрос. Этот элемент управления можно использовать только в группирующем элементе сводки, и он должен быть единственным элементом управления. Настоятельно рекомендуем использовать предоставленный пример кода.

>[!NOTE]
Этот элемент не проходил всестороннее тестирование.


Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  ModificationsXml: это свойство должно быть представлено в формате {Binding Source=delta, Path=DeltaXml}, где разница в значениях определяется в заголовке конфигурации ObjectDataSource.

3.  TransformXsl: это свойство обычно представлено в формате {Binding Source=summaryTransformXsl, Path=/}, где summaryTransformXsl определяется в заголовке конфигурации XmlDataSource.

Готовый пример этого элемента управления см. в подразделе "Элемент Summary Grouping" раздела "Элемент Grouping" выше.

### <a name="uochyperlink"></a>UocHyperLink

Имя: UocHyperLink.

Описание: это простой элемент управления "Гиперссылка". Вы можете использовать его для отображения информации в виде гиперссылки.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  ObjectReference: это необязательное свойство ссылочного типа. Если для идентификатора GUID, который определен в этом свойстве, установлена ссылка на допустимый ресурс, по гиперссылке пользователь может получить доступ к ресурсу. ObjectReference и NavigateUrl (ниже) — взаимоисключающие свойства.

3.  Text: это необязательное свойство строкового типа. Оно используется для определения текста, который отображается в виде гиперссылки.

4.  NavigateUrl: это необязательное свойство строкового типа. Оно используется для определения полного URL-адреса, к которому привязана гиперссылка. NavigateUrl и ObjectReference (выше) — взаимоисключающие свойства.

Пример.

![](media/rcd-configuration-xml-reference/image049.jpg)

>[!NOTE]
Требуется допустимый GUID ресурса, чтобы установить для него ссылку. В этом случае создается вторая гиперссылка с допустимым идентификатором GUID. В первой гиперссылке может быть указан любой веб-сайт.


В следующем фрагменте кода создается гиперссылка перенаправления:

```
<!--Sample for a hyperlink that redirects page.-->
<my:Control my:Name="RedirectHyperlink" my:TypeName="UocHyperLink" my:Caption="Redirect Hyperlink" my:Description="This is a hyperlink that takes you to other pages.">
     <my:Properties>
          <my:Property my:Name="NavigateUrl" my:Value="http://www.microsoft.com"/>
          <my:Property my:Name="Text" my:Value="Microsoft Home Page"/>
     </my:Properties>
</my:Control>
<!--End of Sample for a hyperlink that redirect page-->

```

В следующем фрагменте кода создается гиперссылка на ресурс. Явно выраженную ссылку можно заменить выражением {Binding Source=object, Path=Creator}, чтобы создать привязку к источнику данных. Это допустимо только при наличии диспетчера ресурса и значения ссылочного типа.

```
<!--Sample for a hyperlink that reference object-->
<my:Control my:Name="ReferenceHyperlink" my:TypeName="UocHyperLink" my:Caption="Reference Hyperlink" my:Description="This is a hyperlink gives you an object view of the reference object">
     <my:Properties>
          <my:Property my:Name="ObjectReference" my:Value="e4e048b1-9e43-415e-806c-cf44c429c34c"/>
          <my:Property my:Name="Text" my:Value="View a group in FIM 2010."/>
     </my:Properties>
</my:Control>
<!--End of Sample for a hyperlink that reference object-->
```

### <a name="uocidentitypicker"></a>UocIdentityPicker

Имя: UocIdentityPicker.

Описание: этот элемент управления состоит из необязательного поля "Resolve" и окна "Browse". Необязательное поле "Resolve" содержит необязательное текстовое поле для ввода данных удостоверения, кнопки разрешения для удостоверения и кнопки "Browse" для активации всплывающего окна "Browse". В окне "Browse" можно выбрать удостоверения с помощью элемента управления "Представление списка". Выбранное в окне "Browse" удостоверение отображается в поле "Resolve".

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  UsageKeywords: это необязательное строковое свойство. Вы можете определить список областей поиска для использования в средстве выбора ресурсов, предоставив список используемых ключевых слов, которые поддерживаются структурой SearchScopeConfiguration. Ключевые слова разделены символом (‘).

3.  Filter: это необязательное строковое свойство. Пользователь предоставляет выражение XPath для ограничения выбора ресурсов только теми элементами, которые находятся в определенной области. Filter и UsageKeywords (выше) — взаимоисключающие свойства. При применении области поиска это свойство не работает.

4.  ResultObjectType: это необязательное строковое свойство. Тип ресурса используется, чтобы преобразовать ресурс для просмотра во всплывающем диалоговом окне со списком. Используется со свойством Filter, чтобы помочь средству выбора удостоверений определить, какой тип ресурса возвращается свойством Filter, и соответствующим образом преобразовать данные для просмотра. ResultObjectType и UsageKeywords (выше) — взаимоисключающие свойства. При применении области поиска это свойство не работает. Для этого свойства приемлемы любые одиночные и допустимые строки, а также имена типов ресурсов, например Person.
    Если фильтр должен вернуть несколько типов ресурсов, используется свойство Resource.

5.  PreviewTitle: это предварительная версия заголовка для представления списка. Сведения об этом свойстве см. в разделе UocListView.

6.  ListViewTitle: это необязательное строковое свойство. Это свойство можно использовать для определения текста, отображаемого в верхней части представления списка в качестве заголовка.

7.  Value: это необязательное строковое свойство. Рекомендуем привязать его к атрибуту схемы, чтобы подключить значение к источнику данных.

8.  Mode: это необязательное строковое свойство. Это свойство используется для определения того, сколько удостоверений может быть выбрано средством выбора удостоверений (одно или несколько). Допустимые значения — SingleResult и MultipleResult. По умолчанию задано значение SingleResult.

9.  ObjectTypes: это необязательное свойство строкового типа. Оно позволяет определить список типов ресурсов, в соответствии с которыми пользователь может разрешить записи в поле разрешения для средства выбора удостоверений. Список состоит из имен типов ресурсов, разделенных запятой (,).

10. AttributesToSearch: это необязательное свойство строкового типа. Оно позволяет определить список атрибутов, которые будут использоваться для разрешения элемента в средстве выбора удостоверения. Список состоит из атрибутов схемы, разделенных запятой (,). Например, если для AttributesToSearch задано значение DisplayName, Alias, пользователь может выполнять поиск элементов, установив DisplayName = \<искомое значение\> или Alias = \<искомое значение\>. Рекомендуем вводить имена допустимых атрибутов для целевых типов ресурсов источника данных, указанного в свойстве Value. Целевые типы ресурсов можно найти в поле ObjectTypes. Все атрибуты должны быть допустимыми для любых типов ресурсов, указанных в поле ObjectTypes.

11. ColumnsToDisplay: это необязательное свойство строкового типа. Пользователь предоставляет список имен атрибутов схемы, разделенных запятой (,). Атрибуты, которые определены здесь, составляют столбец в представлении списка в средстве выбора удостоверений.

12. Rows: это необязательное целочисленное свойство. Оно работает, только если для свойства Mode задано значение MultipleResult. Используйте это свойство, чтобы установить нужную высоту текстового поля разрешения в символах.

13. MainSearchScreenText: это необязательное свойство строкового типа. Это настраиваемый текст, который отображается при выполнении поиска в окне обзора.

События:

 • SelectedObjectChanged: это событие создается, когда пользователь изменяет выбранные ресурсы.

Пример.

![](media/rcd-configuration-xml-reference/image052.png)

>[!NOTE]
Чтобы этот пример кода работал, создайте привязку между атрибутом Manager и любым типом настраиваемого ресурса, к которому применяется этот XML-код.


В следующем фрагменте кода создается средство выбора удостоверения в одиночном режиме с помощью свойств Filter и ResultObjectType как часть RCDC:

```
<!--Sample for a single-selection identity picker using Filter and Result Object Type-->
<my:Control my:Name="SingleSelectionIdentityPicker" my:TypeName="UocIdentityPicker" my:Caption="A Single Selection Identity Picker" my:Description="The user is allowed to select only one entry here." my:RightsLevel="{Binding Source=rights, Path=Manager}">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=Manager.Required}"/>
          <my:Property my:Name="Mode" my:Value="SingleResult" />
          <!--Columns displayed in list view in pop-up window-->
          <my:Property my:Name="ColumnsToDisplay" my:Value="DisplayName, ObjectType" />
          <!--Identities will be resolved against following attribute in the resolve textbox when resolve button is clicked.-->
          <my:Property my:Name="AttributesToSearch" my:Value="DisplayName, AccountName" />
          <!--single valued reference type attribute is used to bind the control-->
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=Manager , Mode=TwoWay}" />
          <!--Scoping the list explicitly to All Persons name contains letter "e"-->
          <my:Property my:Name="Filter" my:Value="/Person[contains(JobTitle, 'Manager')]"/>
          <!--Result object type specify the type is Person-->
          <my:Property my:Name="ResultObjectType" my:Value="Person"/>
          <my:Property my:Name="ListViewTitle" my:Value="Select only one entry" />
          <my:Property my:Name="PreviewTitle" my:Value="Entry selected:" />
     </my:Properties>
</my:Control>
<!--End of sample for a single-selection identity picker.-->
```



Пример.

![](media/rcd-configuration-xml-reference/image056.jpg)

>[!NOTE]
Чтобы этот пример кода работал, привяжите атрибут ExplicitMember (многозначный ссылочный атрибут) к типу настраиваемого ресурса. Кроме того, нужно создать области поиска с заданными для свойства UsageKeyword значениями Person и Group.


В следующем фрагменте кода создается элемент управления, представленный изображении выше:

```
<!--Sample for a multiselection Identity Picker uses Search Scope-->
<my:Control my:Name="multiSelectionIdentityPicker" my:TypeName="UocIdentityPicker" my:Caption="A multi Selection Identity Picker" my:Description="The user is allowed to select more than one entry here" my:RightsLevel="{Binding Source=rights, Path=ExplicitMember}">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=ExplicitMember.Required}"/>
          <my:Property my:Name="Mode" my:Value="MultipleResult" />
          <my:Property my:Name="Rows" my:Value="10" />
          <!--There are existing search scopes that has key word "Person" and "Group" use both sets of search scopes here.-->
          <my:Property my:Name="UsageKeywords" my:Value="Person,Group"/>
          <!--Columns displayed in list view in pop-up window-->
          <my:Property my:Name="ColumnsToDisplay" my:Value="DisplayName, ObjectType" />
          <!--Identities will be resolved against following attribute in the resolve textbox when resolve button is clicked.-->
          <my:Property my:Name="AttributesToSearch" my:Value="DisplayName, AccountName" />
          <!--multi valued reference type attribute is used to bind the control-->
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=ExplicitMember , Mode=TwoWay}" />
          <my:Property my:Name="ResultObjectType" my:Value="Resource"/>
          <my:Property my:Name="ListViewTitle" my:Value="Select multiple entries" />
          <my:Property my:Name="PreviewTitle" my:Value="Entries selected" />
     </my:Properties>
</my:Control>
<!--End of sample for a multiselection Identity Picker.-->
```


### <a name="uoclabel"></a>UocLabel

Имя: UocLabel.

Описание: это простой элемент управления "Текстовая подпись"; только для чтения. Рекомендуем использовать этот элемент управления для отображения данных только для чтения.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  Text: это обязательный атрибут строкового типа. Вы можете определить это свойство, указав явное строковое значение или привязав его к источнику данных. Пример привязки, которая присваивает значение этого свойства — {Binding Source=object, Path=\<имя допустимого атрибута\>.

Пример элемента управления UocLabel см. в разделе с примерами простых элементов управления.

### <a name="uoclistview"></a>UocListView

Имя: UocListView.

Описание: это элемент управления "Расширенное представление списка". Он состоит из простого представления списка, необязательного элемента управления "Простой поиск", необязательного элемента управления "Расширенный поиск", необязательного поля предварительного просмотра для выбора и панели с кнопками действий. Необязательный элемент управления "Простой поиск" состоит из области поиска и текстового поля. Элемент управления "Расширенный поиск" — это построитель фильтров. В представлении списка отображается предварительно преобразованный для просмотра список ресурсов. Также здесь могут быть показаны результаты поиска, поступающие от элементов управления поиска в этом элементе управления. Панель с кнопками действий определяет, какие действия могут выполняться, на основе выбора в представлении списка. В поле предварительного просмотра выбранного отображаются элементы, выбранные в представлении списка.

>[!IMPORTANT]
UocListView не работает со ссылочными атрибутами с одним значением. Этот элемент управления можно использовать только с многозначными ссылочными атрибутами. Список ссылочных атрибутов с одним значением см. в описании UocIdentityPicker в этом документе.


Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  SelectedValue: это необязательное свойство строкового типа, которое обычно привязывается к многозначному ссылочному атрибуту, принимающему список строк в формате GUID.

3.  PageSize: это необязательное целочисленное свойство. Позволяет указать, сколько записей будет помещаться на одной странице в элементе управления "Представление списка". Значение по умолчанию — 10 записей. Может быть любым положительным целым числом.

4.  UsageKeyword: это необязательное свойство строкового типа. Позволяет указать список ключевых слов, которые определяют используемую область поиска для элемента управления поиска по представлению списка. На сервере FIM 2010 есть ресурсы для области поиска. Атрибут в структуре SearchScopeConfiguration с именем UsageKeyword используется для группирования набора областей поиска. Представление списка использует этот список ключевых слов. Каждое ключевое слово отделяется запятой (,).
    Атрибут usagekeyword используется для соответствующей области поиска, которую вам нужно отобразить в определенном представлении списка. Такой сценарий работает, только если для свойства ShowSearchControl задано значение true.

5.  SearchControlAutoPostback: это необязательное логическое свойство. Установите для этого свойства значение true, чтобы при активации поиска выполнялась автоматическая обратная передача. По умолчанию для SearchControlAutoPostback задано значение false.

6.  EmptyResultText: это необязательное свойство строкового типа. По умолчанию элементы для него не определены, но ему может быть задано любое строковое значение. Этот текст отображается, если результаты поиска отсутствуют.

7.  ButtonHeight: это необязательное свойство целочисленного типа. Значение этого свойства может быть любым положительным целым числом. Это свойство определяет высоту кнопок на панели действий в пикселях. Значение по умолчанию — 32 пикселя.

8.  ButtonWidth: это необязательное свойство целочисленного типа. Значение этого свойства может быть любым положительным целым числом. Это свойство определяет ширину кнопок на панели действий в пикселях. Значение по умолчанию — 32 пикселя.

9.  CaptionImageMaxHeight: это необязательное свойство целочисленного типа. Значение этого свойства может быть любым положительным целым числом. Это свойство определяет максимальную высоту необязательного заголовка. Значение по умолчанию — 32 пикселя.

10. CaptionImageMaxWidth: это необязательное свойство целочисленного типа. Значение этого свойства может быть любым положительным целым числом. Это свойство определяет максимальную ширину необязательного заголовка . Значение по умолчанию — 32 пикселя.

11. CaptionImageUrl: это необязательное свойство строкового типа. Оно позволяет определить URL-адрес, привязанный к изображению, которое отображается для заголовка.

12. PreviewTitle: это необязательное свойство строкового типа. Оно позволяет определить текст, отображаемый в верхней части поля предварительного просмотра выбранного.

13. EnableSelection: это необязательное свойство логического типа. Оно позволяет определить, находится ли представление списка в режиме выбора. Если представление списка находится в режиме выбора, в крайнем левом столбце представления списка отображаются флажки, а в его нижней части появляется поле предварительного просмотра выбранного. По умолчанию для этого свойства задано значение true.

14. SingleSelection: это необязательное свойство логического типа. Если для представления списка включен режим выбора, установив для этого свойства значение true, можно ограничить выбор только одним элементом из списка. По умолчанию для этого свойства задано значение false. Это означает, что по умолчанию пользователи могут выбрать несколько элементов из списка.

15. RedirectUrl: это необязательное свойство строкового типа. Оно позволяет указать страницу для перенаправления при щелчке элемента гиперссылки в списке. Этот URL-адрес может содержать заполнители, которые во время выполнения будут заменены фактическими значениями. Заполнители выглядят так:

     ◦ {0} — objectType

     ◦ {1} — objectID

     ◦ {2} — displayName

16.  ShowTitleBar: это необязательное свойство логического типа. Оно позволяет указать, должен ли отображаться заголовок. По умолчанию для этого свойства задано значение false.

17.  ShowActionBar: это необязательное свойство логического типа. Оно позволяет указать, должна ли отображаться панель действий. По умолчанию для этого свойства задано значение true.

18.  ShowPreview: это необязательное свойство логического типа. Оно позволяет указать, должна ли отображаться область предварительного просмотра. По умолчанию для этого свойства задано значение true.

19.  ShowSearchControl: это необязательное свойство логического типа. Оно позволяет указать, должен ли отображаться элемент управления поиска. По умолчанию для этого свойства задано значение true.

20.  ResultObjectType: это необязательное свойство строкового типа. Оно позволяет указать ожидаемый тип объекта для результатов поиска. По умолчанию для этого свойства задано значение Resource. Если результат поиска содержит несколько типов ресурсов, для этого свойства должно быть задано значение Resource.

21.  ColumnsToDisplay: это необязательное свойство. Оно позволяет указать, какие атрибуты должны отображаться в представлении списка в виде столбцов. Значения по умолчанию этого свойства — DisplayName и ResourceType. Каждый столбец представлен системным именем атрибута. Каждый столбец отделяется запятой (,). Если представление списка используется в режиме выбора, указывать значение для этого свойства не требуется. В режиме выбора параметры столбца поступают из атрибута SearchScopeColumn в выбранной области поиска.

22.  ListFilter: это необязательное свойство строкового типа. Это выражение xpath, используемое, чтобы преобразовать представление списка для просмотра. Оно работает, только если для свойства ShowSearchControl задано значение false. Если оно установлено, представление списка использует значение этого свойства для запросов. При этом представление списка не находится в режиме выбора. Фильтр можно привязать к строковому атрибуту ресурса следующим образом:<br/><br/>
     `<my:Property my:Name="ListFilter" my:Value="{Binding Source=object, Path=Filter}"/>` <br/> <br/>
     Или же он может являться строкой, которая содержит некоторые предварительно определенные переменные среды, как указано ниже: <br/><br/>
     `<my:Property my:Name="ListFilter" my:Value="/Approval[Request=''%ObjectID%'']"/>`

23.  TargetAttribute: это устаревшее свойство. Его значение должно быть системным именем многозначного атрибута, для которого установлена ссылка. Не рекомендуем использовать это свойство. Например, для управления группами можно заменить код:

  `<my:Property my:Name="TargetAttribute" my:Value="ExplicitMember"/>` <br/>

  следующей строкой: `<my:Property my:Name=”ListFilter” my:Value=”/Group[ObjectID=’%ObjectID%’]/ExplicitMember”/>` <br/><br/>
24.  ItemClickBehavior: это необязательное свойство строкового типа. Оно позволяет указать, какое действие выполняется при щелчке элемента в представлении списка: активация обратной передачи с сервера или отображение представления со сведениями об элементе. Поддерживаются два варианта значений: ModelessDialog и Server. Значение по умолчанию — ModelessDialog.

25.  SearchOnLoad: это необязательное свойство логического типа, указывающее, должен ли элемент управления "Представление списка" подавать запрос о загрузке. Оно применимо, только если представление списка находится в режиме выбора. По умолчанию для этого свойства задано значение true. Можно отключить его, если предполагается, что пользователь будет вводить текст в поле поиска, чтобы получить релевантный результат. В этом случае в представлении списка первоначально отображается сообщение, информирующее пользователя о том, как выполнить поиск. Текст можно настроить при помощи описанных ниже свойств.

26.  MainSearchScreenText: это необязательное свойство строкового типа применимо, только если для SearchOnload задано значение true. Оно позволяет настроить текст, отображаемый в центре представления списка, если в представлении списка не выполняется автоматический поиск. По умолчанию для этого свойства задается текст "Найдите ресурсы с помощью функции поиска, представленной выше". Можно указать текст, который будет более подходящим для вашего сценария.

27.  SubSearchScreenText: это необязательное свойство строкового типа используется для настройки текста, который отображается под MainSearchScreenText. Обычно указывать значение для этого свойства не требуется, если вы не собираетесь добавить некоторые дополнительные инструкции по использованию представления списка.

Примеры использования представления списка с элементом управления UocFilterBuilder для предварительного просмотра списка см. в примерах для UocFilterBuilder выше. UocListView может использоваться и без построителя фильтров.

### <a name="uocnumericbox"></a>UocNumericBox

Имя: UocNumericBox.

Описание: это простое текстовое поле, которое принимает только целочисленные значения. Этот элемент управления поддерживает режим только для чтения и обновляемый режим.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  MaxValue: это необязательное свойство целочисленного типа. Оно позволяет определить клиентскую проверку для элемента управления. Введенное пользователем значение не должно превышать это значение. Вы можете ввести явно выраженное целое число или привязать свойство к целочисленным данным из источника данных с помощью {Binding Source=schema Path=IntegerMaximum}.

3.  MinValue: это необязательное свойство целочисленного типа. Оно позволяет определить клиентскую проверку для элемента управления. Введенное пользователем значение не должно быть меньше этого значения. Вы можете ввести явно заданное целое число или привязать свойство к целочисленным данным из источника данных с помощью {Binding Source=schema Path=IntegerMinimum}.

4.  DefaultValue: это необязательное свойство целочисленного типа. Оно позволяет определить значение по умолчанию для элемента управления, если он используется для создания данных. Это значение может быть только явно заданным статическим целым числом.

5.  Value: это необязательное свойство целочисленного типа. Когда вы привязываете его к данным целочисленного типа из источника данных, значение этого атрибута отображается при загрузке страницы, а затем сохраняется в источнике данных после отправки.

Обработчик:

   • TextChanged: это событие возникает, если текущее значение в элементе управления изменяется.

Пример.

![](media/rcd-configuration-xml-reference/image061.jpg)

>[!NOTE]
В примере кода ниже создается первое числовое поле. Числовое поле не подключено к источнику данных или к информации схемы.

```
<!--Sample for an explicit Numeric Box-->
<my:Control my:Name="SampleExplicitNumericBox" my:TypeName="UocNumericBox" my:Caption="An Explicit NumericBox" my:Description="This is a dummy numeric box that is not linked with data source.">
     <my:Properties>
          <my:Property my:Name="MinValue" my:Value="1"/>
          <my:Property my:Name="MaxValue" my:Value="100"/>
          <my:Property my:Name="DefaultValue" my:Value="1"/>
     </my:Properties>
</my:Control>
<!--End of sample for an explicit Numeric Box.-->

```

В примере кода ниже создается второе числовое поле.

>[!NOTE]
Чтобы этот пример работал, сначала создайте атрибут целочисленного типа с именем AnIntegerAttribute и привяжите его к типу настраиваемого ресурса.

```
<!--Sample for a dynamically rendered numeric box-->
<my:Control my:Name="SampleDynamicNumericBox" my:TypeName="UocNumericBox" my:Caption="{Binding Source=schema, Path=AnIntegerAttribute.DisplayName}" my:Description="{Binding Source=schema, Path=AnIntegerAttribute.Description}" my:RightsLevel="{Binding Source=rights, Path=AnIntegerAttribute}">
     <my:Properties>
          <my:Property my:Name="MaxValue" my:Value="{Binding Source=schema, Path=AnIntegerAttribute.IntegerMaximum}"/>
          <my:Property my:Name="MinValue" my:Value="{Binding Source=schema, Path=AnIntegerAttribute.IntegerMinimum}"/>
          <my:Property my:Name="DefaultValue" my:Value="1"/>
          <my:Property my:Name="Value" my:Value="{Binding Source=object, Path=AnIntegerAttribute, Mode=TwoWay}"/>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=AnIntegerAttribute.Required}"/>
     </my:Properties>
</my:Control>
<!--End of sample for a dynamically numeric box.-->
```


### <a name="uocpicturebox"></a>UocPictureBox

Имя: UocPictureBox.

Описание: этот элемент управления используется, чтобы преобразовать изображение для просмотра (данные двоичного типа). Рекомендуем использовать этот элемент управления с данными двоичного типа. Изображение можно преобразовать для просмотра, использовав указанный URL-адрес, данные двоичного типа или источник атрибута, который содержит данные типа изображения.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  ImageUrl: это необязательное свойство строкового типа. Введите URL-адрес целевого изображения.

3.  MaxHeight: это необязательное свойство строкового типа. Оно определяет максимальную высоту изображения, которое преобразуется для просмотра, в пикселях.

4.  MaxWidth: это необязательное свойство строкового типа. Оно определяет максимальную ширину изображения, которое преобразуется для просмотра, в пикселях.

5.  ImageData: это свойство логического типа. Используйте это свойство для привязки источника данных к отображаемому изображению. Данные в источнике, для которого создается привязка, должны быть двоичными.
    Это поле также можно использовать, чтобы явно задать изображение, предоставив данные в формате byte[].

6.  ImageResource: это необязательное свойство двоичного типа.

7.  AlternativeText: это необязательное свойство строкового типа. Это свойство выводит альтернативный текст, если не удается отобразить изображение.

Пример:

>[!NOTE]
Чтобы использовать этот пример, необходимо привязать существующие данные изображения к элементу управления.


В следующем фрагменте кода создается элемент управления "Поле изображения", которое привязывает источник данных к элементу управления:

```
<!--Sample for a Picture Box control binding with a data source-->
<my:Control my:Name="SamplePictureBoxImageData" my:TypeName="UocPictureBox" my:RightsLevel="{Binding Source=rights, Path=Photo}">
     <my:Properties>
          <my:Property my:Name="MaxHeight" my:Value="100" />
          <my:Property my:Name="MaxWidth" my:Value="100" />
          <my:Property my:Name="ImageData" my:Value="{Binding Source=object, Path=Photo}" />
     </my:Properties>
</my:Control>
<!--End of Sample for a Picture Box control-->
```

В следующем фрагменте кода создается элемент управления "Поле изображения", которое привязывает URL-адрес изображения к элементу управления:

```
<!--Sample for a Picture Box control bind with explicit URL-->
<my:Control my:Name="SamplePictureBoxImageUrl" my:TypeName="UocPictureBox">
     <my:Properties>
          <my:Property my:Name="MaxHeight" my:Value="100" />
          <my:Property my:Name="MaxWidth" my:Value="100" />
          <my:Property my:Name="ImageUrl" my:Value="http://www.microsoft.com/dummypicture.jpg" />
     </my:Properties>
</my:Control>
<!--End of Sample for a Picture Box control-->
```

### <a name="uocradiobuttonlist"></a>UocRadioButtonList

Имя: UocRadioButtonList.

Описание: это простой список переключателей. Варианты в этом списке являются взаимоисключающими. Рекомендуем использовать этот элемент управления, если в списке пять или менее вариантов для выбора. В других случаях рекомендуем использовать UOCListView.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  ValuePath: путь к значению в поле Value. Свойство привязывается к полю Value в элементе Option, который рассматривается в этом документе.

3.  CaptionPath: путь к значению в поле Caption. Свойство привязывается к полю Caption в элементе Option, который рассматривается в этом документе.

4.  HintPath: путь к значению в поле Hint. Свойство привязывается к полю Hint в элементе Option, который рассматривается в этом документе.

5.  SelectedValue: выбранное значение. Это обязательное свойство строкового типа. Оно привязывается к строковым данным из источника данных.

События:

1.  SelectedIndexChanged

2.  CheckedChanged

Параметры

В параметрах для этого элемента управления можно использовать только два элемента Option.

1.  Value: для поля Value в одном элементе Option должно быть задано значение true или false.

2.  Caption: может быть любым строковым значением.

3.  Hint: может быть любым строковым значением.

Пример.

![](media/rcd-configuration-xml-reference/image063.jpg)

>[!NOTE]
Чтобы пример работал, создайте логический атрибут ABooleanAttribute и привяжите его к типу настраиваемого ресурса.

В следующем фрагменте кода создается список переключателей, представленный на изображении выше:

```
<!--Sample for option button list control-->
<my:Control my:Name="SampleRadioButtonList" my:TypeName="UocRadioButtonList" my:Caption="{Binding Source=schema, Path=ABooleanAttribute.DisplayName}" my:Description="{Binding Source=schema, Path=ABooleanAttribute.Description}" my:RightsLevel="{Binding Source=rights, Path=ABooleanAttribute}">
     <my:Options>
          <my:Option my:Value="False" my:Caption="Set Value To False" my:Hint="By selecting this option, you are setting the value of the attribute to false." />
          <my:Option my:Value="True" my:Caption="Set Value To True" my:Hint="By selecting this option, you are setting the value of the attribute to true." />
     </my:Options>
     <my:Properties>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=ABooleanAttribute.Required}" />
          <my:Property my:Name="ValuePath" my:Value="Value" />
          <my:Property my:Name="CaptionPath" my:Value="Caption" />
          <my:Property my:Name="HintPath" my:Value="Hint" />
          <my:Property my:Name="SelectedValue" my:Value="{Binding Source=object, Path=ABooleanAttribute, Mode=TwoWay}" />
     </my:Properties>
</my:Control>
<!--End of Sample for option button list control-->
```


### <a name="uocsimpleradiobutton"></a>UocSimpleRadioButton


Имя: UocSimpleRadioButton.

Описание: это простой элемент управления "Переключатель". Он используется так же, как и для простой флажок. Существует два переключателя, которые отображаются одновременно с текстовой подписью. Рекомендуем привязать элемент управления к данным логического типа.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  TrueText: это необязательное свойство строкового типа. Это текст, который отображается, когда переключатель выбран.

3.  FalseText: это необязательное свойство строкового типа. Это текст, который отображается, когда переключатель не выбран.

4.  SelectedItem: это необязательное свойство логического типа. Это значение указывает, что переключатель выбран. Свойство можно привязать к данным логического типа из источника данных. По умолчанию задано значение false.

События:

   • CheckedChanged: это событие возникает, когда состояние переключателя изменяется с выбранного на невыбранное и наоборот.

Пример.

![](media/rcd-configuration-xml-reference/image066.png)

>[!NOTE]
Чтобы пример работал, создайте логический атрибут ABooleanAttribute и привяжите его к типу настраиваемого ресурса. Данные RCDC данных применяются к одному типу настраиваемого ресурса.

В следующем фрагменте кода создается переключатель, представленный на изображении выше:

```
<!--Sample for simple option button control-->
<my:Control my:Name="SampleSimpleRadioButton" my:TypeName="UocSimpleRadioButton" my:Caption="{Binding Source=schema, Path=ABooleanAttribute.DisplayName}" my:Description="{Binding Source=schema, Path=ABooleanAttribute.Description}" my:RightsLevel="{Binding Source=rights, Path=ABooleanAttribute}">
     <my:Properties>
          <my:Property my:Name="Required" my:Value="{Binding Source=schema, Path=ABooleanAttribute.Required}" />
          <my:Property my:Name="FalseText" my:Value="False"/>
          <my:Property my:Name="TrueText" my:Value="True"/>
          <my:Property my:Name="SelectedItem" my:Value="{Binding Source=object, Path=ABooleanAttribute, Mode=TwoWay}" />
     </my:Properties>
</my:Control>
<!--End of Sample for simple option button control-->
```


### <a name="uoctextbox"></a>UocTextBox

Имя: UocTextBox

Описание: это простое текстовое поле для ввода данных строкового типа. Рекомендуем использовать этот элемент управления для привязки к данным строкового типа.

Свойства:

1.  Все общие свойства: дополнительные сведения см. в разделе "Общие свойства" этого документа.

2.  MaxLength: это необязательный атрибут целочисленного типа. Это свойство указывает максимальную длину входной строки. По умолчанию для этого свойства задано значение 128 символов.

3.  Text: это необязательное свойство строкового типа. Это текст, отображаемый в текстовом поле. Можно определить явно заданные строки, которые отображаются в текстовом поле при начальной загрузке элемента управления, или привязать его к атрибуту схемы строкового типа.

4.  Rows: это необязательное свойство целочисленного типа. Это свойство определяет высоту текстового поля в символах. Значение по умолчанию — 1 символ.

5.  Columns: это необязательное свойство целочисленного типа. Это свойство определяет ширину текстового поля в символах. Значение по умолчанию — 20 символов.

6.  Wrap: это необязательное свойство логического типа. Установив для этого свойства значение true, пользователь включает функцию переноса по словам в текстовом поле. По умолчанию для этого свойства задано значение true.

7.  UniquenessValidationXPath: это необязательное свойство строкового типа. Оно принимает допустимое выражение фильтра XPath FIM и обеспечивает уникальность значения, введенного пользователем, в рамках ресурсов в области фильтра.
    Например, чтобы убедиться, что запрашиваемое пользователем отображаемое имя является уникальным в пределах всех групп безопасности с поддержкой почты в базе данных службы FIM, используется выражение XPath `/Group[DisplayName=’%VALUE%’ and Type=’MailEnabledSecurity’`. Действие проверки выполняется, когда пользователь покидает страницу. Это свойство поддерживается только в RCDC для создания ресурса.

8.  UniquenessErrorMessage: это необязательное свойство строкового типа. Эта строка используется для отображения сообщения об ошибке, если происходит сбой проверки UniquenessValidationXPath, и может быть явно заданным текстом или строковой переменной ресурса. Если это свойство не задано, по умолчанию для сообщения об ошибке проверки задан текст "Значение %VALUE% уже существует. Попробуйте указать другое".

События:

   • TextChanged: это событие возникает, если текст в текстовом поле изменен.

Полный пример кода для этого элемента управления см. в разделе примеров для простых элементов управления.

## <a name="appendix-a-default-xsd-schema"></a>Приложение A. Стандартная схема XSD

Ниже приведена полная схема XSD для всех RCDC по умолчанию, предоставляемых с Microsoft Identity Manager 2016 SP1:

```XML
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<xsd:schema targetNamespace="http://schemas.microsoft.com/2006/11/ResourceManagement" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:my="http://schemas.microsoft.com/2006/11/ResourceManagement" xmlns:xd="http://schemas.microsoft.com/office/infopath/2003" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <xsd:attribute name="TypeName" type="my:requiredString"/>
    <xsd:attribute name="Name" type="my:requiredAlphanumericString"/>
    <xsd:attribute name="Parameters" type="xsd:string"/>
    <xsd:attribute name="DisplayAsWizard" type="xsd:boolean"/>
    <xsd:attribute name="Caption" type="xsd:string"/>
    <xsd:attribute name="AutoValidate" type="xsd:boolean"/>
    <xsd:attribute name="Enabled" type="xsd:string"/>
    <xsd:attribute name="Visible" type="xsd:string"/>
    <xsd:attribute name="IsSummary" type="xsd:boolean"/>
    <xsd:attribute name="IsHeader" type="xsd:boolean"/>
    <xsd:attribute name="HelpText" type="xsd:string"/>
    <xsd:attribute name="Link" type="xsd:string"/>
    <xsd:attribute name="Description" type="xsd:string"/>
    <xsd:attribute name="ExpandArea" type="xsd:boolean"/>
    <xsd:attribute name="Hint" type="xsd:string"/>
    <xsd:attribute name="AutoPostback" type="xsd:string"/>
    <xsd:attribute name="RightsLevel" type="my:requiredString"/>
    <xsd:attribute name="Value" type="xsd:string"/>
    <xsd:attribute name="Handler" type="my:requiredString"/>
    <xsd:attribute name="ImageUrl" type="xsd:string"/>
    <xsd:attribute name="RedirectUrl" type="xsd:string"/>
    <xsd:attribute name="ClickBehavior" type="xsd:string"/>
    <xsd:attribute name="EnableMode" type="xsd:string"/>
    <xsd:attribute name="ValueType" type="xsd:string"/>
    <xsd:attribute name="Condition" type="xsd:string"/>
    <xsd:element name="ObjectControlConfiguration">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:ObjectDataSource" minOccurs="0" maxOccurs="32"/>
                <xsd:element ref="my:XmlDataSource" minOccurs="0" maxOccurs="32"/>
                <xsd:element ref="my:Panel"/>
                <xsd:element ref="my:Events" minOccurs="0" maxOccurs="1"/>
            </xsd:sequence>
            <xsd:attribute ref="my:TypeName"/>
            <xsd:anyAttribute processContents="lax" namespace="http://www.w3.org/XML/1998/namespace"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="ObjectDataSource">
        <xsd:complexType>
            <xsd:sequence/>
            <xsd:attribute ref="my:TypeName"/>
            <xsd:attribute ref="my:Name"/>
            <xsd:attribute ref="my:Parameters"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="XmlDataSource">
        <xsd:complexType  mixed="true">
      <xsd:sequence>
        <xsd:any minOccurs="0" maxOccurs="unbounded" processContents="lax"/>
      </xsd:sequence>
      <xsd:attribute ref="my:Name"/>
      <xsd:attribute ref="my:Parameters"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Panel">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:Grouping" minOccurs="1" maxOccurs="16"/>
            </xsd:sequence>
            <xsd:attribute ref="my:Name"/>
            <xsd:attribute ref="my:DisplayAsWizard"/>
            <xsd:attribute ref="my:Caption"/>
            <xsd:attribute ref="my:AutoValidate"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Grouping">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:Help" minOccurs="0"  maxOccurs="1"/>
                <xsd:element ref="my:Control" minOccurs="1" maxOccurs="256"/>
                <xsd:element ref="my:Events" minOccurs="0" maxOccurs="1"/>
            </xsd:sequence>
            <xsd:attribute ref="my:Name"/>
            <xsd:attribute ref="my:Caption"/>
            <xsd:attribute ref="my:Description"/>
            <xsd:attribute ref="my:Enabled"/>
            <xsd:attribute ref="my:Visible"/>
            <xsd:attribute ref="my:IsHeader"/>
            <xsd:attribute ref="my:IsSummary"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Help">
        <xsd:complexType>
            <xsd:sequence/>
            <xsd:attribute ref="my:HelpText"/>
            <xsd:attribute ref="my:Link"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Control">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:Help" minOccurs="0"  maxOccurs="1"/>
                <xsd:element ref="my:CustomProperties" minOccurs="0"  maxOccurs="1"/>
                <xsd:element ref="my:Options" minOccurs="0"  maxOccurs="1"/>
                <xsd:element ref="my:Buttons" minOccurs="0"  maxOccurs="1"/>
                <xsd:element ref="my:Properties" minOccurs="0"  maxOccurs="1"/>
                <xsd:element ref="my:Events" minOccurs="0" maxOccurs="1"/>
            </xsd:sequence>
            <xsd:attribute ref="my:Name"/>
            <xsd:attribute ref="my:TypeName"/>
            <xsd:attribute ref="my:Caption"/>
            <xsd:attribute ref="my:Enabled"/>
            <xsd:attribute ref="my:Visible"/>
            <xsd:attribute ref="my:Description"/>
            <xsd:attribute ref="my:ExpandArea"/>
            <xsd:attribute ref="my:Hint"/>
            <xsd:attribute ref="my:AutoPostback"/>
            <xsd:attribute ref="my:RightsLevel"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="CustomProperties">
        <xsd:complexType mixed="true">
            <xsd:sequence>
                <xsd:any minOccurs="0" maxOccurs="unbounded" namespace="##targetNamespace" processContents="lax"/>
            </xsd:sequence>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Options">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:Option" minOccurs="0" maxOccurs="unbounded"/>
            </xsd:sequence>
            <xsd:attribute ref="my:ValueType"/>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Option">
        <xsd:complexType>
            <xsd:simpleContent>
                <xsd:extension base="xsd:string">
                    <xsd:attribute ref="my:Value"/>
                    <xsd:attribute ref="my:Caption"/>
                    <xsd:attribute ref="my:Hint"/>
                </xsd:extension>
            </xsd:simpleContent>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Buttons">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:Button" minOccurs="1" maxOccurs="8"/>
            </xsd:sequence>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Button">
        <xsd:complexType>
            <xsd:simpleContent>
                <xsd:extension base="xsd:string">
                    <xsd:attribute ref="my:Name"/>
                    <xsd:attribute ref="my:Caption"/>
                    <xsd:attribute ref="my:Hint"/>
                    <xsd:attribute ref="my:ImageUrl"/>
                    <xsd:attribute ref="my:ClickBehavior"/>
                    <xsd:attribute ref="my:RedirectUrl"/>
                    <xsd:attribute ref="my:Enabled"/>
                    <xsd:attribute ref="my:Visible"/>
                    <xsd:attribute ref="my:EnableMode"/>
                </xsd:extension>
            </xsd:simpleContent>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Properties">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:Property" minOccurs="1" maxOccurs="32"/>
            </xsd:sequence>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Property">
        <xsd:complexType>
            <xsd:simpleContent>
                <xsd:extension base="xsd:string">
                    <xsd:attribute ref="my:Name"/>
                    <xsd:attribute ref="my:Value"/>
                    <xsd:attribute ref="my:Condition"/>                 
                </xsd:extension>
            </xsd:simpleContent>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Events">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element ref="my:Event" minOccurs="1" maxOccurs="16"/>
            </xsd:sequence>
        </xsd:complexType>
    </xsd:element>
    <xsd:element name="Event">
        <xsd:complexType>
            <xsd:simpleContent>
                <xsd:extension base="xsd:string">
                    <xsd:attribute ref="my:Name"/>
                    <xsd:attribute ref="my:Handler"/>
          <xsd:attribute ref="my:Parameters"/>
        </xsd:extension>
            </xsd:simpleContent>
        </xsd:complexType>
    </xsd:element>
    <xsd:simpleType name="requiredString">
        <xsd:restriction base="xsd:string">
            <xsd:minLength value="1"/>
        </xsd:restriction>
    </xsd:simpleType>
  <xsd:simpleType name="requiredAlphanumericString">
    <xsd:restriction base="xsd:string">
      <xsd:pattern value="[A-Za-z0-9_]{1,128}"/>
    </xsd:restriction>
  </xsd:simpleType>
    <xsd:simpleType name="requiredAnyURI">
        <xsd:restriction base="xsd:anyURI">
            <xsd:minLength value="1"/>
        </xsd:restriction>
    </xsd:simpleType>
    <xsd:simpleType name="requiredBase64Binary">
        <xsd:restriction base="xsd:base64Binary">
            <xsd:minLength value="1"/>
        </xsd:restriction>
    </xsd:simpleType>
</xsd:schema>
```



## <a name="appendix-b-default-summary-xsl"></a>Приложение B. Стандартный XSL-код сводки

Ниже приведен полный XSL-код сводки, предоставляемый с Microsoft Identity Manager 2016 SP1:
```XML
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:msxsl="urn:schemas-microsoft-com:xslt">
  <xsl:template name="output-attribute-value">
    <xsl:param name="attribute"/>
    <xsl:param name="type"/>
    <xsl:choose>
      <xsl:when test="$type='Binary'">
        <xsl:value-of select="$attribute" disable-output-escaping="yes"/>
      </xsl:when>
      <xsl:when test="$type='Text'">
        <xsl:text xml:space="preserve" disable-output-escaping="yes">(text data)</xsl:text>
      </xsl:when>
      <xsl:otherwise>
        <xsl:value-of select="translate($attribute,' ','&#160;')" disable-output-escaping="yes"/>
      </xsl:otherwise>
    </xsl:choose>
  </xsl:template>

  <xsl:template name="output-modified-value">
    <xsl:param name="name"/>
    <xsl:param name="attribute1"/>
    <xsl:param name="text1"/>
    <xsl:param name="attribute2"/>
    <xsl:param name="text2"/>
    <xsl:param name="type"/>
    <tr class="listViewRow" style="height:22px;">
      <xsl:if test="position() mod 2 != 0">
        <td class="commonSummaryListViewCellBR ms-vb">
          <xsl:value-of select="$name" disable-output-escaping="yes"/>
        </td>
        <xsl:choose>
          <xsl:when test="$attribute1 and $attribute1!=''">
            <td class="commonSummaryListViewCellBR ms-vb">
              <xsl:call-template name="output-attribute-value">
                <xsl:with-param name="attribute" select="$attribute1"/>
                <xsl:with-param name="type" select="$type"/>
              </xsl:call-template>
            </td>
          </xsl:when>
          <xsl:otherwise>
            <td class="commonSummaryListViewCellBR ms-vb">
              <xsl:copy-of select="$text1"/>
            </td>
          </xsl:otherwise>
        </xsl:choose>
        <xsl:choose>
          <xsl:when test="$attribute2 and $attribute2!=''">
            <td class="commonSummaryListViewCellBR ms-vb">
              <xsl:call-template name="output-attribute-value">
                <xsl:with-param name="attribute" select="$attribute2"/>
                <xsl:with-param name="type" select="$type"/>
              </xsl:call-template>
            </td>
          </xsl:when>
          <xsl:otherwise>
            <td class="commonSummaryListViewCellBR ms-vb">
              <xsl:copy-of select="$text2"/>
            </td>
          </xsl:otherwise>
        </xsl:choose>
      </xsl:if>
      <xsl:if test="position() mod 2 != 1">
        <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
          <xsl:value-of select="$name" disable-output-escaping="yes"/>
        </td>
        <xsl:choose>
          <xsl:when test="$attribute1 and $attribute1!=''">
            <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
              <xsl:call-template name="output-attribute-value">
                <xsl:with-param name="attribute" select="$attribute1"/>
                <xsl:with-param name="type" select="$type"/>
              </xsl:call-template>
            </td>
          </xsl:when>
          <xsl:otherwise>
            <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
              <xsl:copy-of select="$text1"/>
            </td>
          </xsl:otherwise>
        </xsl:choose>
        <xsl:choose>
          <xsl:when test="$attribute2 and $attribute2!=''">
            <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
              <xsl:call-template name="output-attribute-value">
                <xsl:with-param name="attribute" select="$attribute2"/>
                <xsl:with-param name="type" select="$type"/>
              </xsl:call-template>
            </td>
          </xsl:when>
          <xsl:otherwise>
            <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
              <xsl:copy-of select="$text2"/>
            </td>
          </xsl:otherwise>
        </xsl:choose>
      </xsl:if>
    </tr>
  </xsl:template>

  <xsl:template name="output-localized-attribute-value">
    <xsl:param name="locale"/>
    <xsl:param name="attribute"/>
    <xsl:param name="type"/>
    <tr class="listViewRow" style="height:22px;">
      <xsl:if test="position() mod 2 != 0">
        <td class="commonSummaryListViewCellBR ms-vb">
          <xsl:value-of select="$locale" disable-output-escaping="yes"/>
        </td>
        <td class="commonSummaryListViewCellBR ms-vb">
          <xsl:call-template name="output-attribute-value">
            <xsl:with-param name="attribute" select="$attribute"/>
            <xsl:with-param name="type" select="$type"/>
          </xsl:call-template>
        </td>
      </xsl:if>
      <xsl:if test="position() mod 2 != 1">
        <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
          <xsl:value-of select="$locale" disable-output-escaping="yes"/>
        </td>
        <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
          <xsl:call-template name="output-attribute-value">
            <xsl:with-param name="attribute" select="$attribute"/>
            <xsl:with-param name="type" select="$type"/>
          </xsl:call-template>
        </td>
      </xsl:if>
    </tr>
  </xsl:template>

  <xsl:template match="/">
    <xsl:choose>
      <xsl:when test="ModifiedAttributes[@ActionType='Create']">
        <!-- expected XML
        <ModifiedAttributes ActionType="Create">
          <Attribute Name="[attribute's system name]" DisplayName="[attribute's display name]" DataType="[all kinds of ILM data type]" InitializedValue="[the value]"/>
          other <Attribute> elements
        </ModifiedAttributes>
        -->
        <table cellspacing="0" cellpadding="3" class="commonSummaryListViewGridBorder">
          <tr align="left" class="listViewHeader" style="height:22px;">
            <th class="commonSummaryListViewHeaderCellBR">Attribute</th>
            <th class="commonSummaryListViewHeaderCellBR">Value</th>
          </tr>
          <xsl:for-each select="ModifiedAttributes/Attribute">
            <xsl:sort select="@DisplayName" order="ascending"/>
            <tr class="listViewRow" style="height:22px;">
              <xsl:if test="position() mod 2 != 0">
                <td class="commonSummaryListViewCellBR ms-vb">
                  <xsl:value-of select="@DisplayName" disable-output-escaping="yes"/>
                </td>
                <xsl:if test="count(LocalizedValue)!=0">
                  <td class="commonSummaryListViewCellBR ms-vb">
                    <table cellspacing="0" style="width:100%">
                      <tr class="listViewHeader">
                        <th align="left" class="commonSummaryListViewHeaderCellBR">Language</th>
                        <th align="left" class="commonSummaryListViewHeaderCellBR">Status</th>
                      </tr>
                      <xsl:if test="@InitializedValue and @InitializedValue != ''">
                        <xsl:call-template name="output-localized-attribute-value">
                          <xsl:with-param name="locale" select="@Locale"/>
                          <xsl:with-param name="attribute" select="@InitializedValue"/>
                          <xsl:with-param name="type" select="@DataType"/>
                        </xsl:call-template>
                      </xsl:if>
                      <xsl:for-each select="LocalizedValue">
                        <xsl:call-template name="output-localized-attribute-value">
                          <xsl:with-param name="locale" select="@Locale"/>
                          <xsl:with-param name="attribute" select="@InitializedValue"/>
                          <xsl:with-param name="type" select="../@DataType"/>
                        </xsl:call-template>
                      </xsl:for-each>
                    </table>
                  </td>
                </xsl:if>
                <xsl:if test="count(LocalizedValue)=0">
                  <td class="commonSummaryListViewCellBR ms-vb">
                    <xsl:call-template name="output-attribute-value">
                      <xsl:with-param name="attribute" select="@InitializedValue"/>
                      <xsl:with-param name="type" select="@DataType"/>
                    </xsl:call-template>
                  </td>
                </xsl:if>
              </xsl:if>
              <xsl:if test="position() mod 2 != 1">
                <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
                  <xsl:value-of select="@DisplayName" disable-output-escaping="yes"/>
                </td>
                <xsl:if test="count(LocalizedValue)!=0">
                  <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
                    <table cellspacing="0" style="width:100%">
                      <tr class="listViewHeader">
                        <th align="left" class="commonSummaryListViewHeaderCellBR">Language</th>
                        <th align="left" class="commonSummaryListViewHeaderCellBR">Status</th>
                      </tr>
                      <xsl:if test="@InitializedValue and @InitializedValue != ''">
                        <xsl:call-template name="output-localized-attribute-value">
                          <xsl:with-param name="locale" select="@Locale"/>
                          <xsl:with-param name="attribute" select="@InitializedValue"/>
                          <xsl:with-param name="type" select="@DataType"/>
                        </xsl:call-template>
                      </xsl:if>
                      <xsl:for-each select="LocalizedValue">
                        <xsl:call-template name="output-localized-attribute-value">
                          <xsl:with-param name="locale" select="@Locale"/>
                          <xsl:with-param name="attribute" select="@InitializedValue"/>
                          <xsl:with-param name="type" select="../@DataType"/>
                        </xsl:call-template>
                      </xsl:for-each>
                    </table>
                  </td>
                </xsl:if>
                <xsl:if test="count(LocalizedValue)=0">
                  <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
                    <xsl:call-template name="output-attribute-value">
                      <xsl:with-param name="attribute" select="@InitializedValue"/>
                      <xsl:with-param name="type" select="@DataType"/>
                    </xsl:call-template>
                  </td>
                </xsl:if>
              </xsl:if>
            </tr>
          </xsl:for-each>
        </table>
      </xsl:when>
      <xsl:when test="ModifiedAttributes[@ActionType='Modify']">
        <!-- expected XML
        <ModifiedAttributes ActionType="Modify">
          <SingleAttribute Name="[attribute's system name]" DisplayName="[attribute's display name]" DataType="[all kinds of ILM data type]" InitializedValue="[the old value]" SetValue="[the new value]"/>
          other <SingleAttribute> elements
          <MultipleAttribute Name="[attribute's system name]" DisplayName="[attribute's display name]" DataType="[all kinds of ILM data type]" InsertedItem="[inserted items separated by ';']" RemovedItem="[removed items separated by ';']"/>
          other <MultipleAttribute> elements
        </ModifiedAttributes>
        -->
        <table class="commonSummaryListViewGridBorder" cellspacing="0" cellpadding="3">
          <xsl:if test="ModifiedAttributes[count(SingleAttribute)!=0]">
            <tr align="left" class="listViewHeader">
              <th class="commonSummaryListViewHeaderCellBR">Single-Value Attributes</th>
              <th class="commonSummaryListViewHeaderCellBR">Old Value</th>
              <th class="commonSummaryListViewHeaderCellBR">New Value</th>
            </tr>
            <xsl:for-each select="ModifiedAttributes/SingleAttribute">
              <xsl:sort select="@DisplayName" order="ascending"/>
              <xsl:if test="count(LocalizedValue)!=0">
                <tr class="listViewRow">
                  <xsl:if test="position() mod 2 != 0">
                    <td class="commonSummaryListViewCellBR ms-vb">
                      <xsl:value-of select="@DisplayName" disable-output-escaping="yes"/>
                    </td>
                    <td colSpan="2">
                      <table cellspacing="0" cellpadding="0" style="width:100%">
                        <tr align="left" class="listViewHeader">
                          <th class="commonSummaryListViewHeaderCellBR">Language</th>
                          <th class="commonSummaryListViewHeaderCellBR">Old Value</th>
                          <th class="commonSummaryListViewHeaderCellBR">New Value</th>
                        </tr>
                        <xsl:if test="(@InitializedValue and @InitializedValue !='') or (@SetValue and @SetValue != '')">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@InitializedValue"/>
                            <xsl:with-param name="text1">(no initial value)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@SetValue"/>
                            <xsl:with-param name="text2">(value removed)</xsl:with-param>
                            <xsl:with-param name="type" select="@DataType"/>
                          </xsl:call-template>
                        </xsl:if>
                        <xsl:for-each select="LocalizedValue">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@InitializedValue"/>
                            <xsl:with-param name="text1">(no initial value)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@SetValue"/>
                            <xsl:with-param name="text2">(value removed)</xsl:with-param>
                            <xsl:with-param name="type" select="../@DataType"/>
                          </xsl:call-template>
                        </xsl:for-each>
                      </table>
                    </td>
                  </xsl:if>
                  <xsl:if test="position() mod 2 != 1">
                    <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
                      <xsl:value-of select="@DisplayName" disable-output-escaping="yes"/>
                    </td>
                    <td colSpan="2">
                      <table cellspacing="0" style="width:100%">
                        <tr align="left" class="listViewHeader">
                          <th class="commonSummaryListViewHeaderCellBR">Language</th>
                          <th class="commonSummaryListViewHeaderCellBR">Old Value</th>
                          <th class="commonSummaryListViewHeaderCellBR">New Value</th>
                        </tr>
                        <xsl:if test="(@InitializedValue and @InitializedValue !='') or (@SetValue and @SetValue != '')">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@InitializedValue"/>
                            <xsl:with-param name="text1">(no initial value)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@SetValue"/>
                            <xsl:with-param name="text2">(value removed)</xsl:with-param>
                            <xsl:with-param name="type" select="@DataType"/>
                          </xsl:call-template>
                        </xsl:if>
                        <xsl:for-each select="LocalizedValue">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@InitializedValue"/>
                            <xsl:with-param name="text1">(no initial value)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@SetValue"/>
                            <xsl:with-param name="text2">(value removed)</xsl:with-param>
                            <xsl:with-param name="type" select="../@DataType"/>
                          </xsl:call-template>
                        </xsl:for-each>
                      </table>
                    </td>
                  </xsl:if>
                </tr>
              </xsl:if>
              <xsl:if test="count(LocalizedValue)=0">
                <xsl:call-template name="output-modified-value">
                  <xsl:with-param name="name" select="@DisplayName"/>
                  <xsl:with-param name="attribute1" select="@InitializedValue"/>
                  <xsl:with-param name="text1">(no initial value)</xsl:with-param>
                  <xsl:with-param name="attribute2" select="@SetValue"/>
                  <xsl:with-param name="text2">(value removed)</xsl:with-param>
                  <xsl:with-param name="type" select="@DataType"/>
                </xsl:call-template>
              </xsl:if>
            </xsl:for-each>
          </xsl:if>
          <xsl:if test="ModifiedAttributes[count(MultipleAttribute)!=0]">
            <tr align="left" class="listViewHeader">
              <th class="commonSummaryListViewHeaderCellBR">Multiple-Value Attributes</th>
              <th class="commonSummaryListViewHeaderCellBR">Removed Items</th>
              <th class="commonSummaryListViewHeaderCellBR">Inserted Items</th>
            </tr>
            <xsl:for-each select="ModifiedAttributes/MultipleAttribute">
              <xsl:sort select="@DisplayName" order="ascending"/>
              <xsl:if test="count(LocalizedValue)!=0">
                <tr class="uocSummaryTitleTR">
                  <xsl:if test="position() mod 2 != 0">
                    <td class="commonSummaryListViewCellBR ms-vb">
                      <xsl:value-of select="@DisplayName" disable-output-escaping="yes"/>
                    </td>
                    <td>
                      <table cellspacing="0" style="width:100%">
                        <tr align="left" class="listViewHeader">
                          <th class="commonSummaryListViewHeaderCellBR">Language</th>
                          <th class="commonSummaryListViewHeaderCellBR">Removed Items</th>
                          <th class="commonSummaryListViewHeaderCellBR">Inserted Items</th>
                        </tr>
                        <xsl:if test="(@RemovedItem and @RemovedItem!='') or (@InsertedItem and @InsertedItem!='')">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@RemovedItem"/>
                            <xsl:with-param name="text1">(no removed item)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@InsertedItem"/>
                            <xsl:with-param name="text2">(no inserted item)</xsl:with-param>
                            <xsl:with-param name="type" select="@DataType"/>
                          </xsl:call-template>
                        </xsl:if>
                        <xsl:for-each select="LocalizedValue">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@RemovedItem"/>
                            <xsl:with-param name="text1">(no removed item)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@InsertedItem"/>
                            <xsl:with-param name="text2">(no inserted item)</xsl:with-param>
                            <xsl:with-param name="type" select="@DataType"/>
                          </xsl:call-template>
                        </xsl:for-each>
                      </table>
                    </td>
                  </xsl:if>
                  <xsl:if test="position() mod 2 != 1">
                    <td class="ms-alternating commonSummaryListViewCellBR ms-vb">
                      <xsl:value-of select="@DisplayName" disable-output-escaping="yes"/>
                    </td>
                    <td>
                      <table cellspacing="0" style="width:100%">
                        <tr align="left" class="listViewHeader">
                          <th class="commonSummaryListViewHeaderCellBR">Language</th>
                          <th class="commonSummaryListViewHeaderCellBR">Removed Items</th>
                          <th class="commonSummaryListViewHeaderCellBR">Inserted Items</th>
                        </tr>
                        <xsl:if test="(@RemovedItem and @RemovedItem!='') or (@InsertedItem and @InsertedItem!='')">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@RemovedItem"/>
                            <xsl:with-param name="text1">(no removed item)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@InsertedItem"/>
                            <xsl:with-param name="text2">(no inserted item)</xsl:with-param>
                            <xsl:with-param name="type" select="@DataType"/>
                          </xsl:call-template>
                        </xsl:if>
                        <xsl:for-each select="LocalizedValue">
                          <xsl:call-template name="output-modified-value">
                            <xsl:with-param name="name" select="@Locale"/>
                            <xsl:with-param name="attribute1" select="@RemovedItem"/>
                            <xsl:with-param name="text1">(no removed item)</xsl:with-param>
                            <xsl:with-param name="attribute2" select="@InsertedItem"/>
                            <xsl:with-param name="text2">(no inserted item)</xsl:with-param>
                            <xsl:with-param name="type" select="@DataType"/>
                          </xsl:call-template>
                        </xsl:for-each>
                      </table>
                    </td>
                  </xsl:if>
                </tr>
              </xsl:if>
              <xsl:if test="count(LocalizedValue)=0">
                <xsl:call-template name="output-modified-value">
                  <xsl:with-param name="name" select="@DisplayName"/>
                  <xsl:with-param name="attribute1" select="@RemovedItem"/>
                  <xsl:with-param name="text1">(no removed item)</xsl:with-param>
                  <xsl:with-param name="attribute2" select="@InsertedItem"/>
                  <xsl:with-param name="text2">(no inserted item)</xsl:with-param>
                  <xsl:with-param name="type" select="@DataType"/>
                </xsl:call-template>
              </xsl:if>
            </xsl:for-each>
          </xsl:if>
        </table>
      </xsl:when>
    </xsl:choose>
  </xsl:template>
</xsl:stylesheet>
```

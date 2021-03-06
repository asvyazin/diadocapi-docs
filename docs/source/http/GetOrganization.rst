GetOrganization
===============

Имя ресурса: **/GetOrganization**

HTTP метод: **GET**

Параметры строки запроса:

-  *orgId*: идентификатор организации (может отсутствовать).

-  *fnsParticipantId*: идентификатор участника электронного документооборота (может отсутствовать).

-  *inn*: ИНН организации (может отсутствовать).

-  *outputFormat*: формат вывода данных, может отсутствовать. Возможные значения: xml, protobuf (по-умолчанию - protobuf).

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

В строке запроса должен присутствовать ровно один параметр из трех: orgId, fnsParticipantId, inn. 

В теле ответа содержатся справочные данные для организации, сериализованные в запрошенном формате:

-  если в строке запроса не было параметра outputFormat, либо его значение было равно protobuf, данные возвращаются сериализованными в протобуфер :doc:`../proto/Organization`;

-  если значение параметра outputFormat в строке запроса было равно xml, данные возвращаются в формате xml, как в следующем примере:

   ::

       <Organization id="orgId1" inn="1234567890" kpp="123456789" fullName="ООО Яблоко" shortName="ООО Яблоко" joinedDiadocTreaty="true">
         <Boxes>
           <Box id="boxId1" title="Ящик для счетов фактур" />
           <Box id="boxId2" title="Тестовый ящик" />
         </Boxes>
       </Organization>

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  404 (Not Found) - организация с указанным идентификатором не найдена в справочнике;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.
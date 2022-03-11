<details style="text-align: center;">
<summary style="padding-bottom: 10px;"><b style="color: #D93221;">GET</b></summary>
<p style="color: #D52A92;">
HTTP метод GET используется для получения (или чтения) представления ресурса. В случае „удачного” (или не содержащего ошибок) адреса, GET возвращается представление ресурса в формате XML или JSON в сочетании с кодом состояния HTTP 200 (OK). В случае наличия ошибок обычно возвращается код 404 (NOT FOUND) или 400 (BAD REQUEST).
В соответствии спецификации HTTP, GET (так же как и HEAD) запросы используются только для чтения данных, не изменя их.<hr>Таким образом, при соблюдении данного соглашения, они считаются безопасными. То есть они могут использоваться без риска изменения данных, вне зависимости от того, один раз данные были получены, или же 10, или ни разу вовсе. GET (а также HEAD) запросы являются идемпотентными (тождественными), что подразумевает получение идентичных данных при использовании одних и тех же запросов (как при единичном обращении, так и при многократном).
Не стоит использовать GET для небезопасных операций над данными, при данном запросе они не должны быть модифицированы.
</p>
</details>

<details style="text-align: center;">
<summary style="padding-bottom: 10px;"><b style="color: #F58A12;">PUT</b></summary>
<p style="color: #19DEFF;">
Метод PUT обычно используется для предоставления возможности обновления ресурса. Тело запроса при отправке PUT-запроса к существующему ресурсу URI должно содержать обновленные данные оригинального ресурса (полностью, или только обновляемую часть).
Кроме того, PUT может быть использован для создания ресурса, в случае, когда идентификатор ресурса выбирает клиент, а не сервер. Или, если перефразировать — при отправке PUT запроса по адресу, содержащему не существующий идентификатор ресурса. Опять же, стоит помнить, что тело запроса должно быть модификацией оригинального ресурса. Многие считают это запутанным и непонятным. Соответственно, данную возможность метода PUT стоит использовать с осторожностью. Да и при крайней необходимости.
Для создания новых экземпляров ресурса предпочтительнее использование POST запроса. В данном случае, при создании экземпляра будет предоставлен корректный идентификатор экземпляра ресурса в возвращённых данных об экземпляре.
При успешном обновлении посредством выполнения PUT запроса возвращается код 200 (или 204 если не был передан какой-либо контент в теле ответа). Если PUT используется для создания экземпляра — обычно возвращают HTTP код 201 при успешном создании. Возвращать данные в ответ на запрос необязательно. Также не обязательно возвращать ссылку на экземпляр ресурса посредством заголовка `Location` по причине того, что клиент и так обладает идентификатором экземпляра ресурса
PUT не безопасная операция, так как вследствие её выполнения происходит модификация (или создание) экземпляров ресурса на стороне сервера, но этот метод идемпотентен. Другими словами, создание или обновление ресурса посредством отправки PUT запроса — ресурс не исчезнет, будет располагаться там же, где и был при первом обращении, а также, многократное выполнение одного и того же PUT запроса не изменит общего состояния системы (за исключением первого раза, но это обычно опускают из рассмотрения)
Если PUT запрос используется для увеличения счётчика просмотра конкретного ресурса — данный запрос уже не считается идемпотентным. Иногда такое происходит и считается достаточным задокументировать тот факт, что вызов не идемпотентен. Однако строго рекомендуется выдерживать идемпотентность PUT запроса.
</p>
</details>

<details style="text-align: center;">
<summary style="padding-bottom: 10px;"><b style="color: #296395;">PATCH</b></summary>
<p style="color: #D93221;">
PATCH запрос используется для **модификации** ресурса. PATCH запрос должен содержать только изменяемые данные ресурса, а не все его данные.
Это напимнает работу PUT запроса, но в теле запроса содержится набор инструкций описывающих как должен быть изменён ресурс, расположенный на сервере, для формирования новой версии. Это означает, что тело PATCH запроса должно содержать не просто изменения ресурса, а представлять из себя описание на языке внесения изменений (patch language) таких как JSON Patch или XML Patch.
PATCH запрос ни является безопасным, ни идемпотентным. Однако PATСH запрос может быть сформирован таким образом чтобы быть идемпотентным, что в свою очередь помогает предотвратить негативные последствия от коллизий между двумя PATCH запросами к одному и тому же ресурсу в один и тот же промежуток времени. Коллизии нескольких PATCH запросов могут быть более опасными чем коллизии PUT запросов, потому что некоторым форматам изменеий необходимо выполняться от известной базовой-точки или ресурс будет поврежден. Клиенты, использующие такой тип внесения изменений, должны использовать условный запрос на проверку изменения ресурса с момента последнего доступа клиента к нему. Например клиент может использовать ETag в заголовке If-Match в самом PATСH запросе.
</p>
</details>

<details style="text-align: center;">
<summary style="padding-bottom: 10px;"><b style="color: #19DEFF;">POST</b></summary>
<p style="color: #296395;">
PATCH запрос используется для **модификации** ресурса. PATCH запрос должен содержать только изменяемые данные ресурса, а не все его данные.
Это напимнает работу PUT запроса, но в теле запроса содержится набор инструкций описывающих как должен быть изменён ресурс, расположенный на сервере, для формирования новой версии. Это означает, что тело PATCH запроса должно содержать не просто изменения ресурса, а представлять из себя описание на языке внесения изменений (patch language) таких как JSON Patch или XML Patch.
PATCH запрос ни является безопасным, ни идемпотентным. Однако PATСH запрос может быть сформирован таким образом чтобы быть идемпотентным, что в свою очередь помогает предотвратить негативные последствия от коллизий между двумя PATCH запросами к одному и тому же ресурсу в один и тот же промежуток времени. Коллизии нескольких PATCH запросов могут быть более опасными чем коллизии PUT запросов, потому что некоторым форматам изменеий необходимо выполняться от известной базовой-точки или ресурс будет поврежден. Клиенты, использующие такой тип внесения изменений, должны использовать условный запрос на проверку изменения ресурса с момента последнего доступа клиента к нему. Например клиент может использовать ETag в заголовке If-Match в самом PATСH запросе.
</p>
</details>

<details style="text-align: center;">
<summary style="padding-bottom: 10px;"><b style="color: #DF1D66;">DELETE</b></summary>
<p style="color: #F58A12;">
DELETE запрос крайне прост для понимания. Он используется для удаления ресурса, идентифицированного конкретным URI (ID).
При успешном удалении возвращается 200 (OK) код HTTP, совместно с телом ответа, содержащим данные удалённого ресурса (отрицательно сказывается на экономии трафика) или завернутые ответы (Смотрите "Возвращаемые данные"). Также возможно использование HTTP кода 204 (NO CONTENT) без тела ответа.
Согласно спецификации HTTP, DELETE запрос идемпотентен. Если вы выполняете DELETE запрос к ресурсу, он удаляется. Повторный DELETE запрос к ресурсу закончится также: ресурс удалён. Если DELETE запрос используется для декремента счётчика, DELETE запрос не является идемпотентным. Используйте POST для неидемпотентных операций.
Тем не менее, существует предостережение об идемпотентности DELETE. Повторный DELETE запрос к ресурсу часто сопровождается 404 (NOT FOUND) кодом HTTP по причине того, что ресурс уже удалён (например из базы данных) и более не доступен. Это делает DELETE операцию не идемпотентной, но это общепринятый компромисс на тот случай, если ресурс был удалён из базы данных, а не помечен, как удалённый.
</p>
</details>
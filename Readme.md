# Типы HTTP-запросов

### HTTP

HTTP — это протокол, позволяющий получать различные ресурсы, например HTML-документы.
HTTP расшифровывается как HyperText Transfer Protocol, «протокол передачи гипертекста». Изначально этот протокол использовался для передачи гипертекстовых документов в формате HTML. Сегодня он используется для передачи произвольных данных.
В основе HTTP - клиент-серверная структура передачи данных․ Клиент формирует запрос (request) и отправляет на сервер; на сервере запрос обрабатывается, формируется ответ (response) и передается клиенту.
Каждое сообщение состоит из трех частей:
1. стартовая строка;
2. заголовки (-это набор пар имя-значение, разделенных двоеточием. В заголовках передается различная служебная информация: кодировка сообщения, название и версия браузера, адрес, с которого пришел клиент (Referrer) и т.д.);
3. тело (это, собственно, передаваемые данные. В ответе передаваемыми данными, как правило, является html-страница, которую запросил браузер, а в запросе, например, в теле сообщения передается содержимое файлов, загружаемых на сервер. Но как правило, тело сообщения в запросе вообще отсутствует).
При этом обязательной является только стартовая строка. Стартовые строки для запроса и ответа имеют различный формат. Рассмотрим только стартовую строку запроса, которая выглядит так:

METHOD URI HTTP/VERSION,

где METHOD — это как раз метод HTTP-запроса, URI — идентификатор ресурса, VERSION — версия протокола.


### Ресурсы и методы:
URI (Uniform Resource Identifier) — единообразный идентификатор ресурса. Ресурс — это, как правило, файл на сервере (пример URI в данном случае '/styles.css'), но вообще ресурсом может являться и какой-либо абстрактный объект ('/blogs/webdev/' — указывает на блок «Веб-разработка», а не на конкретный файл). Тип HTTP-запроса (HTTP-метод) указывает серверу на то, какое действие мы хотим произвести с ресурсом. По протоколу HTTP можно создавать посты, редактировать профиль, удалять сообщения и многое другое.
Для разграничения действий с ресурсами на уровне HTTP-методов были придуманы следующие варианты:
*GET — получение ресурса;
*POST — создание ресурса;
*PUT — обновление ресурса;
*DELETE — удаление ресурса.

### REST:
(REpresentational State Transfer) — это термин был введен в 2000-м году Роем Филдингом (Roy Fielding) — одним из разработчиков протокола HTTP — в качестве названия группы принципов построения веб-приложений. Вообще REST охватывает более широкую область, нежели HTTP — его можно применять и в других сетях с другими протоколами. REST описывает принципы взаимодействия клиента и сервера, основанные на понятиях «ресурса» и «глагола». В случае HTTP ресурс определяется своим URI, а глагол — это HTTP-метод. REST предлагает отказаться от использования одинаковых URI для разных ресурсов (то есть адреса двух разных статей вроде /index.php?article_id=10 и /index.php?article_id=20 — это не REST-way) и использовать разные HTTP-методы для разных действий. Cовместив имеющуюся спецификацию HTTP и REST-подход наконец-то обретают смысл различные HTTP-методы. GET — возвращает ресурс, POST — создает новый, PUT — обновляет существующий, DELETE — удаляет.

PUT/DELETE запросы можно отправлять посредством XMLHttpRequest, посредством обращения к серверу «вручную» (скажем, через curl или даже через telnet), но нельзя сделать HTML-форму, отправляющую полноценный PUT/DELETE-запрос. Дело в том, спецификация HTML не позволяет создавать формы, отправляющие данные иначе, чем через GET или POST. Поэтому для нормальной работы с другими методами приходится имитировать их искусственно. Например, в Rack (механизм, на базе которого Ruby взаимодействует с веб-сервером; с применением Rack сделаны Rails, Merb и другие Ruby-фреймворки) в форму можно добавить hidden-поле с именем "_method", а в качестве значения указать название метода (например, «PUT») — в этом случае будет отправлен POST-запрос, но Rack сможет сделать вид, что получил PUT, а не POST.


#### Метод GET
Метод GET запрашивает информацию из указанного источника и не влияет на его содержимое. Запрос доступен для кеширования данных и добавления в закладки. Длина запроса ограничена (макс. длина URL - 2048);
**Особенности GET запроса**
+может быть закэширован;
+остается в истории браузера;
+может быть закладкой в браузере;
+не должен использоваться при работе с крайне важными данными;
+имеет ограниченную длину;
+должен применяться только для получения данных.
***Никогда не используйте GET запрос для отправки паролей или других критически важных данных!***
#### Метод POST
Метод POST используется для отправки данных, что может оказывать влияние на содержимое ресурса. В отличие от метода GET запросы POST не могут быть кешированы, они не остаются в истории браузера и их нельзя добавить в закладки. Запросы POST не ограничиваются в объеме;


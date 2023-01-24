# Дипломная работа курса Яндекс.Практикум

Содержание:

1. Веб-приложение Яндекс.Самокат
2. Мобильное приложение Яндекс.Самокат
3. API приложения Яндекс.Самокат

# Веб-приложение Яндекс.Самокат

Задачи: 
1. Разработай mindmap функциональности формы заказа. Не забудь, что функциональность — это логика работы и вёрстка.
2. Составь чек-лист по требованиям к функциональности экрана «Статус заказа». 
3. Для экрана «Сделать заказ» составь проверки на валидацию полей. Заполни их в виде таблицы по шаблону.
4. Проведи тестирование всей функциональности не только по получившимся чек-листам/таблицам, но и по остальным макетам и требованиям. 

Решение: 

1. Mindmap

![MindMap_Samokat drawio](https://user-images.githubusercontent.com/112474525/214313508-8e563997-40e6-4110-a2f6-c9b546586d38.png)

Карта в хорошем разрешении: https://drive.google.com/file/d/1-ovVtbl4kUGbAu0azne4oS4LaQHFOaBn/view?usp=sharing

**2. Чек-лист (содержит около 70 пунктов, удобнее смотреть здесь:** https://docs.google.com/spreadsheets/d/1FFXM88Zm93Bazm39KLg4W0Kf2JFtuwpKDm3\_EAehRJ0/edit?usp=sharing 

3. Проверки на валидацию полей с найденными багами  <https://docs.google.com/spreadsheets/d/1qf192cgg5UQW8WUIh2Ji_P8usgpyiROPDjXRXNbFQbQ/edit?usp=sharing> 



# Мобильное приложение Яндекс.Самокат
===============================================================================================================================================================
**Задачи:**
1. Изучи требования к приложению — здесь.

2. Спроектируй тест-кейсы и протестируй функциональность, которая выделена жирным шрифтом. Не забудь написать кейсы и на вёрстку по макетам к этой функциональности. Макеты лежат в Figma здесь.

**Решение:** 
Тест кейс на функциональность + протестированная верстка с багами (<https://docs.google.com/spreadsheets/d/1EdygZtf97uJYWhIrWVnCP7ADKDfWCN6AAgAGPoiiS-w/edit?usp=sharing> )
#
#
# **API приложения Яндекс.Самокат**
ТЗ:  Разработай чек-лист и протестируй API по требованиям.

Чек-лист : 

|**№**|**Запрос**|**Описание проверки**|**Статус**|**Ссылка на баг-репорт**|
| :- | :- | :- | :-: | :- |
|**Создание курьера: POST /api/v1/courier**|
|1|Создать курьера, и проверить что все данные созданного курьера валидны (Логин и пароль в полях проходят авторизацию)<br><br>`    `"login": "ninja",<br>`    `"password": "4321",<br>`    `"firstName": "naruto"|Код и статус ответа 201 OK|**PASSED**| |
|||Ответ на запрос соответствует шаблону|**PASSED**| |
|||Курьер зарегистрирован в приложении|**PASSED**| |
|2|Повторно зарегистрировать курьера с тем же логином и паролем|Код и статус ответа 409 OK|**PASSED**| |
|||Ответ на запрос "Этот логин уже используется. Попробуйте другой."|**PASSED**| |
|||Курьер не зарегистрирован в приложении|**PASSED**| |
|3|Зарегистрировать курьера. Проверить что Логин, хэш пароля и имя курьера<br>должны записываться в поля  login ,<br>passwordHash и firstName таблицы Couriers|Код и статус ответа 201 OK|**PASSED**| |
|||Ответ на запрос соответсвует шаблону|**PASSED**| |
|||Данные внесены в БД| | |
|||Курьер зарегистрирован в приложении|**PASSED**| |
|4|Создать учетную запись для курьера, поле "login" оставить пустым|Код и статус ответа: 400 Bad Request|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер не будет зарегистрирован в приложении|**PASSED**| |
|5|Создать учетную запись для курьера, в поле "login"<br>- ввести 1 символ ("l"),<br>- ввести 11 символов ("loginloginl"),<br>- ввести 12 символов ("loginloginll"),|Код и статус ответа: 400 Bad Request|**FAILED**|<h2>BUG-1120211</h2>|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|6|Создать учетную запись для курьера, в поле "login"<br>- ввести 2 символ ("lo"),<br>- ввести 5 символов ("login"),<br>- ввести 10 символов ("loginlogin")|Код и статус ответа: 201 Created|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер зарегистрирован в приложении|**PASSED**| |
|7|Создать учетную запись для курьера, в поле "login" <br>- ввести  буквы русского языка "логин",|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120213](https://tracker.yandex.ru/BUG-1120213)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|8|Создать учетную запись для курьера, в поле "login" <br>- ввести цифры "login1",<br>- ввести спецсимволы "login$",<br>- ввести пробел "log in"|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120215](https://tracker.yandex.ru/BUG-1120215)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|9|Создать учетную запись для курьера, не вводить строку "password"|Код и статус ответа: 400 Bad Request|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер не будет зарегистрирован в приложении|**PASSED**| |
|10|Создать учетную запись для курьера, не вводить строку "firstName"|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120216](https://tracker.yandex.ru/BUG-1120216)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|11|Создать учетную запись для курьера, поле "password" оставить пустым|Код и статус ответа: 400 Bad Request|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер не будет зарегистрирован в приложении|**PASSED**| |
|12|Создать учетную запись для курьера, в поле "password"<br>- ввести 1 цифру ("1"),<br>- ввести 3 цифры ("123"),<br>- ввести 5 цифр ("12345"),|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120218](https://tracker.yandex.ru/BUG-1120218)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|13|Создать учетную запись для курьера, в поле "password"<br>- ввести 4 цифры ("1234")|Код и статус ответа: 400 Bad Request|**PASSED**| |
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|14|Создать учетную запись для курьера, в поле "password"<br>- ввести русские буквы 4 символа "тест",<br>- ввести английские буквы 4 символа  "test",|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120219](https://tracker.yandex.ru/BUG-1120219)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|15|Создать учетную запись для курьера, в поле "password"<br>- ввести не целое число "0,1",<br>- ввести дробное число "0/1"|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120220](https://tracker.yandex.ru/BUG-1120220)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|16|Создать учетную запись для курьера, в поле "password" <br>- ввести спецсимволы "12!3",<br>- ввести пробел "123 4"|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120221](https://tracker.yandex.ru/BUG-1120221)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|17|Создать учетную запись для курьера, поле "firstName" оставить пустым|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120216](https://tracker.yandex.ru/BUG-1120216)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|18|Создать учетную запись для курьера, в поле "firstName"<br>- ввести 1 символ ("n"),<br>- ввести 11 символов ("namenamenam"),<br>-  ввести 12 символов ("namenamename"),|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120223](https://tracker.yandex.ru/BUG-1120223)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|19|Создать учетную запись для курьера, в поле "firstName"<br>- ввести 2 символ ("na"),<br>- ввести 5 символов ("namen"),<br>- ввести 10 символов ("namenamena")|Код и статус ответа: 201 Created|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер зарегистрирован в приложении|**PASSED**| |
|20|Создать учетную запись для курьера, в поле "firstName"<br>- ввести 2 символ ("Им"),<br>- ввести 5 символов ("Имяим"),<br>- ввести 10 символов ("ИмяИмяИмяИ")|Код и статус ответа: 201 Created|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер зарегистрирован в приложении|**PASSED**| |
|21|Создать учетную запись для курьера, в поле "firstName" ничего не писать (поле не обязательно)<br>- пустое поле ввода: ""|Код и статус ответа: 201 Created|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер зарегистрирован в приложении|**PASSED**| |
|22|Создать учетную запись для курьера, в поле "firstName" <br>- ввести буквы другого алфавита 登錄密碼密碼|Код и статус ответа: 201 Created|**FAILED**|[BUG-1121716](https://tracker.yandex.ru/BUG-1121716)|
|||Ответ соответствует шаблону|||
|||Курьер зарегистрирован в приложении|||
|23|Создать учетную запись для курьера, в поле "firstName" <br>- ввести цифры "test123",<br>- ввести спецсимволы "test@#$",<br>- ввести пробел "te st"|Код и статус ответа: 400 Bad Request|**FAILED**|[BUG-1120225](https://tracker.yandex.ru/BUG-1120225)|
|||Ответ соответствует шаблону|||
|||Курьер не будет зарегистрирован в приложении|||
|24|Создать учетную запись для курьера, отправить пустой массив|Код и статус ответа: 400 Bad Request|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Курьер не будет зарегистрирован в приложении|**PASSED**| |
|**Удаление учетной записи курьера DELETE /api/v1/courier/:id**|
|1|Проверить возможность удаления существующей учетной записи курьера|Код и статус ответа: 200 OK|**PASSED**| |
|||Ответ соответствует шаблону|**PASSED**| |
|||Учетная запись курьера удалена из БД|**PASSED**| |
|2|Проверить, что при удалении курьевра связанные заказы в БД в  таблице Orders должны быть стёрты|Данные удалились из БД из таблицы Orders |**FAILED**|[BUG-1121718](https://tracker.yandex.ru/BUG-1121718)|
|||||||
|||||||
|3|Проверить возможность удаления существующей учетной записи курьера<br>При этом оставить массив пустым, заполнить только id в запросе|Код и статус ответа: 400|**FAILED**|[BUG-1121719](https://tracker.yandex.ru/BUG-1121719)||
|||Ответ соответствует шаблону||||
|||Данные в БД не изменились||||
|4|Проверить возможность удаления несуществующей учетной записи курьера|Код и статус ответа: 404 Not Found|**PASSED**| ||
|||Ответ соответствует шаблону|**PASSED**| ||
|||Данные в БД не изменились|**PASSED**| ||
|**Получить заказ по его номеру GET /api/v1/orders/track**||
|1|Отправить запрос на получение данных по заказу. <br>Вести номер существующего заказа|Код и статус ответа: 200 OK|**PASSED**| ||
|||Ответ соответствует шаблону|**PASSED**| ||
|||Данные в БД не изменились|**PASSED**| ||
|2|Отправить запрос на получение данных по заказу. <br>Вести номер не существующего заказа|Код и статус ответа: 404 Not Found|**PASSED**| ||
|||Ответ соответствует шаблону|**PASSED**| ||
|||Данные в БД не изменились|**PASSED**| ||
|3|"Отправить запрос на получение данных по заказу. <br>Отправить запрос без номера|Код и статус ответа: 400 Bad Request|**PASSED**| ||
|||Ответ соответствует шаблону|**PASSED**| ||
|||Данные в БД не изменились|**PASSED**| ||

**Найденные баги**
## BUG-1120211
**Ответ 201 на запрос POST /api/v1/courier при значении параметра login = l**

Шаги воспроизведения:

1. Открыть postman

2. Создать запрос 

curl --location --request POST 'https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier' \

--header 'Content-Type: application/json' \

--data-raw '{

`"login": "l",

`"password": "4321",

`"firstName": "saske"

}' 

3.Нажать Send 

4.Получить ответ

ОР - 404, ответ в соответствии с требованиями, курьер не создается 

ФР - 201, курьер создан
## BUG-1120213
**Ответ 201 на запрос POST /api/v1/courier при значении параметра login = логин**

Шаги воспроизведения:

1.Открыть postman

2.Создать запрос

curl --location --request POST '  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier'

--header 'Content-Type: application/json'

--data-raw '{

"login": "логин",

"password": "4321",

"firstName": "saske"

}'

3.Нажать Send

4.Получить ответ

ОР - 404, ответ в соответствии с требованиями, курьер не создается

ФР - 201, курьер создан
## BUG-1120215
**BUG-1120215: Ответ 201 на запрос POST /api/v1/courier при значении параметра login = login!**

Шаги воспроизведения:

1.Открыть postman

2.Сoздать запрос

curl --location --request POST '   https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier'

--header 'Content-Type: application/json'

--data-raw '{

"login": "login!",

"password": "4321",

"firstName": "saske"

}'

3.Нажать Send

4.Получить ответ

ОР - 404, ответ в соответствии с требованиями, курьер не создается

ФР - 201, курьер создан
## BUG-1120216
**Ответ 201 на запрос POST /api/v1/courier при значении параметра First name = ""**

Шаги воспроизведения:

1.Открыть postman

2.Сoздать запрос

curl --location --request POST '   https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier'

--header 'Content-Type: application/json'

--data-raw '{

"login": "login",

"password": "4321",

"firstName": ""

}'

3.Нажать Send

4.Получить ответ

ОР - 404, ответ в соответсвии с требованиями, курьер не создается

ФР - 201, курьер создан
## BUG-1120218
Ответ 201 на запрос POST /api/v1/courier при значении параметра password = 12345

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос
curl --location --request POST '[  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier](https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "logi",
"password": "12345",
"firstName": "saske"
}'
3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответсвии с требованиями, курьер не создается
ФР - 201, курьер создан
## BUG-1120219
**Ответ 201 на запрос POST /api/v1/courier при значении параметра password = тест**

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос
curl --location --request POST '[  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier](https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "log",
"password": "тест",
"firstName": "saske"
}'

3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответствии с требованиями, курьер не создается
ФР - 201, курьер создан

## BUG-1120220
**Ответ 201 на запрос POST /api/v1/courier при значении параметра password = 0/1**

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос

curl --location --request POST '[  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier](https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "logii",
"password": "0/1",
"firstName": "saske"
}'

3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответсвии с требованиями, курьер не создается
ФР - 201, курьер создан
## BUG-1120221
**Ответ 201 на запрос POST /api/v1/courier при значении параметра password = 12!1**

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос
curl --location --request POST '[  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier](https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "loii",
"password": "12!1",
"firstName": "saske"
}'

3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответствии с требованиями, курьер не создается
ФР - 201, курьер создан
## BUG-1120216
**Ответ 201 на запрос POST /api/v1/courier при значении параметра First name = ""**

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос
curl --location --request POST ' [  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier](https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "login",
"password": "4321",
"firstName": ""
}'
3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответствии с требованиями, курьер не создается
ФР - 201, курьер создан
## BUG-1120223
**Ответ 201 на запрос POST /api/v1/courier при значении параметра password = n**

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос

curl --location --request POST '[  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier](https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "loweer",
"password": "1221",
"firstName": "n"
}'

3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответствии с требованиями, курьер не создается
ФР - 201, курьер создан
## BUG-1121716
**Ответ 201 на запрос POST /api/v1/courier при значении параметра firstName = 登錄密碼密碼**

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос

curl --location --request POST '[  https://fbf45369-9d03-47b3-adb0-88ba9df6ef97.serverhub.praktikum-services.ru/api/v1/courier](https://fbf45369-9d03-47b3-adb0-88ba9df6ef97.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "ninjja",
"password": "4321",
"firstName": "登錄密碼密碼"
}'

3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответсвии с требованиями, курьер не создается
ФР - 201, курьер создан
## BUG-1120225
**Ответ 201 на запрос POST /api/v1/courier при значении параметра firstName = test123**

Шаги воспроизведения:

1.Открыть postman
2.Сoздать запрос

curl --location --request POST '[  https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier](https://32a8d4f9-7e82-4075-8947-4e568637b30c.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "lower",
"password": "1221",
"firstName": "test123"
}'

3.Нажать Send
4.Получить ответ

ОР - 404, ответ в соответсвии с требованиями, курьер не создается
ФР - 201, курьер создан
## BUG-1121718
**При удалении курьера по ручке DELETE /api/v1/courier/:id связанные заказы в БД в таблице Orders не удаляются.**

Предусловие:
1.Открыть postman
2.Сoздать запрос для создания курьера

curl --location --request POST '[  https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/courier](https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "ninjqa",
"password": "4321",
"firstName": "naruto"
}'
3.Отправить запрос на создание курьера
4.Создать запрос для создания заказа

curl --location --request POST '[  https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/orders](https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/orders)'
--header 'Content-Type: application/json'
--data-raw '{
"firstName": "Narutо",
"lastName": "Uchiha",
"address": "Konoha, 142 apt.",
"metroStation": 4,
"phone": "+7 800 355 35 35",
"rentTime": 5,
"deliveryDate": "2022-12-25",
"comment": "Saske, come back to Konoha",
"color": [
"BLACK"
]
}'

5.Открыть CYGwin, зайти на сервер
6.Ввести команду /dt, чтобы увидеть таблицы

Шаги воспроизведения:

1. Зарегистироваться в моб. приложении как курьер
1. Принять заказ
1. Завершить заказ
1. Отправить запрос на удаление курьера :

curl --location --request DELETE '[  https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/courier/2](https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/courier/2)'
--header 'Content-Type: application/json'
--data-raw '{
"id": "2"
}'

5.Зайти в БД ORDERS

ОР -при удалении курьера связанные заказы в БД в таблице Orders должны быть стёрты
ФР - при удалении курьера связанные заказы в БД в таблице Orders не удаляются
## BUG-1121719
**Ответ 200 OK На запрос DELETE /api/v1/courier/:id при пустом массиве**

Существующая учетной записи курьера удаляется при пустом массиве и при заполненным ID

Предусловие:
1.Открыть postman
2.Сoздать запрос для создания курьера

curl --location --request POST ' [  https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/courier](https://d9e6dcb8-adba-411d-9a92-7838c6288fa6.serverhub.praktikum-services.ru/api/v1/courier)'
--header 'Content-Type: application/json'
--data-raw '{
"login": "ninjqa",
"password": "4321",
"firstName": "naruto"
}'

3.Открыть CYGwin, зайти на сервер
4. Посмотреть ID курьера в таблице Couriers

Шаги воспроизведения:
1.Открыть postman
2.Сoздать запрос для удаления курьера, но не прописывать массив кода
3.Прописать id курьера только в URL

OР - Ошибка 400, курьера нельзя удалить при пустом теле запроса
ФР - Курьер удален при пустом массиве, ответ 200 ОК







### **[Nazina's Shop] - Автоматизация на Postman'е**

Smoke-тестирование всех доступных через API функций магазина одежды О. Назиной.

![title](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/title.png)


---

***[Ссылка на проект по ручному тестированию магазина](https://github.com/OQASergey/Nazinas_Shop_Testing#readme)***

***[Ссылка на документацию проекта](https://testbase.atlassian.net/wiki/spaces/SHOP/overview?homepageId=1411056054)***

***Ключ:*** https://api.postman.com/collections/30220849-d417c303-1fc9-4700-9707-dd6955623a68?access_key=PMAT-01HCHVN23KVM4XPP1XEGXBC820


<details>
  <summary>Визаулизация тестов</summary>
  
  **Запуск тестов:**
  
![PA_NSh_start](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/PA_NSh_start.gif)

------

**Отображение в консоли Postman'а:**

![PA_NSh_console](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/PA_NSh_console.gif)

------

**Просмотр ошибок:**

![PA_NSh_fails](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/PA_NSh_fails.gif)

------

</details>

<details>
  <summary>Детальное описание проекта</summary>
   
  Проект представляет собой набор smoke-тестов web-приложения через REST API.

  Запросы и пояснения: 
 
  **1. "Создание карточки товара А":**
  
  [Ссылка на документацию ресурса "Create item"](https://testbase.atlassian.net/wiki/spaces/SHOP/pages/1957496610/Create+item)

  - *Body*

  Для ключей "name" и "description" создаётся случайное слово на английском языке (первый символ в верхнем регистре);

  Для ключей "section", "color" и "size" выбираются случайные значения из одноимённых массивов с заранее заготовленными вариантами;
  
  Для ключа "price" генерируется случайное значение [2,998];

  Для ключа "params" создаётся случайное слово на английском языке в нижнем регистре;

  Для ключа "photo" заранее заготовлено изображение, закодированное в base64

- *Pre-req.*

Скрипты генерации значений для ключей "section", "color", "size" и "price";

Сохранение в переменные коллекции значений для "section", "color", "size" и "price"

- *Tests*

[Данный скрипт выполняется здесь и далее в каждом шаге] Вывод статуса ответа в консоль (или параметров ошибки в случае статуса, отличного от "ok" (значение статуса берётся из тела json, т.к. статус ответа всегда 200 OK);

Сохранение в переменные коллекции значений для ключей из ответа "id", "name", "description" и "params";

Извлекается размер (в байтах) изображения в формате base64 и сохраняется в переменные коллекции

**2. "Тест к-А":**
  
  [Ссылка на документацию ресурса "Get item"](https://testbase.atlassian.net/wiki/spaces/SHOP/pages/1969291375/Get+item)

  - *Body*

Для ключа "id" добавляется значение созданного в шаге 1 объекта из переменной коллекции

   - *Tests*

Проводятся тесты сравнения значений ответа и значений из переменных коллекции для всех ключей кроме "photo". Результаты тестов выводятся в консоль postman'а;

Сохраняется в переменные коллекции url декодированного изображения ключа "photo"

  **3. "Тест фото в к-А":**

 Выполняется запрос на получение headers из сохранённой в переменных коллекции url изображения методом HEAD 

  - *Tests*

Берётся актуальное значение веса изображения по url из заголовка Content-Length;

Меняется тип данных актуального значения веса изображения со строчного на числовое;

Выполняется тест сравнение актуального значения веса и значения из сохранённой переменной коллекции для ключа "photo" из шага 1. Результаты тестов выводятся в консоль postman'а

  **4. "Обновление к-А":**
  
  [Ссылка на документацию ресурса "Update item"](https://testbase.atlassian.net/wiki/spaces/SHOP/pages/1969422366/Update+item)

  - *Body*

Для ключа "id" добавляется значение созданного в шаге 1 объекта из переменной коллекции;

Для ключей "name", "section", "description", "color" и "size" выбираются случайные значения из одноимённых массивов с заранее заготовленными вариантами, кроме выбранных в шаге 1;

Для ключей "price" и "params" генерирются случайные значения [2,998], кроме выбранных в шаге 1

- *Pre-req.*

Скрипты генерации новых значений для ключей "name", "section", "description", "color", "size", "price" и "params";

Сохранение в переменные коллекции новых значений для ключей "name", "section", "description", "color", "size", "price" и "params"

**5. "Тест обновления к-А":**

Аналогично шагу 2, только с обновлёнными значениями

**6. "Создания к-Б":**

Аналогично шагу 1, только с новыми значениями для ключей, не совподающими с сохранёнными в коллекции переменными

*Примечание: Значение ключа "name" в шаге 6 и шаге 4 идентичны*

**7. "Тест к-Б":**

Аналогично шагу 2, только со значениями из шага 6

**8. "Тест поиска к-А и к-Б":**
  
  [Ссылка на документацию ресурса "Search"](https://testbase.atlassian.net/wiki/spaces/SHOP/pages/1957464487/Search)

  - *Body*

Для ключа "query" добавляется значение ключа "name" из шага 4 и 6 из переменной коллекции 

- *Pre-req.*

(продолжение текста в разработке)

</details>

___



## **Инструкция по импортированию проектов:**
<details>
  <summary>Развернуть инструкцию</summary>

  
**Для того, чтобы импортировать проект в Вашу коллекцию необходимо сделать следующее:**
- Кликнуть на кнопку "Import" в вашем рабочем пространстве (workspace)

![import1](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/import1.png)
- Вставить ссылку на ключ в появишвееся поле

![import2](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/import2.png)

*В Вашем рабочем пространстве появится новая коллекция с одноимённым названием;*

**Чтобы запустить автотест, необходимо выполнить следующие шаги:**
- Кликнуть на импортированную коллекцию с проектом

![run1](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/run1.png)
- Кликнуть на кнопку "Run collection"

![run2](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/run2.png)
- В выпадающем меню "Advamced Settings" выключить чекбокс "Stop run if an error occers"

![run4](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/run4.png)
- Открыть консоль postman'а (в низу экрана)

![run3](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/run3.png)
- Кликнуть на кнопку "Run [название проекта]"

![run5](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/run5.png)

*Запустятся автотесты. Вся инфомация по результатам тестов отображается в логах консоли postman'а*

![run6](https://github.com/OQASergey/Nazina-s_Shop-automation_Postman/raw/main/pics/run6.png)
</details>

---

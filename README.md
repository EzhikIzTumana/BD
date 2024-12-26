# BD
Тема проекта: Веб-сайт, представляющий собой страховую фирму.
Компания имеет различные филиалы по всей стране. Каждый филиал характеризуется названием, адресом и телефоном. Деятельность компании организована следующим образом: в компанию обращаются различные лица с целью заключения договора о страховании.
В зависимости от принимаемых на страхование объектов и страхуемых рисков, договор заключается по определенному виду страхования (например, страхование автотранспорта от угона, страхование домашнего имущества, добровольное медицинское страхование). При заключении договора фиксируется дата заключения, страховая сумма, вид страхования, тарифная ставка и филиал, в котором заключался договор.
Договоры заключают страховые агенты. Помимо информации об агентах (фамилия, имя, отчество, адрес, телефон), хранится информацию о филиале, в котором работают агенты.
Имеется возможность рассчитывать заработную плату агентам. Заработная плата составляет некоторый процент от страхового платежа (страховой платеж — это страховая сумма, умноженная на тарифную ставку). Процент зависит от вида страхования, по которому заключен договор.
Функциональные требования:
1.    Система ролей: в проекте представлено 3 роли: пользователь, сотрудник и администратор.
2.    Авторизация в системе для пользователя, сотрудника и администратора.
3.    Регистрация пользователей.
4. Возможности каждой из трех ролей
Пользователь:
-     Просмотр филиалов компании
-     Оформление заявки на заключение договора, в зависимости от выбранного объекта и  вида страхования
-     Просмотр своих оформленных заявок,
-  Редактирование или удаление заявки, если она еще не принята в обработку,
-     Написание отзывов,
-     Редактирование своих отзывов,
-     Просмотр промокодов и их применение в заказе,
-     Выход из системы.
Сотрудник:
-     Просмотр заявок от пользователей,
-  Заключение договоров,
-     Просмотр информации о заключенных им договорах,
-     Выход из системы.
Администратор:
-     Просмотр всех заявок и договоров
-     Просмотр статистики заработной платы агентов,
-     Просмотр статистики зарегистрированных пользователей,
-     CRUD операции с пользователями,
-     CRUD операции с заявками, договорами, отзывами и т.д.,
-     Выход из системы.

Список сущностей БД:
1.	Новости
id (serial, primary key) – Уникальный идентификатор
title (varchar(max_length=100, not null)) – Название заголовка
content (varchar(max_length=255, not null)) – Текст стать
image (image)  - Фото
date (timestampz(default=current_timestampz)) – Дата публикации
2.	Контакты
id (serial, primary key) – Уникальный идентификатор
user_id (integer(not null, FK)) – Внешний ключ на пользователя
description (varchar(max_length=255, not null)) – Информация о контакте
photo (image)  – фото пользователя

3.	Вакансии
id (serial, primary key) – Уникальный идентификатор 
name (varchar(max_lenght=100, not null)) – Название вакансии
description (varchar(max_lenght=100, not null)) – Описание вакансии
need (varchar(max_lenght=100, not null)) – Список требований

4.	Отзывы
id (serial, primary key) – Уникальный идентификатор 
name (varchar(max_length=50, not null)) – название отзыва
text (varchar(max_length=255, not null)) – содержимое отзыва
rating (smallint(max=5, min=1, not null)) – оценка(от 1 до 5)
date (timestampz(default=current_timestampz)) – время создания отзыва
user_id (integer(not null, FK)) – Внешний ключ на пользователя

5.	Промокоды и купоны
id (serial, primary key) – Уникальный идентификатор 
code (varchar(max_lenght=15, not null)) – код промокода
discount: smallint(max=99, min=1, not null) – скидка(проценты)
expiry_date (timestampz, not null) – дата истечения действия промокода

6.	Виды страхования
id (serial, primary key) – Уникальный идентификатор 
name (varchar(max_lenght=100, not null)) – Название вида страхования
description (varchar(max_lenght=100, not null)) – Описание вида страхования
commission_rate (smallint(max_lenght=3, not null)) - Процентная ставка для расчета зарплаты агентов
tariff_rate = (float(max_lenght=15, not null)) - Тарифная ставка
7.	Риск страхования
id (serial, primary key) – Уникальный идентификатор 
insurance_type (integer(not null, FK)) - Внешний ключ на тип страхования
name (varchar(max_lenght=100, not null)) – Название риска типа страхования
description (varchar(max_lenght=100, not null)) – Описание  риска типа страхования
8.	Пользователи системы
id (serial, primary key) – Уникальный идентификатор 
status (varchar(max_lenght=15, not null, check (status in (‘Agent’, ‘Customer’))
first_name (varchar(max_lenght=100, not null)) – Фамилия пользователя
 last_name (varchar(max_lenght=100, not null)) – Имя пользователя
middle_name (varchar(max_lenght=100, not null)) – Отчество пользователя
email (varchar(max_lenght=100, unique=True) – Электронная почта пользователя
address (varchar(max_lenght=100, not null)) – адрес пользователя
phone_number (varchar(max_lenght=15, not null)) – номер телефона пользователя
age (smallint(not null)) – возраст пользователя

9.	Объекты страхования
id (serial, primary key) – Уникальный идентификатор 
name (varchar(max_lenght=100, not null)) – Название объекта страхования
description (varchar(max_lenght=100, not null)) – Описание  объекта страхования

10.	Заявки клиентов
id (serial, primary key) – Уникальный идентификатор 
client (integer(not null, FK)) - Внешний ключ на пользователя
department (integer(not null, FK)) - Внешний ключ на отдел
insurance_type (integer(not null, FK)) - Внешний ключ на тип страхования
insurable_object (integer(not null, FK)) - Внешний ключ на объект страхования
insurance_risk (integer(not null, FK)) Внешний ключ на риск страхуемого объекта
insurance_amount (float(max_length = 9, not null)) - Страховая сумма
created_at (timestampz(default=current_timestampz)) – Дата создания
promo_code (integer(not null, FK)) - Внешний ключ на промокод
is_processed (bool(default=False)) – Статус заявки в обработке

11.	 Договоры о страховании
id (serial, primary key) – Уникальный идентификатор 
policy_number (intmax_length =30, not null) - Номер страхового счета
agent (integer(not null, FK)) - Внешний ключ на агента   
start_date (timestampz(default=current_timestampz)) – дата начала действия договора
end_date (timestampz, not null) – дата окончания действия договора
is_active (bool(default=True)) – Статус действительности действия договора

12.	Зарплата агентов
 id (serial, primary key) – Уникальный идентификатор 
 agent (integer(not null, FK)) – Внешний ключ на агента
 policy (integer(not null, FK)) – Внешний ключ на договор
 commission_amount (float, not null) – Сумма комиссии

 

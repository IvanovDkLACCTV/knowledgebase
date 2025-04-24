---
title: "Геозоны в Ceiba2 - LACCTV - Jira Service Management"
source: "https://videotelematic.atlassian.net/servicedesk/customer/portal/5/LA3921-72"
author:
published:
created: 2025-04-24
description:
tags:
  - "clippings"
---
Skip to:

**Dmitrii Ivanov** raised this on 10/Apr/25 5:34 PM

Provide as much detail as possible about your question

Добрый день,

Подскажите, пожалуйста, как можно получить данные о геозонах из Ceiba2?

Каким образом можно данные о геозонах экспортировать и видеорегистратора?

Есть ли Excel файл, в который можно ввести данные о геозонах и импортировать через CMS Ceiba2?

Спасибо

Activity

### ElzarToday 2:31 PM

Добрый день Коллеги.

1. Как можно получить данные о геозонах из Ceiba2?
- Вы можете их настроить через приложение Клиент CB2, для этого нужно перейти к устройству и выбрать пункт Геозоны
![image-20250424-112313.png](https://videotelematic.atlassian.net/24fc69eb-2040-4b20-9eca-29b7f6a7e5cd)
![[Pasted image 20250424174425.png]]
Далее у Вас откроется интерфейс где вы можете просмотреть, добавить, удалить, импортировать и(или) изменить существующие геозоны на текущем ТС.

![image-20250424-112432.png](https://videotelematic.atlassian.net/a98a4950-533c-4c3a-b311-68cb0834e83b)
![[Pasted image 20250424174509.png]]
1. Каким образом можно данные о геозонах экспортировать и видеорегистратора?
- ПО CB2 не предоставляет возможность экспортировать геозоны.
1. Есть ли Excel файл, в который можно ввести данные о геозонах и импортировать через CMS Ceiba2?
- Вы сможете импортировать геозоны на основе данных Долготы и Ширины, однако только в форме линии, другие типы формы досутпны только в интерфейсе настроек.
![image-20250424-111709.png](https://videotelematic.atlassian.net/3abaa796-8433-4ae1-9add-6bda99d7753a)
![[Pasted image 20250424174520.png]]
- Выглядеть это может подобным образом
![image-20250424-111945.png](https://videotelematic.atlassian.net/b3ff8c6c-92e1-401e-84b5-ba3feb0673a9)
![[Pasted image 20250424174527.png]]
Шаблон файла: Geo3.xls

Здесь как мы видим только 2 записи, начала и окончания. Далее для этой геозоны мы можем настроить параметры ниже.

![image-20250424-111320.png](https://videotelematic.atlassian.net/5a41771f-23ce-4651-b1ec-63be10a57275)
![[Pasted image 20250424174612.png]]
Можно также сразу загрузить большое количество точек в виде линии, и настроить параметры для каждой, но стоит учитывать что в одном файле может быть только 1 геозона

### Automatic responseToday 2:31 PM

Your request status has changed to Waiting for customer.
# Домашнее задание к занятию «Базы данных, их типы»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

---

### Задание 1. СУБД

### Кейс
Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать 
правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для
каждой предметной области. 

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему? 
 
1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков.
СУБД должна гарантировать целостность и чёткую структуру данных.

1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы? 

1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к 
маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? 
СУБД должны быть гибкими и быстрыми.

1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?

1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу 
и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.

1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это 
реализовать?

1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов 
по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать
со связями.

1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД 
логистов?

1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?

*Приведите ответ в свободной форме.*

---

### Ответ к заданию 1:

1.1. Мне кажется подойдет реляционная СУБД, например, PostgreSQL, а для ускорения хеширования можно использовать библиотеки, такие как hashlib.

1.2. Если нужна гибкая и легкая СУБД, то мой выбор падает на NoSQL (например MongoDB) т.к. она не имеет предопределенных схем, что и делает ее идеальным кандидатом для для быстро меняющихся сред разработки.

1.3. Думаю можно использовать СУБД, которая была приведена в первом вопросе, реляционная, PostgreSQL.

1.4. Можно попробовать взять какую нибудь сетевую СУБД, но графовые, например как Neo4j, будут работать быстрее, так что думаю лучше присмотрется к графовой.

1.5. Думаю что с этими всеми задачами может справиться PostgreSQL, она поддерживает и реляционные, и NoSQL, и графовые возможности.

---

### Задание 2. Транзакции

2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы 
транзакция завершилась успешно. Ориентируйтесь на шесть действий.

2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?

*Приведите ответ в свободной форме.*

---

### Ответ к заданию 2:

Как я думал:
1. идентификация пользователя
2. ~~выбор способа платежа~~
3. подготовка транзакции (Просмотр балансов пользователей между которыми происходит транзакция, проверка наличия нужных средств с одной из сторон)
4. обработка транзакции (Перемещение самих средств между пользователями, создание точки возврата)
5. подтверждение транзакции
6. обновление данных. (Обновление баланса обоих сторон)

Но думаю корректнее будет выглядеть так:
1.  Авторизация пользователя (id1)
2.  Убывание баланса (id1)
3.  Сохранение баланса (id1)
4.  Увеличение баланса (id2)
5.  Сохранение баланса (id2)
6.  Подтверждение транзакции.

---

### Задание 3. SQL vs NoSQL

3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL. 

3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

*Приведите ответ в свободной форме.*

---

### Ответ к заданию 3:

1. SQL поддерживает транзакции, что гарантирует целостность данных в случае сбоев.
2. Поддержка ACID (Atomicity, Consistency, Isolation, Durability) тоже является преимуществом SQL систем.
3. SQL использует реляционную модель базы данных, что делает эту структуру данных более подходящей для хранения и обработки структурированных данных.
4. В SQL более сложный язык запросов, который больше подходит для большого количества данных.
5. В связи со сложным языком запросов, SQL может работать быстрее из за того что пользователь будет находить по конкретным ключам файл который ему нужен.

---

### Задание 4. Кластеры

Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу 
выделено 1000 машин. 

На основе какого критерия будете выбирать тип СУБД и какая модель *распределённых вычислений* 
здесь справится лучше всего и почему?

*Приведите ответ в свободной форме.*

---

### Ответ к заданию 4:

Буду ориентироваться на тип данных, тип запросов, масштабируемость, гибкость и производительность.
Учитывая все эти критерии мне кажется лучше всего подобрать NoSQL базу данных, т.к. они хорошо масштабируются, обеспечивают высокую производительность и отказоустойчивость при увеличении числа узлов.


---

_Задания,помеченные звёздочкой, — дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже разобраться в материале._

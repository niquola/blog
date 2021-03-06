---
layout: post
title: "Pair Programming"
date:   2014-03-22 10:42:45
abstract: "Доклад про парное программирование на agile days"
categories: xp methodology practice
---


Доклад про парное программирование на [Ag;)e days](http://http://agiledays.ru/)

<iframe src="//player.vimeo.com/video/90645464" width="500" height="313" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

[Слайды](http://niquola.github.io/pair-programming-slides)


## Kent Beck

Кент Бек изобрел unit tests, tdd и еще много всего.

## Pair Programming

В частности парное программирование.
Это когда код проектируется и реализуется двумя
программистами за одной рабочей станцией.

Он подумал:

> Некоторые практики и аспекты положительно
> влияли на результат разработки. И я подумал
> а почему бы их не выкрутить на максимум.

... изобрел __Extreme Programming__

Если тестирующий код это хорошо, то почему бы сразу не писать тесты?

Если лучше совместно решать сложные проблемы и проектировать,
если общее владение кодом это хорошо,
если сложные ошибки проще искать вместе,
то почему бы постоянно не программировать в паре?

## Adoption

Я узнал о парном программировании лет 5 назад,
когда читал книгу "Extreme Programming".
Идея звучала интригующе и запомнилась.
Мы с командой обсудили и даже немного попробовали.
Но тогда TDD оттенил эту технику, и мы занялись
осознанием и внедрением ТDD.

Потом я прочитал статью про проект в котором
__ПП__ было на полное рабочее время. Это опять разожгло интерес.
Мы решили в проекте попробовать тоже выкрутить эту ручку
на максимум - и это был первый заход. Мы в течении нескольких
месяцев работали все рабочее время в парах.

Потом все чаще стали разбиваться, чтобы по отдельности доделать рутинку
или мелкие задачи. И постепенно инициатива угасла.

После была попытка внедрить __Code Review__
Он не прижился - исправлять ошибки пост-фактум было не приятно,
хотелось их допускать поменьше. Также review занимал значительное время
ведущих разработчиков. В процессе ревизии часто хотелось посадить
автора рядом и обсудить с ним решения, дать советы - а когда начинали
писать отчет то энергетика спадала.

Мы вновь заговорили про PP, где-то через год. Причем
у всех в команде остались приятные впечатления от предыдущей попытки
и никто не мог вспомнить почему мы приостановили эту практику.

В итоге мы решили добавить побольше системности и сделали второй заход,
который длится до сих пор (уже около 1.5 лет).

## Real working time

И когда начали, то вспомнили одну своеобразную сторону ПП из-за
которой оно может не прижиться.

Вы удивитесь, но парное программирование первые пару месяцев будет
вас изматывать. Вы не сможете работать больше 4-5 часов пока не появится
привычка.

Это совпадает с исследованиями, в которых утверждается,
что человек способен на полной мощности решать интеллектуальные задаче
не продолжительней чем в течении 4-5 часов.

Этот предел и выжимает из вас парное программирование.

Однако, со временем (как у спортсменов) приходит привычка.
Напряжение постепенно спадает. Вы учитесь в правильное время делать
преременки.

## Statistic

Тех кто не имел дело с парным программированием наверное мучает вопрос -

А что же с производительностью?  Она будет в двое меньше?

Как показывают целый ряд исследований, проведенный на профессиональных программистах и на студентах,
она будет приблизительно такой же.

Говорят, что в среднем на старте она немного ниже в паре,
но потом выравнивается и даже становится выше.

Но мы в качестве бонуса получаем:

### Качество кода выше

Было объективно установлено, а также отмечено самими испытуемыми что качество
решений в паре было выше (и мы это подтверждаем).

Человек на едине с собой склонен к лени и компромиссам.
Проверка идеи, вербализация и т.д.


### Совместное владение кодом

> Ребята кто может добавить функционал или пофиксить ошибку?
> Гриша - но он в отпуске или на другой приоритетной задаче или в отпуске
> Или я боюсь трогать этот код, я не знаю как он работает


Ego-less coding - вы приняли решения вместе и написали код тоже вместе,
вы лояльны к этому коду, вы его понимаете и можете улучшить и расширить.


## Удовлетворение и Эмоциональный Фон

Я заметил, что каждый разработчик рано или поздно (обычно достаточно быстро)
находит свою индивидуально-неудобную задачу-ловушку,
от которой у него портится кровь (скучно, не получается, душа не лежит...).

> меня от этой задачи уже мутит...
> не знаю уже как подобраться
> Петя когда ты наконец...

На мой взгляд, одна из сильных сторон парного программирования - это то, что оно существенно уменьшает
количество таких задач. Программисты чаще пребывают в хорошем расположении духа, реже впадают
в фрустрацию и прокрастинацию. Сейчас у меня например уже рефлекс, если я чую подобную проблему - то
начинаю искать подходящую пару (зная что это лекарство).

## Как долго пара работает вместе

Но вернемся к нашей истории.

Первый вопрос которым мы задались - как долго пара должна работать вместе?

Это как выбор длительности итерации.

Мы попробовали разные варианты:

* Пара меняется раз в день
* Пара меняется раз в пол-дня

Однако задачи которые мы решаем достаточно сложны и требуют времени
на погружение в контекст и переключения.

У нас кросс-функциональная команда и разработчики занимаются всем
от DevOps и генерации по медицинской метаинформации базы данных до дизайна.

Поэтому прижилась практика перемешивать пары на логических milestones функциональности.
Сейчас пара может работать над набором задач в течении недели, потом мы обычно
насильно свопаем.

Здесь можно показать как происходит перемешивание знаний и совместное обладание кодом:

Функциональность начинает делать одна пара.
Потом на логической запятой один человек уходит из пары и добавляется свежий.
Если имеем дело с кросс-фичей таким образом может поучаствовать вся команда.

Обычно на вопрос "кто внесет такие-то изменения или кто может починить то-то?" у нас есть
несколько вариантов ответа.

## Какие пары?

Следующий пункт это - как формировать пары?

Мы заметили, что не все пары равно-эффективны и то, что разные пары подходят для выполнения
разных типов задач!

Тут можно провести аналогию со спортом, где есть понятие связки.
Это два или более игрока, которые друг друга понимают и дополняют.
Они способны действовать более эффективно чем по отдельности или в связке с другими.

Со временем подобные связки самоорганизуются, просто нужно быть внимательным.
Есть атакующие пары, которые могут решать сложные задачи. Есть зачищающие (защитные) пары,
которые хорошо работают напильником и т.д.

Иногда можно образовывать насильственные пары - ради передачи знаний или в образовательных целях.

## Remote Pairing

У нас часть команды в другом городе. И мы заметили проблему
выпадания удаленных разработчиков из текущего контекста команды.
В команде  кипит бурная интеллектуальная жизнь и многие идеи рождаются за
чашечкой кофе. Удаленным ребятам приходилось напрягаться и ловить эхо.

__ПП__ и утренние стэндапы значительно уменьшили эту боль. Живая ежедневная
коммуникация практически стирает пространственную границу.

Для тех кому интересн наш стэк для удаленного ПП:

* Google Hangout - для видео чата
* ssh, mosh, tmux, vim or emacs - для кодинга

## Weak Pairing

Мы сместили точку отчета: те естественным является работа в паре,
и лишь в некоторых случаях пара разбивается. Можно назвать это слабой парой.
Например при мелком багфиксинге, выведении в гринлайн после рефакторинга или на исследовательских
спайках пара по собственному рассмотрению может распаралелиться, но отчитывается и несет ответственность как пара.

## Summary

В настоящий момент мы можем утверждать, что достаточно глубоко освоили и оценили
практику парного программирования. По собственному опыту могу сказать, что
порой решая задачу в одиночку я испытываю острое желание подобрать пару - иду и ищу ее!


  Communication is a blood of team

Если интересно больше, то спрашивайте в комментариях.

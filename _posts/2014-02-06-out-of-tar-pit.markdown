---
layout: post
title:  "Out of the Tar Pit"
date:   2014-02-06 00:00:00
abstract: "Свободный перевод статьи про функционально-реляционный подход"
---

Сложность является основной проблемой при разработке больших информационных систем.
Следуя Бруксу мы различаем случайную (accidental) и существенную  (essential) сложности,
но не разделяем его мнения, что в современных системах в основном осталась только существенная сложность.
Мы изучили основные источники сложности и предлагаем общие подходы, позволяющие исключить случайную
сложность. Конкретнее мы предлагаем подход минимизирующий сложность и основанный на функциональном программировании
и реляционной модели данных Эдгара Кодда.

## Введение

Кризис информационных технологий был зафиксирован впервые в 1968 году и в дальнейшем
лишь усугублялся. Основная проблема разработки и поддержки больших систем это сложность -
большие системы очень трудно понимать. По нашему мнению основным источником сложности
в большинстве систем является управление состоянием (handling state) и сложность их анализа и понимания.
Другими причинами являются объем кода и явное управление потоком выполнения.

Сегодня основными подходоми к управлению состоянием являются:

* объектно-ориентированное программирование, которое ведет к тесной связи состояния и поведения
* и функциональное программирование - которое в своих чистых формах вовсе избегает состояния
и остаточных явлений (side effects)

В обоих этих подходах при создании больших систем выявляются свои (отличные друг от друга) проблемы.
Мы утверждаем, что можно взять лучшее из обоих и, добавив идеи из мира реляционных баз данных,получить
подход, упрощающий создание крупно-масштабных систем.

## Сложность

В статье "Нет серебряной пули" Брукс выделяет четыре характеристики информационных
систем, которые усложняют разработку: сложность, конформизм, изменяемость и невидимость.
Мы считаем, что сложность является самой главной проблемой - остальные либо могут
быть классифицированы как формы сложности или проблематичны только в присутствии сложности.

Сложность ключевая причина большинства проблем в современной информационной индустрии.
Ненадежность, опоздания, проблемы безопасности и даже плохая производительность в крупных
системах часто являются следствием неуправляемой сложности.
Как минимум понимание системы является необходимым требованием для избегания перечисленных проблем.

Актуальность проблемы сложности хорошо известна. Как говорит Дейкстра:

> ... мы должны добиваться предельной ясности и простоты, чтобы не оказаться погребенными
> под нами же созданной сложностью

Проведенные экономистами исследования показали, что в экономике США убытки
из-за проблем с информационными системами составляют приблизительно около $59 биллионов
долларов ежегодно.

Способность понимать и изменять информационные системы критически-важно.
Опасность сложности и важность простоты стала популярной темой в заслуженных лекциях
[Фернандо Корбато](http://en.wikipedia.org/wiki/Fernando_J._Corbat%C3%B3):

> Основная проблема амбициозных информационных систем это сложность...
> поэтому простота и элегантность приобретают особую важность, как путь преодоления сложности


В 1977 Бакус, говоря о сложностях и слабостях традиционных языков, заметил:

> Существует отчаянная необходимость в сильном методологическом подходе, которых
> помог бы нам понимать программы... существующие языки только вносят излишнюю путаницу

Во время своей речи при вручении награды Тюринга в 1989 Хоар сказал:

> ... есть одно качество, которое нельзя купить и это надежность. А цена надежности это простота.
> ... есть два способа написать программу: первый - это сделать ее настолько простой, что в ней не будет очевидных дефектов;
> второй - это сделать ее настолько сложной, что в ней не будет видно очевидных дефектов. Первый способ гораздо сложнее.

И это к сожалению правда - Добиться простоты сложно.

Но одна из целей этой статьи дать некоторые причины для оптимизма.

### Три способа понимания

Мы уже говорили, что основная угроза от сложности это ее влияние на понимание системы.
Поэтому интересно рассмотреть механизмы этого понимания:

* Черный ящик - когда мы смотрим на систему снаружи и заключаем о ней на основании
наблюдения за ее поведением

* Прозрачный ящик - не формальное изучение с заглядыванием внутрь, с надеждой, что эта дополнительная
информация позволит нам понять систему лучше

Из этих двух подходов более важным является второй.

    <p class="calibre1">Of the two informal reasoning is the most important by
    far. This is because — as we shall see below — there are inherent limits to
    what can be achieved by testing, and because informal reasoning (by virtue
    of being an inherent part of the development process) is always used. The
    other justification is that improvements in informal reasoning will lead to
    less errors being created whilst all that improvements in testing can do is
    to lead to more errors being detected. As Dijkstra said in his Turing award
    speech [<a href="references.html#Dij72" class="calibre2">Dij72</a>,
    EWD340]:</p>

    <p class="calibre1">“Those who want really reliable software will discover
    that they must find means of avoiding the majority of bugs to start
    with.”</p>

    <p class="calibre1">and as O’Keefe (who also stressed the importance of
    “understanding your problem” and that “Elegance is not optional”) said
    [<a href="references.html#OK90" class="calibre2">O’K90</a>]:</p>

    <p class="calibre1">“Our response to mistakes should be to look for ways
    that we can avoid making them, not to blame the nature of things.”</p>

    <p class="calibre1">The key problem with testing is that a test (of any
    kind) that uses one particular set of inputs tells you nothing at all about
    the behaviour of the system or component when it is given a different set of
    inputs. The huge number of different possible inputs usually rules out the
    possibility of testing them all, hence the unavoidable concern with testing
    will always be — have you performed the right tests?. The only certain
    answer you will ever get to this question is an answer in the negative —
    when the system breaks.  Again, as Dijkstra observed
    [<a href="references.html#Dij71" class="calibre2">Dij71</a>,
    EWD303]:</p>

    <p class="calibre1">“testing is hopelessly inadequate....(it) can be used
    very effectively to show the presence of bugs but never to show their
    absence.”</p>

    <p class="calibre1">We agree with Dijkstra. <em>Rely</em> on testing at your
    peril.</p>

    <p class="calibre1">This is <em>not</em> to say that testing has no use. The
    bottom line is that all ways of attempting to understand a system have their
    limitations (and this includes both <em>informal reasoning</em> — which is
    limited in scope, imprecise and hence prone to error — as well as <em>formal
    reasoning</em> — which is dependent upon the accuracy of a
    specification). Because of these limitations it may often be prudent to
    employ both testing and reasoning together.</p>

    <p class="calibre1">It is precisely because of the limitations of all these
    approaches that <em>simplicity</em> is vital. When considered next to
    testing and reasoning, simplicity is more important than either. Given a
    stark choice between investment in testing and investment in simplicity, the
    latter may often be the better choice because it will facilitate <em>all</em>
    future attempts to understand the system — attempts of any kind.</p>ппо

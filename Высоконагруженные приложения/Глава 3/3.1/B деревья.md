Журналированые индексы только набирают популярность, но наиболее широко используются b-деревья.

Появились в 1970 и через 10 лет уже использовались повсеместно. Эта структура данных прошла испытанием времени и используется почти во всех базах данных.

Аналогично SS таблица, b-дерево хранит пару ключ-значение в отсортированном по ключу виде. Но на этом сходство заканчивается, конструктивные сходства совсем другие.

Журнализированные индексы разбиваются на блоки обычно по несколько мегабайт и записываются на диск последовательно. Деревья разбивают БД на блоки, обычно по 4 Килобайт, читают и записывают по одной странице за раз. Это лучше для дисков, потому что они тоже разбиваются на блоки фиксированного размера.

Все страницы имеют свой адрес/местоположение, но уже на самом жестком диске, благодаря чему появляется возможность ссылаться на другие блоки индекса, благодаря чему создается дерево блоков/страниц.

![[Pasted image 20250425220647.png]]

Одна из страниц дерева назначается корнем b-дерева, это начало любого поиска. Данная страница содержит ссылки и диапазоны других страниц. Каждая из них отвечает за непрерывний диапозон ключей, а ключи располагающиеся между ссылками, указывают на расположение границ этих диапазонов. Переходя по диапозонам мы найдем нужную нам страницу содержащие отдельные ключи, которая содержит значение для всех ключей или ссылки где можно найти эти значения.

Количество ссылок на дочерние страницы на одной странице b-дерева называют коэффициентом ветвления. На рисунке выше, коэффициент равен 6. Обычно это значение зависит от жесткого диска и значение обычно это равно нескольким сотням.

При необходимости обновить нужно значение, доходим до нужной нам страницы-листа, меняем значение, а после перезаписать новое значение. В случае необходимости добавление нового ключа, находим нужный блок, добавляем значение, если в блоке недостаточно места, этот блок разбивается на два полупустых блока, а родительская страница обновляется.

Этот алгоритм гарантирует, что дерево будет сбалансированным, глубина дерева с ключами будет O (log n). Поэтому не придется ходить по множеству ссылок страниц. К примеру 4ех уровневое дерево страниц по 4 Кбайт с коэффициентом ветвления 500 может хранить 256 ТБайт данных.


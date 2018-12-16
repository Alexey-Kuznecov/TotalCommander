VirtualPanel plugin for Total Commander
---------------------------------------
(English section is below)

Реализация временной панели для Total Commander:
+ может хранить ссылки на файлы и каталоги, а также виртуальные каталоги
+ импорт/экспорт содержимого всей VP или отдельных папок
+ сохранение содержимого VP при выходе, завершении работы Windows, по таймеру или после модификации
+ импорт/экспорт списков имен файлов (например, m3u)
+ ведение лог-файла
+ удаление файлов физически при зажатой клавише Shift
+ корректная обработка операций копирования/перемещения
+ поддержка внутренних команд, расширяющих возможности (выполните команду ? для списка команд)
+ возможность выполнять команды блоками, а также создавать файлы скриптов
+ автовыполняемые скрипты при загрузке состояния или при входе в каталог
+ поддержка внутренних ассоциаций в ТК 7.51 и более поздних
+ поддержка стандартной в ТК команды cd
+ возможность выполнения внешних скриптов
+ поддержка многопоточности (фоновые операции в ТК 7.55 и более поздних)
+ виртуальный браузер с поддержкой перетаскивания файлов
+ полная поддержка Юникода


0. Некоторые условные обозначения

В большинстве случаев в этом файле для обозначения символов и строк используется синтаксис языка Си: символы заключаются в апострофы '', а строки - в кавычки "".

В описании команд параметры или флаги в квадратных скобках являются необязательными, конструкция вида {a|b} означает, что в данном месте нужно указывать либо a, либо b. Фигурные скобки, указанные без символа '|' внутри, как правило нужно указывать явно, т.к. в них заключаются некоторые параметры.


1. Файл конфигурации

Путь к файлу конфигурации ТК сообщает модулю при инициализации. Если этого не было сделано (например, версия программы ниже 5.51) или существует INI файл с именем модуля в его папке, этот файл будет использоваться как файл конфигурации. Кодировка файла может быть как ANSI, так и Юникод - ее можно изменить, пересохранив файл в любом текстовом редакторе.

Путь к файлу конфигурации можно узнать в окне свойств модуля (в сетевом окружении ТК).
Параметры секции [Virtual Panel]:

	AutoSaveInterval
		Интервал автосохранения файла автозагружаемого (главного) файла состояния в секундах;
	AutoSaveListOnEachOp=0
		Сохранять состояние по умолчанию после каждой операции с временной панелью (при наличии несохраненных изменений);
	AutoUpdateScriptName
		Скрипт с таким именем будет выполняться при каждом обновлении каталога;
	DefFileList
		Путь и имя файла главного файла состояния;
	DefFileListNewFormat=1
		Сохранять главный файл состояния в новом формате (занимает меньше места);
	EnableAutoScripts
		Маска выполнения автоматических скриптов;
	Language
		Имя выбранного файла языка сообщений (без пути и расширения);
	LogEnabled
		Маска протоколируемых событий;
	LogPath
		Путь и имя лог-файла;
	MaxLogSize
		Максимальный размер лог-файла в байтах, при достижении которого лог будет обнуляться (с сохранением предыдущей копии).
	RemovedFileIcon, RemovedFolderIcon
		Значки недоступных физических объектов (например, удаленных);
	SaveIniOnUnload=1
		Записывать параметры в файл конфигурации при выгрузке модуля;
	VirtualFolderIcon
		Путь и имя файла (также индекс через запятую) значка виртуального каталога;
	Explorer.RenameByF2=0
		Если опция включена, клавиша F2 в окнах виртуального браузера служит для переименования, если выключена - для обновления окна;
	Explorer.RightPixels=0
		Позволяет задать ширину свободной (последней) колонки в подробном режиме при автоматической подгонке - эта колонка используется для выделения мышью. Если параметр установлен в -1, автоматическая подгонка не используется;
	Explorer.SystemColors=0
		Если опция включена, в окнах виртуального браузера используется стиль Windows, а не ТК (работает быстрее).

Файлы языков сообщений должны находиться в подпапке Languages папки с модулем. Имена файлов произвольны, расширение должно быть .lng. Файлы являются INI файлами, в блоке [Virtual Panel] указываются значения строк с именами 1, 2, 3 и т.д. Вы можете использовать специальные символы "\t", "\n", "\r", '"' в строках; для указания символа '%' в форматных строках необходимо удваивать его, не удаляйте комбинации вида "%s", "%X" и т.п. Как и файл конфигурации, файл языка может быть как в ANSI, так и в Юникоде. Строки русского и английского языков зашиты в код и не требуют файла языка.

Используйте функции автосохранения с осторожностью. Если они будут включены, вполне вероятно, что не удастся отменить некоторые нежелательные изменения (удаление важного скрипта и т.п.). Также автосохранение может несколько замедлить работу, так как модуль будет периодически сохранять главный файл состояния (на время сохранения база блокируется). Вы можете использовать внешние скрипты для сохранения состояния, используя прилагаемую утилиту VPBatch - при этом будет возможность сохранять состояние в любое место или делать резервные копии файла состояния.

Параметр EnableAutoScripts содержит следующие биты: 1 - выполнять скрипты обновления каталога (если указано имя файла скрипта в параметре AutoUpdateScriptName), 2 - выполнять при каждом просмотре содержимого каталога (при поиске файлов и синхронизации), а не только при ручном входе в каталог, 4 - выполнять скрипт >Autoexec при загрузке файла состояния, 8 - не выдавать запрос на выполнение скрипта >Autoexec, 16 - выполнять скрипт >Shutdown при выгрузке модуля.

Если указан главный файл состояния, его содержимое будет загружаться автоматически при инициализации VP, а также сохраняться в этот файл при финализации (и при завершении работы Windows). Также, если указан параметр AutoSaveInterval, состояние системы будет автоматически сохраняться в этот файл с заданным интервалом времени (в фоновом потоке, при наличии изменений с момента прошлого сохранения). Во время сохранения состояния доступ к виртуальной системе будет блокирован. Сохранение производиться не будет, если у файла установлен атрибут только для чтения или отсутствуют права на запись в папку сохранения.

Протоколирование можно включать независимо для нескольких групп событий, указывая нужную комбинацию (сумму) битов маски (значения битов: 1 - начало/конец операций, 2 - действия с файлами, 4 - изменение атрибутов, 8 - перечисление файлов, 16 - выполнение скриптов, 32 - действия в окнах Virtual Explorer). Для включения всех категорий в качестве битовой маски можно использовать значение -1. Для лог-файла можно задать ограничение по размеру, изменив значение параметра MaxLogSize в файле конфигурации.

Значки виртуальных папок и недоступных физических объектов могут быть переопределены. В противном случае будут использоваться значки по умолчанию.

Все параметры файла конфигурации можно изменить непосредственно из диалога конфигурации. При нажатии кнопки ОК в диалоге конфигурации параметры сохраняются в INI-файл.


2. Общие возможности

После установки модуля его "папка" появляется в сетевом окружении, как и всех остальных модулей файловых систем.

Модуль поддерживает следующие типы объектов:
	Ссылка на файл/каталог - может находиться только в виртуальном каталоге, создается при добавлении физического файла на панель VP посредством операций копирования (только для файлов) или с помощью внутренней команды (и для каталогов), при обращении к ней происходит обращение к физическому объекту;
	Виртуальный каталог - обычный тип каталога, создается при копировании папок, а также при использовании команды создания каталога из интерфейса ТК;
	Виртуальный файл - объект, не ссылающийся на физический файл, но отображаемый на панели VP в виде файла (его поле реального объекта может быть пустым, но может содержать скрипт).

Реализованы все функции, поддерживаемые интерфейсом модулей файловых систем ТК (запуск, добавление, перемещение, копирование, удаление, отображение свойств). Если при удалении одного или нескольких объектов удерживать зажатой клавишу Shift (до появления диалога), будет показан диалог подтверждения удаления физических файлов (диалог будет показан в любом случае при попытке удаления файла внутри физического каталога). При копировании папки на панель VP происходит копирование структуры ее подкаталогов посредством виртуальных папок, а также добавление в них ссылок на файлы. Таким образом невозможно создать ссылку на физический каталог, т.к. ТК будет дублировать его структуру. Для создания ссылки на физический каталог можно использовать внутренние команды, или можно просто перетащить этот каталог в окно виртуального браузера. Удаление физических файлов по умолчанию производится в Корзину (если в настройках ТК не стоит удаление напрямую, и не зажата клавиша Shift при подтверждении удаления физических файлов).

Вы можете запускать программы посредством ссылок на файлы, при этом программа будет запущена из текущей папки (если вы находитесь в виртуальной папке, программа будет запущена из своей папки), а также указывать параметры командной строки, как в обычных папках. Кроме того, вы можете использовать команду cd для изменения текущей папки.

Можно использовать стандартные для ТК комбинации клавиш Ctrl+Влево/Вправо для перехода к файлу-источнику на другой панели. Кроме того, если установить фокус на файл или архив и нажать Shift+Enter, модуль откроет папку расположения файла (или содержимое архива) в новой вкладке.

При нажатии кнопки Отмена в окнах прогресса модулей файловых систем ТК не позволяет отменить прерывание. Данная возможность реализована в VP, при этом в силу особенностей ТК второй раз прервать операцию нажатием той же кнопки Отмена нельзя, для повторного отображения диалога прерывания операции необходимо нажать клавишу Esc. Это обусловлено тем, что после первой попытки прерывания ТК постоянно сообщает модулю, что операцию нужно прервать, и эти сообщения игнорируются.


3. Внутренние команды и скрипты

Команды расширяют функциональность модуля, позволяя выполнять действия, недоступные из интерфейса ТК напрямую. Каждая команда начинается с символа '<', в одной командной строке можно указать несколько команд одну за другой. Флаги команд указываются в одном параметре слитно. Последовательность команд образует скрипт.

Поддерживаемые внутренние команды:

	? (или любая неподдерживаемая команда)
		Открыть окно со списком поддерживаемых команд;
	add [/[r][f]] <virtual_path> [{<physical_path_or_script>}]
		Добавить ссылку на физический файл/каталог, виртуальную папку, или файл скрипта, в зависимости от значения второго параметра (скрипт необходимо заключать в фигурные скобки). Флаги: r - создавать промежуточные виртуальные папки, f - заменить существующий объект;
	cd <virtual_path>
		Изменить текущую папку в пределах текущего скрипта;
	config
		Показать окно настроек VP;
	convert <source_filelist_path> <filelist_path> [<virtual_path>]
		Преобразует список виртуальных путей или имён (получаемый в ТК с помощью %F, %L, %WL и т.д.) в список физических путей к файлам. Параметр virtual_path задаёт путь к базовой папке при поиске файлов по относительным путям (например, это должен быть путь к папке с файлами, список имён которых генерируется с помощью %F или %WF);
	deflist <filelist_path>
		Задать главный файл состояния;
	del [/[r][f][d[!]]] <virtual_path_and_mask>
		Удалить объект VP (можно указать маску для имён). Удаление физических объектов посредством данной команды невозможно. Флаги: r - удалять непустые виртуальные папки, f - файлы только для чтения, d - удалять также и папки (если сразу после d поставить !, то только папки);
	eas {<autoupdate_script_name> | <bit_mask>}
		Задать имя скрипта автообновления или маску запуска автовыполняемых скриптов (подробнее в разделе 1 данного Readme; чтобы установкить битовую маску -1, указывайте параметр "-1");
	edit <virtual_path> [<new_script_or_real_path>]
		Редактировать или изменить текст скрипта или путь к источнику для виртуальных объектов (если второй параметр не указан, будет показан диалог редактирования);
	exec [/w] <command> [<parameters>]
		Выполнить указанную команду, как если бы ее ввели в командной строке (например, для запуска скрипта из другого скрипта). Флаги: w - ждать завершения программы (ТК будет блокирован);
	exit
		Прервать выполнение текущего скрипта (запущенного командой exec или прямо из ТК);
	explore [<virtual_path>]
		Открыть новое окно браузера Virtual Explorer (подробнее в разделе 6 данного Readme);
	export [/[a][e][f][r]] <filelist_path> [<virtual_path> [{<masks>}]]
		Экспортировать содержимое всей структуры VP или указанной виртуальной папки в файл списка (только пути к файлам - например, для создания списка вопроизведения). Флаги: a - в кодировке ANSI, e - дописывать к существующему списку, f - перезаписывать существующий файл, r - рекурсивно;
	flush
		Записать параметры в файл конфигурации;
	for [/[d[!]] [%<symbol>] <virtual_path> {<masks>} {<script_to_execute>}
		Выполнить указанный скрипт для каждого найденного в указанном месте файла с именем, удовлетворяющим маске (маскам). Символ '%' и символ, указанные в заголовке команды, будут заменены путём к найденному объекту (или только именем, если после символа процента указать символ '~'). При использовании команды в файле скрипта символ '%' необходимо удваивать. Флаги: d[!] - искать и папки (если с '!', то только папок);
	ifcond {<expression> @ <virtual_path>} {<script_if_true>} [{<else_script>}
		Проверить, истинно ли выражение применительно к указанному файлу. Выражение может содержать числа, скобки, операторы +, -, *, /, условные операторы !, ||, &&, <, >, !=, <=, ==, >=. Помимо этого выражение может содержать ключевые слова, которые будут раскрыты: a[a|c|d|h|r|s|A|C|D|H|R|S] - наличие/отсутствие атрибута (регистр второго символа важен), date[now|ГГГГММДД], time[now|ЧЧММ] - дата и время объекта [или текущие/указанные] (преобразуются в число минут от 2000 года), size - размер файла, script - является ли файл скриптом, valid - доступность файла-источника, like "<mask>" - позволяет проверить, удовлетворяет ли имя файла маске. Если файл недоступен, атрибуты берутся из кэша. Если значение выражения больше 0, оно считается истинным, равно нулю - ложным, меньше нуля или ошибочное - ошибочным (при этом ни один скрипт выполнен не будет);
	ifdef <parameter> {<script_if_defined>} [{<else_script>}]
		Если параметр не пуст, выполнить первый скрипт, иначе - второй (если указан);
	ifexist <virtual_path_and_mask> {<script_if_exists>} [{<else_script>}]
		Если объект существует (при указании маски - хотя бы один), выполнить первый скрипт, иначе - второй (если указан);
	ifok <question_text> {<script_if_ok>} [{<else_script>}]
		Отобразить диалог вопроса с сообщением, и в зависимости от ответа выполнить первый скрипт или второй (если указан);
	lang <language>
		Переключиться на файл языка с указанным именем;
	load [<filelist_path> [<virtual_path>]]
		Добавить к содержимому указанной виртуальной папки содержимое файла состояния VP; если виртуальный путь не указан, выполняется загрузка файлав корневую папку VP, с удалением всего предыдущего содержимого;
	log {<full_path_to_file> | <bit_mask>}
		Задать маску событий для лога или имя лог-файла (подробнее в разделе 1 данного Readme; чтобы установкить битовую маску -1, указывайте параметр "-1");
	move <virtual_path> <new_virtual_path>
		Переместить или переименовать объект VP. Если получатель - существующая папка, объект перемещается в неё. Существующий объект (файл или папка) заменяется вместе с содержимым;
	properties
		Показать окно свойств и параметров VP;
	put [/[a][l][d[!]]] <virtual_path> <physical_path_and_mask>
		Добавить в виртуальную папку ссылки на указанные файлы из физического каталога. Флаги: a - переименовывать добавляемые файлы, если файл с таким именем существует, l - добавить файлы из набора списков файлов, d[!] - добавлять и папки (если с '!', то только папки);
	save [/[a][e][f][m][o][r]] [<filelist_path> [<virtual_path> [{<masks>}]]]
		Экспортировать содержимое всей структуры VP или указанной виртуальной папки в файл состояния (если путь не указан, сохраняется главный файл состояния). Можно указать маску файлов для экспорта. Флаги: a - в кодировке ANSI, e - дописывать к существующему списку, f - перезаписывать существующий файл, m - сохранение только при наличии изменений (единственный допустимый флаг при сохранении списка по умолчанию), o - сохранить полный список (старого формата), r - рекурсивно;
	silent
		Отключить информационные сообщения и сообщения об ошибках во время выполнения команд текущего скрипта;
	tgmove <virtual_path> <physical_path>
		Переименовать/переместить файл-источник элемента VP. Можно указать полный новый путь или только новое имя.

Команды <for, <export, <save поддерживают наборы масок для фильтрации объектов по именам. Наборы масок необходимо заключать в фигурные скобки, например {*.exe *.dat | s* t*} - набор масок для включения файлов *.exe и *.dat за исключением файлов, начинающихся с 's' или 't'.

Если в начале параметра указать символ '?', пользователю будет предложено ввести его значение во время выполнения команды. Если после символа '?' указать двоеточие и текст (как правило, текст с пробелами нужно заключать в кавычки - кроме параметра команды <exec), этот текст будет использован в приглашении ввода параметра. Нажатие клавиши Esc во время выполнения скрипта позволяет прервать его.

При использовании в скрипте вложенных скриптов (например, при добавлении файла скрипта) эти скрипты нужно заключать в фигурные скобки, в противном случае их команды будут считаться частью текущего скрипта. Также в фигурные скобки необходимо заключать все параметры, содержащие символ '<' (например, выражение команды ifcond). Переменные окружения раскрываются автоматически (для вложенных скриптов - во время их выполнения).

Имя файла скрипта должно начинаться с символа '>'. Для защиты файла скрипта от удаления можно установить атрибут только для чтения. Для файлов скрипта можно задать произвольный файл значка непосредственно в самом скрипте, для этого в конец скрипта нужно поместить два знака начала команды ("<<") и путь к файлу со значком (при необходимости также можно указать индекс значка через запятую). В файле скрипта можно использовать переменные окружения, обрамленные символом '%', знаки "%1"-"%9" для подстановки параметров, а также "%0" для подстановки имени файла скрипта. Чтобы вставить символ '%', нужно удвоить его ("%%").

Для запуска внешних программ из скриптов VP нужно добавить в VP ссылку на прилагаемую утилиту Exec и запускать внешние программы с ее помощью.

Файлы списков поддерживаются ANSI, UTF-8 и Unicode. Распознавание кодировки производится исключительно по маркеру в начале файла.


Пример добавления музыкальных файлов, содержащихся в нескольких m3u-списках в папке D:\Music, в папку \Music панели VP:
<put /al \Music D:\Music\*.m3u

Пример команды создания файла скрипта >Refresh для автоматической загрузки видео файлов в текущую виртуальную папку из нескольких физических:
<add >Refresh { <silent <del *.avi <put /a . "D:\Video\*.avi" <put /al . "E:\Video\*.lst" }

Пример создания файла скрипта, позволяющего рекурсивно удалять файлы по заданной маске в текущей папке и подпапках (с указанием значка для скрипта):
<add \>rdelete { <for %%f . "%1" { <del "%%f" } <for /d! %%d . * { <cd "%%d" <exec \>rdelete "%1" } <<shell32.dll,31 }

Пример команды удаления в текущей папке ссылок на файлы размером менее 1 КБ, измененные более 14 дней назад:
<for %f . * { <ifcond { !script && (size < 1024 && date < datenow - 14*24*60) @ %f } { <del "%f" } }

Пример команды удаления в текущей папке всех файлов кроме скриптов, mp3 и m3u:
<for %f . * { <ifcond { !script && !like "*.mp3" && !like "*.m3u" @ %f } { <del "%f" } }

Пример вышеописанной команды, но через использование набора масок (должно работать быстрее):
<for %f . {|*.mp3 *.m3u} { <ifcond { !script @ %f } { <del "%f" } }

Пример файла скрипта, перемещающего папку и выполняющего слияние, если папка назначения существует:
<ifdef "%2" { <for /d %%f "" "%1" { <ifcond "aD @ %2\%%~f" { <for /d! %%g "" "%%f\*" { <exec "%0" "%%g\*" "%2\%%~f\%%~g" } <for %%g "" "%%f\*" { <move "%%g" "%2\%%~f" } <exit } <move "%%f" "%2\%%~f" } } {<ifok {Syntax: >movx <what> <where>} {} }

Пример команды получения списка физических путей к файлам *.mp3 *.m3u | m* из виртуальной папки \Music в файл D:\1.m3u:
<export D:\1.m3u \Music {*.mp3 *.m3u | m*}

Пример команды, добавляющей ссылку на папку ТК (полезно в скрипте >Autoexec для флешки, позволяет запускать из VP программы из папки ТК):
<add /f \COMMANDER_PATH "%COMMANDER_PATH%"


4. Получение информации о файлах/каталогах на панели VP

Собственных информационных полей модуль не содержит, но, так как он является модулем временной панели, поддерживаются все поля других информационных модулей, а также стандартные поля ТК (например, комментарий, путь или имя файла). Например, чтобы увидеть полный путь к физическому файлу-источнику, добавьте колонку с шаблоном [=tc.path][=tc.fullname]. Перед настройкой колонок нужно выбрать модуль <Общие> в раскрывающемся списке над списком колонок.

Есть несколько способов получить содержимое файла скрипта. Один из них - с помощью поля Obj_RealPath из модуля NTLinks (он показывает содержимое скрипта для файлов скриптов). Также есть один способ, интересный принципом получения текста - нужно установить курсор на файл скрипта и нажать F3, при этом ТК покажет сообщение об ошибке открытия файла, в котором будет приведен текст скрипта (ТК в этом сообщении пишет некорректное имя файла, который не получилось открыть).


5. Выполнение внешних скриптов

VP позволяет выполнять скрипты, отправляя ТК специальное сообщение WM_COPYDATA со структурой COPYDATASTRUCT, поле dwData которой должно быть равно 0x5056 (для скрипта в кодировке ANSI) или 0x00500056 (для скрипта в Юникоде), а поле lpData должно указывать на текст скрипта в соответствующей кодировке. Перед скриптом можно указывать строку, содержащую имя модуля VP, который должен выполнить скрипт, а также виртуальную папку, из которой запускать скрипт, в таком случае они разделяются символом '\r', а после папки ставится нулевой символ, за которым идет сам скрипт. Если рабочая папка не указана, будет использована папка, содержимое которой ТК запрашивал последней (наиболее вероятно, что она будет текущей). Для запуска файла из VP используйте команду <exec.

При изменении текущей папки VP новая папка прописывается в переменную окружения "${Virtual Panel}Path", где "Virtual Panel" - имя модуля VP в ТК. Также путь прописывается в переменную "${}Path" - но эта переменная является общей для всех VP, загруженных в ТК.

Вы можете использовать прилагаемую утилиту VPBatch для выполнения скрипта в VP, загруженной в ТК.

Синтаксис командной строки:
VPBatch[.exe] [<параметры>] <скрипт>

Поддерживаемые параметры:
/q"^" - задает символ, который будет заменен на '<' (по умолчанию используется символ '^'; сам символ '<' нельзя использовать в параметрах)
/r"Virtual Panel" - задает имя модуля VP, который должен выполнить команду (если загружено несколько VP)
/r"\\\Virtual Panel\..." - то же, что и выше, но имя модуля извлекается из пути в стиле ТК (для кнопок панели инструментов)
/w"<virtual_path>" - задает рабочую виртуальную папку

Не забывайте, что при вызове VPBatch из командного файла перед символами ^ и > необходимо ставить дополнительный символ ^.

Пример кнопки панели инструментов ТК для добавления ссылки на физический каталог:
VPBatch.exe ^exec { ^ifok "Добавить ссылку на объект как %%${}Path%%"\%N? { ^add /r %N %P%N } {} }


6. Virtual Explorer

Virtual Explorer - это виртуальный браузер, позволяющий открывать любое число окон (новое окно открывается внутренней командой <explore). Каждое окно может отображать содержимое виртуальной или физической папки, ссылка на которую есть в панели (в таком случае в заголовке окна отображается реальный путь), ведется история последних 20 посещенных каталогов. Поддерживается выделение левой кнопкой мыши (как в проводнике Windows).

В окнах браузера поддерживаются следующие комбинации клавиш:
	Alt+Enter
		Показать системные свойства объекта;
	Alt+Влево/Alt+Вправо
		Перейти к предыдущему/следующему каталогу в истории;
	Alt+Вниз
		Показать выпадающее меню с историей каталогов;
	Backspace
		Перейти на уровень вверх;
	Ctrl+\
		Перейти в корневой каталог;
	Ctrl+C
		Прервать чтение содержимого каталога;
	Ctrl+A/Ctrl+Num +
		Выбрать все файлы и папки;
	Ctrl+Num -
		Снять выделение;
	Num *
		Инвертировать выделение;
	Del
		Удалить выбранные элементы (клавиша Shift может использоваться для удаления физических объектов);
	Shift+F6
		Переименовать объект под курсором;
	F2/Ctrl+R
		Обновить содержимое окна;
	Ctrl+F1/Ctrl+F2
		Переключить режим отображения;
	F12
		Переключить режим "поверх других окон";
	Esc
		Закрыть окно браузера.

Реализована возможность перетаскивания файлов между окнами браузера и внешними приложениями (на данный момент файлы перетаскиваются в окна внешних приложений только с их реальными именами, а не виртуальными), также поддерживаются удаление и переименование элементов.


Обсуждение на официальном русскоязычном форуме: http://forum.wincmd.ru/viewtopic.php?t=12969



VirtualPanel plugin for Total Commander
---------------------------------------
(English section)

(If you find any errors in this readme file, please help me to fix them)

Temporary panel plugin for Total Commander:
+ keeps links to files and folders, and virtual folders
+ import/export of whole contents or separate directories
+ saving VP state on exit TC or Windows, by timer or after each modification
+ import/export of usual filelists (like m3u)
+ log file
+ asks for physical removing if Shift is down
+ correct copy/move operations processing
+ internal commands for extra functions (execute ? command for help)
+ batch commands execution and script files support
+ autoexecuted scripts on load state or enter directory
+ supports internal associations in TC 7.51 and later
+ standard cd command support in TC
+ external scripts support
+ multi-threading support (background operations in TC 7.55 and later)
+ virtual explorer with drag-and-drop support
+ full Unicode support


0. Some notation conventions

In most places of this file C language syntax is used to indicate characters and strings: characters are enclosed with apostrophes '' and strings are enclosed with double quotes "".

In command descriptions parameters or flags in square brackets are optional, construction like {a|b} means that either a or b should be used. Curly braces that don't have '|' symbol inside usually should be specified explicitly because they enclose some parameters.


1. Configuration file

Total Commander passes INI file name on plugin loading. If not (e.g. TC version earlier than 5.51) or if INI with plugin's name exists near the plugin, this file will be used as configuration file. File encoding may be ANSI or Unicode - you may change it manually using any text editor.

You may open plugin properties to get path to INI file.
Parameters in [Virtual Panel] section:

	AutoSaveInterval
		Default state file autosave interval in seconds;
	AutoSaveListOnEachOp=0
		Save default state file after each operation with virtual panel (if there are unsaved modifications);
	AutoUpdateScriptName
		Name of script file that will be executed on enter directory;
	DefFileList
		Path to default state file;
	DefFileListNewFormat=1
		Save default filelist using new compact format (uses less disk space);
	EnableAutoScripts
		Automatic scripts execution flags;
	Language
		Current language file name (just name w/o path and extension);
	LogEnabled
		Log event mask;
	LogPath
		Path to log file;
	MaxLogSize
		Max log file size in Bytes (when file size exceeds this limit, it will be renamed and new log file will be started).
	RemovedFileIcon, RemovedFolderIcon
		Icons for inaccessible physical objects (e.g. removed);
	SaveIniOnUnload=1
		Save parameters into configuration file on unload plugin;
	VirtualFolderIcon
		Virtual folder icon path and index after comma;
	Explorer.RenameByF2=0
		If this option is enabled, F2 key renames focused item, else refreshes Virtual Explorer window;
	Explorer.RightPixels=0
		Specifies width of unused (last) column in full view mode after auto realigning - this column is useful for mouse selection. If option is set to -1, auto realigning not used;
	Explorer.SystemColors=0
		If this option is enabled, Windows style used in Virtual Explorer windows instead of TC style (works faster).

Language files must be placed into Language folder near plugin, have any name and extension .lng. Language files are simple INI files, file must have [Virtual Panel] section with translated strings which have names 1, 2, 3 etc. You may use "\t", "\r", "\n" and '"' special characters in strings. In format strings you need to double '%' character, also do not remove combinations like "%s" or "%X" in such strings. Language file may be in ANSI or Unicode. Russian and English languages are hardcoded and don't require language file.

Please be careful with autosave feature. If you enable it and then do some unwanted modification (delete some useful scripts etc) you may lose previous state (by default state is saved only when plugin is unloaded). Also autosave may slow down your work since it plugin will save state file periodically (base is blocked during saving). You may use external scripts for saving state periodically using attached tool VPBatch - you will have chance to specify any path to state file or make backups of state file.

Parameter EnableAutoScripts supports following bits: 1 - use autoupdate scripts on enter directory (if AutoUpdateScriptName contains its name), 2 - execute enter directory script on each folder list (also during file search/sync) instead of execution only on manual browse, 4 - execute >Autoexec script on load state file, 8 - don't ask confirmation on >Autoexec script file execution, 16 - execute >Shutdown script on plugin unload.
	
If DefFileList parameter is specified, this file will be loaded automatically on VP start and saved on exit TC (also on exit Windows). Also, if AutoSaveInterval parameter is specified, VP will save state into this file automatically with given interval (in background thread, only when changes are made since last save). During saving virtual system access is blocked. If you set read-only attribute, this file won't be replaced. Also file won't be saved if there is no write access to save folder.

You may enable log for some event types by combining bits (by summation) in the mask (bits are: 1 - operation start/end, 2 - file actions, 4 - attributes setting, 8 - enum files actions, 16 - scripts execution, 32 - actions in Virtual Explorer windows). To enable all events you may use -1 value as bit mask. Note that you may limit log file size using MaxLogSize parameter in INI.

Virtual folders and links to inaccessible physical objects have special icons. You may edit INI in order to specify any other icons for theese objects.

All configuration parameters may be changed directly from configuration dialog. When you click OK button configuration is saved into INI file.


2. General features

After installing plugin, it can be accessed via Network Neighbourhood just like any other file system plugin.

Following object types are supported:
	Physical file/folder link - may be situated in virtual folder only, created when you add file into VP by copying (only for files) or with help of internal command (also for folders), you may access physical object via this link;
	Virtual folder - usual folder, TC creates it when you copy folder into VP or when you make new folder;
	Virtual file - object that have no link to physical file but TC shows it as a file (it may contain empty real path field or internal script in it).

All supported by Total Commander's FS interface functions are realized (execution, adding, moving, copying, removing, properties displaying). When you hold Shift while confirm deletion, plugin will ask you for physical files remove confirmation (confirmation is asked always when you remove files within physical folder link). When you copy folder into VP, TC copies its structure with virtual folders and file links, you can't create physical folder link directly. You need to use internal commands for adding physical folder links, or you may simply drop that folder into virtual explorer window. When removing physical files, they are placed to Recycle Bin by default (if TC configured to delete directly or Shift key was held on confirm physical files deletion, files are deleted directly).

When you execute application via file links, program launches from its directory (if you're in virtual folder) or from current physical folder (if you're inside of physical folder link). Also you may run programs with parameters and use standard cd command to change current path.

You may use standard TC shortcuts Ctrl+Left/Right if you want to jump to target physical file in inactive panel. Also, if you put focus onto file or archive and press Shift+Enter, VP will jump to this file (or shows archive contents) in new tab.

When you click Cancel in file system progress dialogs, TC doesn't allow to undo aborting. However VP supports such feature, but due to TC limitations it is possible to abort operation by clicking Cancel button only once, next time you will need to press Escape key to display abort dialog. The reason is that module ignores continuous TC notifications about cancelling after first Cancel clicking.


3. Internal commands and scripts

Commands allow to extend plugin functionality. They allow to perform actions unavailable directly from TC interface. Each command must be started with '<' character, you may specify more than one command sequentially in command line. Command flags should be specified in a single parameter w/o spaces. Script is a sequence of commands.

Supported internal commands:

	? (or any unsupported command)
		Show message with list of supported commands;
	add [/[r][f]] <virtual_path> [{<physical_path_or_script>}]
		Add physical file/folder link or a virtual folder or a script file depending on second parameter's value (you must enclose script into braces). Flags: r - create intermediate virtual folders, f - replace existing object;
	cd <virtual_path>
		Change current folder within current script;
	config
		Display settings dialog;
	convert <source_filelist_path> <filelist_path> [<virtual_path>]
		Converts list of virtual names or paths (that may be got via TC parameters like %F, %L, %WF etc.) into list of physical paths to files. Parameter virtual_path sets base virtual path for relative paths in a list (e.g. it should be path to folder with files whose names are listed by %F or %WF);
	deflist <filelist_path>
		Set default state file;
	del [/[r][f][d[!]]] <virtual_path_and_mask>
		Remove VP object (or multiple using mask). You can't remove physical objects with this command. Flags: r - remove non-empty folders, f - remove read-only files, d[!] - remove folders too (with ! - folders only);
	eas {<autoupdate_script_name> | <bit_mask>}
		Set autoupdate script name or autoexecution flags (refer to secion 1 of this Readme for details; in order to set -1 as bit mask use "-1" instead);
	edit <virtual_path> [<new_script_or_real_path>]
		Сhange script text or target path for object. If second parameter is not specified, edit dialog will be shown;
	exec [/w] <command> [<parameters>]
		Execute command as if you enter it in command line (e.g. allows to start another scripts from scripts); Flags: w - wait for program termination (TC will be blocked);
	exit
		Exit from current script (started using exec command or from TC directly);
	explore [<virtual_path>]
		Open new Virtual Explorer window (refer to secion 6 of this Readme for details);
	export [/[a][e][f][r]] <filelist_path> [<virtual_path> [{<masks>}]]
		Export whole VP contents or contents of specified virtual folder into list file (just real paths - e.g. for Playlist creation). Masks allow to filter files to be exported. Flags: a - use ANSI encoding, e - append to existing list, f - overwrite existing file, r - recursively;
	flush
		Save parameters into configuration file;
	for [/[d[!]] [%<symbol>] <virtual_path> {<masks>} {<script_to_execute>}
		Execute some script for each matched object that can be found in specified folder. Percent sign with specified symbol found in script text will be replaced with object path (or just filename if '~' is specified after '%'). You need to double '%' symbol in script files. Flags: d[!] - search folders too (with '!' - folders only);
	ifcond {<expression> @ <virtual_path>} {<script_if_true>} [{<else_script>}
		Check condition for specified file. Expression may contain numbers, round brackets, operators +, -, *, /, conditional operators !, ||, &&, <, >, !=, <=, ==, >=. Also expression may contain keywords that will be expanded to values: a[a|c|d|h|r|s|A|C|D|H|R|S] - check attribute (attribute char case is important), date[now|YYYYMMDD], time[now|HHMM] - file date and time [or current or specified] (values converted to minutes since year 2000), size - file size, script - is it script file or not, valid - target accessibility, like "<mask>" - alows to check if file name matches mask. If target file is inaccessible, attributes are taken from cache. If value of expression is larget than 0, its true, if it is equal to 0, its false, else it is treated as faulty (no script will be executed in this case);
	ifdef <parameter> {<script_if_defined>} [{<else_script>}]
		If parameter is not blank, execute first script, else second (if specified);
	ifexist <virtual_path_and_mask> {<script_if_exists>} [{<else_script>}
		Execute first script if object exists (at least one that matches), else second (if specified);
	ifok <question_text> {<script_if_ok>} [{<else_script>}]
		Display question dialog and executes first or second (if specified) script depending on user's answer;
	lang <language>
		Switch language to specified language file;
	load [<filelist_path> [<virtual_path>]]
		Add objects from specified VP state file to contents of specified virtual folder; if virtual path is omitted, command clears VP and loads specified state file as root;
	log {<full_path_to_file> | <bit_mask>}
		Set log file path or log events mask (refer to secion 1 of this Readme for details; in order to set -1 as bit mask use "-1" instead);
	move <virtual_path> <new_virtual_path>
		Move or renames VP object. If destination is an existing folder, object is moved into it. Existing object (file or folder) will be replaced with all contents;
	properties
		Display properties dialog;
	put [/[a][l][d[!]]] <virtual_path> <physical_path_and_mask>
		Add links to specified physical objects. Flags: a - autorename files if such file already exist, d[!] - folders too (with '!' - folders only), l - add objects from specified file lists;
	save [/[a][e][f][m][o][r]] [<filelist_path> [<virtual_path> [{<masks>}]]]
		Export whole VP contents or contents of specified virtual folder into state file (if path is omitted default state file is saved). Masks allow to filter files to be exported. Flags: a - use ANSI encoding, e - append to existing list, f - overwrite existing file, m - save only if state was changed (the only flag used when default state file is saved), o - save full (old-style) list, r - recursively;
	silent
		Disable information and error messages until end of current script;
	tgmove <virtual_path> <physical_path>
		Allows to rename/move target object. New path may be full name or just filename.

Commands <for, <export, <save support multiple masks for filtering objects. If you specify multiple masks, you must enclose mask set with curly braces, e.g. {*.exe *.dat | s* t*} - mask set that includes files *.exe and *.dat except ones whose names start with 's' or 't'.

You may replace any parameter with '?' symbol if you want this parameter to be asked during script execution. If you specify a colon with following text (usually in quotes if text contains spaces - except for <exec command), this text will be used as ask param dialog text. Also you may interrupt script execution by pressing Esc key.

When you specify nested scripts (e.g. while adding script file) you must enclose each nested script into braces. If not, commands inside of script will be treated as commands of current script. Also it is necessary to enclose into braces all parameters containing '<' character (e.g. ifcond command expression). You may use environment variables in commands and scripts - they are expanded automatically (variables inside script files will be expanded during script execution).

Script file name must be started with '>' character. You may set read-only attribute for script file in order to protect it from removing. Script file has special icon, but you may also specify any external icon. You should specify external icon path (and index after comma, if need) after pair of less-than signs ("<<") at the end of script. In script files you may use environment variables inside pair of '%' chars, symbols "%1"-"%9" to paste parameters, "%0" to paste script file path. You must double '%' char to paste it ("%%").

In order to start external programs from VP scripts you need to add to VP link to attached tool Exec and use it to start external programs.

Supported file lists encodings (for put command) are ANSI, UTF-8 and Unicode. File must have byte order marker set at the beginning to allow encoding detection.


Example of command to add to \Music virtual folder all files from m3u lists in D:\Music physical folder:
<put /al \Music D:\Music\*.m3u

Example of command that creates >Refresh script file that will load video files from some physical folders into current virtual folder:
<add >Refresh { <silent <del *.avi <put /a . "D:\Video\*.avi" <put /al . "E:\Video\*.lst" }

Example of script file creation that allows to remove files by mask in current directory and its subdirectories recursively (script file will have custom icon):
<add \>rdelete { <for %%f . "%1" { <del "%%f" } <for /d! %%d . * { <cd "%%d" <exec \>rdelete "%1" } <<shell32.dll,31 }

Example of command that deletes all files with size less than 1 KB modified more than 14 days ago in current directory:
<for %f . * { <ifcond { !script && (size < 1024 && date < datenow - 14*24*60) @ %f } { <del "%f" } }

Example of command that deletes all files except scripts and *.mp3 and *.m3u in current directory:
<for %f . * { <ifcond { !script && !like "*.mp3" && !like "*.m3u" @ %f } { <del "%f" } }

Example of same command like above but using multiple masks (should work faster):
<for %f . {|*.mp3 *.m3u} { <ifcond { !script @ %f } { <del "%f" } }

Example of script file to move folders and merge them if destination exists:
<ifdef "%2" { <for /d %%f "" "%1" { <ifcond "aD @ %2\%%~f" { <for /d! %%g "" "%%f\*" { <exec "%0" "%%g\*" "%2\%%~f\%%~g" } <for %%g "" "%%f\*" { <move "%%g" "%2\%%~f" } <exit } <move "%%f" "%2\%%~f" } } {<ifok {Syntax: >movx <what> <where>} {} }

Example of command to export list of physical paths for files *.mp3 *.m3u | m* from virtual folder \Music into file D:\1.m3u:
<export D:\1.m3u \Music {*.mp3 *.m3u | m*}

Example of command to add link to TC folder (useful in >Autoexec script on USB stick, allows to start TC tools from VP):
<add /f \COMMANDER_PATH "%COMMANDER_PATH%"


4. Getting information about VP objects

Plugin have no own content fields but temporary panel plugin supports all content plugins fields and standard fields for physical files and folders (e.g. comment field or path field). E.g. to retrieve full path to physical target you should use [=tc.path][=tc.fullname] pattern for column. Do not forget to change file system to <General> in drop-down combo box above column sets list.

There are a lot of ways to get script file contents. One of them is to use Obj_RealPath field of NTLinks plugin (it shows script text for script files). Also there is an interesting way to get script text - you should place cursor onto script file and press F3 key. TC will show you error message with script text.


5. External script execution

VP allows to execute scripts by sending to TC special WM_COPYDATA message with COPYDATASTRUCT struct; dwData field of that struct must be set to 0x5056 (for script in ANSI) or to 0x00500056 (for script in Unicode); lpData field should point to script text to execute. Optionally before script text you may specify root name of VP that should execute script and work path; they must be separated with '\r' character, also null character with following script text must be specified after path. If work path is not specified, VP will use path that was listed in TC last time (most probably it is current virtual path). If you need to execute file from VP, use <exec command.

When current virtual folder changes, new path sets to environment variable "${Virtual Panel}Path", where "Virtual Panel" - VP root name in TC. Also, path sets to variable "${}Path" - but this variable is used by all VPs loaded in TC.

You may use attached tool VPBatch to execute script in VP, loaded in TC. 

Launch VPBatch w/o parameters to read about command line syntax.

Don't forget that if you call VPBatch from batch file you need to add additional ^ character before characters ^ and >.

Example of TC buttonbar button for adding physical folder as link:
VPBatch.exe ^exec { ^ifok "Add as %%${}Path%%"\%N? { ^add /r %N %P%N } {} }


6. Virtual Explorer

Virtual Explorer allows to have any number of browser windows (new window may be opened via <explore internal command). Every window may display virtual folder contents or real one if you have link to it (real path is displayed in window title in this case), last 20 visited folders are kept in browser history. Only left button selection mode is supported (like in Windows Explorer).

Supported keyboard shortcuts are:
	Alt+Enter
		Show properties;
	Alt+Left/Alt+Right
		Navigate through folder history;
	Alt+Down
		Open drop-down folder history menu;
	Backspace
		Go to parent directory;
	Ctrl+\
		Go to root directory;
	Ctrl+C
		Interrupt reading folder contents;
	Ctrl+A/Ctrl+Num +
		Select all files/folders;
	Ctrl+Num -
		Remove selection;
	Num *
		Invert selection;
	Del
		Delete selected items (Shift modified may be used to remove physical objects too);
	Shift+F6
		Rename focused object;
	F2/Ctrl+R
		Reread folder contents;
	Ctrl+F1/Ctrl+F2
		Change folder view mode;
	F12
		Switch "always on top" mode;
	Esc
		Close browser window.

You may drag files between theese windows and external applications (currently dragged to external applications files get original names and not virtual ones), also delete and rename operations are supported.


Discussion page on official board: http://www.ghisler.ch/board/viewtopic.php?t=24293



History:

2013-10-06	2.0.7.1354
	+ sample BAR file added to the plugin package
	* explorer: sometimes item filled with inversed color after hovering it
	* explorer: use proper default text and background colors if not set in TC
	* plugin placed misconfigured VirtualPanel.ini to its folder during installation (introduced in 2.0.7.1330)

2013-08-09	2.0.7.1340
	+ plugin file name used as default root name
	+ explorer: InverseSelection support
	+ explorer: double buffering is now used
	+ explorer: option to use Windows colors (faster)
	* explorer: flickering split cursor fixed
	* explorer: some color fixes
	* explorer: if no selection, focused item is dragged
	* explorer: sometimes focus rectangle disappeared after clicking some item
	* truncate list file after writing
	* fixed copy error in Windows 2000 (introduced in 2.0.6.1264)

2012-11-13	2.0.6.1264
	+ copying encrypted files to target that doesn't support encryption (moving is still not allowed)

2012-10-26	2.0.6.1262
	+ <convert command
	+ multiple include/exclude masks support in <for, <export, <save commands
	+ flag 'e' for <save, <export commands
	* <save command is not recursive by default now (use 'r' flag)
	* null characters in ANSI exported lists
	* correct icons for inaccessible files (like pagefile.sys)
	* explorer: paths for subfolders of links to physical folders haven't displayed in title

2012-09-22	2.0.5.1228
	+ <tgmove command now allows to move files between volumes
	* improved confirm dialog centering
	* fixed direct date/time calculation in <ifcond command (dateYYYYMMDD and timeHHMM)
	* load incomplete language file issue
	* some language corrections

2012-03-03	2.0.5.1208
	+ 64-bit version of Exec.exe added (allows to start processes like regedit.exe in 64-bit environment)
	* FsGetDefRootName returned "Virtual Pane" instead of "Virtual Panel" as default plugin root name (introduced in 1.0.0.922)
	* explorer: enormous font (introduced in 2.0.5.1206)

2011-09-19	2.0.5.1200
	+ 64-bit version of plugin added (requires 64-bit TC version)

2011-09-04	2.0.4.1154
	* loading external icons for scripts bug (introduced in 2.0.4.1150)
	* executing via command line bug (introduced in 2.0.4.1150)

2011-09-03	2.0.4.1150
	+ log report on save deflist (flag 2)
	* explorer: Del deleted all items if ".." was focused and no items selected
	* dynamic TLS is now used instead of static which is buggy for dynamic libraries
	* log string formats for FsDeleteFile, FsRemoveDir, FsMkDir, FsSetAttr slightly changed
	* log string format bug for FsSetTime
	* rename via <move command bug when only name characters case is changed
	* tab order in configuration dialog

2011-07-17	2.0.3.1120
	+ explorer: always on top toolbar button and F12 key
	+ explorer: now is able to delete physical folders recursively
	+ explorer: remove selection mark from focused item if no selection
	* <ifcond function now uses API to calculate exact number of minutes
	* explorer: bad colors when color values are set to -1 in wincmd.ini
	* explorer: focused item didn't become selected on Ctrl+A if inversed cursor used
	* explorer: Del deleted all items if no items were selected

2011-04-13	2.0.1.1090
	+ explorer: history item moves to end when clicked
	+ explorer: Alt+Down shows history
	+ explorer: Explorer.RenameByF2 and Explorer.RightPixels INI options
	* explorer: doesn't erase all history items after current on dir change
	* explorer: drag from root bug
	* explorer: couldn't enter folders after going to root using Ctrl+\
	* wrong processing of "like" operator argument for <ifcond command

2011-04-11	2.0.0.1080
	+ virtual explorer allowing to have any number of browser windows
	+ virtual explorer interface tries to copy TC style
	+ drag-n-drop support between virtual browser windows and external applications
	+ new log event for Virtual Explorer actions
	+ max state file line length is now 8k characters
	+ <put command may add folders from lists created via e.g. cm_SaveSelectionToFile (trailing folder slashes are now stripped)
	+ <edit command now allows to edit empty targets for files
	* recursive intermediate folders creation bug (after some changes in 1.0.0.920)
	* <for command produced wrong names
	* bits 0x01 and 0x02 of LogEnabled parameter exchanged
	* log string format for FsPutFile slightly changed

2011-03-12	1.0.0.920
	+ VPBatch now accepts root name in both direct form and TC-style path form (\\\Virtual Panel\...)
	+ own environment variables expander (leaves %xx% as is if variable xx is undefined)
	+ long scripts are now saved w/o truncation
	* save bug when long scripts are used
	* exception while processing long scripts that were sent via WM_COPYDATA in Unicode

2010-12-01	1.0.0.904
	+ log now shows thread id (for background threads detection)
	* some optimizations
	* correct retrieving plugin version info on Windows 2000
	* wrong filelists processing e.g. in <put command (after some changes in 1.0.0.850)
	* some small fixes

2010-07-12	1.0.0.820
	+ flag 'm' for <save command
	+ autosave after every operation feature (only if state was modified) - you may enable it in settings

2010-05-13	1.0.0.800
	+ always starts executables (.exe, .lnk, .cmd, .bat, .com) itself to set right working path
	+ overwrites list files w/o deleting (preserves attributes and permissions)
	* wrong working path for executables started from command line within virtual folder

2010-04-21	1.0.0.780
	+ always returns FS_EXEC_OK on show properties (TC doesn't show ugly dialog on error)
	+ allows to abort operations by first pressing Cancel button (if user cancels aborting then only by Escape)
	+ thread local storage is used for storing thread-specific data
	* wrong properties dialog for pure virtual objects

2010-04-15	1.0.0.760
	+ flag f for <save and <export commands to overwrite existing file
	+ may execute special >Shutdown script on plugin unload
	+ configuration is saved to INI when user clicks OK button in configuration fialog
	+ new INI parameter SaveIniOnUnload allows to disable saving INI on exit
	+ <flush command to manual save configuration to INI file
	+ <tgmove command to rename/move target object (link is fixed automatically)
	+ log event flag for scripts execution
	+ status log message for VPBatch commands

2010-04-12	1.0.0.700
	+ put, renmove, mkdir operations create absent intermediate folders
	* Ctrl+Tab didn't work after pressing Apply button
	* focus bug in confirmation dialog
	* <exec command bug if parameter was in braces

2010-04-09	1.0.0.690
	+ group answers for link creation question when user tries to move physical file to virtual folder
	+ new settings tab in configuration dialog
	+ configuration dialog uses Windows theme colors (calls EnableThemeDialogTexture function if available)
	+ buttons OK, Cancel, Apply in configuration dialog
	+ internal command <config to show settings tab of configuration dialog
	* open properties command in TC 7.55 was overridden by internal execute feature
	* exception on move from physical folder to virtual
	* overwrite read-only physical file error
	* bug in <save command when started w/o params and user answers No on save deflist question
	* changed line order in information box of configuration dialog (localization line 8)

2010-04-01	1.0.0.620
	+ compact state file format
	+ flag 'o' for <save command to save old-style state file
	+ safe multi-thread enum files (list builds in single critical section during FsFindFirst call)
	+ faster saving (files in subfolders now searched from folder handle and not from root)
	+ faster loading/unloading large states (now boost::fast_pool_allocator is used as map allocator)
	* wrong <for parameters order
	* set time/date for script files bug
	* <put command accepted relative path incorrectly
	* wrong mask processing by <export command

2010-03-29	1.0.0.580
	+ environment variables ${Virtual Panel}Path and ${}Path keep last listed VP path
	+ new flags for <add command (to replace existing object and to create intermediate virtual folders)
	+ multi-thread access to virtual system
	+ <move command
	+ <for command now replaces %~<symbol> with just filename
	+ allows to cancel aborting of any operation (checks if Escape is held instead of accepting TC abort flag)
	* Shift+Enter jumped to file's folder instead of jumping to file (after some changes in 1.0.0.550)
	* Shift+Enter in TC 7.55 was overridden by internal execute feature
	* <for command parameters processing bug
	* buggy parsing paths with ".."
	* removed questions in <save and <export commands after <silent

2010-03-24	1.0.0.550
	+ changed default image base address
	+ now VP may execute scripts sent to TC using WM_COPYDATA message
	+ attached tool VPBatch to send scripts to VP
	* blocks multiple timer event thread creation (event skipped if previous yet working)
	* kills timers and waits for exiting timer event processors when plugin is unloading
	* log path changing from configuration dialog now works
	* fixed launching applications from physical folder

2010-03-15	1.0.0.520
	+ autosave default state file by timer feature
	+ new operator "like" for <ifcond command allows to check if filename matches mask
	+ <exec command now asks for command line if parameter begins with '?'
	+ expanding environment variables in parameters for launched executables
	+ shows help on "?" command too
	+ if parameter looks like ?:"<text>", text is used as ask param dialog text
	* wrong environment variables processing in cd command
	* reread source call after operations removed
	* read-only files delete mode bug
	* "%%" parsing error in script files

2010-03-08	1.0.0.500
	+ supports internal associations in TC 7.51 and later
	+ saves state on exit Windows
	+ multi-thread safe virtual system access
	+ non-modal configuration dialog
	+ standard cd command support in TC

2010-02-25	1.0.0.494
	+ information box in cfg dialog and language, icons etc are updated after changing parameters if need
	+ links to inaccessible folders are treated now as empty folders so TC may delete them
	+ shows time for each log line
	+ percent char in script files is now processed like in usual batch files
	* changed font in cfg dialog and tab view (in some Windows themes vertical tabs are buggy)
	* empty text now may be accepted as parameter value in cfg dialog
	* wrong detection of flag 'a' in <put command

2010-02-17	1.0.0.470
	+ configuration dialog
	+ moving from VP (physical file is copied and link is removed)
	+ <put command may now add files or folders or both
	+ flag 'a' for <put command to autorename file if such file already exists
	+ flag 'w' for <exec command to wait for process termination
	* fixed physical moving from VP (file was moved but link was left)

2010-02-11	1.0.0.420
	+ Shift+Enter jumps to file or enters archive in new tab
	+ new keyword to detect scripts (for <ifcond command)
	+ ifcond now understands relative paths
	+ log file size limit feature
	* fixed dates comparing in <ifcond command (wrong conversion to number of minutes)
	* check for existance before starting autoupdate script (avoid some execution errors)
	* %0 in script now treated as script filename
	* trailing spaces in condition of <ifcond command are removed
	* fixed exporting filenames in ANSI (Unicode w/o BOM was written)

2010-02-06	1.0.0.400
	+ removes physical files to recycle bin by default (checks if Shift is held and corresponding TC setting before)
	+ default filelist now is saved on exit only if VP state was modified during session
	+ <load command may be executed w/o parameters now for loading default filelist state
	+ <eas command now allows to change autoupdate script name
	+ new flag 'a' for <save/<export to save with ANSI encoding
	+ new command <ifcond that allows to check file attributes etc
	* removed locked dialog on exit if INI can't be written
	* all commands now fit into help dialog
	* some other fixes

2010-02-03	1.0.0.370
	+ script files now can be executed with params (supported %0 for whole script text and %1-%9 for parameters)
	+ improved <del command: may remove files or folders or both
	+ new condition commands <ifexist, <ifdef and <ifok
	+ new <for command allowing to execute script for all matched objects (files or folders or both)
	+ new <cd command for changing current path within script
	+ infinite script execution loop protection
	* wrong icon was displayed for inaccessible EXE and LNK
	* crash after entering text in TC request dialog
	* some other fixes that I can't remember :)

2010-02-02	1.0.0.340
	+ plugin now keeps content in %TEMP%\VirtualPanel.lst file by default
	+ inaccessible physical objects have special icons (you may specify another icons in configuration file)
	+ <edit command allows to change script or path
	* fixed crash on first start (with empty configuration file)
	* some small fixes

2010-01-31	1.0.0.322
	+ Unicode support! all functions use Unicode by default; ANSI functions replaced with stubs that call Unicode functions
	+ supports adding files from filelists in ANSI, UTF-8 and Unicode
	+ recursive and/or by mask filelist export
	* removed retrieving plugin file version on Windows 2000 because of strange crash during initialization

2010-01-24	1.0.0.200
	+ now files with read-only attribute may be removed (except scripts), also forced flag 'f' added to <del command
	* now files can be moved from virtual folder even w/o holding Shift key (confirmation is displayed)
	* fixed move file to normal panel (removed error checking if move function succeeds)
	* system search handle leak in FsFindNext function (one handle per file in virtual folder)

2009-12-24	1.0.0.194
	+ added language file support for translation (see sample in Language folder)
	* parameters parsing bug (e.g. for <add command)

2009-12-09	1.0.0.180
	+ added change case only renaming
	+ if INI with plugin's name exists near the plugin, this file is used as configuration file
	+ shows error message if configuration isn't saved (e.g. no write permission to INI)
	* null settings are not saved now when plugin loaded during installation
	* some minor fixes

2009-11-05	1.0.0.166
	* error opening script file mesage if file doesn't exist
	* error copying file within VP - file was moved instead

2009-10-26	1.0.0.162
	+ special delete physical files confirmation dialog
	+ <del command supports wildcards and keeps read-only files
	+ autoexecuted scripts - on load list and on list directory contents
	+ this Readme file :)
	* division by zero when copy empty files from VP
	* new FsExtractCustomIcon function extracts non-standard icons in background and causes TC to use less GDI objects

2009-10-18	1.0.0.121
	+ expanding of environment variables in commands and scripts except braced blocks
	+ import/export partial folder
	+ <put command allows to add physical files and entire filelists (e.g. playlists, full/relative paths) by mask
	+ <export command to export just physical names from virtual folder (e.g. to make playlist)
	+ <load command clears VP contents only if executed w/o second parameter
	+ you can't delete read-only script files (protection)
	+ added panels refreshing after VP operations
	* exception in <load command
	* set attributes for internal objects not always worked

2009-10-12	1.0.0.97
	+ log event groups
	+ correct initialization for older TC versions (w/o FsSetDefaultParams func support)
	+ support full internal paths starting from plugin name (for Ctrl+Shift+Enter)
	+ <add command supports nested blocks of commands in braces
	* log was always disabled at startup

2009-10-12	1.0.0.83
	+ batch script support
	+ if command parameter equals to "?", it is asked (useful for scripts)

2009-10-10	1.0.0.36
	* bug in filelist importing when line end was at the end of buffer

2009-10-10	1.0.0.xx
	! first public release
	+ virtual files/folders, links to physical files/folders
	+ internal commands allow to add/delete objects, import/export filelist and set default filelist
	+ correct links handling by TC
	+ correct copy/move operations between physical paths
	+ physical delete confirmation dialog if Shift is held

TCFS2 Addon for Total Commander
-------------------------------
(English section is below)

Утилита позволяет управлять режимами окна ТК:
+ разворачивать/восстанавливать окно
+ перемещать и изменять размер
+ скрывать и отображать заголовок
+ ставить окно "поверх других окон"
+ отключать любые отключаемые элементы окна ТК
+ изменять текущий путь в панелях
+ перемещать сепаратор файловых панелей
+ эмулировать нажатия клавиш
+ отменять последнее действие запуском команды отката
+ и многое другое...


0. Некоторые условные обозначения

В большинстве случаев в этом файле для обозначения символов и строк используется синтаксис языка Си: символы заключаются в апострофы '', а строки - в кавычки "".

Рабочей копией ТК считается последняя активная копия (запущенный процесс) на момент запуска TCFS2. Все команды работают только с ней.


1. Файл конфигурации

Все функции прописываются в конфигурационный файл и в любой момент могут быть изменены. Конфигурационный файл должен находиться в папке утилиты и иметь такое же имя файла, но расширение INI. В комплект поставки программы входит пример файла конфигурации с некоторыми командами (скопируйте его из папки RU в папку программы).

Конфигурационный файл состоит из следующих: Items (секции команд), Actions (секции действий) и Macros (секции макросов). Действия представляют собой последовательность команд для выполнения, команды в свою очередь содержат список вызовов функций, а также необязательные условия для проверки. Макросы - это константы и функции, к которым можно обращаться из параметров команд. Ниже будут рассмотрены все секции. Каждая строка может содержать комментарий, который указывается после знака ';'.

Чтобы использовать возможности отката действий, программе необходимы права доступа на запись к файлу конфигурации.



1.1. Поддерживаемые функции

Есть два типа функций, которые можно вызывать из команд - функции, выполняющие какое-то действие, и функции проверки какого-либо условия. Большинство параметров функций опциональны, можно просто поставить запятую без параметра, а если параметр последний - не ставить ничего).

Каждый числовой параметр может содержать целочисленное математическое выражение, построенное по правилам языка Си (поддерживаются операторы ( ) ! ~ % * / + - << >> < > <= >= != == & ^ | && || ?:). Во всех функциях, где это имеет смысл, в параметрах можно использовать переменную #, заменяемую на предыдущее значение данного параметра (размер окна, стиль и т.п.), а также вызывать макросы и функции проверки. Числовые операнды функций можно указывать в шестнадцатеричной системе, при этом нужно указывать перед числом знак '$'. Для указания отрицательного числа перед числом ставится знак '-'. Опциональные параметры указаны в квадратных скобках. После имени функции необходимо указывать скобки параметров, даже если параметров нет (как в языке Си).

Если функция принимает строковый параметр (не являющийся арифметическим выражением; например, функции send, tem, ini, set_ini), его необходимо заключать в косые кавычки `` (символ '`' - на клавише с символом '~'), если он содержит пробелы, запятые или скобки (пути к файлам лучше указывать в косых кавычках всегда, при этом сам символ '`' в пути к файлу недопустим). Простые строковые параметры, как правило, можно указывать без косых кавычек, если обратное не указано явно (например, в функции set_ini по наличию кавычек определяется тип параметра). Не будет ошибкой, если каждый строковый параметр будет заключен в косые кавычки. Сложные строки могут состоять из нескольких частей, как строковых, так и числовых (первая часть должна быть строковой, хотя бы пустой строкой ``; числовые параметры могут содержать любые выражения), тогда итоговая строка образуется конкатенацией всех строковых и вычисленных числовых частей.

	0, 1
		Возвращают соответствующую константу, могут использоваться для формирования безусловных условий;
	if(<condition>, [<true_expression>], [<false_expression>])
		Вычисляет и возвращает результат одного из выражений true_expression или false_expression в зависимости от истинности условия condition (если ненулевое, то true_expression). Возвращает 0, ничего не вычисляя, если соответствующее выражение для вычисления не указано. В отличие от оператора ?: вычисляет только одно из выходных выражений;
	loop(<expression>)
		Повторяет вычисление выражения, пока оно не станет равным 0. Возвращает количество выполненных итераций цикла. Переменная @ в выражении расширяется до номера итерации (начиная с 0);
	null(<something>)
		Возвращает 1, если параметр не является пустой строкой. Может быть использована, чтобы проверять, указан ли параметр команды или макроса с параметрами;
	eval(<expression>), test(<expression>)
		Возвращает результат вычисления выражения. Используется, например, для проверки сразу нескольких условий;
	style([<value>], [[<exvalue>])
		Проверяет установленные наборы флагов стилей, сравнивая с указанными. Если сравниваются и основные, и расширенные стили, результаты сравнения объединяются операцией И (истина только если результаты обоих сравнений истинны). Переменная # расширяется до текущих значений наборов флагов. Если переменная # в параметре не используется, то значение параметра сравнивается с ее значением автоматически;
	tcini(<section>, <key>, <value>|`<string_value>`, [<error_value>], [<flags>])
		Позволяет сравнить числовое или строковое значение ключа с указанным именем в указанной секции файла wincmd.ini (или значение error_value, если ключ не найден) с заданным значением. Строки сравниваются целиком, без учёта регистра. При сравнении числовых значений переменная # в выражении расширяется до текущего значения ключа/error_value. Если переменная # в параметре не используется, то результатом будет результат сравнения значения ключа/error_value с value, иначе - результат вычисления выражения (укажите просто # как value, чтобы вернуть значение ключа). Параметр flags по умолчанию равен $1 и строится из суммы значений: $1 - обрабатывать перенаправление секций файла wincmd.ini, $8000 - сравнивать строки с учётом регистра. Перенаправление обрабатывается так же, как в самом ТК, поддерживаются псевдо-переменные %$PERSONAL%, %$APPDATA% and %$LOCAL_APPDATA%, а также обычные переменные окружения;
	ini(`<inipath>`, <section>, <key>, <value>|`<string_value>`, [<error_value>], [<flags>])
		Работает так же, как и tcini, но с указанным в первом параметре INI-файлом;
	msg(<umsg>, <wparam>, <lparam>, [<async_mode>])
		Отправляет сообщение окну ТК и возвращает результат. Если async_mode>0, сообщение посылается через PostMessage, если async_mode<0, через SendMessage (как и при async_mode=0), но без ожидания результата;
	regmsg(<msg_name>)
		Возвращает номер зарегистрированного сообщения с таким именем (вызывает функцию RegisterWindowMessage);
	findwnd([`<class>`], [`<text>`], [<parent>], [<zindex>])
		Возвращает дескриптор окна с заданными текстом и/или именем класса, принадлежащего рабочей копии ТК. Если нужно найти окно с любым классом или текстом, не указывайте соответствующий параметр. Указание дескриптора родительского окна в параметре parent позволяет найти дочернее окно (при этом параметр zindex указывает порядковый номер окна, начиная с 0);
	tcd([`<left_path>`], [`<right_path>`], [S][T], [<async_mode>])
		Отправляет ТК команду смены директорий в панелях. Параметры left_path и right_path указывают пути к директориям левой и правой панели, третий параметр содержит флаги: S - считать левой панелью активную, а правой - неактивную, T - открыть директории в новых вкладках. Укажите async_mode равным 1, чтобы не ждать, пока ТК выполнит команду;
	tcm(<cm_index>, [<async_mode>])
		Отправляет ТК указание выполнить внутреннюю команду с указанным индексом. Индексы можно посмотреть в файле totalcmd.inc и в менеджере команд ТК. Параметр async_mode работает так же, как и у функции msg;
	tem(`<em_command_name> [<parameters>]`, [<async_mode>])
		Отправляет ТК указание выполнить пользовательскую команду с указанным именем. Для запуска команды с параметрами указывайте их через пробел после имени команды и заключайте всю строку в косые кавычки `` (ТК здесь не поддерживает Юникод). Укажите async_mode равным 1, чтобы не ждать, пока ТК выполнит команду;
	send([@]`<keystrokes>`, [<hwnd>])
		Посылает последовательность нажатий клавиш активному окну (например, диалогу) рабочей копии ТК или окну, дескриптор которого указан в параметре hwnd (укажите значение 0, чтобы отключить проверки активности окна). Чтобы отправить специальные клавиши, указывайте их обозначения в фигурных скобках: BACKSPACE, BKSP, BS, BREAK, CAPSLOCK, DEL, DELETE, DOWN, DQ (символ '"'), END, ENTER, ESC, HOME, INS, INSERT, LEFT, NUMLOCK, PGDN, PGUP, PRTSC, RIGHT, SCROLLLOCK, TAB, UP, F1-F12, ADD (Num +), SUBTRACT (Num -), MULTIPLY (Num *), DIVIDE (Num /), VK_xxx (виртуальная клавиша с кодом xxx, например, VK_91 - клавиша Win). Для многократного нажатия укажите в фигурных скобках саму клавишу и число её повторений через пробел. Перед очередной клавишей (или последовательностью клавиш, взятой в круглые скобки) можно указать один или несколько модификаторов: '+' - с зажатым Shift, '^' - с зажатым Ctrl, '%' - с зажатым Alt, '~' - посылать как символ, а не как клавишу (с сохранением регистра и раскладки). Чтобы послать служебную клавишу ('+', '{', '(' и т.п.), возьмите её в фигурные скобки. Префикс '@' включает режим передачи точных строк, в котором все клавиши (включая служебные) посылаются как символы;
	sendmsg(<hwnd>, <umsg>, <wparam>, <lparam>, [<async_mode>])
		Отправляет оконное сообщение окну с дескриптором hwnd. В остальном идентична функции msg;
	varcnt()
		Возвращает количество внутренних переменных (переменные живут до завершения TCFS2);
	varget(<n>)
		Возвращает значение внутренней переменной с индексом n;
	varset(<n>, <x>)
		Записывает x во внутреннюю переменную с индексом n;

	show(<state>)
		Показывает/скрывает окно, вызывая API-функцию ShowWindow с параметром state, допустимые значения можно посмотреть в справке по этой функции;
	move([<x>], [<y>], [<cx>], [<cy>], [<topmost>])
		Перемещает/изменяет размер окна. Первые 4 параметра позволяют задать позицию и размер окна. Если параметр опущен, соответствующее значение не изменяется. Переменная # в этих параметрах расширяется до текущего значения величины, а дополнительная переменная @ - до ширины или высоты экрана. Параметр topmost позволяет включать/выключать режим "поверх других окон" (если не указан, режим не изменяется);
	redraw()
		Вызывает полную перерисовку окна ТК. Например, после переключения заголовка или после блокировки перерисовки окна;
	run_item(<item_name>, [<params>])
		Выполняет команду с указанным именем, затем продолжает выполнять текущую команду. Если команда требует параметры, укажите их, разделяя запятыми;
	run_action(<action_name>)
		Выполняет действие с указанным именем, затем продолжает выполнять текущую команду;
	set_style([<value>], [<exvalue>])
		Изменяет основные и расширенные стили окна. Стили предоставлены набором флагов (перечень флагов - в справке по API-функции SetWindowLong и её параметрам GWL_STYLE и GWL_EXSTYLE). Переменная # расширяется до текущих значений наборов флагов;
	set_tcini(<section>, <key>, [<value>]|`<string_value>`, [<error_value>], [<flags>])
		Позволяет задать/модифицировать ключи wincmd.ini. Если параметр value заключен в косые кавычки ``, он записывается в виде строки, иначе value рассматривается как числовое выражение. Переменная # расширяется до текущего значения ключа (или до значения, указанного в параметре error_value, если ключ не найден). Если параметр value не задан, строка удаляется из INI;
	set_ini(`<inipath>`, <section>, <key>, [<value>]|`<string_value>`, [<error_value>])
		Работает так же, как и set_tcini, но с указанным в первом параметре INI-файлом;
	save_undo(<undo_name>)
		Сохраняет текущую строку отката в действие с указанным именем;
	delay(<msec>)
		Приостанавливает выполнение команды на заданный интервал времени.



1.2. Секция команд

В секции [Items] прописываются команды, содержащие один или несколько вызовов функций для выполнения (разделенные пробелами), необязательное условие необходимости выполнения функции (или выражение из нескольких условий, указанное в параметрах функции test), а также необязательные строку отката. Строка отката дописывается к формируемому действию отката, если условие отката истинно (если оно не указано, проверяется, стало ли ложным условие выполнения функции - если указать 1 как условие отката, откат будет дописываться всегда). Каждая строка может содержать несколько таких команд, разделенных символом '|' - в этом случае слева направо будут проверяться все условия, пока не будет найдено первое истинное - соответствующая команда будет выполнена, дальнейшие команды строки будут проигнорированы.

Id=apply_command1(...) [apply_command2(...) ...] [, check_command(...) [, undo_ids [, undochk_command(...)]]] [| apply_commandN(...) ...] ; Описание

При вызове команды можно сразу за её именем в скобках указать до 9 параметров команды. Эти параметры будут подставлены вместо подстрок #1, #2, ..., #9 во всей строке команды до начала выполнения команды. Если параметр не передан, он будет раскрыт в пустую строку. Рекомендуется заключать символы #1 и т.д. в скобки, чтобы избежать ошибок при подстановке выражений в качестве параметров.


Рассмотрим несколько примеров, поясняющих, как выполняются команды:

Пример команды для выключения панели инструментов ТК:
tb0=tcm(2901), test(hasButtonBar), tb1

Здесь вызывается макрос hasButtonBar, проверяющий, равен ли 1 ключ ButtonBar секции [Layout] файла wincmd.ini (если ключа нет, возвращается значение ошибки, равное 1, так как значение этого ключа в ТК по умолчанию равно 1). Если условие истинно, выполняется команда tcm, отправляющая ТК команду cm_VisButtonbar (2901). Затем условие проверяется вновь (после паузы, задаваемой параметром /d) и, если оно стало ложным, в откат дописывается команда включения панели инструментов tb1.

Пример команды для восстановления окна из развернутого состояния с безусловным добавлением строки отката:
m0p=show(9), test(isMaximized), m1, 1

А здесь проверяется наличие стиля развернутости окна. Функция test вычисляет выражение, вызывая макрос isMaximized, который проверяет присутствие флага WS_MAXIMIZE. Если флаг отсутствует, обработка команды завершается. Если флаг стоит, вызывается функция show(9), а затем команда m1 безусловно дописывается к строке отката. Если не указывать последний параметр 1, то откат будет дописан только если условие test(isMaximized) в результате выполнения команды станет ложным (то есть, окно восстановится из развернутого состояния).

Пример команды, которая проверяет присутствие нескольких элементов окна ТК (кнопки дисков, панель выбора дисков, командная строка), если хотя бы один отключен, все включает, иначе все выключает:
multi_switch=run_action(multi_enable), tcini(Layout, DriveBar1, 0) | run_action(multi_enable), tcini(Layout, DriveCombo, 0) | run_action(multi_enable), tcini(Layout, CmdLine, 0) | run_action(multi_disable)

Начинается команда проверкой условия tcini(Layout, DriveBar1, 0). Если оно истинно (то есть, панель дисков отключена), вызывается действие multi_enable для включения элементов. Иначе проверяется наличие второго элемента, затем третьего (таким способом можно проверить любое число элементов). Если все элементы включены, будет выполнена безусловная команда run_action(multi_disable), которая вызовет действие multi_disable для отключения элементов. Подразумевается, что в секции действий определены действия multi_enable, состоящее из команд db1 dc1 cl1, и multi_disable, состоящее из команд db0 dc0 cl0.

Пример той же команды, которая проверяет присутствие нескольких элементов окна ТК, но с использованием макросов и функции test:
multi_switch=run_action(multi_disable), test(hasDriveBar && hasDriveCombo && hasCmdLine) | run_action(multi_enable)

Вначале вычисляется параметр функции test, при этом вызываются все 3 макроса и выполняется операция И. Функция test возвращает истину, только если все три макроса вернули истину, т.е. все три проверяемых элемента (панель дисков, панель выбора дисков и командная строка) включены. В этом случае вызывается действие multi_disable, в противном случае выполняется действие multi_enable (уже безусловно).

Пример команды, растягивающей окно на весь экран, если это еще не сделано, или же уменьшающей размер окна до среднего, помещая его в середину экрана:
switch_sp=move(# ? 0 : @*7/64, # ? 0 : @*7/64, @-# ? @ : @*25/32, cyWorkArea-# ? cyWorkArea : @*25/32), , switch_sp

Рассмотрим, как это работает, на примере позиции окна по горизонтали. При вычислении выражения # ? 0 : @*7/64 проверяется, равно ли нулю выражение перед знаком ?, и если выражение не равно нулю (т.е. истинно), возвращается первое значение после знака ? (т.е. 0), в противном случае возвращается значение после знака : (т.е. @*7/64). В результате при повторных вызовах команды позиция окна будет переключаться между нулем и 7/64 от размера экрана. Вычисление остальных параметров выполняется таким же образом. Также при вычислении высоты окна вызывается макрос cyWorkArea, возвращающий высоту рабочей области экрана без панели задач.

Пример команды, расширяющей ширину активной панели до 95% путем перемещения разделителя панелей, если разделитель стоит по центру, или сбрасывающей позицию на 50%:
sp_sw_50_95=run_item(sp_set_active, sepPos == 50 ? 95 : 50)

Вызывается макрос sepPos, возвращающий текущую позицию разделителя панелей. Далее вызывается команда sp_set_active со значением 95, если текущая позиция равна 50, или же со значением 50 в противном случае. В свою очередь, команда sp_set_active (входит в базовый комплект), вызванная с параметром 95, устанавливает разделитель в позицию 95%, если активна левая панель, или же в позицию (100-95)%, если активна правая. Для определения активной панели вызывается макрос L_isActive, возвращающий 1, если активна левая панель. Данная команда будет работать только при активном модуле TCFS2Tools, который позволяет определить активную панель и узнать/установить позицию разделителя.

Пример команды, выполняющей разные действия в зависимости от того, зажата ли клавиша Shift или правая кнопка мыши:
check_shift=run_action(action_shift_pressed), test(pressedShift || pressedRButton) | run_action(action_shift_not_pressed)

Функция test вызывает макросы pressedShift и pressedRButton. Если хоть один из них вернёт истину, test вернёт истину, и будет выполнено действие action_shift_pressed, в противном случае будет выполнено действие action_shift_not_pressed. Для определения состояния клавиш вызывается команда модуля TCFS2Tools.

Пример команды, включающей определенную панель инструментов по номеру:
set_bar=if(#1 == 1, tem(em_bar1)) if(#1 == 2, tem(em_bar2)) if(#1 > 0, set_tcini(Layout, ButtonBar, 1), run_item(tb0)) set_tcini(TCFS2, Bar, #1)

Команда может быть использована из других команд, она запоминает номер установленной панели в параметр Bar секции TCFS2 файла wincmd.ini. Вы можете добавить больше вызовов функции if, если используете большее количество панелей. Пользовательские команды em_bar1, em_bar2 и т.д. должны быть определены в ТК. При нулевом параметре команда скрывает панель, при ненулевом - дополнительно записывает в wincmd.ini значение ButtonBar=1 (ТК не делает этого при вызове команды OPENBAR).

Пример команды, которая включает вторую панель инструментов на 10 секунд или возвращает обратно первую:
quick_bar=set_tcini(TCFS2, #0, 0) run_item(set_bar, 1), test(tcini(TCFS2, Bar, #)!=1) | set_tcini(TCFS2, #0, @sid) run_item(set_bar, 2) delay(10000) if(tcini(TCFS2, #0, # == @sid), run_item(set_bar, 1))

Сначала проверяется номер текущей панели. Если активна основная панель, команда записывает ID сеанса в параметр с именем команды в секции TCFS2 файла wincmd.ini и включает вторую панель инструментов. После этого команда ждет 10 секунд, по истечении которых возвращает первую панель, только если сохранённый ID сеанса не изменился. Если команда запускается при активной второй панели, она сбрасывает ID сеанса и возвращает первую панель без ожидания. Идентификатор сеанса здесь позволяет избежать быстрого переключения панелей, если команда вызывается чаще, чем истекает время ожидания (когда третья копия команды запускается, пока первая всё еще в стадии ожидания).

Пример команды для переключения в полноэкранный режим и обратно:
fs2=if(hasCaption, locktc(1) + run_action(fs) + locktc(0) + show(3) + save_undo(fs_undo), show(9) + locktc(1) + run_action(fs_undo) + locktc(0)) run_item(update)

Здесь будет вызван макрос hasCaption для проверки наличия заголовка окна. Если заголовок есть, будут вызваны функции run_action(fs) и save_undo(fs_undo) для переключения в полноэкранный режим (действие fs может быть любым, но для корректной работы данной команды оно должно скрывать заголовок окна) и записи в действие fs_undo команд отката, и затем окно будет развёрнуто. Если же заголовок окна отсутствует (то есть, полноэкранный режим включен), первая команда выполнена не будет, поэтому будет вызвана функция run_action(fs_undo) для выполнения действия отката и окно будет восстановлено. На время выполнения команд действий fs2 или fs_undo будет отключена перерисовка окна с помощью макроса locktc (не блокируйте перерисовку при восстановлении окна из развернутого состояния, это выглядит жутко). Также по завершении команды будет выполнена полная перерисовка окна.

Пример команды, скрывающей панель инструментов, если в BAR-файле %COMMANDER_PATH%\Default.bar более 30 кнопок:
bbhide_if30=if(ini(`%COMMANDER_PATH%\Default.bar`, Buttonbar, Buttoncount, #>30), run_item(tb0))

Функция ini читает значение параметра Buttoncount из BAR-файла и проверяет, больше ли оно 30. Если это так, вызывается команда tb0 для сокрытия панели инструментов.

Пример команды, запускающей инструмент переименования и задающей некоторый шаблон имени, а также опции поиска и замены:
test_hello=send(`^m~(Прощай, Мир! ;{)}){tab}{del}{tab}~(Прощай|;){tab}~(Привет|:){tab 5}{home}`)

Команда посылает нажатие Ctrl+M для запуска инструмента переименования, затем перемещается между полями и заполняет их текстом.

Пример команды, создающей или изменяющей шаблон подсказки с заданным номером, использующей сложные строки:
set_hint_fields=set_tcini(HintsCustomField, `` #1 `exts`, #2) set_tcini(HintsCustomField, `` #1 `fields`, #3)

Команда принимает три параметра: номер шаблона, маску файлов и формат подсказки. Номер шаблона используется для формирования имен ключей, в которые будут записаны значения. Например, для номера 3 строки будут записаны в ключи 3exts и 3fields.



1.3. Секция действий

Секция [Actions] конфигурационного файла содержит действия - последовательности команд для выполнения, разделенные пробелами. Имена действий произвольны, но есть одно встроенное действие с именем Undo - в него при каждом запуске программы будут записываться команды для отката изменений, внесенных в результате работы программы (если не был указан параметр /u-), поэтому задавать его вручную не рекомендуется.



1.4. Секция макросов

Секция [Macros] содержит определения констант и функций, которые можно вызывать при вычислении параметров других функций. Содержимое макросов не подставляется в исходное выражение, а вычисляется при вызове. Каждая строка содержит имя макроса, знак равенства и выражение, которое будет вычислено при обращении к макросу. Правила построения выражений такие же, как и у параметров функций (описаны в п.п. 1.1 данного файла). Как и команды, макросы поддерживают до 9 параметров, которые будут подставлены вместо подстрок #1, #2, ..., #9 в строке выражения перед его вычислением.



1.5 Псевдо-макросы

При вызове функций и макросов можно использовать некоторые предопределенные макросы. Их имена начинаются с символа '@'.

	@sid
		Возвращает идентификатор сеанса. Это значение уникально для каждой запущенной копии TCFS2.



2. Командная строка

Командная строка программы позволяет выполнять как действия, так и одиночные команды, определенные в файле TCFS2.ini, причем любое число за один запуск. Синтаксис:

TCFS2[.exe] [<parameters>] [<actions>] [/ei <commands>] [/ea <actions>] ...

Параметры:
	/d=<msec>
		Задать время в миллисекундах на ожидание между выполнением команды и проверкой условия отката (по умолчанию 50 мс);
	/ea, /ei, /ef
		Указать, чем считать дальнейшие идентификаторы в командной строке - действиями, командами или напрямую содержимым команды;
	/i="<path>"
		Задать конкретный путь к файлу wincmd.ini (по умолчанию читается переменная COMMANDER_INI);
	/u[-]
		Включить/выключить запись действия отката Undo по окончании работы программы;
	/uc
		Очистить текущую строку отката, сформированную с начала работы программы;
	/us[="<action>"]
		Немедленно сохранить текущую строку отката в действие с указанным именем (или в действие Undo, если имя не указано);
	/w[-]
		Включиь/выключить вывод сообщений об ошибках.

Каждый вызов команды, содержащий пробелы, должен быть заключен в кавычки. Также в кавычки следует заключать прямое содержимое команд (после параметра /ef). Не заключайте в общие кавычки более одного вызова действия или команды (после параметров /ea и /ei). Смотрите примеры ниже.


Примеры запуска:

Пример запуска действия undo:
TCFS2 undo

Пример запуска команды fs2 с отключением записи действия Undo (команда работает со своим действием отката):
TCFS2 /u- /ei fs2

Пример запуска действия title_switch и команд m2 и t2 с отключением записи действия Undo, но записью строки отката в действие test_undo:
TCFS2 /u- title_switch /ei m2 t2 /us=test_undo

Пример увеличения позиции разделителя файловых панелей на 10% (необходим TCFS2Tools; кавычки обязательны, т.к. есть пробелы в параметре):
TCFS2 /ei "set_separator(sepPos + 10)"

Пример установки ширины активной панели на 80% с использованием команды с параметром (необходим TCFS2Tools; кавычки необязательны):
TCFS2 /ei "sp_set_active(80)"

Пример переключения между текущим режимом и подробным режимом активной панели (можно указать индекс любого режима из cm_Src*):
TCFS2 /u- /ei switch_viewmode_S(302)

Пример прямого вызова содержимого команды (кавычки вокруг выражения обязательны):
TCFS2 /ef "run_action(fs) save_undo(fs_undo), style(# & $00C00000) | run_action(fs_undo)"

Пример смены текущего пути на D:\ (должна быть определена пользовательская команда em_CD с командой CD и параметром %A):
TCFS2 /ef "tem(`em_CD D:\`)"

Пример перехода в директорию D:\ в неактивной панели:
TCFS2 /ef "tcd(, `D:\`, s)"



3. TCFS2Tools

TCFS2Tools - модуль, предоставляющий расширенные возможности, например, определение активной панели, перемещение разделителя панелей и т.п. Он не входит в стандартный комплект и должен быть загружен и установлен отдельно (страница загрузки здесь: http://wincmd.ru/plugring/tcfs2tools.html).


Обсуждение на официальном русскоязычном форуме: http://forum.wincmd.ru/viewtopic.php?t=13332



TCFS2 Addon for Total Commander
-------------------------------
(English section)

Tool allows controlling TC window modes:
+ maximize/restore window
+ move/resize window
+ hide/show window title
+ enable topmost window mode
+ hide/show any TC interface item
+ change dirs in panels
+ move file panels separator
+ send keypresses
+ undo last action using backup command
+ etc...


0. Some notation conventions

In most places of this file C language syntax is used to indicate characters and strings: characters are enclosed with apostrophes '' and strings are enclosed with double quotes "".

Working TC instance is the TC instance most recently used when TCFS2 is started. All commands work with that instance.

1. Configuration file

All functions are in configuration file and may be changed at any moment. Configuration file must be placed near application and have same name and extension INI. Sample configuration files with some commands are shipped with program (just copy it from EN folder to program's folder).

Configuration file contains following sections: Items (for commands), Actions (for actions) and Macros (for macroses). Each action is a sequence of comamnds to execute, commands contain list of function calls and optional condition checks. Both sections will be described below. Macroses are constants and functions that may be called from parameters of other functions. Each configuration file line may contain a comment that begins with ';' sign.

To use undo feature program must have write access to configuration file.



1.1. Supported functions

There are two groups of functions - functions that do some work and ones that check some condition. Most of function parameters are optional - you may just leave a placeholder (just comma without parameter value) and skip last parameters.

Every numeric parameter can contain integer mathematical expression that corresponding to C language syntax (supported operators are ( ) ! ~ % * / + - << >> < > <= >= != == & ^ | && || ?:). You can also use # variable that will be expanded to actual parameter value in all functions where such thing makes sence. Numeric parameters may be specified in hexadecimal notation, in this case place '$' sign before number. Negative numbers should be started with '-' sign. Optional parameters are enclosed in square brackets. You must specify parameter braces after function name even if there is no parameters (like in C language).

When function accepts string parameter value (i.e. not an numeric expression; e.g. functions send, tem, ini or set_ini), it must be enclosed with grave accents `` (character '`' is on key with '~') when it contains spaces, commas or brackets (file paths must be enclosed with grave accents always, and may not contain '`' char at all). Simple string values may be passed w/o grave quotes if it is not mentioned that it must be quoted (e.g. function set_ini checks if parameter is quoted to determine its type). It is better to quote all string parameters with grave accents. Complex strings may contain multiple parts, both string and numeric ones (first one must be a string, e.g. empty string ``; numeric parts may contain any expressions). Resulting string in such case is a concatenation of all string parts and calculated numeric parts.

	0, 1
		Returns corresponding constant, may be used in unconditional checks;
	if(<condition>, [<true_expression>], [<false_expression>])
		Calculates and returns true_expression or false_expression result depending on condition result (true_expression is calculated for nonzero condition). Returns 0 if corresponding expression is not specified. In contrast to ?: operator if function calculates only one of two output expressions;
	loop(<expression>)
		Repeats calculation of expression until it returns zero. Returns number of executed iterations. Variable @ is expanded to iteration number (zero based);
	null(<something>)
		Returns 1 if parameter is not an empty string. E.g. may be used to check if command/macro parameter is specified;
	eval(<expression>), test(<expression>)
		Returns expression result. May be used e.g. for checking some conditions at once;
	style([<value>], [<exvalue>])
		Checks window styles by comparing them with specified values. Compares results are combined by AND operation if both values are specified (i.e. true only when both comparisons are true). Variable # is expanded to actual set of flags. If # variable is not used parameter value is compared to its value automatically;
	tcini(<section>, <key>, <value>|`<string_value>`, [<error_value>], [<flags>])
		Compares specified string or numeric key in specified section of wincmd.ini (or value specified in error_value parameter if key is not found) with specified value or gets key value. Strings comparison is case insensitive. For numeric keys, variable # in expression is expanded to actual key value/error_value. If # variable is not used, return value is compare result of key value/error_value and parameter value, otherwise function returns expression result (specify just # as value parameter to get key value). Last parameter flags ($1 by default) is a sum of some values: $1 - use redirection of sections in wincmd.ini, $8000 - use case sensitive string comparison. Redirection works in same way as in TC, pseudo-variables %$PERSONAL%, %$APPDATA% and %$LOCAL_APPDATA% and environment variables are supported;
	ini(`<inipath>`, <section>, <key>, <value>|`<string_value>`, [<error_value>], [<flags>])
		Works exactly as tcini but with specified INI instead of wincmd.ini;
	msg(<umsg>, <wparam>, <lparam>, [<async_mode>])
		Sends a message to TC window. If async_mode>0, message will be sent using PostMessage function, if async_mode<0, it will be sent using SendMessage (as if async_mode=0), but w/o waiting for result;
	regmsg(<msg_name>)
		Retrieves message number associated with given name (via RegisterWindowMessage function);
	regmsg(<msg_name>)
		Returns registered message number approriate to given name (calls RegisterWindowMessage function);
	findwnd([`<class>`], [`<text>`], [<parent>], [<zindex>])
		Retrieves a handle to the window with specified class name and window name belonging to working TC instance. If you need to find a window with any class or text, just omit corresponding parameter. You can also specify parent window handle if you want to find some child window (zindex paremeter specifies zero based window Z-order index);
	tcd([`<left_path>`], [`<right_path>`], [S][T], [<async_mode>])
		Sends change dir command to TC. Parameters left_path and and right_path specify paths for left and right panels, thirs parameter contains flags: S - interpret the passed dirs as source/target instead of left/right, T - open passed dir(s) in new tab(s).  You can set async_mode to 1 if you don't want to wait until TC completes the command;
	tcm(<cm_index>, [<async_mode>])
		Sends a message to execute specified TC internal command with specified index. Command indexes you may see in totalcmd.inc file and in TC command browser. Parameter async_mode works in the same way as for msg function;
	tem(`<em_command_name> [<parameters>]`, [<async_mode>])
		Sends a message to execute TC user command with specified name. You can pass parameters to that command, just specify them after command's name and a space and enclose entire line with grave accents `` (TC doesn't support Unicode here). You should set async_mode to 1 if you don't want to wait until TC completes the command;
	send([@]`<keystrokes>`, [<hwnd>])
		Sends the sequence of keystrokes to active window (e.g. dialog) of working TC instance, or to the window whose handle is specified in hwnd parameter (you can pass value 0 to disable window activity checks). You can send special keys by enclosing their names with curly braces: BACKSPACE, BKSP, BS, BREAK, CAPSLOCK, DEL, DELETE, DOWN, DQ ('"' character), END, ENTER, ESC, HOME, INS, INSERT, LEFT, NUMLOCK, PGDN, PGUP, PRTSC, RIGHT, SCROLLLOCK, TAB, UP, F1-F12, ADD (Num +), SUBTRACT (Num -), MULTIPLY (Num *), DIVIDE (Num /), VK_xxx (a virtual key with code xxx, e.g. VK_91 means Win key). In order to repeat some key use curly braces with that key and repeat number after a space. Each keystroke (or a sequence of keystrokes enclosed with round brackets) may have a set of special prefixes: '+' - with Shift, '^' - with Ctrl, '%' - with Alt, '~' - send as characters instead of keystrokes (keeps character case and keyboard layout). In order to send service key ('+', '{', '(' etc) enclose it with curly braces. Prefix '@' enables verbatim mode to send all keystrokes (including service keys) as characters;
	sendmsg(<hwnd>, <umsg>, <wparam>, <lparam>, [<async_mode>])
		Works like msg function but sends this message to window with given handle.
	varcnt()
		Gets number of internal variables (variables live until TCFS2 closes);
	varget(<n>)
		Gets value of internal variable with index n;
	varset(<n>, <x>)
		Stores x to internal variable with index n;

	show(<state>)
		Shows/hides window by calling ShowWindow API function with passed state parameter; you can read about available parameters in ShowWindow function's manual;
	move([<x>], [<y>], [<cx>], [<cy>], [<topmost>])
		Resizes/moves window. First 4 parameters allow setting up window position and size. If parameter is omitted its value preserved. Variable # is expanded to actual parameter value, also additional variable @ is expanded to window width or height. Parameter topmost allows turning topmost window mode on or off (if parameter is missed, mode is not changed);
	redraw()
		Causes full redraw of TC window. E.g. after switching caption or after blocking window redraw;
	run_item(<item_name>, [<params>])
		Executes command (item) with specified name, then return to current command. You may specify any number of parameters divided by comma if command accepts them;
	run_action(<action_name>)
		Executes action with specified name, then return to current command;
	set_style([<value>], [<exvalue>])
		Changes normal and extended window styles. Each value is a set of flags (read more about style flags in manual on SetWindowLong function and its parameters GWL_STYLE and GWL_EXSTYLE). Variable # is expanded to actual set of flags;
	set_tcini(<section>, <key>, [<value>]|`<string_value>`, [<error_value>], [<flags>])
		Sets/modifies wincmd.ini keys. If value parameter is enclosed with grave accents ``, it will be written directly to INI as string, in the other case value should be a numeric expression. Variable # is expanded to actual key value (or to value specified in error_value parameter if key is not found). If value is not specified at all, key will be removed from INI;
	set_ini(`<inipath>`, <section>, <key>, [<value>]|`<string_value>`, [<error_value>])
		Works exactly as set_tcini but with specified INI instead of wincmd.ini;
	save_undo(<undo_name>)
		Saves current undo string to action with specified name;
	delay(<msec>)
		Pauses execution on specified time interval;



1.2. Commands section

Section [Items] contains commands which consist of one or more function calls (divided by spaces), optional execute condition (or expression with some conditions in parameters of test function) and optional undo string. Undo string is appended to undo action if undo condition is true (if undo condition is not specified, program checks if command condition become false after execution of command - you may specify 1 as undo condition to make undo string appending unconditional). Every item line can contain any number of described commands divided with '|' character - this allows checking condition of another function if previous one was already false. If a command with true condition is found, its function is executed and line processing is finished.

Id=apply_command1(...) [apply_command2(...) ...] [, check_command(...) [, undo_ids [, undochk_command(...)]]] [| apply_commandN(...) ...] ; Description

When calling a command, you may specify up to 9 parameters in brackets if command expectes them. Theese parameters will be placed instead of substrings #1, #2, ..., #9 within entire command before its execution. Missed parameters will be expanded to empty string. It is recommended to enclose #1 etc. symbols within brackets to avoid errors when you specify expressions as parameters.


Let's look onto some samples to examine how commands are executed:

Example of command to turn TC button bar off:
tb0=tcm(2901), test(hasButtonBar), tb1

Program calls macro hasButtonBar that checks if ButtonBar key in [Layout] section of wincmd.ini equals to 1 (if key is absent, error value 1 returned since 1 is default value for this key). If condition is true, tcm command is executed that sends to TC cm_VisButtonbar (2901) command. After sending command program makes a short pause (you can set delay using /d command line parameter) and checks same condition again. If condition is false after executing command, tb1 undo command is appended to undo string.

Example of command to restore window from maximized state with unconditional undo item appending:
m0p=show(9), test(isMaximized), m1, 1

Here maximized style is being checked. Test function calls macro isMaximized that checks flag WS_MAXIMIZE. If flag is not set, command does nothing. But if flag is set, function show(9) is called and then item m1 is appended to undo string. If last parameter 1 is not specified, program checks if flag is set after function call and undo item will be appended only if test(isMaximized) condition becomes false (i.e. window is restored).

Example of command that checks presence of some TC window controls (drive buttons, drive combo bar, command line) and enables them if at least one is disabled else disables them all:
multi_switch=run_action(multi_enable), tcini(Layout, DriveBar1, 0) | run_action(multi_enable), tcini(Layout, DriveCombo, 0) | run_action(multi_enable), tcini(Layout, CmdLine, 0) | run_action(multi_disable)

First command checks condition tcini(Layout, DriveBar1, 0). If true (i.e. drive buttons are disabled) multi_enable action is called to enable all controls and line execution is stopped. If drive buttons are enabled second command's condition is checks, then third etc (you can check any number of elements using such method). If all elements are enabled, run_action function calls multi_disable action to enable them all. Note that in actions sections you should have multi_enable action with comamnds db1 dc1 cl1 and multi_disable action with commands db0 dc0 cl0 to use this sample.

Example of same command that checks presence of three TC window controls written using test function:
multi_switch=run_action(multi_disable), test(hasDriveBar && hasDriveCombo && hasCmdLine) | run_action(multi_enable)

Here parameter of test function is calculated. Three macros are called and then OR operation performed. Result is true only when all three macroses return true - i.e. all three window elements are enabled drive buttons, drive combo bar, command line). If so, multi_disable action is called, or multi_enable otherwise (w/o condition).

Example of command that expands window to screen size if it is not expanded yet or shrinks it to medium size and centers otherwise:
switch_sp=move(# ? 0 : @*7/64, # ? 0 : @*7/64, @-# ? @ : @*25/32, cyWorkArea-# ? cyWorkArea : @*25/32), , switch_sp

Let's look how first parameter (window X position) is calculated. When calculating expression # ? 0 : @*7/64 program checks if expression before ? mark is equals to zero, and if expression is non-zero (i.e. it is true) value after ? (i.e. 0) is returned, else value after : (i.e. @*7/64) is returned. So if you call command more than once, it will switch window position between 0 and 7/64 of screen size. Other parameters are calculated in same way. When window height is calculated, macro cyWorkArea is called to get work desktop area height (w/o taskbar).

Example of command that expand active panel width up to 95% by moving separator if its position is 50%, or reset it back to 50% otherwise.
sp_sw_50_95=run_item(sp_set_active, sepPos == 50 ? 95 : 50)

Macro sepPos is called to get current separator position. Then sp_set_active command is called with parameter depending on current separator position: 95 if current position is 50 or 50 otherwise. When command sp_set_active (this command is included into default configuration file) is called with parameter 95, it sets separator position to 95% if left TC panel is active or to (100-95)% otherwise. Macro L_isActive is used to get active panel. Please note that this command will work only if TCFS2Tools module is active (it allows getting/setting separator position and get active panel).

Example of command that executes different actions depending on Shift or right mouse button state:
check_shift=run_action(action_shift_pressed), test(pressedShift || pressedRButton) | run_action(action_shift_not_pressed)

Function test calls macroses pressedShift and pressedRButton. If one of them returns true, test returns true, and action_shift_pressed action is executed. If none of keys pressed, test returns false and action_shift_not_pressed action is executed. Command uses TCFS2Tools for determining key states.

Example of command that switches to buttonbar via its number:
set_bar=if(#1 == 1, tem(em_bar1)) if(#1 == 2, tem(em_bar2)) if(#1 > 0, set_tcini(Layout, ButtonBar, 1), run_item(tb0)) set_tcini(TCFS2, Bar, #1)

This command may be used from other commands, it saves current buttonbar number into Bar parameter in TCFS2 section of wincmd.ini. If you need more buttonbars you may add corresponding if function calls. Of course, user-commands em_bar1, em_bar2 etc. should be defined in TC. In case of zero parameter command hides buttonbar, otherwise it additionally sets ButtonBar=1 in wincmd.ini (TC doesn't do this when you call OPENBAR command).

Example of command that switches to second buttonbar for 10 seconds or back to first one:
quick_bar=set_tcini(TCFS2, #0, 0) run_item(set_bar, 1), test(tcini(TCFS2, Bar, #)!=1) | set_tcini(TCFS2, #0, @sid) run_item(set_bar, 2) delay(10000) if(tcini(TCFS2, #0, # == @sid), run_item(set_bar, 1))

First of all command checks current buttonbar index. If first (main) bar is active, command writes session ID to wincmd.ini and switches to second bar. Then it waits for 10 seconds. After that it returns main bar if saved session ID hasn't changed. If second bar is active when command is called, it resets session ID and switches to main bar w/o delay. Session ID is used here to prevent fast bar switching if you call command frequently (when first session is still waiting when you start third one).

Example of command to switch full-screen mode:
fs2=if(hasCaption, locktc(1) + run_action(fs) + locktc(0) + show(3) + save_undo(fs_undo), show(9) + locktc(1) + run_action(fs_undo) + locktc(0)) run_item(update)

Command checks if window title is visible (by calling hasCaption macro). If it is so, run_action(fs) and save_undo(fs_undo) functions are executed to enable full-screen mode (you may modify fs action as you wish but it should hide window title else this command will not work properly) and to save undo string to action fs_undo, also window is maximized. If title is disabled, first command is skipped and second one with run_action(fs_undo) function call is executed, and window is restored. Macro locktc disables TC window redraw during fs2 or fs_undo actions execution (don't lock window before restoring it from maximized state, it looks ugly). At the end of command TC window redraw is performed.

Example of command that hides buttonbar if %COMMANDER_PATH%\Default.bar file contains more than 30 buttons:

bbhide_if30=if(ini(`%COMMANDER_PATH%\Default.bar`, Buttonbar, Buttoncount, #>30), run_item(tb0))

Function ini reads parameter Buttoncount from BAR file and compares with 30. If it is greater than 30, tb0 command is called to hide buttonbar.

Example of command that starts multi-rename tool and sets some fields:

test_hello=send(`^m~(Goodbye, World! ;{)}){tab}{del}{tab}~(Goodbye|;){tab}~(Hello|:){tab 5}{home}`)

Send function sends Ctrl+M and then jumps between text fields and fills them with some text.

Example of command to set custom hints template with specific number in INI using complex strings:
set_hint_fields=set_tcini(HintsCustomField, `` #1 `exts`, #2) set_tcini(HintsCustomField, `` #1 `fields`, #3)

Command accepts three parameters: template number, file mask and hint format. Template number is used to form names of keys where values are stored. E.g. for number 3 strings will be stored in keys 3exts and 3fields.



1.3. Actions section

Section [Actions] of configuration file contains actions - sequences of items to be executed divided by spaces. Actions may have any names however one predefined action with name Undo exists - it will collect undo commands to revert changes that was made during last program call (if command line parameter /u- was not specified) so it is not recommended to use it manually.



1.4. Macros section

Section [Macros] contains definitions for constants and functions that may be called from expressions passed to other functions. Macroses are calculated on each call, their contents is not pasted into caller expressions. Each section line contains macro name, equals sign and expression that will be calculated on each macro call. Expression uses same rules as functions parameters (refer to paragraph 1.1 of this Readme). Macroses like commands support up to 9 parameters that are placed insted of substrings #1, #2, ..., #9 before expression calculation.



1.5 Pseudo-macroses

There are some predefined macroses that may be used in parameters of functions and macroses. Theese macroses have names that start with '@' character.

	@sid
		Return session identifier. This value is unique for every TCFS2 instance.



2. Command line

Command line allows executing any number of both actions and commands defined in configuration file. Syntax:

TCFS2[.exe] [<parameters>] [<actions>] [/ei <commands>] [/ea <actions>] ...

Parameters:
	/d=<msec>
		Set sleep time before condition check after command execution (default value is 50 ms);
	/ea, /ei, /ef
		Choose how to treat following names in command line - as commands, actions or direct command contents;
	/i="<path>"
		Set path to wincmd.ini (by default COMMANDER_INI environment variable is used);
	/u[-]
		Enable/disable writing default Undo action on program exit;
	/uc
		Clear current undo string that was collected since program start;
	/us[="<action>"]
		Save current undo string to action with specified name (or with Undo name if name is not specified) immediately;
	/w[-]
		Enable/disable error reporting.

You must quote every command call that contains spaces. Also you must quote direct command contents (after /ef parameter). Don't quote in same quotes multiple command calls or action names (after /ea or /ei parameters). Refer to examples below.


Examples:

Example of executing undo action:
TCFS2 undo

Example of executing fs2 command with disabled undo string saving (command uses own undo action):
TCFS2 /u- /ei fs2

Example of executing title_switch action and then m2 and t2 commands with disabled undo string saving - undo string is saved to test_undo action:
TCFS2 /u- title_switch /ei m2 t2 /us=test_undo

Example of increasing panel separator by 10% (active TCFS2Tools required; quotes are necessary since parameter contains spaces):
TCFS2 /ei "set_separator(sepPos + 10)"

Example of changind active panel's width to 80% using command with parameter (active TCFS2Tools required; quotes are not necessary):
TCFS2 /ei "sp_set_active(80)"

Example of switching between current view mode and full mode for active panel (you may specify any other cm_Src* view mode index):
TCFS2 /u- /ei switch_viewmode_S(302)

Example of direct execution of command contents (expression must be quoted):
TCFS2 /ef "run_action(fs) save_undo(fs_undo), style(# & $00C00000) | run_action(fs_undo)"

Example of changing current path to D:\ (user-command em_CD must be defined with command CD and parameter %A):
TCFS2 /ef "tem(`em_CD D:\`)"

Example of changing target panel's path to D:\:
TCFS2 /ef "tcd(, `D:\`, s)"



3. TCFS2Tools

TCFS2Tools is a module that provides additional features like moving panel separator, checking active panel etc. It is not included into standard package and should be downloaded and installed separately (download page is here: http://www.totalcmd.net/plugring/tcfs2tools.html).


Discussion page on official board: http://www.ghisler.ch/board/viewtopic.php?t=29700



History:

2016-01-14	2.3.0.504
	+ added support for <``> quotes (allow grave accents inside)

2015-11-10	2.2.3.498
	* broken # variable in set INI functions (since 2.2.0.456)

2015-09-12	2.2.2.480
	+ findwnd allows searching for child windows of given parent window
	* findwnd searching w/o specifying window class bug

2015-05-06	2.2.1.476
	+ case sensitive and insensitive INI string comparisons
	+ send function is now able to send any virtual key (e.g. Win key as VK_91)
	+ send function supports zero handle value (disables window activity checks)
	* fixed string to number conversion when reading from INI
	* items return 0 if no branches were executed
	* ignoring double quotes bug

2014-05-28	2.2.0.444
	+ complex strings may now be built from multiple strings and calculated numbers
	* warn about end of line when reading function parameters

2014-02-10	2.1.1.424
	+ loop function
	+ special handling of double quotes: ignoring them when inside grave quotes
	+ varcnt, varget, varset functions
	+ verbatim mode for send function

2013-05-24	2.1.0.394
	+ tem function is now able to pass parameters
	+ send function allowing passing keypresses
	+ additional parameters for tcm, tem and msg functions allowing to send messages asynchronously
	+ findwnd function finds TC window
	+ sendmsg function sends messages to specific window
	+ optional parameter for send function allows specifying window
	+ tcd function changes dir(s) in TC
	+ terminate button in report error message
	* strings may now contain syntax characters like ';', '|' and '('
	* strings may now be passed as substituted parameters

2012-11-17	2.0.5.310
	+ set INI string values
	+ remove INI keys

2011-11-14	2.0.4.300
	+ new redraw function
	+ new regmsg function
	+ new ini, set_ini functions
	* wrong environment variables processing in redirection (after 2.0.3.256)
	* test function is renamed to eval (old name is supported for compatibility too)

2011-08-31	2.0.3.264
	+ new if function works like ?: operator but calculates only one expression
	+ new null function that checks if parameter is a null string
	+ redirection in tcini and set_tcini now supports relative paths
	+ hide busy cursor after starting TCFS2
	+ pseudo-macro @sid that have unique value for every TCFS2 instance

2011-05-08	2.0.2.240
	+ new section for macroses that may be called from parameters of functions
	+ now it is possible to call functions directly from parameters of another functions
	+ new function test allows checking complex condition
	+ tcini and set_tcini now support redirection (additional parameter allows disabling it, %$PERSONAL%, %$APPDATA% and %$LOCAL_APPDATA% are supported pseudo-variables)
	+ heap is used for buffers instead of stack (more recursion levels available)
	+ reports some errors, use parameter /w- to disable
	+ tem function allowing executing TC user commands
	- functions separator and set_separator are removed (their functionality moved to TCFS2Tools)
	* set_tcini uses error_value as base if parameter doesn't exist

2010-11-21	1.5.0.10
	+ separator function
	+ now commands may have up to 9 parameters
	* commands w/o parameters in actions were not working after adding parameters support

2010-11-03	1.4.2.30
	+ set_separator function
	+ now functions may be executed directly via command line using parameter /ef
	* more accurate separator position calculation

2010-09-09	1.4.1
	* actions in commands were not working because of incorrectly deleted spaces in lines
	* action in command didn't work if  its name was ended by tab character
	* freeze when /d=<msec> parameter was used
	* crash on msg function call
	* some INI corrections

2010-08-26	1.4.0
	+ all parameters now are correct expressions (note that for some functions format of parameters has changed)
	* minor changes

2010-07-03	1.3.6
	+ new function set_tcini to modify wincmd.ini keys
	+ new operator @ for move function
	* is_style function renamed to style
	* delay was ignored if undo condition missed

2010-06-16	1.3.0
	+ now command is excuted if its condition is TRUE instead of false (more logical)
	+ added optional condition for undo (if not set, checks if command's condition become false)
	+ functions 0 and 1 for conditions
	* /d<msec> and /i"<path>" parameters changed to /d=<msec> and /i="<path>"

2010-06-12	1.2.4
	+ more than one function call in single item supported (divided by spaces)
	+ run_item and run_action functions allow executing commands and actions from commands (with loop protection)
	+ delay function
	+ allows specifying action name to save undo string
	+ save_undo function to save undo action with passed name
	* /u- and /u was messed up
	* garbage in undo string

2010-06-11	1.2
	+ every item can contain any number of else-commands which are executed if previous command's condition already true
	+ style functions now allow working with extended styles too
	+ parameter added for msg function to send message using PostMessage instead of SendMessage

2010-06-05	1.1
	+ allows setting/removing topmost style
	+ allows sending window messages using msg function
	+ relative parameters for move function

2010-06-03	1.0
	! birthday of idea to improve existing TCFS addon
	+ commands to change window style, resize/move window to exact position, send TC command
	+ commands to read window style and wincmd.ini to know if command need to be performed
	+ backup operation feature logs all undo commands from performed functions

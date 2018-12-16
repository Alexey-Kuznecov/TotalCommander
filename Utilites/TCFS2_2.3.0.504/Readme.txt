TCFS2 Addon for Total Commander
-------------------------------
(English section is below)

������� ��������� ��������� �������� ���� ��:
+ �������������/��������������� ����
+ ���������� � �������� ������
+ �������� � ���������� ���������
+ ������� ���� "������ ������ ����"
+ ��������� ����� ����������� �������� ���� ��
+ �������� ������� ���� � �������
+ ���������� ��������� �������� �������
+ ����������� ������� ������
+ �������� ��������� �������� �������� ������� ������
+ � ������ ������...


0. ��������� �������� �����������

� ����������� ������� � ���� ����� ��� ����������� �������� � ����� ������������ ��������� ����� ��: ������� ����������� � ��������� '', � ������ - � ������� "".

������� ������ �� ��������� ��������� �������� ����� (���������� �������) �� ������ ������� TCFS2. ��� ������� �������� ������ � ���.


1. ���� ������������

��� ������� ������������� � ���������������� ���� � � ����� ������ ����� ���� ��������. ���������������� ���� ������ ���������� � ����� ������� � ����� ����� �� ��� �����, �� ���������� INI. � �������� �������� ��������� ������ ������ ����� ������������ � ���������� ��������� (���������� ��� �� ����� RU � ����� ���������).

���������������� ���� ������� �� ���������: Items (������ ������), Actions (������ ��������) � Macros (������ ��������). �������� ������������ ����� ������������������ ������ ��� ����������, ������� � ���� ������� �������� ������ ������� �������, � ����� �������������� ������� ��� ��������. ������� - ��� ��������� � �������, � ������� ����� ���������� �� ���������� ������. ���� ����� ����������� ��� ������. ������ ������ ����� ��������� �����������, ������� ����������� ����� ����� ';'.

����� ������������ ����������� ������ ��������, ��������� ���������� ����� ������� �� ������ � ����� ������������.



1.1. �������������� �������

���� ��� ���� �������, ������� ����� �������� �� ������ - �������, ����������� �����-�� ��������, � ������� �������� ������-���� �������. ����������� ���������� ������� �����������, ����� ������ ��������� ������� ��� ���������, � ���� �������� ��������� - �� ������� ������).

������ �������� �������� ����� ��������� ������������� �������������� ���������, ����������� �� �������� ����� �� (�������������� ��������� ( ) ! ~ % * / + - << >> < > <= >= != == & ^ | && || ?:). �� ���� ��������, ��� ��� ����� �����, � ���������� ����� ������������ ���������� #, ���������� �� ���������� �������� ������� ��������� (������ ����, ����� � �.�.), � ����� �������� ������� � ������� ��������. �������� �������� ������� ����� ��������� � ����������������� �������, ��� ���� ����� ��������� ����� ������ ���� '$'. ��� �������� �������������� ����� ����� ������ �������� ���� '-'. ������������ ��������� ������� � ���������� �������. ����� ����� ������� ���������� ��������� ������ ����������, ���� ���� ���������� ��� (��� � ����� ��).

���� ������� ��������� ��������� �������� (�� ���������� �������������� ����������; ��������, ������� send, tem, ini, set_ini), ��� ���������� ��������� � ����� ������� `` (������ '`' - �� ������� � �������� '~'), ���� �� �������� �������, ������� ��� ������ (���� � ������ ����� ��������� � ����� �������� ������, ��� ���� ��� ������ '`' � ���� � ����� ����������). ������� ��������� ���������, ��� �������, ����� ��������� ��� ����� �������, ���� �������� �� ������� ���� (��������, � ������� set_ini �� ������� ������� ������������ ��� ���������). �� ����� �������, ���� ������ ��������� �������� ����� �������� � ����� �������. ������� ������ ����� �������� �� ���������� ������, ��� ���������, ��� � �������� (������ ����� ������ ���� ���������, ���� �� ������ ������� ``; �������� ��������� ����� ��������� ����� ���������), ����� �������� ������ ���������� ������������� ���� ��������� � ����������� �������� ������.

	0, 1
		���������� ��������������� ���������, ����� �������������� ��� ������������ ����������� �������;
	if(<condition>, [<true_expression>], [<false_expression>])
		��������� � ���������� ��������� ������ �� ��������� true_expression ��� false_expression � ����������� �� ���������� ������� condition (���� ���������, �� true_expression). ���������� 0, ������ �� ��������, ���� ��������������� ��������� ��� ���������� �� �������. � ������� �� ��������� ?: ��������� ������ ���� �� �������� ���������;
	loop(<expression>)
		��������� ���������� ���������, ���� ��� �� ������ ������ 0. ���������� ���������� ����������� �������� �����. ���������� @ � ��������� ����������� �� ������ �������� (������� � 0);
	null(<something>)
		���������� 1, ���� �������� �� �������� ������ �������. ����� ���� ������������, ����� ���������, ������ �� �������� ������� ��� ������� � �����������;
	eval(<expression>), test(<expression>)
		���������� ��������� ���������� ���������. ������������, ��������, ��� �������� ����� ���������� �������;
	style([<value>], [[<exvalue>])
		��������� ������������� ������ ������ ������, ��������� � ����������. ���� ������������ � ��������, � ����������� �����, ���������� ��������� ������������ ��������� � (������ ������ ���� ���������� ����� ��������� �������). ���������� # ����������� �� ������� �������� ������� ������. ���� ���������� # � ��������� �� ������������, �� �������� ��������� ������������ � �� ��������� �������������;
	tcini(<section>, <key>, <value>|`<string_value>`, [<error_value>], [<flags>])
		��������� �������� �������� ��� ��������� �������� ����� � ��������� ������ � ��������� ������ ����� wincmd.ini (��� �������� error_value, ���� ���� �� ������) � �������� ���������. ������ ������������ �������, ��� ����� ��������. ��� ��������� �������� �������� ���������� # � ��������� ����������� �� �������� �������� �����/error_value. ���� ���������� # � ��������� �� ������������, �� ����������� ����� ��������� ��������� �������� �����/error_value � value, ����� - ��������� ���������� ��������� (������� ������ # ��� value, ����� ������� �������� �����). �������� flags �� ��������� ����� $1 � �������� �� ����� ��������: $1 - ������������ ��������������� ������ ����� wincmd.ini, $8000 - ���������� ������ � ������ ��������. ��������������� �������������� ��� ��, ��� � ����� ��, �������������� ������-���������� %$PERSONAL%, %$APPDATA% and %$LOCAL_APPDATA%, � ����� ������� ���������� ���������;
	ini(`<inipath>`, <section>, <key>, <value>|`<string_value>`, [<error_value>], [<flags>])
		�������� ��� ��, ��� � tcini, �� � ��������� � ������ ��������� INI-������;
	msg(<umsg>, <wparam>, <lparam>, [<async_mode>])
		���������� ��������� ���� �� � ���������� ���������. ���� async_mode>0, ��������� ���������� ����� PostMessage, ���� async_mode<0, ����� SendMessage (��� � ��� async_mode=0), �� ��� �������� ����������;
	regmsg(<msg_name>)
		���������� ����� ������������������� ��������� � ����� ������ (�������� ������� RegisterWindowMessage);
	findwnd([`<class>`], [`<text>`], [<parent>], [<zindex>])
		���������� ���������� ���� � ��������� ������� �/��� ������ ������, �������������� ������� ����� ��. ���� ����� ����� ���� � ����� ������� ��� �������, �� ���������� ��������������� ��������. �������� ����������� ������������� ���� � ��������� parent ��������� ����� �������� ���� (��� ���� �������� zindex ��������� ���������� ����� ����, ������� � 0);
	tcd([`<left_path>`], [`<right_path>`], [S][T], [<async_mode>])
		���������� �� ������� ����� ���������� � �������. ��������� left_path � right_path ��������� ���� � ����������� ����� � ������ ������, ������ �������� �������� �����: S - ������� ����� ������� ��������, � ������ - ����������, T - ������� ���������� � ����� ��������. ������� async_mode ������ 1, ����� �� �����, ���� �� �������� �������;
	tcm(<cm_index>, [<async_mode>])
		���������� �� �������� ��������� ���������� ������� � ��������� ��������. ������� ����� ���������� � ����� totalcmd.inc � � ��������� ������ ��. �������� async_mode �������� ��� ��, ��� � � ������� msg;
	tem(`<em_command_name> [<parameters>]`, [<async_mode>])
		���������� �� �������� ��������� ���������������� ������� � ��������� ������. ��� ������� ������� � ����������� ���������� �� ����� ������ ����� ����� ������� � ���������� ��� ������ � ����� ������� `` (�� ����� �� ������������ ������). ������� async_mode ������ 1, ����� �� �����, ���� �� �������� �������;
	send([@]`<keystrokes>`, [<hwnd>])
		�������� ������������������ ������� ������ ��������� ���� (��������, �������) ������� ����� �� ��� ����, ���������� �������� ������ � ��������� hwnd (������� �������� 0, ����� ��������� �������� ���������� ����). ����� ��������� ����������� �������, ���������� �� ����������� � �������� �������: BACKSPACE, BKSP, BS, BREAK, CAPSLOCK, DEL, DELETE, DOWN, DQ (������ '"'), END, ENTER, ESC, HOME, INS, INSERT, LEFT, NUMLOCK, PGDN, PGUP, PRTSC, RIGHT, SCROLLLOCK, TAB, UP, F1-F12, ADD (Num +), SUBTRACT (Num -), MULTIPLY (Num *), DIVIDE (Num /), VK_xxx (����������� ������� � ����� xxx, ��������, VK_91 - ������� Win). ��� ������������� ������� ������� � �������� ������� ���� ������� � ����� � ���������� ����� ������. ����� ��������� �������� (��� ������������������� ������, ������ � ������� ������) ����� ������� ���� ��� ��������� �������������: '+' - � ������� Shift, '^' - � ������� Ctrl, '%' - � ������� Alt, '~' - �������� ��� ������, � �� ��� ������� (� ����������� �������� � ���������). ����� ������� ��������� ������� ('+', '{', '(' � �.�.), �������� � � �������� ������. ������� '@' �������� ����� �������� ������ �����, � ������� ��� ������� (������� ���������) ���������� ��� �������;
	sendmsg(<hwnd>, <umsg>, <wparam>, <lparam>, [<async_mode>])
		���������� ������� ��������� ���� � ������������ hwnd. � ��������� ��������� ������� msg;
	varcnt()
		���������� ���������� ���������� ���������� (���������� ����� �� ���������� TCFS2);
	varget(<n>)
		���������� �������� ���������� ���������� � �������� n;
	varset(<n>, <x>)
		���������� x �� ���������� ���������� � �������� n;

	show(<state>)
		����������/�������� ����, ������� API-������� ShowWindow � ���������� state, ���������� �������� ����� ���������� � ������� �� ���� �������;
	move([<x>], [<y>], [<cx>], [<cy>], [<topmost>])
		����������/�������� ������ ����. ������ 4 ��������� ��������� ������ ������� � ������ ����. ���� �������� ������, ��������������� �������� �� ����������. ���������� # � ���� ���������� ����������� �� �������� �������� ��������, � �������������� ���������� @ - �� ������ ��� ������ ������. �������� topmost ��������� ��������/��������� ����� "������ ������ ����" (���� �� ������, ����� �� ����������);
	redraw()
		�������� ������ ����������� ���� ��. ��������, ����� ������������ ��������� ��� ����� ���������� ����������� ����;
	run_item(<item_name>, [<params>])
		��������� ������� � ��������� ������, ����� ���������� ��������� ������� �������. ���� ������� ������� ���������, ������� ��, �������� ��������;
	run_action(<action_name>)
		��������� �������� � ��������� ������, ����� ���������� ��������� ������� �������;
	set_style([<value>], [<exvalue>])
		�������� �������� � ����������� ����� ����. ����� ������������� ������� ������ (�������� ������ - � ������� �� API-������� SetWindowLong � � ���������� GWL_STYLE � GWL_EXSTYLE). ���������� # ����������� �� ������� �������� ������� ������;
	set_tcini(<section>, <key>, [<value>]|`<string_value>`, [<error_value>], [<flags>])
		��������� ������/�������������� ����� wincmd.ini. ���� �������� value �������� � ����� ������� ``, �� ������������ � ���� ������, ����� value ��������������� ��� �������� ���������. ���������� # ����������� �� �������� �������� ����� (��� �� ��������, ���������� � ��������� error_value, ���� ���� �� ������). ���� �������� value �� �����, ������ ��������� �� INI;
	set_ini(`<inipath>`, <section>, <key>, [<value>]|`<string_value>`, [<error_value>])
		�������� ��� ��, ��� � set_tcini, �� � ��������� � ������ ��������� INI-������;
	save_undo(<undo_name>)
		��������� ������� ������ ������ � �������� � ��������� ������;
	delay(<msec>)
		���������������� ���������� ������� �� �������� �������� �������.



1.2. ������ ������

� ������ [Items] ������������� �������, ���������� ���� ��� ��������� ������� ������� ��� ���������� (����������� ���������), �������������� ������� ������������� ���������� ������� (��� ��������� �� ���������� �������, ��������� � ���������� ������� test), � ����� �������������� ������ ������. ������ ������ ������������ � ������������ �������� ������, ���� ������� ������ ������� (���� ��� �� �������, �����������, ����� �� ������ ������� ���������� ������� - ���� ������� 1 ��� ������� ������, ����� ����� ������������ ������). ������ ������ ����� ��������� ��������� ����� ������, ����������� �������� '|' - � ���� ������ ����� ������� ����� ����������� ��� �������, ���� �� ����� ������� ������ �������� - ��������������� ������� ����� ���������, ���������� ������� ������ ����� ���������������.

Id=apply_command1(...) [apply_command2(...) ...] [, check_command(...) [, undo_ids [, undochk_command(...)]]] [| apply_commandN(...) ...] ; ��������

��� ������ ������� ����� ����� �� � ������ � ������� ������� �� 9 ���������� �������. ��� ��������� ����� ����������� ������ �������� #1, #2, ..., #9 �� ���� ������ ������� �� ������ ���������� �������. ���� �������� �� �������, �� ����� ������� � ������ ������. ������������� ��������� ������� #1 � �.�. � ������, ����� �������� ������ ��� ����������� ��������� � �������� ����������.


���������� ��������� ��������, ����������, ��� ����������� �������:

������ ������� ��� ���������� ������ ������������ ��:
tb0=tcm(2901), test(hasButtonBar), tb1

����� ���������� ������ hasButtonBar, �����������, ����� �� 1 ���� ButtonBar ������ [Layout] ����� wincmd.ini (���� ����� ���, ������������ �������� ������, ������ 1, ��� ��� �������� ����� ����� � �� �� ��������� ����� 1). ���� ������� �������, ����������� ������� tcm, ������������ �� ������� cm_VisButtonbar (2901). ����� ������� ����������� ����� (����� �����, ���������� ���������� /d) �, ���� ��� ����� ������, � ����� ������������ ������� ��������� ������ ������������ tb1.

������ ������� ��� �������������� ���� �� ������������ ��������� � ����������� ����������� ������ ������:
m0p=show(9), test(isMaximized), m1, 1

� ����� ����������� ������� ����� ������������� ����. ������� test ��������� ���������, ������� ������ isMaximized, ������� ��������� ����������� ����� WS_MAXIMIZE. ���� ���� �����������, ��������� ������� �����������. ���� ���� �����, ���������� ������� show(9), � ����� ������� m1 ���������� ������������ � ������ ������. ���� �� ��������� ��������� �������� 1, �� ����� ����� ������� ������ ���� ������� test(isMaximized) � ���������� ���������� ������� ������ ������ (�� ����, ���� ������������� �� ������������ ���������).

������ �������, ������� ��������� ����������� ���������� ��������� ���� �� (������ ������, ������ ������ ������, ��������� ������), ���� ���� �� ���� ��������, ��� ��������, ����� ��� ���������:
multi_switch=run_action(multi_enable), tcini(Layout, DriveBar1, 0) | run_action(multi_enable), tcini(Layout, DriveCombo, 0) | run_action(multi_enable), tcini(Layout, CmdLine, 0) | run_action(multi_disable)

���������� ������� ��������� ������� tcini(Layout, DriveBar1, 0). ���� ��� ������� (�� ����, ������ ������ ���������), ���������� �������� multi_enable ��� ��������� ���������. ����� ����������� ������� ������� ��������, ����� �������� (����� �������� ����� ��������� ����� ����� ���������). ���� ��� �������� ��������, ����� ��������� ����������� ������� run_action(multi_disable), ������� ������� �������� multi_disable ��� ���������� ���������. ���������������, ��� � ������ �������� ���������� �������� multi_enable, ��������� �� ������ db1 dc1 cl1, � multi_disable, ��������� �� ������ db0 dc0 cl0.

������ ��� �� �������, ������� ��������� ����������� ���������� ��������� ���� ��, �� � �������������� �������� � ������� test:
multi_switch=run_action(multi_disable), test(hasDriveBar && hasDriveCombo && hasCmdLine) | run_action(multi_enable)

������� ����������� �������� ������� test, ��� ���� ���������� ��� 3 ������� � ����������� �������� �. ������� test ���������� ������, ������ ���� ��� ��� ������� ������� ������, �.�. ��� ��� ����������� �������� (������ ������, ������ ������ ������ � ��������� ������) ��������. � ���� ������ ���������� �������� multi_disable, � ��������� ������ ����������� �������� multi_enable (��� ����������).

������ �������, ������������� ���� �� ���� �����, ���� ��� ��� �� �������, ��� �� ����������� ������ ���� �� ��������, ������� ��� � �������� ������:
switch_sp=move(# ? 0 : @*7/64, # ? 0 : @*7/64, @-# ? @ : @*25/32, cyWorkArea-# ? cyWorkArea : @*25/32), , switch_sp

����������, ��� ��� ��������, �� ������� ������� ���� �� �����������. ��� ���������� ��������� # ? 0 : @*7/64 �����������, ����� �� ���� ��������� ����� ������ ?, � ���� ��������� �� ����� ���� (�.�. �������), ������������ ������ �������� ����� ����� ? (�.�. 0), � ��������� ������ ������������ �������� ����� ����� : (�.�. @*7/64). � ���������� ��� ��������� ������� ������� ������� ���� ����� ������������� ����� ����� � 7/64 �� ������� ������. ���������� ��������� ���������� ����������� ����� �� �������. ����� ��� ���������� ������ ���� ���������� ������ cyWorkArea, ������������ ������ ������� ������� ������ ��� ������ �����.

������ �������, ����������� ������ �������� ������ �� 95% ����� ����������� ����������� �������, ���� ����������� ����� �� ������, ��� ������������ ������� �� 50%:
sp_sw_50_95=run_item(sp_set_active, sepPos == 50 ? 95 : 50)

���������� ������ sepPos, ������������ ������� ������� ����������� �������. ����� ���������� ������� sp_set_active �� ��������� 95, ���� ������� ������� ����� 50, ��� �� �� ��������� 50 � ��������� ������. � ���� �������, ������� sp_set_active (������ � ������� ��������), ��������� � ���������� 95, ������������� ����������� � ������� 95%, ���� ������� ����� ������, ��� �� � ������� (100-95)%, ���� ������� ������. ��� ����������� �������� ������ ���������� ������ L_isActive, ������������ 1, ���� ������� ����� ������. ������ ������� ����� �������� ������ ��� �������� ������ TCFS2Tools, ������� ��������� ���������� �������� ������ � ������/���������� ������� �����������.

������ �������, ����������� ������ �������� � ����������� �� ����, ������ �� ������� Shift ��� ������ ������ ����:
check_shift=run_action(action_shift_pressed), test(pressedShift || pressedRButton) | run_action(action_shift_not_pressed)

������� test �������� ������� pressedShift � pressedRButton. ���� ���� ���� �� ��� ����� ������, test ����� ������, � ����� ��������� �������� action_shift_pressed, � ��������� ������ ����� ��������� �������� action_shift_not_pressed. ��� ����������� ��������� ������ ���������� ������� ������ TCFS2Tools.

������ �������, ���������� ������������ ������ ������������ �� ������:
set_bar=if(#1 == 1, tem(em_bar1)) if(#1 == 2, tem(em_bar2)) if(#1 > 0, set_tcini(Layout, ButtonBar, 1), run_item(tb0)) set_tcini(TCFS2, Bar, #1)

������� ����� ���� ������������ �� ������ ������, ��� ���������� ����� ������������� ������ � �������� Bar ������ TCFS2 ����� wincmd.ini. �� ������ �������� ������ ������� ������� if, ���� ����������� ������� ���������� �������. ���������������� ������� em_bar1, em_bar2 � �.�. ������ ���� ���������� � ��. ��� ������� ��������� ������� �������� ������, ��� ��������� - ������������� ���������� � wincmd.ini �������� ButtonBar=1 (�� �� ������ ����� ��� ������ ������� OPENBAR).

������ �������, ������� �������� ������ ������ ������������ �� 10 ������ ��� ���������� ������� ������:
quick_bar=set_tcini(TCFS2, #0, 0) run_item(set_bar, 1), test(tcini(TCFS2, Bar, #)!=1) | set_tcini(TCFS2, #0, @sid) run_item(set_bar, 2) delay(10000) if(tcini(TCFS2, #0, # == @sid), run_item(set_bar, 1))

������� ����������� ����� ������� ������. ���� ������� �������� ������, ������� ���������� ID ������ � �������� � ������ ������� � ������ TCFS2 ����� wincmd.ini � �������� ������ ������ ������������. ����� ����� ������� ���� 10 ������, �� ��������� ������� ���������� ������ ������, ������ ���� ���������� ID ������ �� ���������. ���� ������� ����������� ��� �������� ������ ������, ��� ���������� ID ������ � ���������� ������ ������ ��� ��������. ������������� ������ ����� ��������� �������� �������� ������������ �������, ���� ������� ���������� ����, ��� �������� ����� �������� (����� ������ ����� ������� �����������, ���� ������ �� ��� � ������ ��������).

������ ������� ��� ������������ � ������������� ����� � �������:
fs2=if(hasCaption, locktc(1) + run_action(fs) + locktc(0) + show(3) + save_undo(fs_undo), show(9) + locktc(1) + run_action(fs_undo) + locktc(0)) run_item(update)

����� ����� ������ ������ hasCaption ��� �������� ������� ��������� ����. ���� ��������� ����, ����� ������� ������� run_action(fs) � save_undo(fs_undo) ��� ������������ � ������������� ����� (�������� fs ����� ���� �����, �� ��� ���������� ������ ������ ������� ��� ������ �������� ��������� ����) � ������ � �������� fs_undo ������ ������, � ����� ���� ����� ���������. ���� �� ��������� ���� ����������� (�� ����, ������������� ����� �������), ������ ������� ��������� �� �����, ������� ����� ������� ������� run_action(fs_undo) ��� ���������� �������� ������ � ���� ����� �������������. �� ����� ���������� ������ �������� fs2 ��� fs_undo ����� ��������� ����������� ���� � ������� ������� locktc (�� ���������� ����������� ��� �������������� ���� �� ������������ ���������, ��� �������� �����). ����� �� ���������� ������� ����� ��������� ������ ����������� ����.

������ �������, ���������� ������ ������������, ���� � BAR-����� %COMMANDER_PATH%\Default.bar ����� 30 ������:
bbhide_if30=if(ini(`%COMMANDER_PATH%\Default.bar`, Buttonbar, Buttoncount, #>30), run_item(tb0))

������� ini ������ �������� ��������� Buttoncount �� BAR-����� � ���������, ������ �� ��� 30. ���� ��� ���, ���������� ������� tb0 ��� �������� ������ ������������.

������ �������, ����������� ���������� �������������� � �������� ��������� ������ �����, � ����� ����� ������ � ������:
test_hello=send(`^m~(������, ���! ;{)}){tab}{del}{tab}~(������|;){tab}~(������|:){tab 5}{home}`)

������� �������� ������� Ctrl+M ��� ������� ����������� ��������������, ����� ������������ ����� ������ � ��������� �� �������.

������ �������, ��������� ��� ���������� ������ ��������� � �������� �������, ������������ ������� ������:
set_hint_fields=set_tcini(HintsCustomField, `` #1 `exts`, #2) set_tcini(HintsCustomField, `` #1 `fields`, #3)

������� ��������� ��� ���������: ����� �������, ����� ������ � ������ ���������. ����� ������� ������������ ��� ������������ ���� ������, � ������� ����� �������� ��������. ��������, ��� ������ 3 ������ ����� �������� � ����� 3exts � 3fields.



1.3. ������ ��������

������ [Actions] ����������������� ����� �������� �������� - ������������������ ������ ��� ����������, ����������� ���������. ����� �������� �����������, �� ���� ���� ���������� �������� � ������ Undo - � ���� ��� ������ ������� ��������� ����� ������������ ������� ��� ������ ���������, ��������� � ���������� ������ ��������� (���� �� ��� ������ �������� /u-), ������� �������� ��� ������� �� �������������.



1.4. ������ ��������

������ [Macros] �������� ����������� �������� � �������, ������� ����� �������� ��� ���������� ���������� ������ �������. ���������� �������� �� ������������� � �������� ���������, � ����������� ��� ������. ������ ������ �������� ��� �������, ���� ��������� � ���������, ������� ����� ��������� ��� ��������� � �������. ������� ���������� ��������� ����� ��, ��� � � ���������� ������� (������� � �.�. 1.1 ������� �����). ��� � �������, ������� ������������ �� 9 ����������, ������� ����� ����������� ������ �������� #1, #2, ..., #9 � ������ ��������� ����� ��� �����������.



1.5 ������-�������

��� ������ ������� � �������� ����� ������������ ��������� ���������������� �������. �� ����� ���������� � ������� '@'.

	@sid
		���������� ������������� ������. ��� �������� ��������� ��� ������ ���������� ����� TCFS2.



2. ��������� ������

��������� ������ ��������� ��������� ��������� ��� ��������, ��� � ��������� �������, ������������ � ����� TCFS2.ini, ������ ����� ����� �� ���� ������. ���������:

TCFS2[.exe] [<parameters>] [<actions>] [/ei <commands>] [/ea <actions>] ...

���������:
	/d=<msec>
		������ ����� � ������������� �� �������� ����� ����������� ������� � ��������� ������� ������ (�� ��������� 50 ��);
	/ea, /ei, /ef
		�������, ��� ������� ���������� �������������� � ��������� ������ - ����������, ��������� ��� �������� ���������� �������;
	/i="<path>"
		������ ���������� ���� � ����� wincmd.ini (�� ��������� �������� ���������� COMMANDER_INI);
	/u[-]
		��������/��������� ������ �������� ������ Undo �� ��������� ������ ���������;
	/uc
		�������� ������� ������ ������, �������������� � ������ ������ ���������;
	/us[="<action>"]
		���������� ��������� ������� ������ ������ � �������� � ��������� ������ (��� � �������� Undo, ���� ��� �� �������);
	/w[-]
		�������/��������� ����� ��������� �� �������.

������ ����� �������, ���������� �������, ������ ���� �������� � �������. ����� � ������� ������� ��������� ������ ���������� ������ (����� ��������� /ef). �� ���������� � ����� ������� ����� ������ ������ �������� ��� ������� (����� ���������� /ea � /ei). �������� ������� ����.


������� �������:

������ ������� �������� undo:
TCFS2 undo

������ ������� ������� fs2 � ����������� ������ �������� Undo (������� �������� �� ����� ��������� ������):
TCFS2 /u- /ei fs2

������ ������� �������� title_switch � ������ m2 � t2 � ����������� ������ �������� Undo, �� ������� ������ ������ � �������� test_undo:
TCFS2 /u- title_switch /ei m2 t2 /us=test_undo

������ ���������� ������� ����������� �������� ������� �� 10% (��������� TCFS2Tools; ������� �����������, �.�. ���� ������� � ���������):
TCFS2 /ei "set_separator(sepPos + 10)"

������ ��������� ������ �������� ������ �� 80% � �������������� ������� � ���������� (��������� TCFS2Tools; ������� �������������):
TCFS2 /ei "sp_set_active(80)"

������ ������������ ����� ������� ������� � ��������� ������� �������� ������ (����� ������� ������ ������ ������ �� cm_Src*):
TCFS2 /u- /ei switch_viewmode_S(302)

������ ������� ������ ����������� ������� (������� ������ ��������� �����������):
TCFS2 /ef "run_action(fs) save_undo(fs_undo), style(# & $00C00000) | run_action(fs_undo)"

������ ����� �������� ���� �� D:\ (������ ���� ���������� ���������������� ������� em_CD � �������� CD � ���������� %A):
TCFS2 /ef "tem(`em_CD D:\`)"

������ �������� � ���������� D:\ � ���������� ������:
TCFS2 /ef "tcd(, `D:\`, s)"



3. TCFS2Tools

TCFS2Tools - ������, ��������������� ����������� �����������, ��������, ����������� �������� ������, ����������� ����������� ������� � �.�. �� �� ������ � ����������� �������� � ������ ���� �������� � ���������� �������� (�������� �������� �����: http://wincmd.ru/plugring/tcfs2tools.html).


���������� �� ����������� ������������� ������: http://forum.wincmd.ru/viewtopic.php?t=13332



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

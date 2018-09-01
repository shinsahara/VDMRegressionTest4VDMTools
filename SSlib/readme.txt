SSLib -- VDM++ライブラリ written by Shin Sahara

ファイルの説明
	*.vpp		--VDM++のソース（テキストファイル版）

	--以下の説明で、クラスと記述したVDM++ファイルは、インスタンスを持つクラスを定義しているが、
	--モジュールと記述したVDM++ファイルは、インスタンスを持たず、関数型プログラミングで実装している。
	Calendar.vpp	--暦（カレンダー）に関わる機能を持つクラス
	Character.vpp	--文字に関わる機能を持つモジュール
	CommonDefinition.vpp		--事務処理用共通定義
	Date.vpp		--日付に関わる機能を持つクラス
	DoubleListQueue.vpp	--２つの列を使った待ち行列モジュール
	Function.vpp	--関数プログラミングに関わる機能を持つモジュール
	Hashtable.vpp	--ハッシュ表に関する機能を持つモジュール
	Integer.vpp		--整数に関する機能を持つモジュール
	JapaneseCalendar.vpp	--日本の暦に関わる機能（休日など）を持つクラス
	Map.vpp		--写像に関する機能を持つモジュール
	Object.vpp		--オブジェクトに関する共通機能を持つクラス
	Queue.vpp		-- 待ち行列に関わる機能を持つモジュール
	Real.vpp		--実数に関わる機能を持つモジュール
	SBCalendar.vpp	--証券会社向けの暦を持つクラス
	Sequence.vpp	--列（シーケンス）に関わるソートやマージなどの機能を持つモジュール
	Set.vpp		--集合に関わる機能を持つモジュール
	sslib.prj		--SSlib用のVDM++のプロジェクトファイル
	stdlib.prj  --stdlib下の標準ライブラリを使うプロジェクトファイル
	String.vpp		--文字列に関する機能を持つモジュール
	Term.vpp		--開始と終了のTimeを持つ期間を表すモジュール
	test			--テスト用ファイルの入ったフォルダー
	UniqueSequence.vpp	-- 唯一の番号を発番する
	vdm.tc		--テストカバレージの結果が入っているデータ
	
	AllT.vpp		--単体テスト用プログラム（テキストファイル版）
	CalendarT.vpp	--暦クラスを検査する
	DateT.vpp		--日付クラスを検査する
	DoubleListQueueT.vpp	--２重リストで実装された待ち行列クラスを検査する
	HashtableT.vpp	--ハッシュ表を検査する
	IntegerT.vpp	--整数クラスを検査する
	Makefile		--モデルを実行し、ドキュメントSSlib.PDFを生成する
	MapT.vpp		--写像クラスを検査する
	ObjectT.vpp	--オブジェクトクラスを検査する
	RealT.vpp		--十巣クラスを検査する
	SequenceT.vpp	--列クラスを検査する
	setException.script	-- "set exception" オプションを指定した場合のテスト用スクリプト
	SetT.vpp		--集合クラスを検査する
	StringT.vpp		--文字列クラスを検査する
	TestCase.vpp	--回帰テスト用テストケースのスーパークラス
	TestDriver.vpp	--回帰テスト用テストドライバー
	TestLogger.vpp	--回帰テスト用テスト結果出力
	test.script		--テスト用スクリプト
	UniqueSequenceT.vpp	-- 唯一の番号を発番するクラスを検査する
	vdm.tc		--テストカバレージの結果が入っているデータ
	VDMTESTLOG.TXT	--テスト結果のログ
	
	stdlib	-- VDMToolsの標準ライブラリーが入っているフォルダー

古いバージョンの回帰テストライブラリを使った回帰テストの実行方法
	事前条件
		VDMToolsのインストールが終了していること
	手順
		test.prjファイルをダブルクリック
		静的型チェックを行わなくてもインタープリタによる実行はできるが、静的型チェックをやりたければここで Type Check（メニューかボタンから）する
		インタープリタウィンドウでイニシャライズ
		事前条件などのエラーがあった場合も、テストを続けるようにするオプションを設定する
			set exception
		インタープリタウィンドウで以下のコマンドを実行（--以下は注釈なので、実際にはタイプしない）
			cr a := new AllT()	--テスト用クラスのインスタンスを作成指定 a に代入
			debug a.run()			--オブジェクト a の run 操作をデバッグ実行(デバッグが必要なければ print a.run() で実行することもできる）
			tcov write vdm.tc	--コードカバレージの結果をファイル vdm.tcに書き出す
			rtinfo vdm.tc		--コードカバレージ情報をインタープリタ上で表示する
			
			
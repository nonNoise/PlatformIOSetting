=====================================================================
PratformIOを使ってみよう
=====================================================================

▼　Platform.IOで使えるコマンド
--------------------------------------------------

基本形
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    pio [OPTIONS] COMMAND
    platformio [OPTIONS] COMMAND

    ※コマンドは両方使用することができます。ただ毎回platformioと記述するのが面倒なので、pioで慣れてしまうのがおすすめです。どちらも同じ動きをします。

::

    Options:

        --version          Show the version and exit.
            PlatformIOのバージョン表示

        -f, --force        Force to accept any confirmation prompts.

        -c, --caller TEXT  Caller ID (service).

        -h, --help         Show this message and exit.
            Platformのコマンドの意味などを確認できます。

::

    Commands:

        account   Manage PIO Account
            PlatformIOに登録したアカウントにアクセスしたりできます。

        boards    Embedded Board Explorer
            PlatformIOで開発できるボードを確認できます。

        ci        Continuous Integration
    
        debug     PIO Unified Debugger
        
        device    Monitor device or list existing
            PlatformIOに登録されているデバイスの確認ができる

        init      Initialize PlatformIO project or update existing
            PlatformIOを新規に作成する際の初期化コマンド

        lib       Library Manager

        platform  Platform Manager
            PlatformIOに登録されているプラットフォーム（開発環境）への操作

        remote    PIO Remote

        run       Process project environments
            プロジェクトのmakeや書き込み等一括で行うコマンド

        settings  Manage PlatformIO settings
            PlatformIOの設定の確認や変更ができます。

        test      Local Unit Testing

        update    Update installed platforms, packages and libraries
            Platformやライブラリをアップデートします。

        upgrade   Upgrade PlatformIO to the latest version
            PlatformIO自体のアップグレードができます。


最初の設定
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    pio init --board <ボードID>


ボードIDは以下のコマンドより確認することができます。

::

    pio boards 
        これで全部表示

    pio boards arduino
        Arduinoとして登録されているボード一覧
    
    pio boards mbed
        mbedとして登録されているボード一覧
    
    pio boards stm32
        STM32系列のボード一覧
    
    pio boards > boards.TEXT   
        ボード一覧をテキストに保存

PlatformIO, version 3.4.1(2017/10/28　現在登録されているボードリスト)
    

試しに、ArduinoUno の環境を整えます。ArduinoUnoのボードIDは"uno"となりますので（わかりづら！）

::

    pio init --board uno

するど、フォルダーの中に

::

    platformio.ini - Project Configuration File
        PlatformIOの設定ファイル（主にボードIDやファームウェアなど)

    src - Put your source files here
        プログラムを入れるフォルダ。

    lib - Put here project specific (private) libraries
        ダウンロードしたライブラリなどを入れるフォルダ

が出力されます。

試しにLチカプログラム Blinks を試して見たいと思います。

以下のプログラムを　scrフォルダの中で **main.cpp**　というファイルを作り貼り付けます。

::

    /**
    * Blink
    *
    * Turns on an LED on for one second,
    * then off for one second, repeatedly.
    */
    #include "Arduino.h"

    #ifndef LED_BUILTIN
    #define LED_BUILTIN 13
    #endif

    void setup()
    {
        // initialize LED digital pin as an output.
        pinMode(LED_BUILTIN, OUTPUT);
    }

    void loop()
    {
        // turn the LED on (HIGH is the voltage level)
        digitalWrite(LED_BUILTIN, HIGH);

        // wait for a second
        delay(1000);

        // turn the LED off by making the voltage LOW
        digitalWrite(LED_BUILTIN, LOW);

        // wait for a second
        delay(1000);
    }

コピペとかが面倒な際は、以下のコマンドでダウンロードしてきます。

::

    wget ~

blinksプログラムが整ったら、**run** コマンドでコンパイルをします。

::

    pio run

すると、このタイミングでArudinoUNOに必要な開発環境(主にGCC周りや書き込み用ライブラリ)を自動でダウンロードからインストールまで行います。

この動作が大変、大変便利で気持ちよく開発を行うことができます。真似して行きたい環境セットアップ手法ですね。

開発環境のインストールが行われて無事にコンパイルも行われると、最後に以下のような表示がされるはずです。

::

    AVR Memory Usage
    ----------------
    Device: atmega328p

    Program:     928 bytes (2.8% Full)
    (.text + .data + .bootloader)

    Data:          9 bytes (0.4% Full)
    (.data + .bss + .noinit)

    ========================= [SUCCESS] Took 2.38 seconds =========================

コンパイルまでの時間の確認も面白いですが、肝心な項目は **使用メモリー** の箇所です。
自分が作成したプログラムがマイコンのメモリーをどれくらい消費しているか。
プログラマーは常にマイコンのメモリー空間を意識しながら書いて行くと、大変良いプログラムが出来上がると思います。

▼まとめ
--------------------------------------------

以上の内容でPlatformIOの基本的なコマンとの流れが掴めたかと思います。

大まかにまとめると

::

    pio boards
        これで使いたいボードIDを探す
    pio init --board uno
        これでボードID"uno"を選択して初期化
    scrフォルダにmainソースを書く 
    pio run
        runコマンドでコンパイルを行う。GCC環境とかがなければ自動でインストールする。

こんな感じですかね。

次回以降、それぞれの開発環境に合わせたコマンドや書き込み方法をまとめて行きます。


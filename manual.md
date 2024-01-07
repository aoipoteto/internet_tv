# Step2の手順書

## 前提
- mysql  Ver 8.2.0使用  
- MySQLのインストールは済んでいるものとする。
### 1 .MySQLにログイン  
```
mysql --user=root --password
```
( root=ログインするユーザー名によって変更する)  
→実行後パスワードを入力。  
```
mysql >
```
と表示されたらログイン完了!

### 2 .データベースの構築　
- データベースの作成
```
create database hoboABEMA;
```

- データベースの一覧表示
```
show databases;
```
データベースが作成できているかの確認をする。

- データベースの選択
```
use hoboABEMA;
```  



### 3 . テーブルの設計

- テーブルの設計をmd.で行う。  
  ここですべてのテーブル設計をする。

テーブル：Channel(チャンネル)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|name|varchar(100)|||||  

実行するSQL↓
```
create table step2.channel (id bigint(20), name varchar(100));
```

テーブル：TimeSlots(番組枠)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|channel_id|bigint(20)||FOREIGN||
|start_time|DATETIME|||||
|end_time|DATETIME|||||

実行するSQL↓
```
create table step2.TimeSlots (id bigint(20), channel_id bigint(20), start_time datetime, end_time datetime);
```
　　
テーブル：Viewership(視聴数)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|episode_id|bigint(20)||FOREIGN|||
|channel_id|bigint(20)||FOREIGN|||
|time_slot_id|bigint(20)||FOREIGN|||
|views|BIGINT|||||

実行するSQL↓
```
create table step2.Viewership (id bigint(20), episode_id bigint(20), channel_id bigint(20), time_slot_id bigint(20), views bigint);
```


テーブル：Genres(ジャンル)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|name|varchar(100)|||||

実行するSQL↓
```
create table step2.Genres (id bigint(20), name varchar(100));
Query OK, 0 rows affected (0.03 sec)
```

テーブル：Programs(番組)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|title|varchar(100)|||||
|description|TEXT|||||
|genre_id|varchar(100)||FOREIGN|||

実行するSQL↓
```
create table step2.Programs (id bigint(20), title varchar(100), description text, genre_id varchar(100));
```

テーブル：Season(シーズン)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|program_id|bigint(20)||FOREIGN|||
|season_number|INT|||||
  
実行するSQL↓

```
create table step2.Season (id bigint(20), program_id bigint(20), season_number int)
```


テーブル：Episode(エピソード)


|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|season_id|bigint(20)||FOREIGN|||
|episode_number|INt|||||
|title|varchar(100)|||||
|description|TEXT|||||
|duration|TIME|||||
|release_date|DATE|||||

実行するSQL↓

```
create table step2.Episode (id bigint(20), season_id bigint(20), episode_number int, title varchar(100), description text, duration time, release_date date);
```



- テーブルの一覧表示
```
show tables from データべース名;
```

テーブルが全て入力できているかの確認をする。


### 4 . 各テーブルにサンプルデータを入れる

```
INSERT INTO Channel (id, name) VALUES
    -> (1, 'ニュースチャンネル'),
    -> (2, 'エンタメチャンネル'),
    -> (3, 'スポーツチャンネル'),
    -> (4, '映画チャンネル'),
    -> (5, '音楽チャンネル');
```

```
INSERT INTO TimeSlots (id, channel_id, start_time, end_time) VALUES
    -> (1, 1, '2024-01-07 18:00:00', '2024-01-07 19:00:00'),
    -> (2, 2, '2024-01-07 20:00:00', '2024-01-07 21:30:00'),
    -> (3, 3, '2024-01-07 15:30:00', '2024-01-07 17:00:00'),
    -> (4, 4, '2024-01-07 22:00:00', '2024-01-07 23:30:00'),
    -> (5, 5, '2024-01-07 12:00:00', '2024-01-07 14:00:00');
```
```
INSERT INTO Genres (id, name) VALUES
    -> (1, 'ニュース'),
    -> (2, 'ドラマ'),
    -> (3, 'スポーツ'),
    -> (4, 'アクション'),
    -> (5, '音楽');
```

```
INSERT INTO Programs (id, title, description, genre_id) VALUES
    -> (1, '夕刊ニュース', '日常のニュースアップデート', 1),
    -> (2, 'ドラマシリーズ', '引き込まれるドラマのエピソード', 2),
    -> (3, 'スポーツハイライト', '興奮するスポーツの瞬間', 3),
    -> (4, 'アクションムービーナイト', 'スリリングなアクション映画', 4),
    -> (5, '音楽コンサート', '生の音楽パフォーマンス', 5);
```

```
NSERT INTO Viewership (id, episode_id, channel_id, time_slot_id, views) VALUES
    -> (1, 1, 1, 1, 100000),
    -> (2, 2, 2, 2, 150000),
    -> (3, 3, 3, 3, 80000),
    -> (4, 4, 4, 4, 120000),
    -> (5, 5, 5, 5, 90000);
```

```
INSERT INTO Season (id, program_id, season_number) VALUES
    -> (1, 2, 1),
    -> (2, 4, 3),
    -> (3, 5, 2),
    -> (4, 1, 5),
    -> (5, 3, 1);
```

```
INSERT INTO Episode (id, season_id, episode_number, title, description, duration, release_date) VALUES
    -> (1, 1, 1, 'パイロット', 'ドラマシリーズの紹介', '00:45:00', '2024-01-01'),
    -> (2, 2, 4, '最終対決', 'アクションムービーのクライマックス', '01:30:00', '2024-02-15'),
    -> (3, 3, 2, 'ライブトーナメント', 'スポーツトーナメントのハイライト', '01:15:00', '2024-03-10'),
    -> (4, 4, 7, '特別レポート', '重要なイベントの詳細な報道', '00:50:00', '2024-04-22'),
    -> (5, 5, 3, 'ベストモーメント', '思い出深い音楽パフォーマンスの振り返り', '01:00:00', '2024-05-05');
```

### テーブルの内容確認のSQL

```
select * from Channel;
```

```
+------+-----------------------------+
| id   | name                        |
+------+-----------------------------+
|    1 | ニュースチャンネル          |
|    2 | エンタメチャンネル          |
|    3 | スポーツチャンネル          |
|    4 | 映画チャンネル              |
|    5 | 音楽チャンネル              |
+------+-----------------------------+
```

↑入っているのでOK!


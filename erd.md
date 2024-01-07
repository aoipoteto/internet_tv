テーブル：Channel(チャンネル)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|name|varchar(100)|||||


テーブル：TimeSlots(番組枠)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|channel_id|bigint(20)||FOREIGN||
|start_time|DATETIME|||||
|end_time|DATETIME|||||


テーブル：Viewership(視聴数)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|episode_id|bigint(20)||FOREIGN|||
|channel_id|bigint(20)||FOREIGN|||
|time_slot_id|bigint(20)||FOREIGN|||
|views|BIGINT|||||

テーブル：Genres(ジャンル)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|name|varchar(100)|||||

テーブル：Programs(番組)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|title|varchar(100)|||||
|description|TEXT|||||
|genre_id|varchar(100)||FOREIGN|||

テーブル：Season(シーズン)

|カラム名|データ型|NULL|キー|初期値|AUTO INCREMENT|
| ---- | ---- | ---- | ---- | ---- | ---- |
|id|bigint(20)||PRIMARY||YES|
|program_id|bigint(20)||FOREIGN|||
|season_number|INT|||||


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








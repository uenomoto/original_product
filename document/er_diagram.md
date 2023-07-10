## テーブル定義書

![cost_men](https://github.com/uenomoto/original_product/assets/113354283/8217264d-a6e1-49b7-bc6f-bc7f2a8bae10)


**ユーザーテーブル(users)**

| カラム名              | カラム (英語)   | データ型     | NULL 許容 | キー   | 初期値 | AUTO INCREMENT | 備考                                                        |
| --------------------- | --------------- | ------------ | --------- | ------ | ------ | -------------- | ----------------------------------------------------------- |
| ID                    | id              | integer      | 不可      | 主キー |        | Yes            |                                                             |
| 暗号化パスワード      | password_digest | varchar(255) | 可        |        |        |                | bcrypt で暗号化されたパスワード、LINE ログインの場合は NULL |
| 名前                  | username        | varchar(255) | 不可      |        |        |                |                                                             |
| LINE ログイン用の UID | line_uid        | varchar(255) | 可        |        |        |                | sub フィールドから取得、自作ログインの場合は NULL           |
| プロフィール画像      | profile_picture | varchar(255) | 可        |        |        |                | LINE のプロフィール画像の URL、自作ログインの場合は NULL    |
| 作成日時              | created_at      | timestamp    | 不可      |        |        |                |                                                             |
| 更新日時              | updated_at      | timestamp    | 不可      |        |        |                |                                                             |

**オーストークンテーブルテーブル(auth_tokens)**

| カラム名    | カラム (英語) | データ型     | NULL 許容 | キー     | 初期値 | AUTO INCREMENT | 備考             |
| ----------- | ------------- | ------------ | --------- | -------- | ------ | -------------- | ---------------- |
| ID          | id            | integer      | 不可      | 主キー   |        | Yes            |                  |
| トークン    | token         | varchar(255) | 可        |          |        |                | Auth0 のトークン |
| ユーザー ID | user_id       | varchar(255) | 不可      | 外部キー |        |                |                  |

**レシピテーブル(recipes)**

| カラム名    | カラム (英語) | データ型     | NULL 許容 | キー     | 初期値                       | AUTO INCREMENT |
| ----------- | ------------- | ------------ | --------- | -------- | ---------------------------- | -------------- |
| ID          | id            | bigint       | 不可      | 主キー   |                              | Yes            |
| ユーザー ID | user_id       | bigint       | 不可      | 外部キー |                              |                |
| レシピ名    | name          | varchar(255) | 不可      |          |                              |                |
| 合計原価    | total_cost    | decimal      | 不可      |          |                              |                |
| 手順        | instructions  | text         | 可        |          | レシピの手順はまだありません |                |
| 作成日時    | created_at    | timestamp    | 不可      |          |                              |                |
| 更新日時    | updated_at    | timestamp    | 不可      |          |                              |                |

**原材料テーブル(ingredients)**

| カラム名    | カラム (英語) | データ型     | NULL 許容 | キー     | 初期値 | AUTO INCREMENT |
| ----------- | ------------- | ------------ | --------- | -------- | ------ | -------------- |
| ID          | id            | bigint       | 不可      | 主キー   |        | Yes            |
| 仕入れ先 ID | supplier_id   | bigint       | 不可      | 外部キー |        |                |
| 購入価格    | buy_cost      | decimal      | 不可      |          |        |                |
| 購入数量    | buy_quantity  | float        | 不可      |          |        |
| 単位        | unit          | varchar(255) | 不可      |          |        |                |
| 原材料名    | name          | varchar(255) | 不可      |          |        |                |
| 作成日時    | created_at    | timestamp    | 不可      |          |        |                |
| 更新日時    | updated_at    | timestamp    | 不可      |          |        |                |

**レシピ原材料中間テーブル(recipe_ingredients)**

| カラム名  | カラム (英語) | データ型  | NULL 許容 | キー     | 初期値 | AUTO INCREMENT |
| --------- | ------------- | --------- | --------- | -------- | ------ | -------------- |
| ID        | id            | bigint    | 不可      | 主キー   |        | Yes            |
| レシピ ID | recipe_id     | bigint    | 不可      | 外部キー |        |                |
| 原材料 ID | ingredient_id | bigint    | 不可      | 外部キー |        |                |
| 数量      | quantity      | integer   | 不可      |          |        |                |
| 作成日時  | created_at    | timestamp | 不可      |          |        |                |
| 更新日時  | updated_at    | timestamp | 不可      |          |        |                |

**仕入れ先テーブル(suppliers)**

| カラム名    | カラム (英語) | データ型     | NULL 許容 | キー     | 初期値             | AUTO INCREMENT |
| ----------- | ------------- | ------------ | --------- | -------- | ------------------ | -------------- |
| ID          | id            | bigint       | 不可      | 主キー   |                    | Yes            |
| ユーザー ID | user_id       | bigint       | 不可      | 外部キー |                    |                |
| 名前        | name          | varchar(255) | 不可      |          |                    |                |
| 連絡先情報  | contact_info  | varchar(255) | 可        |          | 連絡先はありません |                |
| 作成日時    | created_at    | timestamp    | 不可      |          |                    |                |
| 更新日時    | updated_at    | timestamp    | 不可      |          |                    |                |

**販売価格テーブル(selling_price)**

| カラム名  | カラム (英語) | データ型  | NULL 許容 | キー     | 初期値 | AUTO INCREMENT |
| --------- | ------------- | --------- | --------- | -------- | ------ | -------------- |
| ID        | id            | bigint    | 不可      | 主キー   |        | Yes            |
| レシピ ID | recipe_id     | bigint    | 不可      | 外部キー |        |                |
| 価格      | price         | decimal   | 不可      |          |        |                |
| 変更日    | changed_date  | date      | 不可      |          |        |                |
| 作成日時  | created_at    | timestamp | 不可      |          |        |                |
| 更新日時  | updated_at    | timestamp | 不可      |          |        |                |

**タグテーブル(tags)**

| カラム名 | カラム (英語) | データ型     | NULL 許容 | キー   | 初期値 | AUTO INCREMENT |
| -------- | ------------- | ------------ | --------- | ------ | ------ | -------------- |
| ID       | id            | bigint       | 不可      | 主キー |        | Yes            |
| 名前     | name          | varchar(255) | 不可      |        |        |                |
| 作成日時 | created_at    | timestamp    | 不可      |        |        |                |
| 更新日時 | updated_at    | timestamp    | 不可      |        |        |                |

**レシピとタグの中間テーブル(recipe_tags)**

| カラム名  | カラム (英語) | データ型  | NULL 許容 | キー     | 初期値 | AUTO INCREMENT |
| --------- | ------------- | --------- | --------- | -------- | ------ | -------------- |
| ID        | id            | bigint    | 不可      | 主キー   |        | Yes            |
| レシピ ID | recipe_id     | bigint    | 不可      | 外部キー |        |                |
| タグ ID   | tag_id        | bigint    | 不可      | 外部キー |        |                |
| 作成日時  | created_at    | timestamp | 不可      |          |        |                |
| 更新日時  | updated_at    | timestamp | 不可      |          |        |                |

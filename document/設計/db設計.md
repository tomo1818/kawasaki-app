## 1. テーブル一覧

### 1.1. ユーザーテーブル
```mermaid
erDiagram
Users {
  user_id index   PK "ユーザーの一意の識別子"
  username string "ユーザー名"
  password string "パスワード（ハッシュ化）"
  email    string "メールアドレス"
  profile_picture string "プロフィール画像のurl"
  room_number int "部屋番号"
  authority int "権限(0: ユーザー, 1: 管理者)"
  timestamp TIMESTAMP "ユーザーのタイムスタンプ"
}
```

### 1.2. メッセージテーブル
```mermaid
erDiagram
Messages {
  message_id index PK "メッセージの一意の識別子"
  sender_id index FK "送信者のユーザーID（外部キー参照）"
  receiver_id index FK "受信者のユーザーID（外部キー参照)"
  group_id index FK "グループID（外部キー参照）"
  content VARCHAR "メッセージの本文"
  timestamp TIMESTAMP "メッセージのタイムスタンプ"
}
```

### 1.3. グループテーブル
```mermaid
erDiagram
Groups {
  message_id index PK "グループの一意の識別子"
  group_name VARCHAR(50) "グループの名前"
  created_by index FK "グループを作成したユーザー"
  timestamp TIMESTAMP "グループのタイムスタンプ"
}
```

### 1.4. ロケーションテーブル
```mermaid
erDiagram
Locations {
  location_id index PK "位置情報の一意の識別子"
  user_id index FK "ユーザーの一意の識別子（外部キー参照）"
  latitude DECIMAL "緯度"
  longitude DECIMAL "経度"
  timestamp TIMESTAMP "位置情報のタイムスタンプ"
}
```

### 1.5. ユーザーメッセージテーブル
```mermaid
erDiagram
UserMessages {
  user_message_id index PK "ユーザーメッセージの一意の識別子"
  user_id index FK "ユーザーの一意の識別子（外部キー参照）"
  message_id index FK "メッセージの一意の識別子（外部キー参照）"
  timestamp TIMESTAMP "ユーザーメッセージのタイムスタンプ"
}
```

### 1.6. ユーザーグループテーブル
```mermaid
erDiagram
UserGroups {
  user_group_id index PK "ユーザーグループの一意の識別子"
  user_id index FK "ユーザーの一意の識別子（外部キー参照）"
  group_id index FK "グループの一意の識別子（外部キー参照）"
  timestamp TIMESTAMP "ユーザーグループのタイムスタンプ"
}
```

### 1.7. メッセージグループテーブル
```mermaid
erDiagram
MessageGroups {
  message_group_id index PK "メッセージグループの一意の識別子"
  message_id index FK "メッセージの一意の識別子（外部キー参照）"
  group_id index FK "グループの一意の識別子（外部キー参照）"
  timestamp TIMESTAMP "メッセージグループのタイムスタンプ"
}
```

### 1.8. 食事予約テーブル
```mermaid
erDiagram
MealReservations {
  reservation_id index PK "食事予約の一意の識別子"
  user_id index FK "ユーザーの一意の識別子"
  meal_date DATE "食事予約の日付"
  breakfast boolean "朝食の予約の有無"
  dinner boolean "夕食の予約の有無"
  timestamp TIMESTAMP "食事予約のタイムスタンプ"
}
```

## 2. ER図

```mermaid
erDiagram
  Users ||--|{ Locations: ""
  Users ||--o{ UserMessages: ""
  Users ||--o{ UserGroups: ""
  Users ||--|{ MealReservations: ""
  Messages ||--o{ MessageGroups: ""
  Messages ||--o{ UserMessages: ""
  Groups ||--o{ MessageGroups: ""
  Groups ||--o{ UserGroups: ""

  Users {
    user_id  index   PK "ユーザーの一意の識別子"
    username string "ユーザー名"
    password string "パスワード（ハッシュ化）"
    email    string "メールアドレス"
    profile_picture string "プロフィール画像のurl"
    room_number int "部屋番号"
    authority int "権限(0: ユーザー, 1: 管理者)"
    timestamp TIMESTAMP "ユーザーのタイムスタンプ"
  }

  Messages {
    message_id index PK "メッセージの一意の識別子"
    sender_id  index FK "送信者のユーザーID（外部キー参照）"
    receiver_id index FK "受信者のユーザーID（外部キー参照)"
    group_id   index FK "グループID（外部キー参照）"
    content    VARCHAR "メッセージの本文"
    timestamp TIMESTAMP "メッセージのタイムスタンプ"
  }

  Groups {
    group_id   index PK "グループの一意の識別子"
    group_name VARCHAR(50) "グループの名前"
    created_by index FK "グループを作成したユーザー"
    timestamp TIMESTAMP "グループのタイムスタンプ"
  }

  Locations {
    location_id index PK "位置情報の一意の識別子"
    user_id     index FK "ユーザーの一意の識別子（外部キー参照）"
    latitude    DECIMAL "緯度"
    longitude   DECIMAL "経度"
    timestamp   TIMESTAMP "位置情報のタイムスタンプ"
  }

  MealReservations {
    reservation_id index PK "食事予約の一意の識別子"
    user_id index FK "ユーザーの一意の識別子"
    meal_date DATE "食事予約の日付"
    breakfast boolean "朝食の予約の有無"
    dinner boolean "夕食の予約の有無"
    timestamp TIMESTAMP "食事予約のタイムスタンプ"
  }

  UserMessages {
    user_message_id index PK "ユーザーメッセージの一意の識別子"
    user_id        index FK "ユーザーの一意の識別子（外部キー参照）"
    message_id     index FK "メッセージの一意の識別子（外部キー参照）"
    timestamp      TIMESTAMP "ユーザーメッセージのタイムスタンプ"
  }

  UserGroups {
    user_group_id index PK "ユーザーグループの一意の識別子"
    user_id       index FK "ユーザーの一意の識別子（外部キー参照）"
    group_id      index FK "グループの一意の識別子（外部キー参照）"
    timestamp     TIMESTAMP "ユーザーグループのタイムスタンプ"
  }

  MessageGroups {
    message_group_id index PK "メッセージグループの一意の識別子"
    message_id      index FK "メッセージの一意の識別子（外部キー参照）"
    group_id        index FK "グループの一意の識別子（外部キー参照）"
    timestamp       TIMESTAMP "メッセージグループのタイムスタンプ"
  }
```
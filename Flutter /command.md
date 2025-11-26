# 使用したコマンド

### ■ 開発中に、アプリを Chromeブラウザ上で起動して動作確認するコマンド。
`-d` はデバイス（Device）を指定するオプション。  
ホットリロード・デバッグログを利用しながら開発できる。

```text
flutter run -d chrome
```

### ■ Flutter Web アプリを本番デプロイ用にビルドするコマンド
build/web/ フォルダに静的ファイル（index.html / main.dart.js など）が生成される。

```text
flutter build web
```

##### ■ flutter: The Flutter command-line tool

##### https://docs.flutter.dev/reference/flutter-cli

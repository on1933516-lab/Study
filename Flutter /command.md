# 使用したコマンド

### ■ 開発中に、アプリを Chromeブラウザ上で起動して動作確認するコマンド。
`-d` はデバイス（Device）を指定するオプション。  
ホットリロード・デバッグログを利用しながら開発できる。

```text
flutter run -d chrome
```

・その他デバイス指定オプション
| オプション          | 意味                                         |
|---------------------|----------------------------------------------|
| `-d chrome`         | Chrome で起動して動作確認する                |
| `-d web-server`     | シンプルな Web サーバで起動（Chrome 自動起動なし） |
| `--release`         | 本番ビルドに近い動作（デバッグ機能なし）     |
| `--verbose`         | 詳細ログを出力（デバッグ時に使用）           |



### ■ Flutter Web アプリを本番デプロイ用にビルドするコマンド
build/web/ フォルダに静的ファイル（index.html / main.dart.js など）が生成される。

```text
flutter build web
```

##### ■ flutter: The Flutter command-line tool

##### https://docs.flutter.dev/reference/flutter-cli

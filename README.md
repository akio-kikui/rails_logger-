## やりたかったこと

Railsのerror level以上を標準エラー出力にしたかった

## 何故か？

Google App Engineでエラー検知を飛ばしたかったから

## 試行錯誤

- Rails.logger の仕様上 複数のIOを設定出来なさそ
- カスタマイズした logger作れば行けそうだけど、Rails.logger.error とかの実装を変えたくなかった
- broadcastまでたどり着いた後 loglevelの設定がconfigの中だと書き換えられるので、 config/initializersに配置するしかなかった
- dockerでSTDERR取れないので諦めた
- 標準出力側でError出したくなかったけど　そんなオプションはなさそう（info 出すけど error出さないとかありえ無い) 諦めた

## 確認方法


```
$docker-compose run web bash
$rails s 1>/dev/null

------- 結果 --------
error!!!
```

## 動いたコード

- config/initializers/add_error_logger.rb
- config/initializers/logger_test.rb

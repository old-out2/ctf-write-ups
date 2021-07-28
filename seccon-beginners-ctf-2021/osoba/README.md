# osoba

## write-up
「フラグはサーバの /flag にあります」と書いてあるので、以下サーバ内にある/flagを探す

urlの形が'?page='の形で表される  
配布資料のディレクトリ構造とURLを見比べると`public`ディレクトリからhtmlを取得しているのが分かる  
ディレクトリ指定の形を使って、親階層にある/flagを見つける

```
?page=../flag
```


<details><summary>flag</summary><div>
ctf4b{omisoshiru_oishi_keredomo_tsukuruno_taihen}
</div></details>

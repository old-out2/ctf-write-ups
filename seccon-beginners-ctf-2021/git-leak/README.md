# git-leak

## Write-up
コミットを上書きしたが情報は残っているので

```
git reflog
```

で履歴情報を見ると7387982に上書き処理があるので

```
git checkout 7387982
```

flag.txtが出てくる

## Flag
ctf4b{0verwr1te_1s_n0t_c0mplete_1n_G1t}

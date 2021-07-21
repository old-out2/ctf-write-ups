# c(heck)_url

phpのコードを読むと127.0.0.1を$url=に書ければよいが
if文によって.が👻に代わってしまう。
localhostやapacheにも対策がされているので127.0.0.1の別表記を探すという思考にならないと解けない

探すと16進数で0x7F000001と表記されることが分かった

[127.0.0.1(localhost)を一番面白く表記できた奴が優勝](https://qiita.com/naka_kyon/items/88478be20b300e757fc0)

<details><summary>flag</summary><div>
ctf4b{5555rf_15_53rv3r_51d3_5up3r_54n171z3d_r3qu357_f0r63ry}
</div></details>

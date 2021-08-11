challをredare2で確認しながらpythonのコードを書く
cmpが何回も行われているのでそれを抽出すればよい

<details><summary>回答コード一覧</summary><div>
    
```python
import angr

def solve():
    #ファイルを読み込む
    p = angr.Project('./chall')

    #プログラムの初期状態を保存
    state = p.factory.entry_state()

    #実行状態を最初から管理する
    sim = p.factory.simulation_manager(state)

    #find条件に合致するまで実行を進めて見つけたら止まる
    #0x400000はデフォルトのベースアドレス
    #0x012b8はflagが完成したアドレス
    sim.explore(find=0x400000 + 0x012b8)

    for found in sim.found: #型を合わすために行う
        return found.posix.dumps(0).decode() #sim.foundの一つ目の中身の文字列を返す

if __name__ == '__main__':
    print(solve())
```
<div>
</details>
    
<details><summary>flag</summary><div>
ctf4b{c0n5t4nt_f0ld1ng}
</div></details>

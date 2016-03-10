通常要 revert 一個 commit 時，我們會直接下
```bash
git revert xxxxxxx
```
這樣一來會產生一個新的 commit，把之前做過的改動改回去

不過若你想要 revert 一個 merge，事情就沒有這麼單純了
因為 git 不知道你要 revert 哪一個 branch，所以它會報錯不給 merge

我們必須用
```bash
git revert xxxxxxx -m 1
```
指定 branch 它才會讓你 revert

值得注意的是你要 revert 一個 merge，必須指定 merge 之後的 commit，舉例來說
```bash
* feeec56 Revert "Merge pull request #8 from cjhuang/ycb"
*   95707ca Merge pull request #9 from cjhuang/fix_trunk
|\
| * 7e86ba4 zxcv
|/
* 6013e0f Update version to 1.0.6 by screwdriver:93632:component:node10:8
* 862775c Update version to 1.0.5 by screwdriver:93632:component:node10:7
*   217b939 Merge pull request #8 from cjhuang/ycb
|\
| * c56ef71 foo
| * 70ea922 bar
| * c407515 baz
| * e3b0779 qwer
| * 13c2c14 asdf
* | 42bbf16 Update version to 1.0.4 by screwdriver:93632:component:node10:6
* | 32dea4d Update version to 1.0.3 by screwdriver:93632:component:node10:5
|/
*   aaa42f5 Merge pull request #7 from cjhuang/live_video
```

`feeec56` revert 了 cjhuang/ycb 這個 merge，但它其實是下
```bash
git revert 217b939 -m 1
```
得來的

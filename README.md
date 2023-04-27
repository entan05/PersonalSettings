# 個人的な設定集
個人的な設定の内、公開できるものをつらつらと...

---

## ブラウザ - [Chrome](https://www.google.com/intl/ja_jp/chrome/)
特にGoogleに対し嫌悪感を持っていないので
### 拡張機能
#### [New Tab Redirect](https://chrome.google.com/webstore/detail/new-tab-redirect/icpgjfneehieebagbmdbhnlpiopdcmna)
新しいタブを開く際、指定したページにリダイレクトしてくれる<br>
指定先はGoogle( `https://www.google.com/` )<br>
(「新しいタブ」はショートカットが表示されるのが嫌いなのと、ネットワークに繋がっているか確認するのにタブ開くだけで済むので)

#### [テキストエンコーディング](https://chrome.google.com/webstore/detail/set-character-encoding/bpojelgakakmcfmjfilgdlmhefphglae)
ページのテキストエンコーディングを指定することができる<br>
ごくごく稀に文字化けすることがなくもないので<br>
(今時珍しいっちゃ珍しいが)

#### [uBlacklist](https://chrome.google.com/webstore/detail/ublacklist/pncfbmialoiaghdehhbnbhkkgmjanfhe/)
検索結果から指定のサイトを非表示にする<br>
ブラックリストは以下を購読
https://raw.githubusercontent.com/entan05/PersonalSettings/main/uBlacklist/uBlacklist.txt

#### [Talend API Tester - Free Edition](https://chrome.google.com/webstore/detail/talend-api-tester-free-ed/aejoelaoggembcahagimdiliamlcdmfm)
Postmanみたいなもの<br>
この手のものは入れても持て余すものの、必要な時があったりするので

## スクリプト
### Androidスクショ取得
```Shell
#!/bin/zsh

file=""
if test $# -gt 0 ; then
  file=$1
else
  file="screen.png"
fi

if [ -e $file ]; then
  printf '\a❗️ 既に存在します\n'
  return 0
fi

adb shell screencap -p /sdcard/screen.png
adb pull /sdcard/screen.png $file
adb shell rm /sdcard/screen.png
```
※ 前提条件: `adb` にパスが通っている<br>

`adb_cap.sh` のような名前で保存する<br>
複数台繋がっていると動かないので注意

## .zshrc
```
PROMPT='%F{magenta}%n: %~ %(!.#.$) %f'
export LSCOLORS=gxfxcxdxbxegedabagacad

alias ls='ls -GF'
alias rm='rm -i'
alias xgrep='grep ./ -rnwI -e'
alias ql='qlmanage -p "$@" >& /dev/null'

alias adb_cap='<Androidスクショ取得スクリプトのパス>'

# 以下パス設定
```
基本的にaliasは設定しない<br>
(そうそう機会はないが他人のPCとか触る際にオプションつけ忘れとかしないように)<br>
それでも入れているのは<br>
`ls`: ディレクトリ/ファイルの区別&色分け<br>
`rm`: 削除時の確認<br>
`xgrep`: オプション付きgrep<br>
`ql`: クイックルック(mac)<br>
と自作スクリプト


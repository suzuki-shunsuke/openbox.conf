# openbox.conf

https://wiki.archlinuxjp.org/index.php/Openbox

```
$ sudo pacman -Syu
$ sudo pacman -S openbox
```

```
$ git clone git@github.com:suzuki-shunsuke/openbox.conf.git ~/.config/openbox
$ openbox --reconfigure
```

* キーボード・ショートカットの設定
* 自動起動するアプリケーションの設定
  * tint2

## alsa-utilsをインストールしているが音声が出ない場合


参考: http://qiita.com/xorphitus/items/3711895eb5d9f946c782

```
$ aplay -l
```

でカードとデバイスの番号を調べる。

```
$ aplay -D plughw:{card_id},{device_id} /usr/share/sounds/alsa/Front_Center.wav
```

で音が出れば正しい番号。
音の出るcar\_id、device\_idを特定できたら、
~/.asoundrcに以下を記述する。

```
pcm.!default {
  type hw
  card {card_id}
  device {device_id}
}
```

音量ボタンで音量を調節できるように rc.xmlで設定しているが、
正しいカードIDを指定するように修正する。


```xml
<keybind key="XF86AudioRaiseVolume">
  <action name="Execute">
    <command>amixer -c 1 set Master 5%+ unmute</command>
  </action>
</keybind>
```

## 미디어 옵션 변경하기
VlcMedia 클래스의 메소드 중에 setOption 함수를 이용하면 vlc 를 실행할 때 명령에 옵션을 주듯이, 설정을 조정할 수 있다

### 네트워크 캐싱 수정하기
[VLC command line](https://wiki.videolan.org/VLC_command-line_help/) 을 참조하면, `--live-caching=<integer [0 .. 60000]>` 이라는 옵션을 찾을 수 있다. 

기본값은 1000 인데, 실제 rtsp로 접속하면, 1초 간의 버퍼링을 하게 되므로 지연이 발생한다. 이것을 100 으로 변경해서 실행한다.

simple-player 예제 소스에서, `SimplePlayer.cpp`를 수정한다.

```cpp
void SimplePlayer::openUrl()
{
    QString url =
            QInputDialog::getText(this, tr("Open Url"), tr("Enter the URL you want to play"));

    if (url.isEmpty())
        return;

    _media = new VlcMedia(url, _instance);
    // 옵션을 조정한다.
    _media->setOption(":network-caching=100");

    _player->open(_media);
}

```
명령으로 넘길 때는 `--live-caching=100` 과 같이 하지만, 옵션으로 설정할 때는 `--` 대신 `:` 을 이용한다. 즉, `:network-caching=100` 과 같이 된다.

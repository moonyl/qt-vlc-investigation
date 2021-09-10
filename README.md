# qt-vlc-investigation
qt-vlc 에 대해 조사한 내용을 정리한다.

## libvlc 다운로드
[VLC 홈페이지](https://www.videolan.org/vlc/index.ko.html) 에 들어가봤자 player 설치 프로그램 다운로드 링크만 있고, vlc 개발을 위한 환경을 받을 수 있는 위치는 찾을 수 없다.

윈도우의 경우에는 인스톨 프로그램을 받으면 안 되고, 7z으로 묶여있는 파일을 받아야 한다. 

[VLC 아카이브](http://download.videolan.org/pub/videolan/vlc/) 에서 적당한 버전이 있는 디렉토리로 접근해서 7Z로 압축되어 있는 파일을 하나 다운로드 받는다. 

win64용 최신 버전을 받으려면 [last version](http://download.videolan.org/pub/videolan/vlc/last/win64/)을 접근해서 다운로드 받는다.

다운로드 받은 파일을 적당한 위치에 압축해제 한다. 여기에서는 d:\ref-libs 에 압축해제 했다고 가정한다. 이 경우에 중요한 파일의 위치는 다음과 같다.
* libvlc: D:/ref-libs/vlc-3.0.16/sdk/lib/libvlc.lib
* libvlccore: D:/ref-libs/vlc-3.0.16/sdk/lib/libvlccore.lib
* include 디렉토리: D:/ref-libs/vlc-3.0.16/sdk/include

## qt-vlc 클론하기
적당한 위치에 qt-vlc 를 클론한다. 여기에서는 d:\pilot 위치에서 작업한다.
```cmd
git clone https://github.com/vlc-qt/vlc-qt.git
```

## qt-vlc 빌드하기
qt-vlc를 빌드하기 위해서는 당연히 Qt 개발 환경이 준비되어 있어야 한다.

빌드툴은 visual studio 2017 이 설치되어 있다고 가정한다. 

d:\pilot\vlc-qt 위치에서 build 디렉토리를 생성한 후, build로 진입한다.
```cmd
md build
cd build
```
앞서, 기록한 중요 파일 위치를 참조하여, cmake 를 실행한다.
```cmd
cmake .. -G"Visual Studio 15 2017 Win64" -DCMAKE_BUILD_TYPE=Debug ^
  -DCMAKE_INSTALL_PREFIX="D:/ref-libs/vlc-qt/msvc64" ^
  -DLIBVLC_LIBRARY="D:/ref-libs/vlc-3.0.16/sdk/lib/libvlc.lib" ^
  -DLIBVLCCORE_LIBRARY="D:/ref-libs/vlc-3.0.16/sdk/lib/libvlccore.lib" ^
  -DLIBVLC_INCLUDE_DIR="D:/ref-libs/vlc-3.0.16/sdk/include" ^
  -DCMAKE_PREFIX_PATH="C:/Qt/Qt5.12.7/5.12.7/msvc2017_64"
```
`CMAKE_INSTALL_PREFIX`로 설정한 값은 qt-vlc 를 빌드한 결과물을 최종적으로 설치할 위치이다.

`CMAKE_PREFIX_PATH` 로 설정한 값은 Qt 개발환경이 설치되어 있는 위치이다.

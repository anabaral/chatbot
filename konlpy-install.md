# konlpy 설치해 보기

## Windows 에 설치

### 회사 PC 에 설치 (포기)

이 글을 쓰는 현재 포기상태 (2020-12-11)

참조한 것들:
- https://daewonyoon.tistory.com/200
- https://sdkim817.wordpress.com/2020/01/30/konlpy-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%9D%B4%EC%9A%A9/
- 등등

한 것들은 다음과 같으며, 순서대로 하지는 않았다가 이러저러한 일을 겪은 후 다시 순서대로 진행
- jdk 는 설치되어 있었음. jdk-9 (openjdk)  -- konlpy 패키지가 jdk에 의존함
- python 설치 3.9.1 x64
- JAVA_HOME 환경변수 설정, Path 환경변수 확인
- pip3 install –upgrade pip
- JPype 설치) 두 가지 방법이 있는데, 
  * pip3 install jpype1 명령으로 설치하는 방법과
  * pip3 install JPype1-1.2.0-cp39-cp39-win_amd64.whl 다운받은 파일을 지정해서 설치하는 방법
  * 전자는 Visual C++ Redistributable 어쩌구를 2015 버전부터 설치해야 함  
    - https://visualstudio.microsoft.com/ko/vs/older-downloads/ 에서 Microsoft Build Tools 2015 업데이트 3 다운받아 설치  
      ...만 하지 않고 이것저것 x86 x64 다 설치함. 그러면 최소한 설치 시점 에러는 안남
- pip3 install konlpy

그러나 이렇게 해 봐야 결국 다음 에러를 만남
```
>>> from konlpy.tag import Kkma
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "C:\Users\Administrator\AppData\Local\Programs\Python\Python39-32\lib\site-packages\konlpy\__init__.py", line 12, in <module>
    from konlpy import (
  File "C:\Users\Administrator\AppData\Local\Programs\Python\Python39-32\lib\site-packages\konlpy\tag\__init__.py", line 6, in <module>
    from konlpy.tag._hannanum import Hannanum
  File "C:\Users\Administrator\AppData\Local\Programs\Python\Python39-32\lib\site-packages\konlpy\tag\_hannanum.py", line 7, in <module>
    import jpype
  File "C:\Users\Administrator\AppData\Local\Programs\Python\Python39-32\lib\site-packages\jpype\__init__.py", line 18, in <module>
    import _jpype
ImportError: DLL load failed while importing _jpype: DLL 초기화 루틴을 실행할 수 없습니다.
>>>
```

검색해 보면 분명히 Visual Studio C++ Redistributable 설치와 관련 있을 것 같은데 아무튼 안됨.  
어쩌면 3.8에서는 될 지도 모르나.. 지쳐서 포기. (위에 간략하게 적었지만 하루종일 이것저것 다 해 봄)

그런데 아래처럼 집 PC에서는 잘 되는 것 같으니 같은 방식으로 다시 시도해 봐야겠다..

### 집 PC에 설치 (성공)

집에서의 환경은 회사 PC에서와 조금 다름. 조금 정리해 보자면
- 일단 회사 보안 프로그램 같은 것들이 덕지덕지 깔려있지 않음 (만세!)
- JDK를 open jdk가 아닌 Oracle JDK 를 사용하고 있음
- python 을 예전부터 써 왔기에 옛 버전들이 깔려 있었고, 최근에 추가로 python 3.9.1 을 설치 (python2 는 아예 없음)

뭐 어쨌든 시도를 해 보는데 일단 pip가 안되네... 캡처를 안해서 남아있는 게 없지만 다음 명령들이 모두 'pip 모듈이 없습니다' 에러를 낸다.
```
> python get-pip.py # 정상설치 되었는데도
> pip install konlpy
> pip
> python -m pip
```

조금 고민해 봤는데 다음이 문제였는지도 모른다고 생각해서
- pycharm , Anaconda 들이 깔려 있는 PC에다
- python 3.9.1 을 embedded 모드로 (standalone 설치) 깔아버리고 PATH만 연결한 상태

pycharm , anaconda , python 3.9.1 까지 모두 지우고 회사 PC때에도 마음에 걸렸던 python 3.9.1 까지 깨끗하게 지움.  
그리고 python 3.8.6 을 installer 로 설치.

그러니 모든 게 순탄하고 pip도 실행 잘 되는가 싶은데
```

>pip install konlpy
    ERROR: Command errored out with exit status 1:
     command: 'c:\users\rindon\appdata\local\programs\python\python38-32\python.exe' -u -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'C:\\Users\\rindon\\AppData\\Local\\Temp\\pip-install-b59agya8\\jpype1\\setup.py'"'"'; __file__='"'"'C:\\Users\\rindon\\AppData\\Local\\Temp\\pip-install-b59agya8\\jpype1\\setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' install --record 'C:\Users\rindon\AppData\Local\Temp\pip-record-pq2h6dbc\install-record.txt' --single-version-externally-managed --compile --install-headers 'c:\users\rindon\appdata\local\programs\python\python38-32\Include\JPype1'
         cwd: C:\Users\rindon\AppData\Local\Temp\pip-install-b59agya8\jpype1\
    Complete output (48 lines):
    Falling back to provided JNI headers, since your provided JAVA_HOME "C:\java\jdk11.0.3" does not provide jni.h
    Falling back to provided JNI headers, since your provided JAVA_HOME "C:\java\jdk11.0.3" does not provide jni.h
    Falling back to provided JNI headers, since your provided JAVA_HOME "C:\java\jdk11.0.3" does not provide jni.h
    running install
    running build
    running build_py
    creating build
    creating build\lib.win32-3.8
    creating build\lib.win32-3.8\jpype
    copying jpype\beans.py -> build\lib.win32-3.8\jpype
    copying jpype\dbapi2.py -> build\lib.win32-3.8\jpype
    copying jpype\imports.py -> build\lib.win32-3.8\jpype
    copying jpype\nio.py -> build\lib.win32-3.8\jpype
    copying jpype\pickle.py -> build\lib.win32-3.8\jpype
    copying jpype\protocol.py -> build\lib.win32-3.8\jpype
    copying jpype\types.py -> build\lib.win32-3.8\jpype
    copying jpype\_classpath.py -> build\lib.win32-3.8\jpype
    copying jpype\_core.py -> build\lib.win32-3.8\jpype
    copying jpype\_gui.py -> build\lib.win32-3.8\jpype
    copying jpype\_jarray.py -> build\lib.win32-3.8\jpype
    copying jpype\_jclass.py -> build\lib.win32-3.8\jpype
    copying jpype\_jcollection.py -> build\lib.win32-3.8\jpype
    copying jpype\_jcustomizer.py -> build\lib.win32-3.8\jpype
    copying jpype\_jexception.py -> build\lib.win32-3.8\jpype
    copying jpype\_jinit.py -> build\lib.win32-3.8\jpype
    copying jpype\_jio.py -> build\lib.win32-3.8\jpype
    copying jpype\_jmethod.py -> build\lib.win32-3.8\jpype
    copying jpype\_jobject.py -> build\lib.win32-3.8\jpype
    copying jpype\_jpackage.py -> build\lib.win32-3.8\jpype
    copying jpype\_jproxy.py -> build\lib.win32-3.8\jpype
    copying jpype\_jstring.py -> build\lib.win32-3.8\jpype
    copying jpype\_jthread.py -> build\lib.win32-3.8\jpype
    copying jpype\_jvmfinder.py -> build\lib.win32-3.8\jpype
    copying jpype\_pykeywords.py -> build\lib.win32-3.8\jpype
    copying jpype\__init__.py -> build\lib.win32-3.8\jpype
    package init file 'jpype\_pyinstaller\__init__.py' not found (or not a regular file)
    creating build\lib.win32-3.8\jpype\_pyinstaller
    copying jpype\_pyinstaller\entry_points.py -> build\lib.win32-3.8\jpype\_pyinstaller
    copying jpype\_pyinstaller\example.py -> build\lib.win32-3.8\jpype\_pyinstaller
    copying jpype\_pyinstaller\hook-jpype.py -> build\lib.win32-3.8\jpype\_pyinstaller
    copying jpype\_pyinstaller\test_jpype_pyinstaller.py -> build\lib.win32-3.8\jpype\_pyinstaller
    running build_ext
    Call build extensions
    Using Jar cache
    copying native\jars\org.jpype.jar -> build\lib.win32-3.8
    Call build ext
    building '_jpype' extension
    error: Microsoft Visual C++ 14.0 is required. Get it with "Build Tools for Visual Studio": https://visualstudio.microsoft.com/downloads/
    ----------------------------------------
ERROR: Command errored out with exit status 1: 'c:\users\rindon\appdata\local\programs\python\python38-32\python.exe' -u -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'C:\\Users\\rindon\\AppData\\Local\\Temp\\pip-install-b59agya8\\jpype1\\setup.py'"'"'; __file__='"'"'C:\\Users\\rindon\\AppData\\Local\\Temp\\pip-install-b59agya8\\jpype1\\setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' install --record 'C:\Users\rindon\AppData\Local\Temp\pip-record-pq2h6dbc\install-record.txt' --single-version-externally-managed --compile --install-headers 'c:\users\rindon\appdata\local\programs\python\python38-32\Include\JPype1' Check the logs for full command output.
WARNING: You are using pip version 20.2.1; however, version 20.3.1 is available.
You should consider upgrading via the 'c:\users\rindon\appdata\local\programs\python\python38-32\python.exe -m pip install --upgrade pip' command.
```

... 사실 이 에러는 회사 PC에 설치할 때도 계속 만났던 에러이고, 이를 해결하기 위해 https://visualstudio.microsoft.com/downloads/ 
에 들어가서 정확히 "Build Tools for Visual Studio" 으로 검색을 해 보니 하나 딱 튀어나오는 게 있어서 다운로드 함.
- https://visualstudio.microsoft.com/ko/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16
- 실행하면 여러 파일들을 가져와 설치함
- 화면이 나와 선택하게 함.
  . Visual C++ 빌드 도구 선택하고
  . 설치 세부 정보에서 MSVC v140 - VS 2015 C++ 빌드 도구(v14.00) 를 추가선택
  . 10기가나 필요하다고..? 배보다 배꼽이 더 크네

암튼 설치 끝내고 재부팅하고 다시설치 시도해 보니 잘 된다.
```
>pip install konlpy
Collecting konlpy
  Using cached konlpy-0.5.2-py2.py3-none-any.whl (19.4 MB)
Collecting lxml>=4.1.0
  Using cached lxml-4.6.2-cp38-cp38-win32.whl (3.2 MB)
Collecting tweepy>=3.7.0
  Using cached tweepy-3.9.0-py2.py3-none-any.whl (30 kB)
Collecting beautifulsoup4==4.6.0
  Using cached beautifulsoup4-4.6.0-py3-none-any.whl (86 kB)
Collecting JPype1>=0.7.0
  Using cached JPype1-1.2.0.tar.gz (1.2 MB)
Requirement already satisfied: numpy>=1.6 in c:\users\rindon\appdata\local\programs\python\python38-32\lib\site-packages (from konlpy) (1.19.4)
Collecting colorama
  Using cached colorama-0.4.4-py2.py3-none-any.whl (16 kB)
Collecting requests[socks]>=2.11.1
  Using cached requests-2.25.0-py2.py3-none-any.whl (61 kB)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.0-py2.py3-none-any.whl (23 kB)
Requirement already satisfied: six>=1.10.0 in c:\users\rindon\appdata\local\programs\python\python38-32\lib\site-packages (from tweepy>=3.7.0->konlpy) (1.15.0)
Collecting idna<3,>=2.5
  Using cached idna-2.10-py2.py3-none-any.whl (58 kB)
Collecting urllib3<1.27,>=1.21.1
  Using cached urllib3-1.26.2-py2.py3-none-any.whl (136 kB)
Collecting chardet<4,>=3.0.2
  Using cached chardet-3.0.4-py2.py3-none-any.whl (133 kB)
Collecting certifi>=2017.4.17
  Using cached certifi-2020.12.5-py2.py3-none-any.whl (147 kB)
Collecting PySocks!=1.5.7,>=1.5.6; extra == "socks"
  Using cached PySocks-1.7.1-py3-none-any.whl (16 kB)
Collecting oauthlib>=3.0.0
  Using cached oauthlib-3.1.0-py2.py3-none-any.whl (147 kB)
Using legacy 'setup.py install' for JPype1, since package 'wheel' is not installed.
Installing collected packages: lxml, idna, urllib3, chardet, certifi, PySocks, requests, oauthlib, requests-oauthlib, tweepy, beautifulsoup4, JPype1, colorama, konlpy
    Running setup.py install for JPype1 ... done
Successfully installed JPype1-1.2.0 PySocks-1.7.1 beautifulsoup4-4.6.0 certifi-2020.12.5 chardet-3.0.4 colorama-0.4.4 idna-2.10 konlpy-0.5.2 lxml-4.6.2 oauthlib-3.1.0 requests-2.25.0 requests-oauthlib-1.3.0 tweepy-3.9.0 urllib3-1.26.2
WARNING: You are using pip version 20.2.1; however, version 20.3.1 is available.
You should consider upgrading via the 'c:\users\rindon\appdata\local\programs\python\python38-32\python.exe -m pip install --upgrade pip' command.
```

실행도 잘 되고.
```
> python
Python 3.8.6 (tags/v3.8.6:db45529, Sep 23 2020, 15:37:30) [MSC v.1927 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from konlpy.tag import Kkma
>>> kkma = Kkma()
```

그러나 좀 있다 확인해 본 결과, 내가 python 3.8.6 32-bit 버전을 설치했었다.  
konlpy는 상관 없지만 뒤에 내가 해야 할 tensorflow는 64-bit 버전을 요구한다...

자, 제 2라운드..

- 기존의 python 3.8.6 32-bit 제거
- python 3.8.6 64-bit 설치
- pip install konlpy 설치
- import 및 인스턴스 선언까지 성공!

거기에 더해서
```
>pip install tensorflow
```
이것도 성공.  
휴~

## Linux(Ubuntu)에서 설치

python이 3.6이 설치된 상태라서 따로 3.8을 설치하였음
```
$ sudo apt install openjdk-11-jdk
$ sudo apt install python3.8
$ sudo apt install python3.8-pip
```

링크를 바꿔주지 않으면 python3 실행하면 python3.6이 실행되므로 pip3 도 python3.6 기준으로 설치할 것임. 
```
$ cd /usr/bin
$ sudo ln -fs python3.8 /usr/bin/python3
```

konlpy 설치
```
$ pip3 install konlpy
```

시험 실행
```
$ python3
Python 3.8.0 (default, Oct 28 2019, 16:14:01)
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys, os
>>> from konlpy.tag import Kkma
>>> kkma = Kkma()
```
에러 안 나고 잘 됨. 끝.



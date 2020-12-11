# konlpy 설치해 보기

## Windows 에 설치 (포기)

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

제기랄... Windows는 뭐냐...




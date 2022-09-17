# CMake Tutoral

## 목적

아래의 영상을 보면서 CMake에 대한 기초 익히기

[CMAKE TUTORIAL](https://youtube.com/playlist?list=PLalVdRk2RC6o5GHu618ARWh0VO0bFlif4)


# OS별 CMake Build

[Windows](#Windows)

[MacOS & Linux](#MacOS-&-Linux)

## Windows

### Windows에서 Makefile 생성 방법

참고 영상에서는 기본적으로 Linux를 사용 중이라, Windows에서는
```commandline
$ cmake -S . -B out/build
```
를 했을 때, Makefiles가 아닌 Visual Studio 솔루션 프로젝트 (`.sln`)을 생성함.

그래서 찾다보니 [C++ OpenGL Tutorial : Making a window in GLFW](https://youtu.be/LeLO7gdwQCI) 영상에서 Makefile을 윈도우에서
사용하고 있어서 확인을 해보니 **MinGW**를 설치하는 것이 중요한 포인트다.

[MinGW](https://sourceforge.net/projects/mingw/)는 구글에 검색해서 다운받을 수 있고, 다운을 다 받고, 설치 다 하고 나오는 Basic Setup에
모든 패키지를 일단 설치해줬다.

그러고 `시작 > 시스템 환경 변수 편집 > 환경 변수 > 시스템 변수 > Path`에 MinGW의 실행 파일들이 있는 `bin` 폴더를 등록해주면 된다.
```text
C:\MinGW\bin
```
딱히 설정 안했으면, 위의 경로에 관련 파일들이 있을 것이다.

이렇게 하고 `CMakeLists.txt`가 있는 디렉토리에서 빌드할 때 `-G` 옵션을 추가해주면 된다.
```commandline
$ cmake -S . -B out/build -G "MinGW Makefiles"
-- The C compiler identification is GNU 6.3.0
-- The CXX compiler identification is GNU 6.3.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: C:/MinGW/bin/gcc.exe - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: C:/MinGW/bin/c++.exe - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/Users/habi/OpenGL/cmake-tutorial/out/build
```
이렇게 해서 `out/build`로 들어가보면 `Makefile`이 있는 것을 볼 수 있는데 이놈을 `make` 해주면 된다.

여기에서, Windows용 make를 설치하거나 mingw32-make를 사용하면 된다.
```commandline
# 선택 1
$ make

# 선택 2
$ mingw32-make

# 결과
[ 50%] Building CXX object CMakeFiles/tutorial.dir/main.cpp.obj
[100%] Linking CXX executable tutorial.exe
[100%] Built target tutorial
```

### Windows용 make 설치

- [How to Install and Use “Make” in Windows](https://www.technewstoday.com/install-and-use-make-in-windows/)
- [How to install and use "make" in Windows?](https://stackoverflow.com/questions/32127524/how-to-install-and-use-make-in-windows)

위에 두 글 중에서 아무거나 참고해서 `GnuWin32`를 설치해준다.

1번 글은 `cmd`에서 `Winget`으로 설치하는 방법이고, 2번 글은 `Chocolatey`를 통해서 설치하는 방법이다. 그냥 아무거나 쓰면 될 듯 싶지만,
그래도 말하자면 나는 1번으로 설치했다.

설치하면 이제 `make.exe`를 실행할 수 있는데, 물론 그전에 환경 변수 세팅을 해줘야한다.

`시작 > 시스템 환경 변수 편집 > 환경 변수 > 시스템 변수 > Path`에서 `C:\Program Files (x86)\GnuWin32\bin`을 등록해주면 된다.

물론 여기에서 문제가 있다. Windows는 기본적으로 Visual Studio를 받아오고 있어서 `make`를 써보면 아래 문제가 생긴다.
```commandline
$ make
bash: ./make.bat: No such file or directory
```

그렇다면, 그냥 `make.exe`를 alias를 통해서 `make`로 세팅해주자.
```text
alias make="make.exe"
```

## MacOS & Linux

MacOS는 Mac Mini (M1) 으로, Linux는 Linux Mint로 테스트를 해봤고, 문제 없이 빌드했다.

이 둘은 `make`가 기본적으로 터미널에 들어가있어서 바로 명령어를 실행하면 된다.

`cmake`는 설치해야 되는 걸로 기억하는데, 터미널에서 사용하려면 `brew`로 설치해야 하고, 찾아보면 방법이 자세하게 나온다.

그런데, 나는 cmake 공식 페이지에서 프로그램으로 설치하면서 터미널에서 사용 가능했던걸로 기억하는데, 막상 cmake 경로를 찾아보면 brew 내부에 존재한다.

아무튼, cmake를 설치하면 된다. 공식 다운로드는 여기 ([cmake download](https://cmake.org/download/)) 에서 가능하다.

```commandline
$ cmake -S . -B out/build
-- The C compiler identification is AppleClang 14.0.0.14000029
-- The CXX compiler identification is AppleClang 14.0.0.14000029
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/habi/OpenGL/cmake-tutorial/out/build

$ cd out/build
$ make
[ 50%] Building CXX object CMakeFiles/tutorial.dir/main.cpp.o
[100%] Linking CXX executable tutorial
[100%] Built target tutorial
```

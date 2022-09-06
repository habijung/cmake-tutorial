# CMake Tutoral

## 목적

아래의 영상을 보면서 CMake에 대한 기초 익히기

[CMAKE TUTORIAL](https://youtube.com/playlist?list=PLalVdRk2RC6o5GHu618ARWh0VO0bFlif4)


## Windows에서 Makefile 생성 방법

참고 영상에서는 기본적으로 Linux를 사용 중이라, Windows에서는
```commandline
$ cmake -S . -B out/build
```
를 했을 때, Makefiles가 아닌 Visual Studio 솔루션 프로젝트 (`.sln`)을 생성함.

그래서 찾다보니 [C++ OpenGL Tutorial : Making a window in GLFW](https://youtu.be/LeLO7gdwQCI) 영상에서 Makefile을 윈도우에서
사용하고 있어서 확인을 해보니 **MInGW**를 설치하는 것이 중요한 포인트다.

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

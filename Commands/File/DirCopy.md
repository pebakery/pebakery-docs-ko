# DirCopy

디렉터리를 복사합니다. 하위 디렉터리 및 파일도 복사됩니다.

와일드카드를 사용하여 동시에 여러 디렉터리를 복사할 수 있습니다.

## 문법

```pebakery
DirCopy,<SrcDir>,<DestDir>
```

### 인자

| 인자 | 설명 |
| --- | --- |
| SrcDir | 복사하고자 하는 디렉터리의 전체 경로. 와일드카드 (*, ?)를 사용할 수 있습니다. |
| DestDir | 디렉터리가 복사될 곳의 전체 경로. 대상 경로가 존재하지 않는 경우 새 디렉터리 구조가 생성되며, 존재할 경우 덮어씁니다. |

## 유의사항

`DestDir`가 파일인 경우 오류가 발생합니다.

WinBuilder 082에는 와일드카드가 사용될 경우 DirCopy가 FileCopy와 유사하게 작동하는 버그가 있습니다. PEBakery의 `Simulate WinBuilder's *.* bug in DirCopy` 호환성 옵션을 켜서 이 버그를 흉내낼 수 있습니다. 자세한 정보는 예제 2를 참고하십시오.

## 연관 명령어

[DirMove](./DirMove.md),[DirDelete](./DirDelete.md), [FileCopy](./FileCopy.md), [PathMove](./PathMove.md)

## 예제

`%SrcDir%`*C:\Temp\Src*가 다음 파일들로 구성되어 있다고 가정합니다.

```pebakery
C:\Temp\Src\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
|--- Y.ini
|--- AZ.txt
```

### 예제 1

```pebakery
// %SrcDir% 디렉터리는 그대로 %DestDir%로 복사됩니다.
DirCopy,%SrcDir%,%DestDir%
```

결과

```pebakery
C:\Temp\Dest\
|--- Src\
     |--- AAA\
          |--- A.txt
     |--- ABB\
          |--- B.ini
     |--- ACC\
          |--- C.txt
          |--- D.txt
     |--- AEE\
     |--- Y.ini
     |--- AZ.txt
```

### 예제 2

```pebakery
// %SrcDir% 디렉터리는 그대로 %DestDir%로 복사됩니다.
DirCopy,%SrcDir%\A*,%DestDir%
```

결과

```pebakery
C:\Temp\Dest\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
```

**Simulate WinBuilder's *.* bug in DirCopy 호환성 옵션이 켜져 있을 때의 결과**

```pebakery
C:\Temp\Dest\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
|--- AZ.txt
```
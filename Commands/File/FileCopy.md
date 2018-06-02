# FileCopy

파일을 복사합니다.

와일드카드를 사용하여 한 번에 여러 개의 파일을 복사할 수 있습니다.

## 문법

```pebakery
FileCopy,<SrcFile>,<DestPath>,[PRESERVE],[NOWARN],[NOREC]
```

### 인자

| 인자 | 설명 |
| --- | --- |
| SrcFile | 복사하고자 하는 파일의 전체 경로. 와일드카드 (*, ?)를 사용할 수 있습니다. |
| DestPath | 파일이 복사될 곳의 전체 경로. 파일 하나를 복사하는 경우 대상 경로는 파일 이름입니다. 여러 파일을 복사하는 경우 대상 경로는 디렉터리이며, 존재하지 않는 경우 새 디렉터리 구조가 생성됩니다. |

### 플래그

플래그는 순서에 영향을 받지 않습니다.

| 플래그 | 설명 |
| --- | --- |
| PRESERVE | **(선택)** 대상 파일이 존재하는 경우 덮어씁니다. |
| NOWARN | **(선택)** 대상 파일을 덮어쓸 때 경고 로그를 생성하지 않습니다. |
| NOREC | **(선택)** 와일드카드를 사용할 때 하위 디렉터리를 복사하지 않습니다. |

## 유의사항

파일 이름에 와일드카드가 사용되면 `FileCopy`는 하위 디렉터리를 복사합니다. 이를 막기 위해선 `NOREC` 플래그를 사용하십시오.

와일드카드는 디렉터리 이름 적용되지 않으며, 파일 이름에만 적용됩니다.

## 관련 명령어

[DirCopy](./DirCopy.md), [DirCreate](./DirCreate.md), [FileDelete](./FileDelete.md), [FileMove](./FileMove.md), [PathMove](./PathMove.md)

## 예제

`%SrcDir%` *C:\Temp\Src*가 다음 파일들로 구성되어 있다고 가정합니다:

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

### 에제 1

`C:\Temp\AZ.txt`를 %DestDir% `C:\Temp\myFolder\`로 복사합니다.

```pebakery
FileCopy,%SrcDir%\AZ.txt,%DestDir%
```

결과

```pebakery
C:\Temp\myFolder\
|--- AZ.txt
```

### 예제 2

`C:\Temp\AZ.txt`를 %DestDir% `C:\Temp\myFolder\`로 복사하고 이름을 `B.txt`으로 변경합니다.

```pebakery
FileCopy,%SrcDir%\AZ.txt,%DestDir%\B.txt
```

결과

```pebakery
C:\Temp\myFolder\
|--- B.txt
```

### 예제 3

%SrcDir% 내 모든 `.txt` 파일이 %DestDir%로 복사됩니다.

```pebakery
FileCopy,%SrcDir%\*.txt,%DestDir%
```

결과

```pebakery
C:\Temp\myFolder\
|--- AAA\
     |--- A.txt
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AZ.txt
```

### 예제 4

%SrcDir% 내 모든 `.txt` 파일이 %DestDir%로 복사됩니다. 하위 디렉터리 내 `.txt` 파일은 복사되지 않습니다.

```pebakery
FileCopy,%SrcDir%\*.txt,%DestDir%,NOREC
```

결과

```pebakery
C:\Temp\myFolder\
|--- AZ.txt
```

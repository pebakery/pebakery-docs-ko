# FileDelete

파일을 삭제합니다.

와일드카드를 사용하여 한 번에 여러 파일을 삭제할 수 있습니다.

## 문법

```pebakery
FileDelete,<FilePath>,[NOWARN],[NOREC]
```

### 인자

| 인자 | 설명 |
| --- | --- |
| FilePath | 삭제하고자 하는 파일. 와일드카드 (*, ?)를 사용할 수 있습니다. |

### 플래그

플래그는 순서에 영향을 받지 않습니다.

| 플래그 | 설명 |
| --- | --- |
| NOWARN | **(선택)** 파일이 존재하지 않는 경우 경고 로그를 생성하지 않습니다. |
| NOREC | **(선택)** 와일드카드를 사용하여 파일을 삭제할 때 하위 디렉터리를 무시합니다. |

## 유의사항

와일드카드가 사용되면 하위 디렉터리 내 파일도 함께 삭제됩니다. 이를 예방하기 위해선 `NOREC` 플래그를 사용하십시오.

**삭제한 파일들은 휴지통에서 복구할 수 없습니다.**

## 관련 명령어

[DirDelete](./DirDelete.md), [FileCopy](./FileCopy.md), [PathMove](./PathMove.md)

## 예제

`%SrcDir%` *C:\Temp*가 다음 파일들로 구성되어 있다고 가정합니다.

```pebakery
C:\Temp\
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

`C:\Temp\AZ.txt`가 삭제됩니다.

```pebakery
FileDelete,%SrcDir%\AZ.txt
```

결과

```pebakery
C:\Temp\
|--- AAA\
     |--- A.txt
|--- ABB\
     |--- B.ini
|--- ACC\
     |--- C.txt
     |--- D.txt
|--- AEE\
|--- Y.ini
```

### 예제 2

SrcDir% 내 모든 `.txt` 파일들이 삭제됩니다. 하위 디렉터리 내 `.txt` 파일들도 함께 삭제됩니다.

```pebakery
FileDelete,%SrcDir%\*.txt
```

결과

```pebakery
C:\Temp\
|--- AAA\
|--- ABB\
     |--- B.ini
|--- ACC\
|--- AEE\
|--- Y.ini
```

### 예제 3

SrcDir% 내 모든 `.txt` 파일들이 삭제됩니다. 하위 디렉터리 내 `.txt` 파일들은 삭제되지 않습니다.

```pebakery
FileDelete,%SrcDir%\*.ini,NOREC
```

결과

```pebakery
C:\Temp\
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

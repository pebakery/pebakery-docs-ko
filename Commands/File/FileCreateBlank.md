# FileCreateBlank

빈 파일을 생성합니다.

## 문법

```pebakery
FileCreateBlank,<FilePath>,[Encoding],[PRESERVE],[NOWARN]
```

### 인자

| 인자 | 설명 |
| --- | --- |
| FilePath | 생성하고자 하는 빈 파일의 경로 |
| Encoding | **(선택)** 새 파일에 사용할 텍스트 인코딩. `UTF8`, `UTF16`, `UTF16BE`, `ANSI`가 지원되며, **기본값**은 `ANSI`입니다. |

### 플래그

플래그는 순서에 영향을 받지 않습니다.

| 플래그 | 설명 |
| --- | --- |
| PRESERVE | **(선택)** 존재하는 파일을 덮어쓰지 않습니다. |
| NOWARN | **(선택)** 파일을 덮어쓰는 경우 경고 로그를 생성하지 않습니다. |

## 유의사항

`TXTAddLine`과 같은 특정 명령어들은 존재하는 파일만 쓸 수 있습니다. `FileCreateBlank` 명령어를 사용하여 이러한 상황에서 빈 파일을 미리 생성할 수 있습니다.

배치 파일 (`*.bat`, `*.cmd`)에는 `ANSI` 인코딩을 사용해야 합니다. 일반적인 텍스트 파일의 경우 `UTF16`이나 `UTF8`을 사용하는 것이 매우 권장됩니다.

## 연관 명령어

[TXTAddLine](../TXT/TXTAddLine.md)

## 예제

### 예제 1

빈 파일 Unicode.txt을 생성하고, UTF-16 리틀 엔디안 BOM (U+FEFF)을 씁니다.

```pebakery
FileCreateBlank,C:\Temp\Unicode.txt,UTF16
```

### 예제 2

이 스크립트는 파일이 존재하는지 검사하고 생성해야 할 경우 `FileCreateBlank` 명령을 사용합니다.

```pebakery
[Main]
Title=FileCreateBlank
Description=Show the usage of FileCreateBlank.
Level=5
Version=1
Author=Homes32

[Variables]
%grubMenu%=C:\Temp\menu.lst

[process]
If,Not,ExistFile,%grubMenu%,FileCreateBlank,%grubMenu%
TXTAddLine,%grubMenu%,"TITLE Main Menu",APPEND
```
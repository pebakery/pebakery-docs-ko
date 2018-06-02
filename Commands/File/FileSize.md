# FileSize

**Alias**: `Retrieve,FileSize`

파일의 크기를 계산합니다.

## 문법

```pebakery
FileSize,<FilePath>,<DestVar>
```

### 인자

| 인자 | 설명 |
| --- | --- |
| FilePath | 파일의 전체 경로 |
| DestVar | 파일 크기 (바이트 단위)가 저장될 변수명 |

## 유의사항

`StrFormat,Bytes` 명령어로 바이트 단위 크기를 사람이 읽기 쉬운 단위로 변환할 수 있습니다. (Ex. 3.5MB)

## 관련 명령어

[DirSize](./DirSize), [StrFormat,Bytes](../String/Bytes.md)

## 예제

### 예제 1

```pebakery
[Main]
Title=FileSize
Description=Show the usage of FileSize.
Level=5
Version=1
Author=Homes32

[Variables]
%File%=C:\Windows\notepad.exe

[process]
FileSize,%File%,%Size%
// Use StrFormat to convert the size to a more human readable format.
StrFormat,Bytes,%Size%,%StrSize%
Message,"File Size: %Size% bytes (%StrSize%)"
```

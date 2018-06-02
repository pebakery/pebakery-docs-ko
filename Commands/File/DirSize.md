# DirSize

**Alias**: `Retrieve,DirSize`

디렉터리의 크기를 계산합니다.

## 문법

```pebakery
DirSize,<DirPath>,<%DestVar%>
```

### 인자

| 인자 | 설명 |
| --- | --- |
| DirPath | 디렉터리의 전체 경로 |
| DestVar | 디렉터리 크기 (바이트 단위)가 저장될 변수명 |

## 유의사항

`DirPath` 내 파일이 `Administrator` 권한으로 접근이 불가능한 경우, 크기 계산에서 무시됩니다.

`StrFormat,Bytes` 명령어로 바이트 단위 크기를 사람이 읽기 쉬운 단위로 변환할 수 있습니다. (Ex. 3.5GB)

## 관련 명령어

[FileSize](./FileSize.md), [StrFormat,Bytes](../String/Bytes.md)

## 예제

### 예제 1

```pebakery
[Main]
Title=DirSize
Description=Show the usage of DirSize.
Level=5
Version=1
Author=Homes32

[Variables]
%Dir%=C:\Windows\System32

[process]
DirSize,%Dir%,%Size%
// StrFormat 명령어를 사용하여 바이트 단위 크기를 사람이 읽기 쉬운 단위로 변환합니다.
StrFormat,Bytes,%Size%,%StrSize%
Message,"Dir Size: %Size% bytes (%StrSize%)"
```

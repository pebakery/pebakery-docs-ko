# FileVersion

**Alias**: `Retrieve,FileVersion`

실행 파일의 버전 정보를 읽습니다.

## 문법

```pebakery
FileVersion,<FilePath>,<DestVar>
```

### 인자

| 인자 | 설명 |
| --- | --- |
| FilePath | 파일의 전체 경로 |
| DestVar | 파일 버전이 저장될 변수명 |

## 유의사항

버전 정보를 읽을 수 없는 경우 `0.0.0.0`이 반환됩니다.

## 관련 명령어

없음

## 예제

```pebakery
[Main]
Title=FileVersion
Description=Show the usage of FileVersion.
Level=5
Version=1
Author=Homes32

[Variables]
%File%=C:\Windows\notepad.exe

[process]
FileVersion,%File%,%Ver%
Message,"%File%#$xFile Version: %Ver%"
```
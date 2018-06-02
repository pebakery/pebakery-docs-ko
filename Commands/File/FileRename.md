# FileRename

**Alias**: `FileMove`

파일을 옮기거나 이름을 변경합니다.

## 문법

```pebakery
FileRename,<SrcPath>,<DestPath>
```

### 인자

| 인자 | 설명 |
| --- | --- |
| SrcPath | 옮기거나 이름을 변경하고자 하는 파일의 전체 경로 |
| DestPath | 파일이 옮겨질 곳의 전체 경로 또는 새로 사용할 이름의 경로 |

## 유의사항

`FileRename`은 파일을 옮기기 위해서도 사용될 수 있습니다.
`FileRename` can also be used to move a file.

WinBuilder 082의 `FileRename`는 디렉터리도 옮길 수 있습니다. PEBakery의 `FileRename and DirMove work like PathMove` 호환성 옵션을 활성화하면 `FileRename`가 `PathMove`처럼 작동합니다.

## 관련 명령어

[FileCopy](./FileCopy.md), [PathMove](./PathMove.md)

## 예제

### 예제 1

`A.txt`의 이름을 `B.txt`로 변경합니다.

```pebakery
FileRename,%SrcDir%\A.txt,%SrcDir%\B.txt
```

### 예제 2

`%SrcDir%\A.txt`를 `%DestDir%\B.txt`로 옮깁니다.

```pebakery
FileMove,%SrcDir%\A.txt,%DestDir%\B.txt
```

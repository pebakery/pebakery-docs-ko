# PathMove

파일이나 디렉터리를 옮깁니다.

## 문법

```pebakery
PathMove,<SrcPath>,<DestPath>
```

### 인자

| 인자 | 설먕 |
| --- | --- |
| SrcPath | 옮기고자 하는 파일/디렉터리의 전체 경로 |
| DestPath | 파일/디렉터리가 옮겨질 대상 경로 |

## 유의사항

호환성 옵션 `FileRename and DirMove work like PathMove`을 활성화하면 `FileRename`과 `DirMove`가 `PathMove`처럼 작동합니다.

## 관련 명령어

[DirMove](./DirMove.md), [FileRename](./FileRename.md)

## 예제

### 예제 1

`A.txt`의 이름을 `B.txt`로 변경합니다.

```pebakery
PathMove,%SrcDir%\A.txt,%SrcDir%\B.txt
```

### 예제 2

`%SrcDir%\A.txt`를 `%DestDir%\B.txt`로 옮깁니다.

```pebakery
PathMove,%SrcDir%\A.txt,%DestDir%\B.txt
```

### 예제 3

%DestDir%가 존재하는 경우: `%SrcDir%\A`가 `%DestDir%\A`로 옮겨집니다.
%DestDir%가 존재하지 않는 경우: `%SrcDir%\A`가 `%DestDir%`로 옮겨집니다.

```pebakery
PathMove,%SrcDir%\A,%DestDir%
```

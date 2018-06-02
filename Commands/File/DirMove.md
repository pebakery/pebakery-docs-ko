# DirMove

디렉터리를 옮기거나 이름을 변경합니다.

## 문법

```pebakery
DirMove,<SrcDir>,<DestPath>
```

### 인자

| 인자 | 설명 |
| --- | --- |
| SrcDir | 옮기고자 하는 디렉터리의 전체 경로 |
| DestPath | 디렉터리가 옮겨질 곳의 전체 경로입니다. 대상 경로가 존재하지 않는 경우 새 디렉터리가 생성되며, 존재할 경우 덮어씁니다. |

## 유의사항

WinBuilder 082의 `DirMove`는 파일도 옮길 수 있습니다. PEBakery의 `FileRename and DirMove work like PathMove` 호환성 옵션을 활성화하면 `DirMove`가 `PathMove`처럼 작동합니다.

## 관련 명령어

[DirCopy](./DirCopy), [DirDelete](./DirDelete), [PathMove](./PathMove.md)

## 예제

### 에제 1

```pebakery
DirMove,%SrcDir%\A,%DestDir%
```

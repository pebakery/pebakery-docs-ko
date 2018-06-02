# DirDelete

디렉터리를 삭제합니다. 하위 디렉터리 및 파일도 함께 삭제됩니다.

## 문법

```pebakery
DirDelete,<DirPath>
```

### 인자

| 인자 | 설명 |
| --- | --- |
| DirPath | 삭제하고자 하는 디렉터리의 전체 경로 |

## 유의사항

**삭제한 디렉터리는 휴지통에서 복구할 수 없습니다.**

## 관련 명령어

[FileDelete](./FileDelete)

## 예제 

### 예제 1

```pebakery
// C:\Temp가 삭제됩니다.
DirDelete,C:\Temp
```
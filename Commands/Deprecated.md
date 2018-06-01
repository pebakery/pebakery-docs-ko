# 제거된 명령어

## PEBakery에서 제거된 명령어

다음 명령어들은 WinBuilder 082에 존재하지만, PEBakery에서 구현되지 않았습니다.

### FileByteExtract

더 이상 사용되지 않습니다.

### RegReadBin / RegWriteBin

PEBakery는 유니코드 문자열을 정상적으로 처리할 수 있습니다.

### ExtractAllFilesIfNotExist

더 이상 사용되지 않으며, 다른 방법으로 같은 효과를 낼 수 있습니다.

### StrFormat,CharToOEM / OEMToChar

더 이상 사용되지 않습니다.

### System,Comp80

PEBakery의 명령어 내부 구현은 WinBuilder 082 내부 구조와 무관하며, WinBuilder 080의 구현은 지원하지 않습니다.

### System,FileRedirect / RegRedirect

PEBakery는 AnyCPU나 x64로 컴파일될 수 있으며, 실행을 위해 WOW64를 필요로 하지 않습니다.

### System,IsTerminal

더 이상 사용되지 않습니다.

### System,Log

더 이상 사용되지 않습니다.

### System,SplitParameters

더 이상 사용되지 않으며, PEBakery는 언제나 인자들을 `,`를 기점으로 분리합니다.

### If,License

더 이상 사용되지 않습니다.

## 제거될 예정인 명령어들

PEBakery에서 이 명령어들을 사용할 수는 있지만, 추후 삭제될 예정입니다. 다른 명령어를 사용하는 것을 강력히 추천합니다.

### WebGetIfNotExist

WinBuilder 082에서 제대로 작동하지 않는 명령어입니다.

### StrFormat,ShortPath / LongPath

이 명령어는 레지스트리 `HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation`의 값에 따라 성공할 수도, 실패할 수도 있습니다.

어떤 환경에서도 제대로 작동한다는 보장이 없기에 삭제될 예정입니다.

### System,HasUAC

PEBakery는 이 명령어에 언제나 `True`를 반환합니다.

현재 Microsoft에 의해 지원되는 모든 Windows 버전에서는 User Account Control (UAC)가 기본적으로 켜져 있습니다. 즉 대부분의 환경에서 UAC가 켜져 있다고 가정하는 것이 좋습니다.  많은 사용자들은 UAC를 끄는 것의 보안 위협을 알지 못합니다. 따라서 프로젝트 빌드를 위해 UAC를 끄도록 유도하는 대신 UAC 활성 여부에 상관없이 프로젝트가 성공적으로 빌드되도록 설계하십시오.

### System,RebuildVars

이름과 달리, 이름과 달리 WinBuilder 082에서 이 명령어는 모든 변수를 삭제합니다.

현재 PEBakery에서는 이 명령어가 실행되면 변수를 스크립트 기본값으로 초기화합니다.

### GetParam / PackParam

WinBuilder 082에서 제대로 작동하지 않는 명령어이며, 더 이상 사용되지 않습니다.

PEBakery는 Section 인자 수에 제한이 없기 때문에 이 명령어를 사용할 이유가 없습니다.

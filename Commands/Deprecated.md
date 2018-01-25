# 지원이 중단되었거나 중단될 명령어

다음 명령어들은 더 이상 지원되지 않습니다.

## 지원이 중단된 명령어

### FileByteExtract

더 이상 사용되지 않습니다.

### RegReadBin / RegWriteBin

PEBakery는 RegRead와 RegWrite에서 QWORD와 유니코드 문자열을 지원하기 때문에 더 이상 필요하지 않습니다.

### ExtractAllFilesIfNotExist

더 이상 사용되지 않습니다.

### StrFormat,CharToOEM / OEMToChar

DOS 문자셋은 더 이상 사용되지 않습니다.

### System,Comp80

PEBakery는 WinBuilder 082와 호환되는 구현체이며, WinBuilder 080을 지원하지 않습니다.

### System,FileRedirect / RegRedirect

PEBakery는 AnyCPU나 x64로 컴파일될 수 있으며, 실행에 WOW64가 필요하지 않습니다.

### System,IsTerminal

더 이상 사용되지 않습니다.

### System,Log

더 이상 사용되지 않습니다.

### System,SplitParameters

더 이상 사용되지 않으며, PEBakery는 언제나 인자를 분해합니다.

### If,License

더 이상 사용되지 않습니다.

## 지원이 중단될 명령어

다음 명령어들은 차기 버전에서 지원이 중단될 예정이며, 사용이 권장되지 않습니다.

### ExtractAndRun

WinBuilder의 한계로 인해 이 명령어는 Extract와 ShellExecuteDelete를 사용한 매크로로 구현하는 것이 권장됩니다.

### WebGetIfNotExist

WinBuilder 082는 버그로 인해 이 명령어들을 제대로 실행하지 못하며, 매크로로 구현하는 것이 권장됩니다.

### StrFormat,ShortPath / LongPath

레지스트리 `HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation` 값에 따라 명령어가 제대로 작동할수도, 작동하지 않을수도 있습니다.

이러한 이유로 인해 이 명령어는 모든 환경에서 제대로 작동하리라 보장될 수 없습니다.

### System,HasUAC

PEBakery는 이 명령어에 대해 언제나 `True`를 반환합니다.

Microsoft는 지원하는 모든 Windows 버전에서 User Account Control (UAC)를 기본으로 켜 두었습니다. 대다수의 사용자들은 UAC의 존재 및 UAC를 끄는 것의 위험성을 인지하지 못하고 있습니다. 따라서 프로젝트를 작성할 때 UAC의 상태에 관계없이 프로젝트가 제대로 작동하도록 설계하는 것이 권장됩니다.

### System,RebuildVars

이름과 다르게 변수들을 초기화합니다.

### GetParam / PackParam

WinBuilder 082는 버그로 인해 이 명령어들을 제대로 실행하지 못합니다.

PEBakery는 무한대의 섹션 인자를 지원하기 때문에 이 명령어들은 더 이상 필요하지 않습니다.

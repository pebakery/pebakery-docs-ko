# 코딩 가이드

## 문법 오류 점검

PEBakery를 사용하여 명령어들의 문법 오류를 점검할 수 있습니다.

### 명령어나 섹션 점검

`Utility` 창에서 `Syntax Checker` 탭을 선택하고, 코드를 붙여 넣으십시오.

### 스크립트 점검

프로젝트 트리에서 스크립트를 선택한 뒤, 스크립트 제목 오른쪽에 있는 물음표 모양 버튼을 누르십시오.

`Auto Syntax Check Error` 설정을 활성화하셨다면, 버튼 아이콘의 모양과 색상으로 오류 여부가 보고됩니다.

## 명령어 최적화

파일을 읽고 쓰는 명령어 중 일부는 실행 시점에 자동으로 최적화합니다.

- TXTAddLine
- TXTReplace
- TXTDelLine
- INIRead
- INIWrite
- INIDelete
- INIReadSection
- INIAddSection
- INIDeleteSection
- INIWriteTextLine
- Visible
- ReadInterface
- WriteInterface
- WimExtract
- WimPathAdd, WimPathDelete, WimPathRename

같은 파일에 대한 읽기/쓰기 작업이 여러번 연달아 배치되어 있을 경우, 이 명령들을 한 번에 묶어서 처리하여 성능을 높입니다.

**같은 명렁어들**이 **같은 파일**에 **연달아 배치**되어 있어야 최적화가 이루집니다.

최고의 성능을 얻기 위해 최적화를 염두에 두고 코딩하시는 것을 권장합니다.

### 최적화되는 명령어 배치

다음 예시에서는 여러 TXTAddLine를 사용해 `%ProjectTemp%\Korean_IME_Reference.txt`에 여러 줄의 텍스트를 추가합니다. 최적화된 경우 한 번의 쓰기로 텍스트 파일을 완성합니다.

```pebakery
Set,%w%,%ProjectTemp%\Korean_IME_Reference.txt
FileCreateBlank,%w%
TXTAddLine,%w%,"<Korean IME Script - Reference>",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [TechNet] Add Input Method Editor (IME) to Windows PE 3.0",Append
TXTAddLine,%w%,"  - https://technet.microsoft.com/en-us/library/dd744589%28v=ws.10%29.aspx",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [Blog] Add Hangul IME support on Windows PE 4.0",Append
TXTAddLine,%w%,"  - http://cappleblog.co.kr/549",Append
```

다음 Visible 명령어들도 한 번에 실행됩니다.

```pebakery
Visible,%pBevel3%,True,PERMANENT
Visible,%pCheckBox4%,True,PERMANENT
Visible,%pCheckBox5%,True,PERMANENT
Visible,%pCheckBox6%,True,PERMANENT
Visible,%pCheckBox7%,True,PERMANENT
```

### 최적화되지 않는 명령어 배치

TXTDelLine와 TXTAddLine는 다른 명령어이기에 최적화되지 않습니다.

```pebakery
TXTDelLine,%target_sys%\autorun.cmd,exit
TXTAddLine,%target_sys%\autorun.cmd,"hiderun.exe IMEReg.cmd",Append
```

같은 파일에 쓰는 TXTAddLine가 여러번 호출되었지만, 연달아 배치되어 있지 않아 최적화되지 않습니다.

```pebakery
TXTAddLine,%DestDir%\hello.txt,"Hello World!",Append
Echo,"Hello World!"
TXTAddLine,%DestDir%\hello.txt,"Have a nice day.",Append
```

이 WimExtract 명령어들은 같은 파일을 다루지만, Flag가 다르기에 최적화되지 않습니다.

``` pebakery
WimExtract,%WimDir%\LZX.wim,1,Z.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,A?.txt,%DestDir%,NOACL
```

### 최적화로 인해 발생할 수 있는 문제

최적화가 꺼져 있는 경우, 각 명령어들은 다른 명령어와 독립적입니다. 즉 한 명령어가 실패해도 다른 명령어에 영향을 미치지 않습니다. 하지만 명령어들이 최적화된 경우 오류가 발생할 때 서로에게 의도하지 않는 영향을 미칠 수 있습니다.

`LZX.wim` 이미지가 다음 파일들을 가지고 있다고 가정합시다:

```pebakery
LZX.wim
|--- AZ.txt
|--- B.txt
|--- Z.txt
```

두 번째 WimExtract 명령어에서 존재하지 않는 파일을 압축해제하려고 시도하기에 오류가 발생합니다. 만약 이 명령어들이 실행 시점에서 하나의 명령어로 최적화된 경우, 두 번째 명령어에 의해 발생한 오류 때문에 다른 명령어도 실패하게 됩니다.

```pebakery
WimExtract,%WimDir%\LZX.wim,1,Z.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,A.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,B.txt,%DestDir%,CHECK
```

# 코딩 가이드

## 문법 오류 점검

PEBakery를 사용하여 명령어들의 문법 오류를 점검할 수 있습니다.

### 명령어나 섹션 점검

`Utility` 창에서 `Syntax Checker` 탭을 선택하고, 코드를 붙여 넣으십시오.

### 스크립트 점검

프로젝트 트리에서 스크립트를 선택한 뒤, 오른쪽 위에 있는 체크 모양 (✔️) 버튼을 누르십시오.

`Auto Syntax Check Error` 설정이 활성화되어 있다면, 점검이 스크립트를 선택하는 순간 자동으로 이루어집니다.
버튼의 색이 주황색이면 오류가 있는 것이고, 초록색이면 이상이 없는 것입니다.

## 명령어 최적화

PEBakery는 텍스트를 다루는 명령어의 일부를 자동으로 최적화합니다.

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

같은 파일에 대한 읽기/쓰기 작업이 여러번 연달아 배치되어 있을 경우, 이 명령들을 한 번에 묶어서 처리하여 성능을 높입니다.

**같은 명렁어들**이 **같은 파일**에 **연달아 배치**되어 있어야 최적화가 이루집니다.

최고의 성능을 얻기 위해 최적화을 염두에 두고 코딩하시는 것을 권장합니다.

### 최적화되는 명령어 배치

다음 예시에서는 여러 TXTAddLine를 사용해 하나의 파일에 여러 줄의 텍스트를 추가하며, 이 명령어들은 하나의 TXTAddLineOp로 최적화됩니다.

```pebakery
Set,%w%,%ProjectTemp%\Korean_IME_TheOven.txt
FileCreateBlank,%w%
TXTAddLine,%w%,"<Korean IME Plugin - TheOven Topics>",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [TheOven] Korean IME for Win8.1SE topic",Append
TXTAddLine,%w%,"  - http://TheOven.org/index.php?topic=825",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [TheOven] Korean IME for Win10PESE topic",Append
TXTAddLine,%w%,"  - http://TheOven.org/index.php?topic=1440",Append
Call,StartDoc,%w%
```

Visible 명령어는 언제나 자신이 속해있는 스크립트에 영향을 미칩니다. 따라서, 다음 예시는 하나의 VisibleOp로 최적화됩니다.

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

같은 파일에 쓰는 TXTAddLine가 여러번 호출되었지만, 연달아 배치되어 있지 않기 때문에 최적화되지 않습니다.

```pebakery
TXTAddLine,%DestDir%\hello.txt,"Hello World!",Append
Echo,"Hello World!"
TXTAddLine,%DestDir%\hello.txt,"Have a nice day.",Append
```

### 최적화로 인해 발생할 수 있는 문제.

일반적인 상황에서 오류가 발생하면 오류가 발생하기 전까지의 명령어 실행 내역이 보존됩니다.

하지만 최적화된 명령어에서 오류가 발생하면, 이 명령어가 작업한 모든 내용은 소실됩니다.

따라서 최적화된 코드에서 예기치 못한 오류가 발생하지 않도록 주의하여야 합니다.

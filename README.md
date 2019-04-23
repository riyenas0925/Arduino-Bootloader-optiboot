<h1 align="center">Arduino Bootloader optiboot</h1>

> Atmega8에 UNO 부트로더를 올리면 10초정도 후에 프로그램이 시작되는 문제를 해결하기 위함

## atmega8  optiboot 적용 부트로더

1. AVR STUDIO 4에서 ISP(STK500)연결후 `TOOLS` - `PROGRAM AVR` - `AUTO CONNECT`

2. `MAIN`에서 ATMEGA8에 해당하는 모델 선택 `READ SIGNATURE`로 정상적으로 연결 확인

3. `PROGRAM` 페이지로 이동한다음 FLASH부분에서 자신에게 맞는 부트로더의 HEX파일을 선택한다음 `PROGRAM` 버튼을 누른다
    > (이때 부트로더 HEX파일은 아두이노 설치폴더에 있다.)

4. 아래는 OPTIBOOT_ATMEGA8 의 HEX파일 위치이다.
    > C:\Program Files (x86)\Arduino\hardware\arduino\avr\bootloaders\optiboot\optiboot_atmega8.hex	//아두이노 1.8.5버전 기준

5. 아래와 같이 fuse bit, lock bit를 설정한다.
    ```
    //AVR Studio 기준
    high_fuses=0xdc
    low_fuses=0xbf
    lock_bits=0xCf

    //Code Vision 기준
    SPIEN, BOOTRST,BODEN 체크
    BOOTSZ  Boot Flash size=256 words Boot address=$0F00
    BODLEVEL Brown-out detection at VCC=2.7V
    SUT_CKSEL Ext, Cryatal/Resonator High; Start-up time: 16K CK + 64로 설정
    ```

## 아두이노 설정

1. 아두이노 `프로그램 실행후 파일` - `환경설정` - `추가적인 보드매니저 URLs` 에 
https://github.com/Optiboot/optiboot/releases/download/v6.2/package_optiboot_optiboot-additional_index.json 을 넣고 확인을 누른다

2. `툴` - `보드` - `보드 매니저` - 검색창에 opti 검색후 나오는 패키지를 설치한다.

## 사용방법

1. 툴 - 보드(optiboot on 28-pin cpus), 프로세서(atmega8), cpu speed(16MHz), 프로그래머(avr isp)로 설정후 스케치를 다운로드 하면 된다.

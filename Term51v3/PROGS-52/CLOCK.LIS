10     REM *******************************
11     REM *    Hintergrund-Uhr mit      *
12     REM *    Watchdog-Timer-Reset     *
13     REM *   Auf P1.2 (PWM) des 80C32  *
14     REM * (C) H.-J. Boehling 24.10.99 *
15     REM *******************************
16     XTAL=11059200 : CLEAR  :  FOR I=0 TO 11 : XBY((0C000H+I))=0 :  NEXT I
17     STRING 100,10 : DAY=1 : WDAY=1 : M=1 : YEAR=0
18     PRINT CHR(12), :  REM Bildschirm loeschen
19    $(1)="Montag" : $(2)="Dienstag" : $(3)="Mittwoch"
20    $(4)="Donerstag" : $(5)="Freitag" : $(6)="Samstag" : $(7)="Sonntag"
25     CLOCK 0 : TIME=0 :  ONTIME 0.1,60000 :  CLOCK 1
30     REM ===== Platz fuer das eigene Programm =
59999  GOTO 30
60000  REM ===== Ontime-Interupt jede Sek. ======
60010 TIME=0 : ONTIME 1,60000 :  REM Neu setzen
61000  REM ----- Watchdog Impuls ----------------
61012 PORT1=223 : PORT1=255
61014  REM ----- Uhr stellen --------------------
61015 I=GET :  IF I>0 THEN  PRINT CHR(7),
61016  PRINT HR,":",MIN,":",S,"Uhr am ",$((WDAY))," den",DAY,".",M,".",YEAR,
61017  PRINT "    ",CHR(13),
61018  IF I=0 GOTO 61035
61019  IF I=72 THEN HR=HR+1
61020  IF I=77 THEN MIN=MIN+1
61021  IF I=83 THEN S=S+1
61022  IF I=84 THEN DAY=DAY+1
61023  IF I=87 THEN WDAY=WDAY+1
61024  IF I=79 THEN M=M+1
61025  IF I=74 THEN YEAR=YEAR+1
61026  IF I=104.AND.HR>0 THEN HR=HR-1
61027  IF I=109.AND.MIN>0 THEN MIN=MIN-1
61028  IF I=115.AND.S>0 THEN S=S-1
61029  IF I=116.AND.DAY>1 THEN DAY=DAY-1
61030  IF I=119.AND.WDAY>1 THEN WDAY=WDAY-1
61031  IF I=111.AND.M>1 THEN M=M-1
61032  IF I=106.AND.YEAR>0 THEN YEAR=YEAR-1
61035  REM ----- Uhrzeit berechnen --------------
61036 S=S+1
61038  IF S>59 THEN S=0 : MIN=MIN+1
61039  IF MIN>59 THEN MIN=0 : HR=HR+1
61050  IF HR>23 THEN HR=0 : WDAY=WDAY+1 : DAY=DAY+1
61060  IF WDAY>7 THEN WDAY=1
61080  IF DAY>29.AND.M=2 THEN DAY=1 : M=M+1
61090  IF DAY=29.AND.M2.AND.(4*INT(YEAR/4)<>YEAR) THEN DAY=1 : M=M+1
61100  IF DAY=31.AND.(M=4.OR.M=6.OR.M=9.OR.M=11) THEN DAY=1 : M=M+1
61110  IF DAY>31 THEN DAY=1 : M=M+1
61120  IF M>12 THEN M=1 : YEAR=YEAR+1
61130  IF YEAR>99 THEN YEAR=0
61140  RETI 

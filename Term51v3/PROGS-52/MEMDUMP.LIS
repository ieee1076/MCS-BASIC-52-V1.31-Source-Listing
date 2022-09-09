10     PRINT CHR(12)
20     PRINT "********************************************"
30     PRINT "*          MEMDUMP  Memory reader          *"
40     PRINT "*       (C) H.-J. Boehling 21.08.99        *"
50     PRINT "*     http://home.nexgo.de/H.Boehling      *"
70     PRINT "********************************************" :  PRINT 
80    Z=0 : CK=0
90     REM ------ Eingabe -----------------------------
100    PRINT "Welcher Speicher soll gelistet werden?" :  PRINT 
110    PRINT " -1-  Interner Speicher"
120    PRINT " -2-  Externer Speicher"
130    PRINT " -3-  Programm Speicher" :  PRINT 
140    INPUT "Ihre Wahl   :",W
150    IF W=1 THEN M=0FFH ELSE M=0FFFFH
160    IF W>3 GOTO 10
170    INPUT "Startadresse:",ST
180    PRINT 
190    REM ------ Ausgabe -----------------------------
200    PRINT CHR(12) :  PRINT " Adr.    ",
210    IF W=3 THEN  PRINT "Code Memory   ",
220    IF W=2 THEN  PRINT "Ext. Memory   ",
230    IF W=1 THEN  PRINT "Int. Memory   ",
240    PRINT "HEX                  ASCII"
250    FOR ADDR=ST TO M STEP 8 : K=0
260    PH1. ADDR, :  PRINT " :",
270    REM ------ Hex-Daten ---------------------------
280    FOR B=0 TO 7
290    IF ADDR+B>M THEN  PRINT "    ", :  GOTO 330
300    IF W=3 THEN  PH0. CBY(ADDR+B),
310    IF W=2 THEN  PH0. XBY(ADDR+B),
320    IF W=1 THEN  PH0. DBY(ADDR+B),
330    NEXT B
340    REM ------ ASCII-Daten -------------------------
350    PRINT " | ",
360    FOR B=0 TO 7
370    IF ADDR+B>M THEN  PRINT " ", :  GOTO 430
380    IF W=3 THEN C=CBY(ADDR+B)
390    IF W=2 THEN C=XBY(ADDR+B)
400    IF W=1 THEN C=DBY(ADDR+B)
410    IF C<32.OR.C>126 THEN C=46
420    PRINT CHR(C),
430    NEXT B
440    PRINT " | "
450    REM ------ Weiter Abfrage ----------------------
460   Z=Z+1
470    IF Z=22 GOSUB 540
480    IF K=ASC(N).OR.K=110 THEN ADDR=M : CK=1
490    IF Z=22 THEN Z=0 :  PRINT 
500    NEXT ADDR
510    IF CK=1 GOTO 10
520    GOSUB 540 :  GOTO 10
530    REM ------ Taste abwarten ----------------------
540   K=GET :  IF K>0 THEN 540
550    PRINT " Weiter? ",
560   K=GET :  IF K=0 THEN 560
570    RETURN 

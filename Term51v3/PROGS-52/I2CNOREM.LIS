10     REM *****************************************
20     REM *  I2C-Communication with MCS-51-BASIC  *
30     REM *   over Ports 1.5 (SCL) and 1.6 (SDA)  *
40     REM *    (no remarks for speed version)     *
50     REM *      (C) H.-J. Boehling 07.29.99      *
60     REM *    http://home.nexgo.de/H.Boehling    *
70     REM *                                       *
80     REM *****************************************
90    CLKL=0DFH : CLKH=20H : DATL=0BFH : DATH=40H
100    REM +++ I2C Test ++++++++++++++++++++++++++++
110    REM This test sends out value 0 to 255 to a PCF8574 and read it back 
120   ADDR=040H :  REM I2C address
130    FOR BYTEOUT=0 TO 255
140    GOSUB 270
150    IF (ACK.OR.OUT)>0 THEN 210
160    GOSUB 310
170    IF (ACK.OR.OUT)>0 THEN 210
180    PRINT "Read back:",BYTEIN
190    NEXT 
200    GOTO 120
210    REM +++ I2C Transmission Error ++++++++++++++
220    GOSUB 630 :  REM Stop condition
230    IF ACK=40H THEN  PRINT "ACK failed!"
240    IF OUT=3 THEN  PRINT "Time out!"
250    GOTO 140
260    REM *** Send Data to I2C ********************
270    GOSUB 570 : BOUT=ADDR.AND.0FEH :  GOSUB 340
280   BOUT=BYTEOUT :  GOSUB 340 :  GOSUB 630
290    RETURN 
300    REM *** Read Data from I2C ******************
310    GOSUB 570 : BOUT=ADDR.OR.1 :  GOSUB 340 :  GOSUB 460 :  GOSUB 630
320    RETURN 
330    REM === I2C Send Byte =======================
340   BIT=80H : WERT=0.5
350    FOR I=1 TO 8
360   SDA=(BOUT.AND.BIT)*WERT : BIT=BIT/2 : WERT=WERT+WERT
370   PT1=PORT1.AND.CLKL : PORT1=PT1 : PT1=PORT1.AND.DATL : PORT1=PT1.OR.SDA
380   PT1=PORT1.OR.CLKH : PORT1=PT1
390    NEXT 
400    REM --- Get ACK -----------------------------
410   PT1=PORT1.AND.CLKL : PORT1=PT1 : PT1=PORT1.OR.DATH : PORT1=PT1
420   PT1=PORT1.OR.CLKH : PORT1=PT1 : ACK=PORT1.AND.DATH
430   PT1=PORT1.AND.CLKL : PORT1=PT1
440    RETURN 
450    REM === I2C Get Byte ========================
460   BYTEIN=0 : WERT=0.5
470    FOR I=1 TO 8
480   PT1=PORT1.AND.CLKL : PORT1=PT1 : PT1=PORT1.OR.DATH : PORT1=PT1
490   PT1=PORT1.OR.CLKH : PORT1=PT1 : SDA=(PORT1.AND.DATH)/WERT
500   BYTEIN=BYTEIN.OR.SDA : WERT=WERT+WERT
510    NEXT 
520    REM --- Do ACK -----------------------------
530   PT1=PORT1.AND.CLKL : PORT1=PT1 : PT1=PORT1.AND.DATL : PORT1=PT1
540   PT1=PORT1.OR.CLKH : PORT1=PT1
550    RETURN 
560    REM === I2C Start condition ================
570   OUT=0 : PT1=PORT1.OR.DATH : PORT1=PT1 : PT1=PORT1.OR.CLKH : PORT1=PT1
580    IF OUT=3 THEN 610 :  REM Wait 3 times for bus free
590    IF (PORT1.AND.60H)<>60H THEN OUT=OUT+1 :  GOTO 580
600   PT1=PORT1.AND.DATL : PORT1=PT1
610    RETURN 
620    REM === I2C Stop condition =================
630   PT1=PORT1.AND.DATL : PORT1=PT1 : PT1=PORT1.OR.CLKH : PORT1=PT1
640   PT1=PORT1.OR.DATH : PORT1=PT1
650    RETURN 

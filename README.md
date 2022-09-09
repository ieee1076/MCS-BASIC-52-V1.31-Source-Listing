'''
;*****************************************************************************
;* OPBYTE 43H for POP from H.-J. Boehling 1/2000                             *
;* e-mail: H-Boehling@gmx.de                                                 *
;*****************************************************************************
;
; A feature of BASIC-52 is the ability to add up to 16 custom keywords
; representing commands or instructions that you define with assembler
; routines. For using system routines in your assembler code there are
; operation bytes (for more information see Intels "MCS BASIC-52 MANUAL").
; In the original souce code is no OPCODE to put a value from argument
; stack and store in a variable.
; With BASIC-52 V1.3 you can use OPBYTE 43H which does the same than the
; "POP" statement.
; (Remarked as Boehling 1)
;
;*****************************************************************************
;* Reset millisecond counter on "TIME=" from H.-J. Boehling 2/2000           *
;*****************************************************************************
;
; The command "TIME=0" now zeros the millisecond register so that TIME
; returns with zero.
; (Remarked as Boehling 2)
;
;*****************************************************************************
;* New command "ERASE" by H.-J. Boehling 2/2000                              *
;*****************************************************************************
;
; To erase an EEPROM (fill 16K byte up to 8000H with 0FFH) the new command
; "ERASE" is implemented. It takes 2 min. and 45 sec. to erase the 16K bytes!
; (Remarked as Boehling 3)
;
;*****************************************************************************
;* Correct "ASC(x)" bug by D. Wulf 2/2000                                    *
;*****************************************************************************
;
; BASIC-51 V1.1 gives erroneous results for the "ASC(x)" funktion if "x" is
; one of the following signs : *, +, -, /, <, =, > or ?.
; BASIC-51 V1.3 returns the correct values.
; (Remarked as Wulf 5)
;
;*****************************************************************************
;*****************************************************************************
; To indicate the new version the start message is changed from
; *MCS-51(tm) BASIC V1.1* to
; *MCS-BASIC-52 V1.31*
;
; H.-J. Boehling, D. Wulf 11/26/2001
;*****************************************************************************
'''

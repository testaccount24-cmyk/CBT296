# CBT296
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 296 IS A SERIES OF UTILITIES FROM MR BRUCE LELAND.        *   FILE 296
//*           THIS FILE IS IN IEBUPDTE SYSIN FORMAT AND CONTAINS:   *   FILE 296
//*                                                                 *   FILE 296
//*     CHANGES: --                                                 *   FILE 296
//*                                                                 *   FILE 296
//*     DSAT and DSATNEW fixed for 8-character TSO prefixes.        *   FILE 296
//*          (z/OS 2.3)                                             *   FILE 296
//*                                                                 *   FILE 296
//*     DSAT modified further by Andreas Freybier.  Bugs fixed.     *   FILE 296
//*          All branch instructions replaced by Jump instructions. *   FILE 296
//*          Detailed changes are commented in the source code.     *   FILE 296
//*                                                                 *   FILE 296
//*     DSATNEW renamed by Sam Golob, because of incompatibility    *   FILE 296
//*          with older versions of PDS 8.6.  Newer version         *   FILE 296
//*          PDS86 -- VERSION 8.6.12.13  SEPTEMBER 15, 2011         *   FILE 296
//*          fixes the incompatibility, but if you have an older    *   FILE 296
//*          PDS, this DSAT would cause problems in formatting LC   *   FILE 296
//*          or LISTC or LISTF.  Therefore to keep it separate,     *   FILE 296
//*          I have renamed it to DSATNEW.                          *   FILE 296
//*                                                                 *   FILE 296
//*     DSAT modified by Andreas Freybier, bug fixed by             *   FILE 296
//*          John Kalinich (08/24/2011).  (called DSATNEW)          *   FILE 296
//*                                                                 *   FILE 296
//*     DSAT fixed by Andreas Freybier to support EAV volumes.      *   FILE 296
//*          (this version is in member DSATNEW, and it needs       *   FILE 296
//*          system macros at the z/OS 1.10 level or higher,        *   FILE 296
//*          to assemble.)  (called DSATNEW)                        *   FILE 296
//*                                                                 *   FILE 296
//*     DSAT additional change by John Kalinich to recognize        *   FILE 296
//*          extended format VSAM datasets.  See member $$NOTE5.    *   FILE 296
//*     email:  John Kalinich <jkalinic@outlook.com>                *   FILE 296
//*                                                                 *   FILE 296
//*     DSAT fixed by Ken Sharpe (see $$NOTE4 in the pds            *   FILE 296
//*             for CBT File 296) to recognize HFS datasets.        *   FILE 296
//*     email:  "Sharpe,Ken"<Ken.Sharpe@okdhs.org>                  *   FILE 296
//*                                                                 *   FILE 296
//*     DSAT enhanced by Andreas Freybier, Apr 2003.                *   FILE 296
//*     email:  Andreas.Freybier@Beiersdorf.com                     *   FILE 296
//*                                                                 *   FILE 296
//*     DVOL fixed by Cary Garrett to account for the length        *   FILE 296
//*     change of the CVAFDSM parameter list.                       *   FILE 296
//*     email:  cogarre@ci.birmingham.al.us                         *   FILE 296
//*                                                                 *   FILE 296
//*     Description of Utilities:                                   *   FILE 296
//*                                                                 *   FILE 296
//*         01. DSAT- THE DSAT COMMAND IS USED TO DISPLAY           *   FILE 296
//*                    ALLOCATION INFORMATION FOR DATA SETS         *   FILE 296
//*                    ON A DIRECT ACCESS DEVICE.                   *   FILE 296
//*                                                                 *   FILE 296
//*                    DSAT WILL SEARCH THE OS CATALOG AND          *   FILE 296
//*                    CVOLS FOR THE ENTRIES FOR THE DATA           *   FILE 296
//*                    SETS SPECIFIED.  ALLOCATION                  *   FILE 296
//*                    INFORMATION WILL BE OBTAINED FROM THE        *   FILE 296
//*                    VOLUME TABLE OF CONTENTS, FORMATTED          *   FILE 296
//*                    AND DISPLAYED.  IF A NAME IS AN INDEX        *   FILE 296
//*                    NAME, ALL DATA SETS BELOW THE INDEX          *   FILE 296
//*                    WILL BE DISPLAYED.                           *   FILE 296
//*                                                                 *   FILE 296
//*                    THE USER MAY BYPASS THE CATALOG              *   FILE 296
//*                    SEARCH BY SUPPLYING THE VOLUME SERIAL        *   FILE 296
//*                    ON WHICH THE DATA SET RESIDES.  THIS         *   FILE 296
//*                    OPTION PERMITS DISPLAYING INFORMATION        *   FILE 296
//*                    FOR UNCATALOGED DATA SETS.                   *   FILE 296
//*                                                                 *   FILE 296
//*                    THE ATTRIBUTES TO BE DISPLAYED MAY BE        *   FILE 296
//*                    SELECTED BY THE USER WHEN HE ENTERS          *   FILE 296
//*                    THE DSAT COMMAND BY SPECIFYING               *   FILE 296
//*                    KEYWORD OPERANDS.                            *   FILE 296
//*                                                                 *   FILE 296
//*                    THE DSAT COMMAND MAY BE USED IN              *   FILE 296
//*                    COMMAND PROCEDURES TO FIND THE               *   FILE 296
//*                    ALLOCATION OF A DATA SET OR A GROUP          *   FILE 296
//*                    OF DATA SETS AND SET THE RETURN CODE         *   FILE 296
//*                    TO THE SPECIFIED VALUE.  THE RETURN          *   FILE 296
//*                    CODE MAY THEN BE TESTED WITH THE WHEN        *   FILE 296
//*                    COMMAND.  OUTPUT MAY BE SUPPRESSED BY        *   FILE 296
//*                    SPECIFYING NOPRINT.                          *   FILE 296
//*                                                                 *   FILE 296
//*                    THE USER MAY CHOOSE WHAT INFORMATION         *   FILE 296
//*                    WILL BE DISPLAYED BY ENTERING                *   FILE 296
//*                    KEYWORDS.                                    *   FILE 296
//*                                                                 *   FILE 296
//*         THE INFORMATION THAT MAY BE DISPLAYED IS:               *   FILE 296
//*                                                                 *   FILE 296
//*           1. VOLUME SERIAL ON WHICH THE DATA SET IS LOCATED.    *   FILE 296
//*           2. FILE SEQUENCE NUMBER.                              *   FILE 296
//*           3. DEVICE TYPE CODE FROM CATALOG ENTRY.               *   FILE 296
//*           4. ALLOCATION  (ALLOCATED, USED, AND EXTENTS).        *   FILE 296
//*           5. SECONDARY ALLOCATION (AMOUNT AND UNITS).           *   FILE 296
//*           6. DATA SET ORGANIZATION.                             *   FILE 296
//*           7. DCB (RECFM, BLKSIZE, AND LRECL).                   *   FILE 296
//*           8. CREATION DATE.                                     *   FILE 296
//*           9. EXPIRATION DATE.                                   *   FILE 296
//*          10. FULLY QUALIFIED DATA SET NAME.                     *   FILE 296
//*          11. CCHHR OF THE FORMAT 1 DSCB.                        *   FILE 296
//*          12. GENERATION DATA GROUP DATA.                        *   FILE 296
//*          13. PDS DIRECTORY INFORMATION.                         *   FILE 296
//*                                                                 *   FILE 296
//*          02. DVOL- THE DVOL COMMAND IS USED TO DISPLAY          *   FILE 296
//*                    THE AMOUNT OF FREE SPACE ON A DIRECT         *   FILE 296
//*                    ACCESS DEVICE.                               *   FILE 296
//*                                                                 *   FILE 296
//*                    DVOL WILL READ THE FORMAT 4 AND              *   FILE 296
//*                    FORMAT 5 DSCB'S FROM THE VTOC OF A           *   FILE 296
//*                    DIRECT ACCESS VOLUME AND DISPLAY:            *   FILE 296
//*                                                                 *   FILE 296
//*                    DVOL UPDATED 09/97 TO RECOGNIZE DYNAMIC      *   FILE 296
//*                    UCB'S.                                       *   FILE 296
//*                                                                 *   FILE 296
//*               1.  VOLUME SERIAL                                 *   FILE 296
//*               2.  UNIT ADDRESS                                  *   FILE 296
//*               3.  MOUNT STATUS                                  *   FILE 296
//*               4.  USE STATUS                                    *   FILE 296
//*               5.  NUMBER OF BLANK DSCB'S IN THE VTOC            *   FILE 296
//*               6.  CONDITION OF THE VTOC INDICATORS BYTE         *   FILE 296
//*               7.  VSAM DATA FIELDS                              *   FILE 296
//*               8.  TOTAL FREE SPACE IN TRACKS                    *   FILE 296
//*               9.  NUMBER OF FREE EXTENTS                        *   FILE 296
//*              10.  NUMBER OF FREE CYLINDERS                      *   FILE 296
//*              11.  SIZE OF LARGEST EXTENTS (UP TO 5) IN          *   FILE 296
//*                   CYLINDERS + TRACKS                            *   FILE 296
//*              12.  SIZE OF LARGEST EXTENTS (UP TO 5) IN TRACKS   *   FILE 296
//*                                                                 *   FILE 296
//*                    THE RETURN CODE IS SET TO THE TOTAL          *   FILE 296
//*                    NUMBER OF TRACKS IN THE LARGEST              *   FILE 296
//*                    EXTENTS (UP TO 5) UP TO A MAXIMUM OF         *   FILE 296
//*                    4095.  IF THE NUMBER OF FREE TRACKS          *   FILE 296
//*                    EXCEEDS 4095, THE RETURN CODE WILL           *   FILE 296
//*                    BE SET TO 4095.  IF MORE THAN ONE            *   FILE 296
//*                    VOLUME IS DISPLAYED, THE RETURN CODE         *   FILE 296
//*                    WILL BE REFER TO THE SPACE ON THE            *   FILE 296
//*                    LAST VOLUME.  IF AN ERROR CONDITION          *   FILE 296
//*                    EXISTS ON THE VOLUME, THE RETURN             *   FILE 296
//*                    CODE WILL BE SET TO 0.                       *   FILE 296
//*                                                                 *   FILE 296
//*                    NOTE - IF AN ERROR CONDITION EXISTS          *   FILE 296
//*                           ON THE VOLUME, THE RETURN             *   FILE 296
//*                           CODE WILL BE SET TO 0.                *   FILE 296
//*                                                                 *   FILE 296
//*          03. RESET    -  PERFORMS THE EQUIVALENT OF A DATASET   *   FILE 296
//*                          SCRATCH FOLLOWED BY A REALLOCATION     *   FILE 296
//*                          IN THE SAME SPACE FOR A PDS. THE       *   FILE 296
//*                          NUMBER OF DIRECTORY BLOCKS CAN BE      *   FILE 296
//*                          CHANGED VIA THE PROGRAM PARM.          *   FILE 296
//*                                                                 *   FILE 296
//*          04. BLKDISK   - SEE BELOW FOR A COMPLETE DESCRIPTION:  *   FILE 296
//*                                                                 *   FILE 296
//*       DESCRIPTION:  THIS PROGRAM COMPUTES AN "OPTIMAL"          *   FILE 296
//*           BLOCKSIZE FOR A DISK OR DRUM DATA SET GIVEN THE       *   FILE 296
//*           LOGICAL RECORD LENGTH.  INPUTS INCLUDE THE LRECL      *   FILE 296
//*           AND OPTIONALLY ANY OF THE FOLLOWING:                  *   FILE 296
//*                                                                 *   FILE 296
//*           A.  A KEY LENGTH (ZERO, FOR NO KEY, IS THE            *   FILE 296
//*               DEFAULT)                                          *   FILE 296
//*           B.  THE NUMBER OF RECORDS IN THE DATA SET (USED       *   FILE 296
//*               FOR AN ALLOCATION COMPUTATION -- 100,000 IS       *   FILE 296
//*               THE DEFAULT)                                      *   FILE 296
//*           C.  THE BLOCKSIZE TO USE FOR THE ALLOCATION           *   FILE 296
//*               COMPUTATION (THE RECOMMENDED BLOCKSIZE VALUE      *   FILE 296
//*               IS THE DEFAULT)                                   *   FILE 296
//*           D.  WHETHER OR NOT TO PROVIDE A TRACK CAPACITY        *   FILE 296
//*               REPORT                                            *   FILE 296
//*           E.  WHETHER OR NOT TO VERIFY RESULTS AGAINST          *   FILE 296
//*               "TRKCALC"                                         *   FILE 296
//*                                                                 *   FILE 296
//*       SUPPORTED DEVICES:  THE NAME BY WHICH THIS COMMAND        *   FILE 296
//*           PROCESSOR IS INVOKED DETERMINES THE DEVICE TYPE       *   FILE 296
//*           TO BE USED.                                           *   FILE 296
//*                                                                 *   FILE 296
//*           THE FIRST THREE CHARACTERS OF THE COMMAND NAME        *   FILE 296
//*           (USUALLY "BLK") ARE IGNORED; THE REMAINING FOUR       *   FILE 296
//*           OR FIVE CHARACTERS ARE COMPARED AGAINST A TABLE       *   FILE 296
//*           OF SUPPORTED DEVICES IN THE PROGRAM.  THE VALID       *   FILE 296
//*           ALIAS NAMES FOR THE PROGRAM INCLUDE THE               *   FILE 296
//*           FOLLOWING:                                            *   FILE 296
//*                                                                 *   FILE 296
//*           A.  BLK23051  (FOR 2305-1 DRUMS)                      *   FILE 296
//*           B.  BLK23052  (FOR 2305-2 DRUMS)                      *   FILE 296
//*           C.  BLK2314   (FOR 2314 DISKS)                        *   FILE 296
//*           D.  BLK3330   (FOR 3330 DISKS)                        *   FILE 296
//*           E.  BLK33301  (FOR 3330 MODEL 11 DISKS)               *   FILE 296
//*           F.  BLK3340   (FOR 3340 DISKS)                        *   FILE 296
//*           G.  BLK3350   (FOR 3350 DISKS)                        *   FILE 296
//*           H.  BLK3375   (FOR 3375 DISKS)                        *   FILE 296
//*           I.  BLK3380   (FOR 3380 DISKS)                        *   FILE 296
//*           J.  BLK3390   (FOR 3390 DISKS)                        *   FILE 296
//*           K.  BLK9345   (FOR 9345 DISKS)                        *   FILE 296
//*                                                                 *   FILE 296
//*          05.  REVIEW - SEE FILE 134 FOR THE LATEST VERSION OF   *   FILE 296
//*               THIS PROGRAM.                                     *   FILE 296
//*                                                                 *   FILE 296
//*          06.  HEL - SEE FILE 134 FOR THE LATEST VERSION OF      *   FILE 296
//*               THIS PROGRAM.  ON FILE 134, HEL IS NOW AN         *   FILE 296
//*               ALIAS OF REVIEW.                                  *   FILE 296
//*                                                                 *   FILE 296
//*          07.  XEQ - A COMMAND PROCESSOR THAT IS DESIGNED TO     *   FILE 296
//*               LOAD AND EXECUTE (ATTACH) A PROGRAM IN ONE OF THE *   FILE 296
//*               SYSTEM LINK LIBRARIES OR A USER LIBRARY (TASKLIB) *   FILE 296
//*               (Fixed for 8-character prefixes, and support      *   FILE 296
//*               info.)                                            *   FILE 296
//*                                                                 *   FILE 296
//*          08   COMPARE - A SOMEWHAT MODIFIED VERSION OF THE      *   FILE 296
//*               YALE COMPARE PROGRAM - fixed by Greg Price        *   FILE 296
//*               to handle pds'es better.                          *   FILE 296
//*                                                                 *   FILE 296
//*          09   RELEASE - A TSO COMMAND TO RELEASE EXCESS SPACE   *   FILE 296
//*               OCCUPIED BY A DATASET.  Load Module for SWA above *   FILE 296
//*               the 16M line, assembled on 04/04/2007 by John     *   FILE 296
//*               Kalinich.  File 035 updated on 03/23/2008 by Sam  *   FILE 296
//*               Golob).  See member $$NOTE1.                      *   FILE 296
//*               (Fixed for 8-character TSO prefixes-z/OS 2.3)     *   FILE 296
//*                                                                 *   FILE 296
```

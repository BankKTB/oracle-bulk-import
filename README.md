@echo off

SET PRJ_DIR=c:\db-import
SET RENAME_SCRIPT=%PRJ_DIR%\sql\rename_table.sql
SET CSV_FILE=%PRJ_DIR%\csv\test.csv
SET CTL_FILE=%PRJ_DIR%\ctl\test.ctl
SET LOG_FILE=%PRJ_DIR%\logs\test.log

::SET TODAY=20200527
set TODAY=%date:~10,4%%date:~4,2%%date:~7,2%
echo %TODAY%
SET TABLE_NAME=T
SET RENAME_SQL=RENAME %TABLE_NAME% TO %TABLE_NAME%_%TODAY%;
echo %RENAME_SQL% > %RENAME_SCRIPT%

:: ----------------------------------------
:: ----------------------------------------

:: echo sqlplus %DB_USER%/%DB_PASS%@%DB_NAME% @%RENAME_SCRIPT%
exit | sqlplus %DB_USER%/%DB_PASS%@%DB_NAME% @%RENAME_SCRIPT%

echo sqlldr userid=%DB_USER%/%DB_PASS%@%DB_NAME% data=%CSV_FILE% control=%CTL_FILE% >> %LOG_FILE%



@echo on

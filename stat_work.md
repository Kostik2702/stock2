[tags]: <> (total, period, stat)
*Total for petiod MAX and AVG*
```sql
SELECT
cast(from_unixtime(Tickets.date) AS DATE) AS TicketDate,
AVG(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'AVG',
MAX(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'MAX'
FROM Tickets
where cast(from_unixtime(Tickets.date) AS DATE) > '2019-06-18'
AND cast(from_unixtime(Tickets.date) AS DATE) < '2019-06-26'
AND cast(from_unixtime(Tickets.date) AS TIME) > '08:00:00'
AND cast(from_unixtime(Tickets.date) AS TIME) < '20:00:00'
AND Tickets.status ='11'
GROUP BY TicketDate
```
[tags-end]: <>

[tags]: <> (enterprise, period, stat)
*SMS Enterprise for period*
```sql
SELECT
cast(from_unixtime(Tickets.date) AS DATE) AS TicketDate,
AVG(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'AVG',
MAX(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'MAX'
FROM Tickets, mmdportal_user
WHERE mmdportal_user.id = Tickets.cuid
AND mmdportal_user.last_name in ('Kovalov', 'Izverskaya', 'Kozko', 'Doroshenko', 'Pankin')
AND cast(from_unixtime(Tickets.date) AS DATE) > '2019-06-18'
AND cast(from_unixtime(Tickets.date) AS DATE) < '2019-06-26'
AND cast(from_unixtime(Tickets.date) AS TIME) > '08:00:00'
AND cast(from_unixtime(Tickets.date) AS TIME) < '20:00:00'
AND Tickets.status ='11'
GROUP BY TicketDate
```
[tags-end]: <>

[tags]: <> (enterprise, urgent, period, stat)
*SMS Enterprise URGENT for period*
```sql
SELECT 
cast(TimeResult.dateData AS DATE) AS TicketDate,
AVG(TimeResult.minutes) AS 'AVG',
MAX(TimeResult.minutes) AS 'MAX'
FROM ( SELECT DISTINCT TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60 AS 'minutes',
from_unixtime(Tickets.date) as DateData
FROM
Tickets, mmdportal_user, TicketTestDataSms
WHERE mmdportal_user.id = Tickets.cuid
AND TicketTestDataSms.ticket_id=Tickets.id
AND TicketTestDataSms.urgent = '1'
AND mmdportal_user.last_name in('Kovalov', 'Izverskaya', 'Kozko', 'Doroshenko', 'Pankin')
AND cast(from_unixtime(Tickets.date) AS DATE) > '2019-06-18'
AND cast(from_unixtime(Tickets.date) AS DATE) < '2019-06-26'
AND cast(from_unixtime(Tickets.date) AS TIME) > '08:00:00'
AND cast(from_unixtime(Tickets.date) AS TIME) < '20:00:00'
AND Tickets.status ='11') AS TimeResult
GROUP BY TicketDate
```
[tags-end]: <>


[tags]: <> (transit, period, stat)
*SMS Transit for period*
```sql
SELECT
cast(from_unixtime(Tickets.date) AS DATE) AS TicketDate,
AVG(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'AVG',
MAX(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'MAX'
FROM Tickets, mmdportal_user
WHERE mmdportal_user.id = Tickets.cuid
AND mmdportal_user.last_name in('Peresunko', 'Chaplyguina', 'Kostyria', 'Goncharenko', 'Sosnova', 'Chobotko')
AND cast(from_unixtime(Tickets.date) AS DATE) > '2019-06-18'
AND cast(from_unixtime(Tickets.date) AS DATE) < '2019-06-26'
AND cast(from_unixtime(Tickets.date) AS TIME) > '08:00:00'
AND cast(from_unixtime(Tickets.date) AS TIME) < '20:00:00'
AND Tickets.status ='11'
GROUP BY TicketDate
```
[tags-end]: <>

[tags]: <> (transit, urgent, period, stat)
*SMS Transit URGENT for period*
```sql
SELECT 
cast(TimeResult.dateData AS DATE) AS TicketDate,
AVG(TimeResult.minutes) AS 'AVG',
MAX(TimeResult.minutes) AS 'MAX'
FROM( SELECT DISTINCT 
TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60 AS 'minutes',
from_unixtime(Tickets.date) as DateData
FROM Tickets, mmdportal_user, TicketTestDataSms
WHERE mmdportal_user.id = Tickets.cuid
AND TicketTestDataSms.ticket_id=Tickets.id
AND TicketTestDataSms.urgent = '1'
AND mmdportal_user.last_name in('Peresunko', 'Chaplyguina', 'Kostyria', 'Goncharenko', 'Sosnova', 'Chobotko')
AND cast(from_unixtime(Tickets.date) AS DATE) > '2019-06-18'
AND cast(from_unixtime(Tickets.date) AS DATE) < '2019-06-26'
AND cast(from_unixtime(Tickets.date) AS TIME) > '08:00:00'
AND cast(from_unixtime(Tickets.date) AS TIME) < '20:00:00'
AND Tickets.status ='11'
) AS TimeResult
GROUP BY TicketDate
```
[tags-end]: <>

[tags]: <> (voice, period, stat)
*Voice key for period*
```sql
SELECT
cast(from_unixtime(Tickets.date) AS DATE) AS TicketDate,
AVG(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'AVG',
MAX(TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60) AS 'MAX'
FROM Tickets, mmdportal_user
WHERE mmdportal_user.id = Tickets.cuid
AND mmdportal_user.last_name in('Kondratenko','Paschenko','Skvortsov','Borodai','Mitrjaeva', 'Zhovnirchyk', 'Ihnatenko', 'Palinka', 'Rogalska', 'Azulay')
AND cast(from_unixtime(Tickets.date) AS DATE) > '2019-06-18'
AND cast(from_unixtime(Tickets.date) AS DATE) < '2019-06-26'
AND cast(from_unixtime(Tickets.date) AS TIME) > '08:00:00'
AND cast(from_unixtime(Tickets.date) AS TIME) < '20:00:00'
AND Tickets.status ='11'
GROUP BY TicketDate
```
[tags-end]: <>

[tags]: <> (voice, urgent, period, stat)
*Voice key URGENT for period*
```sql
SELECT 
cast(TimeResult.dateData AS DATE) AS TicketDate,
AVG(TimeResult.minutes) AS 'AVG',
MAX(TimeResult.minutes) AS 'MAX'
FROM(SELECT DISTINCT
TIME_TO_SEC(TIMEDIFF(ROUND(from_unixtime(Tickets.date_finish),0) , ROUND(from_unixtime(Tickets.date),0)))/60 AS 'minutes',
from_unixtime(Tickets.date) as DateData
FROM Tickets, mmdportal_user, TicketTestData
WHERE mmdportal_user.id = Tickets.cuid
AND TicketTestData.ticket_id=Tickets.id
AND TicketTestData.urgent = '1'
and mmdportal_user.last_name in('Kondratenko','Paschenko','Skvortsov','Borodai','Mitrjaeva', 'Zhovnirchyk', 'Ihnatenko', 'Palinka', 'Rogalska', 'Azulay')
AND cast(from_unixtime(Tickets.date) AS DATE) > '2019-06-18'
AND cast(from_unixtime(Tickets.date) AS DATE) < '2019-06-26'
AND cast(from_unixtime(Tickets.date) AS TIME) > '08:00:00'
AND cast(from_unixtime(Tickets.date) AS TIME) < '20:00:00'
AND Tickets.status ='11') AS TimeResult
GROUP BY TicketDate
```
[tags-end]: <>

[tags]: <> (testers,day, stat)
*TESTS per TESTER FOR DAY*
```sql 
SELECT (USERS.last_name ) AS TESTER_SURNAME, (USERS.first_name ) AS TESTER_NAME, VoiceTestsTable.Count AS VOICE, 
SMSTestsTable.Count AS SMS, (VoiceTestsTable.Count + SMSTestsTable.Count) AS TOTAL FROM mmdportal_user AS USERS

JOIN (
	
	SELECT COUNT(VoiceTests.id) AS Count, MMDUSER.last_name AS LAST_NAME
	FROM  mmdportal_user AS MMDUSER
	LEFT JOIN TicketTestData AS VoiceTests
	ON VoiceTests.assigned = MMDUSER.id
	AND VoiceTests.assigned=MMDUSER.id
	AND date (from_unixtime(VoiceTests.date_finish)) = '2019-10-28'
	AND hour(from_unixtime(VoiceTests.date_finish)) > '06:00:00'
	AND hour(from_unixtime(VoiceTests.date_finish)) < '20:00:01'

	where MMDUSER.last_name IN('Konstantin', 'Matros','Nedopako','Shylova','Sachuk','Stepanov','Noskova','Litachevskyi', 'Tyndyryka')
	GROUP BY LAST_NAME
) AS VoiceTestsTable
ON VoiceTestsTable.LAST_NAME = USERS.last_name
 
JOIN(
	SELECT COUNT(SMSTests.id) AS Count, MMDUSER.last_name AS LAST_NAME
	FROM  mmdportal_user AS MMDUSER
	LEFT JOIN TicketTestDataSms AS SMSTests
	ON SMSTests.assigned = MMDUSER.id
	AND SMSTests.assigned=MMDUSER.id
	AND date (from_unixtime(SMSTests.date_finish)) = '2019-10-28'
	AND hour(from_unixtime(SMSTests.date_finish)) > '06:00:00'
	AND hour(from_unixtime(SMSTests.date_finish)) < '20:00:01'

	where MMDUSER.last_name IN('Konstantin', 'Matros','Nedopako','Shylova','Sachuk','Stepanov','Noskova','Litachevskyi', 'Tyndyryka')
	GROUP BY LAST_NAME
) AS SMSTestsTable
ON SMSTestsTable.LAST_NAME = USERS.last_name

group by TESTER_SURNAME
```
[tags-end]: <>

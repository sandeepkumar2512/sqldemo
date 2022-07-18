# sqldemo
#Find person having odd/even person id

SELECT * FROM PERSON_ALIAS WHERE MOD(PERSON_ID,2)=0

#Find person having duplicate person id

SELECT p.PERSON_ID,count(1) FROM PERSON_ALIAS p
GROUP BY p.PERSON_ID 
HAVING COUNT(PERSON_ID) > 1   

#Find person and sum of its alias id

SELECT PERSON_ID, SUM(PERSON_ALIAS_ID)  FROM PERSON_ALIAS
GROUP BY PERSON_ID 
HAVING MOD(PERSON_ID,2)=0

#Find persons with 6th highest person id

SELECT * FROM PERSON_ALIAS 
WHERE PERSON_ID = (
  SELECT t.max_person_id 
  FROM (SELECT MAX(PERSON_ID) AS max_person_id 
        FROM PERSON_ALIAS 
        GROUP BY PERSON_ID 
        ORDER BY PERSON_ID DESC 
        FETCH FIRST 6 ROWS ONLY) t 
  ORDER BY t.max_person_id ASC 
  FETCH FIRST 1 ROW ONLY
)



##Installing mysql server from zipped file
# download mysql zipped file
# extract is in any location e.g C:\sandeep\devenv\mysql-8.0.29-winx64
# add C:\sandeep\devenv\mysql-8.0.29-winx64\bin to system variable
# create folder with name "data" under C:\sandeep\devenv\mysql-8.0.29-winx64\
# from cmd, run 
  >mysqld --initialize --console => to initialize
  >mysqld --console => to start server

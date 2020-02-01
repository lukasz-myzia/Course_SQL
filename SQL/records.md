CREATE INDEX my_index
ON nazwa_tabeli (nazwa_kolumny_1, nazwa_kolumny_2)

DROP INDEX my_index;

1. Wyświetl imion i nazwisk wszystkich pracowników z tabeli employees.
	SELECT first_name AS imie,
	last_name AS nazwisko
	FROM employees;

2. Wyświetlić imiona i nazwiska pracowników, których imiona i nazwiska zaczynają się na literę B (uniezależnić się od wielkości znaków w bazie)
	SELECT first_name as imie, last_name as nazwisko
	from employees
	where upper(last_name) like upper('_E%');

3. Wyświetl imiona, nazwiska i wynagrodzenia pracowników, którzy zarabiają powyżej 10000.
	SELECT first_name as imie, last_name as nazwisko, salary as wynagrodzenie
	from employees
	where salary >1000
	ORDER BY 3;

4. Wyświetl imiona i nazwiska i wynagrodzenia pracowników, którzy zarabiają powyżej od 2000-6000 i uszeregować malejąco według wynagrodzeń.
	SELECT first_name as imie, last_name as nazwisko, salary as wynagrodzenie
	from employees
	where salary BETWEEN 2000 and 6000
	ORDER BY 3 DESC;

5. Wyświetlić liczbę pracowników minimalne, maksymalne i średnie wynagrodzenie w zaokrągleniu do pełnej liczby.
	SELECT count (*) as liczba_prac,
	min(salary) as minimalne,
	round(avg(salary),3) as srednie
	from employees;

1. Wyświetlić liczbę pracowników minimalna maksymalna i średnia pensje w poszczególnych działach. uszeregować malejącej wg średniego wynagrodzenia
	select department_id,count(*) liczba,
	min(salary) min,
	max(salary) max,
	round(avg(salary),0) avg
	from employees
	group by department_id
	order by 5 desc;

2. Wyświetlić liczbę pracowników których średnia płaca jest większa lub równa 10000 sortując
	select department_id, count(*) liczba,
	min(salary) min,
	max(salary) max,
	round(avg(salary),0) avg
	from employees
	group by department_id
	having avg(salary)>=10000
	order by 5 desc;

3. Wyświetlić imiona i nazwiska oraz ich nazwy w systemie komputerowym pracowników. NAZWY pisane dużymi literami pierwsze 5 nazwiska i 3 pierwsze litery imienia.
	select first_name,last_name,
	upper(substr(last_name,1,5)||substr(first_name,1,3)) as LOGIN
	from employees;
	
4. Wyświetlić częstość występowania imion wśród pracowników i uszeregować wg malejąco tej częstości.
	select first_name imie,
	count(*) czestosc 
	from employees
	group by first_name
	order by 2 desc;

5. Polecenie jw. tylko te imiona które występują więcej niż jeden raz.
	select first_name imie,
	count(*) czestosc
	from employees
	group by first_name
	having count(*)>1
	order by 2 desc;

6. Wyświetlić częstość występowania nazwisk na dana literę i uszeregować malejąco tylko te litery na które nazwiska występują więcej jak jeden raz.
	select substr(last_name,1,1) znak,
	count(*) czestosc
	from employees
	group by substr(last_name,1,1)
	having count(*)>1
	order by 2 desc;

7. Wyświetlić imię i nazwisko oraz nazwę działu w którym pracuje osoba.
	select first_name, last_name, department_name
	from employees, departments
	where employees.department_id=departments.department_id;
	
1. Produkt kartezjański
	SELECT
	P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	D.DEPARTMENT_NAME AS NAZWA
	FROM EMPLOYEES P,DEPARTMENTS D;

2. Wyświetlić imiona i nazwiska pracowników oraz nazwy działów, w których pracują.
	SELECT
	P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	D.DEPARTMENT_NAME AS NAZWA
	FROM EMPLOYEES P,DEPARTMENTS D
	WHERE p.department_id = d.department_id;
	
3. Wyświetlić imiona i nazwiska pracowników ,nazwy ich stanowisk oraz nazwy działów, w których pracują.
	SELECT
	P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	D.DEPARTMENT_NAME AS NAZWA,
	S.JOB_TITLE
	FROM EMPLOYEES P,DEPARTMENTS D,JOBS S
	WHERE P.DEPARTMENT_ID=D.DEPARTMENT_ID
	AND P.JOB_ID=S.JOB_ID;

4. Wyświetlić imiona i nazwiska pracowników oraz nazwy działów, w których pracują. Należy uwzględnić tylko pracowników z przypisanymi działami i działy, do których są przypisani pracownicy
	SELECT
	P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	D.DEPARTMENT_NAME AS NAZWA
	FROM EMPLOYEES P INNER JOIN DEPARTMENTS D
	ON P.DEPARTMENT_ID=D.DEPARTMENT_ID;

5. Wyświetlić imiona i nazwiska pracowników , nazwy ich stanowisk oraz nazwy działów, w których pracują. Należy uwzględnić tylko pracowników z przypisanymi działami i działy, do których są przypisani pracownicy oraz stanowiska z przypisanymi pracownikami
	SELECT D.DEPARTMENT_NAME AS NAZWA,
	P.FIRST_NAME IMIE,
	P.LAST_NAME AS NAZWISKO,
	S.JOB_TITLE AS NAZWA
	FROM DEPARTMENTS D
	INNER JOIN (EMPLOYEES P INNER JOIN JOBS S
		ON P.JOB_ID=S.JOB_ID)
	ON P.DEPARTMENT_ID=D.DEPARTMENT_ID;

6. Wyświetlić imiona i nazwiska pracowników oraz nazwy działów, w których pracują. Należy uwzględnić tylko pracowników z przypisanymi i nieprzypisanymi działami oraz działy, do których są przypisani pracownicy
	SELECT P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	D.DEPARTMENT_NAME AS NAZWA
	FROM EMPLOYEES P
	LEFT JOIN DEPARTMENTS D
	ON P.DEPARTMENT_ID=D.DEPARTMENT_ID;
	
7. Wyświetlić imiona i nazwiska pracowników oraz nazwy działów, w których pracują. Należy uwzględnić tylko pracowników z przypisanymi działami oraz działy, do których są i nie są przypisani pracownicy.
	SELECT P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	D.DEPARTMENT_NAME AS NAZWA
	FROM EMPLOYEES P RIGHT JOIN DEPARTMENTS D
	ON P.DEPARTMENT_ID=D.DEPARTMENT_ID;

1.
2. Wyświetlić imiona i nazwiska pracowników pracujących w działach 50 oraz 70 (Unie - suma zbiorów)
	SELECT P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	P.DEPARTMENT_ID AS DZIAL
	FROM EMPLOYEES P
	WHERE P.DEPARTMENT_ID=50
	UNION SELECT P.FIRST_NAME AS IMIE,
	P.LAST_NAME AS NAZWISKO,
	P.DEPARTMENT_ID AS DZIAL
	FROM EMPLOYEES P
	WHERE P.DEPARTMENT_ID =70;

3. Wyświetlić wartości wynagrodzeń, które występują w dziale 30 i nie występują w dziale 50
	SELECT SALARY
	FROM EMPLOYEES
	WHERE DEPARTMENT_ID=30
	MINUS SELECT SALARY
	FROM EMPLOYEES WHERE DEPARTMENT_ID=50;

4. Wyświetlić hierarchiczną zależność pracownik – manager w tabeli EMPLOYEES
	SELECT EMPLOYEE_ID "ID PRACOWNIKA",
	LAST_NAME AS "NAZWISKO PRACOWNIKA",
	MANAGER_ID "ID KIEROWNIKA"
	FROM EMPLOYEES
	CONNECT BY PRIOR EMPLOYEE_ID = MANAGER_ID;

5. Wyświetlić hierarchiczną zależność pracownik – manager w tabeli EMPLOYEES pokazując dodatkowo poziom zagnieżdżenia
	SELECT EMPLOYEE_ID "ID PRACOWNIKA",
	LAST_NAME AS "NAZWISKO PRACOWNIKA",
	MANAGER_ID "ID KIEROWNIKA",
	LEVEL AS "POZIOM ZAGNIEZDZENIA"
	FROM EMPLOYEES
	CONNECT BY PRIOR EMPLOYEE_ID = MANAGER_ID;

6. Wyświetlić hierarchiczną zależność pracowników manager w tabeli pokazując dodatkowo ścieżkę zależności managerów począwszy od pracownika o identyfikatorze 100
	SELECT EMPLOYEE_ID "ID PRACOWNIKA",
	LAST_NAME AS "NAZWISKO PRACOWNIKA",
	MANAGER_ID "ID KIEROWNIKA",
	LEVEL AS "POZIOM ZAGNIEZDZENIA",
	SYS_CONNECT_BY_PATH(LAST_NAME, '/')"SCIEZKA"
	FROM EMPLOYEES
	CONNECT BY PRIOR EMPLOYEE_ID = MANAGER_ID
	START WITH
	EMPLOYEE_ID = 100;

1. Tworzenie tabeli KIERUNKI
	CREATE TABLE KIERUNKI
	(NR NUMBER(4) PRIMARY KEY,
	NAZWA VARCHAR2(25) NOT NULL);

2. Tworzenie tabeli ADRESY
	CREATE TABLE ADRESY
	(NR NUMBER(4) PRIMARY KEY,
	ULICA VARCHAR2(30) NOT NULL,
	NR_DOMU VARCHAR2(30) NOT NULL,
	NR_LOKALU VARCHAR2(30),
	MIEJSCOWOSC VARCHAR2(30) NOT NULL,
	KOD_POCZTOWY VARCHAR2(6) NOT NULL);

3. Tworzenie tabeli STUDENT
	CREATE TABLE STUDENT
	(NR VARCHAR2(4) PRIMARY KEY,
	IMIE VARCHAR2(15) NOT NULL,
	NAZWISKO VARCHAR2(20) NOT NULL,
	KIERUNKI NUMBER(4) REFERENCES KIERUNKI(NR),
	ADRES NUMBER(4) REFERENCES ADRESY(NR));

4. Tworzenie tabeli PRACOWNIK
	CREATE TABLE PRACOWNIK
	(NR NUMBER(4) PRIMARY KEY,
	IMIE VARCHAR2(15) NOT NULL,
	NAZWISKO VARCHAR2(20) NOT NULL,
	WYNAGRODZENIE NUMBER(6,2),
	CONSTRAINT PRACOWNIK_WYNAGRODZENIE CHECK(WYNAGRODZENIE>0),
	ADRES NUMBER(4) REFERENCES ADRESY(NR));

5. Tworzenie tabeli DZIAŁY
	CREATE TABLE DZIALY
	(NR NUMBER(4),
	NAZWA VARCHAR2(20) NOT NULL);
	
6. Dodanie pola do tabeli STUDENT
	ALTER TABLE STUDENT
	ADD (DATA_URODZENIA DATE);

7. Dodanie wymuszenia do tabeli DZIALY
	ALTER TABLE DZIALY
	ADD PRIMARY KEY (NR);

8. Dodanie wymuszenia do tabeli PRACOWNIK
	ALTER TABLE PRACOWNIK
	ADD DZIAL NUMBER(4) REFERENCES DZIALY(NR);
	
9. Modyfikacja pola tabeli STUDENT
	ALTER TABLE STUDENT
	MODIFY (DATA_URODZENIA NOT NULL);

10. Usuwanie pola tabeli STUDENT
	ALTER TABLE STUDENT
	DROP COLUMN DATA_URODZENIA;

11. Zmiana nazwy pola w tabeli STUDENT
	ALTER TABLE STUDENT
	RENAME COLUMN NR TO ID;

12. Modyfikacja wymuszenia w tabeli PRACOWNIK
	ALTER TABLE PRACOWNIK
	MODIFY PRIMARY KEY DISABLE;

13. Usuwanie wymuszenia z tabeli DZIALY
	ALTER TABLE DZIALY
	DROP PRIMARY KEY;

14. Usuwanie tabeli kierunki z klauzula CASCADE CONSTRAINS
	DROP TABLE KIERUNKI CASCADE CONSTRAINTS;

15. Tworzenie sekwencji
	CREATE SEQUENCE NR_PRAC;

16. Tworzenie wyzwalacza dla tabeli PRACOWNIK
	CREATE OR REPLACE TRIGGER T_PRACOWNIK
	BEFORE INSERT ON PRACOWNIK
	FOR EACH ROW
	BEGIN
	IF :new.nr IS NULL THEN
	SELECT NR_PRAC.nextval
	INTO :new.nr FROM DUAL;
	END IF;
	END;

1. Wykorzystanie atrybutu %type
	DECLARE
	imie_pracownika VARCHAR2(20) :='Jan';
	upper_name imie_pracownika%TYPE := UPPER(imie_pracownika);
	lower_name imie_pracownika%TYPE := LOWER(imie_pracownika);
	init_name imie_pracownika%TYPE := INITCAP(imie_pracownika);
	BEGIN
	DBMS_OUTPUT.PUT_LINE(imie_pracownika);
	DBMS_OUTPUT.PUT_LINE(upper_name);
	DBMS_OUTPUT.PUT_LINE(lower_name);
	DBMS_OUTPUT.PUT_LINE(init_name);
	END;

2. Wykorzystanie atrybutu %ROWTYPE
	DECLARE
	rekord_pracownika EMPLOYEES%ROWTYPE;
	BEGIN
	SELECT*INTO rekord_pracownika FROM EMPLOYEES WHERE ROWNUM <2;
	DBMS_OUTPUT.PUT_LINE(rekord_pracownika.last_name);
	END;

3. Wyświetlenie danych pracownika przy pomocy procedury PL/SQL
	DECLARE
	SUBTYPE TImiePracownika IS EMPLOYEES.FIRST_NAME%TYPE;
	SUBTYPE TNazwiskoPracownika IS EMPLOYEES.LAST_NAME%TYPE;
	SUBTYPE TNumerPracownika IS EMPLOYEES.EMPLOYEE_ID%TYPE;
	pracownik_nr TNumerPracownika;
	first_name TImiePracownika;
	last_name TNazwiskoPracownika;
	PROCEDURE get_imie_nazwisko(nrprac TnumerPracownika, imieprac OUT TImiePracownika, nazwiskoprac OUT TNazwiskoPracownika)
	IS
	BEGIN
	SELECT last_name, first_name INTO imieprac, nazwiskoprac
	FROM employees
	WHERE employee_ID=nrprac;
	END get_imie_nazwisko;
	BEGIN
	pracownik_nr:=200;
	get_imie_nazwisko(pracownik_nr,first_name,last_name);
	DBMS_OUTPUT.PUT_LINE('Nr='||pracownik_nr);
	DBMS_OUTPUT.PUT_LINE('Imie='||first_name);
	DBMS_OUTPUT.PUT_LINE('Nazwisko='||last_name);
	END;

4. Wykorzystanie instrukcji for loop do odczytania kursora.
	BEGIN
	FOR prac IN(SELECT * FROM employees
	WHERE ROWNUM<10 ORDER BY employee_id)
	LOOP
	DBMS_OUTPUT.PUT_LINE('Nr = '||prac.employee_id);
	DBMS_OUTPUT.PUT_LINE('Imie = '||prac.last_name);
	DBMS_OUTPUT.PUT_LINE('Nazwisko = '||prac.first_name);
	END LOOP;
	END;
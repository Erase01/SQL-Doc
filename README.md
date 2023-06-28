# SQL-Doc
### Documentation of the most important sql statements

---
#### Als Grundlage der Documentation dient das RDBMS Postgresql

\
**CREATE TABLE:**

```sql
CREATE TABLE asdf               -- erstellen einer neuen Tabelle
(ID int, firstname VARCHAR(255));
```

**Constrains:**

```sql
CREATE TABLE Rechnung
(
RID int NOT NULL UNIQUE,                        -- Unique heißt, dass der Wert nur einmal vergeben werden darf
CustomerID int,
Betrag int NOT NULL,				-- Not Null heißt, dass die Werte in diesem column immer angegeben werden muessen
ZusatzID int NOT NULL SERIAL,			-- SERIAL generiert automatisch einzigartige integer Zahlen
PRIMARY KEY(RID),				-- ein column kann als Primary Key angegeben werden um nach diesem zu mappen/sortieren. Der Primary Key ist zudem unique
FOREIGN KEY(CustomerID) REFERENCES asdf(ID)     -- mit dem Foreign key, kann man auf ein column in einer anderen Tabelle referenzieren
);
```

**DROP TABLE:**

```sql
DROP TABLE asdf                -- entfernen einer Tabelle
```

**Tabelle anzeigen:**

```sql
SELECT table_name 
FROM information_schema.tables                -- alle bestehenden Tabellen anzeigen
WHERE table_schema = 'public'

\dt                                           -- weitere Möglichkeit in Postgresql
```

**Datentypen:**

```sql
CREATE TABLE asdf
			(
			int			-- ganze Zahlenwerte
			DECIMAL(9,2)		-- Kommazahlen mit max. 7 Vorkommastellen und 2 Nachkommastellen - also insgesamt 9 Stellen  
			VARCHAR(255)		-- länge eines Namens/Wortes anhand der Anzahl der Buchstaben 
			BOOLEAN 		-- TRUE oder FALSE Werte 
			VARBINARY(255)		-- Anzahl an Bits ohne feste Größe bis 255 
			)
```

**Werte in column einfügen:**

```sql
INSERT INTO asdf
VALUES (23, 'firstname', 'lastname', 'street', 'city')
```

**Werte in column verändern:**

```sql
UPDATE asdf
SET Street = 'streetname'
WHERE ...
```

**Werte in column löschen:**

```sql
DELETE FROM asdf
WHERE ...
```

**SELECT Arten:**

```sql
SELECT * FROM asdf                                 -- Ausgabe der gesamten(*) Tabelle 

SELECT DISTINCT firstname FROM asdf                -- gibt Werte (wenn doppelt) nur einmal aus 
```

**WHERE:**

```sql
SELECT * FROM asdf		-- Für eine spezifiziertere Ausgabe 
WHERE ID = 23
```

**AND:**

```sql
SELECT * FROM asdf
WHERE ID = 23 AND firstname = 'jklö'                -- beide Werte muessen fuer eine erfolgreiche Ausgabe zutreffen
```

**OR:**

```sql
SELECT * FROM asdf
WHERE ID = 23 OR name = 'jklö'               -- mindestens einer der beiden Werte muss fuer eine erfolgreiche Ausgabe zutreffen 
```

**ORDER BY:**

```sql
SELECT * FROM asdf				
WHERE ID >= 23                -- sortiert nach dem column name, aufsteigend (ASC = Ascending) oder absteigend (DESC = Descending)
ORDER BY firstname (ASC/ DESC)
```

**LIMIT:**

```sql
SELECT * FROM asdf                -- gibt eine definierte Anzahl an Werten aus 
LIMIT 5						
```

**LIKE:**

```sql
SELECT * FROM asdf                -- kann benutzt werden um nach Werten mit bestimmten Parametern wie Buchstaben, Zahlen oder Sonderzeichen zu filtern
WHERE fistname LIKE '%l_'         -- der '_' ersetzt dabei ein Zeichen und das '%' ersetzt mehrere.     
				  -- falls ein Unterstrich oder ein Prozentzeichen im Wert enthalten ist, muss es mit einem '\' maskiert werden
```

**NULL:**

```sql
SELECT * FROM asdf
WHERE lastname IS (NOT) NULL                -- Möglichkeit Werte auf Null bzw. auf nicht Null zu prüfen
```

**IN:**

```sql
SELECT * FROM asdf
WHERE firstname IN                -- Möglichkeit Werte tabellenübergreifend auszugeben  
		(SELECT firstname FROM asdf
		 WHERE ID = 23)
```

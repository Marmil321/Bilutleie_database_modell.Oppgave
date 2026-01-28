### SQL Script:
```sql
CREATE TABLE `kunde` (
  `id` INT AUTO_INCREMENT,
  `navn` VARCHAR(100),
  `telefon_nummer` VARCHAR(20),
  `email` VARCHAR(255),
  PRIMARY KEY (`id`)
);

CREATE TABLE `ekstra_utstyr` (
  `id` INT AUTO_INCREMENT,
  `navn` VARCHAR(255),
  `kostnad` DECIMAL(50,2),
  PRIMARY KEY (`id`)
);

CREATE TABLE `bil` (
  `id` INT AUTO_INCREMENT,
  `register_nummer` VARCHAR(50) UNIQUE,
  `merke` VARCHAR(100),
  `modell` VARCHAR(50),
  `årsmodell` VARCHAR(20),
  `dagspris` DECIMAL(50,2),
  PRIMARY KEY (`id`)
);

CREATE TABLE `utleie_avtale` (
  `id` INT AUTO_INCREMENT,
  `kunde_id` INT NOT NULL,
  `bil_id` INT NOT NULL,
  `startdato` DATETIME NOT NULL,
  `sluttdato` DATETIME NOT NULL,
  `total_pris` DECIMAL(50,2),
  `ekstra_utstyr_id` INT NOT NULL,
  PRIMARY KEY (`id`)
);
```
---
__For å legge til et forhold mellom tabellene trenger vi også:__

```sql
ALTER TABLE utleie_avtale
ADD CONSTRAINT fk_kunde
FOREIGN KEY (kunde_id) REFERENCES kunde(id)

ALTER TABLE utleie_avtale
ADD CONSTRAINT fk_bil
FOREIGN KEY (bil_id) REFERENCES bil(id)

ALTER TABLE utleie_avtale
ADD CONSTRAINT fk_ekstra_utstyr
FOREIGN KEY (ekstra_utstyr_id) REFERENCES ekstra_utstyr(id)
```
---
### Test Data
For å legge til Test data can du kjøre:
```sql
INSERT INTO kunde (navn, telefon_nummer, email)
VALUES 
  ('Per', '12345678', 'per@example.com'),
  ('Pål', '87654321', 'pål@example.com'),
  ('Espen', '11223344', 'espen@example.com');

SELECT * FROM kunde;
```
**Output:**
```shell
+----+---------------+----------------+------------------+
| id | navn          | telefon_nummer | email            |
+----+---------------+----------------+------------------+
|  1 | Per           | 12345678       | per@example.com  |
|  2 | Pål           | 87654321       | pål@example.com  |
|  3 | Espen         | 11223344       | espen@example.com|
+----+---------------+----------------+------------------+
```

# lolzCREATE TABLE test_varchar
(
  idt  INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
  vch1 VARCHAR(50) NOT NULL,
  vch2 VARCHAR(50) NOT NULL,
  vch3 VARCHAR(50) NOT NULL,
  vch4 VARCHAR(50) NOT NULL,
  vch5 VARCHAR(50) NOT NULL,
  vch6 VARCHAR(50) NOT NULL,
  vch7 VARCHAR(50) NOT NULL
);

INSERT INTO test_varchar(vch1, vch2, vch3, vch4, vch5, vch6, vch7) VALUES('123456789', 'AbCdEfGh', '1a2b3c4d', 'teste_string', 'XYZ', 'SAIRAM O TIO E OITO MARIAS', 'sem vogais'),
('987654321', 'Um teste Brasil', 'Corcel 2', 'qtd_estoque', 'ABC', 'O CÉU SUECO', 'abcdario'),
('591034656', 'Atrás do morro', 'Fiat 500', 'nome_principal', 'AEI', 'A TORRE DA DERROTA', 'romana');

SELECT * FROM test_varchar;

#EX1

  SELECT vch1, CONCAT( LEFT(vch1, 4), '/', MID(vch1, 5, 4), '-', RIGHT(vch1, 1)) AS 'EX1' FROM test_varchar;

#EX2



  DELIMITER $$

    CREATE FUNCTION funcao(vch2 VARCHAR(50))

    returns varchar(50)

    BEGIN

      DECLARE x INT;
      DECLARE s varchar(50);
      SET x=1;
      SET s = '';

      WHILE x<=LENGTH(vch2) DO
      IF SUBSTR(vch2, x, 1) = UPPER(SUBSTR(vch2, x, 1)) THEN
      SET s=CONCAT(s, LOWER(SUBSTR(vch2, x, 1)));
      SET x=x+1;
      END IF;
      IF SUBSTR(vch2, x, 1) = LOWER(SUBSTR(vch2, x, 1)) THEN
      SET s=CONCAT(s, UPPER(SUBSTR(vch2, x, 1)));
      SET x=x+1;
      END IF;
    END WHILE;

    return s;

    END $$

  DELIMITER;

  SELECT funcao(vch2);


#EX3
SELECT vch3, REPLACE( REPLACE( REPLACE( REPLACE( REPLACE( REPLACE (REPLACE( REPLACE( REPLACE( REPLACE(vch3,'0',''),'1',''),'2',''),'3',''),'4',''),'5',''),'6',''),'7',''),'8',''),'9','') FROM test_varchar;

#EX4

#EX5
  SELECT vch5, CONCAT(REPEAT(SUBSTRING(vch5, 1, 1), 3), REPEAT(SUBSTRING(vch5, 2, 1), 3), REPEAT(SUBSTRING(vch5, 3, 1), 3)) FROM test_varchar;

#EX6

  DELIMITER $$

    CREATE FUNCTION funcao(vch6 VARCHAR(50))

    returns varchar(50)
    BEGIN
    return REVERSE(REPLACE( REPLACE (REPLACE( REPLACE( REPLACE( REPLACE(vch6,'R',''),'M',''),'S',''),'D',''),'T',''),'C',''));

    END $$

  DELIMITER;



#EX7
SELECT vch7, REPLACE( REPLACE( REPLACE( REPLACE( REPLACE(vch7,'a',''),'e',''),'i',''),'o',''),'u','') FROM test_varchar;

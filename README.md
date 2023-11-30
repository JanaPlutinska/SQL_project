-- Vytvorte dátový model pre systém elekronického obchodu predaja
-- športových potrieb. Pri každom tovare je potrebné evidovať presný
-- názov, krajinu pôvodu, druh tovaru, cenu a stav spracovania
-- objednávky. Systém bude evidovať aj osobnné údaje zákazníkov portálu.
-- Pomocou tohto systému  bude možné objednať si napríklad korčule a 
-- prilbu pre ľadový hokej, ale aj outdoorové či trekingové dámske športové
-- oblečenie. Systém bude poskytovať aj sumárne výkazy predaja jednotlivých 
-- tovarov za zvolené obdobie alebo sumárny mesačný či týždenný predaja
-- tovarov.




CREATE DATABASE sportovy_obchod;

CREATE TABLE mesto
(
   id      SERIAL,
   nazov   VARCHAR (50),
   PSC     CHAR (5),
PRIMARY KEY (id)
);

CREATE TABLE zakaznici
(
   id         SERIAL,
   meno       VARCHAR (20),
   priezvisko VARCHAR (50),
   tel_cislo  CHAR (10),
   email      VARCHAR (50),
   id_mesto   INTEGER,
   ulica      VARCHAR (20),
   cislo      VARCHAR (10),
PRIMARY KEY (id),
FOREIGN KEY (id_mesto) REFERENCES mesto (id) ON UPDATE CASCADE ON DELETE CASCADE
);

CREATE TABLE tovar
(
   id              SERIAL,
   druh_tovaru     VARCHAR (50),
   nazov           VARCHAR (50),
   krajina_povodu  VARCHAR (20),
   cena            DECIMAL (10,2),
PRIMARY KEY (id)
);

CREATE TABLE objednavky
(
   id           SERIAL,
   id_zakaznici INTEGER,
   cislo_faktury VARCHAR (50),
   id_tovar     INTEGER,
   pocet_kusov  INTEGER,
   predajna_cena DECIMAL (10,2),
   datum         DATE,
PRIMARY KEY (id),
FOREIGN KEY (id_zakaznici) REFERENCES zakaznici (id) ON UPDATE CASCADE ON DELETE CASCADE,
FOREIGN KEY (id_tovar) REFERENCES tovar (id) ON UPDATE CASCADE ON DELETE CASCADE
);

-- VKLADANIE UDAJOV

INSERT INTO mesto (id, nazov, PSC)
VALUES
(nextval(‘mesto_id_seq‘), ‘Zilina 1‘, ‘01001‘),
(nextval(‘mesto_id_seq‘), ‘Zilina 4‘, ‘01004‘),
(nextval(‘mesto_id_seq‘), ‘Cadca‘, ‘02201‘),
(nextval(‘mesto_id_seq‘), ‘Ruzomberok‘, ‘04401‘),
(nextval(‘mesto_id_seq‘), ‘Kosice‘, ‘04018‘),
(nextval(‘mesto_id_seq‘), ‘Banska Bystrica‘, ‘97401‘),
(nextval(‘mesto_id_seq‘), ‘Namestovo‘, ‘02901‘),
(nextval(‘mesto_id_seq‘), ‘Poprad 1‘, ‘05801‘),
(nextval(‘mesto_id_seq‘), ‘Trnava‘, ‘91701‘),
(nextval(‘mesto_id_seq‘), ‘Liptovsky Mikulas‘, ‘03101‘),
(nextval(‘mesto_id_seq‘), ‘Presov‘, ‘08001‘)
;

INSERT INTO zakaznici (id, meno, priezvisko, tel_cislo, email, id_mesto, ulica, cislo)
VALUES 
(nextval(‘zakaznici_id_seq‘),‘Milan‘,‘Dobry‘,‘0903007112‘,‘milan.dobry@gmail.com‘,‘1‘,‘Okruzna‘,’25‘),
(nextval(‘zakaznici_id_seq‘),‘Alena‘,‘Vesela‘,‘0949007112‘,‘alena.vesela@gmail.com‘,‘3‘,‘Bukov‘,’736‘),
(nextval(‘zakaznici_id_seq‘),‘Juraj‘,‘Nizky‘,‘0904558963‘,‘juraj.nizky@gmail.com‘,‘4‘,‘Bottova‘,’12‘),
(nextval(‘zakaznici_id_seq‘),‘Anna‘,‘Kratka‘,‘0903131902‘,‘anna.kratka@gmail.com‘,‘2‘,‘Benku‘,’99‘),
(nextval(‘zakaznici_id_seq‘),‘Kata‘,‘Drevena‘,‘0904006512‘,‘kata.drevena@gmail.com‘,‘6‘,’29 augusta‘,’135‘),
(nextval(‘zakaznici_id_seq‘),‘Peter‘,‘Rovny‘,‘0908445779‘,‘peter.rovny@gmail.com‘,‘5‘,‘Adamova‘,’5‘),
(nextval(‘zakaznici_id_seq‘),‘Jana‘,‘Dobra‘,‘0904187563‘,‘jana.dobra@gmail.com‘,‘5‘,‘Benkova‘,’557‘),
(nextval(‘zakaznici_id_seq‘),‘Jan‘,‘Mily‘,‘0907787563‘,‘jan.mily@gmail.com‘,‘7‘,‘Slnecna‘,’57‘),
(nextval(‘zakaznici_id_seq‘),‘Olina‘,‘Kratka‘,‘0949187563‘,‘olina.kratka@gmail.com‘,‘9‘,‘Atomova‘,’55‘),
(nextval(‘zakaznici_id_seq‘),‘Aneta‘,‘Drza‘,‘0904188900‘,‘aneta.drza@gmail.com‘,‘8‘,‘Bajkalska‘,’93‘),
(nextval(‘zakaznici_id_seq‘),‘Alena‘,‘Nahnevana‘,‘0904187563‘,‘alena.nahnevana@gmail.com‘,‘10‘,‘Bottova‘,’11‘),
(nextval(‘zakaznici_id_seq‘),‘Zuzana‘,‘Nudna‘,‘0904765563‘,‘zuzana.nudna@gmail.com‘,‘11‘,‘Hlavna‘,’992‘),
(nextval(‘zakaznici_id_seq‘),‘Tibor‘,‘Nahly‘,‘0908907563‘,‘tibor.nahly@gmail.com‘,‘9‘,‘Bellova‘,’20‘),
(nextval(‘zakaznici_id_seq‘),‘Natalia‘,‘Vesela‘,‘0904185478‘,‘natalia.vesela@gmail.com‘,‘6‘,‘Sasova‘,’9‘),
(nextval(‘zakaznici_id_seq‘),‘Juraj‘,‘Smutny‘,‘0904109587‘,‘juraj.smutny@gmail.com‘,‘2‘,‘Vlcince‘,’332‘),
(nextval(‘zakaznici_id_seq‘),‘Jana‘,‘Mudra‘,‘0909189733‘,‘jana.mudra@gmail.com‘,‘7‘,‘Veterna‘,’971‘),
(nextval(‘zakaznici_id_seq‘),‘Lubomir‘,‘Mudry‘,‘0904274203‘,‘lubo.mudry@gmail.com‘,‘5‘,‘Benkova‘,’12‘)
;



INSERT INTO tovar  (id, druh_tovaru, nazov, krajina_povodu, cena)
VALUES 
(nextval(‘tovar_id_seq‘),‘zimne sporty‘,‘hokejka‘,‘Cina‘,125),
(nextval(‘tovar_id_seq‘),‘zimne sporty‘,‘korcule‘,‘Nemecko‘,45),
(nextval(‘tovar_id_seq‘),‘zimne sporty‘,‘prilba na ladovy hokej‘,‘Turecko‘,77),
(nextval(‘tovar_id_seq‘),‘zimne sporty‘,‘lyze‘,‘Nemecko‘,355),
(nextval(‘tovar_id_seq‘),‘obuv‘,‘tenisky‘,‘Cina‘,‘53‘),
(nextval(‘tovar_id_seq‘),‘obuv‘,‘turisticke topanky‘,‘Cina‘,99),
(nextval(‘tovar_id_seq‘),‘obuv‘,‘kopacky‘,‘Nemecko‘,67),
(nextval(‘tovar_id_seq‘),‘obuv‘,‘tretry‘,‘Polsko‘,117),
(nextval(‘tovar_id_seq‘),‘oblecenie‘,‘tricko‘,‘Slovensko‘,33),
(nextval(‘tovar_id_seq‘),‘oblecenie‘,‘kratasy‘,‘Posko‘,14),
(nextval(‘tovar_id_seq‘),‘oblecenie‘,‘plavky‘,‘Cina‘,17),
(nextval(‘tovar_id_seq‘),‘oblecenie‘,‘teplaky‘,‘Rakusko‘,22),
(nextval(‘tovar_id_seq‘),‘oblecenie‘,‘ciapka‘,‘Cina‘,5),
(nextval(‘tovar_id_seq‘),‘oblecenie‘,‘kupacia ciapka‘,‘Cina‘,3),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘cyklisticke kratasy‘,‘Polsko‘,30),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘cyklisticka prilba‘,‘Cina‘,77),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘cyklisticka vetrovka‘,‘Turecko‘,125),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘kolobezka‘,‘Francuzsko‘,125),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘horsky bicykel‘,‘Taliansko‘,553),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘elektrobicykel‘,‘Spanielsko‘,1199),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘BMX‘,‘Nemecko‘,250),
(nextval(‘tovar_id_seq‘),‘cyklistika‘,‘mestsky bicykel‘,‘Turecko‘,280),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘tenisova raketa‘,‘Cina‘,213),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘kolieskove korcule‘,‘Slovensko‘,65),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘futbalova lopta‘,‘Ceska Republika‘,33),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘trekingove palice‘,‘Madarsko‘,20),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘tenisova lopta‘,‘Cina‘,7),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘skateboard‘,‘Cina‘,73),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘pennyboard‘,‘Anglicko‘,32),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘Batoh‘,‘Turecko‘,42),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘badmintonovy kosik‘,‘Cina‘,10),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘badmintonova sada‘,‘Ceska Republika‘,35),
(nextval(‘tovar_id_seq‘),‘letne sporty‘,‘badmintonova siet‘,‘Slovensko‘,27)
;

INSERT INTO objednavky (id, id_zakaznici, cislo_faktury, id_tovar, pocet_kusov, predajna_cena, datum)
VALUES
(nextval(‘objednavky_id_seq‘),‘1‘,‘1001‘,‘30‘,1,50,’01.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘1‘,‘1001‘,‘23‘,2,220,‘01.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘1‘,‘1001‘,‘27‘,1,8,‘01.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘2‘,‘1002‘,‘9‘,1,35,‘02.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘2‘,‘1002‘,‘13‘,1,6,‘02.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘2‘,‘1002‘,‘11‘,1,25,‘02.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘3‘,‘1003‘,‘2‘,1,49,‘02.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘4‘,‘1004‘,‘15‘,1,35,‘04.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘4‘,‘1004‘,‘16‘,1,80,‘04.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘5‘,‘1005‘,‘28‘,1,78,‘13.01.2020‘),
(nextval(‘objednavky_id_seq‘),‘6‘,‘1006‘,‘32‘,1,39,‘05.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘6‘,‘1006‘,‘33‘,1,30,‘05.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘6‘,‘1006‘,‘31‘,2,11,‘05.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘7‘,‘1007‘,‘3‘,1,80,‘17.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘8‘,‘1008‘,‘4‘,1,360,‘23.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘9‘,‘1009‘,‘5‘,1,58,‘11.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘10‘,‘1010‘,‘7‘,1,75,‘23.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘10‘,‘1010‘,‘25‘,1,35,‘23.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘11‘,‘1011‘,‘5‘,1,55,‘23.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘5‘,‘1012‘,‘8‘,1,120,‘23.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘7‘,‘1013‘,‘28‘,1,75,‘23.02.2020‘),
(nextval(‘objednavky_id_seq‘),‘12‘,‘1014‘,‘6‘,1,101,‘14.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘13‘,‘1015‘,‘10‘,2,16,‘23.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘13‘,‘1015‘,‘14‘,1,5,‘23.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘13‘,‘1015‘,‘11‘,1,25,‘23.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘14‘,‘1016‘,‘12‘,2,25,‘30.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘14‘,‘1016‘,’18‘,1,127,‘30.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘15‘,‘1017‘,’17‘,1,127,‘ 31.03.2020‘),
(nextval(‘objednavky_id_seq‘),‘16‘,‘1018‘,’19‘,1,560,‘ 14.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘17‘,‘1019‘,’20‘,1,1300,‘ 15.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘16‘,‘1020‘,’21‘,1,271,‘ 16.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘4‘,‘1021‘,’22‘,1,300,‘ 17.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘4‘,‘1021‘,’16‘,1,80,‘ 17.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘10‘,‘1022‘,’24‘,1,70,‘ 20.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘10‘,‘1022‘,’16‘,1,80,‘ 20.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘17‘,‘1023‘,’26‘,4,22,‘ 24.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘17‘,‘1023‘,’29‘,1,34,‘ 24.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘17‘,‘1023‘,’26‘,4,22,‘ 24.04.2020‘),
(nextval(‘objednavky_id_seq‘),‘13‘,‘1024‘,’30‘,2,50,‘ 17.05.2020‘),
(nextval(‘objednavky_id_seq‘),‘2‘,‘1025‘,’25‘,3,35,‘ 23.05.2020‘),
(nextval(‘objednavky_id_seq‘),‘2‘,‘1025‘,’7‘,2,75,‘ 23.05.2020‘)
;

-- VYTVORENIE SKUPIN, POUZIVATELOV A PRAV

CREATE GROUP spravca;
CREATE GROUP zamestnanci;

CREATE USER riaditel IN GROUP spravca;
CREATE USER zastupca_riaditela in group spravca;
CREATE USER administrator IN GROUP zamestnanci;
CREATE USER uctovnik IN GROUP zamestnanci;

GRANT ALL ON mesto, zakaznici, tovar, objednavky TO GROUP spravca;
GRANT SELECT, INSERT ON zakaznici, tovar TO GROUP zamestnanci;
GRANT ALL ON mesto, zakaznici, tovar, objednavky TO GROUP zamestnanci;
REVOKE DELETE ON mesto FROM GROUP zamestnanci;

-- VYBER UDAJOV

select * from objednavky where id=33;

select * from objednavky where predajna_cena>100;

select * from objednavky limit 7 offset 10;

select meno, priezvisko, tel_cislo, email, id_mesto from zakaznici;

select trim(meno)|| ' '||trim(priezvisko) as meno from zakaznici;

select priezvisko ||' '|| meno as zakaznik, id_mesto, ulica, cislo from zakaznici;

select druh_tovaru, nazov, count (*), sum (cena) from tovar left outer join objednavky on (tovar.id=objednavky.id_tovar) group by druh_tovaru, tovar.nazov;

select nazov, count (*) from zakaznici left outer join mesto on (mesto.id=zakaznici.id_mesto) group by nazov, mesto.nazov having count (*)>1;

-- POHLADY A AGREGACIE

create view prijem_za_rok as select extract (month from datum) as mesiac, extract (year from datum) as rok, sum (predajna_cena) from objednavky where predajna_cena>0 group by 1,2 union select extract (month from datum) as mesiac, extract (year from datum) as rok, sum (predajna_cena) from objednavky where predajna_cena<0 group by 1,2 order by 1,2,3 desc;
select * from prijem_za_rok;
select druh_tovaru, nazov, pocet_kusov, datum from tovar left outer join objednavky on (objednavky.id_tovar=tovar.id) where extract (year from datum) = 2020 and extract (month from datum) = 1 and extract (week from datum) = 1;
select priezvisko, meno, datum, predajna_cena from objednavky left outer join zakaznici on (zakaznici.id=objednavky.id) where datum in ('01.01.2020','04.01.2020','1.3.2020');
select druh_tovaru, nazov, pocet_kusov, datum from tovar left outer join objednavky on (objednavky.id_tovar=tovar.id) where extract (year from datum) = 2020 and extract (month from datum) =2;

create view platby as select meno, priezvisko, sum(cena) from tovar left outer join zakaznici on (zakaznici.id=tovar.id) group by meno, priezvisko order by meno;
select * from platby;
select druh_tovaru, nazov, pocet_kusov, datum from tovar left outer join objednavky on (objednavky.id_tovar=tovar.id) where extract (year from datum) = 2020 and extract (month from datum) = 5 and extract (day from datum) between 1 and 30;
select sum(pocet_kusov) from objednavky;
select max(predajna_cena) from objednavky;
select avg(pocet_kusov*predajna_cena)::numeric(10,2) as priemerna_cena from objednavky where extract (year from datum)=2020 and extract (month from datum)between 1 and 5;


--tempolarlna tabulka
create view platby as select meno, priezvisko, sum(cena) from tovar left outer join zakaznici on (zakaznici.id=tovar.id) group by meno, priezvisko order by meno;
select meno, priezvisko, sum(cena) into temp tmp_zakaznici from tovar left outer join zakaznici on (zakaznici.id=tovar.id) group by meno, priezvisko order by meno;
\d
select * from tmp_zakaznici;


-- integritne obmedzenia
alter table objednavky alter column pocet_kusov set not null;
alter table mesto alter column PSC set not null;
alter table zakaznici add constraint priezvisko CHECK (length(priezvisko)>3);
alter table zakaznici alter column tel_cislo set not null;


-- modifikacia tabulky zmena udajov v tabulke mesto
alter table mesto add column kraj varchar (50);
 \h update

-- indexy
create index zakaznici_idx on zakaznici (priezvisko, meno);
create unique index zakaznici_inxemail on zakaznici (email, priezvisko);
create index objednavky_idx on objednavky (datum, predajna_cena);

-- pravidla
create rule mesto_rule as on delete to mesto do instead nothing;

CREATE TABLE zakaznici_zaloha
(
   pc         SERIAL,
   id         SERIAL,
   meno       VARCHAR (20),
   priezvisko VARCHAR (50),
   tel_cislo  CHAR (10),
   email      VARCHAR (50),
   id_mesto   INTEGER,
   ulica      VARCHAR (20),
   cislo      VARCHAR (10),
   zmena      timestamp
);

create rule zakaznici_rule as on delete to zakaznici do insert into zakaznici_zaloha
select nextval ('zakaznici_zaloha_pc_seq'), id, meno, priezvisko, tel_cislo, email, id_mesto, ulica, cislo, now() from zakaznici where id=old.id;

delete from zakaznici where id=5;
select * from zakaznici_zaloha;



-- fukcie
-- vytvorime funckiu na zisťovanie prejnej ceny za tabuľky objednavky
-- parametre fukcie: mesiac, rok
-- vystup: hlaska, obsahujúca celkovú sumu penazi na zvoleny mesia a rok
-- nazov funkcie fnc_mesacny_sumar
-- premenne predajna_cena, hlaska
-- odkaz na vstupne premenne: $1 - mesiac, $2 - rok


create or replace function fnc_mesacny_sumar(integer, integer) returns varchar as 
$$
declare rk_suma decimal (10,2);
        hlaska varchar;
 begin
   hlaska='';
   select sum(predajna_cena) into rk_suma from objednavky 
   where extract (year from datum)= $2 and extract(month from datum)=$1;
   IF rk_suma ISNULL
   THEN 
   hlaska= 'V mesiaci '||$1||' roku '||$2||' nie je ziadna suma.';
   ELSE 
   hlaska= 'V mesiaci '||$1||' roku '||$2||' je suma penazi: '||rk_suma||',';
   END IF;
   RETURN hlaska;
end;
$$
language plpgsql;
   
   
     tyzden ALIAS for $1;
   mesiac ALIAS for $2;   
   predajna_cena decimal (10,2); 
   hlaska varchar;
   datum integer;
  

create or replace function fnc_sumar(integer, integer) returns varchar as 
$$
declare mesiac alias for $1;
        rok alias for $2;
		suma_plus decimal (10,2);
		suma_minus decimal (10,2);
        hlaska varchar;
 begin
   hlaska='';
   select sum(predajna_cena) into suma_plus from objednavky
   inner join zakaznici on (zakaznici.id=objednavky.id_zakaznici)
   where extract (month from datum)= $1 and extract(year from datum)=$2 and predajna_cena>0;
   IF suma_plus ISNULL then
      suma_plus:=0;
   END IF;
   select sum(predajna_cena) into suma_minus from objednavky
   inner join zakaznici on (zakaznici.id=objednavky.id_zakaznici)
   where extract (month from datum)=$1 and extract (year from datum)=$2 and predajna_cena<0;
   IF suma_minus ISNULL THEN
      suma_minus:=0;
   END IF;
   hlaska= 'Mesacny sumar za'||$1||'/'||$2||' je obchod v pluse '||suma_plus||' v minuse '||suma_minus||'.'; 
   RETURN hlaska;
 end;
 $$
language plpgsql;

--trigger

create or replace function fnc_zakaznici()
returns trigger as  '
declare
   pocet integer;
   zaznam record;

begin 
if new.email is null then
raise exception ''Email musi byt zadany.'';
end if;
select into pocet count(*) from zakaznici where email=new.email;
if (pocet>0) then
raise exception ''Lutujeme, zakaznik s touto e-mailovou adresou uz existuje'';
end if;
RETURN new;
end; '
language plpgsql;   
create trigger trigger_zakaznici before insert or update on zakaznici for each row execute procedure fnc_zakaznici();

insert into zakaznici values ('19', 'Alena','Dokonala','0908765555',null,'1','1 Maja','139');
insert into zakaznici values ('19', 'Alena','Dokonala','0908765555','alena.nahnevana@gmail.com','1','1 Maja','139');
‘Milan‘,‘Dobry‘,‘0903007112‘,‘milan.dobry@gmail.com‘,‘1‘,‘Okruzna‘,’25‘),

# SQL_project

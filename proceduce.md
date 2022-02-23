# M3_SQL

use demo1;
SELECT * FROM information_schema.TRIGGERS;
SELECT * FROM information_schema.REFERENTIAL_CONSTRAINTS;
SELECT * FROM information_schema.CHECK_CONSTRAINTS;

use qlsv;
alter table tblsinhvien drop check tblsinhvien_chk_1;
use quanlysinhvien;
select studentName, address, class.className
from student join class on student.classID = class.classID;
select class.classID, className, count(student.studentID)
from class join student on class.classID = student.classId
group by classId;
select classID, count(studentID) from student
group by classID;
select studentName, status from student
order by status desc
limit 4;

use qlsv;
ALTER TABLE tbltinh
 ALTER TenTinh SET DEFAULT 'Sandnes';

alter table tbltinh
add constraint unique (MaTinh);
alter table tbltinh
drop INDEX MaTinh;
SELECT * FROM information_schema.REFERENTIAL_CONSTRAINTS;
SELECT * FROM information_schema.CHECK_CONSTRAINTS;
alter table tbltinh
add primary key (MaTinh);
alter table tblsinhvien
add check ( GioiTinh ='Nam' or GioiTinh = 'Nữ');
use qlsv;
alter table tblsinhvien
drop check tblsinhvien_chk_1;
use quanlysinhvien;
alter table mark
drop FOREIGN KEY mark_ibfk_1;
alter table student auto_increment =5;
create schema alo1;
use alo1;

create table test(
                     id int auto_increment not null primary key ,
                     alo varchar(100)
);
alter table test modify id int auto_increment;
delete from test where id =10;
update test set alo = 'haha'
where id = 12;
alter table test alter alo set default 'a';
use alo1;
alter table test add unique (alo ,alo2);
alter table test add check (alo);
alter  table test add primary key (alo);
alter  table  test add foreign key (alo) references ();
select alo from test
where alo is not null;
use alo1;
alter table test add check (alo like 'london%');
alter table test add alo3 varchar(100);

alter table test modify alo varchar(30);
alter table test drop check test_chk_1;

use demo20062;
DELIMITER //

CREATE PROCEDURE findAll()

BEGIN
    SELECT * from orderdetail join product on orderdetail.productId = product.id;
END //

DELIMITER ;
use demo20062;
call findAll();
use classicmodels;
DELIMITER //

CREATE PROCEDURE getCusById
(IN cusNum INT(11))

BEGIN

    SELECT * FROM customers WHERE customerNumber = cusNum;

END //

DELIMITER //
call getCusById(103);
DELIMITER //

CREATE PROCEDURE getCusName1
(IN cusName int(100))

BEGIN

    SELECT customerName, contactFirstName FROM customers WHERE customerNumber like cusName;

END //

DELIMITER //
call getCusName1('103');
use alo1;
CREATE TABLE userroles(
                          user_id INT NOT NULL,
                          role_id INT NOT NULL,
                          PRIMARY KEY(user_id,role_id)

);
use alo1;
select distinct id from product where MOD(ID,2)=0;

select name, length(name) from product order by length(name) limit 1;


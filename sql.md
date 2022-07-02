# M3_SQL


# Lấy các bản ghi có id lẻ
select * from alo123 where id%2 and id !=1

# Lấy 1 kí tự đầu tiên
Select SUBSTRING(name1,1,1) as aki from alo123;
Select SUBSTRING(name1,1,1), SUBSTRING(name2,1,1) as aki from alo123;

use demo20062;
# Tạo 1 bảng
create table copy3(
    idC int not null primary key,
    alo1 varchar(1000),
    alo2 varchar(10000)
);

# Tạo 1 cột trong bảng
alter table product add description varchar(1000) not null;

# Xóa 1 cột trong bảng
alter table product drop description;

# Tạo nhiều cột trong bảng
alter table product add (
    service varchar(1000),
    made varchar(1000));

# Xóa nhiều cột trong bảng
alter table product drop service, drop made;

# Đổi tên 1 bảng
ALTER TABLE order1 RENAME TO order2;

# Sửa thông tin 1 bản ghi trong 1 cột
UPDATE copy1 SET title = 'Rất tốt' WHERE idV = 1;

# Thêm 1 bản ghi vào bảng
insert into product (id, name, price, quantity) values (15, 'Máy đuổi ruồi', 100, 9);

# Xóa toàn bộ bản ghi trong bảng không thể phục hồi
truncate table value;

# Xóa bản ghi với điều kiện
delete from value where idV > 2;

# Xóa 1 bảng
drop table value;

# Thêm tự tăng id
alter table copy1 modify idV int auto_increment;

# id tự tăng bắt đầu từ 5
alter table copy1 auto_increment = 5;

# Lấy tất cả những gì không null với điều kiện
select * from value where column_3 is not null;

# Sửa 1 cột trên 1 bản ghi với điều kiện
update value set valName = 'haha1' where idV = 1;

# Đổi kiểu dữ liệu của 1 cột
alter table value modify valName varchar(200);

# bảng copy2 là bảng trống lấy dữ liệu từ bảng copy1
INSERT INTO copy2 Select * from copy1;

# Đếm độ dài tất cả bản ghi của 1 cột đếm cả dấu
select name, length(name) from product order by length(name) limit 1;

# Đổi kiểu dữ liệu
ALTER TABLE value2 MODIFY COLUMN column_3 varchar(1000);

# tạo view
CREATE VIEW ten_view AS SELECT column_3 FROM value2;

# Xóa view
DROP VIEW ten_view;

# Các kiểu rằng buộc (6 kiểu)
#1 not null
# alter tên_bảng change column tên_cột_cũ tên_cột_mới kiểu_dữ_liệu rằng_buộc
alter table value change column valName valName varchar(100) not null;
ALTER TABLE value2 MODIFY column_3 varchar(1000) NOT NULL;
# bỏ not null
ALTER TABLE value2 MODIFY column_3 varchar(1000) NULL;

#2 DEFAULT
# alter tên_bảng alter tên_cột SET DEFAULT 'nội dung'
alter table value alter valName set default 'alo12';
# xóa default
alter table value ALTER valName DROP DEFAULT;

#3 unique
alter table value add constraint unique (valName);
# xóa unique
alter table value drop index valName;

#4 Thêm khóa chính (primary key)
ALTER TABLE value ADD PRIMARY KEY (idV);

# Xóa khóa chính (primary key)
alter table value drop primary key;

#5 Thêm rằng buộc check
alter table copy3 add check (alo1 = 'Name');

# Xóa rằng buộc check
alter table copy3 drop check copy3_chk_1;

#6 Thêm khóa phụ (foreign key)
alter table value add foreign key (column_4) references value2(column_3);
# Tạo view
CREATE VIEW demo20062.khanh1 as select * from customer;
# Sửa view
update demo20062.khanh1 set name = 'alo2' where id = 1;
# Xóa view
drop view demo20062.khanh1;
# Xem view
select * from demo20062.khanh1;

SELECT * FROM information_schema.TRIGGERS;
SELECT * FROM information_schema.REFERENTIAL_CONSTRAINTS;
SELECT * FROM information_schema.CHECK_CONSTRAINTS;
select * from information_schema.TABLE_CONSTRAINTS
where CONSTRAINT_SCHEMA like 'demo20062';

#BT
#Mức 1
# 1.	In ra các sản phẩm có số lượng từ 30 trở lên.
select * from product where quantity > 30;
# 2.	In ra các sản phẩm có số lượng từ 30 trở lên và có giá trong khoảng 100 đến 200.
select * from product where quantity > 30 and price >100 and price < 200;
# 3.	In ra thông tin khách hàng tuổi lớn hơn 18
select * from customer where age > 18;
# 4.	In ra thông tin khách hàng họ Nguyễn và lớn hơn 20 tuổi
select * from customer where name like 'Nguyễn%' and age > 20;
# 5.	In ra sản phẩm tên bắt đầu bằng chữ M
select * from product where name like 'M%';
# 6.	In ra sản phẩm kết thức bằng chữ E
select * from product where name like '%E';
# 7.	In ra danh sách sản phẩm số lượng tăng dần
select * from product where quantity order by quantity ASC ;
# 8.	In ra danh sách sản phẩm giá giảm dần
select * from product where quantity order by quantity DESC;

# Mức 2:
# 1.	In ra tổng số lượng sản phẩm giá nhỏ hơn 300
select sum(quantity) from product where product.price < 300;
# 2.	In tổng số sản phẩm theo từng giá
select sum(quantity) from product group by price;
# 3.	In ra sản phẩm có giá cao nhất
select * from product order by price DESC limit 1;
# 4.	In ra giá trung bình của tất cả các sản phẩm
select avg(price) from product;
# 5.	In ra tổng số tiền nếu bán hết tất cả sản phẩm.
select sum(price* product.quantity) from product;
# 6.	Tính tổng số sản phẩm giá <300.
select sum(quantity) from product where price < 300;
# 7.	Tìm giá bán cao nhất của các sản phẩm bắt đầu bằng chữ M.
select * from product where name like 'M%'order by price desc limit 1;
# 8.	Thấp nhất của các sản phẩm bắt đầu bằng chữ M.
select * from product where name like 'M%'order by price asc limit 1;
# 9.	Trung bình của các sản phẩm bắt đầu bằng chữ M.
select avg(quantity) from product where name like 'M%';

# Mức 3:
# 1.	In ra tên khách hàng và thời gian mua hàng.
select name, time from customer join order1 on customer.id = order1.customerId;
# 2.	In ra tên khách hàng và tên sản phẩm đã mua
select customer.name, product.name from orderdetail
    join order1 on order1.id = orderdetail.orderId
    join product on orderdetail.productId = product.id
join customer on order1.customerId = customer.id;
# 3.	In ra mã hoá đơn và giá trị hoá đơn
select orderdetail.orderId, product.price * orderdetail.quantity as 'trị giá hóa đơn' from orderdetail
    join product on orderdetail.productId = product.id order by orderId asc;
# 4.	In ra mã hoá đơn và giá trị hoá đơn giảm dần
select orderdetail.orderId, product.price * orderdetail.quantity as 'trị giá hóa đơn' from orderdetail
   join product on orderdetail.productId = product.id
order by product.price * orderdetail.quantity desc;

# Mức 4-10 :
# 1.	In ra các mã hóa đơn, trị giá hóa đơn bán ra trong ngày 19/6/2006 và ngày 20/6/2006.
select orderdetail.orderId, time, product.price * orderdetail.quantity
    as 'trị giá hóa đơn' from orderdetail
    join order1 on orderdetail.orderId = order1.id
join product on orderdetail.productId = product.id
where time = '2006-06-20' or time = '2006-06-19';
# 2.	In ra các mã hóa đơn, trị giá hóa đơn trong tháng 6/2006, sắp xếp theo ngày (tăng dần) và trị giá của hóa đơn (giảm dần).
select orderdetail.orderId, time, product.price * orderdetail.quantity
    as 'trị giá hóa đơn' from orderdetail
                                  join order1 on orderdetail.orderId = order1.id
                                  join product on orderdetail.productId = product.id
where time like '2006-06%' order by time asc , product.price * orderdetail.quantity desc;
# 3.	In ra danh sách các khách hàng (MAKH, HOTEN) đã mua hàng trong ngày 19/06/2007.
select customerId, name from customer
    join order1 on customer.id = order1.customerId where time = '2007-06-19';
# 4.	In ra danh sách các sản phẩm (MASP, TENSP) được khách hàng có tên “Nguyễn Văn A” mua trong tháng 10/2006.
select product.id, product.name from product
    join orderdetail on product.id = orderdetail.productId
join order1 on orderdetail.orderId = order1.id
join customer on order1.customerId = customer.id
where customer.name = 'Nguyễn Văn A';

# 5.	Tìm các số hóa đơn đã mua sản phẩm “Máy giặt” hoặc “Tủ lạnh”.
select orderdetail.orderId from orderdetail join product on orderdetail.productId = product.id
where product.name = 'Máy giặt' or product.name = 'Tủ lạnh' order by orderdetail.orderId;
# 6.	In ra danh sách các sản phẩm (MASP, TENSP) không bán được.
select id, name from product
where name not in (select name from product
    join orderdetail on orderdetail.productId = product.id);
# 7.	In ra danh sách các sản phẩm (MASP, TENSP) không bán được trong năm 2006.
select id, name from product
where name not in (select distinct name from product
    join orderdetail on orderdetail.productId = product.id
    join order1 on orderdetail.orderId = order1.id and time  like '2006%');
# 8.	In ra danh sách các sản phẩm (MASP, TENSP) có giá >200 sản xuất bán được trong năm 2006.
select distinct product.id, name from product
                     join orderdetail on orderdetail.productId = product.id
                     join order1 on orderdetail.orderId = order1.id
where time like '2006%' and price > 200;

# 9.	Có bao nhiêu sản phẩm khác nhau được bán ra trong năm 2006.
select distinct product.id, name from product
                                          join orderdetail on orderdetail.productId = product.id
                                          join order1 on orderdetail.orderId = order1.id
where time like '2006%';
# 10.	Tìm các số hóa đơn đã mua sản phẩm “Máy giặt” hoặc “Tủ lạnh”, mỗi sản phẩm mua với số lượng từ 10 đến 20.
select distinct product.name from orderdetail join product on orderdetail.productId = product.id
where name like 'Máy giặt' or name like 'Tủ lạnh'
                                  and orderdetail.quantity >=10
                                  and orderdetail.quantity < 20;
# 11.	Tìm các số hóa đơn mua cùng lúc 2 sản phẩm “Máy giặt” và “Tủ lạnh”, mỗi sản phẩm mua với số lượng từ 10 đến 20.

# 12.	Tìm số hóa đơn đã mua tất cả các sản phẩm có giá > 200.
# 13.	Tìm số hóa đơn trong năm 2006 đã mua tất cả các sản phẩm có giá <300.
# 14.	Có bao nhiêu sản phẩm khác nhau được bán ra trong năm 2006.
# 15.	Cho biết trị giá hóa đơn cao nhất, thấp nhất là bao nhiêu?
# 16.	Trị giá trung bình của tất cả các hóa đơn được bán ra trong năm 2006 là bao nhiêu?
# 17.	Tính doanh thu bán hàng trong năm 2006.
# 18.	Tìm số hóa đơn có trị giá cao nhất trong năm 2006.
# 19.	Tìm họ tên khách hàng đã mua hóa đơn có trị giá cao nhất trong năm 2006.
# 20.	In ra danh sách 3 khách hàng (MAKH, HOTEN) mua nhiều hàng nhất (tính theo số lượng).
# 21.	In ra danh sách các sản phẩm (MASP, TENSP) có giá bán bằng 1 trong 3 mức giá cao nhất.
# 22.	In ra danh sách các sản phẩm (MASP, TENSP) có tên bắt đầu bằng chữ M, có giá bằng 1 trong 3 mức giá cao nhất (của tất cả các sản phẩm).
# 23.	Tính doanh thu bán hàng mỗi ngày.
select sum( price * orderdetail.quantity), time from order1
    join orderdetail on order1.id = orderdetail.orderId
    join product on orderdetail.productId = product.id
group by time;
# 24.	Tính tổng số lượng của từng sản phẩm bán ra trong tháng 10/2006.
select sum(orderdetail.quantity), product.name from order1
    join orderdetail on order1.id = orderdetail.orderId
join product on orderdetail.productId = product.id
group by product.name;
# 25.	Tính doanh thu bán hàng của từng tháng trong năm 2006.
select sum( price * orderdetail.quantity), time from order1
    join orderdetail on order1.id = orderdetail.orderId
join product on orderdetail.productId = product.id
where time like '2006%'
group by time;
# 26.	Tìm hóa đơn có mua ít nhất 2 sản phẩm khác nhau.

# 27.	Tìm hóa đơn có mua 3 sản phẩm có giá <300 (3 sản phẩm khác nhau).

# 28.	Tìm khách hàng (MAKH, HOTEN) có số lần mua hàng nhiều nhất.
select count(customer.name), customer.name , customer.id from orderdetail
    join order1 on orderdetail.orderId = order1.id
join customer on order1.customerId = customer.id
group by customer.name
order by count(customer.name) desc
limit 1;
# 29.	Tháng mấy trong năm 2006, doanh số bán hàng cao nhất?
select count(time), time from order1 join orderdetail on order1.id = orderdetail.orderId
where time like '2006%'
group by order1.time
order by count(time) desc
limit 1;
# 30.	Tìm sản phẩm (MASP, TENSP) có tổng số lượng bán ra thấp nhất trong năm 2006.
select count(product.name), product.name from product
    join orderdetail on product.id = orderdetail.productId
group by product.name
order by count(product.name) asc
limit 1;
# 31.	Trong 10 khách hàng có doanh số cao nhất, tìm khách hàng có số lần mua hàng nhiều nhất.
select count(customer.name), customer.name from orderdetail
    join order1 on orderdetail.orderId = order1.id
    join customer on order1.customerId = customer.id
group by customer.name
order by count(customer.name) desc

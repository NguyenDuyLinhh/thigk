CREATE DATABASE ONTAP1


CREATE TABLE DONVIUNGHO
(
  MaDVUH VARCHAR(20)PRIMARY KEY,
  HoTenNguoiDaiDien VARCHAR(30)NOT NULL,
  DiaChiNguoiDaiDien VARCHAR(30)NOT NULL,
  SoDienThoaiLienLac VARCHAR(30) NOT NULl,
  SoCMNDNguoiDaiDien VARCHAR(30) NOT NULL,
  SoTaiKhoanNganHang VARCHAR(30) NOT NULL,
  TenNganHang VARCHAR(30) NOT NULL,
  ChiNhanhNganHang VARCHAR(30) NOT NULL,
  TenChuTKNganHang VARCHAR(30) NOT NULL
)

CREATE TABLE DOTUNGHO
(
  MaDotUngHo VARCHAR(20) PRIMARY KEY,
  MaDVUH VARCHAR(20) FOREIGN KEY (MaDVUH) REFERENCES dbo.DONVIUNGHO(MaDVUH),
  NgayUngHo DATE NOT NULL
)

CREATE TABLE HINHTHUCUH
(
  MaHinhThucUH VARCHAR(20) PRIMARY KEY,
  TenHinhThucUngHo VARCHAR(30) NOT NULL
)

CREATE TABLE CHITIETUNGHO
(
  MaDotUngHo VARCHAR(20) NOT NULL,
  MaHinhThucUH VARCHAR(20) NOT NULL,
  PRIMARY KEY (MaDotUngHo, MaHinhThucUH),
  SoLuongUngHo INT NOT NULL,
  DonViTinh VARCHAR(30),
  FOREIGN KEY (MaDotUngHo) REFERENCES dbo.DOTUNGHO(MaDotUngHo),
  FOREIGN KEY (MaHinhThucUH) REFERENCES dbo.HINHTHUCUH(MaHinhThucUH)
)

CREATE TABLE HODAN
(
  MaHoDan VARCHAR(20) PRIMARY KEY,
  HoTenChuHo VARCHAR(30) NOT NULL,
  ToDanPho VARCHAR(30) NOT NULL,
  KhoiHoacThon VARCHAR(30) NOT NULL,
  SoDienThoai VARCHAR(30) NOT NULL,
  DiaChiNha VARCHAR(30) NOT NULL,
  SoNhanKhau VARCHAR(30) NOT NULL,
  DienGiaDinh VARCHAR(30) NOT NULL,
  LaHoNgheo VARCHAR(30) NOT NULL
)

CREATE TABLE DOTNHANUNGHO
(
  MaDotNhanUngHo VARCHAR(20) PRIMARY KEY,
  MaHoDan VARCHAR(20) FOREIGN KEY (MaHoDan) REFERENCES dbo.HODAN(MaHoDan),
  NgayNhanUngHo DATE NOT NULL 
)

CREATE TABLE CHITIETNHANUNGHO
(
  MaDotNhanUngHo VARCHAR(20) NOT NULL,
  MaHinhThucUH VARCHAR(20) NOT NULL,
  PRIMARY KEY (MaDotNhanUngHo, MaHinhThucUH),
  SoLuongNhanUngHo INT NOT NULL,
  DonViTinh VARCHAR(30) NOT NULL,
  FOREIGN KEY (MaDotNhanUngHo) REFERENCES dbo.DOTNHANUNGHO(MaDotNhanUngHo),
  FOREIGN KEY (MaHinhThucUH) REFERENCES dbo.HINHTHUCUH(MaHinhThucUH)
)
INSERT INTO DONVIUNGHO VALUES
('CN001', 'Nguyen Van A1', 'Nui Thanh, Quang Nam', '0905121121', 124898000,	65874000, 'TienPhong Bank',	'Da Nang', 'Nguyen Van A1'),
('CN002', 'Nguyen Van A2',	'Phong Dien, Thua Thien Hue',	'0905121122',	124898001, 65874001, 'Vietcom Bank', 'Quang Nam', 'Nguyen Van A2'),
('CTY01', 'Nguyen Van A3',	'Tam Dao, Vinh Phuc',	'0905121123',	124898002,	65874002,	'DongA Bank',	'Thua Thien Hue',	'Nguyen Van A3'),
('CTY02',	'Nguyen Van A4',	'Ba To, Quang Ngai', '0905121124', 124898003, 65874003,	'Mbank',	'Gia Lai',	'Nguyen Van A4')
SELECT * FROM DOTUNGHO

INSERT INTO DOTUNGHO VALUES
('UH001', 'CN002', '2016/11/18'),
('UH002', 'CTY01', '2015/11/19'),
('UH003', 'CTY02', '2015/08/10'),
('UH004', 'CTY02', '2015/10/20'),
('UH005', 'CTY02', '2016/11/11')

INSERT INTO HINHTHUCUH VALUES
('HT01',	'Tien mat'),
('HT02',	'Mi tom'),
('HT03',	'Quan ao')


INSERT INTO CHITIETUNGHO VALUES
('UH001',	'HT01',	 6000, 	'USD'),
('UH002',	'HT02',	 50, 'Thung'),
('UH003',	'HT03',	 200, 	'Bo'),
('UH003',	'HT01',	 100000, 	'JPY'),
('UH004',	'HT01',	 100000, 	'USD'),
('UH005',	'HT03',	 100, 	'Bo')


INSERT INTO	HODAN VALUES							
	('HD001',	'Tran Van B1',	10,	5,	'0915222000', '12 Tran Van On',	5,	'Cong nhan vien chuc',	'Dung'),
	('HD002',	'Tran Van B2',	11,	6,	'0915222001',	'13 Nguyen Huu Tho',	2,	'Cong nhan vien chuc',	'Sai'),
	('HD003',	'Tran Van B3',	12,	7,	'0915222002',	'14 Phan Chu Trinh',	6,	'Thuong Binh',	'Dung'),
	('HD004',	'Tran Van B4',	13,	7,	'0915222003',	'15 Phan Chu Trinh',	1,	'Me VNAH',	'Dung')
	
INSERT INTO DOTNHANUNGHO VALUES
	('NhanUH001', 'HD003', '2016/11/11'),
	('NhanUH002', 'HD001',	'2016/11/18'),
	('NhanUH003', 'HD003',	'2016/11/20')
		
	
INSERT INTO CHITIETNHANUNGHO VALUES	
	('NhanUH001',	'HT01',	 5000, 	'USD'),					
	('NhanUH001',	'HT02',	 50, 	'Thung'),					
	('NhanUH002',	'HT03',	 100, 	'Bo'),					
	('NhanUH003',	'HT01',	 10000000, 	'VND'),					
	('NhanUH003',	'HT02',	 25, 	'Thung'	),				
	('NhanUH003',	'HT03',	 70, 	'Bo')					
	
	--Liệt kê những hộ dân có từ 5 nhân khẩu trở lên (0.5 điểm)

	
SELECT * FROM dbo.HODAN
WHERE SoNhanKhau >= 5

--Liệt kê các hộ dân là hộ nghèo và thuộc diện gia đình 'Thuong binh' 
--và các hộ dân không là hộ nghèo và thuộc diện gia đình 'Cong nhan vien chuc' (0.5 điểm)

SELECT *
FROM dbo.HODAN
WHERE LaHoNgheo = 'Dung' AND DienGiaDinh = 'Thuong binh'
OR
LaHoNgheo = 'Sai' AND DienGiaDinh = 'Cong nhan vien chuc'

--Liệt kê các đơn vị ủng hộ có MaDVUH bắt đầu bằng cụm từ "CTY"  (0.5 điểm)

SELECT *
FROM dbo.DONVIUNGHO
WHERE MaDVUH LIKE 'CTY%'

--Liệt kê thông tin của toàn bộ các hộ dân, yêu cầu sắp xếp giảm dần theo số nhân khẩu (0.5 điểm)

SELECT *
FROM dbo.HODAN
ORDER BY SoNhanKhau DESC

--Đếm số lượt ủng hộ diễn ra trong ngày hiện tại (của hệ thống) (0.5 điểm)

SELECT COUNT(MaDotUngHo) AS SoLuotUngHo
FROM dbo.DOTUNGHO
WHERE DAY(NgayUngHo) = DAY(GETDATE())

--Liệt kê toàn bộ các loại diện gia đình trong bảng HO_DAN với yêu cầu mỗi loại diện gia đình được liệt kê một lần duy nhất (0.5 điểm)

SELECT DISTINCT DienGiaDinh
FROM dbo.HODAN

--Liệt kê MaDotUngHo, NgayUngHo, HoTenNguoiDaiDien, DiaChiNguoiDaiDien, SoDienThoaiLienLac, SoCMNDNguoiDaiDien
--của tất cả các đợt ủng hộ có trong hệ thống (0.5 điểm)

SELECT MaDotUngHo,NgayUngHo,HoTenNguoiDaiDien,DiaChiNguoiDaiDien,SoDienThoaiLienLac,SoCMNDNguoiDaiDien
FROM dbo.DOTUNGHO duh JOIN dbo.DONVIUNGHO dv
ON dv.MaDVUH = duh.MaDVUH

--Liệt kê MaHoDan, HoTenChuHo, ToDanPho, KhoiHoacThon, DienGiaDinh, MaDotNhanUngHo, NgayNhanUngHo của tất cả các hộ dân
--với yêu cầu những hộ dân nào chưa từng được nhận ủng hộ lần nào thì cũng liệt kê thông tin những hộ dân đó ra (0.5 điểm)

SELECT *
FROM dbo.HODAN d LEFT JOIN dbo.DOTNHANUNGHO dn
ON dn.MaHoDan = d.MaHoDan

--Liệt kê thông tin của các hộ dân đã từng được nhận ủng hộ dưới hình thức là 'Tien mat' hoặc là hộ dân thuộc diện hộ nghèo
--mà có số nhân khẩu dưới 3 người (0.5 điểm)

SELECT DISTINCT dn.MaHoDan,h.HoTenChuHo,h.DiaChiNha,h.KhoiHoacThon,h.DienGiaDinh,h.SoDienThoai,h.SoNhanKhau,h.ToDanPho,h.LaHoNgheo,ht.TenHinhThucUngHo
FROM dbo.HODAN h FULL JOIN dbo.DOTNHANUNGHO dn 
ON h.MaHoDan = dn.MaHoDan 
FULL JOIN dbo.CHITIETNHANUNGHO ct 
ON dn.MaDotNhanUngHo = ct.MaDotNhanUngHo
FULL JOIN dbo.HINHTHUCUH ht
ON ht.MaHinhThucUH = ct.MaHinhThucUH
WHERE ht.TenHinhThucUngHo = 'Tien mat'
OR
LaHoNgheo = 'Dung' AND SoNhanKhau <3

--Liệt kê thông tin của các hộ dân chưa từng được nhận ủng hộ lần nào cả (0.5 điểm)

SELECT *
FROM dbo.HODAN 
WHERE MaHoDan NOT IN (SELECT MaHoDan FROM dbo.DOTNHANUNGHO)

--Liệt kê thông tin của các đơn vị ủng hộ đã từng ủng hộ dưới hình thức 'Tien mat' và chưa từng ủng hộ dưới hình thức 'Quan ao' (0.5 điểm)
SELECT * 
FROM dbo.DONVIUNGHO 
WHERE MaDVUH IN(SELECT MaDVUH FROM dbo.DOTUNGHO 
FULL JOIN dbo.CHITIETUNGHO
ON CHITIETUNGHO.MaDotUngHo = DOTUNGHO.MaDotUngHo
FULL JOIN dbo.HINHTHUCUH
ON HINHTHUCUH.MaHinhThucUH = CHITIETUNGHO.MaHinhThucUH
WHERE TenHinhThucUngHo = 'Tien mat')
AND
MaDVUH NOT IN(SELECT MaDVUH FROM dbo.DOTUNGHO
FULL JOIN dbo.CHITIETUNGHO
ON CHITIETUNGHO.MaDotUngHo = DOTUNGHO.MaDotUngHo
FULL JOIN dbo.HINHTHUCUH
ON HINHTHUCUH.MaHinhThucUH = CHITIETUNGHO.MaHinhThucUH
WHERE TenHinhThucUngHo = 'Quan ao')

--Câu 14:	Liệt kê thông tin của những đơn vị ủng hộ đã từng ủng hộ vào năm "2015" nhưng chưa từng ủng hộ vào năm "2016" (0.5 điểm)
SELECT *
FROM dbo.DONVIUNGHO
WHERE MaDVUH IN(SELECT MaDVUH FROM dbo.DONVIUNGHO INNER JOIN dbo.DOTUNGHO
ON DOTUNGHO.MaDVUH = DONVIUNGHO.MaDVUH
WHERE YEAR(NgayUngHo) = 2015
AND 
DONVIUNGHO.MaDVUH NOT IN ((SELECT MaDVUH FROM dbo.DONVIUNGHO INNER JOIN dbo.DOTUNGHO
ON DOTUNGHO.MaDVUH = DONVIUNGHO.MaDVUH
WHERE YEAR(NgayUngHo) = 2016)))

--Câu 15:	Hiển thị thông tin của những đơn vị ủng hộ đã thực hiện ít nhất 2 đợt ủng hộ tính từ 30/07/2015 đến hết năm 2015 (0.5 điểm)					
			SELECT distinct don.MaDVUH,don.HoTenNguoiDaiDien,don.DiaChiNguoiDaiDien,don.SoDienThoaiLienLac,don.SoCMNDNguoiDaiDien,don.SoTaiKhoanNganHang,don.TenNganHang,don.ChiNhanhNganHang,don.TenChuTKNganHang
			FROM DONVIUNGHO don JOIN DOTUNGHO ON don.MaDVUH=DOTUNGHO.MaDVUH
			WHERE DAY(DOTUNGHO.NgayUngHo)>=2015/07/30 AND YEAR(DOTUNGHO.NgayUngHo)=2015
			group by don.MaDVUH,don.HoTenNguoiDaiDien,don.DiaChiNguoiDaiDien,don.SoDienThoaiLienLac,don.SoCMNDNguoiDaiDien,don.SoTaiKhoanNganHang,don.TenNganHang,don.ChiNhanhNganHang,don.TenChuTKNganHang
			having count(DOTUNGHO.MaDotUngHo)>=2
			
			 
/*Câu 16:	Đếm tổng số đợt được nhận ủng hộ của từng hộ dân trong năm 2016 với yêu cầu chỉ thực hiện tính đối với những					
đợt được nhận ủng hộ có hình thức nhận ủng hộ là 'Tien mat' (0.5 điểm)	*/
			SELECT MaHoDan, COUNT(MaHoDan) AS Số_đợt_nhận_UH FROM DOTNHANUNGHO d JOIN CHITIETNHANUNGHO c ON d.MaDotNhanUngHo = c.MaDotNhanUngHo
			JOIN HINHTHUCUH h ON c.MaHinhThucUH = h.MaHinhThucUH
			WHERE YEAR(NgayNhanUngHo)=2016 and h.TenHinhThucUngHo = 'Tien mat'
			GROUP BY MaHoDan
/*Câu 17:	Liệt kê những ngày vừa diễn ra sự kiện có đơn vị ủng hộ đến trao hàng cứu trợ cho chính quyền,					
	vừa diễn ra sự kiện có hộ dân được chính quyền phân phối hàng cứu trợ, kết quả được sắp xếp tăng dần theo ngày tìm được (0.5 điểm)*/
			


/*Câu 18:	Cập nhật cột DonViTinh trong bảng CHI_TIET_UNG_HO thành NULL đối với record có hình thức ủng hộ với TenHinhThucUngHo là 'Quan ao'					
	và có ngày ủng hộ (NgayUngHo) trước ngày 30/12/2015 (0.5 điểm)*/					
			update CHITIETUNGHO set DonViTinh = null from CHITIETUNGHO c join HINHTHUCUH h on c.MaHinhThucUH = h.MaHinhThucUH
			where h.TenHinhThucUngHo = 'Quan ao'
			select * from CHITIETUNGHO
--Câu 19:	Xóa những hộ dân chưa từng được nhận một lần ủng hộ nào từ chính quyền (0.5 điểm)					
			delete from HODAN 
			where MaHoDan not in
			(select MaHoDan from DOTNHANUNGHO)

			select * from DOTUNGHO
--Câu 20:	Xóa những record trong bảng CHI_TIET_UNG_HO của những đợt ủng hộ diễn ra trước năm 2015 (0.5 điểm)					
			delete from CHITIETUNGHO 
			where MaDotUngHo in
			(select MaDotUngHo from DOTUNGHO 
			where YEAR(NgayUngHo) < 2015)

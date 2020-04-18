# MySQL-Cluster
Đề tài MySQL Cluster
Đề Tài:
Tìm hiểu và triển khai MySQL Cluster


1.	Danh sách thành viên & Công việc
Họ & tên	MSSV	Công việc	Tiến độ
Vũ Đức Minh 	175A071318	- Cài đặt MySQL Cluster
- Hướng dẫn cài đặt
- Hướng dẫn quản trị MySQL Cluster
 
	- Cài đặt hoàn thành
-Hoàn thành 
-Hoàn thành
Đinh Quang Khải 	175A071308	- Cài đặt MySQL Cluster
- Tìm hiểu tài liệu về MySQL Cluster: khái niệm, chức năng, hoạt động.
- Phân tích ưu, nhược điểm 
	- Cài đặt hoàn thành
-Hoàn thành 



-chưa hoàn thành 
2.	Nội dung nghiên cứu : Tìm hiểu và triển khai MySQL Cluster
a.	MySQL Cluster là gì?
-	MySQL Cluster là cơ sở dữ liệu phân tán kết hợp khả năng mở rộng liên tục và tính sẵn sàng cao. Nó cung cấp truy cập thời gian thực trong bộ nhớ với sự nhất quán về tiến trình xử lý trên các bộ dữ liệu phân tán và phân vùng.Nó được thiết kế cho các ứng dụng quan trọng.
-	MySQL Cluster có bản sao giữa các cụm (Cluster) trên nhiều trang web địa lý được tích hợp sẵn. 
-	MySQL Cluster được chứng minh hàng ngày trong các hệ thống phục vụ hàng tỷ người dùng. Nó được sử dụng trong nhiệm vụ quan trọng ứng dụng cốt lõi của mạng điện thoại di động, hệ thống xác thực và trò chơi nền tảng với khối lượng dữ liệu bùng nổ và lượng người dùng tải.

b.	MySQL Cluster có chức năng cụ thể là gì? 
•	MySQL Cluster là cơ sở dữ liệu cần thiết để hỗ trợ sự tăng trưởng và đáp ứng những thách thức mới, bao gồm:

-	Hoạt động đọc, ghi mở rộng.
-	Các bộ dữ liệu lớn được phân phối trên cơ sở hạ tầng phần cứng hoặc đám mây hàng hóa
-	Độ trễ thấp cho trải nghiệm người dùng trong thời gian thực.
-	Tính khả dụng 24 x 7 cho thời gian hoạt động liên tục của dịch vụ.
-	Tính linh hoạt và dễ sử dụng, cho phép các nhà phát triển nhanh chóng khởi động các dịch vụ mới, sáng tạo.
 

c.	Hoạt động của MySQL Cluster [Nếu là kiến trúc/giải pháp] hoặc So sánh Ưu/Nhược điểm
Ưu điểm của MySQL Cluster.
- Tính sẵn sàng cao.
- Hiệu suất tải khi hoạt động. 
d.	Hướng dẫn cài đặt MySQL Cluster trên Ubuntu [CentOS]
Điều kiện tiên quyết
Để hoàn thành hướng dẫn này, bạn sẽ cần tổng cộng ba máy chủ: hai máy chủ cho các nút dữ liệu MySQL dự phòng ( ndbd) và một máy chủ cho Trình quản lý cụm ( ndb_mgmd) và máy chủ / máy khách MySQL ( mysqldvà mysql).
Trong cùng một trung tâm dữ liệu DigitalOcean , hãy tạo các giọt sau với kích hoạt mạng riêng :
•	Ba giọt Ubuntu 18.04 có bật mạng riêng
•	Một người dùng không root với các đặc quyền sudo được cấu hình cho mỗi Giọt. Bạn có thể tìm hiểu cách thực hiện việc này trong Cài đặt máy chủ ban đầu với Ubuntu 18.04 .
Hãy chắc chắn ghi lại các địa chỉ IP riêng của ba Giọt của bạn. Trong hướng dẫn này, các nút cụm của chúng tôi có các địa chỉ IP riêng sau đây:
•	198.51.100.0 sẽ là nút dữ liệu MySQL Cluster đầu tiên
•	198.51.100.1 sẽ là nút dữ liệu thứ hai
•	198.51.100.2 sẽ là nút Trình quản lý cụm & máy chủ MySQL
Khi bạn đã tạo ra các giọt của mình, định cấu hình người dùng không phải root và ghi lại địa chỉ IP cho 3 nút, bạn đã sẵn sàng để bắt đầu với hướng dẫn này.
Bước 1 - Cài đặt và cấu hình Trình quản lý cụm
Trước tiên, chúng tôi sẽ bắt đầu bằng cách tải xuống và cài đặt Trình quản lý cụm MySQL , ndb_mgmd.
Để cài đặt Trình quản lý cụm, trước tiên chúng tôi cần tìm nạp .debtệp trình cài đặt thích hợp từ trang tải xuống chính thức của Cụm sao MySQL .
Từ trang này, bên dưới Chọn Hệ điều hành , chọn Ubuntu Linux . Sau đó, trong Chọn Phiên bản HĐH , chọn Ubuntu Linux 18.04 (x86, 64-bit) .
Cuộn xuống cho đến khi bạn thấy Gói DEB, Máy chủ quản lý NDB và nhấp vào liên kết Tải xuống cho liên kết không chứa dbgsym(trừ khi bạn yêu cầu các biểu tượng gỡ lỗi). Bạn sẽ được đưa đến trang Bắt đầu Tải xuống của bạn . Ở đây, nhấp chuột phải vào Không, cảm ơn, chỉ cần bắt đầu tải xuống của tôi. và sao chép liên kết vào .debtập tin.
Bây giờ, đăng nhập vào Giọt quản lý cụm của bạn (trong hướng dẫn này 198.51.100.2) và tải xuống .debtệp này :
•	cd ~
•	
•	wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-management-server_7.6.6-1ubuntu18.04_amd64.deb
•	
Cài đặt ndb_mgmdbằng dpkg:
•	sudo dpkg -i mysql-cluster-community-management-server_7.6.6-1ubuntu18.04_amd64.deb
•	
Bây giờ chúng ta cần cấu hình ndb_mgmdtrước khi chạy nó trước; cấu hình phù hợp sẽ đảm bảo đồng bộ hóa chính xác và phân phối tải giữa các nút dữ liệu.
Trình quản lý cụm phải là thành phần đầu tiên được khởi chạy trong bất kỳ cụm MySQL nào. Nó đòi hỏi một tệp cấu hình, được truyền vào dưới dạng đối số để thực thi. Chúng tôi sẽ tạo và sử dụng tệp cấu hình sau : /var/lib/mysql-cluster/config.ini.
Trên Giọt quản lý cụm, tạo /var/lib/mysql-clusterthư mục chứa tệp này:
•	sudo mkdir /var/lib/mysql-cluster
•	
Sau đó tạo và chỉnh sửa tệp cấu hình bằng trình soạn thảo văn bản ưa thích của bạn:
•	sudo nano /var/lib/mysql-cluster/config.ini
•	
Dán văn bản sau vào trình soạn thảo của bạn:
/var/lib/mysql-cluster/config.ini
[ndbd default]
# Options affecting ndbd processes on all data nodes:
NoOfReplicas=2  # Number of replicas

[ndb_mgmd]
# Management process options:
hostname=198.51.100.2 # Hostname of the manager
datadir=/var/lib/mysql-cluster  # Directory for the log files

[ndbd]
hostname=198.51.100.0 # Hostname/IP of the first data node
NodeId=2            # Node ID for this data node
datadir=/usr/local/mysql/data   # Remote directory for the data files

[ndbd]
hostname=198.51.100.1 # Hostname/IP of the second data node
NodeId=3            # Node ID for this data node
datadir=/usr/local/mysql/data   # Remote directory for the data files

[mysqld]
# SQL node options:
hostname=198.51.100.2 # In our case the MySQL server/client is on the same Droplet as the cluster manager
Sau khi dán vào văn bản này, đảm bảo thay thế các hostnamegiá trị ở trên bằng địa chỉ IP chính xác của các Giọt mà bạn đã cấu hình. Đặt hostnametham số này là một biện pháp bảo mật quan trọng ngăn các máy chủ khác kết nối với Trình quản lý cụm.
Lưu tệp và đóng trình soạn thảo văn bản của bạn.
Đây là một tệp cấu hình tối thiểu được giảm xuống cho một cụm MySQL. Bạn nên tùy chỉnh các tham số trong tệp này tùy thuộc vào nhu cầu sản xuất của bạn. Đối với một mẫu, ndb_mgmdtệp cấu hình được cấu hình đầy đủ , tham khảo tài liệu về cụm MySQL .
Trong tệp trên, bạn có thể thêm các thành phần bổ sung như nút dữ liệu ( ndbd) hoặc nút máy chủ MySQL ( mysqld) bằng cách nối thêm các thể hiện vào phần thích hợp.
Bây giờ chúng ta có thể bắt đầu trình quản lý bằng cách thực thi ndb_mgmdtệp nhị phân và chỉ định tệp cấu hình của nó bằng -fcờ:
•	sudo ndb_mgmd -f /var/lib/mysql-cluster/config.ini
•	
Bạn sẽ thấy đầu ra sau:
Output
MySQL Cluster Management Server mysql-5.7.22 ndb-7.6.6
2018-07-25 21:48:39 [MgmtSrvr] INFO     -- The default config directory '/usr/mysql-cluster' does not exist. Trying to create it...
2018-07-25 21:48:39 [MgmtSrvr] INFO     -- Successfully created config directory
Điều này chỉ ra rằng máy chủ Quản lý cụm MySQL đã được cài đặt thành công và hiện đang chạy trên Giọt của bạn.
Lý tưởng nhất, chúng tôi muốn tự động khởi động máy chủ Quản lý cụm khi khởi động. Để làm điều này, chúng tôi sẽ tạo và kích hoạt một dịch vụ systemd.
Trước khi tạo dịch vụ, chúng ta cần hủy máy chủ đang chạy:
•	sudo pkill -f ndb_mgmd
•	
Bây giờ, hãy mở và chỉnh sửa tệp Đơn vị systemd sau bằng trình chỉnh sửa yêu thích của bạn:
•	sudo nano /etc/systemd/system/ndb_mgmd.service
•	
Dán vào đoạn mã sau:
/etc/systemd/system/ndb_mgmd.service
[Unit]
Description=MySQL NDB Cluster Management Server
After=network.target auditd.service

[Service]
Type=forking
ExecStart=/usr/sbin/ndb_mgmd -f /var/lib/mysql-cluster/config.ini
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure

[Install]
WantedBy=multi-user.target
Tại đây, chúng tôi đã thêm một bộ tùy chọn tối thiểu hướng dẫn systemd về cách bắt đầu, dừng và khởi động lại ndb_mgmdquy trình. Để tìm hiểu thêm về các tùy chọn được sử dụng trong cấu hình đơn vị này, hãy tham khảo hướng dẫn sử dụng systemd .
Lưu và đóng tập tin.
Bây giờ, tải lại cấu hình trình quản lý của systemd bằng cách sử dụng daemon-reload:
•	sudo systemctl daemon-reload
•	
Chúng tôi sẽ kích hoạt dịch vụ mà chúng tôi vừa tạo để Trình quản lý cụm MySQL bắt đầu khởi động lại:
•	sudo systemctl enable ndb_mgmd
•	
Cuối cùng, chúng tôi sẽ bắt đầu dịch vụ:
•	sudo systemctl start ndb_mgmd
•	
Bạn có thể xác minh rằng dịch vụ Quản lý cụm NDB đang chạy:
•	sudo systemctl status ndb_mgmd
•	
Bạn sẽ thấy đầu ra sau:
● ndb_mgmd.service - MySQL NDB Cluster Management Server
   Loaded: loaded (/etc/systemd/system/ndb_mgmd.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2018-07-26 21:23:37 UTC; 3s ago
  Process: 11184 ExecStart=/usr/sbin/ndb_mgmd -f /var/lib/mysql-cluster/config.ini (code=exited, status=0/SUCCESS)
 Main PID: 11193 (ndb_mgmd)
    Tasks: 11 (limit: 4915)
   CGroup: /system.slice/ndb_mgmd.service
           └─11193 /usr/sbin/ndb_mgmd -f /var/lib/mysql-cluster/config.ini
Điều đó chỉ ra rằng ndb_mgmdmáy chủ Quản lý cụm MySQL hiện đang chạy như một dịch vụ systemd.
Bước cuối cùng để thiết lập Trình quản lý cụm là cho phép các kết nối đến từ các nút Cụm MySQL khác trên mạng riêng của chúng tôi.
Nếu bạn không định cấu hình ufwtường lửa khi thiết lập Giọt này, bạn có thể bỏ qua phần tiếp theo.
Chúng tôi sẽ thêm các quy tắc để cho phép các kết nối đến cục bộ từ cả hai nút dữ liệu:
•	sudo ufw allow from 198.51.100.0
•	
•	sudo ufw allow from 198.51.100.1
•	
Sau khi nhập các lệnh này, bạn sẽ thấy đầu ra sau:
Output
Rule added
Trình quản lý cụm bây giờ sẽ hoạt động và có thể giao tiếp với các nút Cụm khác qua mạng riêng.
Bước 2 - Cài đặt và cấu hình các nút dữ liệu
Lưu ý: Tất cả các lệnh trong phần này phải được thực thi trên cả hai nút dữ liệu.

Trong bước này, chúng tôi sẽ cài đặt ndbdtrình nền nút dữ liệu của cụm cụm MySQL và định cấu hình các nút để chúng có thể giao tiếp với Trình quản lý cụm.
Để cài đặt nhị phân nút dữ liệu, trước tiên chúng ta cần tìm nạp .debtệp trình cài đặt thích hợp từ trang tải xuống chính thức của MySQL .
Từ trang này, bên dưới Chọn Hệ điều hành , chọn Ubuntu Linux . Sau đó, trong Chọn Phiên bản HĐH , chọn Ubuntu Linux 18.04 (x86, 64-bit) .
Cuộn xuống cho đến khi bạn thấy Gói DEB, Mã nhị phân dữ liệu NDB và nhấp vào liên kết Tải xuống cho gói không chứa dbgsym(trừ khi bạn yêu cầu các ký hiệu gỡ lỗi). Bạn sẽ được đưa đến trang Bắt đầu Tải xuống của bạn . Ở đây, nhấp chuột phải vào Không, cảm ơn, chỉ cần bắt đầu tải xuống của tôi. và sao chép liên kết vào .debtập tin.
Bây giờ, đăng nhập vào Giọt nút dữ liệu đầu tiên của bạn (trong hướng dẫn này 198.51.100.0) và tải xuống .debtệp này :
•	cd ~
•	
•	wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster-community-data-node_7.6.6-1ubuntu18.04_amd64.deb
•	
Trước khi chúng ta cài đặt nhị phân nút dữ liệu, chúng ta cần cài đặt một phụ thuộc , libclass-methodmaker-perl:
•	sudo apt update
•	
•	sudo apt install libclass-methodmaker-perl
•	
Bây giờ chúng ta có thể cài đặt nhị phân ghi chú dữ liệu bằng cách sử dụng dpkg:
•	sudo dpkg -i mysql-cluster-community-data-node_7.6.6-1ubuntu18.04_amd64.deb
•	
Các nút dữ liệu kéo cấu hình của chúng từ vị trí tiêu chuẩn của MySQL , /etc/my.cnf. Tạo tập tin này bằng trình soạn thảo văn bản yêu thích của bạn và bắt đầu chỉnh sửa nó:
•	sudo nano /etc/my.cnf
•	
Thêm tham số cấu hình sau vào tệp:
/etc/my.cnf
[mysql_cluster]
# Options for NDB Cluster processes:
ndb-connectstring=198.51.100.2  # location of cluster manager
Chỉ định vị trí của nút Trình quản lý cụm là cấu hình duy nhất cần thiết ndbdđể bắt đầu. Phần còn lại của cấu hình sẽ được lấy trực tiếp từ người quản lý.
Lưu và thoát tệp.
Trong ví dụ của chúng tôi, nút dữ liệu sẽ phát hiện ra rằng thư mục dữ liệu của nó /usr/local/mysql/data, theo cấu hình của người quản lý. Trước khi bắt đầu daemon, chúng tôi sẽ tạo thư mục này trên nút:
•	sudo mkdir -p /usr/local/mysql/data
•	
Bây giờ chúng ta có thể bắt đầu nút dữ liệu bằng lệnh sau:
•	sudo ndbd
•	
Bạn sẽ thấy đầu ra sau:
Output
2018-07-18 19:48:21 [ndbd] INFO     -- Angel connected to '198.51.100.2:1186'
2018-07-18 19:48:21 [ndbd] INFO     -- Angel allocated nodeid: 2
Trình nền nút dữ liệu NDB đã được cài đặt thành công và hiện đang chạy trên máy chủ của bạn.
Chúng tôi cũng cần cho phép các kết nối đến từ các nút MySQL Cluster khác qua mạng riêng.
Nếu bạn không định cấu hình ufwtường lửa khi thiết lập Giọt này, bạn có thể bỏ qua trước để thiết lập dịch vụ systemd cho ndbd.
Chúng tôi sẽ thêm các quy tắc để cho phép các kết nối đến từ Trình quản lý cụm và các nút dữ liệu khác:
•	sudo ufw allow from 198.51.100.0
•	
•	sudo ufw allow from 198.51.100.2
•	
Sau khi nhập các lệnh này, bạn sẽ thấy đầu ra sau:
Output
Rule added
Giờ đây, nút dữ liệu MySQL của bạn có thể giao tiếp với cả Trình quản lý cụm và nút dữ liệu khác qua mạng riêng.
Cuối cùng, chúng tôi cũng muốn trình nền nút dữ liệu tự động khởi động khi máy chủ khởi động. Chúng tôi sẽ thực hiện theo quy trình tương tự được sử dụng cho Trình quản lý cụm và tạo dịch vụ systemd.
Trước khi chúng tôi tạo dịch vụ, chúng tôi sẽ hủy ndbdquy trình đang chạy :
•	sudo pkill -f ndbd
•	
Bây giờ, hãy mở và chỉnh sửa tệp Đơn vị systemd sau bằng trình chỉnh sửa yêu thích của bạn:
•	sudo nano /etc/systemd/system/ndbd.service
•	
Dán vào đoạn mã sau:
/etc/systemd/system/ndbd.service
[Unit]
Description=MySQL NDB Data Node Daemon
After=network.target auditd.service

[Service]
Type=forking
ExecStart=/usr/sbin/ndbd
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure

[Install]
WantedBy=multi-user.target
Tại đây, chúng tôi đã thêm một bộ tùy chọn tối thiểu hướng dẫn systemd về cách bắt đầu, dừng và khởi động lại ndbdquy trình. Để tìm hiểu thêm về các tùy chọn được sử dụng trong cấu hình đơn vị này, hãy tham khảo hướng dẫn sử dụng systemd .
Lưu và đóng tập tin.
Bây giờ, tải lại cấu hình trình quản lý của systemd bằng cách sử dụng daemon-reload:
•	sudo systemctl daemon-reload
•	
Bây giờ chúng tôi sẽ kích hoạt dịch vụ chúng tôi vừa tạo để trình nền nút dữ liệu bắt đầu khởi động lại:
•	sudo systemctl enable ndbd
•	
Cuối cùng, chúng tôi sẽ bắt đầu dịch vụ:
•	sudo systemctl start ndbd
•	
Bạn có thể xác minh rằng dịch vụ Quản lý cụm NDB đang chạy:
•	sudo systemctl status ndbd
•	
Bạn sẽ thấy đầu ra sau:
Output
● ndbd.service - MySQL NDB Data Node Daemon
   Loaded: loaded (/etc/systemd/system/ndbd.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2018-07-26 20:56:29 UTC; 8s ago
  Process: 11972 ExecStart=/usr/sbin/ndbd (code=exited, status=0/SUCCESS)
 Main PID: 11984 (ndbd)
    Tasks: 46 (limit: 4915)
   CGroup: /system.slice/ndbd.service
           ├─11984 /usr/sbin/ndbd
           └─11987 /usr/sbin/ndbd
Điều này chỉ ra rằng ndbdtrình nền nút dữ liệu của cụm cụm MySQL hiện đang chạy như một dịch vụ systemd. Nút dữ liệu của bạn bây giờ sẽ có đầy đủ chức năng và có thể kết nối với Trình quản lý cụm MySQL.
Khi bạn đã hoàn tất thiết lập nút dữ liệu đầu tiên, hãy lặp lại các bước trong phần này trên nút dữ liệu khác ( 198.51.100.1trong hướng dẫn này).
Bước 3 - Cấu hình và khởi động máy chủ và máy khách MySQL
Một máy chủ MySQL tiêu chuẩn, chẳng hạn như máy chủ có sẵn trong kho APT của Ubuntu, không hỗ trợ NDB của cụm công cụ MySQL. Điều này có nghĩa là chúng ta cần cài đặt máy chủ SQL tùy chỉnh được đóng gói cùng với phần mềm MySQL Cluster khác mà chúng ta đã cài đặt trong hướng dẫn này.
Một lần nữa chúng ta sẽ lấy tệp nhị phân MySQL Cluster Server từ trang tải xuống chính thức của MySQL Cluster .
Từ trang này, bên dưới Chọn Hệ điều hành , chọn Ubuntu Linux . Sau đó, trong Chọn Phiên bản HĐH , chọn Ubuntu Linux 18.04 (x86, 64-bit) .
Cuộn xuống cho đến khi bạn thấy Gói DEB và nhấp vào liên kết Tải xuống (nó phải là liên kết đầu tiên trong danh sách). Bạn sẽ được đưa đến trang Bắt đầu Tải xuống của bạn . Ở đây, nhấp chuột phải vào Không, cảm ơn, chỉ cần bắt đầu tải xuống của tôi. và sao chép liên kết vào .tarkho lưu trữ.
Bây giờ, hãy đăng nhập vào Bộ quản lý cụm (trong hướng dẫn này 198.51.100.2) và tải xuống .tarkho lưu trữ này (nhắc lại rằng chúng tôi đang cài đặt Máy chủ MySQL trên cùng một nút với Trình quản lý cụm của chúng tôi - trong cài đặt sản xuất, bạn nên chạy các trình tiện ích này trên các nút khác nhau) :
•	cd ~
•	
•	wget https://dev.mysql.com/get/Downloads/MySQL-Cluster-7.6/mysql-cluster_7.6.6-1ubuntu18.04_amd64.deb-bundle.tar
•	
Bây giờ chúng tôi sẽ trích xuất kho lưu trữ này vào một thư mục có tên install. Đầu tiên, tạo thư mục:
•	mkdir install
•	
Bây giờ giải nén kho lưu trữ vào thư mục này:
•	tar -xvf mysql-cluster_7.6.6-1ubuntu18.04_amd64.deb-bundle.tar -C install/
•	
Di chuyển vào thư mục này, chứa các nhị phân thành phần MySQL Cluster được trích xuất:
•	cd install
•	
Trước khi chúng tôi cài đặt nhị phân máy chủ MySQL, chúng tôi cần cài đặt một vài phụ thuộc:
•	sudo apt update
•	
•	sudo apt install libaio1 libmecab2
•	
Bây giờ, chúng ta cần cài đặt các phụ thuộc của Cluster Cluster, được gói trong tarkho lưu trữ mà chúng ta vừa trích xuất:
•	sudo dpkg -i mysql-common_7.6.6-1ubuntu18.04_amd64.deb
•	
•	sudo dpkg -i mysql-cluster-community-client_7.6.6-1ubuntu18.04_amd64.deb
•	
•	sudo dpkg -i mysql-client_7.6.6-1ubuntu18.04_amd64.deb
•	
•	sudo dpkg -i mysql-cluster-community-server_7.6.6-1ubuntu18.04_amd64.deb
•	
Khi cài đặt mysql-cluster-community-server, một dấu nhắc cấu hình sẽ xuất hiện, yêu cầu bạn đặt mật khẩu cho tài khoản gốc của cơ sở dữ liệu MySQL của bạn. Chọn một mật khẩu mạnh, an toàn và nhấn <Ok> . Nhập lại mật khẩu gốc này khi được nhắc và nhấn <Ok> một lần nữa để hoàn tất cài đặt.
Bây giờ chúng ta có thể cài đặt nhị phân máy chủ MySQL bằng cách sử dụng dpkg:
•	sudo dpkg -i mysql-server_7.6.6-1ubuntu18.04_amd64.deb
•	
Bây giờ chúng ta cần cấu hình cài đặt máy chủ MySQL này.
Cấu hình cho Máy chủ MySQL được lưu trữ trong /etc/mysql/my.cnftệp mặc định .
Mở tệp cấu hình này bằng trình chỉnh sửa yêu thích của bạn:
•	sudo nano /etc/mysql/my.cnf
•	
Bạn sẽ thấy văn bản sau:
/etc/mysql/my.cnf
# Copyright (c) 2015, 2016, Oracle and/or its affiliates. All rights reserved.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; version 2 of the License.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301 USA

#
# The MySQL Cluster Community Server configuration file.
#
# For explanations see
# http://dev.mysql.com/doc/mysql/en/server-system-variables.html

# * IMPORTANT: Additional settings that can override those from this file!
#   The files must end with '.cnf', otherwise they'll be ignored.
#
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mysql.conf.d/
Nối các cấu hình sau vào nó:
/etc/mysql/my.cnf
. . .
[mysqld]
# Options for mysqld process:
ndbcluster                      # run NDB storage engine

[mysql_cluster]
# Options for NDB Cluster processes:
ndb-connectstring=198.51.100.2  # location of management server
Lưu và thoát tệp.
Khởi động lại máy chủ MySQL để những thay đổi này có hiệu lực:
•	sudo systemctl restart mysql
•	
MySQL theo mặc định sẽ tự động khởi động khi máy chủ của bạn khởi động lại. Nếu không, lệnh sau sẽ khắc phục điều này:
•	sudo systemctl enable mysql
•	
Một máy chủ SQL hiện đang chạy trên Trình quản lý cụm / Trình quản lý máy chủ MySQL của bạn.
Trong bước tiếp theo, chúng tôi sẽ chạy một vài lệnh để xác minh rằng cài đặt MySQL Cluster của chúng tôi hoạt động như mong đợi.
Bước 4 - Xác minh cài đặt cụm MySQL
Để xác minh cài đặt Cụm sao của bạn, hãy đăng nhập vào nút Trình quản lý cụm / Máy chủ SQL.
Chúng tôi sẽ mở máy khách MySQL từ dòng lệnh và kết nối với tài khoản gốc mà chúng tôi vừa cấu hình bằng cách nhập lệnh sau:
•	mysql -u root -p 
•	
Nhập mật khẩu của bạn khi được nhắc và nhấn ENTER.
Bạn sẽ thấy một đầu ra tương tự như:
Output
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.22-ndb-7.6.6 MySQL Cluster Community Server (GPL)

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
Khi đã ở trong máy khách MySQL, hãy chạy lệnh sau:
•	SHOW ENGINE NDB STATUS \G
•	
Bây giờ bạn sẽ thấy thông tin về công cụ cụm NDB, bắt đầu bằng các tham số kết nối:
Output

*************************** 1. row ***************************
  Type: ndbcluster
  Name: connection
Status: cluster_node_id=4, connected_host=198.51.100.2, connected_port=1186, number_of_data_nodes=2, number_of_ready_data_nodes=2, connect_count=0
. . .
Điều này cho thấy bạn đã kết nối thành công với Cụm MySQL của mình.
Lưu ý ở đây số lượng ready_data_nodes: 2. Sự dư thừa này cho phép cụm MySQL của bạn tiếp tục hoạt động ngay cả khi một trong các nút dữ liệu bị lỗi. Điều đó cũng có nghĩa là các truy vấn SQL của bạn sẽ được cân bằng tải trên hai nút dữ liệu.
Bạn có thể thử tắt một trong các nút dữ liệu để kiểm tra độ ổn định của cụm. Thử nghiệm đơn giản nhất sẽ là khởi động lại nút nhỏ giọt dữ liệu để kiểm tra đầy đủ quá trình khôi phục. Bạn sẽ thấy giá trị number_of_ready_data_nodesthay đổi 1và sao lưu 2trở lại khi nút khởi động lại và kết nối lại với Trình quản lý cụm.
Để thoát dấu nhắc MySQL, chỉ cần gõ quithoặc nhấn CTRL-D.
Đây là thử nghiệm đầu tiên chỉ ra rằng cụm, máy chủ và máy khách MySQL đang hoạt động. Bây giờ chúng ta sẽ trải qua một thử nghiệm bổ sung để xác nhận rằng cụm đang hoạt động đúng.
Mở bảng điều khiển quản lý Cluster, ndb_mgmsử dụng lệnh:
•	ndb_mgm
•	
Bạn sẽ thấy đầu ra sau:
Output
-- NDB Cluster -- Management Client --
ndb_mgm>
Khi vào trong bàn điều khiển, nhập lệnh SHOWvà nhấn ENTER:
•	SHOW
•	
Bạn sẽ thấy đầu ra sau:
Output
Connected to Management Server at: 198.51.100.2:1186
Cluster Configuration
---------------------
[ndbd(NDB)] 2 node(s)
id=2    @198.51.100.0  (mysql-5.7.22 ndb-7.6.6, Nodegroup: 0, *)
id=3    @198.51.100.1  (mysql-5.7.22 ndb-7.6.6, Nodegroup: 0)

[ndb_mgmd(MGM)] 1 node(s)
id=1    @198.51.100.2  (mysql-5.7.22 ndb-7.6.6)

[mysqld(API)]   1 node(s)
id=4    @198.51.100.2  (mysql-5.7.22 ndb-7.6.6)
Ở trên cho thấy có hai nút dữ liệu được kết nối với node-ids 2 và 3. Ngoài ra còn có một nút quản lý với node-id1 và một máy chủ MySQL với node-id4. Bạn có thể hiển thị thêm thông tin về mỗi id bằng cách nhập số của nó bằng lệnh STATUSnhư sau:
•	2 STATUS
•	
Lệnh trên cho bạn thấy trạng thái, phiên bản MySQL và phiên bản NDB của nút 2:
Output
Node 2: started (mysql-5.7.22 ndb-7.6.6)
Để thoát khỏi loại bàn điều khiển quản lý quit, và sau đó nhấn ENTER.
Bảng điều khiển quản lý rất mạnh mẽ và cung cấp cho bạn nhiều tùy chọn khác để quản trị cụm và dữ liệu của nó, bao gồm tạo bản sao lưu trực tuyến. Để biết thêm thông tin tham khảo tài liệu chính thức của MySQL .
Tại thời điểm này, bạn đã kiểm tra đầy đủ cài đặt MySQL Cluster của mình. Bước kết thúc của hướng dẫn này chỉ cho bạn cách tạo và chèn dữ liệu thử nghiệm vào Cụm MySQL này.
Bước 5 - Chèn dữ liệu vào cụm MySQL
Để thể hiện chức năng của cụm, hãy tạo một bảng mới bằng cách sử dụng công cụ NDB và chèn một số dữ liệu mẫu vào đó. Lưu ý rằng để sử dụng chức năng cụm, động cơ phải được chỉ định rõ ràng là NDB . Nếu bạn sử dụng InnoDB (mặc định) hoặc bất kỳ công cụ nào khác, bạn sẽ không sử dụng cụm.
Đầu tiên, hãy tạo một cơ sở dữ liệu được gọi clustertestbằng lệnh:
•	CREATE DATABASE clustertest;
•	
Tiếp theo, chuyển sang cơ sở dữ liệu mới:
•	USE clustertest;
•	
Bây giờ, tạo một bảng đơn giản gọi là test_tablenhư thế này:
•	CREATE TABLE test_table (name VARCHAR(20), value VARCHAR(20)) ENGINE=ndbcluster;
•	
Chúng tôi đã chỉ định rõ ràng động cơ ndbclusterđể sử dụng cụm.
Bây giờ, chúng ta có thể bắt đầu chèn dữ liệu bằng truy vấn SQL này:
•	INSERT INTO test_table (name,value) VALUES('some_name','some_value');
•	
Để xác minh rằng dữ liệu đã được chèn, hãy chạy truy vấn chọn sau:
•	SELECT * FROM test_table;
•	
Khi bạn chèn dữ liệu vào và chọn dữ liệu từ một ndbclusterbảng, tải cụm sẽ cân bằng các truy vấn giữa tất cả các nút dữ liệu có sẵn. Điều này cải thiện tính ổn định và hiệu suất của việc cài đặt cơ sở dữ liệu MySQL của bạn.
Bạn cũng có thể đặt công cụ lưu trữ mặc định thành ndbclustertrong my.cnftệp mà chúng tôi đã chỉnh sửa trước đó. Nếu bạn làm điều này, bạn sẽ không cần chỉ định ENGINEtùy chọn khi tạo bảng. Để tìm hiểu thêm, tham khảo Hướng dẫn tham khảo MySQL .
	

e.	Hướng dẫn Sử dụng/Quản trị [Mô tả các việc phải thiết lập, sử dụng MySQL Cluster để tạo ra các chức năng Sản phẩm hoặc Cấu hình của giải pháp] 

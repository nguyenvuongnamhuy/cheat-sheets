# Table of Contents

- [Introduce](#introduce)
- [Load Balancing](#load-balancing)
- [Restful API](#restful)
- [GraphQL](#graphql)
- [gRPC](#grpc-remote-procedure-call)
- [Kafka](#kafka)
- [Rabbitmq](#rabbitmq)
- [Typescript](#typescript)
- [Nestjs](#nestjs)
- [Monolithic](#monolithic)
- [Microservice](#microservice)
- [NodeJS](#nodejs)
- [ExpressJS](#express)
- [ORM](#orm-object-relational-mapping)
- [Design Pattern](#design-pattern)
- [Docker](#docker)
- [Authentication & Authorization](#authentication--authorization)
- [Postgres](#postgres)
- [Redis](#redis)
- [Socket](#socketio)
- [FE](#reactjs-nextjs)
- [Nginx](#nginx)
- [Dự án hiện tại](#dự-án-hiện-tại)
- [Agile Scrum](#agile---scrum)
- [Các câu hỏi phỏng vấn senior](#các-câu-hỏi-mẫu-phỏng-vấn-senior-nodejs)

# Introduce

- Hi I'm Huy, I'm a candidate for the fullstack nodejs developer position
- I have 5 years experiences programming in server site with javascript, nodejs and relative frameworks
- Further more I also work in client site with reactjs but I prefer working at the server site
- At work, I'm a responsible person, always try to complete tasks on time, no stop learning & researching about new technology
- And a little bit of my personality, everyone told me that i'm a humorous and sociable person when outside of work

# Load balancing

- là một kỹ thuật cân bằng tải được sử dụng để phân tán lượng truy cập từ phía người dùng
- nhằm cải thiện hiệu suất, độ tin cậy, và khả năng mở rộng của hệ thống

# RESTful

- là một tiêu chuẩn dùng trong việc thiết kế các API cho các ứng dụng web để quản lý các resource.
- thông qua giao thức http và định dạng dữ liệu là JSON, XML

# GraphQL

- là một ngôn ngữ truy vấn được phát triển bởi Facebook
- cho phép phía client xác định chính xác dữ liệu mà họ cần từ server
- tăng tính linh hoạt và giảm số lượng dữ liệu không cần thiết được truyền qua mạng

# gRPC (Remote Procedure Call)

- được dùng để gọi hàm trực tiếp từ server
- sử dụng giao thức http2 và định dạng dữ liệu là protobuf (mã hoá và giải mã dạng nhị phân)

# Kafka

- được thiết kế để xử lý khối lượng lớn dữ liệu trong thời gian thực
- cho phép truyền thông tin giữa các ứng dụng hoặc hệ thống một cách hiệu quả
- có khả năng mở rộng cao và chịu tải tốt và chịu lỗi cao

# RabbitMQ

- sử dụng mô hình đẩy
- giám sát việc xử lý thông điệp, các trình này sẽ xóa thông điệp sau khi thông điệp được xử lý
- gửi hàng ngàn thông điệp mỗi giây

# Typescript

- là ngôn ngữ biên dịch mã nguồn mở được phát triển bởi MS
- là siêu ngữ của javascript, nghĩa là có thể viết code javascript trong file ts
- biên dịch thành javascript để chạy ở client và server
- ưu điểm:
  - kiểu dữ liệu tĩnh: các biến các hàm đều có kiểu dữ liệu -> rõ ràng, dễ hiểu
  - dễ dàng phát hiện lỗi
  - có tính hướng đối tượng: abstract class, interface

# NestJS

- là framework của nodejs, được xây dựng theo kiến trúc modular
- các thành phần chính: module, controller, provider
- những thành phần quan trọng khác:
  - decorator
  - dependency injection
  - middleware
  - interceptor
- ưu điểm:
  - kiến trúc modular: cho phép tách biệt mã nguồn thành các module độc lập, giúp việc quản lý và mở rộng trở nên dễ dàng
  - hỗ trợ typescript
  - hỗ trợ viết test (jest)
  - cộng đồng sử dụng lớn
- nhược điểm:
  - cấu trúc phức tạp
  - hiệu suất kém hơn những framework nhẹ khác

# Monolithic

- Concept
  - Has single code base with multiple modules
  - Has single build system which build entire app and/or dependency
  - Has single executable or deployable binary
  - Sometime be called multi-tier architecture because monolithic apps are divided in 3 or more layer
    -> i.e presentation, business, database, application, ...
- Disadvantage
  - Add new feature -> code base, user base grown -> complicated
  - Scaling become challenging
  - Continuous integration/deployment become complex and time consuming
    -> require dedicated team for build/deploy
  - Large code base makes IDE slow, build time increase
  - Difficult to change technology/language/framework
    -> because everything is tightly coupled and depend up on each other

# Microservice

- là một kiếu kiến trúc phần mềm
- các module trong phần mềm này được chia thành các service nhỏ, độc lập
- mỗi service tập trung vào một chức năng hoặc trách nhiệm riêng
- mỗi service quản lý 1 database riêng và có thể share dữ liệu với nhau
- mỗi service có thể chạy trên nhiều máy khác nhau
- ưu điểm:
  - có khả năng mở rộng
  - dễ bảo trì
  - độc lập (có thể sử dụng nhiều ngôn ngữ/công nghệ cho từng service)
- nhược điểm:
  - độ phức tạp cao, khó quản lý
  - khó khăn trong giao tiếp giữa các service
  - quy trình devops phức tạp

# NodeJS

- là mã nguồn mở được xây dựng trên nền tảng v8 engine được phát triển bởi Google
- cho phép chạy mã javascript phía server
- sử dụng mô hình đơn luồng, cơ chế non-blocking và event loop
- ưu điểm:
  - đơn luồng: giảm thiểu việc tranh chấp tài nguyên
  - non-blocking: có thể chạy các tác vụ song song mượt mà và nhanh chóng, hiệu suất cao
  - V8 engine được thiết kế để tăng hiệu suất và biên dịch mã JavaScript thành mã máy một cách nhanh chóng
- nhược điểm:
  - đơn luồng: bị chặn nếu thực hiện tác vụ nặng hoặc crash
  - asynchorus: bất đồng bộ nên có khả năng bị callback hell

# Express

- là framework nổi tiếng dành cho nodejs, giúp phát triển ứng dụng backend và xây dựng APIs nhanh chóng
- các bước tạo máy chủ http và tạo API đơn giản
- ưu điểm:
  - cộng đồng lớn
  - dễ dàng tích hợp với nhiều thư viện khác
  - hỗ trợ middleware: cho phép chen phần xử lý khác trước khi xử lý yêu cầu
- nhược điểm:
  - không có cấu trúc cố định

# ORM (Object Relational Mapping)

- là thư viện dùng để tương tác với nhiều loại database bằng cách sử dụng kiểu đối tượng thay vì truy vấn trực tiếp
- ưu điểm:
  - có hỗ trợ typescript
  - rõ ràng, dễ hiểu và dễ bảo trì
  - hướng đối tượng: tạo ra các entity đại diện cho các table trong database
  - hỗ trợ mối quan hệ giữa các bảng
  - hỗ trợ migration: theo dõi các thay đổi
- nhược điểm:
  - độ phức tạp cao, yêu cầu hiểu sql thuần trước
  - hạn chế đối với những truy vấn phức tạp

# Design pattern

- là bộ khung, là mẫu thiết kế các giải pháp dùng để giải quyết các vấn đề phổ biến trong lập trình và phát triển phần mềm
- cấu trúc hệ thống rõ ràng, dễ hiểu dễ bảo trì
- có 3 loại:
  - creational patterns: tạo ra đối tượng và quản lý vòng đời của chúng
  - structural patterns: tạo ra cấu trúc linh hoạt và dễ mở rộng, dễ bảo trì
  - behavioral patterns: tạo ra cách các đối tượng tương tác với nhau, chia sẻ trách nhiệm giữa các lớp

# Docker

- docker là một nền tảng và công cụ cho phép các nhà phát triển tạo, triển khai, và chạy các ứng dụng trong các container
- container bao gồm mọi thứ cần thiết để chạy một ứng dụng, như mã, thư viện, và các cấu hình

# Authentication & authorization

- jwt
  - sử dụng thuật toán ký để tạo ra token dựa vào header, secret_key và payload
  - jwt.sign: tạo ra token dựa vào secret_key, payload càng lớn token càng dài
  - jwt.verify:
    - so sánh secret_key truyền vào trùng khớp với secret_key trong token
    - check expired time
    -> return payload
- bcrypt
  - bcrypt là một thuật toán mã hóa dùng để băm và kiểm tra mật khẩu một cách an toàn
  - bảo vệ mật khẩu người dùng bằng cách băm mật khẩu trước khi lưu trữ và sau đó so sánh giá trị băm khi xác thực
  - bcrypt.hash: băm mật khẩu người dùng dựa vào salt, salt càng cao băm càng nhiều lần -> bảo mật cao nhưng chậm
  - bcrypt.compare: băm mật khẩu người dùng nhập vào và compare với hash password lưu trong database
- refresh token
  - được dùng để yêu cầu cấp access token mới khi access token hết hạn và có thời hạn dài hơn access token
  - khác access token về scope trong payload để tránh dùng thay cho access token

# Postgres

- là một hệ quản trị cơ sở dữ liệu quan hệ mã nguồn mở
- nổi tiếng với tính tuân thủ chuẩn SQL: có đầy đủ các lệnh insert, delete, update, join, primary key, foreign key, constraints, ...
- ưu điểm: kiểu dữ liệu json
  - có khả năng mở rộng để tăng hiệu suất ví dụ như replication
  - replication: truyền các bản ghi chứa sự thay đổi từ main db -> replica db
    - streaming sao lưu cả cấu trúc bảng theo thời gian thực (thêm cột)
    - physical giống như streaming nhưng không sao lưu theo thời gian thực
    - logical chỉ sao lưu theo các lệnh insert, update, delete

# Redis

- là một cơ sở dữ liệu lưu trữ trong RAM, được thiết kế để cung cấp hiệu suất cao và độ trễ thấp
- cung cấp hiệu suất cao và độ trễ thấp
- ứng dụng làm cache, database không cần tính bền vững (vì lưu trên RAM), realtime không cần giữ connection như socket
- ưu điểm:
  - lưu dữ liệu trong RAM, giúp truy xuất nhanh hơn nhiều so với cơ sở dữ liệu lưu trữ trên đĩa cứng
  - kiểu dữ liệu da dạng: string, list, set, hash, zset
  - hỗ trợ cơ chế pub/sub
  - hỗ trợ replication
  - có thể dùng làm message queue: không phù hợp với khối dữ liệu lớn và lưu trữ message lâu dài
  - có thể dùng làm cache
  - redis search, redis hash
  - set expired time cho key

# Socket.io

- là một thư viện giúp thực hiện giao tiếp thời gian thực giữa client và server
- ưu điểm:
  - cho phép máy khách và máy chủ trao đổi dữ liệu ngay lập tức khi có thay đổi hoặc khi có sự kiện
  - cho phép truyền dữ liệu hai chiều thông qua việc lắng nghe event
  - tổ chức kết nối theo room để dễ dàng quản lý giao tiếp giữa các nhóm người dùng khác nhau
  - hỗ trợ cơ chế tự động kết nối lại và quản lý các trường hợp ngắt kết nối

# ReactJS, NextJS

- là thư viện của javascript mã nguồn mở được phát triển bởi Facebook
- giúp xây dựng giao diện nhánh chóng
- đặc điểm chính:
  - được thiết kế dựa trên kiến trúc thành phần, các component đó có thể dễ dàng tái sử dụng
  - virtual DOM: những thay đổi sẽ được cập nhật vào virtual DOM sau đó tính toán những thay đổi cần thiết để cập nhật vào DOM thật -> tăng hiệu suất
- render:
  - lần đầu: tạo ra cây thành phần dựa trên cấu trúc JSX, chuyển đổi thành các phần tử DOM và được gắn vào DOM thật
  - lần 2 trở đi: khi có sự thay đổi về state hoặc props sẽ kích hoạt quá trình cập nhật Virtual DOM và tính toán các thay đổi cần thiết để đồng bộ với DOM thật
- Client-side rendering:
  - sử dụng đối với dữ liệu động, theo tương tác của người dùng
  - ít khi reload lại web, tăng trải nghiệm người dùng (single page app)
- Server-side rendering (NextJS):
  - sử dụng đối với dữ liệu tĩnh, render 100% từ server
  - render trước ở server nên tốc độ load nhanh

# Nginx

- được sử dụng để xử lý mã hóa SSL/TLS, giúp bảo mật ứng dụng React.js và bảo vệ dữ liệu truyền qua mạng
- đảm bảo rằng ứng dụng của bạn tuân thủ các tiêu chuẩn bảo mật
- hỗ trợ load balancing

# Dự án hiện tại

- hiểu sâu về dự án đang làm
  - tạo ra hệ thống để giúp offshore chuyển đổi từ SI -> BL
  - queue management
    - tạo queue (SI)
      - luồng esi
        - nhận message từ kafka
        - validate request master, doc type code và check type insert
        - xử lý logic cho nhiều field
        - sau đó lưu vào database
          - doc_queue: master data (thông tin chung 1 queue)
          - doc_queue_detail: detail data (lịch sử update queue)
          - doc_queue_history: lịch sử phiên làm việc cuối cùng của queue (bao gồm thời gian work start, work end của user)
      - luồng email
        - nhận message từ API
        - xử lý tương tự luồng esi
    - timeleft
      - bắn kafka message sau khi đã tạo queue
      - xác định 12 điều kiện của booking number đó bên service khác
      - mang đi tìm bộ rules tương ứng (bên iam service)
      - sau đó tính timeleft cho tất cả các rules tương ứng
      - xác định loại rule cần thiết cho booking number đó (same day, next day, since si receive)
      - sau đó chọn ra 1 rule trong những rule cùng loại có deadline gần nhất và lưu vào database
      - tính timeleft của tất cả queue khi load page
      - recalculate timeleft của tất cả queue đang active
      - recalculate timeleft của tất cả queue mà có 1 trong 12 điều kiện bị thay đổi
    - authentication
      - hiển thị tất cả booking number trên dashboard theo country go-live của user
      - hiển thị theo 3 level theo account của user
        - level 1: theo offshore (doc center id)
        - level 2: theo team
        - level 3: theo booking office
  - inquiry management
    - confirm với onshore/customer về SI trước khi xuất ra BL
    - cho phép offshore và onshore/customer trao đổi về các thông tin trên SI
    - tạo trang admin để offshore quản lý các booking numbers
    - tạo ra workspace để offshore/onshore/customer trao đổi với nhau
    - các chức năng chính:
      - luồng inquiry
        - offshore đặt câu hỏi
        - gửi email
        - onshore/customer trả lời
        - offshore/onshore/customer mở lại câu hỏi
        - offshore resolve
        - offshore upload
      - luồng amendment
        - offshore tạo DraftBL để gửi cho customer confirm
        - customer tạo sửa đổi (amendment)
        - gửi email
        - offshore trả lời
        - offshore/customer mở lại câu hỏi
        - offshore resolve
        - offshore upload
        - customer bấm confirm nếu mọi thứ ok -> tạo BL
- challenges về admin dashboard:
  - truy vấn quá chậm do join nhiều bảng
    - solution: đánh index, tối ưu hoá query, optimize logic code, cdc data sang table mới

# Agile - scrum

# Các câu hỏi mẫu phỏng vấn senior nodejs

- index trong postgres ?
  - b-tree
  - unique
  - compound
- tối ưu performance dự án nodejs như thế nào ?
  - đánh index cho column
  - tối ưu hoá query (tránh dùng select \*, tránh join nhiều bảng) và đánh chỉ mục index cho colummn
  - tránh sql injection
  - dùng caching (redis) để giảm tải truy vấn xuống database
  - dùng promise all
  - tối ưu hoá CPU
    - clustering: chạy nhiều tiến trình Node.js song song, tận dụng các lõi CPU khác nhau
    - load balancer: round robin
- security cho api như thế nào ?
  - sử dụng https
  - authenticate and authorize
  - sử dụng các Header bảo mật
- init source cần làm những gì ?
  - init source
  - tạo structure
    - router
    - controller
    - service
    - repository
    - database module
    - middleware
    - log module
    - enviroment
    - test
    - CI/CD
  - eslint, prettier

---

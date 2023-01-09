[Training bồi dưỡng kỹ năng nghiệp vụ](./_training_term_for_practical_standard-vn.md) > Chapter 01

# Chapter 01

Làm báo cáo về cách thức tạo template của Wordpress và submit cho manager. 

**Yêu cầu khi thao tác**

1. Báo cáo thực hiện dưới hình thức Markdown. 
2. Báo cáo sẽ được lưu trong github của account cá nhân. 
3. Khi research, phải đảm bảo nội dung báo cáo được ghi chép lại bằng từ ngữ của bản thân, không được copy - paste từ các website tham khảo. 
4. Đảm bảo trong báo cáo có phần giải thích cho các mục dưới đây:
   Khái quát về Wordpress
   - Cấu tạo file nguồn (core file) của Wordpress
   - Cách thức kết nối tới database. 
   - Xử lý vòng lặp (loop) cho bài post cơ bản trong Wordpress theme. 
   - Cấu tạo file template - Các file thiết yếu.
   - Nội dung hàm số `the_title()`, `get_the_title()` và sự khác nhau giữa chúng
   - Nội dung hàm số `get_stylesheet_directory_uri()`, `get_stylesheet_directory()` và sự khác nhau giữa chúng

**Đề bài và lưu ý**

Tư liệu trên nền tảng WEB có nhiều thông tin chưa được xác thực rõ ràng hoặc ý kiến từ các cá nhân thiếu kiến thức chuyên môn kỹ thuật, vì vậy phải cố gắng tìm và tham khảo các tài liệu referece chính thống. 

# Trả lời
## Khái quát về Wordpress
### **1. Cấu tạo file nguồn (core file) của Wordpress**
Mã nguồn Wordpress gồm các folders/files chính như sau:
- wp-admin: chứa các file liên quan đến toàn bộ trang dashboard của Wordpress, không nên thay đổi gì trong thư mục này.
- wp-content: gồm các folder
  + languages: chứa các file liên quan đến ngôn ngữ của Wordpress. 
  + themes: chứa tất cả các themes đã được thêm, ngoài ra mình cũng có thể tải theme trực tiếp vào đây, sau đó kích hoạt ở màn hình quản lý theme. Mặc định khi tải Wordpress sẽ có  1 hoặc vài themes mẫu có sẵn.
  + upload: chứa tất cả các file được upload.
  + plugins: chứa các plugin đã được cài đặt, ngoài ra mình cũng có thể upload hoặc xóa download các plugin tại đây(nếu cần thiết), sau đó kích hoạt ở màn hình quản lý và sử dụng plugin như thường.
- wp-include: chứa các chức năng của Wordpress.
- index.php: Tập tin index tải và khởi tạo tất cả các file WordPress khi một trang được yêu cầu bởi người dùng.
- license.txt: chứa license của Wordpress, cho bạn biết mình có quyền sử dụng là gì, ...
- readme.html: như file README.md, chỉ là file hướng dẫn ban đầu.
- wp-activate.php: File dùng để xác nhận qua email khi user đăng ký hoặc đăng nhập, hoặc quên mật khẩu, ... 
- wp-blog-header.php: dùng để load thư viện và theme của Wordpress.
- wp-comments-post.php: dùng để xử lý bình luận.
- wp-config.php: dùng để kết nối với cơ sở dữ liệu. Bên cạnh đó, nó được dùng để đặt ra một số thiết lập chung cho trang web như đường dẫn trang web (url), bật/tắt debug, tăng bộ nhớ cho PHP (WP_MEMORY_LIMIT), vô hiệu hóa tính năng tự động cập nhật của wordpress,...
- wp-config-sample.php: file config mẫu của wordpress, có thể xóa file này.
  Tham khảo:[tại đây] (https://developer.wordpress.org/apis/wp-config-php/)      
- wp-cron.php: lên lịch thực hiện các tác vụ định kỳ, có thể là hàng ngày, hàng tuần, hàng tháng,...
- wp-links-opml.php: Khi sử dụng export trong dashboard các liên kết sẽ không được export, do đó file này sẽ dùng cho việc xử lý export các liên kết đó, các liên kết này sẽ được thể hiện dưới dạng cấu trúc XML.
- wp-load.php: dùng để liên kết, điều hướng để load các nội dung Wordpress khi được yêu cầu.
- wp-login.php: dùng để hiển thị và xử lý nội dung đăng nhập. 
- wp-mail.php: xử lý nhận tin nhắn từ hộp thư của người dùng để hiển thị dưới dạng post.
- wp-settings.php: Cài đặt và cấu hình chung cho Wordpress.
- wp-signup.php: dùng để hiển thị và xử lý nội dung đăng ký.
- wp-trackback.php
- xmlrpc.php: File này giúp Wordpress giao tiếp với các hệ thống/thiết bị bên ngoài, ví dụ như dùng điện thoại để chỉnh sửa, theo dõi, ...
- .htaccess: Một trong những file quan trong và không thể thiếu nếu sử dụng wordpress cũng như các mã nguồn khác. Một tập tin cấu hình máy chủ WordPress sử dụng nó để quản lý Permalinks và chuyển hướng.

### **2. Cách thức kết nối tới database.** 
**Cách này hướng dẫn kết nối database với wordpress trên localhost, làm trên hosting thì tương tự như vậy**
- **Bước 1:** Vào myPHPadmin => Tạo database mới.
- **Bước 2:** Đặt tên database, charset (kế bên database name) -> chọn "utf8_unicode_ci",username, password
- **Bước 3:** Click "Go" để tạo database
- **Bước 4:** Mở file wp-config.php của wordpress lên, tìm đến mục thiết lập database và thay đổi thành thông tin database đã tạo bên trên.
define('DB_NAME', '**tên databse**');
define('DB_USER', '**username**');
define('DB_PASSWORD', '**password**');
define('DB_HOST', 'localhost');
define('DB_CHARSET', 'utf8');

### **3. Xử lý vòng lặp (loop) cho bài post cơ bản trong Wordpress theme.**
Chèn vòng lặp trong template mà mình muốn hiẻn thị, ví dụ: header.php, footer.php,php, index.php,...
Lấy ví dụ code bên dưới để hình dung:
```
<?php
    if( have_posts() ) : while ( have_posts() ) : the_post();
?> <!–Đóng PHP để viết HTML tiện hơn ở dưới–>
    <!–Nội dung một bài viết–>
    <article <?php post_class() ?> >
        <h1><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h1>
        <summary>
            <?php the_content(); ?>
        </summary>
        <footer>
            <?php the_tags(); ?>
        </footer>
    </article>
    <!–kết thúc nội dung–>

<?php endwhile; endif; // Kết thúc vòng lặp ?>
```
Trong đó: 
-  if( $wp_query->have_posts() ): have_posts() trả về true thì vòng lặp white được thực hiện.
- while( $wp_query->have_posts() ): Nếu have_posts() == TRUE thì vòng lặp tiếp tục thực hiện, không thì ngừng.
- $wp_query->the_post(): Thiết lập số thứ tự bài viết trong chỉ mục của query.
- echo $post->post_title: in ra màn hình title của bài post.
**Note:** 
1. Để giới hạn kết quả hiển thị của vòng lặp trên một trang. Ta vào dashboard => Setting => Reading => Tại mục "Blog Pages show at most" nhập số lượng mà mình muốn hiển thị.
2. Để xem chính xác trên trang có bao nhiêu query, và nó gửi như thế nào thì chúng ta phải debug mới thấy được. Cách đơn giản nhất là mình cài plugin Debug Bar sau đó vào wp-config.php chèn đọan code bên dưới vào file:
```
define( ‘SAVEQUERIES’, true );
```
3. Kết quả của query sẽ được lưu vào đối tượng $wp_query.
**Tham khảo:**[SỬ DỤNG WP QUERY VÀ LOOP (VÒNG LẶP) ĐỂ LẤY BÀI VIẾT] (https://thachpham.com/wordpress/wordpress-development/su-dung-wp-query-va-loop-vong-lap-de-lay-bai-viet.html)

### **4. Cấu tạo file template - Các file thiết yếu.**
- Templatecó thể được hiểu như là một cái khuôn mẫu được định dạng sẵn nhằm mục đích hiển thị nội dung trên website. 
- Một theme trong wordpress thì gồm nhiều file template.
- Cấu tạo file template. Để 1 trang web wordpress hoạt đông được thì ta cần một số file template thiết yếu bên dưới.<br>
![Cấu tạo file template](https://thachpham.com/wp-content/uploads/2015/07/twentyfifteen-template.jpg)
- Trong đó: 
    + style.css: Tập tin này không chỉ là chứa các CSS trong theme mà nó còn có chức năng khai báo thông tin của theme như tên theme, tên tác giả, số phiên bản,…nhằm có thể hiển thị trong khu vực Themes của WordPress. Nếu theme không có tập tin này thì theme không được xem là hợp lệ. Không nên xóa các thông tin về theme trong file style.css
    + function.php: chứa những đoạn code PHP để khai báo các tính năng đặc biệt, hoặc sử dụng hàm add_theme_support() để khai báo các tính năng trong theme. functions.php không phải là template nên nó sẽ không hiển thị ra bên ngoài nhưng mà nó sẽ được thực thi, và tất cả code PHP trong đây sẽ được thực thi khi website được tải ra.
    + index.php: là template để sử dụng cho trang chủ, mà nó còn là template gốc của website nếu như các template khác chưa được khai báo. Ví dụ nếu theme không có tập tin single.php để làm template cho trang nội dung của Post, thì nó sẽ sử dụng tập tin index.php để hiển thị. Các template khác cũng vậy.
    + header.php: dùng để khai báo phần header của trang, bao gồm các thẻ như <html>, <head>, <body>,…Và sau đó ở các template khác, chúng ta sẽ gọi nó ra bằng template tag get_header().
    + footer.php: cũng giống như header.php đó là được sử dụng để khai báo phần chân trang của theme. Rồi sau đó ở các template khác ta sẽ gọi nó ra bằng get_footer().
    + sidebar.php: có thể khai báo sidebar trực tiếp vào các template khác với hàm dynamic_sidebar() nhưng nếu mình cần sử dụng sidebar ở nhiều template khác nhau thì ta nên viết code hiển thị sidebar vào tập tin sidebar.php. Rồi sau đó sẽ dùng hàm get_sidebar() để gọi template này ra.
**Các template khác trong theme**
Các template dưới đây nó sẽ không bắt buộc mình phải tạo ra như các tập tin ở trên, nhưng nó sẽ được sử dụng nếu như ta có khai báo. Template nào không khai báo thì nó sẽ sử dụng template cấp cao hơn. Ví dụ nếu single-child.php không khai báo thì nó sẽ sử dụng single.php.
#### **4.1 Template hiển thị trang lưu trữ**
Template này sẽ sử dụng cho tất cả các trang lưu trữ trên website. Trang lưu trữ là các trang phân loại bài viết như category, tag, custom taxonomy,…
- **archive.php** – Định dạng hiển thị cho toàn bộ trang lưu trữ trên website như lưu trữ theo ngày tháng, category, tag, custom taxonomy,..
- **category.php** – Định dạng hiển thị cho toàn bộ category của website.
    + **category-tin-tuc.php** – Định dạng hiển thị trang category có slug là tin-tuc.
    + **category-123.php** – Định dạng hiển thị cho category mang ID 123.
- **tag.php** – Định dạng hiển thị toàn bộ tag của website.
    + **tag-tin-tuc.php** – Định dạng hiển thị toàn bộ tag có slug là tin-tuc.
    + **tag-123.php** – Định dạng hiển thị toàn bộ tag có ID là 123.
- **author.php** – Định dạng hiển thị cho trang toàn bộ các tác giả trong website.
    + **author-admin.php** – Định dạng trang hiển thị tác giả tên admin.
    + **author-123.php** – Định dạng trang hiển thị tác giả có ID là 123.
- **archive-product.php** – Định dạng trang hiển thị danh sách các bài viết thuộc post type tên product.
- **taxonomy-product-category.php** – Định dạng trang hiển thị danh sách các bài viết thuộc custom taxonomy tên product-category.
#### **4.2 Template hiển thị trang nội dung**
Template này sẽ định dạng cho trang hiển thị nội dung của Post hoặc Page hoặc một Custom Post Type nào đó.
- **single.php** – Định dạng trang hiển thị nội dung của tất cả các Post.
    + **single-product.php** – Định dạng trang hiển thị nội dung tất cả các post trong post type tên product.
    + **single-hello.php** – Định dạng trang hiển thị nội dung của post có slug là hello.
    + **single-123.php** – Định dạng trang hiển thị nội dung của post mang ID là 123.
- **page.php** – Định dạng hiển thị toàn bộ Page trong website.
    + **page-123.php** – Định dạng hiển thị page có ID là 123.
### **4.3 Template trang chủ**
Các template này sẽ được sử dụng cho việc định dạng hiển thị của trang chủ.
- index.php
- front-page.php
- home.php
### **4.4 Template trang 404**
Template này sẽ hiển thị lỗi 404 trong website, và nó chỉ có 1 tập tin duy nhất là 404.php.
### **4.5 Template trang kết quả tìm kiếm**
Khi sử dụng chức năng tìm kiếm trên website, kết quả tìm kiếm sẽ được hiển thị bằng template search.php. Nếu search.php không tồn tại thì nó sẽ dùng archive.php.
## **5. Nội dung hàm số `the_title()`, `get_the_title()` và sự khác nhau giữa chúng**
- **the_title()** Hiển thị tiêu đề post hiện tại trong truy vấn.
- **get_the_title()** truy xuất tiêu đề bài đăng bằng cách sử dụng id bài đăng tùy chọn, id của nội dung cụ thể được chuyển dưới dạng tham số, id bài đăng mặc định get_the_title bằng 0 có nghĩa là hầu hết tiêu đề bài đăng hiện tại
Sự khác nhau giữa get_the_title() với the_title()
| the_title()    |get_the_title() |
|: -------- |: ------- |
| Sử dụng trong vòng lặp  | Được sử dụng bên ngoài vòng lặp để truy xuất một bài post    |
| Không cần thêm gì ở phía trước | khi viết phải thêm "echo" phía trước     |
| Nhận ba tham số tùy chọn, hai tham số đầu tiên là tham số tùy chọn chuỗi, ví dụ: <?php the_title('<h1>','</h1>');?> và tham số thứ ba là boolean. Nếu thay tham số thứ ba bằng false sẽ khiến the_title in tiêu đề bài đăng bằng cách lặp lại. the_title sẽ chỉ xuất ra một tiêu đề bài đăng, tiêu đề mới nhất. Vì vậy, bạn sẽ không thể truy xuất các tiêu đề khác của bài đăng.  | Chỉ nhận một tham số tùy chọn là số của bài đăng (id bài đăng) hoặc đối tượng WP_Post để lấy các dữ liệu khác của bài đăng như tiêu đề của bài đăng gốc.    | 
## **6. Nội dung hàm số `get_stylesheet_directory_uri()`, `get_stylesheet_directory()` và sự khác nhau giữa chúng**

- **get_stylesheet_directory_uri()** được dùng để hiển thị hình ảnh được lưu trữ bên trong thư mục /images bên trong thư mục của child theme.
- **get_stylesheet_directory()** Khi bạn cần phải include file khác vào bên trong cấu trúc thư mục, bạn cần sử dụn get_stylesheet_directory(). Từ style.css trong thư mục parent theme, get_stylesheet_directory() trỏ tới thư mục trong child theme của bạn (không phải trong parent theme). Để tham chiếu đến thư mục này bạn sử dung get_template_directory() để thay thế.
- Sự khác nhau giữa get_stylesheet_directory_uri() với get_stylesheet_directory()
    - **get_stylesheet_directory_uri()** cung cấp URL, được sử dụng với các tài nguyên front-end.
    - **get_stylesheet_directory()** cung cấp đường dẫn của file.

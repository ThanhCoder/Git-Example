I: SQL
- Case 1: Create Database and Table, Insert information into table.

    Create database Language_HT;

    Create table Language(id int not null auto_increment,
    popularity varchar(10),language varchar(50), primary key(id);

    Insert table Language(popularity,language) values('100','PHP'),
    ('200','PYTHON'),('300','JAVA'),('400','NODEJS');

- Case 2: Category list from lowest to highest.

    Select language,popularity from Language order by popularity DESC;

        RESULT:

            +----------+--------------+
            | language | popularity   |
            +----------+--------------+
            | NODEJS   | 400          |
            | JAVA     | 300          |
            | PYTHON   | 200          |
            | PHP      | 100          |
            +----------+--------------+


- Case 3: The 3st highest popularity is PYTHON (n= 200, input: PYTHON)
    
    Select language from Language where popularity = 200;

II: Coding (use language PHP)
<?php
function Convert_Roman($num) {
    $n = intval($num);
    $res = '';

    /***  truyền vào mảng  ***/
    $roman_numerals = array(
        'M' => 1000,
        'CM' => 900,
        'D' => 500,
        'CD' => 400,
        'C' => 100,
        'XC' => 90,
        'L' => 50,
        'XL' => 40,
        'X' => 10,
        'IX' => 9,
        'V' => 5,
        'IV' => 4,
        'I' => 1
    );

    foreach ($roman_numerals as $roman => $number)
    {
        // chia cho số nguyên với hàm intval 
        $matches = intval($n / $number);

        /*** assign the roman char * $matches ***/
        $res .= str_repeat($roman, $matches);

        /*** rút ngắn số dư ***/
        $n = $n % $number;
    }

 return strtolower($res);
}

// Hiển thị theo tham số truyền vào
echo "Kết quả:".Convert_roman(19);
// Kết quả: XIX
?>

III: Solution
- Trình bày hiểu biết của bạn về hệ thống lưu trữ mật khẩu.

-------------------------------------------------------------------------------
* TH1: Sử dụng công cụ quản lý mật khẩu (third party) bên thứ 3.
    Hiện nay có rất nhiều công cụ hỗ trợ lưu trữ mật khẩu: Google Chrome,
    Interner Browser... tuy nhiên vẫn có những trình duyệt vẫn bắt chúng ta có 
    mật khẩu root. Tài khoản User trung bình 1 thời gian nhất định sẽ phải thiết
    lập đổi mật khẩu tránh trường hợp database bị dò gỉ ra ngoài.

    Khi người dùng tạo 1 account, mật khẩu sẽ được lưu vào hệ thống, những lần 
    đăng nhập tiếp theo sẽ tự động gợi ý nhập mật khẩu đã lưu và người dùng
    không cần phải nhập lại mật khẩu.

-------------------------------------------------------------------------------
* TH2: Lưu mật khẩu theo dạng mã hóa 

- Hàm băm(hash function) MD5: 
    Khi người dùng nhập vào dữ liệu sẽ không lưu mật khẩu dưới dạng trực tiếp
    mà lưu dưới dạng mã hóa md5, khi lưu mã hash thì khi người dùng nhập chuỗi
    sẽ băm chuỗi thành chuỗi hash và lưu chuỗi hash lại.

    + Ưu điểm:
    - Tạo chuỗi dài và phức tạp bảo vệ mật khẩu người dùng
    - Độ bảo mật cao
    + Ngược điểm:
    - Sẽ không biết nguồn gốc của mật khẩu là gì.
    - Độ rủi ro vẫn cao vì hacker có thể dịch ngược lại trên CrackStation.
    - Nếu người dùng quên mật khẩu chỉ có thể reset mật khẩu chứ không cho người
    dùng tìm lại được vì nguyên lý hash là 1 chiều, chỉ có băm tiếp và so sánh với
    chuỗi lưu trên database.

- Lưu mật khẩu sử dụng mã hóa Bcrypt:
    Sử dụng Bcrypt sẽ cải thiện an toàn hơn MD5 vì mỗi lần thực hiện sẽ sinh ra
    1 chuỗi mã hóa khác nhau cùng 1 mật khẩu nhập vào. 
-------------------------------------------------------------------------------
- TH3:
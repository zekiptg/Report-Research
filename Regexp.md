# Regular Expression Literals and Syntax trong Ruby

## 1/ Regular Expression là gì ?
Regular Expressions hay còn được gọi với cái tên ngắn gọn là Regex là một trong những công cụ để xử lý chuỗi từ đơn giản đến phức tạp mạnh mẽ nhất và được áp dụng rộng rãi nhất trong việc lập trình.

Có thể kể tới như là kiểm tra xem email có hợp lệ hay không, hay khó hơn như refactor một block code phức tạp, tìm kiếm và thay thế một số pattern cụ thể nào đó, etc.

Chỉ chừng đó thôi chúng ta có thể đủ thấy rằng Regex là một công cụ cực kì mạnh mẽ, có thể dùng trong code, có thể dùng chung với editor, và nếu bạn là một developer thực thụ thì nó là thứ không thể thiếu trong hành trang của bạn.

Hiểu một cách ngắn gọn và đơn giản thì Regex là cách để diễn tả một đoạn mẫu phức tạp dùng để tìm kiếm (search pattern) bằng một chuỗi. Ví dụ như bạn có thể check chuỗi bao gồm chữ hoặc số, hay bạn có thể đi sâu hơn là kiểm tra số lượng kí tự, vị trí của kí tự, chữ hoa, chữ thường, và nhiều hơn nữa.

## 2/ Regular Expression Literals 
* 2.1 Khái niệm

    Như ta đã được biết thì Regexp hay còn gọi là Regular Expression có thể giúp chúng ta xử lý các mẫu search pattern phức tạp nhưng làm thế nào để sử dụng nó trong ruby hay các ngôn ngữ lập trình khác. Đơn giản là bạn chỉ cần thêm dấu forward slash "/" đứng trước và cuối trong phần định nghĩa Regexp của bạn 
    
        Ví dụ: /Ruby?/ đây là một regexp 
        # Ở đây thì regexp nãy sẽ match với chuỗi Rub hoặc Ruby

* 2.2 Các modifier characters

    Không phải regexp chỉ kết thúc bởi dấu "/" mà chúng ta còn có thể thêm vào sau nó những kí tự hay còn được gọi là modifier characters

    i: Khi dùng kí tự i phía sau dấu "/" thì ta bỏ qua trường hợp phân biệt hoa thường

        Ví dụ: /ruby?/i 

        # Trong trường hợp này thì sẽ match với chuỗi ruby hoặc RUB hoặc Rub,... 
    ***
    m: Thì ta sẽ dùng trong trường hợp chuỗi chúng ta là chuỗi nhiều dòng vậy làm thế nào để ta match chuỗi nhiều dòng, đơn giản là chúng ta chỉ cần thêm dấu "." vào nơi xuất hiện dòng mới

        Ví dụ: /rub.y/m

        # Trong trường hợp nãy ta sẽ match với chuỗi 
        `Rub
        y`
        ở đây mình xuống sau khi kết thúc chũ b nên trong regexp chúng ta sẽ đạt dấu chấm sau chữ b
    ***
    x: Sẽ cho phép match với các khoảng trắng và những comments khi ta sử dụng regexp

        Ví dụ: /r uby/x

        # Thì kết quả ở đây ta vẫn match với chữ ruby
    ***
    u,e,s,n: Nếu bạn dùng regexp nhưng bạn muốn nó match với mã encoding khác thì bạn có thể dùng các option sau 
    
        u(UTF-9), e(EUC), s(SJIS), n(ASCII). Còn nếu bạn không dùng option này thì mặc định nó sẽ tự động nhận source encoding chương trình mà các bạn đang phát triển
    
    Trên đây là một số các modifier basic mà mình hay dùng và còn rất nhiều các Modifier các bạn có thể tham khảo ở đây: 


    https://www.regular-expressions.info/refmodifiers.html


 ## 3/ Regular Expression Syntax

Hiện nay thì có rất nhiều ngôn ngữ lập trình hỗ trợ regexp cũng như được cung cấp các syntax được phổ biến một cách rột rãi bởi Perl. 

Sau đây mình sẽ phân loại ra các syntax cơ bản thường hay được sử dụng trong regexp.

| Syntax | Matching |
| ------------- | ------------- |
| 1- Literal characters |    |
/ruby/ | Match với "ruby". Phải chính xác là ký tự đó
| 2- Character classes  |
/[Rr]uby/| Match với"Ruby" hoặc "ruby"
/rub[ye]/| Match với"ruby" hoặc "rube"
/[aeiou]/| Match với Nguyên âm
/[0-9]/| Mattch với Các số từ 0-9
/[a-zA-Z0-9]/| Match với ký tự thường hoa và số
/[^aeiou]/| Match với tất cả ký tự ngoài trừ nguyên âm
| 3- Special Character classes  |
/./| Match với Tất cả cả ký tự trừ ký tự xuống dòng
/\d/| Match với Ký tự là số
/\D/| Match với Ký tự không phải là số
/\s/| Match với Ký tự là khoảng trắng, như /[\t\r\n\f]/
/\S/| Match với Ký tự không phải là khoảng trắng như /[^\t\r\n\f]/
/\w/| Match với Một Ký tự, như /[A-Za-z0-9]/
/\w/| Match với Không phải là ký tự, như  /[^A-Za-z0-9]/
| 4- Repetition  |
/ruby?/| Match với "rub" hoặc "ruby
/ruby*/| Match với "rub" với 0 hoặc nhiều ký tự "y"
/ruby+/| Match với "rub" với 1 hoặc nhiều ký tự "y"
/\d{3}/| Match vớichính xác 3 ký tự là số
/\d{3,}/| Match với 3 ký tự là số hoặc nhiều hơn 3 ký tự là số
/\d{3,5}| Match với 3,4,5 ký tự là số
| 5- Grouping with parentheses  |
/([Rr]uby(, )?)+/| Match với Grouped "Ruby", "Ruby, ruby, ruby", etc.
| 6- Alternatives  |
/ruby\|rube/| Match với "ruby" hoặc "rube"
/rub(y\|le)/| Match với "ruby" hoặc "ruble"
/ruby(!+\|\?)| Match với "ruby" theo sau là một hoặc nhiều dấu ! hoặc một dấu "?"
| 7- Anchors |
/^Ruby/| Match với "Ruby" bắt đầu một chuỗi hoặc một dòng 
/Ruby$/| Match với "Ruby" kết thúc một chuỗi hoặc một dòng
/\ARuby/| Match với "Ruby" bắt đầu một chuỗi
/Ruby\Z/| Match với "Ruby" kết thúc một chuỗi
/\bRuby\b/| Match với "Ruby" chỉ duy nhất khớp với chuỗi "Ruby" trên một dòng
/\bRuby\b/| Match với "rub" trong "ruby" or "rube" ... nhưng không thể "rub" đứng một mình mà phía sau không có kí tự nào
/Ruby(?=!)/| Match với "Ruby" Nếu có kí tự ! đằng sau nó
/Ruby(?!!)/| Match với "Ruby" Nếu không có kí tự ! đằng sau nó
| 8- pecial syntax with parentheses |
/R(?#comment)/| Match với "R" còn lại là Comment
/R(?i)uby/| Match với "R" và phần còn lại có thể in hoa hoặc thường("RuBy","RUBy",...)


## 4/ Kết bài
Hi vọng bài viết của mình sẽ giúp các bạn có thêm những kiến thức về cú pháp trong regexp và có thể áp dụng kiến thức này vào trong việc xử lý chuỗi phức tạp. 

Và mình cũng xin cảm ơn các bạn đã đọc nếu có sai sót mình mong các bạn có thể góp ý cho mình để ra những bài viết chất lượng hơn nữa nhé 




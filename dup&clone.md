# Dup và Clone (Deep Copy) trong Ruby

## 1/khái niệm cơ bản về copy trong lập trình
Có hai khái niệm mà chúng ta cần nắm đó là Copy và Object 
* Copy là gì ?

    Cụ thể thì copy đơn giản chỉ là ta sao chép một thứ gì đó cũng giống như trong đời sống ta copy hay ở đây là bắt chước cách nói chuyện hay bắt chước cách cư xử, xử lý vấn đề của một người

        Còn trong lập trình ta có 2 khái niệm về Copy 
        đó là Reference Copy (Copy Tham chiếu) và Object Copy (Copy toàn bộ)
    ***
    * Reference Copy (Copy Tham chiếu)
        
        Copy Tham chiếu là khi ta gán một biến cho một object thì biến đó sẽ trỏ đến vùng nhớ của object mà nó copy. Nói có vẻ thì dài dòng lý thuyết vậy còn mình sẽ đi vào ví dụ cho mọi người có thể dễ hiểu hơn
        
            Ví dụ: Ta có Một Object là person_1 = Person.new,

            Vậy khi ta gán person_2 = person_1 thì person_2 đang trỏ đến object person 1 
            (đối với các bạn đã từng học qua C thì có lẽ đây không phải là khái niệm gì quá xa lạ). 

            Vậy khi ta thay đổi person_2 thì person_1 cũng thay đổi vì cả hai cùng đang trỏ tới một object. 
          
        Mình sẽ nói rõ hơn ví dụ này ở phần sau nên những bạn chưa hiểu lắm thì yên tâm nhé. 
    ***       
    * Object Copy (Copy toàn bộ)

        Copy toàn bộ cũng như cái tên của nó là copy toàn bộ mọi thứ mà Object đó có. 

            Ví dụ: Ta có person_1 có các thuộc tính person_1.name và person_1.adress
            thì với Object copy ta sẽ copy toàn bộ các thuộc tính này

            Nhưng giả sử  ở đây ta có thuộc tính name là một Object có hai thuộc tính khác là firstname và lastname,
            thì khi copy ta cũng sẽ copy toàn bộ các thuộc tính này của person_1.name

        Vậy Object copy là ta copy tất cả những thuộc tính, phương thức mà object đó có cũng như copy tất cả các object con của nó. 

        Trong phần này mình sẽ chỉ tập chung vào Object Copy và tiếp theo chúng ta sẽ đi vào khái niệm rất quan trọng đó là Shallow Copy và Deep Copy 
## 2/ Shallow Copy and Deep Copy    
### 2.1 Shallow Copy 
Có thể nói Shallow Copy là một Object Copy, nhưng quá trình copy chỉ copy reference (địa chỉ vùng nhớ) của object cần copy. Ví dụ sau sẽ giúp các bạn hiểu rõ hơn về Shallow Copy

    Ví dụ: ta có một Object h1 = Person.new là Object của Person Class, và ta có  biến h2 = h1 và h3 = h2. 

    Ta giả sử class Person có thuộc tính là height
    Ta có: h1.height = 165 

    Sau đây ta sẽ thực hiện phép gán h2.height = 170

    Vậy câu hỏi đặt ra ở đây liệu h1.height = 165 hay 170 ???
    Câu trả lời ở đây là h1.height = 170 
    và h3 cũng như vậy ta có h3.height bằng 170. 
    Vậy lí do ở đây là gì ???

    Như trên ví dụ trên ta có thể thấy 
    khi ta thực hiện phép gán cho một object 
    thì ta tham chiếu đến object đó 
    hay nói cách khác là ta trỏ chung đến object đó 

    (nếu bạn nào từng học qua C chắc sẽ nắm rõ khái niệm 
    con trỏ cũng như tham chiếu và tham trị)

Vậy nhược điểm của Shallow Copy là khi chúng ta thay đổi giá trị của Shallow Copy Object thì sẽ ảnh hưởng đến giá trị của Object gốc .
***
### 2.2 Deep Copy 
Deep Copy cũng là một Object Copy, nhưng Khác với Shallow Copy thì Deep Copy sẽ không copy reference tới object cần copy, mà thay vào đó sẽ tạo ra một object mới độc lập với object cần copy. Như vậy mọi thay đổi của object mới sẽ không ảnh hưởng tới object gốc. Ta có thể thấy đã khắc phục được nhược điểm của Shallow Copy.

Vậy làm thế nào để sử dụng Deep Copy. Với Ruby chúng ta sẽ có hai phương thức giúp chúng ta có thể thực hiện Deep Copy dễ dàng đó là dup và clone. 

Tại sao lại có hai phương thức mà không phải 1, chúng ta sẽ tìm hiểu ở phần tiếp theo để có thể hiểu rõ hơn hai phương thức này và sự cần thiết của chúng trong lập trình Ruby.
## 3/ Dup và Clone trong Ruby
Ta có thể thấy không có gì khác biệt giữa dup và clone thông qua ví dụ minh họa sau:

Sử dụng dup:

    test = {:a => 1, :b => 2 } 
    a = test.dup 
    a[:a] = 3
    => a = {:a => 3,:b => 2 }
    test
    => {:a => 1, :b => 2 }

Sử dụng clone

    test = {:a => 1, :b => 2 } 
    a = test.dup 
    a[:a] = 3
    => a = {:a => 3,:b => 2 }
    test
    => {:a => 1, :b => 2 }

Như vậy các bạn chắc đang thắc mắc tại sao hai phương thức này giống nhau đều là deep copy mà sao lại không dùng 1 cái mà lại dùng tận 2 cái vậy.

Và vì vậy ở phần này mình sẽ giúp các bạn phân biệt được sự khác nhau cơ bản giữa hai phương thức này thông qua 3 trường hợp cụ thể như sau:  
***
### 3.1 Single class và Frozen state
* Single class
    
    Sử dụng dup:
    
        a = Object.new
        def a.foo; :foo end
        p a.foo
        # => :foo
        b = a.dup
        p b.foo
        # => undefined method `foo' for #<Object:0x007f8bc395ff00> (NoMethodError)
    Sử dụng clone:

        a = Object.new
        def a.foo; :foo end
        p a.foo
        # => :foo
        b = a.clone
        p b.foo
        # => :foo
    Như ví dụ trên ta có thể thấy clone làm được đó là copy singleton class của object bị copy trong khi sử dụng dup chúng ta sẽ không thể copy được và sẽ xuất hiện lỗi như các bạn thấy ở trên là undefined method.
    ***
* Frozen State

    Sử dung dup:

        a = Object.new
        a.freeze
        p a.frozen?
        # => true
        b = a.dup
        p b.frozen?
        # => false
    
    Sử dụng clone:

        a = Object.new
        a.freeze
        c = a.clone
        p c.frozen?
        # => true
    
    Ta thấy với việc sử dụng dup để copy object thì trạng thái freeze trước đó sẽ không được copy. Còn với clone thì chúng ta sẽ có thể copy được trạng thái frozen của Object

    Như ví dụ trên ta có thể thấy rõ b.frozen? cho kết quả là false (dup) còn với c.frozen? cho kết quả là true (clone)

***
### 3.2 Module

Ta sẽ lấy ví dụ khi một Object thừa kế module liệu việc sử dụng dup và clone sẽ có sự khác biệt thế nào khi copy Object thừa kế module đó

Ta có class và Module sau:

        class Klass
        attr_accessor :str
        end

        module Foo
        def foo; "foo"; end
        end

        s1 = Klass.new #=> #<Klass:0x401b3a38>
        s1.extend(Foo) #=> #<Klass:0x401b3a38>
        s1.foo #=> "foo"


Sử dụng dup:
    
    s3 = s1.dup #=> #<Klass:0x401b3a38>
    s3.foo #=> NoMethodError: undefined method `foo' for #<Klass:0x401b3a38>

Sử dụng clone:

    s2 = s1.clone #=> #<Klass:0x401b3a38>
    s2.foo #=> "foo"

Như vậy dup chỉ sẽ copy được các phương thức con của Object còn với clone ta có thể copy được cả phương thức con của Object và phương thức được kế thừa từ các module .
***
### 3.3 ActiveRecord

Ở phần này chúng ta sẽ sử dụng dup và clone để duplicate các Object, mà ở các Object này có liên kết với các thao tác của Object Active Record. 

Sau đây là ví dụ đơn giản để các bạn thấy được sự khác biệt giữa dup và clone khi duplicate một object có liên kết với Active Record:

Ta có model là User ta sẽ thực hiện truy vấn User với id là 1 qua phương thức find :

    user_1 = User.find(1)
    user_1: {:id => 1, :name =>"Name1"}
Sử dụng dup:

    user_dup = user_1.dup
    user_dup: {:id => nil, :name => "Name1"}
Sử dụng clone:
   
    user_clone = user_1.clone
    user_clone: {:id => 1, :name => "Name1"}

Vậy ta có thể thấy nếu ta sử dụng phương thức save với dup (user_dup.save)thì sẽ tạo ra một đối tượng mới trong db, còn với clone (user_clone) thì sẽ update record với id là 1 trong db .

***
## 4/ Kết luận

Vậy qua bài viết này thì mình đã trình bày tổng quan về thế nào là copy trong lập trình và các phương thức để copy một Object trong ngôn ngữ lập trình ruby

Và theo mình thì tùy vào các bài toán cũng như tình huống cụ thể  mà các bạn sẽ lựa chọn nên dùng dup hay clone một cách hợp lý và mình cũng hi vọng thông qua những kiến thức này các bạn sẽ có thể có cái nhìn tổng quan về copy cũng như sử dụng linh hoạt qua lại giữa hai phương thức dup và clone. 

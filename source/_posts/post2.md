---
layout: posts
title: Biến và Kiểu dữ liệu trong Java
date: 2024-12-30 07:21:06
---
Bạn đã bao giờ tự hỏi làm thế nào mà máy tính có thể hiểu và xử lý những thông tin khác nhau như số, chữ cái hay giá trị đúng/sai? Hay tại sao cùng là con số 5 nhưng đôi khi nó lại được biểu diễn khác nhau? Câu trả lời nằm ở những kiểu dữ liệu mà chúng ta sẽ cùng khám phá trong bài học này.

## 1. Kiểu dữ liệu nguyên thủy (Primitive Data Types)

Kiểu dữ liệu nguyên thủy là những kiểu dữ liệu cơ bản nhất trong Java, được hệ thống định nghĩa sẵn. Chúng đại diện cho các giá trị đơn giản như số, ký tự hoặc giá trị logic.

### 1.1 Kiểu số nguyên
- byte: Dùng để lưu trữ các số nguyên nhỏ, thường dùng để biểu diễn các giá trị nhỏ như tuổi, mã số.
- short: Dùng để lưu trữ các số nguyên có kích thước lớn hơn byte một chút.
- int: Kiểu số nguyên được sử dụng phổ biến nhất, dùng để biểu diễn các số nguyên thông thường.
- long: Dùng để lưu trữ các số nguyên rất lớn.

Ví dụ:
```java
byte age = 25; // Tuổi của một người
short year = 2023; // Năm hiện tại
int population = 1000000; // Dân số của một thành phố
long universeAge = 13800000000L; // Tuổi của vũ trụ (đơn vị năm)
```
### 1.2 Kiểu số thực
- float: Dùng để lưu trữ các số thực với độ chính xác đơn.
- double: Dùng để lưu trữ các số thực với độ chính xác kép.
Ví dụ:
```java
float price = 19.99f; // Giá của một sản phẩm
double pi = 3.14159265359; // Số pi
```
### 1.3 Kiểu ký tự
- char: Dùng để lưu trữ một ký tự duy nhất.
Ví dụ:
```java
char grade = 'A'; // Một chữ cái
```
### 1.4 Kiểu logic
- boolean: Chỉ có hai giá trị: true hoặc false, dùng để biểu diễn các giá trị logic.
Ví dụ:
```java
boolean isStudent = true; // Kiểm tra xem một người có phải là sinh viên hay không
```
### Tóm lại
Các kiểu dữ liệu nguyên thủy cung cấp những công cụ cơ bản để lưu trữ và thao tác với dữ liệu trong Java. Việc chọn kiểu dữ liệu phù hợp sẽ giúp bạn viết code hiệu quả và tránh các lỗi không mong muốn.
### Ví dụ minh họa
Giả sử bạn muốn viết một chương trình tính toán diện tích hình chữ nhật. Bạn sẽ cần các biến để lưu trữ chiều dài, chiều rộng và diện tích.
```java
double length = 10.5; // Chiều dài (m)
double width = 5.2; // Chiều rộng (m)
double area = length * width; // Tính diện tích
System.out.println("Diện tích hình chữ nhật là: " + area + " m²");
```
Trong ví dụ này, chúng ta sử dụng kiểu double để lưu trữ các số thực vì chiều dài và chiều rộng có thể có giá trị thập phân.

## 2 Khai Báo, Sử Dụng Biến và Hằng Số

Chào các bạn, tiếp nối phần 1 về giới thiệu ngôn ngữ Java, hôm nay chúng ta sẽ cùng tìm hiểu về một khái niệm cực kỳ quan trọng trong lập trình: **Biến (Variables)** và **Hằng số (Constants)**. Hiểu rõ về biến và hằng số sẽ giúp bạn viết code Java một cách hiệu quả và dễ dàng hơn.

### 2.1 Khai Báo và Khởi Tạo Biến
Trong Java, biến được sử dụng để lưu trữ dữ liệu. Mỗi biến có một kiểu dữ liệu (data type) xác định loại giá trị mà nó có thể chứa (ví dụ: số nguyên, số thực, chuỗi ký tự).

**Cú pháp:**
```java
<kiểu_dữ_liệu> <tên_biến>; // Khai báo
<tên_biến> = <giá_trị>; // Khởi tạo

// Khai báo và khởi tạo cùng lúc
<kiểu_dữ_liệu> <tên_biến> = <giá_trị>;
```

**Ví dụ:**
```java
int number; // Khai báo biến kiểu số nguyên
number = 10; // Khởi tạo giá trị cho biến number

String name = "John"; // Khai báo và khởi tạo biến kiểu chuỗi

int x = 1, y = 2, z = 3; // Khai báo nhiều biến cùng kiểu trên một dòng
```

### 2.2 Hằng Số (Constants)
Hằng số là các biến có giá trị không thay đổi trong suốt quá trình thực thi chương trình. Trong Java, chúng ta sử dụng từ khóa `final` để khai báo hằng số.
Cú pháp:
```java
final <kiểu_dữ_liệu> <TÊN_HẰNG> = <giá_trị>;
```

**Lưu ý:** Tên hằng số thường được viết bằng chữ in hoa và các từ được phân tách bằng dấu gạch dưới (`_`).

**Ví dụ:**
```java
final double PI = 3.14159;
final int MAX_STUDENTS = 100;
final int DAYS_IN_WEEK = 7;
```

## 3. Phạm Vi của Biến (Variable Scope)
Phạm vi của biến xác định nơi mà biến có thể được truy cập trong code. Có 3 loại phạm vi biến chính:

- **Biến cục bộ (Local Variables):** Được khai báo bên trong một phương thức (method) hoặc một khối lệnh (block). Chỉ có thể được truy cập bên trong phương thức hoặc khối lệnh đó.
- **Biến instance (Instance Variables):** Được khai báo bên trong một lớp (class) nhưng bên ngoài bất kỳ phương thức nào. Mỗi đối tượng (object) của lớp sẽ có một bản sao riêng của biến instance.
- **Biến static (Class Variables):** Được khai báo với từ khóa `static`. Chỉ có một bản sao duy nhất của biến static được chia sẻ bởi tất cả các đối tượng của lớp.

**Ví dụ**:
```java
public class ScopeExample {
    private int instanceVar = 1; // Biến instance
    private static int staticVar = 2; // Biến static

    public void demonstrateScope() {
        int localVar = 3; // Biến local

        if (true) {
            int blockVar = 4; // Biến block
            System.out.println("Block variable: " + blockVar);
        }

        // blockVar không thể truy cập ở đây
        System.out.println("Instance variable: " + instanceVar);
        System.out.println("Static variable: " + staticVar);
        System.out.println("Local variable: " + localVar);
    }
}
```

## 4. Ép Kiểu (Type Casting)
Ép kiểu là quá trình chuyển đổi một biến từ kiểu dữ liệu này sang kiểu dữ liệu khác. Có hai loại ép kiểu:

- **Ép kiểu ngầm định (Widening Casting - tự động):** Chuyển đổi từ kiểu dữ liệu nhỏ hơn sang kiểu dữ liệu lớn hơn (ví dụ: `int` sang `long`, `float` sang `double`). Quá trình này diễn ra tự động.
- **Ép kiểu tường minh (Narrowing Casting - ép buộc):** Chuyển đổi từ kiểu dữ liệu lớn hơn sang kiểu dữ liệu nhỏ hơn (ví dụ: `double` sang `int`). Cần sử dụng toán tử ép kiểu `(kiểu_dữ_liệu)`.

**Ví dụ:**
```java
// Ép kiểu ngầm định
int numberInt = 100;
long numberLong = numberInt;

// Ép kiểu tường minh
double numberDouble = 100.99;
int numberInt2 = (int) numberDouble; // Giá trị sẽ bị mất phần thập phân
```

## 5. Quy Tắc Đặt Tên Biến
Việc đặt tên biến rõ ràng và nhất quán rất quan trọng để code dễ đọc và dễ bảo trì. Một số quy tắc đặt tên biến trong Java:

- Tên biến bắt đầu bằng chữ cái, dấu gạch dưới (`_`) hoặc dấu đô la (`$`).
- Tên biến phân biệt chữ hoa và chữ thường (case-sensitive).
- Sử dụng camelCase cho tên biến (ví dụ: `studentAge`, `firstName`).
- Sử dụng chữ in hoa và dấu gạch dưới cho tên hằng số (ví dụ: `MAX_SIZE`).

## 6. Ví dụ Tổng Hợp
```java
public class VariablesDemo {
    private static final double TAX_RATE = 0.1;
    private String productName;
    private double price;

    public VariablesDemo(String name, double price) {
        this.productName = name;
        this.price = price;
    }

    public double calculateTotalPrice(int quantity) {
        double subtotal = price * quantity;
        double tax = subtotal * TAX_RATE;
        return subtotal + tax;
    }

    public static void main(String[] args) {
        VariablesDemo product = new VariablesDemo("Laptop", 1000.0);
        int orderQuantity = 2;
        double totalPrice = product.calculateTotalPrice(orderQuantity);

        System.out.printf("Product: %s%n", product.productName);
        System.out.printf("Quantity: %d%n", orderQuantity);
        System.out.printf("Total Price (including %.1f%% tax): $%.2f%n", TAX_RATE * 100, totalPrice);
    }
}
```
Hy vọng bài viết này giúp các bạn hiểu rõ hơn về biến và hằng số trong Java. Hẹn gặp lại các bạn ở những bài viết tiếp theo!
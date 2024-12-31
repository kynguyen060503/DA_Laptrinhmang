---
layout: posts
title: Mảng và ArrayList trong Java
date: 2024-12-31 07:22:44
tags:
---
Bài viết này sẽ hướng dẫn chi tiết về mảng (Array) và ArrayList trong Java, hai cấu trúc dữ liệu quan trọng để lưu trữ tập hợp các giá trị. Chúng ta sẽ cùng tìm hiểu cách khai báo, khởi tạo, thao tác với mảng, giới thiệu về ArrayList, so sánh giữa chúng và các phương thức thường dùng của ArrayList.

## 1. Mảng (Array) trong Java

Mảng trong Java là một đối tượng chứa một số lượng cố định các phần tử có cùng kiểu dữ liệu. Các phần tử này được lưu trữ liên tiếp trong bộ nhớ và được truy cập thông qua chỉ số (index), bắt đầu từ 0.

### 1.1. Khai báo và khởi tạo mảng

#### Khai báo:
```java
// Khai báo mảng
kiểu_dữ_liệu[] tên_mảng;
kiểu_dữ_liệu tên_mảng[]; // Cách khai báo khác (ít được dùng)
```
Ví dụ:
```java
int[] numbers; // Khai báo mảng số nguyên
String[] names; // Khai báo mảng chuỗi
```

#### Khởi tạo:
Có ba cách khởi tạo mảng:

1. **Khởi tạo bằng từ khóa `new` và kích thước:**
```java
// Cú pháp
Tên_mảng = new kiểu_dữ_liệu[kích_thước];
```
Ví dụ:
```java
numbers = new int[5]; // Khởi tạo mảng numbers có 5 phần tử kiểu int
names = new String[3]; // Khởi tạo mảng names có 3 phần tử kiểu String
```

2. **Khởi tạo đồng thời với giá trị:**
```java
// Cú pháp
kiểu_dữ_liệu[] tên_mảng = {giá_trị_1, giá_trị_2, ..., giá_trị_n};
```
Ví dụ:
```java
int[] numbers = {1, 2, 3, 4, 5}; // Khởi tạo mảng numbers với 5 giá trị
String[] names = {"Alice", "Bob", "Charlie"}; // Khởi tạo mảng names với 3 giá trị
```

3. **Khởi tạo kết hợp:**
```java
int[] numbers = new int[]{1, 2, 3, 4, 5};
```

### 1.2. Các thao tác với mảng

1. **Truy cập phần tử:** Sử dụng chỉ số để truy cập phần tử.
```java
int firstElement = numbers[0]; // Lấy phần tử đầu tiên (chỉ số 0)
numbers[2] = 10; // Gán giá trị 10 cho phần tử thứ ba (chỉ số 2)
```

2. **Duyệt mảng:** Sử dụng vòng lặp `for` hoặc `for-each`.
```java
// Vòng lặp for
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

// Vòng lặp for-each (enhanced for loop)
for (int number : numbers) {
    System.out.println(number);
}
```

3. **Độ dài mảng:** Sử dụng thuộc tính `length`.
```java
int length = numbers.length; // Lấy độ dài của mảng numbers
```

#### Ví dụ minh họa:
```java
public class ArrayExample {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 8, 1, 9};

        System.out.println("Các phần tử của mảng:");
        for (int number : numbers) {
            System.out.print(number + " ");
        }
        System.out.println();

        System.out.println("Độ dài của mảng: " + numbers.length);

        numbers[1] = 7; // Thay đổi giá trị phần tử thứ hai

        System.out.println("Mảng sau khi thay đổi:");
        for (int number : numbers) {
            System.out.print(number + " ");
        }
        System.out.println();
    }
}
```

## 2. ArrayList trong Java

ArrayList là một lớp trong Java Collections Framework, cho phép lưu trữ một tập hợp các đối tượng một cách động. Khác với mảng, ArrayList có thể tự động thay đổi kích thước khi thêm hoặc xóa phần tử.

### 2.1. Khai báo và khởi tạo ArrayList

```java
import java.util.ArrayList;

ArrayList<Kiểu_dữ_liệu> tên_ArrayList = new ArrayList<>();
```

Ví dụ:
```java
ArrayList<Integer> numbers = new ArrayList<>(); // ArrayList chứa số nguyên
ArrayList<String> names = new ArrayList<>(); // ArrayList chứa chuỗi
```

### 2.2. Các phương thức thường dùng của ArrayList

| **Phương thức**        | **Mô tả**                                                                 |
|-------------------------|---------------------------------------------------------------------------|
| `add(element)`          | Thêm một phần tử vào cuối ArrayList.                                     |
| `add(index, element)`   | Chèn một phần tử vào vị trí `index`.                                      |
| `get(index)`            | Lấy phần tử tại vị trí `index`.                                          |
| `set(index, element)`   | Thay thế phần tử tại vị trí `index` bằng `element`.                      |
| `remove(index)`         | Xóa phần tử tại vị trí `index`.                                          |
| `remove(object)`        | Xóa phần tử đầu tiên bằng `object` được chỉ định.                        |
| `size()`                | Trả về số lượng phần tử trong ArrayList.                                |
| `clear()`               | Xóa tất cả các phần tử trong ArrayList.                                 |
| `contains(element)`     | Kiểm tra xem ArrayList có chứa `element` hay không (trả về `true/false`). |
| `indexOf(element)`      | Trả về chỉ số của lần xuất hiện đầu tiên của `element`, hoặc `-1` nếu không tìm thấy. |
| `isEmpty()`             | Kiểm tra xem ArrayList có rỗng hay không.                               |

#### Ví dụ minh họa:
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>();

        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        System.out.println("Các phần tử trong ArrayList:");
        for (String name : names) {
            System.out.println(name);
        }

        names.remove(1); // Xóa phần tử tại chỉ số 1 (Bob)

        System.out.println("ArrayList sau khi xóa:");
        System.out.println(names);

        System.out.println("Kích thước ArrayList: " + names.size());
    }
}
```

## 3. So sánh Array và ArrayList

| **Đặc điểm**            | **Array**                          | **ArrayList**                       |
|-------------------------|------------------------------------|-------------------------------------|
| Kích thước              | Cố định.                           | Có thể thay đổi động.               |
| Kiểu dữ liệu            | Có thể chứa kiểu nguyên thủy hoặc đối tượng. | Chỉ chứa đối tượng (sử dụng Wrapper classes cho kiểu nguyên thủy). |
| Hiệu năng               | Nhanh hơn cho các thao tác truy cập trực tiếp bằng chỉ số. | Chậm hơn một chút do cơ chế tự động thay đổi kích thước và boxing/unboxing. |
| Tính linh hoạt          | Kém linh hoạt hơn.                 | Linh hoạt hơn.                      |

## Kết luận

Mảng phù hợp khi bạn biết trước số lượng phần tử và cần hiệu năng cao cho việc truy cập trực tiếp. ArrayList phù hợp khi bạn cần một cấu trúc dữ liệu có thể thay đổi kích thước linh hoạt. Hy vọng bài viết này giúp bạn hiểu rõ hơn về mảng và ArrayList trong Java. Mình là Kỷ, hẹn gặp lại bạn trong bài viết tiếp theo của mình nhé!

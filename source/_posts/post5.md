---
layout: posts
title: Phương thức (Method) trong Java
date: 2024-12-31 07:22:48
tags:
---

Phương thức là một khái niệm quan trọng trong Java, giúp tổ chức code thành các khối chức năng riêng biệt, dễ quản lý và tái sử dụng. Trong bài viết này, chúng ta sẽ tìm hiểu:

- Định nghĩa phương thức.
- Tham số và giá trị trả về.
- Nạp chồng phương thức (Method Overloading).
- Phương thức đệ quy (Recursive Method).
- Best practices khi viết phương thức.

## 1. Định nghĩa phương thức

Phương thức trong Java là một khối mã lệnh thực hiện một nhiệm vụ cụ thể. Nó giúp chia chương trình thành các phần nhỏ hơn, dễ quản lý và tái sử dụng.

**Cú pháp định nghĩa phương thức:**

```java
[access_modifier] [static] [return_type] method_name([parameter_list]) {
    // Body của phương thức (các câu lệnh)
    [return value;] // Nếu return_type khác void
}
```

- **`access_modifier`**: Phạm vi truy cập của phương thức (ví dụ: `public`, `private`, `protected`).
- **`static`**: Nếu có từ khóa `static`, phương thức thuộc về lớp, ngược lại thuộc về đối tượng.
- **`return_type`**: Kiểu dữ liệu trả về của phương thức. Nếu phương thức không trả về giá trị nào, sử dụng `void`.
- **`method_name`**: Tên của phương thức.
- **`parameter_list`**: Danh sách các tham số (nếu có), mỗi tham số có dạng `kiểu_dữ_liệu tên_tham_số`.
- **`return value`**: Giá trị trả về của phương thức (chỉ khi `return_type` khác `void`).

**Ví dụ:**

```java
public class MethodExample {

    // Phương thức không trả về giá trị (void)
    public static void printMessage(String message) {
        System.out.println(message);
    }

    // Phương thức trả về tổng của hai số nguyên
    public static int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        printMessage("Xin chào!"); // Gọi phương thức printMessage
        int sum = add(5, 3); // Gọi phương thức add và gán kết quả cho biến sum
        System.out.println("Tổng là: " + sum);
    }
}
```

## 2. Tham số và giá trị trả về

- **Tham số (Parameters)**: Là các giá trị được truyền vào phương thức khi gọi. Chúng cho phép phương thức nhận dữ liệu và thực hiện các thao tác dựa trên dữ liệu đó.
- **Giá trị trả về (Return Value)**: Là kết quả mà phương thức trả về sau khi thực hiện xong nhiệm vụ. Kiểu dữ liệu của giá trị trả về được khai báo ở `return_type`.

**Ví dụ:**

Phương thức `add(int a, int b)` nhận hai tham số kiểu `int` và trả về tổng của chúng cũng là kiểu `int`.

## 3. Method Overloading (Nạp chồng phương thức)

Nạp chồng phương thức cho phép định nghĩa nhiều phương thức có cùng tên nhưng khác nhau về số lượng hoặc kiểu dữ liệu của tham số. Java sẽ tự động chọn phương thức phù hợp dựa trên các tham số được truyền vào khi gọi.

**Ví dụ:**

```java
public class OverloadingExample {

    public static int add(int a, int b) {
        return a + b;
    }

    public static double add(double a, double b) {
        return a + b;
    }

    public static int add(int a, int b, int c) {
        return a + b + c;
    }

    public static void main(String[] args) {
        System.out.println(add(2, 3)); // Gọi phương thức add(int, int)
        System.out.println(add(2.5, 3.7)); // Gọi phương thức add(double, double)
        System.out.println(add(1, 2, 3)); // Gọi phương thức add(int, int, int)
    }
}
```

## 4. Recursive Method (Phương thức đệ quy)

Phương thức đệ quy là phương thức tự gọi chính nó. Nó được sử dụng để giải quyết các bài toán có thể chia nhỏ thành các bài toán con tương tự.

**Ví dụ: Tính giai thừa của một số nguyên dương**

```java
public class RecursiveExample {

    public static int factorial(int n) {
        if (n == 0) {
            return 1;
        } else {
            return n * factorial(n - 1); // Gọi đệ quy
        }
    }

    public static void main(String[] args) {
        System.out.println("5! = " + factorial(5));
    }
}
```

**Lưu ý quan trọng khi sử dụng đệ quy:**

- Cần có điều kiện dừng (base case) để tránh bị tràn bộ nhớ do gọi đệ quy vô hạn (`StackOverflowError`).

## 5. Best practices khi viết phương thức

- **Tên phương thức rõ ràng, dễ hiểu**: Nên sử dụng động từ để đặt tên phương thức (ví dụ: `calculateArea()`, `getName()`, `printData()`).
- **Phương thức nên thực hiện một nhiệm vụ duy nhất**: Tránh viết các phương thức quá dài và phức tạp.
- **Hạn chế số lượng tham số**: Nếu phương thức có quá nhiều tham số, nên xem xét việc sử dụng một đối tượng để nhóm các tham số lại.
- **Kiểm tra tính hợp lệ của tham số**: Đảm bảo rằng phương thức xử lý đúng các trường hợp đầu vào không hợp lệ.
- **Viết documentation cho phương thức (Javadoc)**: Giúp người khác (và cả chính bạn sau này) hiểu rõ chức năng của phương thức.

**Ví dụ Javadoc:**

```java
/**
 * Tính tổng của hai số nguyên.
 * @param a Số nguyên thứ nhất.
 * @param b Số nguyên thứ hai.
 * @return Tổng của a và b.
 */
public static int add(int a, int b) {
    return a + b;
}
```

## Kết luận

Phương thức là một công cụ mạnh mẽ trong Java giúp code dễ đọc, dễ bảo trì và tái sử dụng. Hiểu rõ và áp dụng các best practices sẽ giúp bạn viết code chất lượng hơn. Hy vọng bài viết này hữu ích cho bạn. Nếu có bất kỳ câu hỏi nào, đừng ngần ngại đặt câu hỏi!

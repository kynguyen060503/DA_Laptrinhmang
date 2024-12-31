---
layout: posts
title: Lập trình hướng đối tượng (OOP) trong Java
date: 2024-12-31 07:22:54
tags:
---
## 1. Class và Object

### Class (Lớp)
- Là một bản thiết kế hoặc khuôn mẫu để tạo ra các đối tượng.
- Định nghĩa các thuộc tính (attributes) và hành vi (behaviors) của các đối tượng.
- **Ví dụ:** Class là bản vẽ thiết kế ngôi nhà, Object là ngôi nhà được xây dựa trên bản vẽ.

### Object (Đối tượng)
- Là một thể hiện cụ thể của một lớp.
- Mỗi đối tượng có các giá trị riêng cho các thuộc tính.

### Ví dụ
```java
// Định nghĩa class Dog
class Dog {
    String breed; // Giống chó
    String name;  // Tên chó
    int age;      // Tuổi chó

    // Phương thức sủa
    void bark() {
        System.out.println("Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Tạo object (instance) của class Dog
        Dog myDog = new Dog();
        myDog.breed = "Husky";
        myDog.name = "Alaska";
        myDog.age = 3;

        Dog yourDog = new Dog();
        yourDog.breed = "Poodle";
        yourDog.name = "Lucky";
        yourDog.age = 2;

        System.out.println("My dog is a " + myDog.breed + " named " + myDog.name + ", " + myDog.age + " years old.");
        myDog.bark(); // Gọi phương thức bark()

        System.out.println("Your dog is a " + yourDog.breed + " named " + yourDog.name + ", " + yourDog.age + " years old.");
        yourDog.bark(); // Gọi phương thức bark()
    }
}
```

## 2. Thuộc tính và Phương thức

### Thuộc tính (Attributes)
- Là các đặc điểm, tính chất của đối tượng.
- Biểu diễn bằng các biến instance (instance variables).

### Phương thức (Methods)
- Là các hành động đối tượng có thể thực hiện.
- Là các khối mã lệnh thực hiện một nhiệm vụ cụ thể.

| Khái niệm  | Mô tả                                | Ví dụ trong class Dog |
|-------------|------------------------------------|--------------------------|
| Thuộc tính | Đặc điểm, tính chất của đối tượng | `breed`, `name`, `age`   |
| Phương thức | Hành động đối tượng thực hiện     | `bark()`                 |

## 3. Constructor (Hàm khởi tạo)

### Đặc điểm
- Tên trùng với tên của class.
- Không có kiểu trả về (ngay cả `void`).

### Ví dụ
```java
class Dog {
    String breed;
    String name;
    int age;

    // Constructor
    public Dog(String breed, String name, int age) {
        this.breed = breed;
        this.name = name;
        this.age = age;
    }

    void bark() {
        System.out.println("Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog("Husky", "Alaska", 3); // Sử dụng constructor
        System.out.println(myDog.name); // Alaska
    }
}
```

## 4. `this` keyword (Từ khóa `this`)

### Mục đích
- Tham chiếu đến đối tượng hiện tại.
- Phân biệt biến instance và biến cục bộ có cùng tên.
- Gọi constructor khác trong cùng class (constructor chaining).

### Ví dụ 1: Phân biệt biến
```java
class Dog {
    String name;

    public Dog(String name) {
        this.name = name; // `this.name` là biến instance, `name` là tham số
    }
}
```

### Ví dụ 2: Constructor chaining
```java
class Dog {
    String breed;
    String name;
    int age;

    public Dog(String breed) {
        this(breed, "Unknown", 0); // Gọi constructor khác
    }

    public Dog(String breed, String name, int age) {
        this.breed = breed;
        this.name = name;
        this.age = age;
    }
}
```

## 5. Access Modifiers (Bộ sửa đổi truy cập)

### Loại Access Modifiers

| Modifier    | Mô tả                                                         |
|-------------|------------------------------------------------------------------|
| `public`    | Truy cập được từ bất kỳ đâu.                                  |
| `protected` | Truy cập được từ class hiện tại, subclass, và các class trong package. |
| `default`   | (Không modifier) Chỉ truy cập được từ các class trong package.        |
| `private`   | Chỉ truy cập được từ bên trong class hiện tại.                     |

### Bảng tóm tắt

| Modifier    | Same Class | Same Package | Subclass | World |
|-------------|------------|--------------|----------|-------|
| `public`    | Yes        | Yes          | Yes      | Yes   |
| `protected` | Yes        | Yes          | Yes      | No    |
| `default`   | Yes        | Yes          | No       | No    |
| `private`   | Yes        | No           | No       | No    |

### Ví dụ
```java
class Dog {
    public String breed; // Truy cập từ bất kỳ đâu
    private int age;    // Chỉ truy cập từ bên trong class Dog

    public void setAge(int age) {
        if (age >= 0) {
            this.age = age;
        }
    }

    public int getAge() {
        return this.age;
    }
}
```

## Kết luận
Hiểu rõ các khái niệm Class, Object, Thuộc tính, Phương thức, Constructor, `this` keyword và Access Modifiers là nền tảng vững chắc để tiếp cận lập trình hướng đối tượng trong Java.

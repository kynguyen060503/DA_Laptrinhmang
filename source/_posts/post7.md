---
layout: posts
title: Kế thừa (Inheritance) và Đa hình (Polymorphism) trong Java
date: 2024-12-31 07:22:57
tags:
---

Chào bạn, bài viết này sẽ giới thiệu về Lập trình hướng đối tượng (OOP) trong Java, một paradigm (mô hình lập trình) quan trọng. Chúng ta sẽ tìm hiểu các khái niệm cơ bản như Class và Object, Thuộc tính và Phương thức, Constructor, từ khóa this và Access Modifiers.

## 1. Kế thừa (Inheritance)

Kế thừa cho phép một class (lớp con/subclass) kế thừa các thuộc tính và phương thức từ một class khác (lớp cha/superclass hoặc lớp cơ sở/base class). Nó tạo ra mối quan hệ "is-a" (là một). Ví dụ, "Chó là một động vật" (Dog is an Animal).

### Lợi ích của kế thừa
- **Tái sử dụng code:** Tránh việc viết lại code đã có ở lớp cha.
- **Mở rộng:** Dễ dàng thêm các chức năng mới cho lớp con mà không ảnh hưởng đến lớp cha.
- **Tính đa hình:** Cho phép xử lý các đối tượng thuộc các lớp khác nhau thông qua một kiểu chung (kiểu của lớp cha).

### Ví dụ:
```java
// Lớp cha (Animal)
class Animal {
    String name;

    public Animal(String name) {
        this.name = name;
    }

    void eat() {
        System.out.println(name + " is eating.");
    }
}

// Lớp con (Dog) kế thừa từ Animal
class Dog extends Animal {
    String breed;

    public Dog(String name, String breed) {
        super(name); // Gọi constructor của lớp cha
        this.breed = breed;
    }

    void bark() {
        System.out.println("Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog("Alaska", "Husky");
        myDog.eat(); // Gọi phương thức của lớp cha
        myDog.bark(); // Gọi phương thức của lớp con

        Animal myAnimal = new Animal("Generic Animal");
        myAnimal.eat();
    }
}
```

## 2. Ghi đè phương thức (Method Overriding)

Ghi đè phương thức cho phép lớp con định nghĩa lại một phương thức đã được định nghĩa trong lớp cha với cùng tên, cùng kiểu trả về và cùng danh sách tham số. Nó cho phép lớp con tùy chỉnh hành vi của phương thức được kế thừa.

### Quy tắc ghi đè:
- Tên phương thức phải giống nhau.
- Kiểu trả về phải giống nhau (hoặc là kiểu con của kiểu trả về của lớp cha - covariant return type).
- Danh sách tham số phải giống nhau.
- Access modifier của phương thức ở lớp con phải có phạm vi truy cập rộng hơn hoặc bằng phạm vi truy cập của phương thức ở lớp cha.

### Ví dụ:
```java
class Animal {
    void makeSound() {
        System.out.println("Generic animal sound.");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Woof!"); // Ghi đè phương thức makeSound()
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();
        myAnimal.makeSound(); // In ra: Generic animal sound.

        Dog myDog = new Dog();
        myDog.makeSound(); // In ra: Woof!
    }
}
```

## 3. Từ khóa `super`

Từ khóa `super` được sử dụng để:
- Gọi constructor của lớp cha.
- Truy cập các thành viên (thuộc tính và phương thức) của lớp cha.

### Ví dụ:
```java
public Dog(String name, String breed) {
    super(name); // Gọi constructor của lớp Animal
    this.breed = breed;
}
```

## 4. Đa hình (Polymorphism)

Đa hình (có nghĩa là "nhiều hình dạng") cho phép một đối tượng có thể biểu hiện dưới nhiều dạng khác nhau. Trong Java, đa hình được thể hiện thông qua:

### 4.1. Ghi đè phương thức (Runtime Polymorphism/Dynamic Polymorphism)
- Quyết định phương thức nào sẽ được gọi được thực hiện tại thời điểm chạy chương trình.

### 4.2. Nạp chồng phương thức (Method Overloading) (Compile-time Polymorphism/Static Polymorphism)
- Quyết định phương thức nào sẽ được gọi được thực hiện tại thời điểm biên dịch.

### Ví dụ về đa hình với ghi đè phương thức:
```java
Animal animal1 = new Animal("Generic Animal");
Animal animal2 = new Dog("Alaska", "Husky"); // Đa hình: biến kiểu Animal tham chiếu đến đối tượng Dog

animal1.makeSound(); // In ra: Generic animal sound.
animal2.makeSound(); // In ra: Woof! (phương thức của Dog được gọi)
```

## 5. Abstract class và Interface

### Abstract class (Lớp trừu tượng)
- Là một lớp không thể được khởi tạo trực tiếp.
- Được sử dụng để định nghĩa một khuôn mẫu chung cho các lớp con.
- Có thể chứa các phương thức trừu tượng (không có phần thân) và phương thức thông thường.

#### Ví dụ:
```java
abstract class Shape {
    abstract double getArea(); // Phương thức trừu tượng
}

class Circle extends Shape {
    double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    double getArea() {
        return Math.PI * radius * radius;
    }
}
```

### Interface (Giao diện)
- Là một tập hợp các phương thức trừu tượng (và các hằng số).
- Một lớp có thể implement nhiều interface.

#### Ví dụ:
```java
interface Drawable {
    void draw();
}

class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle.");
    }
}
```

### So sánh Abstract class và Interface:

| Đặc điểm          | Abstract class                           | Interface                                |
|-------------------|------------------------------------------|-----------------------------------------|
| **Khởi tạo**     | Không thể khởi tạo trực tiếp             | Không thể khởi tạo                      |
| **Phương thức**  | Có thể chứa phương thức trừu tượng và thông thường | Chỉ chứa phương thức trừu tượng (trước Java 8), default method, static method |
| **Biến**         | Có thể chứa biến instance                | Chỉ chứa hằng số (static final)         |
| **Kế thừa**      | Một lớp chỉ có thể kế thừa một abstract class | Một lớp có thể implement nhiều interface |
| **Mục đích**     | Định nghĩa một khuôn mẫu chung           | Định nghĩa một hợp đồng                 |

## Kết luận
Kế thừa và Đa hình là hai khái niệm cốt lõi của OOP, giúp code trở nên linh hoạt, dễ bảo trì và tái sử dụng hơn. Hiểu rõ về Ghi đè phương thức, từ khóa `super`, Abstract class và Interface sẽ giúp bạn áp dụng OOP hiệu quả hơn trong lập trình Java.

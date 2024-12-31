---
layout: posts
title: Cấu trúc điều khiển trong Java
date: 2024-12-30 07:22:38
tags:
---
Cấu trúc điều khiển là một phần kiến thức rất quan trọng, giúp điều khiển luồng thực thi của chương trình một cách linh hoạt.

### 1. Câu lệnh if-else

Câu lệnh `if-else` cho phép thực hiện một khối lệnh nếu điều kiện là đúng (`true`) và một khối lệnh khác nếu điều kiện là sai (`false`).

#### Cú pháp:
```java
if (điều_kiện) {
    // Khối lệnh được thực hiện nếu điều kiện đúng
} else {
    // Khối lệnh được thực hiện nếu điều kiện sai
}
```

#### Ví dụ:
```java
int age = 20;

if (age >= 18) {
    System.out.println("Bạn đã đủ tuổi bầu cử.");
} else {
    System.out.println("Bạn chưa đủ tuổi bầu cử.");
}
```

#### Hình ảnh minh họa:
![Hình minh họa if-else](#)

### 2. Câu lệnh switch-case

Câu lệnh `switch-case` cho phép lựa chọn một trong nhiều khối lệnh dựa trên giá trị của một biến.

#### Cú pháp:
```java
switch (biểu_thức) {
    case giá_trị_1:
        // Khối lệnh 1
        break;
    case giá_trị_2:
        // Khối lệnh 2
        break;
    ...
    default:
        // Khối lệnh mặc định (nếu không có case nào khớp)
}
```

#### Ví dụ:
```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Thứ hai");
        break;
    case 2:
        System.out.println("Thứ ba");
        break;
    case 3:
        System.out.println("Thứ tư");
        break;
    default:
        System.out.println("Ngày không hợp lệ");
}
```

#### Hình ảnh minh họa:
![Hình minh họa switch-case](#)

### 3. Vòng lặp for

Vòng lặp `for` cho phép lặp lại một khối lệnh một số lần xác định.

#### Cú pháp:
```java
for (khởi_tạo; điều_kiện; cập_nhật) {
    // Khối lệnh được lặp lại
}
```

#### Ví dụ:
```java
for (int i = 0; i < 5; i++) {
    System.out.println("Giá trị của i: " + i);
}
```

#### Hình ảnh minh họa:
![Hình minh họa vòng lặp for](#)

### 4. Vòng lặp while và do-while

#### Vòng lặp while
Lặp lại một khối lệnh khi điều kiện là đúng.

##### Cú pháp:
```java
while (điều_kiện) {
    // Khối lệnh được lặp lại
}
```

##### Ví dụ:
```java
int i = 0;
while (i < 5) {
    System.out.println("Giá trị của i: " + i);
    i++;
}
```

#### Vòng lặp do-while
Tương tự như `while`, nhưng khối lệnh được thực hiện ít nhất một lần trước khi kiểm tra điều kiện.

##### Cú pháp:
```java
do {
    // Khối lệnh được lặp lại
} while (điều_kiện);
```

##### Ví dụ:
```java
int i = 0;
do {
    System.out.println("Giá trị của i: " + i);
    i++;
} while (i < 5);
```

#### Hình ảnh minh họa:
![Hình minh họa vòng lặp while và do-while](#)

### 5. break và continue

#### break
Thoát khỏi vòng lặp ngay lập tức.

#### continue
Bỏ qua lần lặp hiện tại và chuyển sang lần lặp tiếp theo.

#### Ví dụ:
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break; // Thoát khỏi vòng lặp khi i = 5
    }
    if (i == 3) {
        continue; // Bỏ qua khi i = 3
    }
    System.out.println("Giá trị của i: " + i);
}
```

Hy vọng bài viết này giúp bạn hiểu rõ hơn về cấu trúc điều khiển trong Java. Nếu bạn có bất kỳ câu hỏi nào, đừng ngần ngại đặt câu hỏi. Chúc bạn học tập tốt!

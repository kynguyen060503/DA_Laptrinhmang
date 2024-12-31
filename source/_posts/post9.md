---
layout: posts
title: Xử lý chuỗi trong Java
date: 2024-12-31 07:23:07
tags:
---
Bài viết này sẽ hướng dẫn chi tiết về xử lý chuỗi trong Java, bao gồm các phương thức của lớp `String`, `StringBuilder` và `StringBuffer`, Regular Expression (Biểu thức chính quy), Pattern và Matcher, cùng với các ví dụ thực tế.

## 1. String methods (Các phương thức của String)
Lớp `String` cung cấp rất nhiều phương thức để thao tác với chuỗi. Dưới đây là một số phương thức quan trọng:

| Phương thức | Mô tả | Ví dụ |
|-------------|-------|-------|
| `length()`  | Trả về độ dài của chuỗi. | `"Hello".length()` trả về `5`. |
| `charAt(int index)` | Trả về ký tự tại vị trí index. | `"Hello".charAt(0)` trả về `'H'`. |
| `concat(String str)` | Nối chuỗi `str` vào cuối chuỗi hiện tại. | `"Hello".concat(" World")` trả về `"Hello World"`. |
| `toUpperCase()` | Chuyển đổi chuỗi thành chữ in hoa. | `"hello".toUpperCase()` trả về `"HELLO"`. |
| `toLowerCase()` | Chuyển đổi chuỗi thành chữ in thường. | `"HELLO".toLowerCase()` trả về `"hello"`. |
| `trim()` | Loại bỏ khoảng trắng ở đầu và cuối chuỗi. | `" Hello ".trim()` trả về `"Hello"`. |
| `substring(int beginIndex)` | Trả về chuỗi con bắt đầu từ vị trí `beginIndex`. | `"Hello".substring(1)` trả về `"ello"`. |
| `substring(int beginIndex, int endIndex)` | Trả về chuỗi con từ `beginIndex` đến `endIndex` (không bao gồm `endIndex`). | `"Hello".substring(1, 4)` trả về `"ell"`. |
| `replace(char oldChar, char newChar)` | Thay thế tất cả các ký tự `oldChar` bằng `newChar`. | `"Hello".replace('l', 'p')` trả về `"Heppo"`. |
| `replace(String oldString, String newString)` | Thay thế tất cả các chuỗi `oldString` bằng `newString`. | `"Hello World".replace("World", "Java")` trả về `"Hello Java"`. |
| `startsWith(String prefix)` | Kiểm tra xem chuỗi có bắt đầu bằng `prefix` hay không. | `"Hello".startsWith("He")` trả về `true`. |
| `endsWith(String suffix)` | Kiểm tra xem chuỗi có kết thúc bằng `suffix` hay không. | `"Hello".endsWith("lo")` trả về `true`. |
| `contains(CharSequence s)` | Kiểm tra xem chuỗi có chứa chuỗi `s` hay không. | `"Hello".contains("el")` trả về `true`. |
| `indexOf(String str)` | Trả về vị trí đầu tiên của chuỗi `str` trong chuỗi hiện tại, hoặc `-1` nếu không tìm thấy. | `"Hello".indexOf("el")` trả về `1`. |
| `split(String regex)` | Chia chuỗi thành một mảng các chuỗi con dựa trên biểu thức chính quy `regex`. | `"Hello,World".split(",")` trả về `{ "Hello", "World" }`. |
| `equals(Object anObject)` | So sánh chuỗi với một đối tượng khác. Trả về `true` nếu hai chuỗi giống nhau. | `"Hello".equals("Hello")` trả về `true`. |
| `equalsIgnoreCase(String anotherString)` | So sánh chuỗi với một chuỗi khác, bỏ qua phân biệt chữ hoa chữ thường. | `"Hello".equalsIgnoreCase("hello")` trả về `true`. |
| `valueOf(Object obj)` | Chuyển đổi một đối tượng thành chuỗi. | `String.valueOf(123)` trả về `"123"`. |

**Ví dụ:**
```java
String str = "  Hello World!  ";
System.out.println(str.trim().toUpperCase()); // In ra: HELLO WORLD!
String[] words = str.split(" ");
for (String word : words) {
    if (!word.isEmpty()){
        System.out.println(word);
    }
}
```

## 2. StringBuilder và StringBuffer
Cả `StringBuilder` và `StringBuffer` đều được sử dụng để tạo và thao tác với các chuỗi có thể thay đổi (mutable strings). 
- **`String`** là bất biến (immutable), nghĩa là mỗi khi bạn thay đổi một chuỗi `String`, một đối tượng mới sẽ được tạo ra. Điều này có thể gây tốn hiệu năng nếu bạn thực hiện nhiều thao tác thay đổi chuỗi.

### So sánh:
| Đặc điểm | String | StringBuilder | StringBuffer |
|----------|--------|---------------|--------------|
| Tính thay đổi | Bất biến (Immutable) | Có thể thay đổi (Mutable) | Có thể thay đổi (Mutable) |
| Hiệu năng | Chậm (khi thay đổi nhiều) | Nhanh | Chậm hơn StringBuilder |
| An toàn luồng | An toàn | Không an toàn | An toàn |

### Các phương thức chính:
- `append(String str)`: Nối chuỗi `str` vào cuối.
- `insert(int offset, String str)`: Chèn chuỗi `str` vào vị trí `offset`.
- `delete(int start, int end)`: Xóa chuỗi từ `start` đến `end` (không bao gồm `end`).
- `reverse()`: Đảo ngược chuỗi.
- `toString()`: Chuyển đổi thành `String`.

**Ví dụ:**
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
sb.insert(5, ",");
System.out.println(sb.toString()); // In ra: Hello, World

StringBuffer sbf = new StringBuffer("Java");
sbf.reverse();
System.out.println(sbf.toString()); // In ra: avaJ
```

## 3. Regular Expression cơ bản (Biểu thức chính quy)
Regular Expression (Regex hoặc RegExp) là một chuỗi các ký tự đặc biệt được sử dụng để mô tả một mẫu tìm kiếm. 

### Một số ký tự đặc biệt trong Regex:
- `.`: Bất kỳ ký tự nào (ngoại trừ dòng mới).
- `^`: Bắt đầu chuỗi.
- `$`: Kết thúc chuỗi.
- `[]`: Một tập hợp các ký tự (ví dụ: `[abc]` khớp với 'a', 'b' hoặc 'c').
- `[^]`: Phủ định của tập hợp (ví dụ: `[^abc]` khớp với bất kỳ ký tự nào không phải 'a', 'b' hoặc 'c').
- `*`: Lặp lại 0 hoặc nhiều lần.
- `+`: Lặp lại 1 hoặc nhiều lần.
- `?`: Lặp lại 0 hoặc 1 lần.
- `{n}`: Lặp lại chính xác `n` lần.
- `{n,m}`: Lặp lại từ `n` đến `m` lần.
- `\d`: Một chữ số (tương đương `[0-9]`).
- `\D`: Không phải là chữ số (tương đương `[^0-9]`).
- `\w`: Một ký tự chữ (tương đương `[a-zA-Z0-9_]`).
- `\W`: Không phải là ký tự chữ (tương đương `[^a-zA-Z0-9_]`).
- `\s`: Một khoảng trắng (space, tab, newline).
- `\S`: Không phải là khoảng trắng.

**Ví dụ:**
- `a.b`: Khớp với "aab", "acb", "a1b",...
- `^Hello`: Khớp với chuỗi bắt đầu bằng "Hello".
- `World$`: Khớp với chuỗi kết thúc bằng "World".
- `[0-9]+`: Khớp với một hoặc nhiều chữ số.
- `\d{3}-\d{3}-\d{4}`: Khớp với định dạng số điện thoại (ví dụ: 123-456-7890).

## 4. Pattern và Matcher
Trong Java, lớp `Pattern` đại diện cho một biểu thức chính quy đã được biên dịch, và lớp `Matcher` được sử dụng để thực hiện các thao tác so khớp trên một chuỗi.

### Các bước sử dụng:
1. **Tạo Pattern:**
```java
Pattern pattern = Pattern.compile("regex"); // regex là biểu thức chính quy
```

2. **Tạo Matcher:**
```java
Matcher matcher = pattern.matcher("inputString"); // inputString là chuỗi cần so khớp
```

3. **Thực hiện so khớp:** Sử dụng các phương thức của `Matcher` để thực hiện các thao tác.

### Một số phương thức quan trọng của Matcher:
| Phương thức | Mô tả |
|-------------|-------|
| `matches()` | Kiểm tra xem toàn bộ chuỗi đầu vào có khớp với biểu thức chính quy hay không. |
| `find()` | Tìm kiếm chuỗi con tiếp theo trong chuỗi đầu vào khớp với biểu thức chính quy. |
| `group()` | Trả về chuỗi con được tìm thấy bởi lần so khớp gần nhất. |
| `start()` | Trả về vị trí bắt đầu của chuỗi con được tìm thấy. |
| `end()` | Trả về vị trí kết thúc của chuỗi con được tìm thấy. |
| `replaceAll(String replacement)` | Thay thế tất cả các chuỗi con khớp với biểu thức chính quy bằng chuỗi `replacement`. |
| `replaceFirst(String replacement)` | Thay thế chuỗi con đầu tiên khớp với biểu thức chính quy bằng chuỗi `replacement`. |

**Ví dụ:**
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexExample {
    public static void main(String[] args) {
        String text = "The quick brown fox jumps over the lazy dog.";
        String regex = "\\b\\w{5}\\b"; // Tìm các từ có 5 ký tự

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(text);

        System.out.println("Các từ có 5 ký tự:");
        while (matcher.find()) {
            System.out.println("Found value: " + matcher.group() + " start: " + matcher.start() + " end: " + matcher.end());
        }

        String phoneRegex = "\\d{3}-\\d{3}-\\d{4}";
        String phoneNumbers = "123-456-7890, 9876543210, 555-123-4567";
        Pattern phonePattern = Pattern.compile(phoneRegex);
        Matcher phoneMatcher = phonePattern.matcher(phoneNumbers);

        System.out.println("\nSố điện thoại:");
        while (phoneMatcher.find()) {
            System.out.println(phoneMatcher.group());
        }

        String replacedText = phoneMatcher.replaceAll("XXX-XXX-XXXX");
        System.out.println("\nChuỗi sau khi thay thế: " + replacedText);
    }
}
```

## 5. Các ví dụ thực tế về xử lý chuỗi

### Kiểm tra định dạng email:
```java
String emailRegex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";
Pattern emailPattern = Pattern.compile(emailRegex);
Matcher emailMatcher = emailPattern.matcher("test@example.com");
if (emailMatcher.matches()) {
    System.out.println("Email hợp lệ.");
}
```

### Kiểm tra tính hợp lệ của mật khẩu:
Điều kiện: Ít nhất 8 ký tự, chứa chữ hoa, chữ thường, số và ký tự đặc biệt.
```java
String passwordRegex = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=])(?=\\S+$).{8,}$";
Pattern passwordPattern = Pattern.compile(passwordRegex);
Matcher passwordMatcher = passwordPattern.matcher("P@$$wOrd123");
if (passwordMatcher.matches()) {
    System.out.println("Mật khẩu mạnh.");
}
```

### Thay thế các ký tự đặc biệt trong chuỗi:
```java
String textWithSpecialChars = "This is a string with !@#$%^&*()_+ special characters.";
String cleanText = textWithSpecialChars.replaceAll("[^a-zA-Z0-9\\s]", ""); // Giữ lại chữ, số và khoảng trắng
System.out.println(cleanText);
```

---

## Kết luận
Xử lý chuỗi là một phần quan trọng trong lập trình Java. Việc nắm vững các phương thức của lớp `String`, cách sử dụng `StringBuilder` và `StringBuffer` để tối ưu hiệu năng, và đặc biệt là sức mạnh của Regular Expression thông qua `Pattern` và `Matcher` sẽ giúp bạn xử lý các bài toán liên quan đến chuỗi một cách hiệu quả. Hy vọng bài viết này đã cung cấp cho bạn đầy đủ kiến thức cần thiết.

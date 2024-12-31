---
layout: posts
title: File I/O Cơ Bản
date: 2024-12-31 07:23:12
tags:
---
Chúng ta sẽ tìm hiểu cách đọc và ghi file văn bản, thực hiện các thao tác với file và thư mục, sử dụng try-with-resources và xử lý ngoại lệ trong quá trình làm việc với File I/O.

## 1. Đọc file văn bản

Để đọc file văn bản trong Java, chúng ta thường sử dụng các lớp **FileReader** và **BufferedReader**:

- **FileReader**: Đọc dữ liệu theo từng ký tự.
- **BufferedReader**: Đọc dữ liệu theo từng dòng, hiệu quả hơn khi đọc file lớn.

### Ví dụ:

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadFileExample {
    public static void main(String[] args) {
        String filePath = "input.txt"; // Đường dẫn đến file

        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Lỗi đọc file: " + e.getMessage());
        }
    }
}
```

### Giải thích:

- `try (BufferedReader br = ...)`: Sử dụng **try-with-resources** để tự động đóng `BufferedReader` sau khi sử dụng, tránh rò rỉ tài nguyên.
- `new FileReader(filePath)`: Tạo một `FileReader` để đọc dữ liệu từ file.
- `new BufferedReader(...)`: Tạo một `BufferedReader` để đọc dữ liệu theo từng dòng.
- `br.readLine()`: Đọc một dòng từ file. Trả về `null` nếu đã đến cuối file.
- `catch (IOException e)`: Xử lý ngoại lệ `IOException` có thể xảy ra trong quá trình đọc file.

## 2. Ghi file văn bản

Để ghi file văn bản, chúng ta thường sử dụng các lớp **FileWriter**, **BufferedWriter** hoặc **PrintWriter**:

- **FileWriter**: Ghi dữ liệu theo từng ký tự.
- **BufferedWriter**: Ghi dữ liệu theo từng khối, hiệu quả hơn khi ghi nhiều dữ liệu.
- **PrintWriter**: Cung cấp các phương thức tiện lợi để ghi dữ liệu theo nhiều định dạng (ví dụ: `print()`, `println()`, `printf()`).

### Ví dụ:

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;

public class WriteFileExample {
    public static void main(String[] args) {
        String filePath = "output.txt";

        try (BufferedWriter bw = new BufferedWriter(new FileWriter(filePath));
             PrintWriter pw = new PrintWriter(new FileWriter("output_print_writer.txt"))) {
            bw.write("Đây là dòng đầu tiên.\n");
            bw.write("Đây là dòng thứ hai.");
            pw.println("Dòng đầu tiên dùng PrintWriter");
            pw.printf("Đây là số: %d và chuỗi %s", 123, "ví dụ");
        } catch (IOException e) {
            System.err.println("Lỗi ghi file: " + e.getMessage());
        }
    }
}
```

### Giải thích:

- `try (BufferedWriter bw = ...)`: Sử dụng **try-with-resources** để tự động đóng `BufferedWriter` sau khi sử dụng.
- `new FileWriter(filePath)`: Tạo một `FileWriter` để ghi dữ liệu vào file. Nếu file không tồn tại, nó sẽ được tạo. Nếu file đã tồn tại, nội dung cũ sẽ bị ghi đè (overwrite). Để ghi tiếp vào file (append), sử dụng `new FileWriter(filePath, true)`.
- `bw.write(...)`: Ghi dữ liệu vào file.
- `pw.println(...)`: Ghi một dòng vào file, tự động thêm dấu xuống dòng.
- `pw.printf(...)`: Ghi dữ liệu theo định dạng.

## 3. Thao tác với File và thư mục

Lớp **File** cung cấp các phương thức để thao tác với file và thư mục:

| Phương thức       | Mô tả                                                                 |
|-------------------|----------------------------------------------------------------------|
| `exists()`        | Kiểm tra xem file hoặc thư mục có tồn tại hay không.                |
| `createNewFile()` | Tạo một file mới.                                                   |
| `mkdir()`         | Tạo một thư mục mới.                                               |
| `mkdirs()`        | Tạo một thư mục mới, bao gồm cả các thư mục cha nếu cần.           |
| `delete()`        | Xóa file hoặc thư mục.                                             |
| `isFile()`        | Kiểm tra xem đối tượng là file hay không.                          |
| `isDirectory()`   | Kiểm tra xem đối tượng là thư mục hay không.                       |
| `getName()`       | Lấy tên của file hoặc thư mục.                                     |
| `getAbsolutePath()`| Lấy đường dẫn tuyệt đối của file hoặc thư mục.                     |
| `listFiles()`     | Trả về một mảng các `File` đại diện cho các file và thư mục con.   |

### Ví dụ:

```java
import java.io.File;
import java.io.IOException;

public class FileOperationsExample {
    public static void main(String[] args) throws IOException {
        File file = new File("myfile.txt");
        if (file.createNewFile()) {
            System.out.println("File created: " + file.getAbsolutePath());
        } else {
            System.out.println("File already exists.");
        }

        File dir = new File("mydir");
        if (dir.mkdir()) {
            System.out.println("Directory created: " + dir.getAbsolutePath());
        }

        File nestedDir = new File("parent/child");
        if (nestedDir.mkdirs()) {
            System.out.println("Nested directories created: " + nestedDir.getAbsolutePath());
        }

        File[] files = new File(".").listFiles(); // Lấy danh sách các file trong thư mục hiện tại
        if (files != null) {
            for (File f : files) {
                System.out.println(f.getName());
            }
        }

        file.delete();
        dir.delete();
        nestedDir.delete(); // Chú ý: cần xóa các thư mục con trước
        new File("parent").delete();
    }
}
```

## 4. try-with-resources

**try-with-resources** là một tính năng mới trong Java 7 giúp tự động đóng các tài nguyên (resources) như file, kết nối database sau khi sử dụng. Nó giúp tránh rò rỉ tài nguyên và làm cho code gọn gàng hơn.

### Cú pháp:

```java
try (ResourceType resource = new ResourceType()) {
    // Sử dụng resource
} catch (ExceptionType e) {
    // Xử lý ngoại lệ
}
```

- `ResourceType` phải implement interface `AutoCloseable`.

### Ví dụ (đã được sử dụng ở các ví dụ trên):

```java
try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
    // ...
}
```

## 5. Xử lý ngoại lệ với File I/O

Các thao tác với file I/O có thể gây ra nhiều loại ngoại lệ, trong đó phổ biến nhất là `IOException`. Bạn nên xử lý các ngoại lệ này bằng `try-catch` block để chương trình hoạt động ổn định.

### Ví dụ:

```java
try {
    // ...
} catch (IOException e) {
    System.err.println("Lỗi: " + e.getMessage());
    e.printStackTrace(); // In ra stack trace để debug (chỉ dùng trong quá trình phát triển)
}
```

## Một số lưu ý quan trọng

### Đường dẫn tuyệt đối và đường dẫn tương đối

- **Đường dẫn tuyệt đối (absolute path)**: Chỉ định đầy đủ vị trí của file/thư mục từ thư mục gốc (ví dụ: `C:\path\to\file.txt` trên Windows, `/path/to/file.txt` trên Linux/macOS).
- **Đường dẫn tương đối (relative path)**: Chỉ định vị trí của file/thư mục so với thư mục hiện tại của chương trình (ví dụ: `file.txt`, `folder/file.txt`).

### Dấu phân cách đường dẫn

- **Windows** sử dụng dấu `\` (backslash). Trong Java, bạn cần escape dấu `\` bằng cách sử dụng `\\` (ví dụ: `"C:\\path\\to\\file.txt"`).
- **Linux/macOS** sử dụng dấu `/` (forward slash).
- Sử dụng `File.separator` để chương trình hoạt động đúng trên mọi hệ điều hành:

```java
String filePath = "mydir" + File.separator + "myfile.txt";
```

### Encoding (mã hóa ký tự)

Khi đọc/ghi file văn bản, bạn cần chú ý đến encoding của file. Encoding phổ biến là `UTF-8`. Để chỉ định encoding, bạn có thể sử dụng `InputStreamReader` và `OutputStreamWriter`:

```java
try (BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream(filePath), "UTF-8"))) {
    // ...
}

try (BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(filePath), "UTF-8"))) {
    // ...
}
```

### Đóng tài nguyên

Đảm bảo đóng tất cả các stream (ví dụ: `BufferedReader`, `BufferedWriter`, `FileInputStream`, `FileOutputStream`) sau khi sử dụng để tránh rò rỉ tài nguyên. **try-with-resources** giúp bạn thực hiện việc này một cách tự động và an toàn.

### Kiểm tra sự tồn tại của file/thư mục trước khi thao tác

Sử dụng `file.exists()` để kiểm tra xem file/thư mục có tồn tại hay không trước khi thực hiện các thao tác như đọc, ghi, xóa.

### Đường dẫn đến thư mục hiện tại

Có thể lấy đường dẫn đến thư mục hiện tại của ứng dụng bằng:

```java
String currentDir = System.getProperty("user.dir");
System.out.println("Thư mục hiện tại: " + currentDir);
```

## Ví dụ tổng hợp

```java
import java.io.*;

public class FileIOExample {
    public static void main(String[] args) {
        String inputFile = "input.txt";
        String outputFile = "output.txt";

        try {
            // Đọc file với UTF-8
            try (BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream(inputFile), "UTF-8"))) {
                String line;
                System.out.println("Nội dung file input.txt:");
                while ((line = br.readLine()) != null) {
                    System.out.println(line);
                }
            }
            // Ghi file với UTF-8
            try (BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(outputFile), "UTF-8"))) {
                bw.write("Đây là nội dung được ghi vào file output.txt với UTF-8.\n");
                bw.write("Ví dụ khác.");
            }
            System.out.println("Đã ghi thành công vào file output.txt");
        } catch (IOException e) {
            System.err.println("Lỗi I/O: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Hy vọng với phần bổ sung này, bạn đã có cái nhìn đầy đủ và chi tiết về thao tác File I/O trong Java. Nếu bạn có bất kỳ câu hỏi nào khác, đừng ngần ngại hỏi!

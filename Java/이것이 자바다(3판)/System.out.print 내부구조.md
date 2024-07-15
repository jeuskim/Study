```java
// System.java
package java.lang;
public final class System {
    public static final InputStream in = null;
    public static final PrintStream out = null;
    public static final PrintStream err = null;
    // out = new PrintStream(new BufferedOutputStream(new FileOutputStream(FileDescriptor.out)));
}
```



- 명령형 프로그래밍(튜링 기계 모델 기반)

  1. 상태 변화: 프로그램의 상태 변경
  2. 명령의 순서: 명령의 순차적 실행 중시
  3. 부수 효과: 함수가 외부 상태를 변경 가능

- 함수형 프로그래밍(람다 대수 기반)

  1. 순수성: 순수 함수와 부수 효과의 제거를 강조

  2. 고차 함수: 함수를 인자로 받거나 반환할 수 있는 고차 함수를 사용

  3. 불변성: 데이터가 불변

     > 익명 함수, 함수를 값 취



- 람다 대수(lambda calculus)

  > 정의: 계산을 함수와 함수의 연산으로 추상화한 체계이다.
  >
  > 특징: 튜링 완전성을 만족시키며 튜링 기계와 동치이다.

  - 튜링 완전성(Turing completeness)

    > 정의: 어떤 프로그래밍 언어나 추상 기계가 튜링 기계와 동일한 계산 능력을 가진다는 의미이다.

  - 튜링 기계(Turing machine) - 컴퓨터

    > 정의: 계산하는 기계의 일반적인 개념을 설명하기 위한 수학적 모형의 일종이다.

    - 테이프(Tape) - 메모리(RAM, 디스크)

      > 테이프: 일정한 크기의 셀(Cell)로 나뉘어 있는 종이 테이프로 길이는 무한하다.
      >
      > RAM(Random Access Memory): 데이터를 일시적으로 저장하는 휘발성 메모리로 실행 중인 프로그램과 데이터를 저장하는 데 사용된다.

      - 셀(Cell)

        > 기호가 기록되어 있다.(비어 있을 때는 비어있다는 기호)

    - 헤드(Head) - CPU

      > 헤드: 종이 테이프의 특정 한 셀을 읽을 수 있는 헤드(헤드나 테이프가 이동)
      >
      > CPU(Central Processing Unit): 명령어를 해석하고 실행하며 컴퓨터 시스템의 작동 제어

    - 상태 기록기(State register) - 프로그램 카운터, 레지스터

      > 상태 기록기: 현재 튜링 기계의 상태를 기록하고 있는 장치
      >
      > 프로그램 카운터: 현재 실행 중인 명령어의 주소를 가리키는 CPU 내의 레지스터
      >
      > 레지스터: CPU 내부의 고속 메모리 위치

      - 개시 상태(Start state)

        > 상태 기록기가 초기화된 상태를 의미

      - 종료 상태(Halt state)

        > 수행이 종료된 상태

    - 행동표(Action table) - 소프트웨어 프로그램(운영 체제, 응용 프로그램)

      > 행동표: 특정 상태에서 특정 기호를 읽었을 때 해야 할 행동을 지시한다.
      >
      > 운영 체제(Operating System): 컴퓨터 하드웨어와 소프트웨어 리소스를 관리하고, 사용자와 컴퓨터 간의 인터페이스를 제공하는 시스템 소프트웨어이다.

      - 기호를 지우거나 고쳐쓴다.
      - 헤드를 오른쪽, 왼쪽으로 한 칸 움직이거나 그 자리에 머문다.
      - 같은 상태나 새로운 상태로 간다.



```java
// OutputStream.java
// 데이터를 바이트 스트림으로 출력하는 기능을 제공한다.
// 스트림: 데이터를 연속적으로 처리하거나 전송하기 위한 추상화된 개념
package java.io;
public abstract class OutputStream implements Closeable, Flushable {
    public OutputStream() {}
}
```



```java
// FilterOutputStream.java
// 기본 출력 스트림에 대해 추가적인 기능을 제공하는 필터 역할을 한다.
// 기본 출력 스트림: 프로그램이 데이터를 출력하는 데 사용하는 특정한 스트림
package java.io;
public class FilterOutputStream extends OutputStream {
    protected OutputStream out;
    private volatile boolean closed;
    private final Object closeLock = new Object();
    
    public FilterOutputStream(OutputStream out) {
        this.out = out;
    }
}
```



```java
// PrintStream.java
// 텍스트 데이터를 표준 출력 장치에 출력하는 기능을 제공한다.
// 표준 출력 장치: 기본적으로 데이터를 출력하는 데 사용되는 장치
package java.io;
public class PrintStream extends FilterOutputStream
    implements Appendable, Closeable {
    private fianal boolean autoFlush;
    private boolean trouble = false;
    private Formatter formatter;
    private BufferedWriter textOut;
    private OutputStreamWriter charOut;
    
        private PrintStream(boolean autoFlush, OutputStream out) {
            super(out);
            this.autoFlush = autoFlush;
            this.charOut = new OutputStreamWriter(this);
            this.textOut = new BufferedWriter(charOut);
        }
        private PrintStream(boolean autoFlush, Charset charset, OutputStream out) {
            this(out, autoFlush, charset);
        }
        public PrintStream(OutputStream out) {
            this(out, flase);
        }
        public PrintStream(OutputStream out, boolean autoFlush) {
            this(autoFlush, requireNonNull(out, "Null output stream"));
        }
    
        public PrintStream(OutputStream out, boolean autoFlush, String encoding)
            throws UnsupportedEncodingException {
            this(requireNonNull(out, "Null output stream"), autoFlush, toCharset(encoding));
        }
        public PrintStream(OutputStream out, boolean autoFlush, Charset charset) {
            super(out);
            this.autoFlush = autoFlush;
            this.charOut = new OutputStreamWriter(this, charset);
            this.textOut = new BufferedWriter(charOut);
        }
        public PrintStream(String fileName) throws FileNotFoundException {
            this(false, new FileOutputStream(fileName));
        }
        public PrintStream(String fileName, String csn)
            throws FileNotFoundException, UnsupportedEncodingException {
            this(false, toCharset(csn), new FileOutputStream(fileName));
        }
        public PrintStream(String fileName, Charset charset) throws IOException {
            this(false, requireNonNull(charset, "charset"), new FileOutputStream(fileName));
        }
        public PrintStream(File file) throws FileNotFoundException {
            this(false, new FileOutputStream(file));
        }
        public PrintStream(File file, String csn)
            throws FileNotFoundException, UnsupportedEncodingException {
            this(false, toCharset(csn), new FileOutputStream(file));
        }
        public PrintStream(File file, Charset charset) throws IOException {
            this(false, requireNonNull(charset, "charset"), new FileOutputStream(file));
        }
    
    private static <T> T requireNonNull(T obj, String message) {
        if (obj == null)
            throw new NullPointerException(message);
        return obj;
    }
    private void newLine() {
        try {
            synchronized (this) {
                ensureOpen();
                textOut.newLine();
                textOut.flushBuffer();
                charOut.flushBuffer();
                if (autoFlush)
                    out.flush();
            }
        }
        catch (InterruptedIOException x) {
            Thread.currentThread().interrupt();
        }
        catch (IOException x) {
            trouble = true;
        }
    }
    public void println() {
        newLine();
    }
}
```



```java
// BufferedOutputStream.java
// 데이터를 출력할 때 버퍼링을 제공하여 출력 성능을 향상시키는 클래스이다.
package java.io;
public class BufferedOutputStream extends FilterOutputStream {
    protected byte buf[];
    protected int count;
    
    public BufferedOutputStream(OutputStream out) {
        this(out, 8192);
    }
    public BufferedOutputStream(OutputStream out, int size) {
        super(out);
        if (size <= 0) {
            throw new IllegalArgumentException("Buffer size <= 0");
        }
        buf = new byte[size];
    }
}
```





```java
// FileOutputStream.java
// 파일에 데이터를 바이트 스트림으로 출력하는 기능을 제공하는 클래스이다.
package java.io;
public class FileOutputStream extends OutputStream {
    private static final JavaIOFileDescriptorAccess fdAccess =
        SharedSecrets.getJavaIOFileDescriptorAccess();
    private final FileDescriptor fd;
    private volatile FileChannel channel;
    private final String path;
    private final Object closeLock = new Object();
    private violatile boolean closed;
    
    public FileOutputStream(String name)
        throws FileNotFoundException {
        this(name != null ? new File(name) : null, false);
    }
    public FileOutputStream(String name, boolean append)
        throws FileNotFoundException {
        this(name != null ? new File(name) : null, append);
    }
    public FileOutputStream(File file)
        throws FileNotFoundException {
        this(file, false);
    }
    public FileOutputStream(File file, boolean append)
        throws FileNotFoundException {
        String name = (file != null ? file.getPath() : null);
        @SuppressWarnings("removal")
        SecurityManager security = System.getSecurityManager();
        if (security != null) {
            security.checkWrite(name);
        }
        if (name == null) {
            throw new NullPointerException();
        }
        if (file.isInvalid()) {
            throw new FileNotFoundException("Invalid file path");
        }
        this.fd = new FileDescriptor();
        fd.attach(this);
        this.path = name;

        open(name, append);
        FileCleanable.register(fd);
    }
    
    public FileOutputStream(FileDescriptor fdObj) {
        @SuppressWarnings("removal")
        SecurityManager security = System.getSecurityManager();
        if (fdObj == null) {
            throw new NullPointerException();
        }
        if (security != null) {
            security.checkWrite(fdObj);
        }
        this.fd = fdObj;
        this.path = null;

        fd.attach(this);
    }
}
```



```java
// FileDescriptor.java
// 파일이나 소켓과 같은 운영 체제의 I/O자원을 나타내는 추상화된 핸들을 표현하기 위한 클래스이다.
package java.io;
public final class FileDescriptor {
    private int fd;
    private long handle;
    private Closeable parent;
    private List<Closeable> otherParents;
    private boolean closed;
    private boolean append;
    
    public FileDescriptor() {
        fd = -1;
        handle = -1;
    }
    private FileDescriptor(int fd) {
        this.fd = fd;
        this.handle = getHandle(fd);
        this.append = getAppend(fd);
    }
    	
    public static final FileDescriptor in = new FileDescriptor(0);
    public static final FileDescriptor out = new FileDescriptor(1);
    public static final FileDescriptor err = new FileDescriptor(2);
    
    synchronized void attach(Closeable c) {
        if (parent == null) {
            // first caller gets to do this
            parent = c;
        } else if (otherParents == null) {
            otherParents = new ArrayList<>();
            otherParents.add(parent);
            otherParents.add(c);
        } else {
            otherParents.add(c);
        }
    }
}
```



```java
// OutputStreamWriter.java
// 바이트 스트림을 문자 스트림으로 변환하는 역할을 한다.
// OutputStream을 래핑하여 문자 인코딩을 처리한다.
package java.io;
public class OutputStreamWriter extends Writer {
    private final StreamEncoder se;
    
    public OutputStreamWriter(OutputStream out) {
        super(out);
        se = StreamEncoder.forOutputStreamWriter(out, this,
                Charset.defaultCharset());
    }
}
```



```java
// StreamEncoder.java
// 문자 데이터를 바이트 데이터로 인코딩하는 클래스이다.
package sun.nio.cs;
public class StreamEncoder extends Writer {
    private static final int DEFAULT_BYTE_BUFFER_SIZE = 8192;
    private volatile boolean closed;
    
    
}
```



```java
// Charset.java
package java.nio.charset;
public abstract class Charset implements Comparable<Charset> {
    private static volatile Charset defaultCharset;
    
    public static Charset defaultCharset() {
        if (defaultCharset == null) {
            synchronized  (Charset.class) {
                String csn = GetPropertyAction.
                    	privilegedGetProperty("file.encoding");
                Charset cs = lookup(csn);
                if (cs != null)
                    defaultCharset = cs;
                else
                    defaultCharset = sun.nio.cs.UTF_8.INSTANCE;
            }
        }
        return defaultCharset;
    }
}
```



- 

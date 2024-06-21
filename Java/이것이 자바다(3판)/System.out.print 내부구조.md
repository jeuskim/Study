```java
// System.java
package java.lang;
public final class System {
    public static final InputStream in = null;
    public static final PrintStream out = null;
    public static final PrintStream err = null;
}
```



```java
// PrintStream.java
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


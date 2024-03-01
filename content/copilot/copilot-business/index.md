class Book {
    private String title;
    private String author;
    private int code;
    private int numPages;

    public Book(String title, String author, int code, int numPages) {
        this.title = title;
        this.author = author;
        this.code = code;
        this.numPages = numPages;
    }

    public String getInfo() {
        return String.format("%s, %s (%d), %d pages", title, author, code, numPages);
    }
}

class eBook extends Book {
    private double sizeMB;

    public eBook(String title, String author, int code, double sizeMB) {
        super(title, author, code, -1);
        this.sizeMB = sizeMB;
    }

    @Override
    public String getInfo() {
        return String.format("%s, %s (%d), %.2f MB", title, author, code, sizeMB);
    }
}

class BookStore {
    private List<Book> books;

    public BookStore() {
        books = new ArrayList<>();
    }

    public void addElement(Book book) {
        books.add(book);
    }

    public void searchElement(int code) {
        Book book = findBookByCode(code);
        if (book != null) {
            System.out.println("Book found: " + book.getInfo());
        } else {
            System.out.println("Book with code " + code + " not found!");
        }
    }

    private Book findBookByCode(int code) {
        for (Book book : books) {
            if (book.getCode() == code) {
                return book;
            }
        }
        return null;
    }
}

class PrintFrame {
    // ... GUI implementation ...

    public void printBooks() {
        // Sort books by code
        Collections.sort(books, Comparator.comparingInt(Book::getCode));

        // Print book details
        for (Book book : books) {
            System.out.println(book.getInfo());
        }

        // Print book counts
        int conventionalCount = 0;
        int electronicCount = 0;
        for (Book book : books) {
            if (book instanceof Book) {
                conventionalCount++;
            } else {
                electronicCount++;
            }
        }
        System.out.println("Total conventional books: " + conventionalCount);
        System.out.println("Total electronic books: " + electronicCount);
    }
}

public class Main {
    public static void main(String[] args) {
        // Create books
        Book book1 = new Book("Book 1", "Your Name", 100, 200);
        Book book2 = new Book("Book 2", "Author 2", 101, 300);
        eBook ebook1 = new eBook("eBook 1", "Author 3", 102, 1.5);
        eBook ebook2 = new eBook("eBook 2", "Author 4", 103, 2.0);

        // Create bookstore and add books
        BookStore bookstore = new BookStore();
        bookstore.addElement(book1

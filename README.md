# perpus_Association_aknas
class Book:
    def __init__(self, judul, penulis):
        self.judul = judul
        self.penulis = penulis
        self.is_available = True

    def borrow(self):
        if self.is_available:
            self.is_available = False
            return True
        else:
            return False

    def return_book(self):
        self.is_available = True


class LibraryMember:
    def __init__(self, name):
        self.name = name
        self.borrowed_books = []

    def borrow_book(self, book):
        if book.borrow():
            self.borrowed_books.append(book)
            print(f"{self.name} telah meminjam buku '{book.judul}' by {book.penulis}")
        else:
            print(f"The book '{book.judul}' by {book.penulis} is currently not available.")

    def return_book(self, book):
        if book in self.borrowed_books:
            book.return_book()
            self.borrowed_books.remove(book)
            print(f"{self.name} telah mengembalikan buku '{book.judul}' by {book.penulis}")
        else:
            print(f"The book '{book.judul}' by {book.penulis}' is not in the borrowed list of {self.name}.")

    def display_borrowed_books(self):
        print(f"Buku yang dipinjam oleh {self.name}:")
        if len(self.borrowed_books) == 0:
            print("Tidak ada buku yang dipinjam")
        for book in self.borrowed_books:
            print(f"Judul: {book.judul}")
            print(f"Penulis: {book.penulis}")
            print(f"Ketersediaan: {'Available' if book.is_available else 'Tidak tersedia'}")
            print()



member = LibraryMember("Nanda")


book1 = Book("Laskar Pelangi", "Andrea Hirata")
book2 = Book("Bumi Manusia", "Pramoedya Ananta Toer")


member.borrow_book(book1)
member.borrow_book(book2)

member.display_borrowed_books()
member.return_book(book1)

member.display_borrowed_books()

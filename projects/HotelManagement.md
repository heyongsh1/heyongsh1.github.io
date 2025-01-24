---
layout: project
type: project
image: img/Library-Logo.png
title: "Library Management System"
date: 2023
published: true
labels:
  - Vs Code
  - Google Docs
summary: "A Library Management System that we created in ICS 211"
---

<img class="img-fluid" src="../img/LMS.png">

In ICS 211 our group was asked to create a library management system using C++. We used a website called Replit to collaborate work on the code and share our ideas/codes within the group. There was add book, delete book, edit book, search book, view all books, and quit. 

<hr>

<pre>
class Book {
private:
  std::string isbn;
  std::string title;
  std::string author;
  std::string edition;
  std::string publication;




public:
  virtual void displayBookInfo() const {
      std::cout << "ISBN: " << isbn << "\nTitle: " << title << "\nAuthor: " << author
                << "\nEdition: " << edition << "\nPublication: " << publication << "\n";
  }








  void setIsbn(const std::string& value) { isbn = value; }
  void setTitle(const std::string& value) { title = value; }
  void setAuthor(const std::string& value) { author = value; }
  void setEdition(const std::string& value) { edition = value; }
  void setPublication(const std::string& value) { publication = value; }




  std::string getIsbn() const { return isbn; }
  std::string getTitle() const { return title; }
  std::string getAuthor() const { return author; }
  std::string getEdition() const { return edition; }
  std::string getPublication() const { return publication; }
};




class Fiction : public Book {
private:
  std::string genre;




public:
  void setGenre(const std::string& g) { genre = g; }
  std::string getGenre() const { return genre; }




   void displayBookInfo() const override {
      std::cout << "Fiction Book\n";
      Book::displayBookInfo();
      std::cout << "Genre: " << genre << "\n";
  }
};




class NonFiction : public Book {
private:
  std::string topic;




public:
  void setTopic(const std::string& t) { topic = t; }
  std::string getTopic() const { return topic; }




   void displayBookInfo() const override {
      std::cout << "Non-Fiction Book\n";
      Book::displayBookInfo();
      std::cout << "Topic: " << topic << "\n";
  }
};




class Library {
private:
  static const int MAX_BOOKS = 100;
  Book* books[MAX_BOOKS];         
  int numBooks;                     




public:
  Library() : numBooks(0) {}




   void addBook(Book* book) {
      if (numBooks < MAX_BOOKS) {
          books[numBooks++] = book;
      } else {
          std::cout << "Library is full. Cannot add more books.\n";
      }
  }




  void deleteBook(const std::string& isbn) {
      for (int i = 0; i < numBooks; ++i) {
          if (books[i]->getIsbn() == isbn) {
            
              for (int j = i; j < numBooks - 1; ++j) {
                  books[j] = books[j + 1];
              }
              delete books[--numBooks];
              std::cout << "Book with ISBN " << isbn << " deleted.\n";
              return;
          }
      }
      std::cout << "Book with ISBN " << isbn << " not found.\n";
  }




   void searchBook(const std::string& isbn) const {
      for (int i = 0; i < numBooks; ++i) {
          if (books[i]->getIsbn() == isbn) {
              books[i]->displayBookInfo();
              return;
          }
      }
      std::cout << "Book with ISBN " << isbn << " not found.\n";
  }




  void viewAllBooks() const {
      if (numBooks == 0) {
          std::cout << "No books in the library.\n";
      } else {
          std::cout << "All Books in the Library:\n";
          for (int i = 0; i < numBooks; ++i) {
              books[i]->displayBookInfo();
              std::cout << "------------------------\n";
          }
      }
  }








  void editBook(const std::string& isbn) {
      for (int i = 0; i < numBooks; ++i) {
          if (books[i]->getIsbn() == isbn) {
              std::cout << "Enter new details for the book with ISBN " << isbn << ":\n";
              std::string newTitle;
              std::cout << "Enter new Title: ";
              std::cin.ignore();
              std::getline(std::cin, newTitle);
              books[i]->setTitle(newTitle);
              std::cout << "Book details updated.\n";
              return;
          }
      }
      std::cout << "Book with ISBN " << isbn << " not found.\n";
  }




   ~Library() {
      for (int i = 0; i < numBooks; ++i) {
          delete books[i];
      }
  }
};




int main() {
  Library library;




  int choice;
  std::string isbn;




  do {
      std::cout << "\nLIBRARY MANAGEMENT SYSTEM\n"
                << "[1] ADD FICTION BOOK\n"
                << "[2] ADD NONFICTION BOOK\n"
                << "[3] DELETE BOOK\n"
                << "[4] EDIT BOOK\n"
                << "[5] SEARCH BOOK\n"
                << "[6] VIEW ALL BOOKS\n"
                << "[7] EXIT\n\n"
                << "Enter Choice: ";
      std::cin >> choice;




      switch (choice) {
          case 1: {
              // Add a new fiction book
              Fiction* newFiction = new Fiction();




            
              std::cout << "Enter ISBN: ";
              std::cin >> isbn;
              newFiction->setIsbn(isbn);




              std::cout << "Enter Title: ";
              std::cin.ignore();
              std::getline(std::cin, isbn);
              newFiction->setTitle(isbn);




              std::cout << "Enter Author: ";
              std::getline(std::cin, isbn);
              newFiction->setAuthor(isbn);




              std::cout << "Enter Edition: ";
              std::getline(std::cin, isbn);
              newFiction->setEdition(isbn);




              std::cout << "Enter Publication: ";
              std::getline(std::cin, isbn);
              newFiction->setPublication(isbn);




              std::cout << "Enter Genre: ";
              std::getline(std::cin, isbn);
              newFiction->setGenre(isbn);


              std::cout << "Book Added";
              library.addBook(newFiction);
              break;
          }
          case 2: {
              // Add a new nonfiction book
              NonFiction* newNonFiction = new NonFiction();




              std::cout << "Enter ISBN: ";
              std::cin >> isbn;
              newNonFiction->setIsbn(isbn);




              std::cout << "Enter Title: ";
              std::cin.ignore();
              std::getline(std::cin, isbn);
              newNonFiction->setTitle(isbn);




              std::cout << "Enter Author: ";
              std::getline(std::cin, isbn);
              newNonFiction->setAuthor(isbn);




              std::cout << "Enter Edition: ";
              std::getline(std::cin, isbn);
              newNonFiction->setEdition(isbn);




              std::cout << "Enter Publication: ";
              std::getline(std::cin, isbn);
              newNonFiction->setPublication(isbn);




              std::cout << "Enter Topic: ";
              std::getline(std::cin, isbn);
              newNonFiction->setTopic(isbn);


              std::cout << "Book Added!!!!";
              library.addBook(newNonFiction);
              break;
          }
          case 3: {
              // Delete a book
              std::cout << "Enter ISBN of the book to delete: ";
              std::cin >> isbn;
              library.deleteBook(isbn);
              break;
          }
          case 4: {
              // Edit book details
              std::cout << "Enter ISBN of the book to edit: ";
              std::cin >> isbn;
              library.editBook(isbn);
              break;
          }
          case 5: {
              // Search for a book
              std::cout << "Enter ISBN of the book to search: ";
              std::cin >> isbn;
              library.searchBook(isbn);
              break;
          }
          case 6: {
              // View all books
              library.viewAllBooks();
              break;
          }
          case 7: {
              // Exit the program
              std::cout << "Exiting the program.\n";
              break;
          }
          default: {
              std::cout << "Invalid choice. Please try again.\n";
              break;
          }
      }




  } while (choice != 7);




  return 0;
}

</pre>

<hr>

Source: <a href="https://docs.google.com/document/d/1jpQbiyqe7CwpEd0ZL1BhP7pYfsnICr3eLIA-m5oNKw0/edit?tab=t.0"><i class="large github icon "></i>Group-8-Project</a>

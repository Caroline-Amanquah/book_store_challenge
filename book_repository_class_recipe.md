Books Model and Repository Classes Design Recipe
Copy this recipe template to design and implement Model and Repository classes for a database table.

1. Design and create the Table:
- Completed

2. Create Test SQL seeds:

TRUNCATE TABLE books RESTART IDENTITY; 

INSERT INTO books (title, author_name) VALUES ('Nineteen Eighty-Four', 'George Orwell');
INSERT INTO books (title, author_name) VALUES ('Mrs Dalloway', 'Virginia Woolf');
INSERT INTO books (title, author_name) VALUES ('Emma', 'Jane Austen');
INSERT INTO books (title, author_name) VALUES ('Dracula', 'Bram Stoker');
INSERT INTO books (title, author_name) VALUES ('The Age of Innocence', 'Edith Wharton');

psql -h 127.0.0.1 book_store_test < seeds_books.sql

3. Define the class names

class Book
end

class BookRepository
end

4. Implement the Model class
Define the attributes of your Model class.

class Book
  attr_accessor :id, :title, :author_name
end

5. Define the Repository Class interface

class BookRepository

  def all
    # Executes the SQL query:
    # SELECT id, title, author_name FROM books;

    # Returns an array of book objects.
  end

end
6. Write Test Examples
Write Ruby code that defines the expected behaviour of the Repository class, following your design from the table written in step 5.

These examples will later be encoded as RSpec tests.


# 1
# Get all books

repo = BookRepository.new
books = repo.all

expect(books.length).to eq(5)
  

7. Reload the SQL seeds before each test run
Running the SQL code present in the seed file will empty the table and re-insert the seed data.

  def reset_books_table
    seed_sql = File.read('spec/seeds_books.sql')
    connection = PG.connect({ host: '127.0.0.1', dbname: 'book_store_test' })
    connection.exec(seed_sql)
  end

  describe BookRepository do
    before(:each) do 
      reset_books_table
    end
  end 

8. Test-drive and implement the Repository class behaviour
After each test you write, follow the test-driving process of red, green, refactor to implement the behaviour.
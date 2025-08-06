# CIDRIE_Learning

## File Pasring and Data Extraction
### This program done by splitting the contents in the given file
```
with open("sample_logs.txt") as file:
    for line in file:
        if "ERROR" in line:
            timestamp = line.split(']')[0][1:]
            error = line.split(']')[1].split("ERROR")[1].strip()
            print(f"{timestamp} {error}")
```

## Library Management System
### This program is to add new books to the library and show the status while borrowing. Also return status about the book availability
```
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author
        self.available = True
    def borrow(self):
        if self.available:
            self.available = False
            print(f"You borrowed '{self.title}'")
        else:
            print(f"Sorry, '{self.title}' is already borrowed")
    def return_book(self):
        if not self.available:
            self.available = True
            print(f"You returned '{self.title}'")
        else:
            print(f"'{self.title}' was not borrowed")
    def __str__(self):
        if self.available:
            status = "Available"
        else:
            status = "Borrowed"
        return f"'{self.title}' by {self.author} - {status}"

class Library:
    def __init__(self):
        self.books = []
    def add_book(self, book):
        self.books.append(book)
    def show_books(self):
        print("\nLibrary Details:")
        for book in self.books:
            print(book)
    def find_book(self, title):
        for book in self.books:
            if book.title.lower() == title.lower():
                return book
        return None

book1 = Book("Reminders of Him", "Colleen Hoover")
book2 = Book("The Happy Place", "Emily Henry")
library = Library()
library.add_book(book1)
library.add_book(book2)
book = library.find_book("Spanish Love Deception")
if book:
    book.borrow()
    book.return_book()
else:
    print(f"Book not found")
library.show_books()
```

## Pandas Analysis
### First read a csv file and replaced the null values with mean value. Then displayed the mean of each subjects 
```
import pandas as pd
df = pd.read_csv("sample_data.csv")
\df_filled = df.copy()

# Take each column except name
for column in df.columns[1:]:

    # find the mean of each column by skipping null values(NaN)
    mean = df[column].mean(skipna=True)

    # fill the null values(NaN) with calculated mean
    df_filled[column] = df_filled[column].fillna(mean)

# calculate the mean of each subject
sub_avg = df_filled.iloc[:, 1:].mean()

print("Cleaned Data:")
print(df_filled)
print("Average Marks per Subject:")
print(sub_avg)
```
## Time Complexity
### This program is done by passing a million set and target value. If the sum of two numbers from the list is same as the target value then print pair found else print not found
```
def pair(nums, target):
    num_set = set()
    for i in nums:
        num = target - i
        if num in num_set:
            return(num, i)
        num_set.add(i)
    return None

nums = range(1000001)
target = 10

# pass million set and target value
result = pair(nums, target)

if result:
    print("Pair found", result)
else:
    print("No pair found")
```

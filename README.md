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
## Face Detection using HAAR classification
### This code uses OpenCV and a Haar Cascade to detect faces from a live webcam feed and highlight the face and T-zone region in real time.
```
import cv2

face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
)

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    frame = cv2.flip(frame, 1)
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    faces = face_cascade.detectMultiScale(gray, 1.1, 5)

    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (255, 0, 0), 2)

        tz_x1 = int(x + 0.25 * w)
        tz_y1 = int(y + 0.15 * h)
        tz_x2 = int(x + 0.75 * w)
        tz_y2 = int(y + 0.65 * h)

        cv2.rectangle(
            frame,
            (tz_x1, tz_y1),
            (tz_x2, tz_y2),
            (0, 255, 0),
            2
        )

    cv2.imshow("OpenCV + Haar + T-Zone", frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

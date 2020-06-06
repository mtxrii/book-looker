# Book Looker
A sleek web app with the express purpose of looking up books.

<img src="https://i.imgur.com/pzXgpCP.png" width=60%>

## Background
This app uses the Google Books API to return and display a list of book requests. While it is not a search engine of its own, it does provide an elegant view of the Google Books virtual library, and has some nice tools regarding ISBNs. This project has mainly served us as practice for creating web apps and using Json APIs.

### Usage
To find books, simply input a title, author or ISBN, and the closest results will be displayed in card format. Clicking on a book card displays a description of the book with a link at the bottom to search for it on amazon.

<img src="https://i.imgur.com/VTptbQY.png" width=60%>

## ISBNs
This app also serves as a utility to check the validity of International Standard Book Numbers (ISBNs) and provides random generation of valid ISBNs as well.

### Usage
To check an ISBN's validity, simply search for it. If it is not a valid ISBN, you will be notified and no search will be preformed. If it is valid, but no book has been assigned to it, then the search will turn up empty. Of course if a book by that ISBN does exist, it will come up.

Under the `ISBN Gen` tab, pressing the `Generate New` button will provide pseudorandomized valid ISBN codes. The button on the right of them copies that code.

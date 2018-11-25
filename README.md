# BookEx - Frontend

Allows users to search books, add books to their favourites or wishlist, indicate which book they are currently reading, and offer up books for loan (and see which books other users are offering for loan).

## How it works for users
- On app load the home page displays a selection of books users have added to their favourites and wishlists, and on the right shows a leaderboard of books people are currently reading, and how many readers each has.
- Without being logged in, users can search for books, and click for more details. 
- When logged in users can add books to their favourites or wishlist, indicate they are currently reading a book, and offer a book up for loan (or remove it from availability for loan)
- From the loan shelf page, users can see what books are available for loan, and click on any to see which user has it available.
- From their profile page, users can view and remove books on their wishlist and favourite lists.

## Frontend structure
Written in React. `npm install && npm run start` to start the frontend in development mode. The backend is live on Heroku and the frontend will get data from and post data to that server unless told otherwise (in API.js). Backend code is here: https://github.com/CiaranMn/bookex-backend

The app routing depending on user action is set out in App.js and can be thought of in 3 sections:
- The navigation header, which is always there (but displays different links depending on whether a user is logged in)
- The left main-container, which at first displays a sample of books users have already added to their lists. It will change to displaying one of: search results containing book when a search is made; the user's wishlist and favourite lists on the profile page; or the list of books available for loan on the loan shelf page. The random sample can be returned to by clicking on the logo.
- The right-container, which at first displays the leaderboard of popular books (books which users have indicated they are currently reading), and changes to display book details when a book is clicked, the signup form, or the user's profile box (basic info).

Both the book cards in search results and user lists (which appear on the left) and the book details page (on the right) need to know what books are on which lists for a current user, to allow them to add/remove books to lists directly from the search results or book details depending on their preference. This has led to the state and logic relating to adding and removing from lists living in App, a lot of drilling down props, and makes the application a prime candidate for refactoring to use Redux.

### Other things of note
- API.js makes requests are made to the backend, which deals with the Google Books API for searches, and persists books to the database when users save them on any list. It also saves JSON Web Tokens to browser localStorage following signup or login and retrieves them as necessary for requests requring authentification.
- The BookCard component does a lot of work, appearing in the search results, popular books box, and lists on the user profile page, with conditional styling depending on where it is rendered.
- BookDetails also has a lot of logic, as it displays whether a user is reading a book, has favourited a book, has added it to their wishlist, or has offered it for loan, and allows them to change the status of any of those (there are arguably too many lists involved at the moment)
- There is endless scroll/fetching on the search results when users scroll down, but not on the welcome page displaying books users have already added to their lists, which will only ever get a sample of 100 from the backend.

## TODO
**Refocus the app on the 'loan shelf' function** - the world probably doesn't need another Goodreads but building/company intranets could maybe use a book exchange:
- Loans to be associated with locations, and users to be shown loans available in their location only
- Facility for users to message people with loans on offer expressing interest (with email alert to recipient)
- Loan offerers to record when they have lent a book out, and see in their profile who it was given to and when
- Feature to log when a book is returned, and have it go back on the loan shelf (unless the owner doesn't want it to)
- Wishlist feature to be tweaked to tie in to loan exchange concept, e.g. 'user is looking to borrow this book if anyone has it'

**Also** 
- connect Redux to reduce the state/prop-passing contortion currently going on (unless the refocusing mentioned makes this less worthwhile)
- make clearer to users what different pages are showing them (e.g. there is no indication at present that the homepage initially displays books that other users have added to their favourites/wishlist)
- allow users to edit their registration information



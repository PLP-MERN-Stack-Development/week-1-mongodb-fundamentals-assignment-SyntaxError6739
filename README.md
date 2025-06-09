[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=19737399&assignment_repo_type=AssignmentRepo)
# MongoDB Fundamentals Assignment

This assignment focuses on learning MongoDB fundamentals including setup, CRUD operations, advanced queries, aggregation pipelines, and indexing.

## Assignment Overview

You will:
1. Set up a MongoDB database
2. Perform basic CRUD operations
3. Write advanced queries with filtering, projection, and sorting
4. Create aggregation pipelines for data analysis
5. Implement indexing for performance optimization

## Getting Started

1. Accept the GitHub Classroom assignment invitation
2. Clone your personal repository that was created by GitHub Classroom
3. Install MongoDB locally or set up a MongoDB Atlas account
4. Run the provided `insert_books.js` script to populate your database
5. Complete the tasks in the assignment document

## Files Included

- `Week1-Assignment.md`: Detailed assignment instructions
- `insert_books.js`: Script to populate your MongoDB database with sample book data

## Requirements

- Node.js (v18 or higher)
- MongoDB (local installation or Atlas account)
- MongoDB Shell (mongosh) or MongoDB Compass

## Submission

Your work will be automatically submitted when you push to your GitHub Classroom repository. Make sure to:

1. Complete all tasks in the assignment
2. Add your `queries.js` file with all required MongoDB queries
3. Include a screenshot of your MongoDB database
4. Update the README.md with your specific setup instructions

## Resources

// MongoDB Books Database - Complete Tutorial
// This tutorial covers CRUD operations, advanced queries, aggregation, and indexing

// ============================================
// TASK 2: BASIC CRUD OPERATIONS
// ============================================

// Step 1: Connect to MongoDB and select database
use('bookstore');

// Step 2: Insert Books Data (insert_books.js script)
const booksData = [
  {
    title: "The Great Gatsby",
    author: "F. Scott Fitzgerald",
    genre: "Classic Literature",
    published_year: 1925,
    price: 12.99,
    in_stock: true,
    pages: 180,
    publisher: "Scribner"
  },
  {
    title: "To Kill a Mockingbird",
    author: "Harper Lee",
    genre: "Classic Literature",
    published_year: 1960,
    price: 14.99,
    in_stock: true,
    pages: 281,
    publisher: "J.B. Lippincott & Co."
  },
  {
    title: "1984",
    author: "George Orwell",
    genre: "Dystopian Fiction",
    published_year: 1949,
    price: 13.99,
    in_stock: false,
    pages: 328,
    publisher: "Secker & Warburg"
  },
  {
    title: "Pride and Prejudice",
    author: "Jane Austen",
    genre: "Romance",
    published_year: 1813,
    price: 11.99,
    in_stock: true,
    pages: 432,
    publisher: "T. Egerton"
  },
  {
    title: "The Catcher in the Rye",
    author: "J.D. Salinger",
    genre: "Coming-of-age Fiction",
    published_year: 1951,
    price: 15.99,
    in_stock: true,
    pages: 277,
    publisher: "Little, Brown and Company"
  },
  {
    title: "Harry Potter and the Philosopher's Stone",
    author: "J.K. Rowling",
    genre: "Fantasy",
    published_year: 1997,
    price: 16.99,
    in_stock: true,
    pages: 223,
    publisher: "Bloomsbury"
  },
  {
    title: "The Lord of the Rings",
    author: "J.R.R. Tolkien",
    genre: "Fantasy",
    published_year: 1954,
    price: 24.99,
    in_stock: false,
    pages: 1216,
    publisher: "George Allen & Unwin"
  },
  {
    title: "Dune",
    author: "Frank Herbert",
    genre: "Science Fiction",
    published_year: 1965,
    price: 18.99,
    in_stock: true,
    pages: 688,
    publisher: "Chilton Books"
  },
  {
    title: "The Hobbit",
    author: "J.R.R. Tolkien",
    genre: "Fantasy",
    published_year: 1937,
    price: 13.99,
    in_stock: true,
    pages: 310,
    publisher: "George Allen & Unwin"
  },
  {
    title: "Brave New World",
    author: "Aldous Huxley",
    genre: "Dystopian Fiction",
    published_year: 1932,
    price: 14.99,
    in_stock: true,
    pages: 268,
    publisher: "Chatto & Windus"
  },
  {
    title: "The Da Vinci Code",
    author: "Dan Brown",
    genre: "Thriller",
    published_year: 2003,
    price: 17.99,
    in_stock: true,
    pages: 454,
    publisher: "Doubleday"
  },
  {
    title: "Gone Girl",
    author: "Gillian Flynn",
    genre: "Thriller",
    published_year: 2012,
    price: 16.99,
    in_stock: false,
    pages: 419,
    publisher: "Crown Publishing Group"
  }
];

// Insert all books into the collection
db.books.insertMany(booksData);
console.log("✅ Successfully inserted", booksData.length, "books");

// ============================================
// BASIC CRUD QUERIES
// ============================================

// 1. Find all books in a specific genre
console.log("\n📚 Books in Fantasy genre:");
db.books.find({ genre: "Fantasy" }).pretty();

// 2. Find books published after a certain year (e.g., after 2000)
console.log("\n📅 Books published after 2000:");
db.books.find({ published_year: { $gt: 2000 } }).pretty();

// 3. Find books by a specific author
console.log("\n✍️ Books by J.R.R. Tolkien:");
db.books.find({ author: "J.R.R. Tolkien" }).pretty();

// 4. Update the price of a specific book
console.log("\n💰 Updating price of 'The Great Gatsby':");
db.books.updateOne(
  { title: "The Great Gatsby" },
  { $set: { price: 15.99 } }
);
console.log("Price updated successfully");

// Verify the update
db.books.findOne({ title: "The Great Gatsby" }, { title: 1, price: 1 });

// 5. Delete a book by its title
console.log("\n🗑️ Deleting 'Gone Girl':");
db.books.deleteOne({ title: "Gone Girl" });
console.log("Book deleted successfully");

// ============================================
// TASK 3: ADVANCED QUERIES
// ============================================

// 1. Find books that are both in stock and published after 2010
console.log("\n🔍 Books in stock and published after 2010:");
db.books.find({
  $and: [
    { in_stock: true },
    { published_year: { $gt: 2010 } }
  ]
}).pretty();

// 2. Use projection to return only title, author, and price fields
console.log("\n📋 Books with selected fields only:");
db.books.find(
  { genre: "Fantasy" },
  { title: 1, author: 1, price: 1, _id: 0 }
).pretty();

// 3. Sorting by price (ascending)
console.log("\n📈 Books sorted by price (ascending):");
db.books.find(
  {},
  { title: 1, price: 1, _id: 0 }
).sort({ price: 1 }).pretty();

// 4. Sorting by price (descending)
console.log("\n📉 Books sorted by price (descending):");
db.books.find(
  {},
  { title: 1, price: 1, _id: 0 }
).sort({ price: -1 }).pretty();

// 5. Pagination - First page (5 books per page)
console.log("\n📄 Page 1 (first 5 books):");
db.books.find(
  {},
  { title: 1, author: 1, price: 1, _id: 0 }
).limit(5).pretty();

// 6. Pagination - Second page
console.log("\n📄 Page 2 (next 5 books):");
db.books.find(
  {},
  { title: 1, author: 1, price: 1, _id: 0 }
).skip(5).limit(5).pretty();

// ============================================
// TASK 4: AGGREGATION PIPELINE
// ============================================

// 1. Calculate average price of books by genre
console.log("\n📊 Average price by genre:");
db.books.aggregate([
  {
    $group: {
      _id: "$genre",
      averagePrice: { $avg: "$price" },
      bookCount: { $sum: 1 }
    }
  },
  {
    $project: {
      genre: "$_id",
      averagePrice: { $round: ["$averagePrice", 2] },
      bookCount: 1,
      _id: 0
    }
  },
  {
    $sort: { averagePrice: -1 }
  }
]).pretty();

// 2. Find the author with the most books
console.log("\n👑 Author with most books:");
db.books.aggregate([
  {
    $group: {
      _id: "$author",
      bookCount: { $sum: 1 },
      books: { $push: "$title" }
    }
  },
  {
    $sort: { bookCount: -1 }
  },
  {
    $limit: 1
  },
  {
    $project: {
      author: "$_id",
      bookCount: 1,
      books: 1,
      _id: 0
    }
  }
]).pretty();

// 3. Group books by publication decade
console.log("\n📅 Books grouped by publication decade:");
db.books.aggregate([
  {
    $addFields: {
      decade: {
        $subtract: [
          "$published_year",
          { $mod: ["$published_year", 10] }
        ]
      }
    }
  },
  {
    $group: {
      _id: "$decade",
      count: { $sum: 1 },
      books: {
        $push: {
          title: "$title",
          year: "$published_year"
        }
      }
    }
  },
  {
    $project: {
      decade: { $concat: [{ $toString: "$_id" }, "s"] },
      count: 1,
      books: 1,
      _id: 0
    }
  },
  {
    $sort: { "_id": 1 }
  }
]).pretty();

// ============================================
// TASK 5: INDEXING
// ============================================

// 1. Create index on title field
console.log("\n🔍 Creating index on title field:");
db.books.createIndex({ title: 1 });
console.log("✅ Index created on title field");

// 2. Create compound index on author and published_year
console.log("\n🔍 Creating compound index on author and published_year:");
db.books.createIndex({ author: 1, published_year: -1 });
console.log("✅ Compound index created");

// 3. List all indexes
console.log("\n📋 All indexes on books collection:");
db.books.getIndexes();

// 4. Performance analysis with explain()
console.log("\n⚡ Query performance WITHOUT index (simulation):");
// First, let's see a query that would benefit from indexing
const explainResult = db.books.find({ title: "The Great Gatsby" }).explain("executionStats");
console.log("Execution stats:", {
  totalDocsExamined: explainResult.executionStats.totalDocsExamined,
  totalDocsReturned: explainResult.executionStats.totalDocsReturned,
  executionTimeMillis: explainResult.executionStats.executionTimeMillis,
  indexUsed: explainResult.executionStats.executionStages.stage === "IXSCAN"
});

// Query using the compound index
console.log("\n⚡ Query performance WITH compound index:");
const explainCompound = db.books.find({ 
  author: "J.R.R. Tolkien", 
  published_year: { $gte: 1950 } 
}).explain("executionStats");

console.log("Compound index execution stats:", {
  totalDocsExamined: explainCompound.executionStats.totalDocsExamined,
  totalDocsReturned: explainCompound.executionStats.totalDocsReturned,
  executionTimeMillis: explainCompound.executionStats.executionTimeMillis,
  indexUsed: explainCompound.executionStats.executionStages.stage === "IXSCAN"
});

// ============================================
// ADDITIONAL USEFUL QUERIES
// ============================================

// Complex query combining multiple conditions
console.log("\n🎯 Complex query - Fantasy books under $20 published after 1950:");
db.books.find({
  $and: [
    { genre: "Fantasy" },
    { price: { $lt: 20 } },
    { published_year: { $gt: 1950 } }
  ]
}, {
  title: 1,
  author: 1,
  price: 1,
  published_year: 1,
  _id: 0
}).sort({ published_year: -1 }).pretty();

// Text search preparation (create text index)
console.log("\n🔍 Creating text index for search:");
db.books.createIndex({ 
  title: "text", 
  author: "text", 
  genre: "text" 
});

// Text search example
console.log("\n🔍 Text search for 'tolkien':");
db.books.find({ $text: { $search: "tolkien" } }, {
  title: 1,
  author: 1,
  score: { $meta: "textScore" },
  _id: 0
}).sort({ score: { $meta: "textScore" } }).pretty();

// ============================================
// SUMMARY STATISTICS
// ============================================

console.log("\n📊 DATABASE SUMMARY:");
console.log("Total books:", db.books.countDocuments());
console.log("Books in stock:", db.books.countDocuments({ in_stock: true }));
console.log("Out of stock books:", db.books.countDocuments({ in_stock: false }));
console.log("Genres available:", db.books.distinct("genre").length);
console.log("Authors in collection:", db.books.distinct("author").length);

// Price statistics
const priceStats = db.books.aggregate([
  {
    $group: {
      _id: null,
      minPrice: { $min: "$price" },
      maxPrice: { $max: "$price" },
      avgPrice: { $avg: "$price" },
      totalValue: { $sum: "$price" }
    }
  },
  {
    $project: {
      minPrice: 1,
      maxPrice: 1,
      avgPrice: { $round: ["$avgPrice", 2] },
      totalValue: { $round: ["$totalValue", 2] },
      _id: 0
    }
  }
]).toArray();

console.log("Price statistics:", priceStats[0]);

// ============================================
// CLEANUP FUNCTIONS (Optional)
// ============================================

// Function to reset the collection
function resetCollection() {
  db.books.drop();
  console.log("Collection reset successfully");
}

// Function to remove all indexes (except _id)
function removeAllIndexes() {
  db.books.dropIndexes();
  console.log("All custom indexes removed");
}

console.log("\n✅ MongoDB Books Database Tutorial Completed!");
console.log("🎉 All tasks have been successfully demonstrated:");
console.log("   ✓ CRUD Operations");
console.log("   ✓ Advanced Queries with Projection and Sorting");
console.log("   ✓ Aggregation Pipelines");
console.log("   ✓ Indexing and Performance Analysis");
console.log("   ✓ Pagination Implementation");
console.log("   ✓ Text Search Capabilities");

- [MongoDB Documentation](https://docs.mongodb.com/)
- [MongoDB University](https://university.mongodb.com/)
- [MongoDB Node.js Driver](https://mongodb.github.io/node-mongodb-native/) 

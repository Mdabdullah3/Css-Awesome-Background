Question-1 == What is the purpose of creating a model with an interface and schema in MongoDB? How does it help in defining the structure of a collection?

Ans == Structure Definition: The interface defines the structure of the document in the collection, specifying the fields and their types. It acts as a blueprint for the documents stored in the collection. The schema further enforces this structure and allows defining additional validation rules, default values, and more.

Type Checking: By defining an interface, you can ensure that the data inserted or retrieved from the collection adheres to a specific structure and data types. This helps catch potential errors during development, ensuring that the data is consistent and correctly used throughout the application.

Validation and Constraints: The schema allows you to define validation rules for fields in the collection. These rules can enforce data types, check for required fields, define allowed values, and more. This helps maintain data integrity and prevent invalid or inconsistent data from being stored.

Question 2 == Explain the concept of field filtering in MongoDB. How can you specify which fields to include or exclude in the returned documents?

Ans == In MongoDB, you can specify field filters using the projection parameter in the find() method or the aggregate() method. There are two approaches to field filtering:

Inclusion Projection: db.collection.find({}, { field1: 1, field2: 1 }) - Returns documents with only field1 and field2 included.

Exclusion Projection: db.collection.find({}, { field1: 0, field2: 0 }) - Returns documents with field1 and field2 excluded.

Mixed Projection: db.collection.find({}, { field1: 1, field2: 0 }) - Returns documents with field1 included and field2 excluded.

Question 3 == What are instance methods in MongoDB models? Provide an example of a custom instance method and explain its purpose.

Ans == In MongoDB models, instance methods are custom methods that are defined on individual document instances. These methods are specific to each document and can be called on the document itself. Instance methods provide a way to encapsulate and define custom behavior or functionality for a specific document.

// Example MongoDB model
const bookSchema = new mongoose.Schema({
  title: String,
  author: String,
  genre: String,
  publicationYear: Number,
  price: Number
});

// Custom instance method
bookSchema.methods.calculateDiscountedPrice = function(discountPercentage) {
  const discountedPrice = this.price - (this.price * (discountPercentage / 100));
  return discountedPrice;
};

const Book = mongoose.model('Book', bookSchema);

// Usage
const book = new Book({
  title: 'Example Book',
  author: 'John Doe',
  genre: 'Fiction',
  publicationYear: 2021,
  price: 100
});

console.log(book.calculateDiscountedPrice(20)); // Output: 80


Question 4 == How do you use comparison operators like "$ne," "$gt," "$lt," "$gte," and "$lte" in MongoDB queries? Provide examples to illustrate their usage.

Ans == In MongoDB queries, comparison operators like "$ne" (not equal), "$gt" (greater than), "$lt" (less than), "$gte" (greater than or equal to), and "$lte" (less than or equal to) are used to perform comparisons between values in documents.

Here are examples to illustrate the usage of these comparison operators in MongoDB queries:

   1. "$ne" (not equal):
    db.books.find({ genre: { $ne: 'Sci-Fi' } });

   2. "$gt" (greater than):
   db.books.find({ rating: { $gt: 4.5 } });

   3. "$lt" (less than):
   db.books.find({ price: { $lt: 100 } });

   4."$gte" (greater than or equal to):
   db.books.find({ publicationYear: { $gte: 2020 } });

   5."$lte" (less than or equal to):
   db.books.find({ rating: { $lte: 4 } });

Question 5 == What are MongoDB’s “$in” and “$nin” operators? How can you use them to match values against an array of values or exclude values from a given array?

Ans == MongoDB's "$in" and "$nin" operators are used to match values against an array of values or exclude values from a given array in a MongoDB query.

1. "$in" operator:
The "$in" operator matches documents where the value of a field matches any value in the specified array.
db.books.find({ genre: { $in: ['Fantasy', 'Sci-Fi'] } });

2. "$nin" operator:
The "$nin" operator is the opposite of "$in" operator. It matches documents where the value of a field does not match any value in the specified array.
db.books.find({ genre: { $nin: ['Mystery', 'Thriller'] } });
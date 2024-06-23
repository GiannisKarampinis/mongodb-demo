# MongoDB Quick Reference Guide - Tutorial

# `find`

In MongoDB, the `find` command is used to query documents from a collection. It supports various options for filtering, projecting, sorting, limiting results, and more.

## Command Structure

```javascript
db.collection.find(
   <query>,
   <projection>
).sort(
   <sorting>
).limit(
   <limit>
).skip(
   <skip>
).collation(
   <collation>
).hint(
   <hint>
).explain(
   <verbosityMode>
)

db.collection.countDocuments( { <query> } );
```

## Components

<table>
    <tr>
        <td><code>db.collection</code></td>
        <td>Specifies the collection from which to retrieve documents.</td>
    </tr>
    <tr>
        <td><code>query</code></td>
        <td>Specifies the criteria for selecting documents using MongoDB's query language.</td>
    </tr>
    <tr>
        <td><code>projection</code></td>
        <td>Specifies which fields to include (1) or exclude (0) in the results.</td>
    </tr>
    <tr>
        <td><code>.sort(sorting)</code></td>
        <td>Specifies the sorting order of the results (1 for ascending, -1 for descending).</td>
    </tr>
    <tr>
        <td><code>.limit(limit)</code></td>
        <td>Limits the number of documents returned.</td>
    </tr>
    <tr>
        <td><code>.skip(skip)</code></td>
        <td>Skips a specified number of documents before returning results.</td>
    </tr>
    <tr>
        <td><code>.collation(collation)</code></td>
        <td>Specifies language-specific rules for string comparison.</td>
    </tr>
    <tr>
        <td><code>.hint(hint)</code></td>
        <td>Forces MongoDB to use a specific index for the query.</td>
    </tr>
    <tr>
        <td><code>.explain(verbosityMode)</code></td>
        <td>Provides detailed information on the query execution plan.</td>
    </tr>
</table>

<h2>MongoDB Query Operators</h2>

<table>
  <tr>
    <th>Operator</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  <tr>
    <td>$eq</td>
    <td>Matches values that are equal to a specified value.</td>
    <td>{ field: { $eq: value } }</td>
  </tr>
  <tr>
    <td>$gt</td>
    <td>Matches values that are greater than a specified value.</td>
    <td>{ field: { $gt: value } }</td>
  </tr>
  <tr>
    <td>$gte</td>
    <td>Matches values that are greater than or equal to a specified value.</td>
    <td>{ field: { $gte: value } }</td>
  </tr>
  <tr>
    <td>$lt</td>
    <td>Matches values that are less than a specified value.</td>
    <td>{ field: { $lt: value } }</td>
  </tr>
  <tr>
    <td>$lte</td>
    <td>Matches values that are less than or equal to a specified value.</td>
    <td>{ field: { $lte: value } }</td>
  </tr>
  <tr>
    <td>$ne</td>
    <td>Matches all values that are not equal to a specified value.</td>
    <td>{ field: { $ne: value } }</td>
  </tr>
  <tr>
    <td>$in</td>
    <td>Matches any of the values specified in an array.</td>
    <td>{ field: { $in: [value1, value2, ...] } }</td>
  </tr>
  <tr>
    <td>$nin</td>
    <td>Matches none of the values specified in an array.</td>
    <td>{ field: { $nin: [value1, value2, ...] } }</td>
  </tr>
  <tr>
    <td>$and</td>
    <td>Joins query clauses with a logical AND.</td>
    <td>{ $and: [ { condition1 }, { condition2 }, ... ] }</td>
  </tr>
  <tr>
    <td>$or</td>
    <td>Joins query clauses with a logical OR.</td>
    <td>{ $or: [ { condition1 }, { condition2 }, ... ] }</td>
  </tr>
  <tr>
    <td>$not</td>
    <td>Inverts the effect of a query expression.</td>
    <td>{ field: { $not: { $eq: value } } }</td>
  </tr>
  <tr>
    <td>$nor</td>
    <td>Joins query clauses with a logical NOR.</td>
    <td>{ $nor: [ { condition1 }, { condition2 }, ... ] }</td>
  </tr>
  <tr>
    <td>$exists</td>
    <td>Matches documents that have the specified field.</td>
    <td>{ field: { $exists: true/false } }</td>
  </tr>
  <tr>
    <td>$type</td>
    <td>Selects documents if a field is of the specified type.</td>
    <td>{ field: { $type: "string" } }</td>
  </tr>
  <tr>
    <td>$all</td>
    <td>Matches arrays that contain all elements specified in the query.</td>
    <td>{ field: { $all: [value1, value2, ...] } }</td>
  </tr>
  <tr>
    <td>$elemMatch</td>
    <td>Matches documents that contain an array field with at least one element matching all the specified query criteria.</td>
    <td>{ field: { $elemMatch: { condition1, condition2, ... } } }</td>
  </tr>
  <tr>
    <td>$size</td>
    <td>Selects documents if the array field is a specified size.</td>
    <td>{ field: { $size: sizeValue } }</td>
  </tr>
  <tr>
    <td>$expr</td>
    <td>Allows the use of aggregation expressions within the query language.</td>
    <td>{ $expr: { $gte: [ "$field1", "$field2" ] } }</td>
  </tr>
  <tr>
    <td>$geoWithin</td>
    <td>Selects documents within a bounding GeoJSON geometry.</td>
    <td>{ field: { $geoWithin: { $geometry: { type: "Polygon", coordinates: [ [ [x1, y1], [x2, y2], ... ] ] } } } }</td>
  </tr>
  <tr>
    <td>$near</td>
    <td>Returns geospatial objects in proximity to a point.</td>
    <td>{ field: { $near: { $geometry: { type: "Point", coordinates: [longitude, latitude] } } } }</td>
  </tr>
  <tr>
    <td>$text</td>
    <td>Performs a text search on the content of fields indexed with a text index.</td>
    <td>{ $text: { $search: "searchString" } }</td>
  </tr>
</table>

<br>
<br>

# MongoDB Aggregation Pipeline

<p align = "justify">
The MongoDB aggregation framework is a powerful tool for performing complex data processing and transformation operations on collections. It uses a pipeline approach, where documents are passed through a series of stages, each performing a specific operation on the data. The aggregation pipeline is a sequence of stages that process documents. Each stage transforms the documents as they pass through the pipeline. The stages can filter, sort, group, reshape, and modify documents.
</p>

## Basic Structure

```javascript
db.collection.aggregate([
    { <stage1>: { <stage-specific-operator>: <arguments> } },
    { <stage2>: { <stage-specific-operator>: <arguments> } },
    ...
])
```

## $match

Preliminary filtering of documents with the aim to pass only those that match the specified condition(s).
Similar to a `find` query.

```javascript
{
  $match: {
    status: "active";
  }
}
```

## $group

<p align = "justify">
Groups documents by a specified key/identifier-expression and apply the accumulator expressions to each group.
The id field is required when performing a grouping operation. You can set it as a specific property of the document
e.g if there is a property named group inside the documents, or set it to null and provide a second grouping pattern to
be implemented from $group.
</p>

```javascript
{ $group: { _id: "$field", total: { $sum: "$amount" } } }
```

## $project

Reshapes each document in the stream, such as by adding, removing, or renaming fields. Works like the 2nd {} inside a `find` query.

```javascript
{ $project: { name: 1, total: 1, status: 1 } }
```

## $sort

Sorts the documents based on the specified fields.

```javascript
{
  $sort: {
    total: -1;
  }
}
```

## $limit

Limits the number of documents passed to the next stage.

```javascript
{
  $limit: 5;
}
```

## $skip

Skips a specified number of documents before passing the remaining documents to the next stage.

```javascript
{
  $skip: 10;
}
```

## $unwind

Deconstructs an array field from the input documents to output a document for each element.

```javascript
{
  $unwind: "$items";
}
```

## $lookup

Performs a left outer join to another collection in the same database.

```javascript
{
    $lookup: {
        from: "otherCollection",
        localField: "localField",
        foreignField: "foreignField",
        as: "newField"
    }
}
```

## $out

Writes the resulting documents of the aggregation pipeline to a specified collection.

```javascript
{
  $out: "newCollection";
}
```

<!-- Aggregation Operators -->
<h2>Aggregation Operators</h2>

<!-- Accumulator Operators (used in $group and other stages) -->
<h3>Accumulator Operators</h3>
<ul>
    <li><strong>$sum:</strong> Returns the sum of numeric values.</li>
    <li><strong>$avg:</strong> Returns the average of numeric values.</li>
    <li><strong>$min:</strong> Returns the minimum value.</li>
    <li><strong>$max:</strong> Returns the maximum value.</li>
    <li><strong>$first:</strong> Returns the first value.</li>
    <li><strong>$last:</strong> Returns the last value.</li>
    <li><strong>$push:</strong> Returns an array of values.</li>
    <li><strong>$addToSet:</strong> Returns an array of unique values.</li>
</ul>

<!-- Array Operators -->
<h3>Array Operators</h3>
<ul>
    <li><strong>$arrayElemAt:</strong> Returns the element at the specified array index.</li>
    <li><strong>$concatArrays:</strong> Concatenates arrays to return a new array.</li>
    <li><strong>$filter:</strong> Selects a subset of the array to return based on the specified condition.</li>
    <li><strong>$size:</strong> Returns the number of elements in an array.</li>
    <li><strong>$slice:</strong> Returns a subset of an array.</li>
</ul>

<!-- Conditional Operators -->
<h3>Conditional Operators</h3>
<ul>
    <li><strong>$cond:</strong> Evaluates a boolean expression to return one of two specified values.</li>
    <li><strong>$ifNull:</strong> Evaluates an expression and returns the value if not null, otherwise returns a specified value.</li>
    <li><strong>$switch:</strong> Evaluates a series of case expressions and returns the first value for which a condition is true.</li>
</ul>

<!-- Date Operators -->
<h3>Date Operators</h3>
<ul>
    <li><strong>$dateToString:</strong> Converts a date object to a string.</li>
    <li><strong>$year, $month, $dayOfMonth, $hour, $minute, $second, $millisecond:</strong> Extracts parts of a date.</li>
</ul>

<!-- String Operators -->
<h3>String Operators</h3>
<ul>
    <li><strong>$concat:</strong> Concatenates strings.</li>
    <li><strong>$substr:</strong> Returns a substring of a string.</li>
    <li><strong>$toLower:</strong> Converts a string to lowercase.</li>
    <li><strong>$toUpper:</strong> Converts a string to uppercase.</li>
</ul>

<!-- Type Conversion Operators -->
<h3>Type Conversion Operators</h3>
<ul>
    <li><strong>$toInt, $toString, $toBool, $toDouble:</strong> Converts a value to the specified type.</li>
</ul>

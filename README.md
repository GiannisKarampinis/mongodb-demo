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

The MongoDB aggregation framework is a powerful tool for performing complex data processing and transformation operations on collections. It uses a pipeline approach, where documents are passed through a series of stages, each performing a specific operation on the data.

## Basic Structure

```javascript
db.collection.aggregate([
    { <stage1>: { <stage-specific-operator>: <arguments> } },
    { <stage2>: { <stage-specific-operator>: <arguments> } },
    ...
])
```

## $match

Filters documents to pass only those that match the specified condition(s).
Similar to a find query.

```javascript
{
  $match: {
    status: "active";
  }
}
```

## $group

Groups documents by a specified key and can perform aggregations on the grouped data.

```javascript
{ $group: { _id: "$field", total: { $sum: "$amount" } } }
```

## $project

Reshapes each document in the stream, such as by adding, removing, or renaming fields.

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

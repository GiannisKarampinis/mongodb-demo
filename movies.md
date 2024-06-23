## MongoDB Atlas Database Queries on sample_mflix Database

### Queries:

1. Display only the title and year for all movies, sorted from oldest to newest and in descending alphabetical order.

   ```mongodb
   db.movies.find( {}, { _id: 0, 'title':1, 'year':1} ).sort({ 'year':1, 'title':-1 })
   ```

2. Display the title, year, and directors for movies released after 2012 with a duration of up to 90 minutes.

   ```mongodb
   db.movies.find(  {year: {$gt: 2012}, runtime:{$lte:90}  }, {_id:0, title:1, year:1, directors:1} )
   ```

3. Display movies that either do not have the "rated" feature or have "rated" with values "unrated" or "passed".

   ```mongodb
   db.movies.find( { $or: [ { rated: {$exists:false} }, {rated: "unrated"}, {rated: "passed"} ]  }, { _id:0, title:1 } )
   ```

   ```mongodb
   db.movies.find({$or: [{rated: {$in: ['passed', 'unrated']}}, {rated: {$exists:false}}]})
   ```

4. Display the title and awards for the top 20 movies with the most comments (num_mflix_comments), sorted in descending order based on comments.

   ```mongodb
   db.movies.find( {}, { _id:0, title: 1, awards: 1, num_mflix_comments: 1} ).sort({ "num_mflix_comments":-1  }).limit(20)
   ```

5. Display details of movies featuring either "Al Pacino" or "Gary Oldman".

   ```mongodb
   db.movies.find( { cast: {$in:['Al Pacino', 'Gary Oldman']}   } , {}  )
   ```

6. Display details of movies categorized as both "Crime" and "Drama".

   ```mongodb
   db.movies.find( { genres: { $all : ['Crime', 'Drama']} } , {} )
   ```

7. Display details of movies featuring "Tom Hanks" but not "Meg Ryan".

   ```mongodb
   db.movies.find( { cast: {$in:['Tom Hanks'] }, cast: { $nin:['Meg Ryan'] } })
   ```

8. Display the count of actors, directors, and writers for each movie.

   ```mongodb
    db.movies.aggregate(
        [
            {
                $project:
                {
                    title:1,
                    _id:0,
                    numActors: { $size: "$cast" },
                    numDirectors: { $size: "$directors" },
                    numWriters: { $cond: { if:
                                    {$isArray:"$writers"},
                                    then: {$size:"$writers"},
                                    else:"$writers"
                                        }
                                }
                }
            }
        ]
    )
   ```

    <p align ="justify">
   \*MongoDB projection is a powerful tool that can be used to extract only the fields you
   need from a document(not all fields).
   For the writers field, a check is performed to determine if it is an array within the JSON. Only then do we retrieve its size; otherwise, if it is a simple field, we simply return its value.
    </p>

9. Display the count, maximum, and minimum duration per movie rating (rated).

   ```mongodb

   ```

10. Display the count of movies that have at least a 3.5 rating from viewers and 5 from critics per year, for years with at least 3 such movies.

    ```mongodb

    ```

11. Display the count and list of movies per country and genre, for pairs that have fewer than 20 movies.

    ```mongodb

    ```

12. Display the count and list of movie titles per genre for movies in which "Edward Norton" has acted.

    ```mongodb

    ```

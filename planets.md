# MongoDB - sample_guides.planets

## Practice with the following queries

1. Planets' names starting from the closest to the Sun to the farthest.

   ```mongodb
    db.planets.find({},{_id:0, name:1}).sort({orderFromSun:1})
   ```

2. Planets with either O2 or N in their atmosphere.

   ```mongodb
    db.planets.find({mainAtmosphere:{$in:['O2','N']}})
   ```

3. Planets with both H2 and He in their atmosphere.

   ```mongodb
    db.planets.find({mainAtmosphere:{$all:['H2','He']}})
   ```

   ```mongodb
    db.planets.find(
        {
            mainAtmosphere:{$in:['H2']},
            mainAtmosphere:{$in:['He']}
        }
    )
   ```

   ```mongodb
   db.planets.find(
       {
         $and:[
            {
                mainAtmosphere:{$in:['H2']}
            },
            {
                mainAtmosphere:{$in:['He']}
            }
         ]
       }
   )
   ```

4. Planets with rings, sorted alphabetically.

   ```mongodb
    db.planets.find({hasRings:true}).sort({name:1})
   ```

5. Planet with the highest maximum surface temperature.

   ```mongodb
    db.planets.find().sort({'surfaceTemperatureC.max':-1}).limit(1)
   ```

   ```mongodb
    db.planets.find({}, {name:1, "surfaceTemperatureC.max":1, _id:0}).sort({'surfaceTemperatureC.max':-1}).limit(1)
   ```

6. Planets without rings or without N in their atmosphere.

   ```mongodb
    db.planets.find({$or:[{hasRings:false}, {mainAtmosphere:{$nin:
   ['N']}}]})
   ```

7. Number of planets with average surface temperature greater than -100.

   ```mongodb
    db.planets.countDocuments({'surfaceTemperatureC.mean':{$gt:-100}})
   ```

   or with an aggregation pipeline:

   ```mongodb
    db.planets.aggregate(
        [
            { $match: { 'surfaceTemperatureC.mean':{$gt:-100} } },
            { $group: {_id:null, counter:{$sum: 1 } } }
        ]
    )
   ```

8. Number of planets and average surface temperature per planetary group (pgroup).

   ```mongodb
   db.planets.aggregate([{$group:{_id:'$pgroup', plithos:{$sum:1},
   avgtemp:{$avg:'$surfaceTemperatureC.mean'}}}])
   ```

9. Number of planets per group that are ranked after the 3rd position from the Sun, sorted in descending order by count.

   ```mongodb
   db.planets.aggregate([{$match:{orderFromSun:{$gt:3}}}, {$group:
   {_id:'$pgroup', plithos:{$sum:1}}}, {$sort:{plithos:-1}}])
   ```

10. Count and list of planets for each element in the atmosphere.

    ```mongodb
    db.planets.aggregate([ { $unwind: "$mainAtmosphere" }, { $group: { _id:"$mainAtmosphere", count: { $sum: 1 }, planets: {$addToSet: '$name' } } } ])
    ```

    ```mongodb
    db.planets.aggregate([{$unwind:{path: '$mainAtmosphere'}}, {$group:{_id:'$mainAtmosphere', plithos:{$sum:1},planets:{$addToSet:'$name'}}}])
    ```

11. Count and list of planets with average surface temperature of at least 14 degrees for each element in the atmosphere present in at least two planets.

    ```mongodb
    db.planets.aggregate([{$match:{'surfaceTemperatureC.mean':{$lte:14}}},
    {$unwind:{path:'$mainAtmosphere'}},{$group:{_id:'$mainAtmosphere',
    plithos:{$sum:1}, planets:{$addToSet:'$name'}}}, {$match:{plithos:
    {$gte:2}}}])
    ```

12. Number of planets per atmosphere element and planetary group.

    ```mongodb
    db.planets.aggregate([{$group:{_id: {'atmo':'$mainAtmosphere', 'pgr':'$pgroup'}, plithos:{$sum:1}, planets:{$addToSet:'$name'}}}])
    ```

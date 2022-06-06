# sequelize

`Sequelize supports the standard associations`

-  One-To-One
-  One-To-Many
-  Many-To-Many

`Sequelize provides four types of associations`

- The HasOne association
- The BelongsTo association
- The HasMany association
- The BelongsToMany association

`Defining the Sequelize associations`

```
const A = sequelize.define('A', /* ... */);
const B = sequelize.define('B', /* ... */);

A.hasOne(B); // A HasOne B
A.belongsTo(B); // A BelongsTo B
A.hasMany(B); // A HasMany B
A.belongsToMany(B, { through: 'C' }); // A BelongsToMany B through the junction table C
```

They all accept an options object as a second parameter (optional for the first three, mandatory for belongsToMany containing at least the through property):
```
A.hasOne(B, { /* options */ });
A.belongsTo(B, { /* options */ });
A.hasMany(B, { /* options */ });
A.belongsToMany(B, { through: 'C', /* options */ });
```

# Creating the standard relationships
- To create a One-To-One relationship, the hasOne and belongsTo associations are used together;
- To create a One-To-Many relationship, the hasMany and belongsTo associations are used together;
- To create a Many-To-Many relationship, two belongsToMany calls are used together.

`Note: there is also a Super Many-To-Many relationship,`

setup a One-To-One relationship between them such that Bar gets a fooId column.

```
Foo.hasOne(Bar);
Bar.belongsTo(Foo);

```
```
CREATE TABLE IF NOT EXISTS "foos" (
  /* ... */
);
CREATE TABLE IF NOT EXISTS "bars" (
  /* ... */
  "fooId" INTEGER REFERENCES "foos" ("id") ON DELETE SET NULL ON UPDATE CASCADE
  /* ... */
);
```

For example, to configure the ON DELETE and ON UPDATE behaviors, you can do:

```
Foo.hasOne(Bar, {
  onDelete: 'RESTRICT',
  onUpdate: 'RESTRICT'
});
Bar.belongsTo(Foo);
```

# One-To-Many relationships
```
Team.hasMany(Player);
Player.belongsTo(Team);
```

```
CREATE TABLE IF NOT EXISTS "Teams" (
  /* ... */
);
CREATE TABLE IF NOT EXISTS "Players" (
  /* ... */
  "TeamId" INTEGER REFERENCES "Teams" ("id") ON DELETE SET NULL ON UPDATE CASCADE,
  /* ... */
);
```

`Like One-To-One relationships, ON DELETE defaults to SET NULL and ON UPDATE defaults to CASCADE.`

# Many-To-Many relationships

Many-To-Many associations connect one source with multiple targets, while all these targets can in turn be connected to other sources beyond the first.

```
const Movie = sequelize.define('Movie', { name: DataTypes.STRING });
const Actor = sequelize.define('Actor', { name: DataTypes.STRING });
Movie.belongsToMany(Actor, { through: 'ActorMovies' });
Actor.belongsToMany(Movie, { through: 'ActorMovies' });
```

```
CREATE TABLE IF NOT EXISTS "ActorMovies" (
  "createdAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  "updatedAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  "MovieId" INTEGER REFERENCES "Movies" ("id") ON DELETE CASCADE ON UPDATE CASCADE,
  "ActorId" INTEGER REFERENCES "Actors" ("id") ON DELETE CASCADE ON UPDATE CASCADE,
  PRIMARY KEY ("MovieId","ActorId")
);
```

```
const awesomeCaptain = await Captain.findOne({
  where: {
    name: "Jack Sparrow"
  }
});
// Do stuff with the fetched captain
console.log('Name:', awesomeCaptain.name);
console.log('Skill Level:', awesomeCaptain.skillLevel);
// Now we want information about his ship!
const hisShip = await awesomeCaptain.getShip();
// Do stuff with the ship
console.log('Ship Name:', hisShip.name);
console.log('Amount of Sails:', hisShip.amountOfSails);
```


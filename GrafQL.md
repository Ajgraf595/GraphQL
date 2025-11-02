
# GraphQL Exercise (Pronounced Graf)
*(queries intentionally shuffled, with playful aliases, fragments, and harmless quirks — all still valid GraphQL)*

**Playground Link:** [Star Wars GraphQL (SWAPI)](https://star-wars-sb.netlify.app)
This link you use to get to the actual activity
1. delete what is in the box
2. copy and paste each Query separately to test


> **How to use this file explicitly**  
> 1) Paste each query into the **left panel** of the SWAPI GraphiQL playground.  
> 2) Run with **Cmd/Ctrl + Enter**.  
> 3) Copy the JSON from the **right panel** into the “Response” blocks for your submission.

---

## A. Starships First (because why not?)

### Query (3 starships — using an alias and an extra field for clarity)
```graphql
{
  firstThree: allStarships(first: 3) {
    starships {
      name
      model
      __typename # harmless: returns the type name
    }
    totalCount
  }
}
```

### Response (paste yours)
```json
// your JSON here
```

---

## B. Characters + Their Starships (with a nested alias)

### Query
```graphql
{
  allPeople(first: 5) {
    people {
      pilotName: name # aliasing name
      starshipConnection {
        ships: starships {
          name
        }
      }
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## C. Films… but with an alias on the root field

### Query (list all film titles)
```graphql
{
  movies: allFilms {
    films {
      title
    }
    totalCount
  }
}
```

### Response
```json
// your JSON here
```

---

## D. A Specific Character (Luke) — plus id for proof

### Query
```graphql
{
  person(id: "cGVvcGxlOjE=") {
    name
    id
  }
}
```

### Response
```json
// your JSON here
```

---

## E. Five Planets (odd spacing + comments, still valid!)

### Query
```graphql
{
  allPlanets(   first:    5   ) {   # weird spacing is fine
    planets {
      name  # only the name here
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## F. Species + Languages (with a typo comment that doesn’t matter)

### Query
```graphql
{
  allSpecies(first: 5) {
    species {
      name
      language # "Galactic Basic", etc.
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## G. Planets + Climates (requesting list field order doesn’t matter)

### Query
```graphql
{
  allPlanets(first: 5) {
    planets {
      climates
      name
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## H. Vehicles + Cost (3 vehicles)

### Query
```graphql
{
  allVehicles(first: 3) {
    vehicles {
      name
      costInCredits
    }
    totalCount
  }
}
```

### Response
```json
// your JSON here
```

---

## I. Characters in a Film (A New Hope) — show just names

### Query
```graphql
{
  film(id: "ZmlsbXM6MQ==") {
    title
    characterConnection {
      characters {
        name
      }
      totalCount
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## J. Multi‑Film Characters (filter later by totalCount > 1)

### Query
```graphql
{
  allPeople {
    people {
      name
      filmConnection {
        totalCount
      }
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## K. Aggregate Film Stats (count only)

### Query
```graphql
{
  allFilms {
    totalCount
  }
}
```

### Response
```json
// your JSON here
```

---

## L. Full Character Profile (fragment demo + homeworld)

### Query
```graphql
fragment PersonCore on Person {
  name
  birthYear
  homeworld { name }
}

{
  person(id: "cGVvcGxlOjE=") {
    ...PersonCore
    starshipConnection { starships { name } }
    filmConnection     { films     { title } }
  }
}
```

### Response
```json
// your JSON here
```

---

## M. Characters + Homeworld Populations (first 5)

### Query
```graphql
{
  allPeople(first: 5) {
    people {
      name
      homeworld {
        name
        population
      }
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## N. Vehicles, Their Pilots, and Pilots’ Species (first 3)

### Query
```graphql
{
  allVehicles(first: 3) {
    vehicles {
      name
      pilotConnection {
        pilots {
          name
          species { name }
        }
      }
    }
  }
}
```

### Response
```json
// your JSON here
```

---

## O. Films and Their Associated Entities (first 3 films)

### Query
```graphql
{
  allFilms(first: 3) {
    films {
      title
      characterConnection { characters { name } }
      planetConnection    { planets   { name } }
      starshipConnection  { starships { name } }
    }
  }
}
```

### Response
```json
// your JSON here
```

---

### ✅ Notes
- **Aliases** like `movies:` or `pilotName:` only change the key name in the response — the data is the same.  
- **Comments** (`# like this`) and odd **whitespace** won’t affect execution.  
- **Fragments** (`fragment PersonCore on Person`) keep things DRY and readable.  
- Run each query separately (one at a time) in the editor.
 // Start of Selection
# TD 1: MongoDB

## Queries and Outputs

### 2.1 
**Requête:**
```javascript
db.grades.findOne();
db.zips.findOne();
```

**Nombre de résultats:** 1

**Output:** 

```json
{
  "_id": ObjectId("50b59cd75bed76f46522c34e"),
  "student_id": 0,
  "class_id": 2,
  "scores": [
    {
      "type": "exam",
      "score": 57.92947112575566
    },
    {
      "type": "quiz",
      "score": 21.24542588206755
    },
    {
      "type": "homework",
      "score": 68.1956781058743
    },
    {
      "type": "homework",
      "score": 67.95019716560351
    },
    {
      "type": "homework",
      "score": 18.81037253352722
    }
  ]
}
```

```json
{
  "_id": "01001",
  "city": "AGAWAM",
  "loc": [
    -72.622739,
    42.070206
  ],
  "pop": 15338,
  "state": "MA"
}
```

### 2.2
**Requête:**
```javascript
db.grades.find({});
```

**Nombre de résultats:** 280

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c361"),
  "student_id": 3,
  "class_id": 10,
  "scores": [
    {
      "type": "exam",
      "score": 35.47946463550763
    },
    {
      "type": "quiz",
      "score": 94.14222652833352
    },
    {
      "type": "homework",
      "score": 58.43343860077279
    },
    {
      "type": "homework",
      "score": 66.83562834109681
    }
  ]
}
```

### 2.3
**Requête:**
```javascript
db.grades.countDocuments();
```

**Nombre de résultats:** 280

### 2.4
**Requête:**
```javascript
db.grades.find({ class_id: 20 });
```

**Nombre de résultats:** 7

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c45e"),
  "student_id": 46,
  "class_id": 20,
  "scores": [
    {
      "type": "exam",
      "score": 27.79390777259294
    },
    {
      "type": "quiz",
      "score": 29.18509374453628
    },
    {
      "type": "homework",
      "score": 59.51122184508205
    },
    {
      "type": "homework",
      "score": 74.05819778852317
    },
    {
      "type": "homework",
      "score": 86.91457200027877
    }
  ]
}
```

### 2.5
**Requête:**
```javascript
db.grades.find({ class_id: { $lte: 20 } });
```

**Nombre de résultats:** 188

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c36d"),
  "student_id": 4,
  "class_id": 8,
  "scores": [
    {
      "type": "exam",
      "score": 60.13912489935064
    },
    {
      "type": "quiz",
      "score": 16.49453097445802
    },
    {
      "type": "homework",
      "score": 20.64686745448644
    },
    {
      "type": "homework",
      "score": 72.03200074025955
    },
    {
      "type": "homework",
      "score": 23.97256438707867
    }
  ]
}
```

### 2.6
**Requête:**
```javascript
db.grades.find({ 
  $expr: { 
    $gte: ["$student_id", "$class_id"] 
  } 
});
```

**Nombre de résultats:** 188

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c3a6"),
  "student_id": 15,
  "class_id": 0,
  "scores": [
    {
      "type": "exam",
      "score": 84.22482529114681
    },
    {
      "type": "quiz",
      "score": 68.51195197931716
    },
    {
      "type": "homework",
      "score": 48.135589104224
    }
  ]
}
```

### 2.7
**Requête:**
```javascript
db.grades.find({ 
  class_id: { 
    $lte: 20, 
    $gte: 10 
  } 
});
db.grades.find({ 
  $expr: { 
    $and: [
      { $gte: [ "$class_id", 10 ] }, 
      { $lte: [ "$class_id", 20 ] }
    ] 
  } 
});
```

**Nombre de résultats:** 100

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c383"),
  "student_id": 8,
  "class_id": 11,
  "scores": [
    {
      "type": "exam",
      "score": 89.12537830331416
    },
    {
      "type": "quiz",
      "score": 11.48939533818351
    },
    {
      "type": "homework",
      "score": 16.96585149869495
    },
    {
      "type": "homework",
      "score": 17.8760904208101
    },
    {
      "type": "homework",
      "score": 80.93286662099982
    },
    {
      "type": "homework",
      "score": 28.93004389653184
    }
  ]
}
```

### 2.8
**Requête:**
```javascript
db.grades.find({}, { 
  "ue": "$class_id", 
  "etu": "$student_id", 
  "_id": 0 
});
```

**Nombre de résultats:** 280

**Output:** 
```json
{
  "ue": 10,
  "etu": 3
}
```

### 3.1
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $project: {
      somme: { $add: [ "$class_id", "$student_id" ] },
      class_id: 1,
      student_id: 1
    }
  }
]);
```

**Nombre de résultats:** 280

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c361"),
  "student_id": 3,
  "class_id": 10,
  "somme": 13
}
```

### 3.2
**Requête:**
```javascript
db.zips.aggregate([
  { 
    $match: { 
      pop: { $gte: 10000 } 
    } 
  }
]);
```

**Nombre de résultats:** 7634

**Output:** 
```json
{
  "_id": "01109",
  "city": "SPRINGFIELD",
  "loc": [
    -72.554349,
    42.114455
  ],
  "pop": 32635,
  "state": "MA"
}
```

### 3.3
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $sort: { 
      class_id: 1, 
      student_id: 1 
    } 
  }
]);
```

**Nombre de résultats:** 280

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c3dd"),
  "student_id": 25,
  "class_id": 2,
  "scores": [
    {
      "type": "exam",
      "score": 39.8052260869232
    },
    {
      "type": "quiz",
      "score": 85.59336208703981
    },
    {
      "type": "homework",
      "score": 16.3016460205172
    },
    {
      "type": "homework",
      "score": 4.62963742991297
    }
  ]
}
```

### 3.4
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $unwind: "$scores" 
  }
]);
```

**Nombre de résultats:** 1241

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c352"),
  "student_id": 0,
  "class_id": 24,
  "scores": {
    "type": "homework",
    "score": 86.79352850434199
  }
}
```

### 3.5
**Requête:**
```javascript
db.zips.aggregate([
  { 
    $group: {
      _id: "$city",
      minpop: { $min: "$pop" }
    } 
  }
]);
```

**Nombre de résultats:** 16584

**Output:** 
```json
{
  "_id": "ROCIADA",
  "minpop": 480
}
```

### 3.6
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $lookup: {
      from: "zips", 
      localField: "student_id", 
      foreignField: "pop",
      as: "zipsdocs"
    } 
  }
]);
```

**Nombre de résultats:** 280

**Output:** 
```json
{
  "_id": ObjectId("50b59cd75bed76f46522c361"),
  "student_id": 3,
  "class_id": 10,
  "scores": [
    {
      "type": "exam",
      "score": 35.47946463550763
    },
    {
      "type": "quiz",
      "score": 94.14222652833352
    },
    {
      "type": "homework",
      "score": 58.43343860077279
    },
    {
      "type": "homework",
      "score": 66.83562834109681
    }
  ],
  "zipsdocs": [
    {
      "_id": "04570",
      "city": "SQUIRREL ISLAND",
      "loc": [
        -69.630974,
        43.809031
      ],
      "pop": 3,
      "state": "ME"
    },
    {
      "_id": "60604",
      "city": "CHICAGO",
      "loc": [
        -87.632999,
        41.87845
      ],
      "pop": 3,
      "state": "IL"
    },
    {
      "_id": "99692",
      "city": "DUTCH HARBOR",
      "loc": [
        -167.510656,
        53.362757
      ],
      "pop": 3,
      "state": "AK"
    }
  ]
}
```

### 4.1
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $unwind: "$scores" 
  },
  { 
    $group: {
      _id: "$scores.type",
      nombre: { $sum: 1 }
    } 
  }
]);
```

**Nombre de résultats:** 3

**Output:** 
```json
{
  "_id": "exam",
  "nombre": 280
}
{
  "_id": "quiz",
  "nombre": 280
}
{
  "_id": "homework",
  "nombre": 681
}
```

### 4.2
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $unwind: "$scores" 
  },
  { 
    $match: { "scores.type": "exam" } 
  },
  { 
    $group: {
      _id: "$class_id",
      meilleure: { $max: "$scores.score" }
    } 
  }
]);
```

**Nombre de résultats:** 31

**Output:** 
```json
{
  "_id": 5,
  "meilleure": 88.22950674232497
}
```

### 4.3
**Requête:**
```javascript
db.zips.aggregate([
  { 
    $group: {
      _id: { city: "$city", state: "$state" },
      total: { $sum: "$pop" }
    } 
  },
  { 
    $sort: { total: -1 } 
  },
  { 
    $limit: 10 
  },
  { 
    $project: {
      city: "$_id.city",
      state: "$_id.state",
      total: 1
    } 
  }
]);
```

**Nombre de résultats:** 10

**Output:** 
```json
{
  "_id": {
    "city": "DALLAS",
    "state": "TX"
  },
  "total": 940191,
  "city": "DALLAS",
  "state": "TX"
}
```

### 4.4
**Requête:**
```javascript
db.zips.aggregate([
  { 
    $group: {
      _id: { city: "$city", state: "$state" },
      popcity: { $sum: "$pop" }
    } 
  },
  { 
    $group: {
      _id: "$_id.state",
      popmoy: { $avg: "$popcity" }
    } 
  }
]);
```

**Nombre de résultats:** 51

**Output:** 
```json
{
  "_id": "NM",
  "popmoy": 5872.360465116279
}
```

### 4.5
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $unwind: "$scores" 
  },
  { 
    $match: { 
      "scores.type": "exam",
      "scores.score": { $gte: 50.0 }
    } 
  },
  { 
    $group: {
      _id: "$class_id",
      students: { $push: "$student_id" }
    } 
  }
]);
```

**Nombre de résultats:** 31

**Output:** 
```json
{
  "_id": 11,
  "students": [
    0,
    3,
    8,
    12,
    14,
    23,
    44
  ]
}
```

### 4.6
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $unwind: "$scores" 
  },
  { 
    $group: {
      _id: { 
        class_id: "$class_id",
        student_id: "$student_id",
        type: "$scores.type"
      },
      moy: { $avg: "$scores.score" }
    } 
  },
  { 
    $group: {
      _id: { 
        class_id: "$_id.class_id", 
        student_id: "$_id.student_id" 
      }, 
      note: { $avg: "$moy" }
    } 
  }
]);
```

**Nombre de résultats:** 280

**Output:** 
```json
{
  "_id": {
    "class_id": 22,
    "student_id": 15
  },
  "note": 45.88060866381033
}
```

### 4.7
**Requête:**
```javascript
db.grades.aggregate([
  { 
    $unwind: "$scores" 
  },
  { 
    $group: {
      _id: { 
        class_id: "$class_id",
        type: "$scores.type"
      },
      moy: { $avg: "$scores.score" }
    } 
  },
  { 
    $group: {
      _id: "$_id.class_id",
      meilleure_moy: { $max: "$moy" },
      moy_types: { $push: { type: "$_id.type", moy: "$moy" } }
    } 
  },
  { 
    $unwind: "$moy_types" 
  },
  { 
    $match: { 
      $expr: { 
        $eq: [ "$meilleure_moy", "$moy_types.moy" ] 
      } 
    } 
  },
  { 
    $project: {
      class_id: "$_id",
      epreuve_mieux_reussie: "$moy_types.type"
    } 
  }
]);
```

**Nombre de résultats:** 31

**Output:** 
```json
{
  "_id": 14,
  "class_id": 14,
  "epreuve_mieux_reussie": "exam"
}
```

# TD 2: MapReduce

## Outputs

### 2. Mono processeur
**Code:**
```python
def word_count_single_processor(data_lines):
    """
    Counts word occurrences using a single processor.
    Measures and returns the time taken.
    """
    start_time = time.time()
    word_counts = Counter()
    
    for line in data_lines:
        words = line.split()
        word_counts.update(words)
    
    end_time = time.time()
    elapsed_time = end_time - start_time
    return word_counts, elapsed_time
```

**Single-Processor Time Taken:** 8.4327 seconds

### 3.Multi-processeurs

**Map function:**
```python
def map_function(text_chunk):
    """Fonction de map : retourne un dictionnaire des fréquences de mots pour le morceau de texte."""
    word_freq = {}
    for word in text_chunk.split():
        if word in word_freq:
            word_freq[word] += 1
        else:
            word_freq[word] = 1
    return word_freq
```

**Reduce function:**
```python
def reduce_function(counter_a, counter_b):
    """Reduce function: merges two word count dictionaries by summing counts."""
    for word, count in counter_b.items():
        if word in counter_a:
            counter_a[word] += count
        else:
            counter_a[word] = count
    return counter_a
```

**Average time taken with 2 processors on 5 runs:** 10.245 +/- 0.477 seconds

**Average time taken with 3 processors on 5 runs:** 9.321 +/- 0.110 seconds

**Average time taken with 4 processors on 5 runs:** 8.863 +/- 0.262 seconds

(**Average time taken with 1 processors on 5 runs:** 10.374 +/- 0.159 seconds)

### 4. Visualisation

![image](images/Distribution%20of%20Total%20Execution%20Time%20vs.%20Number%20of%20Processes.png)

![image](images/Distribution%20of%20Chunking,%20Mapping,%20and%20Reducing%20Times%20vs.%20Number%20of%20Processes.png)

Le multi-processing diminue légèrement le temps total d'exécution par rapport à l'exécution séquentielle. Avec 1 processus, le temps moyen est autour de 10,5 s. En augmentant le nombre de processus (2 à 4), une légère réduction est observée, atteignant environ 9 s avec 4 processus. L'amélioration reste modérée et dépend du coût de gestion des processus parallèles.

### 5. Conclusion

**Avantages de MapReduce**
- **Scalabilité** : Permet de traiter de grandes données en les divisant en tâches indépendantes.
- **Tolérance aux pannes** : Réessaie uniquement les tâches échouées.
- **Équilibrage de charge** : Répartit les tâches pour une meilleure utilisation des ressources.
- **Simplicité** : Structure claire avec les phases chunking, mapping et reducing.

Bien que MapReduce facilite le traitement distribué, les gains de performance restent limités pour certaines tâches peu complexes.

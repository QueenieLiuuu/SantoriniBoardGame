# Santorini

### Dependency
```
Java 16+
npm/yarn up-to-date
```

### How to run
```
1. mvn test
2. mvn spring-boot:run
3. cd src/react/santorini
4. yarn start / npm start (both works)
5. open localhost:3000 in your browser, then enjoy!
```

### Game Content
1. We support all basic gods. Note that if you are new, you can start from "Man".
![Santorini1](https://github.com/QueenieLiuuu/SantoriniBoardGame/blob/master/santorini1.png)

2. Clean and easy-to-use UI. On the left-bottom there are buttons for god powers.  
e.g. Hermes is very free so he can choose move/build/pass.
![Santorini2](https://github.com/QueenieLiuuu/SantoriniBoardGame/blob/master/santorini2.png)

3. The number on the cell shows the level, "X" means a dome. Right part are infomations and 
   Undo/Redo buttons (very smooth).
![Santorini3](https://github.com/QueenieLiuuu/SantoriniBoardGame/blob/master/santorini3.png)

4. Finally we got a winner.
![Santorini4](https://github.com/QueenieLiuuu/SantoriniBoardGame/blob/master/santorini4.png)

#### God cards:
Apollo, Artemis, Athena, Atlas, Demeter, Hephaestus, Hermes, Minotaur, Pan, Prometheus

#### Undo:
For undo/redo functions, I need to maintain a list of immutable contexts. When undo, the program 
go back along the contexts and restore to previous states. Since a context is like a dataframe 
that contains all the detailed information, we could undo/redo perfectly.

To make the context immutable, I set the Context class final, and all fields final. Then I 
deleted all setters. For convenience, especially for unit-tests, I did not make the getters 
return copied objects. Since there are limited amount of APIs, so the half-immutable model is 
not likely to leak. Instead, I write a copy() function for all models and it's a deep copy. 

When I generate the context for next timeframe, I certainly not pass the reference of the fields.
Instead, I deep copy all nested fields and carefully solved recursion.

Thus, each context is independent and immutable.

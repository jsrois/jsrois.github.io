---
title: 'Afterdojo: the Args kata'
---

Yesterday we had another Coding Dojo. This started some months ago as a preparation for a TDD course and has became a regular thing. Until now, we practiced refactoring and TDD with _classic_ katas (`FizzBuzz`, `Parrot`), but this one was a freer, more open thing.

The `Args` kata put us in the position of designing and implementing a small system from scratch, and, still, it can be challenging. In _The Coding Dojo Handbook_, Emily Bache _destaca
This time I'm approaching this kata as a way of applying Outside-In TDD and also to

"test-infected" (Kent Beck)

Goals (apart from solving the kata):
- Acceptance Tests and outside-in TDD.
- Mocking with python3
	- mocks are 1st class citizens (unittest)

Other Achievements:
- python `re` package 
- Turns out empty strings are `Falsy` in python ! (see below for details)

### Discussing the problem

We all make command-line apps from time to time. Even if you are running a web service, you might be running `./server.py -p 8080 --logs /tmp/log.txt`. And we all know that, when building an application, command line arguments is the more prone to change and fragile part. Fortunately, we have tools like `Apache Commons CLI` or Python's  `argparse` to do the job. Still, parsing arguments is a problem most developers can relate to. 

Discussion, modelling the problem, nouns in kata description.

Without entering in too many details, let's say that we agree to define two types of parameters: for instance, when calling our app the following way:

```
./application_server.py -d -l /var/lib/application/log.txt -p 8080
```

Can you spot the two types of parameters? In this example, `-l` and `-p` are _valued_ parameters (they take, respectively, `/var/lib/application/log.txt` and `8080` as values), while `-d` is a _flag_ parameter (e.g. it may activate a `debug` mode in our application).

##### Default values

At this point of the, one of the concepts emerging in the discussion (because remember, we haven't even started coding!) is the need for declaring default values for the parameters in the schema. Do we want default values? Let's think of a `-b` valued parameter. One option is to make it mandatory to introduce 
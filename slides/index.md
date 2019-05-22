- title : Level Up with Generative Testing
- description : Adding generative testing to your repertoire.
- author : Shane Charles
- theme : night
- transition : default

***

### Level Up with Generative Testing 


***

### Thank You

![Sponsors](images/sponsorlogos.png)

***
<!-- .slide: class="two-floating-elements" -->
### About me

<div class="two-floating-elements">
<img src="images/mvp_logo_vertical.png" alt="mvp" style="height:145px;border:0;margin: auto;"/>
    <ul>
     <li>Shane Charles</li>
<li>White Light Computing, Inc.</li>
<li>Functional programming enthusiast</li>
<li>Board member for Full Stack MB</li>
</ul>
</div>




    type ContactType = | Twitter | Blog | GitHub

    let getContactInfo = function
      | Twitter -> "@dead_stroke"
      | Blog    -> "https://geekeh.com"
      | GitHub  -> "shanecharles"

***

### Our Path

- Generative testing
- Property based testing 
- Stateful testing
- Testing in the wild
- Wrap up

***

### Generative Testing

- Property based testing
- Stateful testing (Model based testing)
- Random testing
  - Fuzzing 

***
### What does generative testing look like?

    open FsCheck

    let Addition_commutative_property (x: int, y: int) =
      x + y = y + x


---
### Python

    [lang=python]
    from hypothesis import given
    from hypothesis.strategies import integers
    
    @given(integers(), integers())
    def test_addition_commutative_property(x, y):
        assert x + y == y + x


---
### Clojure


    [lang=clojure]
    (require '[clojure.test.check :as tc])
    (require '[clojure.test.check.generators :as gen])
    (require '[clojure.test.check.properties :as prop])

    (def addition_commutative_property
      (prop/for-all [v (gen/tuple gen/int gen/int)]
       (let [x (first v)
             y (second v)]
        (= (+ x y) (+ y x)))))

  
---
### C#

    [lang=c#]
    using Xunit;
    using FsCheck.Xunit;

    namespace PropertyTests
    {
      public class AdditionProperties
      {
        [Property(EndSize = 1000)]
        public void Addition_commutative_property(int x, int y)
        {
          Assert.Equal(x + y, y + x);
        }
      }
    }


***
### Why should we?

- Actively looks for undiscovered bugs
- Requires deeper understanding of domain
  - Sets of inputs and outputs vs example based
- Generates inputs/sequences we wouldn't
- Help avoid Pesticide Paradox

---
### But we can generate random data in
### {unit testing framework}?

- Shrinking

---
#### Shrinking sounds slow?

- No
- Yes
- It depends
- It's worth it

***

### When should we?

- Mission critical functions
- Complex solutions
  - Lots of input variations
- APIs
- End to end testing

***

### Test not

- Overly simple
- Minimal input variation
- Language primitives

***



### Property Based Testing

> Given a subset of inputs, there exists a property which dictates a subset of outputs.

---
### Property Patterns

- There and back
- Somethings never change
- Different path same destination
- Test oracle
- Hard to prove, easy to verify

---
### To some code

***

### Stateful Testing / Model based testing


---
### What do we do

- Create model
 - Simplified representation
- Execute actions
 - Model
 - System
- Check for divergence

***

### Real world situation

- Worker uses RFID tag for identification
- Screen prompts available actions for shift
- Actions: 
  - Start floor
  - End floor
  - Start break
  - End break

***

### Finite State Machine

![fsm](images/finitestatemachine1.png)

***

### More code

***

### Divergence Problems

- System under test
- Model
- Both above
- Specification

***
### Further inspection

![fsm2](images/finitestatemachine2.png)

---
### Missing state

![fsm3](images/finitestatemachine3.png)

***
### Question

Who thinks they can benefit from generative testing?

---
### Quviq QuickCheck

![Autosar](images/autosar.png)
![Partners](images/autosar-partners.jpg)

---
### What they found

- Specification errors
- Incompatibilities
- Priority rollover

---
### Jepsen.io

- Testing distributed systems
- Exercise database CAP constraints
 - Consistency
 - Availability
 - Partition tolerant (network)

---
### Jepsen found 

- MongoDB
 - 2013: Major loss of data
 - 2015: Dirty reads and some data loss
- Elasticsearch
 - ~34% data loss
- Redis
 - ~56% write loss
- RabbitMQ, Cassandra, etcd, etc.

***
### Summary

- Generative testing works

***

### Thank You

    type ContactType = | Twitter | Blog | GitHub

    let getContactInfo = function
      | Twitter -> "@dead_stroke"
      | Blog    -> "https://geekeh.com"
      | GitHub  -> "shanecharles"

***

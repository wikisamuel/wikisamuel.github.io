# TP3 : Java++
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* Use of advanced OOP concepts
* Enums
* Containers
* Exceptions
* Creation and comparison of simple Artifical Intelligences (AI)

This is not a brand new practical work. The main goal is to stabilize your Java knowledge.

Some leftovers from practical work 2 are back. Let's code some AI !

----

## COVID-19 Warning
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* Due to the COVID-19, the exam will not take place at school. This practical work will be evaluated.
* You have to produce one project per student, and export it as an archive file. See further instructions on Moodle.
* To get a good grade, you are expected to do the *sidequests*. The *bonus* and *going deeper* parts are for the best students.

----

## Starting point
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* For this session we will start from our previous works. 
* Start by grabing the code from [https://github.com/wikisamuel/wikisamuel.github.io/raw/master/java/TP2-baseTP3.zip](https://github.com/wikisamuel/wikisamuel.github.io/raw/master/java/TP2-baseTP3.zip)   
* Eclipse can import the project using "File => Import => General => Existing projects into Workspace" feature
* Take some time to make sure you understand the code and what it is doing. Feel obviously free to ask questions about it

----

## 1. Species enumeration
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
At this point, species are created at runtime within the main function.  
Supposing species are immutable and that no new species can be created, the code would be a lot more readable and simple if we created them once and for all
* Using an Enum, rework the code to clearly instantiate all available species
* Enjoy how smaller the main function now is and how everything is a lot more clear

----

## 2. Lot of stuff
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  

_Some of you might already have done this work during the last session using a List. This is slightly different this time, but you can still reuse part of your work._

To implement the inventory, we need the appropriate data structure 
* Which data structure would you use ?
* Add a data structure implementing the [Set](https://docs.oracle.com/javase/7/docs/api/java/util/Set.html) interface to Inventory
* Inside main, add some items to the player's inventory
* Add a totalPrice() method to this inventory. It returns the total price of all items contained in the inventory
* Inside main, once it's filled, display the total price of the inventory
* Sidequest : rewrite Inventory's [toString()](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#toString--) method to display the list of all item owned
* Sidequest : rewrite the getLevelFromXp() method inside Level class

----

## 3. Lot of stuff (Brand new !)
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  

* The inventory now has a limited space (10 items). Adding an item to a full inventory fails and the user should be informed of that.
* Sidequest : create a Pokedex class that will keep track of all species that the player has met. For each species, we need to know if the player has encountered it, fought it or never encountered it.

----

## 4. More action
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  

_Some of you might already have done this work during the last session. Feel free to reuse it._

Before writing AIs, we need to add more depth to fights
* Pokemons can now defend. Add a defense score (between 0 and 90). This will be the percentage of damage that will be mitigated on each attack  
* Write a defend() method that increases the defense score by 10 (up to a maximum of 90)
* The logic for damage dealt change slightly. It is now : attacker's strength * (1 - target's defense score / 100). Every attack deals at least 1 damage.  
* Simulate a fight in which one of the pokemon defends for 3 turns 

----

## 5. Special powers
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  

* We want to add special powers to our Pokemons. Special powers are not associated with species (i.e. two Pokemons from the same specie could have different special powers). A Pokemon could have 0 to several special powers.
* Special powers are *strong* : a strong Pokemon is able to trigger an earthquake (it displays *Brrr* to the console) ; *clever* : a clever Pokemon can solve an equation (it displays *x+2=4* to the console), and *beautiful* : a beautiful Pokemon can charm other Pokemons (it displays *Hey !* to the console).
* Define a StrongCleverBulbasaur class : a StrongCleverBulbasaur is a kind of Pokemon which Specie is Bulbasaur.
* Define 3 interfaces for various types of special powers.
* Make StrongCleverBulbasaur have the strong and clever special powers. Implement relevant methods.
* Define BeautifulCleverCharmander the same way.

----

## (bonus) 6. AI may be the future (part 1)
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  

_Some of you might already have done this work during the last session. Feel free to reuse it._

Let's write some very basic AI that will be able to decide the best move each time
* Create an AI implementation wich acts as follow : the "brute" one constantly attacks
* Test your AI creating a Pokemon fight
* Create a second AI implementation : the "vicious" one that defends until it reachs 90 defense and then attacks
* Make the 2 AI fight using the pokemons you want

----

## (bonus) 6. AI may be the future (part 2)

_Some of you might already have done this work during the last session. Feel free to reuse it._

* What do both AI implementations have in common ? Define the signature of an AI method
* Create the corresponding AI interface and make both AI implement it
* Create a third implementation using your own algorithm
* Sidequest : write an AI tournament. They compete against each other. Each won fight (using generated pokemon data) scores 1 point for the winning AI


----

## Going deeper
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" --> 
 
* Checkout the code from Olivier Levitt's repository [https://bitbucket.org/olevitt/formations/src/master/poo-java/TPs/TP2/](https://bitbucket.org/olevitt/formations/src/master/poo-java/TPs/TP2/) . You will find a full correction for the second practical work (TP2). Copy the "IAGeniale" class and make it fight your own AI. Improve your own AI until it beats "IAGeniale" (which, in reality, is not that geniale)
* Using you new knowledge on arrays, investigate the infamous String[] args in main parameters
* (Going a whole lot deeper) : generate a large amount of data "hpPokemon1, strengthPokemon1, defensePokemon1,hpPokemon2, strengthPokemon2, defensePokemon2, action => fight's result". Using a statistical method of your choice or deep learning on this data, create an AI. Make it compete with other AIs.
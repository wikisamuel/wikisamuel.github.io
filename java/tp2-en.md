# TP2 : OOP like a boss
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* Use of advanced OOP concepts
* New various features for the application 
* Creation and comparison of simple AIs

----

## Starting point
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* For this practical work, we will start from where we ended last week
* You can either use your code from last week or download a correction from this git repository :  
[https://github.com/wikisamuel/wikisamuel.github.io/raw/master/java/TP1.zip](https://github.com/wikisamuel/wikisamuel.github.io/raw/master/java/TP1.zip)  
* Eclipse can import the project using "File => Import => General => Existing projects into Workspace" feature
* Take some time to make sure you understand the code and what it is doing. Feel obviously free to ask questions about it

----

## 1. Cleanup
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* During practical work 1, all attributes where defined as public. What issues do you think this choice may lead to ?

Using as much IDE's power as we can,<br />we are going to refactor the code to respect encapsulation,<br />i.e. for all classes :
* Make the relevant attributes private
* Write getters and setters
* Define useful constructors (if needed)
* Change the Main class accordingly

----

## 2. Items (part 1)
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
* Pokemons will now be able to use various kinds of items. All items have a name and a price (the price it costs at the pokeshop) and a usage type (either permanent, one use or unusable)  
* Sweets are items 
* By default, all items have the following String representation : "name (price pokedollars)"

----

## 2. Items (part 2)
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->   
* Pokeballs also are items. A pokeball has a base efficiency (an integer between 0 and 100) and a efficiency multiplier which depends on its type. 
* Simple pokeballs do not exist. A pokeball is always special. 2 types of pokeballs currently exist : ultraball (with a multiplier of 2) and greatball (with a multiplier of 3)  
* For all pokeballs, we need to know the real efficiency which is calculated as follows : base efficiency * multiplier

----

## 3. Inventory
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
The player now has access to an inventory    
* Create an empty Inventory class. Inventory will soon contain the list of all items the player currently have.
* Create a Player class with an Inventory attribute. In this game, there will always be only one Player. This player should be accessible from anywhere in the application. The player won't change during gameplay.  

----

## 4. Lot of stuff
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
To implement the inventory, we need the appropriate data structure 
* Take a look at List interface : [https://docs.oracle.com/javase/8/docs/api/java/util/List.html](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)  
* Take a look at ArrayList class (implementation) : [https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)  
* Add a list of items to the Inventory class
* Within the main function, add some items to the player's inventory 
* Add a totalPrice() method to this inventory. It returns the total price of all items contained in the inventory
* Inside main, once it's filled, display the total price of the inventory
* Sidequest : rewrite Inventory's [toString()](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#toString--) method to display the list of all item owned
* Sidequest : notice there are other List implementations :[https://docs.oracle.com/javase/tutorial/collections/implementations/list.html](https://docs.oracle.com/javase/tutorial/collections/implementations/list.html)

----

## (bonus) 5. More action
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
Before writing AIs, we need to add more depth to fights
* Pokemons can now defend. Add a defense score (between 0 and 90). This will be the percentage of damage that will be mitigated on each attack  
* Write a defend() method that increases the defense score by 10 (up to a maximum of 90)
* The logic for damage dealt change slightly. It is now : attacker's strength * (1 - target's defense score / 100). Every attack deals at least 1 damage.  
* Simulate a fight in which one of the pokemon defends for 3 turns

----

## (bonus) 6. AI may be the future (part 1)
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
Let's write some very basic AI that will be able to decide the best move each time
* Create an AI implementation wich acts as follow : the "brute" one constantly attacks
* Test your AI creating a Pokemon fight
* Create a second AI implementation : the "vicious" one that defends until it reachs 90 defense and then attacks
* Make the 2 AI fight using the pokemons you want

----

## (bonus) 6. AI may be the future (part 2)

* What do both AI implementations have in common ? Define the signature of an AI method
* Create the corresponding AI interface and make both AI implement it
* Create a third implementation using your own algorithm
* Sidequest : write an AI tournament. They compete against each other. Each won fight (using generated pokemon data) scores 1 point for the winning AI

----

## Going deeper
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" --> 

[https://bitbucket.org/olevitt/formations/src/master/poo-java/TPs/TP2/](https://bitbucket.org/olevitt/formations/src/master/poo-java/TPs/TP2/)  
* Checkout the code from Olivier Levitt's repository [https://bitbucket.org/olevitt/formations/src/master/poo-java/TPs/TP2/](https://bitbucket.org/olevitt/formations/src/master/poo-java/TPs/TP2/) . You will find a correction for this practical work (TP2). Copy the "IAGeniale" class and make it fight your own AI. Improve your own AI until it beats "IAGeniale" (which, in reality, is not that geniale)
* Make your AI compete against other AI in the room
* (Going a whole lot deeper) : generate a large amount of data "state of pokemon1, state of pokemon2, action => fight's result". Using deep learning on this data, create an AI. Make it compete with other AIs
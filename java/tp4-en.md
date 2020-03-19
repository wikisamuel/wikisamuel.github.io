# TP4 : a real project
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* Using Maven, adding dependencies
* Unit testing
* Run SQL requests against a DB
* Run a webserver

----

## Starting point
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
* For this session we will start from a light version of previous works.
* It's about the same as a finished TP3 except IAs implementations.
* Please use this specific version even if you completed TP3.
* Start by grabing the code from [TODO-PutUrlHere](TODO-PutUrlHere)  
* Import the project into eclipse.

----

## COVID-19 Warning
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->
Two steps of this practical session will change wether you are doing it from an Ensai VM or your personal computer. This is the first one.

* In order to use maven, it may be necessary to configure the network proxy if you are using an Ensai VM. Instructions are available on Moodle : [http://foad.ensai.fr/course/view.php?id=31](http://foad.ensai.fr/course/view.php?id=31)
* Some students using a shared connection on a campus might have a similar issue, unfortunately we cannot guess in advance what is their specific proxy address and port. Google "check proxy" with your Operating System name and version might help to find a procedure to get them. Then customize the file on Moodle with those pieces of information.
* In order to know where to put this settings.xml file if you don't use a VM, go to Eclipse > Window > Preferences > Maven > User Settings, then put the file at the relevant location and hit the "Update Settings" button

----

## 1. Mavenisation
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
Maven will give us a lot of power but we first need to set it up.  

* Right click on your Java project > configure > convert to Maven Project.
* Look at you pom.xml file, and the tree in your explorer
* Run the app
* Sidequest : use maven to compile and generate a JAR

----

## 2. Unit testing
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
* Add [JUnit (5.6.0)](https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api/5.6.0) dependency
* Write and run a unit test that will check that the attack() method deals the right amount of damage (The spec was defined in TP3 : "The logic for damage dealt change slightly. It is now : attacker's strength * (1 - target's defense score / 100). Every attack deals at least 1 damage")  
* Detect and correct the algorithm's error
* Sidequest : browse to you local maven repository and open the junit JAR to see what's inside

----

## 3. JDBC
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
JDBC (Java DataBase Connectivity) is a Java standard for interacting with a relational database (whatever its type).  

* The way you use JDBC and the code you write doesn't depend on the database management system (DBMS) you are using (PostgreSQL, SQLite, Oracle, Sqlserver).  
* You are free to use whatever DBMS you want. We suggest you use either the database provided by Ensai (PostgreSQL) if you are working on a VM, or SQlite which stores data locally inside a file if you are working on your personal computer.

----

## 3.1 : PostgreSQL configuration
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
If you are working on an Ensai VM, you can choose to connect to your PostgreSQL database.  
<b>Database info</b> :  
Host sgbd-eleves.domensai.ecole
Port 5432  
Database idX9876 (replace with your own id)  
User idX9876 (replace with your own id)  
Password idX9876 (replace with your own id)  
  
<b>The PostgreSQL JDBC driver</b> :  
https://mvnrepository.com/artifact/org.postgresql/postgresql/42.2.11

URL JDBC : jdbc:postgresql://hote/database?user=...&password=...

----

## 3.2 : SQLite configuration
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
If you are working on your personal computer, you have to use SQLite.

SQLite stores the data inside a single file (it can also store it in memory), so you only need the SQLite JDBC driver :  
https://mvnrepository.com/artifact/org.xerial/sqlite-jdbc/3.30.1

URL JDBC : jdbc:sqlite:C:/path/to/the/db/base.db

----

## 4. Hello SQL
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
```Java
String url = "jdbc:postgresql://hote/database?user=...&password=...";
//String url = "jdbc:sqlite:C:/chemin/vers/la/base/base.db";
Connection connection = DriverManager.getConnection(url);
```
This code will open a connection with the database.  
Once you have an open connection, you can execute queries :   
```Java
PreparedStatement ps = connection.prepareStatement("CREATE TABLE pokemon(id INT PRIMARY KEY)");
ps.executeUpdate();
```
```Java
PreparedStatement ps = connection.prepareStatement("INSERT INTO pokemon(id) VALUES(?)");
ps.setInt(1,42);
ps.executeUpdate();
```
```Java
PreparedStatement ps = connection.prepareStatement("SELECT * FROM pokemon");
ResultSet result = ps.executeQuery();
```
https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html

----

## 5. Enjoy DB
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
* When the application starts, insert some Pokemon data into the database
* During fights, keep an history of each action made
* Handle errors (exceptions) when the database is unreachable or the query is invalid

----

## (bonus) 6. AI may be the future (part 1)
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  

_If you haven't done it in previous sessions, implement some IA logic._

Let's write some very basic AI that will be able to decide the best move each time
* Create an AI implementation wich acts as follow : the "brute" one constantly attacks
* Test your AI creating a Pokemon fight
* Create a second AI implementation : the "vicious" one that defends until it reachs 90 defense and then attacks
* Make the 2 AI fight using the pokemons you want

----

## (bonus) 6. AI may be the future (part 2)

_If you haven't done it in previous sessions, implement some IA logic._

* What do both AI implementations have in common ? Define the signature of an AI method
* Create the corresponding AI interface and make both AI implement it
* Create a third implementation using your own algorithm
* Sidequest : write an AI tournament. They compete against each other. Each won fight (using generated pokemon data) scores 1 point for the winning AI


----

## (bonus) 7. A webserver
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" -->  
* Using [Javalin](https://javalin.io/), write a webserver 
* On /pokemon, display the list of pokemons stored in the database
* On /fight, start a fight and display the result. Display the whole fight's history


----

## Going deeper
<!-- .slide: data-state="no-toc-progress" class="no-toc-progress" --> 
* Using [Maven shade plugin](https://maven.apache.org/plugins/maven-shade-plugin/examples/executable-jar.html), create a runnable JAR file. Run it without using eclipse
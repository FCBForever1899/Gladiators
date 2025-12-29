package games;

import java.util.ArrayList;

import edu.rutgers.cs112.BST.BSTNode;

/**
 * This class contains methods to represent a Coliseum in Gladiators.
 * It manages cities, people, and the duel process.
 * 
 * @author Kal Pandit
 * @author Maksims Kurjanovics Kravcenko
 * @author Pranay Roni
 */
public class Coliseum {

    private ArrayList<City> cities; // all cities in Gladiators.
    private BSTNode<City> game; // root of the BST. The BST contains cities that are still in the game. 

    /**
     * Default constructor, initializes an empty list of cities.
     */
    public Coliseum() {
        cities = new ArrayList<>();
        game = null; 
    }

    /**
     * Sets up Gladiators, the universe in which the duels takes place.
     * Reads cities and people from the input file.
     * 
     * @param filename will be provided by client to read from using StdIn
     */
    public void setupGladiators(String filename) {
        StdIn.setFile(filename); // open the file - done only once here
        setupCities();
        setupPeople();
    }

    /**
     * Reads the following from input file:
     * - Number of cities
     * - city IDs
     * Add cities into the cities ArrayList in order of appearance. 
     */
    public void setupCities() {
        // WRITE YOUR CODE HERE 
        int n = StdIn.readInt(); //declare n variable to read integers in file
        
        int e = 0;  //declare e variable as integer reader in file
        while (e<n){    //while e is less than n
            e++;    //increment e to read next integer
            int cityID = StdIn.readInt();   //cityID is the variable read
            City city = new City(cityID);   //set up city object
            cities.add(city);   //add city
        }
        


    }

    /**
     * Reads the following from input file:
     * Number of people
     * Space-separated: first name, last name, birth month (1-12), age, city id, effectiveness 
     * 
     * You should add each person to the corresponding city based on their city id.
     * If the person's birth month is odd, add to oddPopulation, else add to evenPopulation.
     */
    public void setupPeople() { 
        // WRITE YOUR CODE HERE
        int n = StdIn.readInt(); //read integers of line
        for (int i = 0; i < n; i++){   //increment through the lies
            
            String firstName = StdIn.readString();    //index 0 in line is firstName
            String lastName = StdIn.readString();     //index 1 in line is lastName
            //for (int j = 2; j <p.length; j++){
                //String[] c = StdIn.readLine().split(null);
                //int age = c[3];
           // int [] ints = new int[p.length + 2];    //fastforward to ints, starting in index 2
            //for (int c = 0; c <= p.length + 2; ){
            int birthMonth = StdIn.readInt();  //index 0 for ints is birthMonth
            int age = StdIn.readInt(); //index 1 for ints is age
            int cityID = StdIn.readInt();//index 2 for ints is cityID
            int effectiveness = StdIn.readInt();   //index 3 for ints is effectiveness
            //}
            Person person = new Person(firstName, lastName, birthMonth, age, cityID, effectiveness);    //create person object
            
            for (int z = 0; z < cities.size(); z++){
                //City city = cities.get(cityID);          
                  //if the cityID's match
                  if (cities.get(z).getCityNumber() == cityID){
                    if (birthMonth % 2 == 0){   //if the person's birth month is even, add to even population
                            
                        cities.get(z).addEvenPerson(person);
                    } else {                                //else if the person's birh month is odd, add to odd population
                        cities.get(z).addOddPerson(person);
                        
                    }
                  }
                
            }
            
                
                
            
            
            //}
        }
 
    }

    /**
     * Adds a city to the game BST.
     * If the city is already added, do nothing
     *  
     * @param newCity the city we wish to add
     */
public void addCityToGame(City newCity) {
    // WRITE YOUR CODE HERE
    //for (int i = 0; i < cities.size(); i++){
        //cities[i] = cityID;
        //game = new BSTNode<City>(newCity);
    
        BSTNode<City> parentNode = new BSTNode<City>(newCity);
        //BSTNode<City> childNode = new BSTNode<City>(newCity);
        
        if (game == null){
        //game = new BSTNode<City>(newCity);
        game = parentNode;
    } else {
        BSTNode<City> ptr = game;
        while (ptr != null){
            if (ptr.getData().getCityNumber() > newCity.getCityNumber()){
                if (ptr.getLeft()==null){
                    ptr.setLeft(parentNode);
                    //childNode.setLeft(ptr);
                    return;
                } else {
                    ptr = ptr.getLeft();
                    
                }
            } else //if (ptr.getData().getCityNumber() > newCity.getCityNumber()){
                if (ptr.getRight()==null){
                    ptr.setRight(parentNode);
                    //childNode.setRight(ptr);
                    return;
                } else {
                    ptr = ptr.getRight();
                    
                }
        

            // } else {
            //     return;
            // }
        }
    //}
    }

        
        
       
        
        
        //BSTNode <City> root = game;
        //int rootValue = game.getCityNumber();
        //int cityID = newCity.getCityNumber();
        
        // while (ptr != null){
        //     parentNode = ptr;
        //     //int ptrValue = ptr.getData().getCityNumber();
        //     //int cityID = newCity.getCityNumber();
        //     if (newCity.getCityNumber() > ptr.getData().getCityNumber()){
        //         // if (ptr.getRight() == null){
        //         //     ptr.setRight(ptr);
        //         // } else {
        //             ptr = ptr.getRight();
        //         //}
        //     } else {
        //         // if (ptr.getLeft() == null){
        //         //     ptr.setLeft(ptr);
        //         // } else {
        //             ptr = ptr.getLeft();
        //         //}
        //         return;
        //     }
        //     if (newCity.getCityNumber() > parentNode.getData().getCityNumber()){
        //         parentNode.setRight(ptr);
        //     } else {
        //         parentNode.setRight(ptr);
        //     }
        // }
 
    }

    /**
     * Searches for a city inside of the BST given the city id.
     * 
     * @param id the city to search
     * @return the city if found, null if not found
     */
    public City findCity(int id) {
        // WRITE YOUR CODE HERE
        //City city = new City((id));
        //BSTNode<City> parentNode = new BSTNode<City>(city);
        //City targetCity = new City(id);
        //int targetID = targetCity.getCityNumber();
        BSTNode <City> ptr = game;

        while (id != ptr.getData().getCityNumber()){
            
            if (id > ptr.getData().getCityNumber()){
               
                if (ptr.getRight() == null){
                    return null;
                }
                 ptr = ptr.getRight();
            } else {
                
                if (ptr.getLeft() == null){
                    return null;
                }
                ptr = ptr.getLeft();
            }
            
        }



        return ptr.getData(); // Replace this line, it is provided so the code compiles
    }

   
    /**
     * Selects two duelers from the tree, according to a series of selection rules.
     * View the assignment description for exact implementation details.
     * 
     * @return the pair of dueler retrieved from this method.
     */
    public DuelPair selectDuelers() {
        // WRITE YOUR CODE HERE

        DuelPair duelPair = new DuelPair();
        int [] oddCity = new int[] {-1};
        int [] evenCity = new int[] {-1};
        
        oddYoungWarrior(game, duelPair, oddCity);
        evenYoungWarrior(game, duelPair, oddCity[0], evenCity);
        
        if (duelPair.getPerson1() == null){
            oddRandomWarrior(game, duelPair, evenCity[0], oddCity);
        }

        if (duelPair.getPerson2() == null){
            evenRandomWarrior(game, duelPair, oddCity[0], evenCity);
        }

        

        return duelPair; // Replace this line, it is provided so the code compiles
    }

    public Person oddYoungWarrior (BSTNode<City> cityNode, DuelPair duelPair, int[] oddCity){
        if (cityNode == null || duelPair.getPerson1() != null){
            return null;
        }
        //boolean x = false; //check for break point from recursive loop

        
        City city = cityNode.getData();

        if (city != null) {
            ArrayList<Person> oddPopulation = city.getOddPopulation();

            for (int e = 0; e < oddPopulation.size(); e++){
                Person person1 = oddPopulation.get(e);
                if (person1.isYoungWarrior()){
                    duelPair.setPerson1(person1);
                    oddPopulation.remove(e);
                    oddCity[0] = city.getCityNumber();
                    return person1;
                }
                //min variable, add to duelPair, get element at first index

                
            }
        }
        if (duelPair.getPerson1() == null){
            Person person1 = oddYoungWarrior(cityNode.getLeft(), duelPair, oddCity);
            if (person1 == null){
                return oddYoungWarrior(cityNode.getRight(), duelPair, oddCity);
            } else {
                return person1;
            }

        } else {
            return null;
        }

        // if (duelPair.getPerson1() == null) {
        //     oddYoungWarrior(cityNode.getLeft(), duelPair, oddCity);
        // }

        
        
    }

    public Person evenYoungWarrior (BSTNode<City> cityNode, DuelPair duelPair, int noCity, int[] evenCity){
        if (cityNode == null || duelPair.getPerson2() != null){
            return null;
        }
        City city = cityNode.getData();

        if (city != null && city.getCityNumber() != noCity){

            ArrayList <Person> evenPopulation = city.getEvenPopulation();

            for (int e = 0; e < evenPopulation.size() && duelPair.getPerson2() == null; e++){
                Person person2 = evenPopulation.get(e);
                if (person2.isYoungWarrior()){
                    duelPair.setPerson2(person2);
                    evenPopulation.remove(e);
                    evenCity[0] = city.getCityNumber();
                    return person2;
                }
            }
        }

        if (duelPair.getPerson2() == null){
            Person person2 = evenYoungWarrior(cityNode.getLeft(), duelPair, noCity, evenCity);
            if (person2 == null){
                return evenYoungWarrior(cityNode.getRight(), duelPair, noCity, evenCity);
            } else {
                return person2;
            }
        } else {
            return null;
        }
        
        // if (duelPair.getPerson2() == null){
        //     evenYoungWarrior(cityNode.getLeft(), duelPair, noCity, evenCity);
        // } 
        // if (duelPair.getPerson2() == null){
        //     evenYoungWarrior(cityNode.getRight(), duelPair, noCity, evenCity);
        // }
    }

    public Person oddRandomWarrior (BSTNode<City> cityNode, DuelPair duelPair, int noCity, int[]oddCity){

        if (cityNode == null || duelPair.getPerson1() != null){
            return null;
        }
        City city = cityNode.getData();
        if (city != null && duelPair.getPerson1() == null && city.getCityNumber() != noCity ){
            ArrayList<Person> oddPopulation = city.getOddPopulation();
            if (!oddPopulation.isEmpty()){
                int i = StdRandom.uniform(oddPopulation.size());
                Person person1 = oddPopulation.remove(i);
                duelPair.setPerson1(person1);
                oddCity[0] = city.getCityNumber();
            }
        }

        // if (duelPair.getPerson1() == null){
        //     oddRandomWarrior(cityNode.getLeft(), duelPair, noCity, oddCity);
        // }
        // if (duelPair.getPerson2() == null){
        //     oddRandomWarrior(cityNode.getRight(), duelPair, noCity, oddCity);
        // }
        
        
        if (duelPair.getPerson1() == null) {
            Person person1 = oddRandomWarrior(cityNode.getLeft(), duelPair, noCity, oddCity);
            if (person1 == null){
                return oddRandomWarrior(cityNode.getRight(), duelPair, noCity, oddCity);
            } else {
                return person1;
            }
        } else {
            return null;
        }

        
    }

    public Person evenRandomWarrior (BSTNode<City> cityNode, DuelPair duelPair, int noCity, int[]evenCity){
        if (cityNode == null || duelPair.getPerson2() != null){
            return null;
        }
        City city = cityNode.getData();
        if (city != null && city.getCityNumber() != noCity && duelPair.getPerson2() == null){
            ArrayList<Person> evenPopulation = city.getEvenPopulation();
            if (!evenPopulation.isEmpty()){
                int i = StdRandom.uniform(evenPopulation.size());
                Person person2 = evenPopulation.remove(i);
                duelPair.setPerson2(person2);
                evenCity[0] = city.getCityNumber();
            }

        }

        
        if (duelPair.getPerson2() == null) {
            Person person2 = evenRandomWarrior(cityNode.getLeft(), duelPair, noCity, evenCity);
            if (person2 == null){
                return evenRandomWarrior(cityNode.getRight(), duelPair, noCity, evenCity);
            } else {
                return person2;
            }
        } else {
            return null;
        }

    
    }

    /**
     * Removes a city from the BST given the city id.
     * 
     * @param id the city to eliminate
     */
    public void eliminateCity(int id) {
        // WRITE YOUR CODE HERE
        
        game = delete(game, id);
        

        // BSTNode<City> ptr = game;
        // BSTNode<City> ptrParent = null;

        // if (ptr == null){
        //     return;
        // }

        
        // while (id != ptr.getData().getCityNumber()){
        //     //ptrParent = ptr;
        //     //System.out.println(ptr.getData().getCityNumber());
        //     if (id > ptr.getData().getCityNumber()){
        //         ptr.setRight(ptr.);
        //     } else if (id < ptr.getData().getCityNumber()){
        //         ptr = ptr.getLeft();
        //     }
        // }

        

        // if (ptr.getLeft() == null && ptr.getRight() == null){ //if ptr had no children
        //     if (ptr == game){   //if ptr the root (game)
        //          game = null;    //set ptr to null 
        //     } else if (ptrParent.getLeft() == ptr){
        //         ptrParent.setLeft(null);
        //     } else {
        //         ptrParent.setRight(null);
        //     }   
               

        // } else if (ptr.getLeft() == null || ptr.getRight() == null){
        //     BSTNode<City> ptrChild = ptr.getRight();
        //     if (ptrChild == null){
        //         ptrChild = ptr.getLeft();
        //     }
        //      if (ptrParent.getLeft() == ptr){
                
        //         ptrParent.setLeft(ptrChild);
               
        //     } else if (ptrParent.getRight() == ptr){
        //         ptrParent.setRight(ptrChild);
        //     } 
        // }else {
        //         BSTNode<City> successorNode = new BSTNode<City>(ptr.getData());
        //         successorNode.setLeft(ptr.getLeft());
        //         successorNode.setRight(ptr.getRight());
        //         BSTNode<City> successorNodeChild= successorNode.getRight();
        //         while (successorNodeChild.getLeft() != null){
        //             successorNode = successorNodeChild;
        //             successorNodeChild = successorNode.getLeft();
                    
                        
        //         }
        //         if (successorNode.getData() == ptr.getData()){
        //             successorNodeChild.setLeft(ptr.getLeft());

        //         } else {
        //             successorNode.setLeft(successorNodeChild.getRight());

        //             successorNodeChild.setLeft(ptr.getLeft());
        //             successorNodeChild.setRight(ptr.getRight());
        //         }

        //         if(ptr == game){
        //             game = successorNodeChild;
        //         }
        //         else if (ptrParent.getLeft() == ptr){
        //             ptrParent.setLeft(successorNodeChild);
        //         } else {
        //             ptrParent.setRight(successorNodeChild);
        //         }
                
        //     }
        
        //BSTNode<City> successorNode = new BSTNode<City>(ptr.getData());
        //return successorNode;
        
        

        


    }

    private BSTNode<City> delete(BSTNode<City> game, int id){
        BSTNode<City> ptr = game;
        //BSTNode<City> ptrParent = null;

    if (ptr == null){
        return null;
    }    



    //ptrParent = ptr;
    //System.out.println(ptr.getData().getCityNumber());
        if (id > ptr.getData().getCityNumber()){
            ptr.setRight(delete(ptr.getRight(), id));
        } else if (id < ptr.getData().getCityNumber()){
            ptr.setLeft(delete(ptr.getLeft(),id));
        } else {
            if (ptr.getLeft() == null && ptr.getRight() == null){ //if ptr had no children
                return null;
            } else if (ptr.getLeft() == null){
                return ptr.getRight();
            } else if (ptr.getRight() == null) {
    

                return ptr.getLeft();
            } else {
                BSTNode<City> successorNode = ptr.getRight();
                while (successorNode.getLeft() != null){
                    successorNode = successorNode.getLeft();
                    // City ptrCity = ptr.getData();
                    // City successorCity = successorNode.getData();
                    // ptrCity.setCityNumber(successorCity.getCityNumber());
                    // ptrCity.setOddPopulation(new ArrayList<>(successorCity.getOddPopulation()));
                    // ptrCity.setEvenPopulation(new ArrayList<>(successorCity.getEvenPopulation()));
                    // ptr.setRight(delete(ptr.getRight(), ptrCity.getCityNumber()));
                }
                City ptrCity = ptr.getData();
                City successorCity = successorNode.getData();
                ptrCity.setCityNumber(successorCity.getCityNumber());
                ptrCity.setOddPopulation(new ArrayList<>(successorCity.getOddPopulation()));
                ptrCity.setEvenPopulation(new ArrayList<>(successorCity.getEvenPopulation()));
                ptr.setRight(delete(ptr.getRight(), ptrCity.getCityNumber()));

    


    
    
    
}

}





return ptr;

}

       

    /**
     * Eliminates a dueler from a pair of duelers.
     * - Both duelers in the DuelPair argument given will duel
     * - Winner gets added back to their city
     * - If a cities odd OR even population is empty, eliminate it from the game 
     * 
     * @param pair of persons to fight each other.
     */
    public void eliminateDueler(DuelPair pair) {
        // WRITE YOUR CODE HERE
        Person person1 = pair.getPerson1();
        Person person2 = pair.getPerson2();
        if (pair.getPerson1() == null && pair.getPerson2() == null){
            return;
        }
        
        if (pair.getPerson1() == null || pair.getPerson2() == null){
            Person soloDueler = person1;
            if (soloDueler == null){
                soloDueler = person2;
            }
            if (soloDueler != null){
                City city = findCity(soloDueler.getCityNumber());
                if (city != null){
                    if (soloDueler.getBirthMonth() % 2 == 0){
                        city.getEvenPopulation().add(soloDueler);
                    } else {
                        city.getOddPopulation().add(soloDueler);
                    }
                }
            }
            return;
           
        } 
        Person winner = person1.duel(person2);
        Person loser;
        if (winner == person1){
            loser = person2;
        } else {
            loser = person1;
        }

        City cityOfWinner = findCity(winner.getCityNumber());
        City cityOfLoser = findCity(loser.getCityNumber());

        if (cityOfWinner != null){
            if (winner.getBirthMonth() % 2 == 0){
                cityOfWinner.getEvenPopulation().add(winner);
            } else {
                cityOfWinner.getOddPopulation().add(winner);
            }
        } 

        if (cityOfLoser != null){
            
            cityOfLoser.getEvenPopulation().remove(loser);
             
            cityOfLoser.getOddPopulation().remove(loser);
            
        }


        if (cityOfWinner != null){
            if (cityOfWinner.getOddPopulation().isEmpty() || cityOfWinner.getEvenPopulation().isEmpty()){
                eliminateCity(cityOfWinner.getCityNumber());
            }
        }

        if (cityOfLoser != null){
            if (cityOfLoser.getEvenPopulation().isEmpty() || cityOfLoser.getOddPopulation().isEmpty()){
            eliminateCity(cityOfLoser.getCityNumber());
        }
        }
        
            
        

    }

    /**
     * ***** DO NOT REMOVE OR UPDATE this method *********
     * 
     * Obtains the list of cities for the Driver.
     * 
     * @return the ArrayList of cities for selection
     */
    public ArrayList<City> getCities() {
        return this.cities;
    }

    /**
     * ***** DO NOT REMOVE OR UPDATE this method *********
     * 
     * Returns the root of the BST
     */
    public BSTNode<City> getRoot() {
        return game;
    }
}

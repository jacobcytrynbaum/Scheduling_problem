//This class reads in a file with student class information, builds a graph of classes, and greedily makes a exam schedule.
//There is a method to create a vector of exam slots which calls on a method to create each tree in the vector, 
//which calls on a method to determine adjacency.
//This further can print the overall exam schedule and each student’s individual schedule

import structure5.*;
import java.util.Scanner;
import java.util.Iterator;
class Scheduler {
 private Scanner scanny;
 private Graph<String, String> classes;                     //graph for all the classes
 private Vector<BinarySearchTree<String>> slots = new Vector<BinarySearchTree<String>>(); //BST for the time slots
 private OrderedVector<Student> theSchool = new OrderedVector<Student>(); //ordered vector for all the students
 
 // Run the program
 public static void main(String[] args){
  Scheduler examiner = new Scheduler(args[0]); //call the constructor
  examiner.Slotter();                          //create all the exam slots
  examiner.examSchedule();                     //print the exam schedule
  examiner.studentSchedules();                 //print each student’s schedule
 }
 
 //pre: filename is valid
 //This constructs the graph of classes and reads in all the student-class information
 public Scheduler(String filename){
  Assert.pre(filename != null, "filename is null");
  FileStream input = new FileStream(filename);
  classes = new GraphListUndirected<String, String>();
  scanny = new Scanner(input); //use the scanner on the file
  while(scanny.hasNext()){
  String name = scanny.nextLine(); //get the name of the student
  Student testee = new Student(name); //make a new student who is taking tests
  for(int i = 0; i<4; i++){
   String theClass = scanny.nextLine();
   testee.add(theClass); //add each class to Student object
   classes.add(theClass); //add each class to the graph
  }
  theSchool.add(testee); //add to the list of students in the school
  for(int k = 0; k<testee.getCount()-1; k++){
   for(int j = (k+1); j<testee.getCount(); j++){
    classes.addEdge(testee.getClass(k), testee.getClass(j), null); //loop through, adding an edge between each combination of a student’s classes
   }
  }
 }
 //System.out.println(classes.toString());  // print out the entire graph. Used only as a test
 }


  // Creates the next slot (a tree) and adds it to the vector of slots
 public void Slotter(){
  Assert.pre(classes.size()>0, "nothing to slot");
  int counter = classes.size();
  while(counter>0){
   BinarySearchTree<String> nextTree = this.buildNext(classes); //call buildnext to get the next tree
   slots.add(nextTree); //add the tree
   counter = counter - nextTree.size(); // decrement the counter until it is zero, at which point I am done moving all classes into slots
 }
}


 //Creates a slot in the form of a tree and passes it back to the slotter
 public BinarySearchTree<String> buildNext(Graph<String, String> remaining){
  Assert.pre(!remaining.isEmpty(), "graph is empty, can’t make another slot");
  BinarySearchTree<String> tree = new BinarySearchTree<String>(); //new tree
  Iterator it = remaining.iterator(); //iterate through the graph
  while(it.hasNext()){
   String nextClass = it.next().toString(); //get the next class
    if(!this.isAdjacent(nextClass, tree) && !classes.isVisited(nextClass)){
    tree.add(nextClass);
    classes.visit(nextClass); //add the class to the tree and visit the
    class in the graph
   }
  }
 return tree;
 }
 
 
 //returns whether or not a vertex is adjacent to anything in the rest of a tree
 public boolean isAdjacent(String vertex, BinarySearchTree<String> currentSlot){
  Iterator checker = currentSlot.iterator();
  while(checker.hasNext()){
   if(classes.containsEdge(vertex, checker.next().toString())){ //if the graph has an edge between the vertex and anything in the tree already, return true
   return true;
  }
 }
 return false;
 }
 
 
 //prints out each student’s schedule, slots start at 1 instead of 0
 public void studentSchedules(){
  System.out.println("");
  Iterator<Student> schedules = theSchool.iterator(); //iterate though my ordered vector of students
  while(schedules.hasNext()){
   Student nextKiddo = schedules.next();
   System.out.println(nextKiddo.getName()); //print out the student
   for(int i = 0; i < nextKiddo.getCount(); i++){
    String nextClass = nextKiddo.getClass(i); //get the next class
    for( int j = 0; j < slots.size(); j++){
     if(slots.get(j).contains(nextClass)){ //find that class in the corresponding slot
      System.out.println("Slot " + (j+1) + ": " + nextClass);
      break;
     }
    }
   }
  }
 }

 //print the exame schedule
 public void examSchedule(){
  System.out.println("Exam Schedule");
  for(int p = 0; p < slots.size(); p++){
   System.out.println("");
   BinarySearchTree<String> slot = slots.get(p); //get a time slot
   Iterator<String> classIt = slot.iterator();
   System.out.print( "Slot " + (p+1) + ": " ); //print slot number starting at 1
   while(classIt.hasNext()){ //iterate over the slot
    System.out.print(classIt.next() + " ");
   }
  }
 }
}

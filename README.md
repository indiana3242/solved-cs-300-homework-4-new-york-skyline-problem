Download Link: https://assignmentchef.com/product/solved-cs-300-homework-4-new-york-skyline-problem
<br>
The İstanbul skyline problem, often mistakenly called the New York skyline problem, is the problem of drawing the skyline of a city given a set of buildings of that city. In this homework you will write a program whose input is a list of the locations and sizes of buildings, and whose output is a description of the visible skyline, that is, how the city looks as an outline, when viewed from a distance.   For a real-life version of this problem, go to Vaniköy on the Asian side of the Bosphorus, and, as you sip your tea, contemplate on how the skyline will look as the sun sets over the European side.

To make things simple, the buildings will be given using just two dimensions, x and y, rather than three, ignoring the depth value. (Think of x as horizontal and y as vertical.) Each building will be a rectangle with its base on the x-axis. Thus, a building can be completely described by giving the x-coordinates of its left and right sides, and the y coordinate (or height) of its top side. The input will be read from standard input. The first line of the input indicates how many buildings there are in the city, and each succeeding line will indicate the x-coordinate of the left side of a building followed by the ycoordinate of the top side of the building, followed by the x-coordinate of the right side of the building.  The following is an example of a valid input to the program:

4

2 50 10

35 20 55

30 60 45

5 75 25

Notice that buildings may overlap. For example, the first building, which spans 2 through 10 on the x-axis, overlaps the fourth building, which spans 5 through 25 on the x-axis. If the right x-coordinate of a building is the same as the left x-coordinate of another building, then the two buildings are considered to be side by side (though their heights may differ!)

The output of this program should be a description of the skyline of the city. The skyline is the upper outline of the buildings in the city. To be more precise, the skyline is a function that maps each x-coordinate to the y-coordinate of the tallest building that covers that x-coordinate. Since all of our buildings are rectangles, this function will be a curve consisting of horizontal and vertical line segments. Your program should describe the skyline function by listing each x coordinate at which the height of the skyline changes, along with the new coordinate of the skyline at that x. Your program should do this in the direction of increasing x coordinate (i.e., left to right). For example, the following output describes the skyline of the input above:

0 0

2 50

5 75

25 0

30 60

45 20

55 0

This output indicates that initially the skyline is at height 0 (which may be different if there is a building starting at 0). At x-coordinate 2, the height of the skyline becomes 50. The height remains 50 until x-coordinate 5, at which point (because of the fourth building) it becomes 75. Then, at x-coordinate 25 the height becomes 0, and so forth.  The following figure depicts this instance of the problem where the buildings are shown with rectangles and the skyline is shown with the think outline.

<h1>1   The Modified Priority Queue Class</h1>

The first part of this assignment is to implement a class that we will call a “Modified Priority Queue,” (MPQ) that will be useful in computing the skyline of a set of buildings. The MPQ is a simple variation on the priority queue class that we used heaps to implement. The only difference is that the items that are maintained by a MPQ object internally have two components (say <em>value</em> and <em>label</em>), as opposed to just a value that is used to compare the items in a priority queue.  The first component is again a value with which the items can be compared to each other just as in a priority queue.  The other, <em>label</em>, is an identifying number that identifies a specific item in the MPQ.  Thus for instance you can insert an item and either access or delete an item with the maximum value component or with a specific identifying number.




Your class definition should at least have the following method that could be useful for the rest of the homework.




<ul>

 <li>Constructor</li>

 <li>Destructor</li>

 <li>void insert(Comparable value, int label): This method inserts an item with the given value and label into the MPQ.</li>

 <li>Comparable Remove(int label): This method removes the value with this label and returns it.</li>

 <li>Comparable GetMax( ): This method returns the maximum value that is currently stored. (<strong>Note that contrary to priority queues, we do not remove the value from the MPQ data structure!</strong>)</li>

 <li>Finally, our class must allow us to check if it is empty, using the function</li>

</ul>

Boolean IsEmpty( ).

You will use heaps to implement MPQs. Let us assume that you call the array for the heap as <em>Heap</em>. The tricky part is to maintain a link between a value and a label assigned to it. For this, it will be convenient to have a parallel private array of integers, called <em>Location</em>, whose <em>i</em><sup>th</sup> entry contains the position in the heap of the item having label <em>i</em>. Thus you can locate a heap entry with a given <em>label</em> in <em>O(1)</em> time, instead of searching for it in the heap in <em>O(N)</em> time. At all times, for the valid entries in the heap, <em>Heap[Location[i]].label </em>equals <em>i</em>, and <em>Location[Heap[j].label]</em> equals <em>j</em>. When you move an element around in the heap, you should be careful to change the corresponding value in <em>Location </em>to contain the new position of the element.

<h1>2   The Skyline Program</h1>

Once you have implemented the MPQ Class, you will write the code that computes the skyline of a city. We suggest the following algorithm outline but certainly you are welcome to come up with your own, but you should employ the MPQ class.

<ol>

 <li>Read in the descriptions of all of the buildings from a file called <strong>txt</strong>. The format will be as given earlier.</li>

 <li>Once you have read all the data in, put all of the x-coordinates of the left and right sides in a separate array (of size twice the number of buildings) together, and sort them into ascending order of the x-coordinates using some fast sorting algorithm (you can use heapsort, but you will have to modify it a bit). With each xcoordinate, also keep the identity of the corresponding building in the same array (e.g., the sequence number of the building as you read them in), and which side (left or right) it belongs to.</li>

 <li>Make a left-to-right sweep across the city by examining the x-coordinates in the sorted list in ascending order. During the course of the sweep, the MPQ is used to keep track of which buildings span the current x coordinate and which of the buildings has the maximum height. You will have to figure out how to use the MPQ class for this. After each insertion and deletion, check to see if the maximum height of the buildings in the MPQ has changed. If so, output the x- coordinate that has just been examined, followed by the new current maximum height to the standard output.</li>

</ol>



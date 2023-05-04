Download Link: https://assignmentchef.com/product/solved-csci-1200-data-structures-homework-1-morphological-image-processing
<br>
At the core of many advanced computer vision algorithms for image segmentation, feature detection, and classification are several basic morphological image processing operations that modify the borders between neighboring clusters of similarly colored pixels. The <em>dilation </em>operation adds pixels along the boundary to expand or grow a cluster. The <em>erosion </em>operation shrinks the boundary of the cluster by reassigning pixels along the boundary to a background color. We’ll also implement a simple <em>replace </em>operation to change all pixels in the image of color A to color B. And the <em>floodfill </em>operation that is similar to replace, but only changes pixels that are part of the same connected cluster.

The diagram on the right illustrates the details of the dilation and erosion operations. In both cases we will use a plus-shaped <em>structuring element </em>that contains the 4 adjacent pixels to a candidate pixel. When deciding which pixels to add to expand the boundary of the grey cluster during a <em>dilation </em>operation, we place the structuring element over each candidate pixel and ask if the shape overlaps or “hits” any of the existing grey pixels. If it does, we change its color to the foreground color (grey). In contrast, when shrinking the boundary during <em>erosion</em>, we consider removing each pixel from the cluster. If all of the pixels of the structuring element do not fully “fit” within the grey cluster of pixels we will set that pixel to the background color (white).

You will work with command line arguments, file input and output, and the STL C++ string and vector classes to manipulate manipulate a grid of ASCII characters (instead of a traditional color image file). Please read the entire assignment carefully before starting to program.

<h1>Command Line Arguments</h1>

Your program will expect 4-6 command line arguments, depending on the requested operation. The 1st argument is the name of the input ASCII art image file. The 2nd argument is the name of the output file where the ASCII art image resulting from the operation should be written. The 3rd argument is the name of one of 4 operations that should be performed: replace, dilation, erosion, or floodfill. Here are some example command lines:

./image_processing.out input4.txt output4_replace.txt replace X O

./image_processing.out input4.txt output4_dilation.txt dilation X

./image_processing.out input4.txt output4_erosion.txt erosion X .

./image_processing.out input4.txt output4_floodfill.txt floodfill 2 10 O

The number and purpose of the remaining arguments on the command line depend on the operation. For a <em>replace </em>operation, the 4th argument is the character that should be removed from the image and the 5th argument is the character that should be substituted in those locations. For the <em>dilation </em>operation, the 4th argument is the foreground character (clusters of pixels of this “color” should increase in size). For the <em>erosion </em>operation, the 4th argument is the foreground character (clusters of pixels of this “color” should decrease in size). We also need to know the background color that will replace pixels that are removed from the foreground object and the 5th argument is that background character. Finally, for the <em>floodfill </em>operation, the 4th and 5th command line arguments are the integer coordinates of the starting point for floodfill (row &amp; column respectively) and the 6th command line argument is the replacement character.

Note that certain ASCII characters have special meaning on the command line, and it will be necessary to <em>escape </em>that meaning by preceding those characters by a backslash () to make sure your program receives the desired character.

<h1>Examples and More Information</h1>

In many computer vision applications, these operations are applied sequentially, one after the other. Note that these operations are generally not commutative. The <em>opening </em>operation is the result of first applying erosion and then dilation. The effect of opening is to round sharp outer corners and remove tiny islands. The <em>closing </em>operation is achieved by first performing dilation and then erosion. The effect of closing is to fill in small gaps within the foreground object and smooth inner corners.

./image_processing.out output4_erosion.txt output4_opening.txt dilation X

./image_processing.out output4_dilation.txt output4_closing.txt erosion X .

<table width="675">

 <tbody>

  <tr>

   <td width="98">input4.txt</td>

   <td width="98">output4 replace.txt</td>

   <td width="99">output4 dilation.txt</td>

   <td width="98">output4 erosion.txt</td>

   <td width="104">output4 floodfill.txt</td>

   <td width="98">output4 opening.txt</td>

   <td width="82">output4 closing.txt</td>

  </tr>

  <tr>

   <td width="98">………….…………...XXX…..X....XXX…..X....XXX……....XXX……....XXXXXXX…...XXXXXXX…...XXXXXXX….………….………….</td>

   <td width="98">………….…………...OOO…..O....OOO…..O....OOO……....OOO……....OOOOOOO…...OOOOOOO…...OOOOOOO….………….………….</td>

   <td width="99">…………...XXX…..X...XXXXX…XXX..XXXXX…XXX..XXXXX….X...XXXXXXXX…..XXXXXXXXX….XXXXXXXXX….XXXXXXXXX…..XXXXXXX….………….</td>

   <td width="98">………….………….………….…X…………X…………X…………XX……..…XXXXX…..………….………….………….</td>

   <td width="104">………….…………...XXX…..O....XXX…..O....XXX……....XXX……....XXXXXXX…...XXXXXXX…...XXXXXXX….………….………….</td>

   <td width="98">………….………….…X………..XXX……....XXX……....XXX……....XXXXXX…....XXXXXXX….…XXXXX…..………….………….</td>

   <td width="82">………….…………...XXX…..X....XXX…..X....XXX……....XXXX……...XXXXXXX…...XXXXXXX…...XXXXXXX….………….………….</td>

  </tr>

 </tbody>

</table>

You must follow the specifications for the command line arguments and functionality exactly as described in this handout to receive full credit. Sample input and output files are posted on the course website, and the validation and automatic grading on the submission server will also help you check your work. More information on command line arguments and file I/O in C++ is available on the course webpage under <a href="http://www.cs.rpi.edu/academics/courses/fall15/csci1200/other_information.php">“</a><a href="http://www.cs.rpi.edu/academics/courses/fall15/csci1200/other_information.php">Misc. C++ Programming Info</a><a href="http://www.cs.rpi.edu/academics/courses/fall15/csci1200/other_information.php">”</a>.

<h1>Image Bounds &amp; other Error Checking</h1>

When the structuring element is placed at the edge of the image, one or more pixels may fall off the edge and not overlap legal image coordinates. You do not want to access data that does not exist (a memory error that could give weird output or crash the program!). Be sure to add appropriate checks in your program to skip these out-of-bounds coordinates.

You may assume that the input image file is properly formatted and contains a rectangular grid of non-white space characters. However, to help with your own debugging, you should implement simple error checking to ensure that the command line arguments are appropriate and that the input and output file streams are successfully opened. Your program should exit gracefully with a useful error message sent to std::cerr if there is a problem with the arguments.

<h1>Extra Credit</h1>

For extra credit you may extend your program to work with larger and/or differently shaped structuring elements. Paste interesting examples &amp; comparisons of your results into your README.txt file. You may add additional command line arguments to specify an alternate structuring element; however, make sure your program uses the plus-shaped structuring element by default and still works as described above so you get full credit for the main homework on the submission server!



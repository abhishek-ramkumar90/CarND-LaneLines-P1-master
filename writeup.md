
#**Steps to execute the project ** 
1) Clone or download this project   

2)Execute the file named LaneDetection.ipynb

3)All the output images will be generated in result_images folder and the output videos including the challege video will be generated     in the result_videos folder

Note:(Kindly Delte all the files present inside result_images and result_videos folder the commited Images and videos are the actual          output which will be automatically genereated once when you run the python file(LaneDetection.ipynb))






#**Finding Lane Lines on the Road** 


My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I converted the image to gray scale to indentify bright pixels  easily

Second,I applied a gaussian blur using opencv.gaussianBlur api ,the reason to using this function was to remove noise from the grayscale image

Third,Then i applied the canny edge detection algorith to the above image to identify edges , canny edge detection highlights edges when there is a great difference in the pixel values between adjacent points

Fourth,I applied a regionmask only to keep the region which i am interested in and then i applied the hough Transform to detect lines in the region of interest 

To draw lines i used the draw_lines function where i did the following 
   a)Find slopes of all lines
     But only care about lines where abs(slope) > slope_threshold.
   
   b) And then i found the left and right lines depending on the slope value,Lines which slant towards right have a negative slope thus       left lanes have negative slopes and Lines which  slant towards left have positive slopes thus right Lanes have positive slope  , i       also applied a filter to include left lanes where in the x- co-ordinates are always less than the centre-coordinates and right           lanes whose x-coordinates and greater than the centre coordinates.
    
   c) After collecting these lines i interrated them individually(one for left and one for right) and collecting their x,y cordinates         and applying the linear regression to get the slope and y-intercept of the individual lines
   
   d) To find 2 end points for right and left lines, used for drawing the line .I got the y-cordinates from the image and the calculated       the x-coordinates for the two lines using the following equation # y = m*x + b --> x = (y - b)/m
    
    e) I merged the points using opencv.line function
    
    
Fifth,I added my original colour image on top of the CannyEdge image to get the original image with lane lines detected in red colour 


There are few short comings in the process which i have implemented ,
   a) Code quality is not good as their was some time issues 
   
   b) I have hardcoded some values without assigning them to a global variable 
   
   c) For the video challege My Lane line for the left lanes gets a little bit distorted when the colour of the road changes from dark         gray to light gray, I have to adjust the threshold values which i have provided 
   
   
 
  
Few possible improvents to my pipeline would be to collect points and draw a curve using opencv.polylines function which might put a proper curve imposition on top of the lanes where their is a curve instead of a straight line , the reason i was not able to do that was lak of knowledge in python and opencv,but i will definetly some research and implement it in future to detect a smooth and clear lines 

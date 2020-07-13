# Social-distancing-surveillance-using-computer-vision



# AI powered social distancing surveillance system in Office and Public places.




# Introduction :

Maintaining social distancing is a very crucial issue in a COVID-19 outbreak scenario. This is an effective way to control the spread of the virus. However, it is very difficult to maintain and monitor the social distancing norms in many cases, such as in public places, offices, and workplaces, where working in very close proximity was a requirement. To tackle all these problems we can design as an AI-powered mass surveillance system to help to maintain the social distancing in such scenarios.



# Description with all technical details :


In the fight against the COVID-19, social distancing has proven to be a very effective measure to slow down the spread of the disease. People are asked to limit their interactions with each other, reducing the chances of the virus being spread with physical or close contact.

In past also AI/Deep Learning has shown promising results on a number of daily life problems. Here I will go through detailed explanation of how we can use Python, Computer Vision and Deep Learning to monitor social distancing at public places and workplaces.

To ensure social distancing protocol in public places and workplace, I have developed social distancing detection tool that can monitor if people are keeping a safe distance from each other by analyzing real time video streams from the camera. For example: People at workplaces, factories, shops we can integrate this tool to their security camera systems and can monitor wether people are keeping a safe distance from each other or not.

# Features:

- Detect humans in the frame with yolov3.
- Calculates the distance between every human who is detected in the frame.
- Shows how many people are at High, Low and Not at risk.


# Implementation Details:


# Camera Prespective Transformation or Camera Calibration:

As the input video may be taken from an arbitrary perspective view, the first step is to transform perspective of view to a bird’s-eye (top-down) view. As the input frames are monocular (taken from a single camera), the simplest transformation method involves selecting four points in the perspective view which define ROI where we want to monitor social distancing and mapping them to the corners of a rectangle in the bird’s-eye view. Also these points should form parallel lines in real world if seen from above(birds eye view). This assumes that every person is standing on the same flat ground plane. This top view or bird eye view has the property that points are distributed uniformally horizontally and vertically(scale for horizontal and vertical direction will be different).From this mapping, we can derive a transformation that can be applied to the entire perspective image.

We draw 8 points on first frame using mouse click event. First four points will define ROI where we want to monitor social distancing. Next 3 points will define 180 cm(unit length) distance in horizontal and vertical direction and those should form parallel lines with ROI. In above image we can se point 5 and point 6 defines 180 cm in real life in horizontal direction and point 5 and point 7 defines 180 cm in real life in vertical direction. As we can see ROI formed by first 4 points has different length in horizontal and vertical direction, so number of pixels in 180 cm for horizontal and vertical direction will be different in rectangle(bird’s eye view) formed after transformation. So from point 5,6,7 we are calculating scale factor in horizontal and vertical direction of the bird’s eye view, e.g. how many pixels correspond to 180 cm in real life.

# Detection:

The second step to detect pedestrians and draw a bounding box around each pedestrian. For simplicity, i am using an open-source pedestrian detection network based on the Yolo v3 architecture. To clean up the output bounding boxes, we apply minimal post-processing such as non-max suppression (NMS) and various rule-based heuristics, so as to minimize the risk of overfitting.

# Distance Calculation:

Now we have bounding box for each person in the frame. We need to estimate person location in frame. i.e we can take bottom center point of bounding box as person location in frame.Then we estimate (x,y) location in bird’s eye view by applying transformation to the bottom center point of each person’s bounding box, resulting in their position in the bird’s eye view.Last step is to compute the bird’s eye view distance between every pair of people and scale the distances by the scaling factor in horizontal and vertical direction estimated from calibration.

# How it works:

- Running main.py will give you frame(first frame) where you need to draw ROI and distance scale.
- The second step to detect pedestrians and draw a bounding box around each pedestrian.
- Now we have bounding box for each person in the frame. We need to estimate person location in frame. i.e we can take bottom center point of bounding box as person location in   frame. Then we estimate (x,y) location in bird’s eye view by applying transformation to the bottom center point of each person’s bounding box, resulting in their position in     the bird’s eye view.
- Last step is to compute the bird’s eye view distance between every pair of people(Point) and scale the distances by the scaling factor in horizontal and vertical direction       estimated from calibration.
- Lastly we can draw Bird’s Eye View for region of interest(ROI) and draw bounding boxes according to risk factor for humans in a frame and draw lines between boxes according to   risk factor between two humans.
- Red, Yellow, Green points represents risk to human in Bird’s eye view. Red: High Risk, Yellow: Low Risk and Green: No Risk.
- Red, Yellow lines between two humans in output tells they are violating social distancing rules.

# Future work(any suggestions and contributions are welcomed)  :

- In this system, we can add face recognition.
- We can add modules for registration of face, Indentifications of face.
- we can add module for automatic fine or penalty system also.

# Requirements:

You will need the following to run this code:

Python 3.5.2
Opencv(CV2) 4.2.0
numpy 1.14.5
argparse

For person detection:
yolov3.weights, yolov3.cfg files ( weights file in not present because of size issue. It can be downloaded from here : https://pjreddie.com/media/files/yolov3.weights )

For running:
Good GPU, for faster results. CPU is also fine. Also for CPU you can use yolov3-tiny.weights (https://pjreddie.com/media/files/yolov3-tiny.weights).


# Team :

- Gautam Pala
- Jayesh Kriplani
- Rushabh Patel
- Pranam Doshi
- Vatsal Lalcheta



# Work in progress

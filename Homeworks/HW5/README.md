
Multiple Object Tracking
Teammates: Jason Li

Problem Definition
Give a concise description of current problem. What needs to be solved? Why is the result useful? Do you make any assumptions? What are the anticipated difficulties?

The goal of this part of the programming assignment is to learn more about the practical issues that arise when designing a tracking system. You are asked to track moving objects in video sequences, i.e., identifying the same object from frame to frame:

First, we need a model to predict the position of an object on a frame, which can be done based on its position in a previous frame. We could either use an alpha-beta filter or kalman filter to track object state, and need to correlate these predicted positions from frame to frame.

We anticipate issues with object detection, crossing paths and object occlusion.

Method and Implementation
Give a concise description of the implemented method. For example, you might describe the motivation of your idea, the algorithmic steps of your methods, or the mathematical formulation of your method.

We track objects using their calcucated centroid locations. We preprocess images by subtracting the background of the frames using cv2.createBackgroundSubtractorMOG2(), then blur the image using a 3x3 kernel, and perform erosion and dilation. We store detected object data in a tracker object that we create. This includes the object's position, Kalman filter parameters and location history. The Kalman filter is used to predict the position of the tracked object in the subsequent frames. We used the Hungarian method to associate a detected object with its location history. Then, we update the filter parameters as well as the list of tracked objects.

Results
List your experimental results. Provide examples of input images and output images. If relevant, you may provide images showing any intermediate steps. If your work involves videos, do not submit the videos but only links to them.

Attached bat_tracked.avi and cell_tracked.avi.

Discussion
Discuss your method and results:

What are the strengths and weaknesses of your method?
The tracking results are optimal when the objects are detected correctly and the object isnt occluded.

Do your results show that your method is generally successful or are there limitations? Describe what you expected to find in your experiments, and how that differed or was confirmed by your results.
The method is generally successful.

Potential future work. How could your method be improved? What would you try (if you had more time) to overcome the failures/limitations of your work?
This could be improved by accurately matching objects to their last known location when an object disappears and then reappears.

Conclusions
Based on your discussion, what are your conclusions? What is your main message?

As long as the objects don't occlude each other and don't move chaotically our algorithm is fairly successful in tracking multiple objects.

Questions

1. Show your tracking results on some portion of the sequence. In addition to showing your tracking results on an easy portion of the data, identify a challenging situation where your tracker succeeds, and a challenging situation where your tracker fails.

I've attached videos of tracking on both datasets. Our tracker succeeds in handling cell division, making them two distinct new tracks, but when many objects bunch together the tracker tends to convert them into a single unit.

2. How do you decide to begin new tracks and terminate old tracks as the objects enter and leave the field of view?

We compare the number of detected centroids to the number of assigned tracks to determine the presence of new tracks. If there are more centroids than tracks, we ascertain that a new object has entered the frame. If an object leaves the FOV, we count the number of frames where it is absent and if it surpasses the threshold we delete it.

3. What happens with your algorithm when objects touch and occlude each other, and how could you handle this so you do not break track?

When objects get too close or occlude each other the algorithm tends to bunch them together. Since we track objects by finding contours and their centroids, close objects fuse into one contour. One of the objects will therefore be missing from subsequent frames before it surpasses the threshold and is dropped.

4. What happens when there are spurious detections that do not connect with other measurements in subsequent frames?

If we detect spurious detections that do not connect with other measurements in subsequent frames, they are deleted once they reach the threshold of the number of frames for which an object can be missing.

5. What are the advantages and drawbacks of different kinematic models: Do you need to model the velocity of the objects, or is it sufficient to just consider the distances between the objects in subsequent frames?

Velocity is necessary to detect occlusion and enable better tracking in those situations because it gives a better estimate of location than just position.

Credits and Bibliography
Cite any papers or other references you consulted while developing your solution. Citations to papers should include the authors, the year of publication, the title of the work, and the publication information (e.g., book name and publisher; conference proceedings and location; journal name, volume and pages; technical report and institution).

https://github.com/mabhisharma/Multi-Object-Tracking-with-Kalman-Filter
https://github.com/srianant/kalman_filter_multi_object_tracking
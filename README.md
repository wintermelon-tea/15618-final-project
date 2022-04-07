# Titel: Parallel Image Blending
## Team Members: Amanda Xu (xinyix2), Ziming He (zimingh)

### SUMMARY: 
We are going to explore parallel versions of various image blending techniques, which include gradient blending, seam-driven image blending and pyramid blending. We will be implementing parallel versions of those image blending/stitching techniques on NVIDIA GPUs using CUDA.

### BACKGROUND: 
For those image blending techniques, the sequential version often focuses on doing work around one pixel at a time. We propose to apply parallelism to speedup the process by letting the GPU perform work on multiple pixels at the same time. For example, for gradient based blending such as Poisson blending, the sequential version will process the pixels in the source regions one at a time using surrounding pixels to calculate the gradient, and in the parallel version, we would like to compute the results of the blend for multiple pixels or regions at the same time. This way, we can greatly speed up the entire process.

![Before and After Poisson based gradient blending](https://user-images.githubusercontent.com/16871889/159832443-f90c470c-9d24-42fb-a733-a0cb9343fe96.PNG)

And for seam-driven image stitching such as seam cutting that finds minimum error boundary, the subdivision for tasks is different for the dynamic programming implementation. We can still parallelize through each scan to increase the overall speedup. Each of those image blending techniques require us to think of different ways of subdivision as well as grouping pixels for better resource management.

### THE CHALLENGE: 
The main challenges would be around the memory limit and the access patterns. Since many of those images may be very large and the access pattern around the stitching regions may not be optimal in terms of the storage. We hope to experiment more about how to better prepare the images for task division as well as the I/O process between host and device. In other words, how should we subdivide the tasks such that we can avoid repetitively loading and saving intermediate results between the host and device. There should be little to no divergent executions.

### RESOURCES: 
We will probably use the GHC machine for the entire project. There may exist CUDA implementation for some of the image stitching techniques but we will start with implementing sequential versions of those techniques with CUDA and move on to parallel versions and further optimizations. 
### GOALS AND DELIVERABLES: 
Our 75% goal is to implement one parallel version of one image blending technique. Our 100% goal is to implement parallel versions for at least two image blending techniques. Our 125% goal is to implement parallel versions for at least two image blending techniques with optimized access patterns. In the poster session we will provide a program that can be run to show the difference between sequential and parallel version of those image blending techniques. This program will produce the output in different amount of time. The speedup should be obvious if we use high-resolution images (minutes with sequential version and seconds with parallel version). We are not sure the exact speedup that we can achieve at the moment, but it should be in the ballpark of 10x.
### PLATFORM CHOICE: 
We will be coding in C++ with the CUDA framework on GHC machines with NVIDIA GPU devices. This is a good choice because we are doing a large number of tasks that are the same across hundreds or thousands of pixels and CUDA programming should be the best platform for use in this project.
### SCHEDULE: 
1. Week 1(0323 - 0330): Implement sequential version of one image blending technique
2. Week 2(0331 - 0406): Implement parallel version of one image blending technique and performance evaluation
3. Week 3(0407 - 0413): Checkpoint on 0411 with milestone report. Implement sequential version of another image blending technique
4. Week 4(0414 - 0420): Implement parallel version of another image blending technique and performance evaluation, comparison between both image blending techniques
5. Week 5(0421 - 0429): More memory access patterns optimizations. Prepare the poster for the poster session.

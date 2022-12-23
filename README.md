# Mandelbrot Set

## Introduction

Welcome to the project memory of the implementation of the Mandelbrot set. The Mandelbrot set is a mathematical object that has fascinated mathematicians, computer scientists, and artists alike. In this project, I aimed to delve deeper into the properties and behavior of the Mandelbrot set.

To begin, let's define the Mandelbrot set. It is a set of complex numbers, which are numbers that can be written in the form a + bi, where a and b are real numbers and i is the imaginary unit defined as the square root of -1. The Mandelbrot set is defined as the set of complex numbers c for which the function f(z) = z^2 + c does not diverge when iterated from z = 0. This means that a complex number c belongs to the Mandelbrot set if the sequence f(0), f(f(0)), etc., remains bounded in the complex plane when starting with z = 0 and applying the function f repeatedly.

To visualize the Mandelbrot set, I used a computer program that plots the set in the complex plane and colors each point according to whether it belongs to the set or not. Points that belong to the Mandelbrot set are colored black, while points that do not belong to the set are colored according to how quickly the function f diverges for that point. The resulting image is highly detailed and intricate, with a repeating pattern that exhibits self-similarity at various scales.

The Mandelbrot set has a number of interesting properties and has been studied extensively by mathematicians and computer scientists. It is also popular among recreational mathematicians and has been featured in numerous books and articles. Despite its mathematical origins, the Mandelbrot set has also been embraced by the art world, with many artists creating works based on the set and its visual representations. In this project, I had the opportunity to explore the Mandelbrot set and its various characteristics in more detail.

One particularly noteworthy aspect of the Mandelbrot set is its fractal nature. Fractals are geometric shapes that exhibit self-similarity at different scales, and they can be generated using a recursive process. The Mandelbrot set is an example of a fractal that can be generated using a recursive mathematical process. The study of fractals has led to many important mathematical discoveries and has had applications in fields such as computer graphics, data compression, and image processing. The intricate and detailed nature of fractals has also made them popular in the art world, with many artists creating works based on fractal patterns and shapes. The Mandelbrot set, in particular, has been widely studied and has been featured in numerous books and articles. It has also been embraced by the art world, with many artists creating works based on the set and its visual representations.

## Implementation

The objective of this project was to plot the Mandelbrot Set in the complex plane using a computer program written in C and SDL (Simple DirectMedia Layer) library.
For that, I have created a few .c and .h files along with a Makefile that compiles, links and runs the program with one command. 

### fractal.c
The provided code is a function called "set_mandelbot" that is used to plot the Mandelbrot set, a mathematical object defined as the set of complex numbers for which the function f(z) = z^2 + c does not diverge when iterated from z = 0. In other words, a complex number c belongs to the Mandelbrot set if the sequence f(0), f(f(0)), etc., remains bounded in the complex plane when starting with z = 0 and applying the function f repeatedly.

The "set_mandelbot" function takes four arguments: an integer representing the width of the image, an integer representing the height of the image, a string containing the pixel data for the image, and a struct called "world_coordinates" that represents the boundaries of the complex plane to be plotted. The function begins by calculating the pixel width and height of the image based on the dimensions of the complex plane and the width and height of the image. This allows the function to map the complex plane to the image pixels.

Next, the function sets the radius of the circle around the Mandelbrot set and the number of iterations to perform on each point in the complex plane. The radius of the circle is used to determine whether a complex number diverges or remains stable. If the magnitude of the complex number is greater than the radius of the circle after a certain number of iterations, it is considered to have diverged and is not part of the Mandelbrot set. The number of iterations to perform is a trade-off between accuracy and performance. A higher number of iterations will produce a more accurate plot of the Mandelbrot set, but it will also take longer to compute.

The function then uses an OpenMP directive to parallelize the outer for loop, which iterates over each row and column of the image. For each pixel, the function uses the Mandelbrot recursive formula to determine whether the complex number corresponding to that pixel belongs to the Mandelbrot set or diverges. If the complex number diverges, the function sets the pixel to a specific color based on the number of iterations performed. If the complex number remains stable, the function sets the pixel to black. This allows the function to visualize the Mandelbrot set as an image by coloring points that belong to the set differently from those that do not.

Finally, the function writes the pixel data to the "rgb" array using the values stored in the "pixel" array. The function then returns, allowing the caller to write the pixel data to a bitmap image file or display it on the screen. The resulting image will be a visualization of the Mandelbrot set, with points that belong to the set colored black and points that do not belong to the set colored according to how quickly the function f diverges for that

### bmp.c
The write_bmp function is responsible for converting a raw image stored in the rgb array into a bitmap image file with the .bmp format. The function receives four parameters: the filename of the new image, the raw image data stored in the rgb array, the length of the rgb array in bytes, and the width of the image in pixels.

The first step in the function is to calculate the height of the image in pixels using the length and width parameters. Then, the function declares a static variable called screenshots_count which is used to generate unique filenames for the images. The width of the image is padded to a multiple of 4, in order to comply with the BMP format specification. This is done with the help of the round4 function, which is an internal function defined at the beginning of the file.

Next, the function allocates memory for a new array called bitmap, which will store the image data in the BMP format. The size of this array is calculated as the product of the height of the image, the padded width of the image, and the size of a single character in bytes.

The main processing of the function happens in a nested loop, where each pixel of the image is processed. The loop iterates through each row and column of the image, and for each pixel, it sets the corresponding values in the bitmap array. The pixel values are set using the values from the rgb array, which stores the image in the RGB format. The pixel values are stored in the opposite order in the BMP format, so the function uses the 2 - color index

### main.c
The main function in this code initializes and sets up an SDL window and renderer, which will be used to display the Mandelbrot set. It also defines the world coordinates of the set, which will determine which area of the set is displayed in the window. The user is given instructions on how to interact with the program, and the program waits for the user to press a key before continuing.

Once the window and renderer are set up, the program enters a loop that will run until the user closes the window or quits the program. Within this loop, the program handles user input, generates a new frame of the Mandelbrot set based on the current world coordinates, and displays the frame in the window.

To handle user input, the program uses the SDL_PollEvent function to check for events, such as key presses or mouse movements. If the user has pressed a key, the program updates the world coordinates based on the key that was pressed. For example, if the user pressed the "w" key, the program would decrease the value of the set_up coordinate, effectively moving the displayed portion of the set upward.

To generate a new frame of the Mandelbrot set, the program calls the set_mandelbot function from the fractal.h file, passing in the current world coordinates and a pointer to the memory array that will hold the pixel data for the frame. The set_mandelbot function iterates over each pixel in the frame, calculates the corresponding complex number in the Mandelbrot set, and determines whether the complex number tends to infinity or remains stable. Based on this, it sets the pixel's color value in the memory array.

Finally, to display the frame in the window, the program creates a texture from the memory array and uses the SDL_RenderCopy function to render the texture to the window. The program then calls SDL_RenderPresent to update the window with the new frame. This process is repeated continuously until the user closes the window or quits the program.

### Makefile
The Makefile provided is a build automation tool that specifies how to compile the source code in the src directory and generate the binary executable in the bin directory. It also has commands to clean up the directories and run the program.

The first section specifies the directories where the source files, header files, object files, and the final executable are stored. These are the SRC, INCLUDE, BIN, and DIST directories, respectively.

The second section defines the variables used for compilation and linking. The CC variable specifies the compiler to use (in this case, gcc). The CFLAGS variable specifies the flags to pass to the compiler, including the include directory (-I$(INCLUDE)), warning flags (-Wall -Wextra -Werror), and optimization level (-O3). The LDFLAGS variable specifies the flags to pass to the linker, including the OpenMP flag (-fopenmp) and the SDL2 library flag (-lSDL2). The TARGET variable specifies the name and path of the final executable.

The all target is the default target that is built when no target is specified. It first runs the clean target to remove any files from previous builds, then runs the setup target to create the necessary directories, and finally runs the $(TARGET) target to build the executable.

The setup target simply creates the bin and dist directories if they don't already exist.

The $(TARGET) target specifies the dependencies that need to be built before it can be built. These are the object files located in the dist directory. It then uses the CC and LDFLAGS variables to compile and link the object files into the final executable.

The $(DIST)/bmp.o, $(DIST)/main.o, and $(DIST)/fractal.o targets specify how to build the object files from their corresponding source files. They use the CC and CFLAGS variables to compile the source files into object files and place them in the dist directory.

The clean target removes the bin and dist directories.

The run target first builds the program using the all target and then runs the executable.

The tidy target cleans the directories and moves any .bmp files into a pics directory.

The clangd target generates a JSON file called compile_commands.json that can be used by clangd (a language server for C, C++, and Objective-C) to provide better code completion, error highlighting, and other features. This target requires the bear tool to be installed.

## Testing and validation

Throughout the development of this project I have encountered some issues related to performance and unexpected behaviour. The first issue I had to tackle was indeed related to performance. When compiling the code only using the bmp file, it would take around a minute when displaying the whole set. However, when setting the woorld coordinates deep in, as in, a few decimals, it would take around ten minutes to generate a single frame. The idea was to create an interactive program that allowed the user to smoothly travel within the set, and having to wait more than 10 minutes for some frames to be rendered was far from ideal. I realised the logic on set_mandelbrto could be improved and changed to only perform the exact number of iterations needed.

Besides that, I investigated further on some optimisation concepts and realised that using OpenMP compiler would critically improve my program's performance. It essentially tells the compiler to create a team of threads to execute the loop in parallel, with each thread responsible for executing a portion of the loop iterations. Now the processor uses the maximum number of threads available.

Lastly, The O3 flag is an optimization flag that can be passed to the compiler. It tells the compiler to apply a set of aggressive optimization techniques to the code being compiled, with the goal of producing faster and more efficient machine code. These optimization techniques may include inlining functions, vectorizing loops, and unrolling loops, among others. The O3 flag is generally considered to be the most aggressive optimization level offered by most compilers. It is typically used when the primary goal is to produce the fastest and most efficient code possible, at the expense of longer compilation times and potentially larger code size.

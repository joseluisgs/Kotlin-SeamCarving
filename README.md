# Kotlin  Seam Carving
Proyecto de evaluación para el título de Kotlin Developer en Jetbrains Academy. Consiste en trabajar con distintas imágenes aplicando Seam Carving.

[![Kotlin](https://img.shields.io/badge/Code-Kotlin-blueviolet)](https://kotlinlang.org/)
[![LISENCE](https://img.shields.io/badge/Lisence-MIT-green)]()
![GitHub](https://img.shields.io/github/last-commit/joseluisgs/Kotlin-SeamCarving)


![imagen](https://www.adesso-mobile.de/wp-content/uploads/2021/02/kotlin-einfu%CC%88hrung.jpg)

## Acerca de
Este proyecto de la academia Jetbrains fue realizado con el fin de evaluar la capacidad de desarrollo de Kotlin. Dada una imagen consiste en oprrar cone lla usando Seam Carving

- [Kotlin  Seam Carving](#kotlin--seam-carving)
  - [Acerca de](#acerca-de)
  - [Enunciado](#enunciado)
    - [Parte 1](#parte-1)
      - [Description](#description)
    - [Parte 2](#parte-2)
      - [Description](#description-1)
    - [Parte 3](#parte-3)
      - [Description](#description-2)
    - [Parte 4](#parte-4)
      - [Description](#description-3)
    - [Parte 5](#parte-5)
      - [Description](#description-4)
    - [Parte 6](#parte-6)
      - [Description](#description-5)
  - [Autor](#autor)
    - [Contacto](#contacto)
  - [Licencia](#licencia)

## Enunciado
### Parte 1
#### Description
Your task is to draw a black rectangle of a given size, draw two red lines crossing it and save the image. Your program should read the rectangle's width and height, as well as the output file name from the input. We will use only .png file format for this project.

We recommend to use java.awt.image.BufferedImage class to handle and manipulate the image data and javax.imageio.ImageIO for reading and saving images from/to a file. You can check out some nice explanations and examples of BufferedImage and ImageIO to be more confident in what you're doing. You can also look at official documentation on BufferedImage and ImageIO classes.

Tests use hash comparison of output files to test your solution. Using the proposed classes will help you avoid unintended difficulties.



### Parte 2
#### Description
Before digital photography came around, people used to work with negative images on film. Let’s get nostalgic and emulate a warm analog negative film image!

To create a negative image, you should invert all color components for every pixel. Inverted color for (r, g, b) is (255 - r, 255 - g, 255 - b).

Objective
At this stage, you should add command-line parameters to specify the input and output files for your program. Use parameter -in for the input file path and parameter -out for the output file path. For simplicity, we will use only .png file format in this project. Your program should read the specified input image file, inverse colors and save the file to a given location.

Example
The greater-than symbol followed by a space (> ) represents the user input. Note that it's not part of the input.

> java Main -in sky.png -out sky_negative.png

### Parte 3
#### Description
Now you are able to manipulate pictures and ready to start.

The first step is to calculate the energy for each pixel of the image. Energy is the pixel's importance. The higher the pixel energy, the less likely this pixel is to be removed from the picture while reducing.

There are several different energy functions invented for seam carving. In this project, we will use dual-gradient energy function.

The energy of the pixel (x, y)(x,y) is E(x, y) = \sqrt{\Delta_x^2(x, y)+\Delta_y^2(x, y)}E(x,y)= 
Δ 
x
2
​
 (x,y)+Δ 
y
2
​
 (x,y)
​
 

Where the square of x-gradient \Delta_x^2(x, y) = R_x(x, y)^2+G_x(x, y)^2+B_x(x, y)^2Δ 
x
2
​
 (x,y)=R 
x
​
 (x,y) 
2
 +G 
x
​
 (x,y) 
2
 +B 
x
​
 (x,y) 
2
 

y-gradient \Delta_y^2(x, y) = R_y(x, y)^2+G_y(x, y)^2+B_y(x, y)^2Δ 
y
2
​
 (x,y)=R 
y
​
 (x,y) 
2
 +G 
y
​
 (x,y) 
2
 +B 
y
​
 (x,y) 
2
 

Don't be confused! You will calculate values \Delta_x^2(x, y)Δ 
x
2
​
 (x,y) and \Delta_y^2(x, y)Δ 
y
2
​
 (x,y) that are already squared, so you don't need to square them again to calculate E(x, y)E(x,y).

Where R_x(x, y)R 
x
​
 (x,y), G_x(x, y)G 
x
​
 (x,y), B_x(x, y)B 
x
​
 (x,y) are differences of red, green and blue components between pixels (x+1, y)(x+1,y) and (x -1 , y)(x−1,y).

Let's consider a grey pixel (2, 1)(2,1) on the example image:



X-differences are:
R_x(2, 1) = 255-150=105,\ \ G_x(2, 1) = 250-150 = 100, \ \ B_x(2, 1) = 155 - 100 = 55R 
x
​
 (2,1)=255−150=105,  G 
x
​
 (2,1)=250−150=100,  B 
x
​
 (2,1)=155−100=55
So, x-gradient is \Delta_x^2(2, 1) = 105^2+100^2+55^2=24050Δ 
x
2
​
 (2,1)=105 
2
 +100 
2
 +55 
2
 =24050

Y-differences are:
R_y(2, 1) = 50 - 10 = 40, \ \ G_y(2, 1)=255-250 = 5, \ \ B_y(2, 1) = 255 - 40 = 215R 
y
​
 (2,1)=50−10=40,  G 
y
​
 (2,1)=255−250=5,  B 
y
​
 (2,1)=255−40=215
Same for y-gradient \Delta_y^2 = 40^2 + 5^2+215^2 = 47850Δ 
y
2
​
 =40 
2
 +5 
2
 +215 
2
 =47850

Finally, E(2, 1) = \sqrt{24050 + 47850} = 268.14E(2,1)= 
24050+47850
​
 =268.14

Energy for border pixels is calculated with a 1-pixel shift from the border. For example:
E(0, 2)=\sqrt{\Delta_x^2(1, 2) + \Delta_y^2(0, 2)}E(0,2)= 
Δ 
x
2
​
 (1,2)+Δ 
y
2
​
 (0,2)
​
 
E(1, 0)=\sqrt{\Delta_x^2(1, 0) + \Delta_y^2(1, 1)}E(1,0)= 
Δ 
x
2
​
 (1,0)+Δ 
y
2
​
 (1,1)
​
 
E(0, 0)=\sqrt{\Delta_x^2(1, 0) + \Delta_y^2(0, 1)}E(0,0)= 
Δ 
x
2
​
 (1,0)+Δ 
y
2
​
 (0,1)
​
 

Objective
Calculate energies for all pixels of the image. Normalize calculated energies using the following formula:
intensity = (255.0 * energy / maxEnergyValue).toInt()

To display energy as a grey-scale image, set color components of the output image pixels to calculated intensity. For example, (red = intensity, green = intensity, blue = intensity).

You should use double precision in this and in the following stages.

Example
The greater-than symbol followed by a space (> ) represents the user input. Note that it's not part of the input.

> java Main -in sky.png -out sky-energy.png


### Parte 4
#### Description
Now you are ready to find the best seam to remove. Vertical seam is a sequence of adjacent pixels crossing the image top to bottom. The seam can have only one pixel in each row of the image. For example, subsequent pixels for pixel (x,y)(x,y) are (x -1, y + 1)(x−1,y+1), (x, y + 1)(x,y+1) , and (x + 1, y + 1)(x+1,y+1).

The best seam to remove is the seam with the lowest sum of pixel energies from all possible seams. The problem of finding the best seam is very similar to finding the shortest path in a graph. Think of pixels as vertices. Connect them with imaginary edges. Edge weight should be equal to the energy of the pixel this edge is pointing to.



The easiest way to apply the shortest path finding algorithm to your energy graph is to add imaginary zero rows with the horizontal links on the top and on the bottom. Then you can search for the shortest path between top-left and bottom-right corners.



Also, you can come up with a dynamic programming solution without adding rows.

Objective
At this stage, your program should find the seam with the lowest energy and highlight it in red. Red is (255, 0, 0).

Example
The greater-than symbol followed by a space (> ) represents the user input. Note that it's not part of the input.

> java Main -in sky.png -out sky-seam.png

### Parte 5
#### Description
Description
Now you should implement horizontal seam search. It is the same as vertical. Use the transposed view of your image.

Objective
Find the horizontal seam and highlight it in red.

Example
The greater-than symbol followed by a space (> ) represents the user input. Note that it's not part of the input.

> java Main -in sky.png -out sky-horizontal-seam.png

### Parte 6
#### Description
Now you have everything to resize the image while preserving its content. Simply remove the seam, then remove the seam from the resulting image and so on!

Objective
Add two more command line parameters. Use parameter -width for the number of vertical seams to remove and -height for horizontal seams.

At this stage, your program should reduce the input image and save the result using the following algorithm:

Find a vertical seam and remove all the pixels that this seam contains. Then find another vertical seam on the resulted image and delete all the pixels that the second seam contains. Repeat the process until you remove the specified number of vertical seams.
Do the same, but with horizontal seams.
Example
The greater-than symbol followed by a space (> ) represents the user input. Note that it's not part of the input.

Example 1:

In the following example, the program should reduce the image width by 125 pixels and height by 50 pixels

> java Main -in sky.png -out sky-reduced.png -width 125 -height 50


## Autor

Codificado con :sparkling_heart: por [José Luis González Sánchez](https://twitter.com/joseluisgonsan)

[![Twitter](https://img.shields.io/twitter/follow/joseluisgonsan?style=social)](https://twitter.com/joseluisgonsan)
[![GitHub](https://img.shields.io/github/followers/joseluisgs?style=social)](https://github.com/joseluisgs)

### Contacto
<p>
  Cualquier cosa que necesites házmelo saber por si puedo ayudarte 💬.
</p>
<p>
    <a href="https://twitter.com/joseluisgonsan" target="_blank">
        <img src="https://i.imgur.com/U4Uiaef.png" 
    height="30">
    </a> &nbsp;&nbsp;
    <a href="https://github.com/joseluisgs" target="_blank">
        <img src="https://distreau.com/github.svg" 
    height="30">
    </a> &nbsp;&nbsp;
    <a href="https://www.linkedin.com/in/joseluisgonsan" target="_blank">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/LinkedIn_logo_initials.png/768px-LinkedIn_logo_initials.png" 
    height="30">
    </a>  &nbsp;&nbsp;
    <a href="https://joseluisgs.github.io/" target="_blank">
        <img src="https://joseluisgs.github.io/favicon.png" 
    height="30">
    </a>
</p>


## Licencia

Este proyecto está licenciado bajo licencia **MIT**, si desea saber más, visite el fichero [LICENSE](./LICENSE) para su uso docente y educativo.
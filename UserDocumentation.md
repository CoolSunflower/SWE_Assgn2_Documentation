# Interpolator (User Documentation)

This document explains the User Interface for the Interpolator software. 

```
Submitted by Team 10 for CS346 Assignment 2.
Team Members:
    Adarsh Gupta (220101003)
    Chouhan Shreyan (220101031)
    D Hayagrivan (220101032)
    Divyansh Chandak (220101039)
    Yash Jain (220101115)
```

## How to Run
- TBD!

## User Interface
The user experience can be divided into 2 phases:
- Initialising program with data
- Interpolating new data samples

### Initialising program with data
After starting the program the first input needed is the filename containing the input 1D paired data for the interpolator. The input format is detailed in the following section.
The filename must be provided with double backslashes for it to be correctly parsed. An example correct filename is `D:\\IITG\\6th SEMESTER\\SWE Lab\\Assignment2\\data.txt`.
This initial interface is as follows:
```bash
Interpolator!

Submission by Team 10:
         220101003       Adarsh Gupta
         220101031       Chouhan Shreyan
         220101032       D Hayagrivan
         220101039       Divyansh Chandak
         220101115       Yash Jain

[Info] File Name Format Example: D:\\IITG\\6th SEMESTER\\SWE Lab\\Assignment2\\data.txt (Use Double Backslashes)
[Input] Input the filename:
```

Once the user enters the correctly formatted filename, the program parses the data in the file and displays the number of points parsed correctly. Ensure that the file you have provided exists and the terminal has read permission for the file.

In case of an error the program gracefully exits with the following error:
```bash
[Input] Input the filename: hello
[Input Error] Could not open file. Either invalid filename or user does not have permission.
Press Enter to exit...
```

If the file exists and can be opened, the data in the file is parsed and the user is provided the parsing steps along with any warnings encountered regarding incorrect format:
```bash
[Input] Input the filename: D:\\IITG\\6th SEMESTER\\SWE Lab\\Assignment2\\data.txt
[Input Warning] Could not parse line: 9.9 ninety
[Input Warning] Could not parse line: 13.3
[Input Warning] Could not parse line: 15.0 text
[Success] Successfully parsed 12 points from the input file.
[Success] Successfully initialised interpolater with points.
```

### Interpolating new data samples
Post data initialisation, the user is prompted with the usage instruction along with an input prompt.
```bash
[Info] Usage: <X Value> <Method in {1, 2, 3, 4, 5}> or `help`.
> 
```

#### help Command
Running the `help` command presents the avalaible user commands.
```bash
> help
Usage:
        <X Value> <Method in {1, 2, 3, 4, 5}> - Calculate interpolated value
        exit - Quit the program
        help - Show this message
        poly - Prints the Calculated Polynomials for Newton and Lagrange Method.
For interpolation:
        1. Piecewise Constant Interpolation
        2. Nearest Neighbor Interpolation
        3. Linear Interpolation
        4. Newton's Divided Difference Interpolation
        5. Lagrange Interpolation
```

#### Interpolation
The user can provide any X value along with the interpolation method to use. The program will validate the method number and calculate and output the predicted Y value.
```bash
> 5 3
X = 5, Calculated Y = 50.4545
> 2 8
[Error] Invalid input! Write `help` for usage.
```

#### poly Command
The `poly` command prints the calculated polynomials for Newton's Divided Difference and Lagrange Interpolation method.
```bash
> poly
Evaluated Newtons Polynomial: P(x) = -122.20 + (10.06)(x - -12.20) + (-3.11)(x - -12.20)(x - 0.50) + (2.07)(x - -12.20)(x - 0.50)(x - 1.00) + (-0.61)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50) + (0.11)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50)(x - 4.40) + (-0.01)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50)(x - 4.40)(x - 6.60) + (0.00)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50)(x - 4.40)(x - 6.60)(x - 8.80) + (-0.00)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50)(x - 4.40)(x - 6.60)(x - 8.80)(x - 11.10) + (0.00)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50)(x - 4.40)(x - 6.60)(x - 8.80)(x - 11.10)(x - 14.40) + (-0.00)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50)(x - 4.40)(x - 6.60)(x - 8.80)(x - 11.10)(x - 14.40)(x - 16.60) + (0.00)(x - -12.20)(x - 0.50)(x - 1.00)(x - 2.50)(x - 4.40)(x - 6.60)(x - 8.80)(x - 11.10)(x - 14.40)(x - 16.60)(x - 17.70)
Evaluated Lagrange Polynomial: 0.0000x^11-0.0000x^10+0.0001x^9-0.0012x^8+0.0074x^7+0.0834x^6-2.0683x^5+18.3113x^4-85.2933x^3+210.2663x^2-227.6391x+76.3334
```

#### exit Command
Exits the program without errors.

## Input Format and Constraints
The input file should have newline seperated x, y values.

Example file data:
```
0.5 5.5
1.0 -10.0
2.5 25.3
4.4 44.4
```

Any erroneous inputs will be flagged during data initialisation. The number ranges supported by the program are: `1.7E +/- 308 (fifteen digits)`.

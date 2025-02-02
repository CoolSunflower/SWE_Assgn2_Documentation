# Interpolator (Technical Documentation)

This document contains the technical implementation details of the Interpolator software.

# Overall Workflow
The overall technical workflow proceeds as follows:
1. Display Initialisation Prompts: Implemented in the `displayInitPrompt()` function and just displays preset strings.
2. Input File Name from User and Parse the file for data values: Explained in [Data Loading](#data-loading) section.
3. Initialise Interpolator with Points: Explained in [Interpolator Initialisation](#interpolator-initialisation) section.
4. Continously parse user prompt and take appropriate actions: Explained in [User Input Processing](#user-input-processing) section.

The input paired points are represented via tha following structure:
```cpp
struct Point{
	double x, y;

	bool operator<(const Point &other) const{
		return x < other.x;
	}
};
```

Everything is handled via the Interpolation Class which has the following prototype:
```cpp
class Interpolation{
private:
    vector<Point> points; // The inputted array
    
    // Information for Newtons Divided Difference Method, populated during Initialisation step
    vector<double> coefficients;
    vector<double> x_values;
    vector<double> expanded_poly;       // Stores the final polynomial coefficients
    string NewtonPolynomial1;           // Stores intermediate polynomial expression
    string NewtonPolynomial2;           // Stores final polynomial expression

public:
    void processInput(vector<Point>&); // This function is responsible for initialisation of the data structures used in the entire interpolation process
    
    void calculateValue(double x, int method); // This function implements the main user interface to predict the interpolated value for any input via the specified interpolation method

    void NewtonPolynomial(void); // Prints the Newtons Polynomial (both intermediate and final) calculted during initialisation
    void LagrangePolynomial(void); // Prints the Lagrange Polynomial for the interpolation

private:
    // Interpolation functions that are called by calculateValue based on the method
    double piecewiseConstantInterpolation(double x);
    double nearestNeighborInterpolation(double x);
    double linearInterpolation(double x);
    double newtonInterpolation(double x);
    double lagrangeInterpolation(double x);
};
```

## Data Loading
The user provided file name is read into a string called `fileName`. This string is passed as a const char* to the `loadData()` function. The `loadData()` function returns a vector of `Point`'s. This vector contains all the points that were successfully parsed from the user input file, assuming no errors.

```cpp
	string fileName; ...
	getline(cin, fileName);
	vector<Point> points = loadData(fileName.c_str());
```

**Working**: We start by creating a temporary vector of `Point`'s called tempPoints and a file stream object from the user provided filename. At this stage if the file is not open we assume that the user provided filename is either invalid or the user does not have appropriate permission and we raise an error for the same, following which we exit with code 1.

If the file is successfully opened, we parse the file line by line. Each line is read from the file via the `getline()` function. From this line we try to extract the double values of x and y, in case of any error a user warning is raised with the contents of the line. If the values of x and y are successfully parsed from that line, we create a push a `Point` into the temporary vector.

Once all lines in the files are parsed, the `Point`'s are sorted (based on their X values, look at the < operator declaration in the struct). After this 2 security checks are implemented:
1. There exists atleast one point.
2. There does not exist any two points with same X values (checked by comparing adjacent enteries since Points are sorted on X).

The final temporary vector of `Point`'s is returned by the function containig all the values that were successfully read from the file in a sorted order.

## Interpolator Initialisation 
An interpolator object is created and the processInput function is called using the vector of `Point`'s returned by the loadData function.

```cpp
	// Parse File in the interpolator
	interpolater.processInput(points);
```

For interpolation methods 1, 2, 3 and 5 no further processing needs to be done on the input and hence the input `vector<Point>` is directly stored in private variable `points` of the Interpolation class.

However for method 4, i.e. Newton's Divided Difference Method, some preprocessing needs to be done to populate the private variables `coefficients`, `x_values` and `expanded_poly` of the Interpolation class. This function also calculates the string of the Intermediate and Expanded Polynomial form and saves it in the respective string variables to print if `poly` is called by the user.


**- TBD (Divyansh)**

## User Input Processing


### Piecewise Constant Interpolation Implementation

### Nearest Neighbor Interpolation Implementation

### Linear Interpolation Implementation

### Newton’s Divided Difference Interpolation Implementation

### Lagrange Interpolation Implementation


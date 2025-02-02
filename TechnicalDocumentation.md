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
    string NewtonsPolynomial;

public:
    void processInput(vector<Point>&); // This function is responsible for initialisation of the data structures used in the entire interpolation process
    
    void calculateValue(double x, int method); // This function implements the main user interface to predict the interpolated value for any input via the specified interpolation method

    void NewtonPolynomial(void); // Prints the Newtons Polynomial calculted during initialisation
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

**Working**: 




## Interpolator Initialisation 


## User Input Processing


### Piecewise Constant Interpolation Implementation

### Nearest Neighbor Interpolation Implementation

### Linear Interpolation Implementation

### Newton’s Divided Difference Interpolation Implementation

### Lagrange Interpolation Implementation


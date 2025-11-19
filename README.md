#include "triangle.h"
#include <iostream>

int main() {
    Triangle t1(3, 4, 5), t2(5, 5, 5);

    std::cout << "First triangle: " << t1 << std::endl;
    std::cout << "Second triangle: " << t2 << std::endl;

    std::cout << "Sum of perimeters: " << t1 + t2 << std::endl;

    if (t1 == t2)
        std::cout << "Triangles have equal areas" << std::endl;
    else
        std::cout << "Triangles have different areas" << std::endl;

    return 0;
}

#include "triangle.h"
#include <iostream>
#include <cmath>

#ifndef M_PI
#define M_PI 3.14159265358979323846
#endif

Triangle::Triangle(double sideA, double sideB, double sideC)
    : a(sideA), b(sideB), c(sideC) {
}

double Triangle::Perimeter() const {
    return a + b + c;
}

double Triangle::Area() const {
    double p = Perimeter() / 2.0;
    return sqrt(p * (p - a) * (p - b) * (p - c));
}

double Triangle::operator+(const Triangle& other) const {
    return this->Perimeter() + other.Perimeter();
}

bool Triangle::operator==(const Triangle& other) const {
    return fabs(this->Area() - other.Area()) < 1e-6;
}

std::ostream& operator<<(std::ostream& os, const Triangle& triangle) {
    os << "Triangle: a=" << triangle.a << ", b=" << triangle.b << ", c=" << triangle.c;
    return os;
}

std::istream& operator>>(std::istream& is, Triangle& triangle) {
    is >> triangle.a >> triangle.b >> triangle.c;
    return is;
}

#ifndef TRIANGLE_H
#define TRIANGLE_H

#include <iostream>
#include <cmath>

class Triangle {
private:
    double a, b, c;

public:
    Triangle(double sideA = 0, double sideB = 0, double sideC = 0);
    double Perimeter() const;
    double Area() const;

    // Перевантаження операцій
    double operator+(const Triangle& other) const;
    bool operator==(const Triangle& other) const;
    friend std::ostream& operator<<(std::ostream& os, const Triangle& triangle);
    friend std::istream& operator>>(std::istream& is, Triangle& triangle);
};

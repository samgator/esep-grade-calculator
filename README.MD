# ESEP Grade Calculator

A lightweight Go library for calculating weighted course grades across assignments, exams, and essays.

## Prerequisites

- **Go**: 1.24+

## Project Structure

- `grade-calculator/`: Contains the Go module (`esep/grade-calculator`), source code, and tests.

## Usage

```go
package main

import (
	"fmt"
	esep "esep/grade-calculator"
)

func main() {
	gc := esep.NewGradeCalculator()

	// Add grades (name, score, gradeType)
	gc.AddGrade("Assignment 1", 95, esep.Assignment)
	gc.AddGrade("Midterm Exam", 88, esep.Exam)
	gc.AddGrade("Final Essay", 92, esep.Essay)

	// Calculate letter grade
	finalGrade := gc.GetFinalGrade()
	fmt.Println("Final Grade:", finalGrade)
}
```

### Grade Categories & Weights

| Category | Weight | Type Constant |
| :--- | :--- | :--- |
| Assignments | 50% | `Assignment` |
| Exams | 35% | `Exam` |
| Essays | 15% | `Essay` |

### Grading Scale

- **A**: 90+
- **B**: 80–89
- **C**: 70–79
- **D**: 60–69
- **F**: < 60

## Running Tests

From the repository root, enter the `grade-calculator/` directory:

```bash
cd grade-calculator
go test -v ./...
```

### Code Coverage

Generate and inspect test coverage:

```bash
cd grade-calculator
go test -coverprofile=coverage.txt ./...
go tool cover -func=coverage.txt
```

View HTML coverage report:

```bash
go tool cover -html=coverage.txt
```

## Notes

- **Empty Categories**: At least one grade must currently be provided for each category to prevent division by zero in `computeAverage`.
- **Known Implementation Issues**: `computeAverage` currently sums slice indices instead of values, and `calculateNumericalGrade` references exams for essays.

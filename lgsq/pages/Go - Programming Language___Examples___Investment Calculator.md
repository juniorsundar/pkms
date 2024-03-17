- ```gomod
  module example.com/investment-calculator
  
  go 1.21.6
  ```
- ```go
  package main
  
  import (
  	"fmt"
  	"math"
  )
  
  const inflationRate float64 = 2.5
  
  func main() {
  	//! ====Go can automatically infer the type.====
  	// investmentAmount := 1000
  
  	//! ====It is also possible to declare a type.====
  	// var investmentAmount float64 = 1000
  
  	//! ====Instatiate the variable and can edit it later====
  	var investmentAmount float64
  
  	//! ====It is possible to declare multiple variables in one go====
  	// var investmentAmount, years float64 = 1000, 10
  	// investmentAmount, years := 1000.0, 10.0
  	// investmentAmount, years, expectedReturnRate := 1000.0, 10.0, 5.5
  
  	//! ====In some cases it is also possible to define variables of different types====
  	// var investmentAmount, years = 1000, "10"
  
  	var expectedReturnRate float64 = 5.5
  
  	// float64 := 10
  	var years float64 = 10
  
  	//! ====Constants can be declared with const keyword====
  	// const inflationRate float64 = 2.5
  
  	fmt.Print("Investment Amount: ")
  	//! ====Need to pass pointers for fmt.Scan====
  	fmt.Scan(&investmentAmount)
  
  	// fmt.Print("Expected Return Rate: ")
  	outputText("Expected Return Rate: ")
  	fmt.Scan(&expectedReturnRate)
  
  	fmt.Print("Investment Horizon: ")
  	fmt.Scan(&years)
  
  	// ====Can convert variables between data types with a wrap float64() or int()====
  	// futureValue := float64(investmentAmount) * math.Pow(1+expectedReturnRate/100, float64(years))
  	// var futureValue float64 = investmentAmount * math.Pow(1+expectedReturnRate/100, years)
  	// var futureRealValue float64 = futureValue / math.Pow(1+inflationRate/100, years)
  
  	//! ====Use function to calculate future values instead====
  	futureValue, futureRealValue := calculateFutureValues(investmentAmount, expectedReturnRate, years)
  
  	// ====Different ways to print statements====
  	// fmt.Println("Future value before inflation:", futureValue)
  	// fmt.Println("Future value after inflation:", futureRealValue)
  	// fmt.Printf("Future Value: %v\nFuture Value after Inflation: %v\n", futureValue, futureRealValue)
  	// fmt.Printf("Future Value: %.0f\nFuture Value after Inflation: %.1f\n", futureValue, futureRealValue) //0.xf (where x is d.p.)
  
  	formattedFV := fmt.Sprintf("Future Value: %.0f\n", futureValue)
  	formattedRFV := fmt.Sprintf("Future Value after Inflation: %.1f\n", futureRealValue)
  	fmt.Print(formattedFV, formattedRFV)
  	// fmt.Printf(`Future Value: %.0f
  	// Future Value after Inflation: %.1f`, futureValue, futureRealValue)
  }
  
  func outputText(text string) {
  	fmt.Print(text)
  }
  
  // func calculateFutureValues(investmentAmount float64, expectedReturnRate float64, years float64) (float64, float64) {
  // 	fv := investmentAmount * math.Pow(1+expectedReturnRate/100, years)
  // 	rfv := fv / math.Pow(1+inflationRate/100, years)
  // 	return fv, rfv
  // }
  
  // ====Another way to define functions with outputs====
  func calculateFutureValues(investmentAmount float64, expectedReturnRate float64, years float64) (fv float64, rfv float64) {
  	fv = investmentAmount * math.Pow(1+expectedReturnRate/100, years)
  	rfv = fv / math.Pow(1+inflationRate/100, years)
  	return
  }
  ```
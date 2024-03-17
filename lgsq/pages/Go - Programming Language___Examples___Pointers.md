- ```gomod
  module example.com/pointers
  
  go 1.22.0
  ```
- ```go
  package main
  
  import "fmt"
  
  func main() {
  	age := 32 //! regular variable
  
  	var agePointer *int
  	agePointer = &age //! pointer variable
  
  	fmt.Println("Age:", *agePointer)
  
  	// adultYears := getAdultYears(agePointer)
  	// adultYears := getAdultYears(age)
  	// fmt.Println("Adult years:", adultYears)
  
  	editAgeToAdultYears(agePointer)
  	fmt.Println("Adult years:", age)
  }
  
  func editAgeToAdultYears(age *int) {
  	*age = *age - 18
  }
  
  func getAdultYears(age *int) int {
      // ====cannot perform pointer arithmetic in Go====
      return *age - 18
  }
  
  // func getAdultYears(age int) int {
  //     return age - 18
  // }
  ```
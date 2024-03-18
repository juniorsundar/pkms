- ```gomod
  // go.mod
  module example.com/bank
  
  go 1.22.0
  
  require github.com/Pallinder/go-randomdata v1.2.0
  ```
- ```go
  // bank.go
  package main
  
  import (
  	"fmt"
      "example.com/bank/fileops"
      "github.com/Pallinder/go-randomdata"
  )
  
  const accountBalanceFile string = "balance.txt"
  
  func main() {
  	accountBalance, err := fileops.GetFloatFromFile(accountBalanceFile)
  	if err != nil {
  		fmt.Println("Error:", err)
  		fmt.Println("Continuing with default balance of $1000.00")
  	}
  
  	fmt.Println("Welcome to Go Bank!")
      fmt.Println("Reach us 24/7 at", randomdata.PhoneNumber())
  
  	for {
  		fmt.Println("=====================")
  
  		// ====Can call function from the other file since====
  		// ====both files belong to same main package====
  		presentOption()
  
  		var choice int
  		fmt.Print("Select Option: ")
  		fmt.Scan(&choice)
  		fmt.Println("You Chose: ", choice)
  
  		if choice == 1 {
  			fmt.Printf("Your balance is $%.2f\n", accountBalance)
  		} else if choice == 2 {
  			fmt.Print("Enter amount to deposit: ")
  			var depositAmount float64
  			fmt.Scan(&depositAmount)
  
  			if depositAmount <= 0 {
  				fmt.Println("Invalid amount. Amount must be greater than 0.")
  				continue
  			}
  
  			accountBalance += depositAmount
  			fmt.Printf("Your new balance is $%.2f\n", accountBalance)
  			fileops.WriteFloatToFile(accountBalance, accountBalanceFile)
  		} else if choice == 3 {
  			fmt.Print("Enter amount to withdraw: ")
  			var withdrawAmount float64
  			fmt.Scan(&withdrawAmount)
  
  			if withdrawAmount <= 0 {
  				fmt.Println("Invalid amount. Amount must be greater than 0.")
  				continue
  			}
  			if withdrawAmount > accountBalance {
  				fmt.Println("Insufficient funds.")
  				continue
  			}
  
  			accountBalance -= withdrawAmount
  			fmt.Printf("Your new balance is $%.2f\n", accountBalance)
  			fileops.WriteFloatToFile(accountBalance, accountBalanceFile)
  		} else {
  			fmt.Println("Exiting...")
  			break
  		}
  	}
  }
  ```
- ```go
  // communication.go
  package main // Assign to the same package
  
  import "fmt"
  
  func presentOption () {
      fmt.Println("What do you want to do?")
      fmt.Println("1. Check Balance")
      fmt.Println("2. Deposit Money")
      fmt.Println("3. Withdraw Money")
      fmt.Println("4. Exit")
  }
  ```
- ```go
  // fileops/filerw.go
  package fileops
  
  import (
  	"errors"
  	"fmt"
  	"os"
  	"strconv"
  )
  
  // ====Only variables and functions with capital letters can be exported====
  func WriteFloatToFile(float float64, fileName string) {
  	var floatText string = fmt.Sprint(float)
  	os.WriteFile(fileName, []byte(floatText), 0644) // 0644 = read and write
  }
  
  func GetFloatFromFile(fileName string) (float64, error) {
  	data, err := os.ReadFile(fileName)
  	if err != nil {
  		return 1000, errors.New("Failed to find/read file.")
  	}
  
  	var floatText string = string(data)
  	float, err := strconv.ParseFloat(floatText, 64)
  	if err != nil {
  		return 1000, errors.New("Failed to parse float.")
  	}
  
  	return float, nil
  }
  ```
- ```gomod
  module example.com/bank
  
  go 1.21.6
  ```
- ```go
  package main
  
  import (
  	"errors"
  	"fmt"
  	"os"
  	"strconv"
  )
  
  const accountBalanceFile string = "balance.txt"
  
  func writeBalanceToFile(balance float64) {
  	var balanceText string = fmt.Sprint(balance)
  	os.WriteFile(accountBalanceFile, []byte(balanceText), 0644) // 0644 = read and write
  }
  
  func getBalanceFromFile() (float64, error) {
  	data, err := os.ReadFile(accountBalanceFile)
  	if err != nil {
  		return 1000, errors.New("Failed to find/read file.")
  	}
  
  	var balanceText string = string(data)
  	balance, err := strconv.ParseFloat(balanceText, 64)
  	if err != nil {
  		return 1000, errors.New("Failed to parse balance.")
  	}
  
  	return balance, nil
  }
  
  func main() {
  	accountBalance, err := getBalanceFromFile()
  	if err != nil {
  		fmt.Println("Error:", err)
          // panic("Cannot continue, sorry.")
          fmt.Println("Continuing with default balance of $1000.00")
  	}
  
  	fmt.Println("Welcome to Go Bank!")
  
  	// for i := 0; i < 2; i++ {
  	for {
  		fmt.Println("=====================")
  
  		fmt.Println("What do you want to do?")
  		fmt.Println("1. Check Balance")
  		fmt.Println("2. Deposit Money")
  		fmt.Println("3. Withdraw Money")
  		fmt.Println("4. Exit")
  
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
  			writeBalanceToFile(accountBalance)
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
  			writeBalanceToFile(accountBalance)
  		} else {
  			fmt.Println("Exiting...")
  			break
  		}
  
  		//! ====In Go, the break statement cannot exit the loop from inside a switch statement====
  		//! ====this is because the break statement simply breaks the switch statement====
  		// switch choice {
  		// case 1:
  		// 	fmt.Printf("Your balance is $%.2f\n", accountBalance)
  		// case 2:
  		// 	fmt.Print("Enter amount to deposit: ")
  		// 	var depositAmount float64
  		// 	fmt.Scan(&depositAmount)
  		//
  		// 	if depositAmount <= 0 {
  		// 		fmt.Println("Invalid amount. Amount must be greater than 0.")
  		// 		continue
  		// 	}
  		//
  		// 	accountBalance += depositAmount
  		// 	fmt.Printf("Your new balance is $%.2f\n", accountBalance)
  		// case 3:
  		// 	fmt.Print("Enter amount to withdraw: ")
  		// 	var withdrawAmount float64
  		// 	fmt.Scan(&withdrawAmount)
  		//
  		// 	if withdrawAmount <= 0 {
  		// 		fmt.Println("Invalid amount. Amount must be greater than 0.")
  		// 		continue
  		// 	}
  		// 	if withdrawAmount > accountBalance {
  		// 		fmt.Println("Insufficient funds.")
  		// 		continue
  		// 	}
  		//
  		// 	accountBalance -= withdrawAmount
  		// 	fmt.Printf("Your new balance is $%.2f\n", accountBalance)
  		// default:
  		// 	fmt.Println("Exiting...")
  		// 	return
  		// }
  	}
  }
  ```
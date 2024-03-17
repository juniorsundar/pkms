- ```gomod
  // go.mod
  module example.com/structs
  
  go 1.22.0
  ```
- ```go
  // structs.go
  package main
  
  import (
  	"fmt"
  
  	"example.com/structs/user"
  )
  
  
  func main() {
  	firstName := getUserData("Please enter your first name: ")
  	lastName := getUserData("Please enter your last name: ")
  	birthDate := getUserData("Please enter your birthdate (MM/DD/YYYY): ")
  
  	// var appUser User = User{firstName, lastName, birthDate, time.Now()}
  	// appUser := User{firstName, lastName, birthdate, time.Now()}
  	// appUser = User{
  	//     firstName: firstName,
  	//     lastName: lastName,
  	//     birthdate: birthdate,
  	//     createdAt: time.Now(),
  	// }
  	// var appUser User = newUser(firstName, lastName, birthDate)
  	// var appUser *User = newUser(firstName, lastName, birthDate)
  	// appUser, err := newUser(firstName, lastName, birthDate)
  	appUser, err := user.New(firstName, lastName, birthDate)
  
      if err != nil {
          panic(err)
      }
  
      admin := user.NewAdmin("test@example.come", "admin")
      // ====If you use anonymous embedding, you can access the fields and methods directly====
      // admin.User.OutputUserDetail()
      admin.OutputUserDetail()
      admin.ClearUserName()
      admin.OutputUserDetail()
  
  	// fmt.Println(appUser)
  	// outputUserDetail(&appUser)
  	appUser.OutputUserDetail()
  	appUser.ClearUserName()
  	appUser.OutputUserDetail()
  }
  
  // func outputUserDetail(user *User) {
  //     // ====Standard method is as follow. But Go has shortcut so can access the====
  //     // ====fields directly====
  //
  //     // fmt.Println((*user).firstName, (*user).lastName, (*user).birthDate)
  //     fmt.Println(user.firstName, user.lastName, user.birthDate)
  // }
  
  func getUserData(promptText string) string {
  	fmt.Print(promptText)
  	var value string
      // ====Scanln runs until carriage return hit====
  	fmt.Scanln(&value)
  	return value
  }
  ```
- ```go
  // user/user.go
  package user
  
  import (
  	"errors"
  	"fmt"
  	"time"
  )
  
  type User struct {
  	firstName string
  	lastName  string
  	birthDate string
  	createdAt time.Time
  }
  
  type Admin struct {
      email string
      password string
      // user User
      // ====or call anonymously====
      User
  }
  
  func NewAdmin(email, password string) Admin {
      return Admin{
          email: email,
          password: password,
          User: User{
              firstName: "ADMIN",
              lastName: "ADMIN",
              birthDate: "---",
              createdAt: time.Now(),
          },
      }
  }
  
  // ====Creating struct methods====
  // func (user User) outputUserDetail() {
  func (user User) OutputUserDetail() {
  	// ====the (user User) above is a "Receiver" argument====
  	fmt.Println(user.firstName, user.lastName, user.birthDate)
  }
  
  // ====Function that changes data in a struct====
  // ====it needs to take in the receiver as a pointer====
  //
  //	func (user User) clearUserName() {
  //	    user.firstName = ""
  //	    user.lastName = ""
  //	}
  // func (user *User) clearUserName() {
  func (user *User) ClearUserName() {
  	user.firstName = ""
  	user.lastName = ""
  }
  
  // ====Creator or Constructor aren't feature of go====
  // ====just a convention====
  //
  //	func newUser(firstName, lastName, birthDate string) User {
  //		return User{
  //	        firstName: firstName,
  //	        lastName:  lastName,
  //	        birthDate: birthDate,
  //	        createdAt: time.Now(),
  //	    }
  //	}
  // func newUser(firstName, lastName, birthDate string) (*User, error) {
  // func NewUser(firstName, lastName, birthDate string) (*User, error) {
  func New(firstName, lastName, birthDate string) (*User, error) {
  	if firstName == "" || lastName == "" || birthDate == "" {
  		return nil, errors.New("First Name, Last Name and Birth Date are required")
  	}
  
  	return &User{
  		firstName: firstName,
  		lastName:  lastName,
  		birthDate: birthDate,
  		createdAt: time.Now(),
  	}, nil
  }
  ```
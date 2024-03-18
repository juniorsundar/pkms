- ```gomod
  // go.mod
  module example.com/note
  
  go 1.22.0
  ```
- ```go
  // main.go
  package main
  
  import (
  	"bufio"
  	"fmt"
  	"os"
  	"strings"
  
  	"example.com/note/note"
  )
  
  func main() {
  	title, content := getNoteData()
  
  	note, err := note.New(title, content)
  	if err != nil {
  		fmt.Println("Error:", err)
          return
  	}
  
  	note.Display()
      result := note.Save()
      if result != nil {
          panic("Error saving note.")
      }
  
      println("Note saved successfully!")
  }
  
  func getNoteData() (string, string) {
  	title := getUserInput("Note title: ")
  	content := getUserInput("Note content: ")
  	return title, content
  }
  
  func getUserInput(prompt string) string {
  	fmt.Print(prompt)
  
  	// var value string
  	// ====Scanln only works for single word inputs====
  	// fmt.Scanln(&value)
  
  	reader := bufio.NewReader(os.Stdin)
  	text, err := reader.ReadString('\n') //! Read until this. We are using single quote as it refers to a byte type
  	if err != nil {
  		return ""
  	}
  
  	text = strings.TrimSuffix(text, "\n")
  	text = strings.TrimSuffix(text, "\r") //! For windows users
  	return text
  }
  ```
- ```go
  package note
  
  import (
  	"encoding/json"
  	"errors"
  	"fmt"
  	"os"
  	"strings"
  	"time"
  )
  
  type Note struct {
  	Title     string `json:"title"`
  	Content   string `json:"content"`
  	CreatedAt time.Time `json:"created_at"`
  }
  
  func New(title, content string) (Note, error) {
  	if title == "" || content == "" {
  		return Note{}, errors.New("Invalid input.")
  	}
  
  	return Note{
  		Title:     title,
  		Content:   content,
  		CreatedAt: time.Now(),
  	}, nil
  }
  
  func (note Note) Display() {
      fmt.Println("Your note titled:", note.Title, "was created at", note.CreatedAt)
      fmt.Println("Contains: ", note.Content)
  }
  
  func (note Note) Save() (error) {
      fileName := strings.ReplaceAll(note.Title, " ", "_")
      fileName = strings.ToLower(fileName) + ".json"
      
      json, err := json.Marshal(note) //! Only works on structs with all fields public
      if err != nil {
          return err
      }
  
      return os.WriteFile(fileName, json, 0644)
  }
  ```
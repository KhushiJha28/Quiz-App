# Quiz-App
import random
dbms_questions = [
    {"question": "Which of the following relational algebra operations do not require the participatingtables to be union-compatible?", "options": ["Union", "Difference", "Join"], "answer": "Join"},
    {"question": "Relational algebra does not have?", "options": ["Selection Operator", "Aggregation Operator", "Projection Operator"],
     "answer": "Aggregation Operator"},
    {"question": "What do you mean by one to many relationships?", "options": ["Many classes may have many teachers", "One teacher can have many classes", "One class may have many teachers"],
     "answer": "One teacher can have many classes"},
    
]

python_questions = [
    {"question": "Who developed the Python language?", "options": ["Zim Den", "Guido van Rossum", "Niene Stom"],
     "answer": "Guido van Rossum"},
    {"question": " In which year was the Python language developed?", "options": ["1989", "1972", "1980"], "answer": "1989"},
    {"question": "In which language is Python written?", "options": ["C", "PHP", "English"],
     "answer": "C"},
    ]

dsa_questions = [
    {"question": "Which of the following highly uses the concept of an array?", "options": ["Binary Search tree", "Spatial locality", "Caching"], "answer": "Spatial locality"},
    {"question": "Which one of the following is the size of int arr[9] assuming that int is of 4 bytes?", "options": ["9", "36", "40"], "answer": "36"},
    {"question": "Which one of the following is the process of inserting an element in the stack?",
     "options": ["Push", "Add", "Insert"], "answer": "Push"},
    
]

users_db = {}
def register():
    print("\n--- Registration ---")
    username = input("Enter a new username: ")
    if username in users_db:
        print("Username already exists. Try logging in or choose another username.")
    else:
        password = input("Enter a new password: ")
        users_db[username] = password
        print("Registration successful!")
def login():
    print("\n--- Login ---")
    username = input("Enter username: ")
    password = input("Enter password: ")
    if username in users_db and users_db[username] == password:
        print("Login successful!")
        return True
    else:
        print("Invalid username or password.")
        return False
def choose_quiz():
    print("\n--- Choose Quiz ---")
    print("1. dbms")
    print("2. python")
    print("3. dsa")

    choice = input("Enter your choice (1/2/3): ")
    if choice == '1':
        return dbms_questions
    elif choice == '2':
        return python_questions
    elif choice == '3':
        return dsa_questions
    else:
        print("Invalid choice. Please select again.")
        return choose_quiz()
def conduct_quiz(questions):
    print("\n--- Quiz Started ---")
    selected_questions = random.sample(questions, 3)
    score = 0

    index = 1
    for i in selected_questions:
        print(f"\nQ{index}. {i['question']}")

        option_index = 1
        for option in i['options']:
            print(f"{option_index}. {option}")
            option_index += 1

        answer = input("Enter your answer (1/2/3): ")
        if i['options'][int(answer) - 1] == i['answer']:
            score += 1
        index += 1

    print(f"\nQuiz Completed! Your score is {score}/3.")
    return score
def main():
    while True:
        print("\n--- Welcome to the Quiz App ---")
        print("1. Register")
        print("2. Login")
        print("3. Exit")
        option = input("Enter your choice: ")

        if option == '1':
            register()
        elif option == '2':
            if login():
                while True:
                    questions = choose_quiz()
                    conduct_quiz(questions)
                    again = input("\nDo you want to attempt again? (yes/no): ")
                    if again.lower() != 'yes':
                        break
            else:
                print("Login failed. Try again.")
        elif option == '3':
            print("Exiting the quiz app. Goodbye!")
            break
        else:
            print("Invalid option. Please select again.")
if __name__ == "__main__":
    main()

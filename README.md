# My-Small-Projects

# Login-and-Registration-System
# 🔐 Login & Registration System — C++

A file-based **Login and Registration System** built in C++ using **Object-Oriented Programming (OOP)** concepts. This project demonstrates real-world use of classes, file handling, input validation, and basic password encryption.

---

## 📌 Features

- ✅ **User Registration** — Register with a unique username and password
- ✅ **Duplicate Username Detection** — Prevents registering the same username twice
- ✅ **Input Validation** — Checks for empty fields and minimum length requirements
- ✅ **Password Encryption** — Caesar Cipher (+3 ASCII shift) to secure passwords
- ✅ **File Storage** — All credentials stored persistently in `Data.txt`
- ✅ **User Login** — Verifies identity by matching encrypted credentials from file
- ✅ **Interactive Menu** — Continuous while loop menu for smooth user experience
- ✅ **Success & Error Messages** — Clear feedback for every action

---

## 🛠️ Concepts Used

| Concept | Usage |
|---|---|
| Classes & Objects | `Login_and_Registration_System` class |
| File Handling | `ifstream`, `ofstream`, `ios::app` |
| String Manipulation | `find()`, `length()`, `empty()`, `substr()` |
| Encryption | Caesar Cipher — ASCII +3 shift |
| Input Validation | Empty check, minimum length check |
| Control Flow | `while loop`, `switch-case` |

---

## 📂 Project Structure

```
📁 Login-Registration-System
├── main.cpp       → Main source code
└── Data.txt       → Auto-generated file storing user credentials
```

---

## ⚙️ How It Works

### Registration Flow
```
Enter Username & Password
        ↓
   Validate Input
  (empty? too short?)
        ↓
  Search for Duplicate
   Username in File
        ↓
  Encrypt Password
  (Caesar Cipher +3)
        ↓
  Save to Data.txt ✅
```

### Login Flow
```
Enter Username & Password
        ↓
   Validate Input
        ↓
  Encrypt Input Password
        ↓
  Match with File Records
        ↓
  Login Success ✅ or
  Invalid Credentials ❌
```

---

## 🔐 Encryption Example

| Plain Password | Encrypted (stored in file) |
|---|---|
| `1234` | `4567` |
| `abcd` | `defg` |
| `pass` | `sdvv` |

Each character's ASCII value is shifted by **+3** before saving. During login, the same shift is applied to the input and then compared — so the plain password is **never stored directly**.

---

## 💻 How to Run

```bash
# Compile
g++ main.cpp -o program

# Run
./program        # Linux/Mac
program.exe      # Windows
```

---

## 📋 Menu Options

```
===== Menu =====
1) Registration
2) Login
3) Exit
```

---

## 🧪 Sample Output

```
===== Menu =====
1) Registration
2) Login
3) Exit
Enter Your Choice : 1
Enter Username : UbaidUllah
Enter Password : 1234
User Registered Successfully!

Enter Your Choice : 2
Enter Username : UbaidUllah
Enter Password : 1234
Login Successful! Welcome, UbaidUllah!
```

---

## 📖 What I Learned

- How to use **file handling** in C++ (`fstream`)
- How to implement **OOP principles** with classes and member functions
- How to apply **basic encryption** to protect user data
- How to **validate user input** before processing
- How to build a **menu-driven program** using loops and switch-case

---

## 🚀 Future Improvements

- [ ] Add stronger encryption (e.g., hashing)
- [ ] Add password update / delete user feature
- [ ] Add admin panel
- [ ] Store data in structured format (CSV or JSON)

---

## 👨‍💻 Author

**UbaidUllah**
Computer Science Student | C++ & OOP Enthusiast

---

> *"Every bug fixed is a lesson learned."* 💪

# 🎓 CGPA Calculator

A console-based CGPA Calculator built in **C++** that takes course details as input, calculates semester GPA, displays a formatted result, and saves it to a text file.

---

## 📌 Features

- Input number of courses dynamically at runtime
- Enter grade and credit hours for each course
- Converts letter grades to grade points automatically
- Calculates semester GPA and overall CGPA
- Displays formatted results to console
- Saves full report to `GPA_Result.txt`

---

## ⚙️ Concepts Used

| Concept | Where Applied |
|---|---|
| Aggregation | `GPA` class holds a pointer to externally created `Course` objects |
| Dynamic Memory Allocation | `Course` array allocated on heap using `new` at runtime |
| Exception Handling | Input validation, division-by-zero guard, file error handling |
| File Handling | Results saved to `GPA_Result.txt` using `ofstream` |

---

## 🏗️ Class Design

### `Course` (Data Class)
Stores three fields per course:
- `Credit_Hours` — number of credit hours
- `Grade` — letter grade entered by user (e.g. `A+`, `B-`, `C`)
- `Grade_Points` — numeric value converted from the letter grade

### `GPA` (Logic Class)
Handles input, calculation, display, and file saving.

> `GPA` **has-a** `Course` → This is **Aggregation**

The `GPA` class receives a pointer to an externally created `Course` array. It does not create or destroy the array — ownership stays in `main()`. This distinguishes aggregation from composition.

---

## 🧠 Logic / Approach

1. Ask the user how many courses they have
2. Dynamically allocate a `Course` array on the heap (`new Course[n]`)
3. Pass the array into the `GPA` class — establishing the aggregation relationship
4. Loop through each course and collect credit hours and grade via `Input()`
5. Convert the letter grade to grade points using `Grade_to_Points()`
6. Calculate GPA as: `Total Weighted Grade Points ÷ Total Credit Hours`
7. Display results to console via `Display()`
8. Save results to `GPA_Result.txt` via `Save_To_File()`
9. Free heap memory using `delete[]`

---

## 🔒 Exception Handling

**Credit Hours Validation**
- `cin.fail()` triggers `invalid_argument` on non-numeric input
- Zero or negative values throw another `invalid_argument`
- `cin.clear()` and `cin.ignore()` reset the input buffer before retrying

**Grade Validation**
- `Grade_to_Points()` throws `invalid_argument` on unrecognized grade
- Calling loop catches it and re-prompts with valid grade list

**Division by Zero Guard**
- `GPA_Calculation()` throws `runtime_error` if total credit hours equals zero

**File Error Guard**
- `Save_To_File()` throws `runtime_error` if output file cannot be created

**Memory Allocation Failure**
- `main()` catches `bad_alloc` in case `new` fails due to insufficient heap memory

---

## 💾 Dynamic Memory Allocation

```cpp
courses = new Course[n];   // Heap allocation — size known only at runtime
// ... work done ...
delete[] courses;           // Memory freed — prevents memory leaks
```

A static array like `Course courses[5]` can't be used here because `n` is only known after user input. `delete[]` is called in all exit paths including catch blocks.

---

## 🔡 Supported Grades

| Grade | Points |
|---|---|
| A+ / A | 4.0 |
| A- | 3.7 |
| B+ | 3.3 |
| B | 3.0 |
| B- | 2.7 |
| C+ | 2.3 |
| C | 2.0 |
| D | 1.0 |
| F | 0.0 |

> Grades are case-insensitive — `b+` and `B+` are both accepted.

---

## 🖥️ How to Run

```bash
# Compile
g++ -o cgpa_calculator main.cpp

# Run
./cgpa_calculator
```

Output will be displayed in the console and saved to `GPA_Result.txt` in the same directory.

---

## 📂 Output File Sample

```
==========================================
              GPA CALCULATOR
==========================================

Course Details
------------------------------------------

Course: 1
Credit Hours: 3
Grade: A
Grade Point: 4.00

Course: 2
Credit Hours: 2
Grade: B+
Grade Point: 3.30

==========================================
                 Result
==========================================
Total Credit Hours: 5
Total Grade Points: 18.60
Semester GPA: 3.72
Total CGPA: 3.72
```

---

## 🛠️ Tech Stack

- **Language:** C++
- **Compiler:** G++ (C++11 or later)
- **Libraries:** `iostream`, `fstream`, `stdexcept`, `iomanip`, `limits`, `string`

Sure! Here is a more vibrant and emoji-filled version of the text formatted as a publication.

---

# Lexical Analyzer in C Using Lex/Flex 📚✨

## **Introduction** 🚀
The provided code is a simple lexical analyzer implemented using **Lex** (also known as **Flex**), a tool for generating scanners (or lexers) from regular expressions. This scanner recognizes different types of tokens such as keywords, identifiers, operators, strings, numbers, and comments from C code. 🖥️🔍

The goal of this lexical analyzer is to read input source code and categorize each part of it (or token) into predefined types such as keywords, operators, strings, etc. These types are then displayed to the user in a neat format. 🎯💻

## **Understanding the Lexical Analyzer** 🧐

### **Lexical Analysis** 📝
Lexical analysis is the first phase of a compiler or interpreter 🧑‍💻. The main task here is to split the input stream (which is typically source code) into meaningful chunks called **tokens**. Each token represents a logical unit in the source code, such as a keyword, operator, or variable. ⚙️

### **Lex Tool** 🛠️
- **Lex** is a program that generates lexical analyzers (scanners) from regular expressions. It’s used to define the structure of the tokens and the actions to take when each token is encountered.
- **Flex** is a faster, free implementation of **Lex**, but the syntax remains the same. ⚡

### **Regular Expressions** 🔎
Regular expressions (regex) are patterns that define how a token should be recognized. In the lexical analyzer, these patterns describe keywords, operators, strings, and other token types. For example:
- Keywords are matched using patterns like `"int"|"char"|"if"`.
- Numbers are matched with patterns like `[0-9]+(\.[0-9]+)?` for integers and floats. 💡

### **Actions** 🖱️
In Lex/Flex, actions are written in C code and specify what should happen when a token is matched. These actions typically involve printing the token's value and its category (e.g., keyword, operator, etc.). For example, when a keyword is matched, the action might be `{ display(0); }`. 🖨️

---

## **Step-by-Step Implementation** 🛠️🚀

### **1. Define Tokens Using Regular Expressions** 🔐

Tokens are defined using regular expressions, and these are categorized into the following types: 

1. **Keyword**: Reserved words such as `int`, `char`, `void`, `if`, etc. 🗝️
2. **Reserved**: Special reserved identifiers like `main`, `printf`, etc. 📝
3. **Comments**: Single-line (`//`) and multi-line (`/*...*/`) comments. 💬
4. **Operators**: Arithmetic, relational, and assignment operators like `+`, `-`, `=`, etc. ➕➖✖️
5. **Preprocessor**: Preprocessor directives starting with `#`. 🛠️
6. **String**: Strings enclosed in double quotes `"..."`. 💬💻
7. **Identifier**: Variable or function names. 🆔
8. **Number**: Numeric values (integers or floats). 🔢
9. **Invalid literal**: For any unrecognized characters. ⚠️

### **2. Define Actions to Display Token Type** 🎯

Each token has an associated action that is performed when the token is matched. In the provided code, the action is to call the `display()` function, passing an integer representing the token type. 

Example:
- When a keyword is matched, the action looks like `{ display(0); }`, where `0` corresponds to the **"keyword"** category.

### **3. Define the `display()` Function** 💻📊

The `display()` function is responsible for printing the matched token and its category. It uses the `yytext` variable (provided by Lex/Flex) to get the current matched string and the `word[]` array to map the token type to its name.

```c
void display(int n) {
    printf("\n%s --> %s\n", yytext, word[n]);
}
```

### **4. Handle Special Characters (Spaces and Tabs) ✂️**

In Lex/Flex, you can ignore characters such as spaces, tabs, and newlines which don’t contribute to the tokenization process. This is done with empty actions like:

```c
[\n\t' ']          {};   // Ignore spaces and tabs
```

### **5. Handle Unrecognized Characters** ❓

If the lexical analyzer encounters a character that doesn’t match any predefined regular expression, it will fall through to a default action. In this code, the default action is:

```c
.                 { display(5); }  // For any unrecognized characters
```

This action displays the character as an "invalid literal" ⚠️.

### **6. Integrating with `yyin`** 📂

The `yyin` file pointer is used to specify the input file to be analyzed. If a filename is provided as a command-line argument, `yyin` is set to that file, otherwise, it reads from the standard input.

```c
if (argc > 1) {
    yyin = fopen(argv[1], "r");
    if (!yyin) {
        printf("could not open %s \n", argv[1]);
        exit(0);
    }
}
```

### **7. The `yywrap()` Function** 🔄

The `yywrap()` function is required by Lex/Flex and is used to handle the end-of-file (EOF) situation. It returns 1 when there is no more input to process.

```c
int yywrap() {
    return 1;
}
```

### **8. Main Function** 🎬

The `main()` function opens the input file (if provided), invokes `yylex()` to start the lexical analysis, and processes the tokens.

```c
int main(int argc, char **argv) {
    if (argc > 1) {
        yyin = fopen(argv[1], "r");
        if (!yyin) {
            printf("could not open %s \n", argv[1]);
            exit(0);
        }
    }
    yylex();
    return 0;
}
```

---

## **How to Run This Program** 🏃‍♂️💨

### **Step 1: Create the Lex File** 📝
1. Save the provided code into a file named `lexer.l`.

### **Step 2: Generate the C Code Using Flex** ⚡
Use the `flex` command to generate the C code from the Lex file:
```bash
flex lexer.l
```

This will generate a file called `lex.yy.c` containing the C code for the lexical analyzer.

### **Step 3: Compile the C Code** ⚙️
Use a C compiler (like `gcc`) to compile the generated code:
```bash
gcc lex.yy.c -o lexer -lfl
```

### **Step 4: Run the Program** 🏃‍♀️
You can now run the lexical analyzer by passing a C source file as an argument:
```bash
./lexer input.c
```

Where `input.c` is the C code you want to analyze.

---
### **Output**
![image](https://github.com/user-attachments/assets/5ac91fd3-51c7-4036-9d36-07c8e457f34f)

## **Conclusion** 🎉

This simple lexical analyzer reads C source code and classifies tokens into categories like keywords, operators, numbers, and identifiers. It uses regular expressions to define the token patterns and executes corresponding actions when those patterns are matched. This process is an essential part of compiling or interpreting code. 🧑‍💻💡

Feel free to experiment with different input files and explore how the program identifies various parts of C code! 🚀🔍
## **Happy Learning!!**
![image](https://github.com/user-attachments/assets/06194f64-a79e-4544-a22b-58a1f6e754e7)

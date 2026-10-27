# FunWithCPP: Hangman

> **Graduate coursework (2022), archived.** This repo is kept for reference and is not maintained. The last small edit was in September 2023.

FunWithCPP is a Hangman game for the console. The program picks a random animal name from a built-in list of 20, such as `turtle`, `kangaroo` or `hippopotamus`. You guess one lower-case letter at a time and are allowed 5 wrong guesses. After each wrong guess, the program draws more of an ASCII gallows. You win when every letter is revealed. If you run out of guesses, the program shows the word.

## Build

The only source file is `FunWithCPP.cpp`, and it uses only the standard library.

```bash
g++ -std=c++17 FunWithCPP.cpp -o hangman
```

*(not verified: g++ is not installed on the test machine)*

With MSVC, or by opening `FunWithCPP.sln` in Visual Studio:

```bat
cl /std:c++17 /EHsc FunWithCPP.cpp /Fe:hangman.exe
```

**Verified on 2026-10-27:** MSVC 14.51 (`cl /std:c++17 /EHsc /W4`) compiled it successfully. It gave two narrowing-conversion warnings, C4267 and C4244.

## Run

```bash
./hangman
```

Sample start of a game. The word is random, so your output will differ.

```
Your guess word is:------
Enter your guess letter:
e

Yay! You have found the letter
You can have 5 more wrong attempts
Your guess word is:----e-

Enter your guess letter:
a

Whoops! that letter is not present in the word
...
You can have 4 more wrong attempts
```

## Known issues

- `new char[secretWordLength]` allocates one byte too few. `replaceDashes` then writes the `'\0'` terminator one byte past the end of the buffer, which is a heap overflow. The fix is to allocate `length + 1` or use `std::string`.
- On a win, `main` returns before `delete[] guessWord`, so the buffer leaks.
- `rand() % 20` hard-codes the list length.
- Guessing the same wrong letter again costs another try.

Graduate coursework (2022), archived.

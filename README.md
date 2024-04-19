HANGMAN CODE :
import random

def choose_word(): words = ["hangman", "python", "programming", "computer", "game", "code"] return random.choice(words)

def display_word(word, guessed_letters): displayed_word = "" for letter in word: if letter in guessed_letters: displayed_word += letter else: displayed_word += "_" return displayed_word

def hangman(): word = choose_word() guessed_letters = [] incorrect_guesses = 0 max_attempts = 6

print("Welcome to Hangman!")
print("Try to guess the word.")

while True:
    print("\nWord:", display_word(word, guessed_letters))

    guess = input("Enter a letter: ").lower()

    if len(guess) != 1 or not guess.isalpha():
        print("Please enter a single letter.")
        continue

    if guess in guessed_letters:
        print("You already guessed that letter.")
        continue

    guessed_letters.append(guess)

    if guess not in word:
        incorrect_guesses += 1
        print("Incorrect guess.")
        print("Attempts left:", max_attempts - incorrect_guesses)
        if incorrect_guesses >= max_attempts:
            print("Sorry, you lost. The word was:", word)
            break
    else:
        print("Correct guess!")

    if all(letter in guessed_letters for letter in word):
        print("Congratulations! You guessed the word:", word)
        break
hangman()

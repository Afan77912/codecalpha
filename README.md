import random

def choose_word():
    words = ['python', 'hangman', 'programming', 'developer', 'computer', 'algorithm', 'variable', 'function']
    return random.choice(words)

def display_word(word, guessed_letters):
    displayed_word = ''
    for letter in word:
        if letter in guessed_letters:
            displayed_word += letter
        else:
            displayed_word += '_'
    return displayed_word

def hangman():
    print("Welcome to Hangman!")

    word = choose_word()
    guessed_letters = []
    incorrect_guesses = 0
    max_incorrect_guesses = 6

    while incorrect_guesses < max_incorrect_guesses:
        print(f"\nWord: {display_word(word, guessed_letters)}")
        print(f"Incorrect guesses left: {max_incorrect_guesses - incorrect_guesses}")
        guess = input("Guess a letter: ").lower()

        # Check if the input is valid
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            continue

        # Check if the letter was already guessed
        if guess in guessed_letters:
            print("You've already guessed that letter.")
            continue
        
        guessed_letters.append(guess)

        # Check if the guess is in the word
        if guess in word:
            print(f"Good guess! '{guess}' is in the word.")
        else:
            print(f"Oops! '{guess}' is not in the word.")
            incorrect_guesses += 1

        # Check if the player has won
        if all(letter in guessed_letters for letter in word):
            print(f"\nCongratulations! You've guessed the word: {word}")
            break

    if incorrect_guesses == max_incorrect_guesses:
        print(f"\nSorry, you've lost! The word was: {word}")

if __name__ == "__main__":
    hangman()

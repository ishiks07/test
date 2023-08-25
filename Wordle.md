"""NMTAFE ICTPRG302:
#salam ishikura
#11/08/2023
Guess-My-Word Project Application"""
# See the assignment worksheet and journal for further details.
# Begin by completing the TODO items below in the order you specified in the journal

import random

print("Guess My Word is a simple and fun single player puzzle game A player has to guess a mystery 5 letter word.\n"
      "you have 6 attempts.\n"
      "🟩 means the letter is correct and in the right spot.\n"
      "🟨means the letter is correct but in the wrong spot.\n"
      "🟥 means the letter is not in the word.\n"
      "If at any point you want to quit,\n"
      "type i give up\n"
      "GOOD LUCK!!\n")

TARGET_WORDS = './word-bank/target_words.txt'
VALID_WORDS = './word-bank/all_words.txt'
already_guessed = []

TARGET_WORDS
try:
    target_word_file = open(TARGET_WORDS)
except:
    print("No file found")
    quit()

target_word_file = target_word_file.read().split()
target_word = random.choice(target_word_file)

MAX_TRIES = 6
tries = 0

while True:
    guess = input("Enter guess? ").lower()
    if guess == "i give up":
        print(f"The word was, {target_word}")
        break
    try:       
        valid_word_file = open(VALID_WORDS)
    except:
        print("No file found")
        quit()

        valid_word_file = valid_word_file.read().split()
    # do the length
    if len(guess) != 5:
        print("Please enter a 5 letter word.")
        continue
    if guess in valid_word_file:
        print(f"{guess} is a valid word")

    else:
        print(f"{guess} is not a valid word\n"
              f"Try again")
        continue
    if guess in already_guessed:
        print(f"you have already said {guess}\n"
              f"try again")
        continue

    else:
        already_guessed.append(guess)

    if guess == target_word:
        print("Correct guess!")
    else:
        tries += 1
    if tries == MAX_TRIES:
        print(" Game Over\n"
              " The word was,", target_word)
        break
    guess_upper = (guess).upper()
    print(guess_upper)

    score = ["0", "0", "0", "0", "0"]
    count = 0
    guess_list = list(guess)
    target_list = list(target_word)
    for letter in guess_list:
        if letter in target_list:
            if letter == target_list[count]:
                score[count] = "🟩"
            else:
                score[count] = "🟨"
        else:
            score[count] = "🟥"
        count += 1
    print("Your Guess -", score)
    tries_left = MAX_TRIES - tries
    print(f"you have {tries_left} tries left")
    if guess == target_word:
        print("Congrats You got the correct word🕺🏾🕺🏾")
        break

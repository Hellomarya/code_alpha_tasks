#TASK 1
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



#TASK 2
# CodeAlpha_StockPortfolioTacker
import requests

class StockPortfolio:
    def __init__(self):
        self.stocks = {}

    def add_stock(self, symbol, quantity):
        if symbol in self.stocks:
            self.stocks[symbol] += quantity
        else:
            self.stocks[symbol] = quantity

    def remove_stock(self, symbol, quantity):
        if symbol in self.stocks:
            self.stocks[symbol] -= quantity
            if self.stocks[symbol] <= 0:
                del self.stocks[symbol]
        else:
            print("Stock not found in portfolio.")

    def get_portfolio_value(self):
        total_value = 0
        for symbol, quantity in self.stocks.items():
            price = self.get_stock_price(symbol)
            total_value += price * quantity
        return total_value

    def get_stock_price(self, symbol):
        api_key = 'YOUR_API_KEY'
        url = f'https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol={symbol}&apikey={api_key}'
        response = requests.get(url)
        data = response.json()
        if 'Global Quote' in data:
            return float(data['Global Quote']['05. price'])
        else:
            print("Error fetching stock price.")
            return 0

# Example usage
portfolio = StockPortfolio()
portfolio.add_stock('AAPL', 10)
portfolio.add_stock('GOOGL', 5)
print("Portfolio value:", portfolio.get_portfolio_value())


#TASK 3
# CodeAlpha_BasicChatbot
Task 3 Basic Chatbot
import nltk
import random

# Download NLTK data if not already downloaded
nltk.download('punkt')

# Define responses
responses = {
    "hi": ["Hello!", "Hi there!", "Hey!"],
    "how are you": ["I'm good, thanks!", "I'm doing well, how about you?", "All good here!"],
    "bye": ["Goodbye!", "See you later!", "Bye! Have a great day!"]
}

# Function to get a response based on user input
def get_response(message):
    message = message.lower()
    if message in responses:
        return random.choice(responses[message])
    else:
        return "I'm not sure how to respond to that."

# Main loop for chatting
print("Chatbot: Hello! How can I help you?")
while True:
    user_input = input("You: ")
    if user_input.lower() == 'exit':
        print("Chatbot: Goodbye!")
        break
    response = get_response(user_input)
    print("Chatbot:", response)


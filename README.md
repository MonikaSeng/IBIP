import random
from collections import Counter

class RockPaperScissorsAI:
    def __init__(self):
        self.history = []
        self.choices = ['rock', 'paper', 'scissors']

    def simple_ai(self):
        # Random choice - basic AI
        return random.choice(self.choices)

    def pattern_ai(self):
        # Pattern recognition: counter the user's most frequent move
        if not self.history:
            return self.simple_ai()
        counter = Counter(self.history)
        most_common = counter.most_common(1)[0][0]
        # Counter logic: rock->paper, paper->scissors, scissors->rock
        counter_moves = {'rock': 'paper', 'paper': 'scissors', 'scissors': 'rock'}
        return counter_moves[most_common]

    def record(self, user_choice):
        self.history.append(user_choice)


def get_winner(user, computer):
    if user == computer:
        return "Draw"
    wins = {'rock': 'scissors', 'scissors': 'paper', 'paper': 'rock'}
    if wins[user] == computer:
        return "User"
    return "Computer"


def play_game():
    ai = RockPaperScissorsAI()
    print("Welcome to Rock Paper Scissors!")
    print("Type 'rock', 'paper', 'scissors', or 'quit' to exit.")
    rounds = 0
    user_wins = 0
    computer_wins = 0

    while True:
        user_input = input("Your move: ").strip().lower()
        if user_input == 'quit':
            print("Game over!")
            print(f"You won {user_wins} out of {rounds} rounds.")
            break
        if user_input not in ai.choices:
            print("Invalid input! Please enter 'rock', 'paper', or 'scissors'.")
            continue

        # Switch between simple_ai and pattern_ai based on rounds played
        if rounds < 5:
            computer_choice = ai.simple_ai()
        else:
            computer_choice = ai.pattern_ai()

        print(f"Computer chose: {computer_choice}")
        ai.record(user_input)
        winner = get_winner(user_input, computer_choice)
        if winner == "User":
            print("You win this round!")
            user_wins += 1
        elif winner == "Computer":
            print("Computer wins this round!")
            computer_wins += 1
        else:
            print("It's a draw!")
        rounds += 1
        print(f"Score => You: {user_wins}, Computer: {computer_wins}, Draws: {rounds - user_wins - computer_wins}\n")

if __name__ == "__main__":
    play_game()# IBIP
